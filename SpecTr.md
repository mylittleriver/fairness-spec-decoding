## A brief analysis of the differences between the two algorithms

The left shows the algorithm of Speculative decoding, and the right shows the algorithm of SpecTr.

<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/02274570-3e21-4d70-af89-376bd331dc9c" width = "32%" alt=""/>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/80807457-6e11-42a9-bedb-6315b71c96bb" width = "48%" alt=""/>
<br>



The main difference lies in the number of sampled drafts sampled from the small model and the selection algorithm that selects a valid sequence from multiple draft sequences.
- draft construction: construct K sampled drafts sampled from the small model
  - independently sample K draft sequences from the small model
  - add get_k_candidates() method to return K candidate_ids
- draft selection algorithm: OTM-k and K-SEQ
  - when K=1, it is the original speculative decoding and achieves optimal coupling and optimal acceptance probability (OTM-k)
  - when K>1, provide an approximate suboptimal solution K-SEQ 
  - needs modification to _speculative_sampling() method

 K-SEQ:
 
 ![image](https://github.com/user-attachments/assets/c6649c8c-2f46-4b8e-93cb-418c034ea368)

The algorithm output the first accepted sample or result from a residual distribution p<sub>res</sub> if none of the samples is accepted. To guarantee that the final returned token is a valid sample from q, we choose an appropriate ρ ∈ [1, k] and accept Xi with probability min(1, q(Xi)/(ρ · p(Xi))) instead of min(1, q(Xi)/(p(Xi))) as in Speculative Decoding.

How to compute ρ:

![image](https://github.com/user-attachments/assets/152f1be6-1489-4f62-bd24-ce89c6fe919e)


## code implementation

draft construction - get_k_candidates():

'''
def get_k_candidates(input_ids, k):
  candidate_ids_list = []
  candidate_logits_list = []
  for _ in range(k):
    #sample k drafts
  return candidate_ids_list, candidate_logits_list
          
        
    
'''

One question: are the followings contradictory?

optimal transport cost (1 - optimal acceptance probability):
![image](https://github.com/user-attachments/assets/91303dcd-2395-4b96-b997-158e67849439)

acceptance probability:
<div style="text-align: center;">
    <img src="https://github.com/user-attachments/assets/e2484505-4f8d-4531-abc7-2c9c0b6a63c8" width="60%" alt=""/>
</div>
 
 

