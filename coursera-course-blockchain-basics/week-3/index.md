# Algorithms and techniques

- Summarize the working of public key cryptography and asymmetric key encryption. 
- Explain simple hashing & Merkle tree hash.
- Explore the application of hashing and cryptography in protecting the Blockchain.

**Hashing** and **asymmetric key encryption** techniques are predominantly used for securing  the chain and for efficient **validation** and **verification**. They depend on several complex proven algorithms. 

- We provide a high level view of the application of these algorithms,  and the role they play in securing the decentralized chain in the four lessons of this module namely
  - Public-key cryptography
  - secure hashing
  - transaction integrity
  - block integrity.
- We'll begin this module by discussing the concept of asymmetric key encryption, then we'll define the concept of hashing, followed by the algorithms used for various hashing needs of the block chain protocol.  We then explain the techniques that use these algorithms,  to manage the integrity of the transactions and the blocks in a block chain. 

## Public key cryptography



blockchains decentralized network participants,  are not necessarily known to each other. Credentials cannot be checked by the conventional means such as verifying who you are with your driver's license. Participants can join and leave the chain as they wish.  They operate beyond the boundaries of trust.  Given this context.  

- how do you identify the peer participants?  
- How do you authorize and authenticate the transactions? 
- How do you detect forged or faulty transactions? 

by using Public-key cryptography algorithm that we'll discuss in this lesson. 

<img src="https://www.hacksandsecurity.org/sites/default/files/u3/1_23RpkZuWAeSP7x0YdMtsdQ.png"/>

**symmetric key** = same key is used for encryption and decryption,

problems : 

- it is easy to derive the secret key from the encrypted data. 
- the key distribution, how do you pass the key to the participant transacting? 
- These issues are further exasperated in a block chain decentralized network where participants are unknown to each other. 



**asymmetric / Public-key cryptography**  = employs two different keys that take care of both the issues of symmetric key encryption.



Now let's look at an example, authenticate the sender and the receiver. 

<img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1617266227/Untitled_Diagram-Page-2_2_yaugjm.png"/>

Let's say a participant in Buffalo wants to transact with the participant in Kathmandu. Instead of sending just a simple message, a participant in Buffalo will send a transaction data encrypted by Buffalo's private key, and then encrypted by Kathmandu's public key. Kathmandu will first decrypt the data using its own private key, then use Buffalo's public key to decrypt assigned transaction data. 

This ensures that only Kathmandu can decrypt and receive the data and that only Buffalo could have sent the data. A popular implementation of public key, private key is the **Rivest Shamir Adleman (RSA)** algorithm.  Common application of RSA is the passwordless user authentication, for example for accessing a virtual machine on Amazon cloud. Though RSA is very commonly used in many applications,  block chains need a more efficient and stronger algorithm.  Efficiency is a critical requirement since public key pair is frequently used in many different operations in block chain protocol. 

Elliptic Curve Cryptography, ECC family of algorithms is  used in the bitcoin as well as an Ethereum block chain for generating the key pair.  Why ECC not RSA?  ECC is stronger than RSA for a given number of bits.  Did you know that 256 bit ECC key pair is equal in  strength to about 3072 bits of RSA key pair.  Both bitcoin and Ethereum use ECC based algorithms for their encryption needs.

## Hashing 



Why should we learn about encryption hashing, you may ask. 



The private public key pair is  a metaphorical passport to participating in transacting on the blockchain.  Similar to how you learn to use a credit card,  secure it and protect it. 



You need to protect the private key for the security of your assets on the blockchain.  In this lesson, we learn hashing that plays a critical role in the blockchain process,  and also in the integrity of the transaction and confidentiality of data. 

- A hash function or hashing transforms and maps  an arbitrary length of input data value to a unique fixed length value.

- Input data can be a document, tree data, or a block data. 

- The following are two basic requirements of a hash function. The algorithm chosen for the hash function should be a **one-way function** and it should be **collision free**. These requirements are achieved by choosing a strong algorithm such as secure hash,  and by using appropriately large number of bits in the hash value.

- Most common hash size now is 256 bits and the common functions are SHA-3, SHA-256 and Keccak. 

- **Hash value space**, how good is 256 bits hash?  A 256-bit hash value space is indeed very large. 2 to the power of 256 possible combinations of values. 

  

We'll compare two different approaches for hashing based on how the constituent elements are organized. 

A **simple hash** and a **Merkle tree hash.** 

Here we illustrate simple hashing and Merkle tree hashing with ADD as a hash function. We use the data 10, 4, 6, 21 and 19 and ADD as a hash function.  Actual hashing functions are quite complex and are variations of SHA-3, and the data values are much larger,  mainly 256 to 512 bit values.  

In the simple hash approach, all the data items are linearly arranged and hashed. 

In a tree-structured approach, the data is at the leaf nodes of the tree,  leaves are pairwise hash to arrive at the same hash value as a simple hash. 



<img src="https://hackernoon.com/hn-images/1*2ZLfmh8Uo21qK0gUEd9YNA.png"/>



When is a tree-structured hash used? 

- fixed number of items to be hashed,  such as the items in a block header
- verifying the **composite** block integrity and not the individual item integrity,  we use simple hash. 

When is a simple hash used? 

- the number of items differ from block to block, for example, number of transactions, number of states,  number of receipts, we use the tree structure for computing the hash. 

