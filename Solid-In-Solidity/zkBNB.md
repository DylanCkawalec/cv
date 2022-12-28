---
title: zkBNB - Solid in Solidity
description: A complete overview of the Solidity programming language. There are many resources out there for Solc programmer, however, I feel like they are boring and they do not encapsulate the full inner workings of the language itself. I feel like it is best to have a working document that can be updated over time. 
lang: en
html: en
author: Dylan Kawalec
---
# zkBNB - Solid in Solidity 


##### *zkBNB - Solid in Solidity* is easy to understand. It uses **metaphors**, **similies**, and **visualizations** that will help you enjoy learning Solidity programming and avoid feeling like you're bashing your head against a wall. Building layer 2 scaling solutions is exciting and will add a lot of value to new and existing projects living in the BNB ecosystem. 🎅
---
## Road to Web3 | *Sections*

###### Web 1.0 : 
- This section provides a general overview of Solidity and Binance Smart Chain, including **installation** instructions and a review of **fundamental concepts** such as types, conditions, and functions.
    - Covering the basics of blockchain ✅
    - Setting up your Binance Work Station ✅
        - setting up a **zkBNB** project
    - Smart contracts on zkBNB.
    - Breaking down variables and functions for BNB
    - Learning how we can be expressive in our code and control our contract's structure
###### Web 2.0 : 
- What we can do on **zkBNB** vs **BSC**
- **Writing**, **testing** and **debugging** smart contracts on zkBNB
- Bridging BEP2<>BEP20<>zkBNB tokens
- (**TBD**)
###### Web 3.0 : 
- Prioritizing **security** and **upgradability** when working with contracts handling large amounts of money in Solidity. In this section, we'll delve into the details of **Assembly code** and **token contracts** to learn various **design patterns** and become proficient in Solidity programming.

    - *Further reading for stress testing zkBNB to build games with added privacy.*  (**TBD**)

        - Exciting use cases that I believe are now avaiable to developers that would like to integrate zkBNB into a new or existing project

