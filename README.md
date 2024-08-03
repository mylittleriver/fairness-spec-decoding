- evaluate_honest_spec.ipynb generates the completions using speculative decoding and plots the token accpetance ratio graph (n_matches/max_new_tokens). But to obtain n_matches, the following changes need to be made to transformers/generation/utils.py and transformers/generation/candidate_generator.py:
- > ![image](https://github.com/user-attachments/assets/3d656aa2-8539-4644-8b59-973732a95122)


- likelihood_difference.ipynb plots the distribution of the likelihood difference (p_i - q_i) between the larger and smaller model before and after finetuning.

- category_frequency_datasets.ipynb plots the frequency of each category (female, male, etc) in each dataset (ag_news/sst2/wikitext).
  
