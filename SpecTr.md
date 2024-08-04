## A brief analysis of the differences between the two algorithms

The left shows the algorithm of Speculative decoding, and the right shows the algorithm of SpecTr

 <center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://github.com/user-attachments/assets/02274570-3e21-4d70-af89-376bd331dc9c" width = "32%" alt=""/>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="https://github.com/user-attachments/assets/80807457-6e11-42a9-bedb-6315b71c96bb" width = "48%" alt=""/>
    <br>
    


The main difference lies in the number of sampled drafts sampled from the small model and the selection algorithm that selects a valid sequence from multiple draft sequences.

1− 
π∈Π(p,q)
min
​
 P 
X,Y∼π
​
 (Y

=X)= 
π∈Π(p,q)
max
​
 P 
X,Y∼π
​
 (Y=X)=1− 
x∈Ω
∑
​
 min(p(x),q(x))
<div style="text-align: center;">
    <img 
        style="border-radius: 0.3125em; box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);"
        src="https://github.com/user-attachments/assets/331d9d99-5197-40f5-8a7d-7ea0c98862c2" 
        width="30%" 
        alt=""
    />
</div>

 
 

