The newly plotted token acceptance ratio graph for the setting [gpt2/distilgpt2, temperature 1e-9] has less disparity than the initial result, thus I replotted the token acceptance ratio graph for previous settings to verify the previous results. After checking whether the newly plotted graph is consistent with the distribution of likelihood difference of the same setting [gpt2/distilgpt2, temperature 1e-9], it is found that they are indeed consistent. I did the new plotting repeatedly for several times and on two different servers, and I've checked that the models used haven't been updated. Therefore, it can be inferred that the newly plotted graphs are correct and initial result of token acceptance ratio graph was wrong. I have modified the code for plotting each time with a new setting, so I think it's because the code for plotting the initial result was wrong and the mean of token acceptance ratio for each category was not properly calculated. However, I have observed some features of the newly plotted graphs, and below are some analysis.

### gpt2/distilgpt2:

For models gpt2/distilgpt2, the result is stable when temperature = 1e-9, and differs slightly each time when temperature = 1.

When temperature = 1, the ratio of queer_gender_pronoun is always the highest, and the ratio of queer_gender_xenogender is always the lowest before finetuning. After finetuning, the highest and lowest ratio for all categories change each time, and the ratios increase generally.

When temperature = 1e-9, the ratio of nonqueer_gender is always among the lowest ones both before and after finetuning. After finetuning, the ratio of nonqueer_orientation always increases and becomes the highest, and the ratios increase generally, the disparity between the highest and lowest ratio also increases. When max_new_tokens increases, i.e., more new tokens are generated, the ratios also increase generally.

Below is the frequency of each category in ag_news dataset. When temperature = 1e-9, for the categories that appear in the dataset, i.e. female, male, queer_gender. nonqueer_orientation and queer_orientation, their ratios increase after finetuning, and for other categories that don't appeear in ag_news, their ratios don't change or decrease when max_new=10, and some of them increase when max_new is larger. This suggest that when finetuning the model on a dataset that contains the words of a category, the token acceptance ratio of that category increases. But the amount of increase is not linear to the frequency, for example, "male" appears 110407 times and "nonqueer_orientation" appears 1088 times, but the amount of increase of nonqueer_orientation is always larger or equal to that of male.

![image](https://github.com/user-attachments/assets/3a9d0d73-8fec-47c4-931c-b5c93917a0b4)




max new = 10:
<!--(at first I thought the reason for the difference between the new and initial results may be that I use "gpt2" instead of "openai-community/gpt2", but their results are similar so it's not the reason)
openai-community/gpt2:
![image](https://github.com/user-attachments/assets/96b45d40-b1a3-4e34-a2cf-4ef9e0a85c6e) -->

<!--gpt2: -->
![image](https://github.com/user-attachments/assets/454f2813-e2c2-48ab-b720-3d2a784537bf)

![image](https://github.com/user-attachments/assets/da143f48-129a-45b3-a7bd-66ff15d0df87)

![image](https://github.com/user-attachments/assets/5b6d4d11-56bd-4b70-8cfa-633f6719fd6c)


![image](https://github.com/user-attachments/assets/9879def0-9286-4a8a-8632-1119acde2932)

![image](https://github.com/user-attachments/assets/b470c232-5c6a-4e3f-8970-9f08b5542bf5)

![image](https://github.com/user-attachments/assets/0b9ed5f8-6da4-4f86-ba53-37c5ad202148)


![image](https://github.com/user-attachments/assets/fce07b5b-fa84-460d-b923-4f707a67da06)

![image](https://github.com/user-attachments/assets/666cad40-750f-49f9-9acc-d57fc29c295c)



max new = 20:

![image](https://github.com/user-attachments/assets/8f686df7-3a11-482c-b06f-f7ae186cc675)
![image](https://github.com/user-attachments/assets/747d0a51-4222-4bf0-a4af-8229a66e6a91)




max new = 30:
![image](https://github.com/user-attachments/assets/f94c8d70-7f6b-44eb-9de8-9a8c38acc143)

![image](https://github.com/user-attachments/assets/aea8f5de-e33d-4abe-b869-8ac359408369)


max new = 40:
![image](https://github.com/user-attachments/assets/6ad10647-a793-45f9-9abf-40d39ff82438)
![image](https://github.com/user-attachments/assets/d6b2f347-13be-4d21-9494-1f7b5353147d)


### neo-1.3B/neo-125M:

For neo-1.3B/neo-125M, the result is also stable when temperature = 1e-9. It seems to have more disparity than gpt2/distilgpt2 when temperature = 1e-9. But when temperature = 1, it has less disparity. 

frequency of each category in sst2 dataset:
![image](https://github.com/user-attachments/assets/e28aa625-3b7c-42d1-bd41-9b159c457727)
frequency of each category in wikitext dataset:
![image](https://github.com/user-attachments/assets/caa8f71c-0715-4267-8d95-b4fca9d36228)
frequency of each category in imdb dataset:
![image](https://github.com/user-attachments/assets/35767d80-7264-4e16-aa34-6cc1274d7b00)


max new = 10:
![image](https://github.com/user-attachments/assets/d38da234-ad1f-4ced-9992-dfdb8ab57bc0)
![image](https://github.com/user-attachments/assets/507e77c8-af09-4c0c-863e-696cfb267d3e)


![image](https://github.com/user-attachments/assets/c274c3a7-c098-4723-a6a1-f023e48ea38c)


max new = 20:
![image](https://github.com/user-attachments/assets/5398f1ca-f63b-4eb8-8307-25d584e94f27)
![image](https://github.com/user-attachments/assets/b3f3dc60-101d-4445-b378-7389f68013f7)
