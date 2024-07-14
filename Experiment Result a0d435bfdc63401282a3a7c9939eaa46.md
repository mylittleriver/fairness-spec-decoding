# Experiment Result

main model: gpt2, assistant model: distilgpt2

### finetuning both models on ag_news:

parameters:

![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled.png)

![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled%201.png)

main model (gpt2):

![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled%202.png)

assistant model (distilgpt2):

![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled%203.png)

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

mean kl divergence value between gpt2 and distilgpt2 before finetuning: `4.3072e-06`

mean kl divergence value between gpt2 and distilgpt2 after finetuned on ag_news: `4.4415e-06`

![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled%204.png)

### percentage of tokens coming from the assistant model

without finetuning:

![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled%205.png)

finetuned on ag_news with 1 epoch:

![Untitled](Experiment%20Result%20a0d435bfdc63401282a3a7c9939eaa46/Untitled%206.png)

### toxicity
before finetuning:
![image](https://github.com/user-attachments/assets/0fa5cd1c-8df1-4558-a14d-34135690a713)

