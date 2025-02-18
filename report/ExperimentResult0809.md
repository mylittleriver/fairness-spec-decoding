## Distribution of p_i and q_i for accepted, rejected and both tokens of all groups

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/d1a6d877-36f0-48aa-9520-f8d3af7d1388" width = "43%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/6ed46ed9-6f07-433a-b4f5-b60b5ba011a3" width = "43%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/1817c75d-b1d6-45d6-a76a-d189e3765cef" width = "43%" alt=""/>
</center>

KDE of distribution of p_i and q_i for accepted tokens of all groups:
![image](https://github.com/user-attachments/assets/66b51cf6-be01-4e92-aa14-63470340fa7b)

KDE of distribution of p_i and q_i for rejected tokens of all groups:
![image](https://github.com/user-attachments/assets/45b04987-b66e-4381-9450-deee6ee234c6)

what else processing can be done to p_i and q_i for each token?
<img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/4e7231f6-144e-45e4-bccd-62e3118bb8e6" width = "70%" alt=""/>

## Goal: to find tokens that smaller model has higher confidence but rejected, and tokens that smaller model has higher confidence and accepted; to seperate into specific groups and find disparity among groups

The pair with greatest disparity in terms of acceptance rate is queer/queer_gender_pronoun, with acceptance rate 0.837 for queer, 0.904 for queer_gender_pronoun. 

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/14c0601b-7b46-463f-9bed-7643cdc30c0d" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/941c9eed-5972-4290-96b6-a134ac491359" width = "44%" alt=""/>
</center>

The distribution of likelihood difference and acceptance rate/rejection rate of other categories are shown below:

<center>
 <img src="https://github.com/user-attachments/assets/08391b8d-383d-4144-bfbf-472a3ad47545" width = "44%" alt=""/>
 
 <img src="https://github.com/user-attachments/assets/df201453-00b4-4b5c-8df7-cbaff93fa2e4" width = "44%" alt=""/>
</center>

<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/6efb2960-c760-43c4-b2d2-14347b23d608" width = "44%" alt=""/>
</center>
<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/515d2ee9-4309-4ff1-86ec-6a1cf2363d1c" width = "44%" alt=""/>
</center>

<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/e9713e42-997b-4732-90e3-59ad2736d4b4" width = "44%" alt=""/>
</center>
<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/b247fc47-28a7-4735-955f-a5b4fe192d9b" width = "44%" alt=""/>
</center>

<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/3211b46c-1ee0-4470-b34e-e0fc52cfb19e" width = "44%" alt=""/>
</center>
<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/63a91582-02a5-4c7d-bf12-6d2d33709c5c" width = "44%" alt=""/>
</center>

## Change num_assistant_tokens_schedule from heuristic to constant and change num_assistant_tokens to see what will change

### Distribution of p_i and q_i for accepted, rejected and both tokens of all groups
<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/b6cfdb55-a96c-4cf2-815f-ee96c68f783f" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/a7c8ec3e-dc35-4039-a011-bbcabd9414b3" width = "44%" alt=""/>
</center>

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/530a173b-7543-4f0c-af9c-b7567a395d66" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/a6f0fd92-2d58-4f58-bd39-0227accc4fd0" width = "44%" alt=""/>
</center>

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/55e5b88d-0911-47f5-bd50-9b01030f713d" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/fb4e51ce-8d7d-4526-9033-7facb796bca1" width = "44%" alt=""/>
</center>


### Distribution of likelihood difference

The pair with greatest disparity in terms of acceptance rate becomes queer_gender_pronoun/queer_gender_xenogender, with acceptance rate 0.912 for queer, 0.811 for queer_gender_pronoun.

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/dce05283-daee-402e-bfed-6eb884e4f35f" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/cfbf333f-9b14-4018-960e-e12582c08fea" width = "38%" alt=""/>
</center>

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/f656014f-aa84-4c4f-be33-302d200c2390" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/775ee0f1-8e97-49b5-a04d-04ae479d7ff6" width = "38%" alt=""/>
</center>

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/ce3eb4a0-f967-4c9a-8060-1807f83a4575" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/ee4c15d0-a533-4df9-aad5-f1927eec824f" width = "38%" alt=""/>
</center>

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/6cb3db88-db58-415e-b8b7-0821d8009dcb" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/8dc98925-acde-4ccb-94f1-4ed7745e41ab" width = "38%" alt=""/>
</center>

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/7d5e3241-c666-46d7-8900-2b7f7f01accc" width = "44%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/93f4d7d8-406b-444d-836a-0ec8ab13702a" width = "38%" alt=""/>
</center>










