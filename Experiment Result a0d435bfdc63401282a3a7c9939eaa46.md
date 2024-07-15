# Experiment Result

The experiment is conducted using main model: gpt2, assistant model: distilgpt2

## Question
1. Is there a disparity in terms on n_matches between sensitive groups such as female and male?
- **Yes, before finetuning we notice a disparity. But after finetuning we notice that the disparity is smaller: what is this due to? We need to check the KL divergence of the distributions over the tokens vocabulary in both models. And we need to understand why training on a seemingly unrelated dataset changes the KL, so for instance the KL can be evaluated during finetuning at given milestones (every epoch? every training step?)**

	The disparity in terms of n_matches (or ratio of n_matches to max new tokens, which indicates the percentage of tokens coming from the assistant model) is shown below:
	
	without finetuning:
	
	![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled%205.png)
	
	finetuned on ag_news with 1 epoch:
	
	![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled%206.png)

	finetuned on ag_news with 3 epochs:

	<img width="747" alt="image" src="https://github.com/user-attachments/assets/ad040ec9-3a51-4d87-b995-6fc97509fccd">

	
	
	For now, I have finetuned both models on the seemingly unrelated dataset ag_news for 1, 2, 3 epochs using the following parameters and evaluated the mean KL value at these epochs respectively. Compared to without fine-tuning, which had a mean KL divergence value of 4.3072e-06, the values were 4.4415e-06, 4.2127e-06, and 4.1808e-06 at epochs 1, 2, and 3 respectively. This shows an initial increase in the mean KL divergence at epoch 1, followed by a decrease at epochs 2 and 3. 
	
	
	<img width="866" alt="image" src="https://github.com/user-attachments/assets/a2066ffb-e5c1-4103-baff-48348395d671">

	
	fine-tuning parameters:
	
	```python
	batch_size = 8
	num_workers = os.cpu_count()
	max_steps = 5
	bf16 = True
	fp16 = False
	gradient_accumulation_steps = 32
	context_length = 512
	logging_steps = 100
	save_steps = 100
	learning_rate = 0.00005
	num_train_epochs=3
	 ```

	```python
 	training_args = TrainingArguments(
	    output_dir='logs',
	    eval_strategy='steps',
	    weight_decay=0.01,
	    load_best_model_at_end=True,
	    per_device_train_batch_size=batch_size,
	    per_device_eval_batch_size=batch_size,
	    logging_strategy='steps',
	    save_strategy='steps',
	    logging_steps=logging_steps,
	    save_steps=save_steps,
	    save_total_limit=2,
	    bf16=bf16,
	    fp16=fp16,
	    report_to='tensorboard',
	    num_train_epochs=num_train_epochs,
	    dataloader_num_workers=num_workers,
	    gradient_accumulation_steps=gradient_accumulation_steps,
	    learning_rate=learning_rate,
	    lr_scheduler_type='constant',
	)
 	```
 
	
	
	
	
	below is the information during fine-tuning:
	
	main model (gpt2):
	
	<img width="387" alt="image" src="https://github.com/user-attachments/assets/a9a635c8-5325-41fc-a264-073b6d23fc51">

	
	assistant model (distilgpt2):
	
	<img width="388" alt="image" src="https://github.com/user-attachments/assets/29629048-badd-49dd-b4eb-f91204cd3337">

	
	code for generating kl divergence:
	
	```python
	import torch.nn.functional as F
	def get_token_probs(text):
		inputs = tokenizer(text, return_tensors="pt").to(model.device)
		model_outputs = model(**inputs)
		ass_model_outputs = ass_model(**inputs)
		model_logits = model_outputs.logits
		ass_model_logits = ass_model_outputs.logits
		model_token_probs = torch.softmax(model_logits[0, -1, :], dim=0)
		ass_model_token_probs = torch.softmax(ass_model_logits[0, -1, :], dim=0)
		kl_div = F.kl_div(ass_model_token_probs.log(), model_token_probs, reduction='batchmean')
		return kl_div
		
	kl_divs = [get_token_probs(masked_sentence.replace(' [M].','')) for masked_sentence in tqdm(masked_templates.keys())]
	```
	
	I calculated KL over the honest dataset: `kl_divs = [get_token_probs(masked_sentence.replace(' [M].','')) for masked_sentence in tqdm(masked_templates.keys())]` and compared the mean value of KL before and after fine-tuning.

