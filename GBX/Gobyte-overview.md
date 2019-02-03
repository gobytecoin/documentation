# Full Overview of GOBYTE

## 1.1 Project repositories
### https://github.com/gobytecoin
- [GoByte Wallet](https://github.com/gobytecoin/gobyte) - main repository for GBX wallets
- [Documentation](https://github.com/gobytecoin/Documentation) - all documentation
- [GoByteDeployment](https://github.com/gobytecoin/GoByteDeployment) - deployment scripts and config files

## 1.2 Block explorer
- https://explorer.gobyte.network/

## 1.3 GBX consensus algorithm
GBX adopts a PoW algorithm called NeoScrypt.

## 1.4 Block Producing Speed of GBX
The network currently produces 1 block per 120 seconds.

## 1.5 Transaction model
The adopted transaction model is the UTXO model. The smallest unit of GBX is bit, 1 GBX=10,000,000 bits.

## 1.6 Account model
One account has only one corresponding address, which is needed for transfers. The multi-signature mechanism is not yet implemented on the current version of network. There are three ways to create an account on the main blockchain.
```
a.  Create account with an existing account.
b.  Send GBX to a new address to create account.
c.  Send tokens to a new address to create account.
```

# 2. GoByte’s network structure

## 2.1 Node types
There are three types of nodes on GoByte’s network: Masternode(which require 1,000 GBX locked), Full Node and simple node.

Node: A client that operates on the network which is able to send and receive transactions (GoByte Android Wallet, GoByte Pay wallet, etc.)

Full node: A client that operates on the network and maintains a full copy of the blockchain. Sends and receives transactions as well, updates the blockchain with block entries and confirmations from miners. (GoByte-Qt)

Masternode: A client that does all of the above and also enables/performs additional functions, see here. Gets paid a portion of the block reward. (GoByte-Qt daemon configured to act as Masternode)

## 2.2 Mainnet and testnet

### Mainnet
- Block Explorer: https://explorer.gobyte.network/
- Config: --

### Testnet
- Block Explorer: http://texplorer.gobyte.network/
- Config: --

# 3. Operation of node

## 3.1 Recommended hardware specifications
```
Minimum specifications for full node deployment
CPU：2-core
RAM：2G
Bandwidth：100M
DISK：1T
Recommended specifications for full node deployment
CPU：8-core or more 
RAM：16G or more 
Bandwidth：500M and more
DISK：10T or more

Minimum specifications for Master node deployment
CPU：2-core
RAM：2G
Bandwidth：100M
DISK：1T
Recommended specifications for Master node deployment
CPU：8-core or more
RAM：16G or more
Bandwidth：500M and more
DISK：10T or more

DISK capacity depends on the actual transaction volume after deployment, but it’s always better to leave some excess capacity.
```

## 3.2 Start the full node and Master node
Please follow the guide here to configure and deploy both nodes: 
- Master: ???
- Full: ???

We also provide a script to deploy Master node:
- https://github.com/gobytecoin/masternode-script-gobyte/blob/master/README.md

# 4. GoByte API
The GoByte Nodes support both a gRPC Service and a HTTP Gateway

## 4.1 API Definition
Please see the isnsight API.
- [Insight API](https://github.com/gobytecoin/insight-api-gobyte/blob/master/README.md)

## 4.2 Explanation of APIs
### 4.2.1 gRPC interface
The Full Node and Master nodes each run a gRPC service that you can connect to.

- [gRPC Tutorial](https://grpc.io/docs/)
- [gRPC API](https://github.com/tronprotocol/Documentation/blob/master/English_Documentation/TRON_Protocol/TRON_Wallet_RPC-API.md) -> Edit


### 4.2.2 HTTP Interface
The FullNode and MasterNode both have an HTTP Service running on them. All parameters are encoded as `HEX` and returned as Hex or `base58check`. If you're trying to pass an address in, please decode from `base58check` and convert it to `HEX`.

- [HTTP Service API](https://github.com/D0WN3D/Documentation/blob/master/GBX/Gobyte-http.md) -> Edit

- [Address DEBUG Tool](https://paper.gobyte.network/) -> Use "Wallet Details"

# 5. Transaction Fees
To keep the network operating smoothly, GoByte network requires every account to pay a fee for every transaction. 

The fee schedule for GoByte 0.13.x is as follows:

Transaction type	Recommended fee	Per unit
Standard transaction	.00001 GBX	Per kB of transaction data
InstantSend autolock	.00001 GBX	Per kB of transaction data
InstantSend	.0001 GBX	Per transaction input
PrivateSend	.001 GBX	Per 10 rounds of mixing (average)

See also: ???

## 5.1 Definition of Private Send
PrivateSend gives you true financial privacy by obscuring the origins of your funds. 
All the GoByte in your wallet is comprised of different “inputs”, which you can think of as separate, discrete coins. 
PrivateSend uses an innovative process to mix your inputs with the inputs of two other people, without having your coins ever leave your wallet. You retain control of your money at all times.

The PrivateSend process works like this:

PrivateSend begins by breaking your transaction inputs down into standard denominations. These denominations are 0.001, 0.01, 0.1, 1 and 10 GBX – much like the paper money you use every day.
Your wallet then sends requests to specially configured software nodes on the network, called “masternodes”. 
These masternodes are informed then that you are interested in mixing a certain denomination. 
No identifiable information is sent to the masternodes, so they never know “who” you are.
When two other people send similar messages, indicating that they wish to mix the same denomination, a mixing session begins. 
The masternode mixes up the inputs and instructs all three users’ wallets to pay the now-transformed input back to themselves. 
Your wallet pays that denomination directly to itself, but in a different address (called a change address).
In order to fully obscure your funds, your wallet must repeat this process a number of times with each denomination. Each time the process is completed, it’s called a “round”. Each round of PrivateSend makes it exponentially more difficult to determine where your funds originated. The user may choose between 1-16 rounds of mixing.
This mixing process happens in the background without any intervention on your part. When you wish to make a transaction, your funds will already be anonymized. No additional waiting is required.

```
Note that PrivateSend transactions will be rounded up so that all transaction inputs are spent. 
Any excess GoByte will be spent on the transaction fee.

IMPORTANT: Your wallet only contains 1000 of these “change addresses”. 
Every time a mixing event happens, one of your addresses is used up. 
Once enough of them are used, your wallet must create more addresses. 
It can only do this, however, if you have automatic backups enabled. 
Consequently, users who have backups disabled will also have PrivateSend disabled.
```

## 5.2 Definition of Instant Send
Traditional decentralized cryptocurrencies must wait for certain period of time for enough blocks to pass to ensure that a transaction is both irreversible and not an attempt to double-spend money which has already been spent elsewhere. This process is time-consuming, and may take anywhere from 15 minutes to one hour for the widely accepted number of six blocks to accumulate. Other cryptocurrencies achieve faster transaction confirmation time by centralizing authority on the network to various degrees.

GoByte suffers from neither of these limitations thanks to its second-layer network of masternodes. Masternodes can be called upon to form voting quorums to check whether or not a submitted transaction is valid. If it is valid, the masternodes “lock” the inputs for the transaction and broadcast this information to the network, effectively promising that the transaction will be included in subsequently mined blocks and not allowing any other spending of these inputs during the confirmation time period.

InstantSend technology will allow for cryptocurrencies such as GoByte to compete with nearly instantaneous transaction systems such as credit cards for point-of-sale situations while not relying on a centralized authority. Widespread vendor acceptance of GoByte and InstantSend could revolutionize cryptocurrency by shortening the delay in confirmation of transactions from as long as an hour (with Bitcoin) to as little as a few seconds.
 
# 6. User address generation
## 6.1 Algorithm description
1. First generate a key pair and extract the public key (a 64-byte byte array representing its x,y coordinates). 
2. Hash the public key using sha3-256 function and extract the last 20 bytes of the result. 
3. Add `5` to the beginning of the byte array. Length of the initial address should be 21 bytes. 
4. Hash the address twice using sha256 function and take the first 4 bytes as verification code. 
5. Add the verification code to the end of the initial address and get an address in base58check format through base58 encoding. 
6. An encoded mainnet address begins with G and is 34 bytes in length.
```
Please note that the sha3 protocol we adopt is KECCAK-256.
```

## 6.2 Mainnet addresses begin with G
```
    address = 5||sha3[12,32): 53a523b449890854c8fc460ab602df9f31fe4293f 
    sha256_0 = sha256(address): 06672d677b33045c16d53dbfb1abda1902125cb3a7519dc2a6c202e3d38d3322 
    sha256_1 = sha256(sha256_0): 9b07d5619882ac91dbe59910499b6948eb3019fafc4f5d05d9ed589bb932a1b4 
    checkSum = sha256_1[0, 4): 9b07d561 
    addchecksum = address || checkSum: 453a523b449890854c8fc460ab602df9f31fe4293f9b07d561 
    base58Address = Base58(addchecksum): GJCnKsPa7y5okkXvQAidZBzqx3QyQ6sxMW
```

## 6.3 Java code demo
See: ???

# 7. Transaction signing
See: https://github.com/tronprotocol/Documentation/blob/master/English_Documentation/Procedures_of_transaction_signature_generation.md
Edit This

# 8. Calculation of transaction ID
Hash the Raw data of the transaction.
in java
```
Hash.sha256(transaction.getRawData().toByteArray())
```
in php  by William
```
try {
      $request = new \Protocol\NumberMessage(); 
      $request->setNum(319139);
      list($reply, $status) = $fullnode->GetBlockByNum($request)->wait();
      $i=0;
      foreach($reply->getTransactions() as $trans){
        echo $i++;
        echo ": ";
        echo hash("sha256", $trans->getRawData()->serializeToString());
        echo "\n";
      }
    } catch (Exception $e) {
        echo 'Caught exception: ',  $e->getMessage(), "\n";
    }
```

# 9. Calculation of block ID
Block ID is a combination of block height and the hash of the blockheader’s raw data. To get block ID, first hash the raw data of the blockheader and replace the first 8 bytes of the hash with the blockheight, as the following:
```
private byte[] generateBlockId(long blockNum, byte[] blockHash) {
 byte[] numBytes = Longs.toByteArray(blockNum);
 byte[] hash = blockHash;
 System.arraycopy(numBytes, 0, hash, 0, 8);
 return hash;
}
```
BlockHash is the hash of the raw data of the blockheader, which can be calculated as the following:
```
Sha256Hash.of(this.block.getBlockHeader().getRawData().toByteArray())
```
# 10. Construction and signature of transaction
Based on your own needs there are two methods to construct a transaction. You can either invoke the gRPC / HTTP API through a full node to build the transaction externally, or create the transaction locally.

## 10.1 Invoke APIs on the full node
You can construct transactions with corresponding APIs.

- gRPC API: https://github.com/tronprotocol/Documentation/blob/master/English_Documentation/TRON_Protocol/TRON_Wallet_RPC-API.md
- HTTP API: https://github.com/tronprotocol/Documentation/blob/master/TRX/Tron-http.md
Edit This!

## 10.2 Local construction
Based on your method of constructing a transaction you are required to populate all fields of a transaction to construct it locally. Please note that you will need to configure the details of reference block and expiration, so you will need to connect to the mainnet during transaction construction. We advise that you set the latest block on the full node as your reference block and production time of the latest block+N minutes as your expiration time. N could be any number you find fit. The backstage condition is `Expiration > production time of the latest block and Expiration < production time of the latest block + 24 hours`. If the condition is fulfilled, then the transaction is legitimate, and if not, the transaction is expired and will not be acknowledged by the network.
A method of setting reference block: set RefBlockHash as subarray of newest block's hash from 8 to 16, set BlockBytes as subarray of newest block's height from 6 to 8. [The demo code](https://github.com/tronprotocol/wallet-cli/blob/master/src/main/java/org/tron/demo/TransactionSignDemo.java) is as follows:  
```
 public static Transaction setReference(Transaction transaction, Block newestBlock) {
    long blockHeight = newestBlock.getBlockHeader().getRawData().getNumber();
    byte[] blockHash = getBlockHash(newestBlock).getBytes();
    byte[] refBlockNum = ByteArray.fromLong(blockHeight);
    Transaction.raw rawData = transaction.getRawData().toBuilder()
        .setRefBlockHash(ByteString.copyFrom(ByteArray.subArray(blockHash, 8, 16)))
        .setRefBlockBytes(ByteString.copyFrom(ByteArray.subArray(refBlockNum, 6, 8)))
        .build();
    return transaction.toBuilder().setRawData(rawData).build();
  }
```
Look at a method of setting Expiration and transaction timestamp:
```
  public static Transaction createTransaction(byte[] from, byte[] to, long amount) {
    Transaction.Builder transactionBuilder = Transaction.newBuilder();
    Block newestBlock = WalletClient.getBlock(-1);

    Transaction.Contract.Builder contractBuilder = Transaction.Contract.newBuilder();
    Contract.TransferContract.Builder transferContractBuilder = Contract.TransferContract
        .newBuilder();
    transferContractBuilder.setAmount(amount);
    ByteString bsTo = ByteString.copyFrom(to);
    ByteString bsOwner = ByteString.copyFrom(from);
    transferContractBuilder.setToAddress(bsTo);
    transferContractBuilder.setOwnerAddress(bsOwner);
    try {
      Any any = Any.pack(transferContractBuilder.build());
      contractBuilder.setParameter(any);
    } catch (Exception e) {
      return null;
    }
    contractBuilder.setType(Transaction.Contract.ContractType.TransferContract);
    transactionBuilder.getRawDataBuilder().addContract(contractBuilder)
        .setTimestamp(System.currentTimeMillis())//timestamp should be in millisecond format
        .setExpiration(newestBlock.getBlockHeader().getRawData().getTimestamp() + 10 * 60 * 60 * 1000);//exchange can set Expiration by needs
    Transaction transaction = transactionBuilder.build();
    Transaction refTransaction = setReference(transaction, newestBlock);
    return refTransaction;
  }
```
## 10.3 Signature
After a transaction is constructed, it can be signed using the ECDSA algorithm. For security reasons, we suggest all exchanges to adopt offline signatures. 

https://github.com/tronprotocol/Documentation/blob/master/English_Documentation/TRON_Protocol/Procedures_of_transaction_signature_generation.md


## 10.4 Demo
The demo for local transaction construction and signing can be found at:
https://github.com/tronprotocol/wallet-cli/blob/master/src/main/java/org/tron/demo/TransactionSignDemo.java.


# 11. Master Nodes and Voting
The Master Nodes(MN) take important roles to build and operate on GoByte network such as block validation and transaction packing. They receive some GBX as rewards. Every 120 seconds a new block is generated. The MNs receive 70% GBX of the reward and transaction fees per block in sequence. This means that the MNs will be rewarded over 8.6625 GBX per block.

All GBX holders can vote for governance objects as long as they have a Master Node available. Master Node can be activated by freezing 1,000 GBX. To vote for governance objects you can use your favorite wallet or [GoByte Pay, the official Web module](https://portal.gobytepay.com/)

See also: "Add Guide How To Vote"


# 12. Relevant files
See also: https://github.com/tronprotocol/Documentation#documentation-guide
