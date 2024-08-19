## Distribution of p_i and q_i for accepted, rejected and both tokens of all groups

![image](https://github.com/user-attachments/assets/d1a6d877-36f0-48aa-9520-f8d3af7d1388)

![image](https://github.com/user-attachments/assets/6ed46ed9-6f07-433a-b4f5-b60b5ba011a3)

![image](https://github.com/user-attachments/assets/1817c75d-b1d6-45d6-a76a-d189e3765cef)


## Goal: to find tokens that smaller model has higher confidence but rejected, and tokens that smaller model has higher confidence and accepted; to seperate into specific groups and find disparity among groups

The pair with greatest disparity in terms of acceptance rate is queer/queer_gender_pronoun, with acceptance rate 0.837 for queer, 0.904 for queer_gender_pronoun. 

<center>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/14c0601b-7b46-463f-9bed-7643cdc30c0d" width = "38%" alt=""/>
 <img style="border-radius: 0.3125em;
 box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
 src="https://github.com/user-attachments/assets/941c9eed-5972-4290-96b6-a134ac491359" width = "38%" alt=""/>
</center>

The distribution of likelihood difference and acceptance rate/rejection rate of other categories are shown below:

<center>
 <img src="https://github.com/user-attachments/assets/08391b8d-383d-4144-bfbf-472a3ad47545" width = "38%" alt=""/>
 
 <img src="https://github.com/user-attachments/assets/df201453-00b4-4b5c-8df7-cbaff93fa2e4" width = "38%" alt=""/>
</center>

<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/6efb2960-c760-43c4-b2d2-14347b23d608" width = "38%" alt=""/>
</center>
<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/515d2ee9-4309-4ff1-86ec-6a1cf2363d1c" width = "38%" alt=""/>
</center>

<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/e9713e42-997b-4732-90e3-59ad2736d4b4" width = "38%" alt=""/>
</center>
<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/b247fc47-28a7-4735-955f-a5b4fe192d9b" width = "38%" alt=""/>
</center>

<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/3211b46c-1ee0-4470-b34e-e0fc52cfb19e" width = "38%" alt=""/>
</center>
<center>
<img style="border-radius: 0.3125em;
box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
src="https://github.com/user-attachments/assets/63a91582-02a5-4c7d-bf12-6d2d33709c5c" width = "38%" alt=""/>
</center>

## Change num_assistant_tokens_schedule from heuristic to constant and change num_assistant_tokens to see what will change

![image](https://github.com/user-attachments/assets/b6cfdb55-a96c-4cf2-815f-ee96c68f783f)

![image](https://github.com/user-attachments/assets/a7c8ec3e-dc35-4039-a011-bbcabd9414b3)

![image](https://github.com/user-attachments/assets/530a173b-7543-4f0c-af9c-b7567a395d66)

![image](https://github.com/user-attachments/assets/a6f0fd92-2d58-4f58-bd39-0227accc4fd0)

![image](https://github.com/user-attachments/assets/55e5b88d-0911-47f5-bd50-9b01030f713d)

![image](https://github.com/user-attachments/assets/fb4e51ce-8d7d-4526-9033-7facb796bca1)