Note that the state is a variable that may be modified by a smart contract execution, and the result of the execution may be returned in a receipt. We'll learn more about their use in course two. 

Tree structure helps the efficiency of repeated operations, such as transaction modification and the state changes from one block to the next. Log N versus N. 

Summarizing, in Ethereum,

- hashing functions are used for generating account addresses,  digital signatures, transaction hash,  state hash, receipt hash and block header hash. 
- SHA-3, SHA-256, Keccak-256 are some of the algorithms commonly used by hash generation in blockchains.

## Transaction Integrity

To manage the integrity of a transaction we need 

- a secure unique **account address**. a standard approach to uniquely identify the participants in the decentralized network. 
- **authorization** of the transaction by the sender through **digital signing**. 
- **verification** that the **content** of that transaction is **not modified**. 

We use a combination of **hashing** and **public key cryptography**,  that we learned in the last two lessons to solve these problems. 

1. Let's start with the **address of the accounts**.  Addresses of accounts are generated using public key, private key pair.

- a 256-bit random number is generated, and designated as the private key. Kept secure and locked using a passphrase. 
- an ECC algorithm is applied to the private key, to get a unique public key. This is the private public key pair. 
- a hashing function is applied to the public key to obtain account address. The address is shorter in size,  only 20 bytes or 160 bits. 

2. Now that we have the account address,  let's look at the transaction initiated by this address.  A transaction for transferring assets will have to be 

- authorized

- non-repudiatable

- unmodifiable. 

  

  we first examine, the **digital signing process**, and then apply it to that transaction. 

  <img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1616568094/kladblok-Page-14_zhnb71.png" style="zoom: 67%;" />

  

- Data is hashed and encrypted. = **digital signature**

- The receiver gets the original data, and the **secure hash digitally signed**. 

- Receiver can recompute the hash of the original data received,  and compare it with the received hash to verify the integrity of the document. 



Now, consider the transaction to be that data. 

- find the hash of the data fields of the transaction. 
- encrypt that hash  using the private key of the participant originating the transaction. Thus, digitally signing the transaction to  authorize and making the transaction non-repudiable. 
- this hash just added to the transaction. It can be verified by others decrypting  it using the public key of the sender of the transaction, and recomputing the hash of the transaction. 
- Then, compare the computed hash and the hash received at the digital signature. 
- If that is a match,  accept the transaction.  Otherwise, reject it. 
- Note that for the complete transaction verification, the timestamp,  nons, account balances, and sufficiency of fees are also verified.

## Securing Blockchain

As we discussed before, some of the main components of the Ethereum block are 

- the header
- the transactions
- the transaction hash or the transaction root
- the state hash, or the state root. 

Integrity of the block is managed by assuring that

-  the block header contents are not tampered with
- the transactions are not tempered with
- state transitions are efficiently computed, hashed, and verified. 

Remember, the block chain is supposed to be an immutable record. In Ethereum, the block hash is the block of all the elements in the block header, including the transaction root and state root hashes. It is computed by applying a variant of SHA-3 algorithm called Keccak on all the items of the block header. 



<img src="https://www.researchgate.net/profile/Ingo-Weber-2/publication/330752524/figure/fig1/AS:720996399063040@1548910345223/Ethereum-block-header-and-state-merkle-tree.png"/>



You would see a real example of bitcoin block hash in the quiz associated with this module.  A typical block has about 2,000 transactions in bitcoin and about 100 transaction Ethereum.  We need an efficient way to detect tampering and validate the transaction efficiently. 

Hashes of transaction in a block are processed in a tree structure called **Merkle tree hash** that we discussed in earlier lesson. Merkle tree hash is also used for computing the **state root hash**,  since only the hash of the chained states from block to block have to be re-computed. It is also used for **receipt hash root**. 



<img src="https://upload.wikimedia.org/wikipedia/commons/9/95/Hash_Tree.svg"/>

Remember the advantage over flat versus tree representation. If any transaction is to be verified, only one path to the tree has to be checked.  You don't have to go through the entire set of transactions. 

Smart contract execution in Ethereum results in state transitions.  Every state change requires **state root hash re-computation.**  Instead of computing hash for the entire set of states,  only the affected path in the Merkle tree needs to be re-computed. 

When the state 19 is changed to 20,  that results in the path including 31, 41, and the state root hash 64 to be re-computed. Only that path is re-computed, not the entire tree. 

<img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1617278985/Screenshot_from_2021-04-01_14-09-25_bcbi3v.png" style="zoom: 33%;" />



Now, let's move on to **block hash computation**.  => computed by first computing the **state root hash**, **transaction root hash** and then **receipt root hash**, shown at the bottom of the block header. 

These roots and all the other items in the header are hashed together with the variable nonce to solve the proof of work puzzle. 

<img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1617279129/Screenshot_from_2021-04-01_14-11-55_y8i8tg.png"/>



Block hash serves two important purposes: 

- verification of the integrity of the block and the transactions
- formation of the **chain link** by embedding the previous block hash in the current block header. If any participant node tampers with the block,  it's hash value changes resulting in the mismatch of  the hash values and rendering the local chain of the node in an invalid state.  Any future blocks initiated by the node would  be rejected by other miners due to hash mismatch. This enforces the immutability of the chain. 

Summarizing

- a combination of  hashing and encryption are used for securing the various elements of the block chain. 
- Private public key pair and hashing are  important foundational concepts in decentralized networks that operate beyond trust boundaries.