![](https://i.imgur.com/iiBcDjD.jpg)


---
# Web 1.0
- Instead of reading the all of ethereum's documentation, the [Bridge Builders DAO](https://bridge-builders.gitbook.io/bbd/welcome-builder-start/learning-the-blockchain/0.1-evm-ethereum) has already synthesized all of it into a single page document that you can read. This will give you a general overview of how most EVM blockchains work. 

## Spawing the chain

Ethereum compatible blockchains such as the **[Binance Smart Chain](https://academy.binance.com/en)**, are decentralized distributed databases (DDD) that have no single point of failure. Servers maintain the state of the DDD using with what's known as a ledger, which records every entry made by anyone in the world. When a person stakes, or invests, in a blockchain, they have shared ownership of it. This shared ownership cannot be changed, making the ledger immutable. In other words, it cannot be altered or tampered with. Additionally, these blockchains are transparent, meaning that all transactions and entries are visible to everyone. They are also resistant to corruption, making them secure and reliable for recording and storing data.

In a blockchain system, accounts update the current state of the ledger, or database, through a process called a transaction. **Smart contracts** are self-executing contracts with the terms of the agreement between buyer and seller being directly written into lines of code. These contracts act as intermediaries for users to interact with the blockchain ledger and facilitate the execution of transactions. Transactions are processed and temporarily separated from the main ledger, and then eventually added back onto the chain, updating the state of the ledger for all users to see. In this way, smart contracts and transactions work together to update and maintain the current state of the blockchain ledger.

Blockchains are designed to be **trustworthy**, **autonomous**, and resistant to the need for intermediaries or middlemen. This means that no one person or group owns the entire chain, and no one person is responsible for managing accounts or processing transactions. Instead, the network of users collectively maintains the integrity and security of the blockchain. Smart contracts are self-executing contracts with the terms of the agreement written into lines of code, and they play a key role in facilitating transactions and interactions on the blockchain. Because they operate independently and do not require a central authority to enforce their terms, smart contracts are often referred to as decentralized autonomous organizations **(DAOs)**.

users sign transactions using a combination of public and private keys, which are used for highly sophisticated cryptographic purposes. This process is commonly referred to as **symmetric** and **asymmetric** key encryption. The private key is a unique code that is used to sign and authorize a transaction, while the public key is a unique code that is used to identify the user and verify the authenticity of the transaction. Together, these keys enable secure and reliable communication and transactions on the blockchain. 

**By the way, never share your private key with anyone, only your public key.** 

Blocks have a *fingerprint* known as a **hash**, which has a fixed length that is formed using the input data being collected in each block in the block chain. This is stored on the blockchain 

- If you want to play with SHA-256, [click here](https://passwords-generator.org/sha256-hash-generator). Try typing in your name and gernating a hash. Change it, and watch the hash change. Then try changing it back to the original input value you started with. 

Every account has a unique finger print. Know one will ever be able to decrypt your hash to discover the original input value, unless you gave it away. This is commonly reffered to as your **key phrase**.

When we make transactions on the blockchain, we use **digital signatures** to prove that the transaction is legitimate and can be trusted. A digital signature is created using a private key, which is a unique code that only the owner of the key knows. To sign a transaction or contract, we use our private key to create a digital signature.

The network of servers validating the blockchain, known as nodes, can then verify the authenticity of the transaction by checking the digital signature against the corresponding public key. The public key is a unique code that is associated with the private key, and it is used to identify the user and verify the authenticity of the transaction. By validating the public key, the nodes can confirm that the transaction was indeed signed by the owner of the private key, and they can trust that the transaction is valid. 

> A digital signature is like a special writing that only you can make.
It's used to prove that you did something online or sent a message.
Your computer uses a special "key" to make the digital signature.
When someone else gets the message or sees what you did, their computer checks the signature.
If the signature is correct, they know it was really you. If not, they might not trust it.

## Binance Governance 
- [Read the BSC white Paper](https://github.com/bnb-chain/whitepaper/blob/master/WHITEPAPER.md)
### [Beacon Chain Governance](https://docs.bnbchain.org/docs/beaconchain/governance)
![](https://i.imgur.com/VN4DHHc.png)
### [Binance Smart Chain Governance](https://docs.bnbchain.org/docs/learn/bsc-gov)
![](https://i.imgur.com/E1VJ2UX.png)



Blockchain technology is designed to be a trustless and fair system for managing assets. Trustless refers to the fact that the system does not rely on any central authority or intermediary to enforce rules or facilitate transactions. Instead, it relies on the collective power of the network of users to maintain the integrity and security of the system. This means that individuals do not have to trust any one person or entity to ensure that their assets are being handled fairly and securely.

"*Radically fair*" refers to the fact that the system is designed to be transparent and unbiased. All transactions and interactions on the blockchain are recorded and visible to all users, and the rules for the system are predetermined and cannot be altered by any single person or group. This ensures that all users are treated equally and that the system operates in a fair and transparent manner.

However, the concept of radical fairness is closely tied to the idea of [**consensus**](https://docs.bnbchain.org/docs/learn/consensus). In BNB blockchain network, consensus refers to the process of **agreeing on the state** of the ledger, including both blocks that have already been stored and blocks that will be stored in the future. There have been many different consensus models proposed by various blockchain networks, each with varying levels of complexity. 


[![Binance Smart Chain Picture](https://i.imgur.com/NtF0s7S.png)](https://docs.bnbchain.org/docs/zkbnb/zkbnb-overview/)

In the case for the Binance Smart Chain, it uses a [**Proof of Authority Stake**](https://docs.bnbchain.org/docs/beaconchain/learn/architecture) consensus, which simply means that validators must verify they are trusted before being issues keys to stake and validate the BNB chain. 

> **Please read the [Bridge Builder DAO](https://bridge-builders.gitbook.io/bbd/welcome-builder-start/learning-the-blockchain/0.1-evm-ethereum) to get more information about how all of this works under the hood for Ethereum's POS network.** 



## Accountability
### Accounts

> **We'll see this keyword `External` in Solidity later.** 

**External account**: This refers to a user who has a public and private key. The first 160 out of the 256 characters of the public key are used for people to share with others, while the private key is kept secret and never shared with others.

- BSC Account:   `0xa19dEf1C91fD63615E03caAF0d5EAF2Eba81fFFc`

This `account` holds a `balance`, and can execute **functions** in **smart contracts**. 

**Contract accounts**:  These do not have a private key, but they do contain code that can be executed if an **external signer** uses the appropriate amount of `gas` to execute the contract on the blockchain. In the case for BSC, you have a 140M gas ceiling per block. 
When people buy things, they perform a **transaction**, which costs a fee that is consumed by miners; that fee is the gas users or contracts spend. 

*Where* or *who* is responsible for paying the fee, is denoted using the `from` keyword. 
Where the transaction's ether is going to, is denoted using the `to` keyword-- and the `value` keyword is the amount of ether being passed between acounts.


---
--- 
--- 
## Testing Smart Contracts
Go to [remix](https://remix-project.org/) and watch [Youtube](https://www.youtube.com/watch?v=WmeWbo7wzGI) to figure out how to use it with other blockchains you want to program for. Or you can make really fast progress and read this [Harmony tutorial](https://bridge-builders.gitbook.io/bbd/welcome-builder-start/building-a-currency/1.2-hrc-20-harmony-token) and launch your first token (STEP-BY-STEP). This process of launching a token on Harmony would be the same as ethereum, or binance; just make sure you are using a BNB wallet when interacting with the code on remix. You can use this faucet to get test BNB tokens 

## First, Hello Solidity.
```solidity!
pragma solidity 0.8.1;

// This is the contract definition
contract HelloSolidity {
  // This is a private state variable
  string private message;

  // This is the constructor function
  constructor() public {
    // Initialize the message variable
    message = "Hello, Solidity, that was super easy...";
  }

  // This is a public function that returns the value of the message variable
  function getMessage() public view returns (string memory) {
    return message;
  }
}

//if you read this line by line, don't try to memorize anything, just read it slowly. You will see how simple it is, even if this new to you. 
```

> Solidity compiles this code into **[byte code](https://medium.com/@eiki1212/explaining-ethereum-contract-abi-evm-bytecode-6afa6e917c3b)**, which is then converted into **[Opcode](https://ethereum.org/en/developers/docs/evm/opcodes/)** instructions that are stored in the stack and processed using memory. After compilation, the memory is discarded and any data in the machine state is transferred to the **World state**, which is the storage associated with the blockchain. 
> To much storage can be expensive, so it is generally best practice to write shorter and simpler contracts to minimize costs! 
> Defining the `pragma` version is also a good practice for ensuring the security of your contract 😉

#### ABI := `external` & `public` functions + (parameters) & `return` types.
- **ABI** is important because it **defines** contracts for what they are, and allows anyone, the callers, to **invoke** the contract **externally**. It's also what makes the contract ***unique***.  


#### Bytecode := Low level instructions for the compiler, which uses Opcode to interpret the meaning of these instructions. 
- later on I'll describe how the compiler works under the hood once we start talking about assembly code, but that's not important right now. 
- Remember **Bytecode** and **ABI**

###### Further reading
>If you want to get a super head start, synthesize any developer portal of your choice, such as [Binance's](https://bnbdev.community) to see how they would summarize their fundamental blockchain concepts. All chains are different, and not all blockchains use Solidity -- check that first to see if this is even worth your time. 

---
## EVM compiler "cliff note"
![](https://i.imgur.com/LzWi2hF.png)
![](https://i.imgur.com/IjxvtSB.png)
![](https://i.imgur.com/sI9Xyo1.png)

--- 


# Building on Binance Smart Chain

BNB has several chains to choose from to build your contracts. 

1. BNB (Binance Beacon Chain)
- This is where the [Binance DEX](https://www.binance.com/en) lives, and where all **staking** and **voting** occurs.

2. [**BSC**](https://www.bnbchain.org/en/developers) (Layer One [Binance Smart Chain](https://docs.bnbchain.org/docs/bnbIntro))
- Any smart contract can be deployed here.


3. [**zkBNB**](https://docs.bnbchain.org/docs/zkbnb/zkbnb-overview/) (Layer Two Zero-Knowledge Rollup Chian)
- Gaming, NFT, AMM & Metaverse chain. This is a performance chain meant to make transactions cheaper and faster, but will only be compatable with *some* contract logic. Read the [zkBNB Docs](https://github.com/bnb-chain/zkbnb/) to learn more. 


4. [**BAS**](https://www.bnbchainlist.org) (Binance Side-Chain)
- "Customizable Layer Two Blockchain". These side-chains can also leverage zkBNB chain as their own rollup system as well, and are essentially copy's of the Binance Smart Chain with limited validator's running the nodes. Side-Chains have the same security features as the Binance Smart Chain. 

5. [TBD] - [The Future](https://docs.bnbchain.org/docs/dev-outlook/scaling)
6. [TBD] - [is Near](https://docs.bnbchain.org/docs/dev-outlook/scaling)
---
### *BNB Architecture Graphics*
![](https://i.imgur.com/Fagvtt2.png)
### [Binance Side-Chain](https://docs.bnbchain.org/docs/BNBSidechain/overview/bs-overview)
![](https://i.imgur.com/ave0esl.png)

### [zkBNB](https://docs.bnbchain.org/docs/zkbnb/zkbnb-overview)
![](https://i.imgur.com/JYZjtY0.jpg)

--- 
---
# Setting up your [Binance Workstation](https://bnbdev.community/community)

In this overview, we will be discussing how to build smart contracts in Solidity for the zkBNB chain. The zkBNB chain is a fast and efficient Layer 2 blockchain that is suitable for use with **non-fungible tokens** (NFTs), **games**, **automated market makers** (AMMs), and **tokens**. The focus of this tutorial will be on creating contracts for these types of assets, as most of the custom Solidity logic is typically used in these types of applications. **zkBNB** has built in liquidity pools, Native Name Services, an NFT marketplace 'out-of-the-box', 10,000 TPS and 100x lower fee's while still using  native BEP20 tokens.

The process of writing a smart contract on the Binance Smart Chain is the same as the process for writing a smart contract on the zkBNB chain. The steps and considerations involved in writing a smart contract are the same for both chains. 

## Important links! 👩🏼‍💻
**Main network**: [zkBNB Main Repository](https://github.com/bnb-chain/zkbnb)
- ["zkBNB SDK"](https://github.com/bnb-chain/zkbnb-go-sdk) : The `ZkBNB Go SDK` provides a thin wrapper around thin all the apis provided by ZkBNB, including a simple key manager for signing txs and sending signed txs to ZkBNB.
- ["Layer 2 ZkBNB Rollup Library"](https://github.com/bnb-chain/zkbnb-crypto): `zkbnb-crypto` is the crypto library for ZkBNB Protocol. It implements rollup block circuit and supports exporting groth16/plonk proving key, verifying key and solidity verifier contract
- [Layer One & Two Communitcation Contract](https://github.com/bnb-chain/zkbnb-contract): The above framework shows that the `zkbnb-contract` is one of the core components, it is the entrance and exit of L2 ecosystem. `zkbnb-contract` achieves full security of the BSC layer 1, and acts as the communication relayer between the zkBNB chain and the BSC chain. It also gives us a "full exit" request in case the user can request through L1 smart contract to withdraw funds if he thinks that his transactions are censored by ZkBNB.

**Test network**: [BSC Testnet](https://testnet.bscscan.com/)

### Scaffold
- [BSC Truffle Starterbox ](https://bnbdev.community/library/scaffolds/seSdZOOFjg) (Good to have)


### Tools
- [Nodereal BNB](https://nodereal.io/bnb-dev-tools) (Custom)
- [zkBNB Wallet](https://test.zkbnbchain.org/wallet)


### Final Project: Full stack zkBNB
- [BSC Full stack guide](https://github.com/bnb-chain/bnb-chain-tutorial/tree/main/01-%20Hello%20World%20Full%20Stack%20dApp%20on%20BSC) (without zkBNB integration)

> It is important to keep the following links open and accessible as you progress through this tutorial. You should have these links open in separate tabs so that you can easily refer to them as needed.

---
### Prepare your zkBNB Workstation
You will need to make sure you have your developer workstation ready to go: Refer to the following packages: 

- instead of using `geth`, we will be using the Binance cli instead.
```
npm install -g @binance-chain/cli
```
- **Node.JS**: 
    - Download the latest stable version of Node.js from the official website (https://nodejs.org/) or using a package manager such as Homebrew (for macOS) or APT (for Linux).
    - Follow the installation instructions provided by the Node.js website or package manager to install Node.js and npm on your system.
    - Once Node.js and npm are installed, you can verify that they are correctly installed by running the following commands:
        ```
        node -v
        ```
        ```
        npm -v
        ```
    - In case you need to change the version of node to a specific version in case this tutorial becomes to outdated, then run the `brew install nvm` and run `nvm use ##.##.##` to change the version of node. You can easily switch between version of node/npm by running `brew switch node 12.22.0`.




- [**Ganache-cli**](https://trufflesuite.com/ganache/) 
    - This is a local blockchain environment tool which we'll use to interact with the binance client's private key to test our application locally. 
    - You're welcome to download the cli version instead of the complete application. However, it is easier to configure tests using the application. It's totally your preference. 
        ```
        npm install -g ganache-cli
        ```
        
- [**Solidity**](https://docs.soliditylang.org/en/latest/solidity-by-example.html)
    - We'll install solidity globally to our system.
        ```
        npm install -g solc
        ```
    - Check to see that it was installed correctly. 
        ```
        solc --version
        ```
    - Keep in mind that these instructions are for installing Solidity globally on your system. If you only want to install Solidity for a specific project, you can use the `npm init` command to create a new `package.json` file for your project and then use npm install to install Solidity as a dependency for your project.
    - if npm is not working, then install it using **homebrew**
        ```
        brew install solidity
        ```
        `solc --version`

- **Wallet**
    * You're welcome to use either **Metamask**, or **trust wallet**. 

    - [Metamask testnet configuration](https://www.coincarp.com/chainlist/binance-smart-chain-testnet/) 

- [**Web3**](https://github.com/web3/web3.js) : the version you will be using will already be configured using `truffle` but you're welcome to install it globally; however, it's not nessesary. 

- **Truffle**: `npm install -g truffle` & `truffle version`

    - If you only want to install Truffle for a specific project, you can use the `npm init` command to create a new `package.json` file for your project and then use npm install to install Truffle as a dependency for your project.



---
# Setting up zkBNB Workstation
1. zkBNB SDK + Truffle + .env, .secret, 
---
--- 
# Smart Contracts on zkBNB


 
---
---
---
---

## Breaking down variables and functions


### State Variables:
**Bool**: A boolean type that can store either "true" or "false". (1 or 0)

**Uint8/256**: An unsigned integer type that can store only positive numbers. The size of the type (8 or 256 bits) determines the range of values it can hold.

**Int8/256**: A signed integer type that can store positive or negative numbers. The size of the type (8 or 256 bits) determines the range of values it can hold.

**bytes**: A fixed-size byte array that can hold up to 32 bytes of data.

**address**: A special type that represents an Ethereum account address. It is a 20-byte value.

**Payable address**: A special type of address that can receive ether through the .send and .transfer methods.

**Enumerations** (enums) are custom data types that represent predefined constants. They must have at least one member and cannot have a semicolon at the end. Enums cannot be declared within functions and can be updated using modifiers.

**Reference types** in Solidity include arrays, structs, and strings. These types are stored in memory and are passed "by reference" when assigned to variables or passed as function arguments.

**Mapping**: A key-value data structure that cannot be declared within functions or used as state variables. Mappings can be "*passed by reference*" in a function if there is a state variable, but they cannot be iterated through using the "=>" operator.

**Array**: A type that can hold a fixed or dynamic number of elements of the same type. Arrays of strings or bytes are considered "***special***" arrays.

**Struct**: A reference type data structure that can hold a combination of different types.
In Solidity, when values are "**passed by value**," the values in the memory location are copied to the target location. When values are "**passed by reference**," a pointer to the memory location is copied, creating a new variable instance that refers to the original data.

### State Variables and their Qualifiers

**Internal**: Cannot be modified by external functions or contracts.
**External**: Can be modified by external functions or contracts through an interface.
**Private**: Owned by the contract and not accessible to derived contracts.
**Public**: Accessible through a "getter" function.

**Modifiers:**
> Constant: Immutable and cannot be modified.
New: Only applies to contracts or arrays, and allows them to be created dynamically.

**Functions**:
>View: Alias for constant functions, which do not modify the contract's state.
Pure: Does not read or write to the contract's state.
Payable: Can accept ether, and will fail if the sender does not provide enough ether.

**Literals**:
>String literals: Surrounded by single or double quotes.
Numeric literals: Integers or floats.
Hexadecimal literals: Prefixed with "0x".

**Arrays**:
>Dynamic arrays: Can be modified using methods such as .pop, .push, and .length (except for strings).
Fixed arrays: Cannot be modified.

**Methods**:
>.balance: Returns the balance of an address type.
.call, .delegateCall, .callcode: Used to call functions on other contracts.
.send, .transfer: Used to send ether to another address.

### Storage and Memory
In Solidity, a **modifier** is a special type of function that is executed before a target function. The underscore character ('_') is used as a placeholder to indicate the target function, and the rest of the code in the modifier is executed before the target function.

The "**payable**" modifier is used to indicate that a function can accept ether as an argument. It is often used in conjunction with the "**require**" keyword in a modifier to check the balance of the sender before executing the function. *The "payable" modifier is usually placed in the return statement for functions*.

The "**msg.sender**" variable represents the address of the sender of the current message or transaction.

In Solidity, there are three types of memory: **storage, memory, and calldata.**

>**Storage**: Global and permanent, with assignments creating a new copy in storage.
**Memory**: Temporary and only exists during the execution of a function. Assignments to memory variables from state variables create a new copy in memory. Assignments of memory variables to other memory variables do not copy the data into storage.
**Calldata:** Contains the arguments of a function and is not modifiable.
The stack is a data structure in Solidity that is used to store state variables and function arguments. It has a depth of 1024 levels, and attempting to go beyond this depth will cause an exception to be thrown.


### Variable composition with functions
In Solidity, a struct is a *custom data* type that consists only of variables and mappings. It is used to group related data together and can be used in place of multiple separate variables.

An **event** is a mechanism in Solidity that allows external calls to be notified about the state of the contract. Events are stored on the blockchain in the "LogsBloom" data structure and can be used to track the history of a contract. The "emit" keyword is used to raise an event and notify external calls.

A **function** in Solidity is a block of code that can be executed by calling it with the "**this**" keyword. There can be only one unnamed function per contract, known as the "**fallback function**," which is executed when no function name is specified. Functions can use the "**return**" keyword to specify a value to be returned to the caller.

Variables declared in function arguments are stored in "*calldata*" or "*memory*" depending on the type of the variable. If a variable is declared within a function, it is stored in "*memory*." If it is a reference type, it must be declared as such. References in functions with "*storage*" should point to state variables in the contract. Arguments supplied by modifiers (callers) are stored in "calldata" or "*memory.*"

The "**keccak256**" function is a cryptographic hash function that generates a hash of the argument passed to it. It is commonly used in Solidity to create unique identifiers or to verify the integrity of data.

## Variables & Functions

# Being expressive in our code and control our contract's structure