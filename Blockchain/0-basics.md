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

# Layer 2 : compute layer (blockchain computer)
DAPP logic is encoded in a program that runs on blockchain.  
- Rules are enforced by a public program (public source code)
  - transparency : no single trusted 3rd party 
DAPP program is executed by parties who create new blocks.
- public verifiability : everyone can verify state transactions


# Layer 3 : App layer : DApps
DApps run on blockchain computer.  

# Layer 4 : UI layer : user facing servers  
![DeFi ecosystem](/img/DeFi-ecosystem.png)


# Cryptography background  
- H is CRH : hash function is a collusion resistant hash function H.  
```
Example : SHA-256 { x : len(x)< 2^64 bytes } -> { 0 , 1 } ^ 256
```
- Application
  - checksum : check whether 2 data are same
  - committing to a list (of transactions) : use "Merkle tree", a tree of hashes
  - 32 byte root

![Merkle tree](/img/Merkle_tree.png)

# digital signature
- discrete-log signatures
  - short sigs (48 or 64 bytes) and public keys (32 bytes)
  - Bitcoin, Ethereum
- BLS signatures
  - 48 bytes, aggregtable, easy threshold
  - Ethereum 2.0
- SNARK proof

# scaling blockchain
transaction rate:
- Bitcoin 5 Tx / sec , Ethereum 20 Tx / sec  
- Visa (centralized) network 24,000 Tx / sec  
- gas price / Tx fees : $2 ~ $60 / Tx  


scaling approaches:
- faster concensus
- payment channels : most Tx are off chain peer-to-peer
- Layer 2 approaches : zxRollup , Optimistic Rollup
- Sidechains : Polygon and others

# scaling Etherum using Rollup
main tool : SNARK  
```
C : a program that always terminates in <= B steps
x : public input to C
w : private input to C
prover (C,x,w) - short proof pi -> (C,x)
```
main point : verifier's runtime is *much less* than running C.   

- zkrollup
  - transactions within a Rollup system is easy
  - moving funds in and out of Rollup system (L1<=> L2) is more expensive
    - requires posting more data on L1 network => higher Tx fee
  - moving funds from one Rollup system to another (L2 <=> L2)
    - either via L1 network (expensive) or via a direct L2 <=> L2 bridge (cheap)

zkEVM




