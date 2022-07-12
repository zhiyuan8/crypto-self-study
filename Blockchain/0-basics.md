# Terminology
- blockchain : **a blockchain provides coordination between many parties, when there is no single trusted party.**  
  - If there is trusted party, no need for blockchain. 


# blockchain layer:  
```
user facing tools (cloud server)
application layer (Dapps, smart contracts)
compute layer (blockchain computer)
consensus layer
```
![DeFi layer](/img/DeFi-layer.png)

# Layer 1 : consensus layer
A **public append-only data structure**
- persistence : once added, data can never be removed （achieved by replication).  
- consensus : 共识 all honest participants have same data.    
- liveness : honest participants can add new transactions.    
- open : anyone can add data. Not just authorized participants.    


- How are blocks added to chain:  
1. A,B,C sign transactions using their secret keys
2. They sign their transactions to the blockchain network which is a collections of miniers
3. gosip protocol replicates and propogates all these transactions throughout the network
4. By leader election mechanism, a miner gets elected to create the next block.
5. The leader takes the current pending transaction, then he posts this block onto blockchain, gets Ethereum reward.
6. The other miniers look at that block and they verify that block is valid.  


![blockchain](/img/blockchain.png)

![blockchain](/img/blockchain2.png)

# Layer 2 : compute layer (blockchain computer)
DAPP logic is encoded in a program that runs on blockchain.  
- Rules are enforced by a public program (public source code)
  - transparency : no single trusted 3rd party 
DAPP program is executed by parties who create new blocks.
- public verifiability : everyone can verify state transactions


# Layer 3 : App layer : DApps
DApps run on blockchain computer.    
Dapps are interfaces that interact with the blockchain through the use of smart contracts. From the front, Dapps look and behave like regular web and mobile applications, except that they interact with a blockchain and in different ways.  

# Layer 4 : UI layer : user facing servers  
![DeFi ecosystem](/img/DeFi-ecosystem.png)


# Important cryptographic primitives


## 1. Collision resistant hash functions and Merkle trees
- H is CRH : hash function is a collusion resistant hash function H.  
- instead of writing transaction S to the blockchain, can just write commit(S) to chain.   
```
Example : SHA-256 { x : len(x)< 2^64 bytes } -> { 0 , 1 } ^ 256
```
- Application
  - checksum : check whether 2 data are same
  - committing to a list (of transactions) : use "Merkle tree", a tree of hashes
  - 32 byte root


- verify one trasaction 
  - Alice has a large file m, she publishes h = H(m) (32bytes)  
  - Bob has h, later Alice sends large file m' s.t. H(m') = h. 
  - H is CRH (collision-resistent hashing). Bob is convinced that ```m = m'```   
  - ```h = H(m)``` is a binding commitment to m. Otherwise, h may leakage information about m.  


- verify a list of trasaction  
  - Alice has S = (m1,m2, ... , mn)  
  - Bob to prove S[4] = m4, he needs:  
```
y2 = H(m3,m4)  
y5 = H(y1,y2)  
h' = H(y5,y6)  
accept if h = h'  
```

![Merkle tree](/img/Merkle_tree.png)


## 2. digital signatures
To authorize and prove a transaction.  
- discrete-log signatures
  - short sigs (48 or 64 bytes) and public keys (32 bytes)
  - Bitcoin, Ethereum
- BLS signatures
  - 48 bytes, aggregtable, easy threshold
  - Ethereum 2.0

![digital signature](/img/digital-signature.png)


## 3. zk-SNARK 零知识简洁的非交互知识论证  
zk-SNARK stands for : 'Zero-Knowledge Succinct Non-Interactive Argument of Knowledge' 零知识简洁的非交互知识论证   
Used for scaling and privacy.  
```
C : a program that always terminates in <= B steps
x : public input to C
w : private input to C
prover (C,x,w) - short proof pi -> (C,x)
```
main point : verifier's runtime is *much less* than running C.   


# 4. scaling blockchain
- blockchain transaction rate:
  - Bitcoin 5 Tx / sec , Ethereum 20 Tx / sec  
  - Visa (centralized) network 24,000 Tx / sec  
  - gas price / Tx fees : $2 ~ $60 / Tx  

- scaling approaches:
  - faster concensus, mordern blockchains (Solana, polkadot)
  - payment channels : most Tx are off chain peer-to-peer (Lightening)
  - Layer 2 approaches : 
    - batch many Tx into a single Tx
    - **zxRollup** , **Optimistic Rollup**
  - Sidechains : **Polygon** and others

- HTLC logic : hashed timelock contract
  - two ways to close channel


## 4.1 ZK Rollup
standard L1 chains : **every** miner must verify **every** posted Tx.   
Ethereum 1000X processing time improve : SNARK proof  
- zkrollup
  - transactions within a Rollup system is easy
  - moving funds in and out of Rollup system (L1<=> L2) is more expensive
    - requires posting more data on L1 network => higher Tx fee
  - moving funds from one Rollup system to another (L2 <=> L2)
    - either via L1 network (expensive) or via a direct L2 <=> L2 bridge (cheap)

L1 Ethereum to L2 zkRollup  
zkEVM. 
Solidity compatibility : coordinator can produce a SNARK proof for the execution of a short solidity program.  
- easy to migrate a DAPP from **L1 Ethereum to L2 zkRollup**
- reduce Tx fees and increase Tx rate compared to L1


## 4.2 Optimistic Rollup  
- same principal as zkRollup, but no SNARK proofs. less work for server.  
- Instead, coordinator posts Tx data on chain without a proof, then give a few days for validators to complain
  - If a posted Tx is invalid : anyone can submit a **fraud proof** and win a reward. Rollup server gets slashed.  
  
## 4.3 Data availability : zkSync vs zkPorter
If coordinator dies, new coordinator needs all current account information.   
- zkSync : store all Tx data on blockchain (Ethereum).
  - higher gas fee, good for high value assets.
- zkPorter : store all Tx data on a new blockchain

# Interoperability & Composability
- Interoperability : Move assets from one chain to another, because a user owns funds / assets on one blockchain system. 
  - via bridges and pegged coin   
  - cross-chain protocols: XCMP, IBC...   
- Composability : enable a DAPP on one blockchain to call a DAPP on another.  
- federated bridge


