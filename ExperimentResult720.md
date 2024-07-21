## Experiment Result

### Question

The reason for the reduce of toxicity after finetuning the model on random datasets may be that the gpt2 model has inherent biases, so we need to use different models other than gpt2. May consider EleutherAI/gpt-neo-1.3B and EleutherAI/gpt-neo-125M. Also, we need to finetune the main and assistant models on two different datasets, and then finetune them on the same datasets and re-conduct the experiments.

After finetuning the gpt-neo-1.3B and gpt-neo-125M on sst2 and wikitext respectively, and then finetuning the two models on the third dataset imdb, the disparity in terms of n_matches/max new tokens still exist, and the ratio doesn't change much (average ratio for all groups: 0.505 w/o finetuning on imdb, 0.49 w/ finetuning on imdb). In contrast, finetuning gpt2/distillgpt2 on ag_news reduced the disparity and increased the ratio (average ratio: 0.47 w/o finetuning, 0.72 w/ finetuning).

 <center>
    <img style="border-radius: 0.3125em;
/*     box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://github.com/user-attachments/assets/0884cefa-6d01-4b6b-9899-78ac64b843ac" width = "45%" alt=""/> */
    <img style="border-radius: 0.3125em;
/*     box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://github.com/user-attachments/assets/cc2019df-4b1e-4d3d-af40-caf3d5306203" width = "45%" alt=""/> */
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999;
    padding: 2px;">
      n_matches/max new tokens after finetuning neo-1.3B/neo-125M on sst2/wikitext respectively (left) and after finetuning the two models on the third dataset imdb (right)
  	</div>
</center>







