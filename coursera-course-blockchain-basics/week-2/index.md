# ethereum blockchain - smart contracts



## smart contracts

- Bitcoin blockchain => the mother of blockchains => intended for p2p transfer of value 
- **Ethereum** 2013 : framework for **code execution**
  - centerpiece and thrust of this blockchain is a **smart contract.** 
  - took a significant step towards transforming the blockchain into a computational framework that  provided opportunities in the decentralized realm. 
  - Ethereum supports smart contracts and a VM on which smart contracts execute. 
  - Smart contracts enable decentralized application that accomplish more than a transfer of value. => Efficient **automation of decentralized application** such as supply chain. 

<u>goals</u>

- you will be able to discuss the smart contract. 
- Illustrate ethereum blockchain protocol, structural elements, and operational aspects. 
- Demonstrate the concept of **gas**,  the fuel or the payment model for code execution and the incentive model for the Ethereum blockchain.

<img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1616650452/blockchain-Page-2_fpfid9.png"/>

What is a smart contract? 

- a piece of code deployed in the blockchain node. 
- Execution is initiated by a message embedded in the transaction. 
- Digital currency transfer request simple addition and subtraction. 
- Ethereum enables transaction that may carry out more sophisticated operations.  For example, a transaction could require a conditional transfer, it may require some evaluation,  it may need more than one signature for transfer of assets, or it may involve waiting for a specific time or date. 



> example of what a smart contract can do. 
>
> An auction bidding smart contract could execute this logic. If the age of a bidder is greater than 18 and the bid is greater than the minimum bid,  then, accept the bid,  or else reject the bid. 



What does the smart contract look like?  => Structurally, a smart contract resembles a **class definition in an object oriented design**. It has data, functions or methods with modifiers public or private,  along with getter and set of functions. 

How do you write a smart contract? => programming languages have been designed for coding smart contracts. 

**Solidity** is one such language.  

```solditiy
pragma solidity >=0.4.22 <0.9.0; // indicates the version of the solidity language.

// contract's name
// This particular contract is for one integer storage.
contract SimpleStorage {
    uint storedData;

    function set(uint x) { 
    	storedData = x;
    }
    
    function get(uint x) constant returns (uint) { 
    	return storedData;
    }
}
```

- Where does the code in the smart contract get executed? 
- Where is it located in a node? 

We need a computational infrastructure to execute any arbitrary code.  Every node in Ethereum network should be able to execute the code irrespective of that underlying type of hardware or operating system. 

=> Ethereum Virtual Machine, **EVM**. = a run anywhere obstruction layer for the contract code. 

A smart contract written in a high level programming language is translated into EVM byte code,  and then, deployed on the Ethereum Virtual Machine, EVM.  Every node will host the same smart contract codes on the EVM. 

Summarizing

- smart contracts add a layer of logic and computation to the trust infrastructure supported by the blockchain. 
- Smart contracts allow for execution of code.  Enhancing the basic value transfer capability of the Bitcoin blockchain. 
- The code for this smart contract is written in  a high level language like Solidity and compiled into byte code. 
- The code for the smart contracts is executed on a special structure known as Ethereum Virtual Machine.

## ethereum structure

<img src="https://static.coindesk.com/wp-content/uploads/2017/03/state-3-15-01.png" style="zoom: 15%;" />

<img src="https://imgur.com/3dlka35.png" style="zoom: 25%;" />

<img src="https://www.oreilly.com/library/view/mastering-blockchain/9781787125445/graphics/B05975_07_32.jpg" style="zoom: 33%;" />



- BTC blocking state is defined in terms of **UTXOs** and a reference implementation of the Wallet application that held the account reference. 
- Ethereum formally introduce the concept of an **account** as a part of the protocol. 
  - originator + target of a transaction. 
  - A transaction directly updates the account balances <=> to maintaining the state such as in the BTC UTXOs. 
    It allows for transmission of value, messages and data between the accounts which result in the state transitions.  transfers are implemented using transactions. 
  - There are two types of accounts
    - Externally Owned Accounts or **EOA** are controlled by private keys. 
      - An EOA is needed to participate in the Ethereum network.  It interacts with the blockchain using transactions. 
    - Contract Accounts or **CA** are controlled by the code and can be activated only by an EOA
      - A Contract Account represents a smart contract. 
  - Every account has a **coin balance**.   The participant node can send transaction 
    - for Ether transfer
    - to invoke a smart contract code 
    - both. 
    - all transactions require fees. 
  - An account needs sufficient balance to meet fees needed for transactions.  Fees are paid in **Wei**.  Wei is a lower denomination of Ether
- A transaction in Ethereum includes
  - recipient of the message
  - digital signature of the sender authorizing the transfer
  - amount of Wei to transfer
  - optional data field or payload that contains a message to a contract, 
  - STARTGAS = a value for  the maximum # of computational steps the transaction is allowed. 
  - GASPRICE = this represents the fee a sender is willing to pay for the computations. 



<img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1616663631/Screenshot_from_2021-03-25_10-13-36_qql6jr.png"/>

<img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1616663797/Screenshot_from_2021-03-25_10-16-25_yoj87y.png"/>

 

