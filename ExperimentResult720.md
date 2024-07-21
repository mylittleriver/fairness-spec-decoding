## Experiment Result

### Question

The reason for the reduce of toxicity after finetuning the model on random datasets may be that the gpt2 model has inherent biases, so we need to use different models other than gpt2. May consider EleutherAI/gpt-neo-1.3B and EleutherAI/gpt-neo-125M. Also, we need to finetune the main and assistant models on two different datasets, and then finetune them on the same datasets and re-conduct the experiments.

After finetuning the gpt-neo-1.3B and gpt-neo-125M on sst2 and wikitext respectively, and then finetuning the two models on the third dataset imdb, the disparity in terms of n_matches/max new tokens still exist, and the ratio doesn't change much (average ratio for all groups: 0.505 w/o finetuning on imdb, 0.49 w/ finetuning on imdb). In contrast, finetuning gpt2/distillgpt2 on ag_news reduced the disparity and increased the ratio (average ratio: 0.47 w/o finetuning, 0.72 w/ finetuning).



 <center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://github.com/user-attachments/assets/6a1f524c-4c79-400d-8516-06242480b9e5" width = "50%" alt=""/>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://github.com/user-attachments/assets/70d71649-a1f4-42aa-b3f1-58ddee3b3340" width = "50%" alt=""/>
    <br>
    
</center>