## Question
2. Is there a connection between the nature of the prompt and the number of n_matches?
- Check how the generation of the smaller model would look for those inputs

	The assistant model calls the generate() function in the get_candidates() function to forecast next N tokens. Need to find the generation mode when the assistant model calls the generate() function. Below is the get_candidates() function:

	```python
	def get_candidates(self, input_ids: torch.LongTensor) -> Tuple[torch.LongTensor, Optional[torch.FloatTensor]]:
	        """
	        Fetches the candidates to be tried for the current input.
	
	        Args:
	            input_ids (`torch.LongTensor` of shape `(batch_size, sequence_length)`):
	                Indices of input sequence tokens in the vocabulary. [What are input IDs?](../glossary#input-ids)
	
	        Return:
	            `torch.LongTensor` of shape `(batch_size, candidate_length)` containing the candidate sequences to be
	            assessed by the model and a `torch.FloatTensor` of shape `(batch_size, candidate_length,
	            vocabulary_size)` containing the logits associated to each candidate.
	        """
	        input_ids = input_ids.to(self.assistant_model.device)
	
	        # Don't generate more than `max_length - 1` candidates since the target model generates one extra token.
	        new_cur_len = input_ids.shape[-1]
	        # print("self.num_assistant_tokens in get_candidates(): ",self.num_assistant_tokens)
	        max_new_tokens = min(int(self.num_assistant_tokens), self.generation_config.max_length - new_cur_len - 1)
	        min_new_tokens = max(min(max_new_tokens, self.main_model_min_length - new_cur_len), 0)
	        if max_new_tokens == 0:
	            return input_ids, None
	
	        # 1. If it is not the first round of candidate generation, prepare the inputs based on the input_ids length
	        # (which implicitly contains the number of accepted candidates from the previous round)
	        has_past_key_values = self.assistant_kwargs.get("past_key_values", None) is not None
	        if has_past_key_values:
	            new_cache_size = new_cur_len - 1
	            self.assistant_kwargs["past_key_values"] = _crop_past_key_values(
	                self.assistant_model, self.assistant_kwargs["past_key_values"], new_cache_size - 1
	            )  # the assistant does not have the token after the last match, hence the -1
	
	            self.assistant_kwargs = _prepare_attention_mask(
	                self.assistant_kwargs, new_cur_len, self.assistant_model.config.is_encoder_decoder
	            )
	            self.assistant_kwargs = _prepare_token_type_ids(self.assistant_kwargs, new_cur_len)
	
	        # 2. Forecast next N tokens using the assistant model.
	        assistant_generation_kwargs = {
	            self.input_ids_key: input_ids,
	            "min_new_tokens": min_new_tokens,
	            "max_new_tokens": max_new_tokens,
	            "generation_config": self.generation_config,
	            "logits_processor": self.logits_processor,
	        }
	
	        assistant_output = self.assistant_model.generate(**assistant_generation_kwargs, **self.assistant_kwargs)
	
	        assistant_output=assistant_output[0]
	        # 3. Update variables for the next round of candidate generation
	        self.assistant_kwargs["past_key_values"] = assistant_output.past_key_values
	
	        # 4. Prepare variables for output
	        candidate_logits = torch.stack(assistant_output.scores, dim=1)
	        candidate_ids = assistant_output.sequences
	        return candidate_ids, candidate_logits
	```

  
- compute the likelihood difference for the rejected completions, i.e. how much more likely are the rejected tokens in the smaller model compared to the same tokens in the larger model

	- How does the likelihood of the rejected tokens change: does it get closer to the likelihood of the larger model or does it diverge more?
   	What metric can I use to measure the change of the likelihood of the rejected tokens? Below is the code for computing the likelihood difference for the rejected tokens and I'm not sure if this is what we want
   
   	```python
	    	l=len(ac_list)
		diff_list=[]
		rej_diff_list=[]
		for i in range(l):
		    diff_list.append(p_list[i]-q_list[i])
		    if(ac_list[i]==False):
		        rej_diff_list.append(p_list[i]-q_list[i])
		    else:
		        rej_diff_list.append(0)
	    	print(diff_list)
		print(rej_diff_list)
    	```
    
    	In one example,
    
    	```python
		diff_list = [-0.025181710720062256, -0.00875278189778328, 0.0026961565017700195, 0.036100927740335464, 0.05424255132675171, 0.172138512134552, 0.03679084777832031, -0.8780305981636047, -0.5250230431556702, -0.31442582607269287, -0.37354910373687744, -0.5111374258995056, 0.07692824304103851, 0.023552268743515015, 0.0667230486869812, 0.03793586790561676, 0.04668661579489708, -0.005420982837677002, -0.04322227090597153, -0.09433448500931263, 0.02496097981929779, -0.12218058109283447]
		rej_diff_list = [0, 0, 0, 0, 0, 0, 0, -0.8780305981636047, -0.5250230431556702, -0.31442582607269287, -0.37354910373687744, -0.5111374258995056, 0, 0, 0, 0, 0, 0, 0, -0.09433448500931263, 0, 0]
    	```
        


## Question

4. Batch size

Currently in Transformers speculative decoding is only supported for batch_size = 1

```python
if generation_mode == GenerationMode.ASSISTED_GENERATION:
    if generation_config.num_return_sequences > 1:
	raise ValueError(
	    "num_return_sequences has to be 1 when doing assisted generate, "
	    f"but is {generation_config.num_return_sequences}."
	)
    if batch_size > 1:
	raise ValueError("assisted generate is only supported for batch_size = 1")
```

## Question

5. Model finetuning
- We should try another finetuning dataset to see if the models are also more aligned after this new finetuning just to understand if a mere finetuning step is enough to align the two models.

	Yes, after finetuning on another dataset ag_news the models are also more aligned. SST2 and ag_news are seemingly unrelated datasets for this task, but finetuning both models on these datasets makes the result (disparity in terms of n_matches between sensitive groups) more aligned. The original way of finetuning in the lora paper was finetuning the models on the counterfactuals generated by tulu-v1-llama2-7b. I will consider generating the counterfactuals and finetuning the models on the counterfactuals as well.

## Question

6. Does the finetuning always improve the model completion? In other words, according to some metric (for instance presence of bias) do the completions get better after finetuning: this is important when we finetune with counterfactuals to see if the smaller model catches up in producing less biased completions faster. After fine-tuning, the 

	I assume the presence of bias can be represented as toxicity, and I use toxicityMeasure_interactive.py and plot_toxicity.ipynb to plot the toxicity before and after finetuning. After fine-tuning on ag_news for 1 epoch, the number of toxic sentence completions has decreased.

	### toxicity
	
	before fine-tuning:
	
	![image](https://github.com/user-attachments/assets/0fa5cd1c-8df1-4558-a14d-34135690a713)
	
	
	after fine-tuning on ag_news for 1 epoch:
	
	![image](https://github.com/user-attachments/assets/dbffe494-b8ef-4b3d-82b3-48032119322f)