Ethereum block structure has 

- a header
- transaction
- runner-up block headers. Block details. 

Summarizing

- accounts are basic units of Ethereum protocol. 
- Externally Owned Accounts and Smart Contract Accounts. 
- An Ethereum transaction includes not only fields what transfer of Ethers but  also messages for invoking Smart contract. 
- An Ethereum block contains the usual previous block hash, nonce, transaction details but also details about gas or fees limits, the state of the Smart Contracts and Runner-Up headers, 

## ethereum operations

```javascript
const currentBlockIndex = 1
const blocks = [...]
const block = blocks[currentBlockIndex]
const previousBlock = blocks[currentBlockIndex-1]
if(isValid(previousBlock)){
    const validTiming = block.timestamp > previousBlock.timestamp && block.timestamp < (new Date() + twoDays)
    const validPow = block.pow
    const lastState = previousBlock.lastState
    if(validTiming && validPow){
      let i = 0 
      for(const transaction in block.transactionList){
          S[i+1] = apply(S[i], transaction)
          i++
      }
    }
}
```

For a simple Ether transfer we need 

- the amount to transfer (transferred to their respective accounts. )
- the target address
- the fees or gas points. (transferred to their respective accounts. )



<img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1617256095/Untitled_Diagram_1_gtsseo.png"/>





**Ethereum node** is  a computational system representing a business entity or an individual participant.  

**Ethereum full node** hosts the software needed for transaction *initiation*, *validation*,  *mining*, *block creation*, *smart contract execution* and the *EVM*. 



Smart contracts

- are designed, developed,  compiled and deployed on the EVM 

- there can more than one smart contract in an EVM. 

- When the target address in a transaction is a smart contract,  the execution code corresponding to 

  the smart contract is activated and executed on the EVM. 

- The input needed for this execution  is extracted from the **payload field** of the transaction. 
- the Current **state** of the smart contract is the values of the variables defined in it. 
- smart contract state can be updated via its execution. 
- Results of this execution are kept in receipts. A blockchain maintains both the **state hash** and the **receipt hash** (see later). 
- All the transactions generated are validated. 
  - checking the time-stamp and the nonce combination to be valid
  - checking the availability of sufficient fees for execution. 
- Miner nodes in the network 
  - receive,  verify, gather and execute transactions. 
  - The in-work smart contract code is executed by all miners. 
- Validated transactions are broadcast and gathered for block creation. 
- The consensus protocol used is a memory-based rather than a CPU-based proof of work. 



Who pays for all these operations;  validation, verification and consensus?  we'll explore the Incentive Model that answers this question.

## incentive model



- **mining** is the process used to secure the network by validating the computations,  collecting them to form a block, verifying them, and broadcasting it.
- Ethereum also uses a incentive-based model for block creation.



In this lesson we'll explore some relevant concept about fee structure and  the incentive model.



<img src="https://res.cloudinary.com/dri8yyakb/image/upload/v1617260133/Screenshot_from_2021-04-01_08-55-08_odutsw.png" style="zoom:50%;" />



Every action in Ethereum requires crypto fuel, or gas.  

- Gas points are used to specify the fees inside of Ether, for ease of computation using standard values. 

- Gas points allow for  cryptocurrency independent valuation of the transaction fee and computation fees. 
  - Ether, as a cryptocurrency, varies in value with market swings, but  gas points do not vary. Ethereum has specified gas points for each type of operation.  Mining process computes gas points required for execution of a transaction. 
  - If the fee specified and the gas points in the transaction are not sufficient, it is rejected.  This is similar to mailing a letter with insufficient postage
  - The gas points needed for execution must be in the account balance for  the execution to happen.  If there is any amount left over after the execution of a transaction,  it is returned to the originating account.



So far we looked at the gas related items in a transaction,  now let's look at the gas related items in a block. 

**Gas limit** and **gas spent**. 

- **Gas limit** is the amount of gas points available for a block to spend.  For example, if a block specifies a limit of 1 million  units of gas, and a basic Ether transaction fee is 20,000,  this particular Ethereum block can fit about 50 plain Ether transactions.  If we add smart contract transactions also into this block,  that usually requires more gas, and the number of transactions for this block will likely be lower.
- **Gas spent** is the actual amount of gas  spent at the completion of the block creation. 

Now let's look at the mining incentive model.  The proof of work puzzle winner (miner that creates a new block),  is incentivised with the base fees of **three Ethers, and  the transaction fees** in Ethereum blockchain. The winning miner also gets the fees, gas points for  execution of a smart contract transactions.



That there may be other miners who also solve the puzzle besides the winner. These miners will solve the puzzle, but didn't win the block are called **Ommers**.  The blocks created by them are called Ommer Blocks.  These are added as Ommer Blocks, or side blocks, to the main chain. Ommer miners also get a small percentage of the total gas points  as a consolation and for network security. 

Summarizing

- any transaction in Ethereum, including transfer of Ethers,  requires fees or gas points to be specified in the transactions.  
- Miners are paid fees for security, validation,  execution of smart contract, as well as for creation of blocks. 



## resources

[ethereum-docs](https://ethdocs.org/en/latest/introduction/what-is-ethereum.html)