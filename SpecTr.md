## A brief analysis of the differences between the two algorithms

The left shows the algorithm of Speculative decoding, and the right shows the algorithm of SpecTr.

 <center>
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

 -  needs modification to get_candidates() method to return K candidate_ids
- draft selection algorithm: OTM-k and K-SEQ
 - when K=1, it is the original speculative decoding and achieves optimal coupling and optimal acceptance probability (OTM-k)
 - when K>1, provide an approximate solution K-SEQ
   

<div style="text-align: center;">
    <img 
        style="border-radius: 0.3125em; box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);"
        src="https://github.com/user-attachments/assets/331d9d99-5197-40f5-8a7d-7ea0c98862c2" 
        width="18%" 
        alt=""
    />
</div>

 
 

