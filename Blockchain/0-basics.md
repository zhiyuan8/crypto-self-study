# Terminology
blockchain : a blockchain provides coordination between many parties, when there is no single trusted party.  

blockchain layer:  
```
user facing tools (cloud server)
application layer (Dapps, smart contracts)
compute layer (blockchain computer)
consensus layer
```


# consensus layer
A **public append-only data structure**
- persistence : once added, data can never be removed （achieved by replication).  
- consensus : 共识 all honest participants have same data.    
- liveness : honest participants can add new transactions.    
- open : anyone can add data. Not just authorized participants.    

informal, not focus of this class.    

- How are blocks added to chain:  


# compute layer (blockchain computer)
transparency  
public verifiability  

# App layer : DApps
DApps run on blockchain computer.  

# UI layer : user facing servers  


Compound  

Uniswap  

Custodial services  

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




