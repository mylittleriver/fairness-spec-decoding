- evaluate_honest_spec.ipynb generates the completions using speculative decoding and plots the token accpetance ratio graph (n_matches/max_new_tokens). 

- likelihood_difference.ipynb plots the distribution of the likelihood difference (p_i - q_i) between the larger and smaller model before and after finetuning.

- category_frequency_datasets.ipynb plots the frequency of each category (female, male, etc) in each dataset (ag_news/sst2/wikitext/imdb).

- finetuning.ipynb is for finetuning the larger and smaller models on the same or different datasets. The previous experiments include finetuning gpt2/distilgpt2 both on ag_news; finetuning gpt-neo-1.3B/gpt-neo-125M on sst2 and wikitext respectively, and then finetuning both on IMDB.
  
To obtain the information of n_matches, p_i and q_i etc, some changes need to be made to transformers/generation/utils.py and transformers/generation/candidate_generator.py. The utils.py and candidate_generator.py here are the modified ones that could run properly with the previous ipynbs.

