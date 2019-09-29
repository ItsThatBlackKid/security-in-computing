# Lecture 5: Privacy Preseveration Computation


## What is *data* privacy and types of Data Privacy

* <span style="color:darkred">Information Privacy</span> (also known as data privacy) is the privacy of personal information and usually relates to personal data stored on computer systems. It relates to different data types, including:
  * <span style="color:darkred">Internet Privacy  (online privacy) </span>: All personal dat shared over the internet is subject to privacy issues. Most websites publish a privacy policy that details the website's inteded use of collected online and/or offline collected data.
  * <span style="color:darkred">Financial Privacy</span>: Financial information is particuarly sensitive, as it may easily be used to cmmit online and/or offline fraud
  * <span style="color:darkred">Medical Privacy</span>: All medical records are subejct to stringent laws that address user access privileges. By law, security and authentication systems are often required for individuals that process and store medical records

### How can Data Privacy be applied? 

Information privacy may be applied in nuemrous ways, including encryption, authentication, and data masking

## Basic Building Blocks for Privacy Preserving Computation
* (+) Adding encrypted numbers securely: 
  * A sender encrypts two numbers with a generated public key and sends the encrypted numbers to the cloud. The cloud multiplies (x) the encrypted numbers to perform additoin and sends the result to the receiver who decrpyts it.
* (x) Multiplying encrypted numbers securely:
  * A sender encrypts two numbers with a generated public key and sends the encrypted numebrs to the cloud. Cloud multiplies encrypted numbers to perform multiplication (x) and sends the results to the receiver who decrypts it.

* Partially homorphic
  * RSA Homomorphism: Multiplying numbers secretly
  * Paillier Homorphism: Adding numbers secretly
  * ElGamal Homomorphism: Multiplying numbers secretly  
* Fully homomorphic: add and multiply numbers secretly
* Pros and cons: 
  * partially homomorphic schemes are faster, but limited in their capabilities - cannot add and multiply simultaenously
  * Fully homomorphic schemes can do both simultaneously but are very slow

## RSA Homomorphism: Multiplying two numbers secretly

* Say the sender encrypts two messages <span style="color:darkred">$M_1=3$</span> and <span style="color:darkred">$M_2=4$</span> with public key: <span style="color:darkred">$n=33,e=7$</span> and private key <span style="color:darkred">$d=3$</span> as follows:<span style="color:darkred">$C_1=M_{1}^e\bmod n = 3^7\bmod33=2187\bmod33=9$</span>
<span style="color:darkred">$C_2=M_2^e\bmod n=4^7\bmod33=16384\bmod33=16$</span>
* Sends sends <span style="color:darkred">$C_1=9$</span> and <span style="color:darkred">$C_2=16$</span> to the cloud to multiply the numbers.
* The cloud finds that <span style="color:darkred">$C_1\cdot C_2=144$</span>. It sends the multiplied value to receiver
* Receiver decrypts <span style="color:darkred">$144^3\bmod33=12$</span> which is <span style="color:darkred">$M_1\cdot M_2=3\cdot4=12$</span>

