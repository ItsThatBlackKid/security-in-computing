
<!-- TOC -->
- [1. Lecture 6: Digital Signatures](#1-lecture-6-digital-signatures)    
- [1.1. What is digital signature](#11-what-is-digital-signature)
- [1.2. What is the basic idea](#12-what-is-the-basic-idea)
- [1.3. Principles of digital signatures](#13-principles-of-digital-signatures)
- [1.4. RSA Signature System: the steps](#14-rsa-signature-system-the-steps)        
    - [1.4.1. Key generation: public key](#141-key-generation-public-key)
    - [1.4.2. Key generation: private key](#142-key-generation-private-key)
        
    - [1.4.3. Signing and verification](#143-signing-and-verification)

- [1.5. Elgamal Signature System: the steps](#15-elgamal-signature-system-the-steps)  
    - [1.5.1. ElGamal Public Key Generation](#151-elgamal-public-key-generation)
    - [1.5.2. ElGamal Signing](#152-elgamal-signing)
    - [1.5.3. ElGamal Verification](#153-elgamal-verification)<!-- /TOC -->
# 1. Lecture 6: Digital Signatures

## 1.1. What is digital signature


* A technical term for demonstrating authenticity of a digital message from a trusted source. A digitaal signature uses bits of datas as a key to verify the authenticity of the message in a few steps:
  * Authentication of the sender's identity.
  * Confirmation that the sender sent the message
  * Verification that the message was received exactly as it was sent

* Digital signatures are used in a wide variety of settings, from verifying financial transactions to authenticating a webpage or a new software distribution.

## 1.2. What is the basic idea

* The sender encrypts the message using a private key, and the receiving party decrypts using the public key.

## 1.3. Principles of digital signatures

* In order to achieve this we have to apply public-key cryptography
* The process starts with a sender signing the message <span style="color: darkorange">$m$</span>
* The signature algorithm is a function of the sender's private key, <span style="color:darkorange">$k_{pr}$</span>
* After signing the message, the signature $s$ is appended to the message $m$ and the pair <span style="color:darkorange">$(m,s)$</span> is sent to Alice

## 1.4. RSA Signature System: the steps

Suppose Bob (the sender) wants to send a signed message <span style="color:darkorange">$m=88$</span> to Alice ( the receiver). The first steps are exactly the same as in RSA encryption: Bob computes his RSA parameters and sends the public key to Alice. In contrast, the private key is used for signing while the public key is needed to verify the signature. The steps: 

* Parameter settings + Public and Private key generation (by the sender)
* Signing (by the sender)
* Verification (by the receiver)

### 1.4.1. Key generation: public key

* Bob picks two prime numbers <span style="color:darkorange">$p=17$</span> and <span style="color:darkorange"> $q=11$</span>
* Bob calculates <span style="color:darkorange">$n=p\cdot q=17\cdot 11 = 187$</span>
* Bob calculates <span style="color:darkorange">$\phi (n)=(p-1)\cdot (q-1) = (17-1) \cdot (11-1) = 160$</span>
* Bob chooses a prime number <span style="color:darkorange">$e$ </span> such that $e$ is co-prime to <span style="color:darkorange">$\phi(n)$</span>, i.e. <span style="color:darkorange">$\phi(n)$</span> is not divisible by <span style="color:darkorange">$e$</span>
* So, the numbers <span style="color:darkorange">$n= 187$</span> and <span style="color:darkorange">$e=7$</span> become Bob's (the sender's) public key <span style="color:darkorange">$(187,7)$ </span>. Bob sends the public key to Alice. 

### 1.4.2. Key generation: private key

* Bob generates a private key to sign the message <span style="color:darkorange">$m=88$</span>. Let <span style="color:darkorange">$d$</span> be the private key. Then <span style="color:darkorange">$de=1mod\phi(n)$</span>

$$
d \cdot 7 = 1 mod  160
\\
d = 7^{-1} mod 160\\
d = 23 \text{ this is our private key}
$$

### 1.4.3. Signing and verification

* Bob signs the message using private key <span style="color:darkorange">$d=23$></span> as follows:<span style="color:darkorange">
$s= m^d\text{ }mod\text{ }n =88^{23}mod\text{ }187=11$ 
</span>

* Bob sends $(m,s)=(88,11)$ to Alice
* Alice verifies using public key $(n = 187, e =7)$ as follows: $m'=s^emod\text{ } n=11^7mod\text{ }187=88$

## 1.5. Elgamal Signature System: the steps
Suppose Bob (the sender) wants to send a signed message <span style="color:darkred">$m=5$</span> to Alice (the receiver). The steps are exactly the same as done for ElGamal encryption, except the public  key is used for verification.

### 1.5.1. ElGamal Public Key Generation
* Bob selects a prime <span style="color:darkred">$p=11$</span> and generator (e.g. primitive root) <span style="color:darkred">$g=2$</span> and chooses a private key parameter <span style="color:darkred">$x=8$</span>.
* Bob generates a public key parameter <span style="color:darkred">$y=g^x\bmod p=2^8\bmod11=3$</span>
* Bob sends the public key <span style="color:darkred">$(p=11,g=2,y=3)$</span> to ALice.

### 1.5.2. ElGamal Signing
* Bob selects a random number <span style="color:darkred">$k$</span> such that <span style="color:darkred">$1 \leq k \leq p -2$</span> while satisfying <span style="color:darkred">$gcd(k,p-1)=1$</span>. Let's pick <span style="color:darkred">$k=9$</span>. Obviously, <span style="color:darkred">$gcd(9,10)=1$</span>
* Bob computes signature parameters as follows 

$$
\begin{matrix}
r & = &g^k\bmod p \\
& = &2^9\bmod 11=6\\
\\
s & = & k^{-1}(m-x\cdot r)\bmod(p-1)\\
& = &9^{-1}(-43)\bmod10 \\
& = &-387\bmod{10}=3
\end{matrix}
$$

* Bob sends signed message <span style="color:darkred">$(m=5,r=6,s=3)$</span>

### 1.5.3. ElGamal Verification

* Alice checks <span style="color:darkred">$r \geq 1$</span> and <span style="color:darkred">$r \leq p-1$</span>. If true, she accepts the signature. Otherwise she rejects.
* Alice computers verification parameters <span style="color:darkred">$v$</span> and <span style="color:darkred">$w$</span> as follows: $v  =  g^m\bmod p=2^5\bmod11 =10$ and $w=y^r\cdot r^s\bmod p = 3^6\cdot6^3\bmod11=3\cdot7\bmod11=10$




