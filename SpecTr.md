## A brief analysis of the differences between the two algorithms

The left shows the algorithm of Speculative decoding, and the right shows the algorithm of SpecTr.

<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/02274570-3e21-4d70-af89-376bd331dc9c" width = "32%" alt=""/>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/80807457-6e11-42a9-bedb-6315b71c96bb" width = "48%" alt=""/>
<br>



The main difference lies in the number of sampled drafts (batch size) sampled from the small model and the selection algorithm that selects a valid sequence from multiple draft sequences.
- draft construction: construct K sampled drafts sampled from the small model
  - independently sample K draft sequences from the small model
  - code modification: add get_k_candidates() method to return K candidate_ids
- draft selection algorithm: OTM-k and K-SEQ
  - when K=1, it is the original speculative decoding and achieves optimal coupling and optimal acceptance probability (OTM-k)
  - when K>1, provide an approximate suboptimal solution K-SEQ 
  - code modification: add _speculative_sampling_spectr() method

 K-SEQ:
 
 ![image](https://github.com/user-attachments/assets/c6649c8c-2f46-4b8e-93cb-418c034ea368)

The algorithm output the first accepted sample or result from a residual distribution p<sub>res</sub> if none of the samples is accepted. To guarantee that the final returned token is a valid sample from q, we choose an appropriate ρ ∈ [1, k] and accept Xi with probability min(1, q(Xi)/(ρ · p(Xi))) instead of min(1, q(Xi)/(p(Xi))) as in Speculative Decoding.

How to compute ρ:

![image](https://github.com/user-attachments/assets/152f1be6-1489-4f62-bd24-ce89c6fe919e)

$\beta_{p,q}(\rho)$ is decreasing in $\rho$, so is $1 - (1 - \beta_{p,q}(\rho))^k$.


sequence level selection:

![image](https://github.com/user-attachments/assets/e85d392d-51a5-4f65-a030-413da82a8d96)

### Question raised

If temperature = 0, the K draft tokens would be the same?

## code implementation

draft construction - get_k_candidates():

```
def get_k_candidates(input_ids, k):
  candidate_ids_list = []
  candidate_logits_list = []
  for _ in range(k):
    #sample k drafts
  return candidate_ids_list, candidate_logits_list
```
draft selection - _assisted_decoding_spectr() and _spceulative_sampling_spectr():

```
def _assisted_decoding_spectr(
        self,
        input_ids: torch.LongTensor,
        k: int, # take k as input
        candidate_generator: CandidateGenerator,
        logits_processor: LogitsProcessorList,
        logits_warper: LogitsProcessorList,
        stopping_criteria: StoppingCriteriaList,
        generation_config: GenerationConfig,
        synced_gpus: bool,
        streamer: Optional["BaseStreamer"],
        **model_kwargs,
    )
  # get k samples from get_k_candidates()
  candidate_input_ids_list, candidate_logits_list = candidate_generator.get_k_candidates(input_ids,k)
```

calculate ρ<sup>*</sup>:
```
def beta_pq(rho, p, q):
    return torch.sum(torch.minimum(p/rho , q)).item()

def equation(rho, p, q, k):
    beta = beta_pq(rho, p, q)
    return 1 - (1 - beta)**k - rho * beta

rho_star, = fsolve(equation, initial_guess, args=(p.cpu().numpy(), q.cpu().numpy(), k))
rho_star = max(lower_bound, min(upper_bound, rho_star))
```


### One question: are the followings contradictory?

optimal transport cost (1 - optimal acceptance probability):
![image](https://github.com/user-attachments/assets/91303dcd-2395-4b96-b997-158e67849439)

acceptance probability:
<div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/e2484505-4f8d-4531-abc7-2c9c0b6a63c8" width="60%" alt=""/>
</div>
 
 

