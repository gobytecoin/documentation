# GOBYTE Wallet RPC-API

## For the specific definition of API, please refer to the following link:  
https://github.com/gobytecoin/gobyte/tree/master/src/rpc

## Frequently used APIs:
1. Get general info of the wallet (similar to bitcoin getinfo)  
getinfo 
2. Get balance of an address (similar to bitcoin getbalance)  
getbalance
3. Create a new address (similar to bitcoin getnewaddress)  
You can create an address at the local system.  
And you can create a new address on blockchain by calling rpc api getnewaddress.
4. Retrieve the list of transaction history by address (similar to bitcoin listtransactions)  
listtransactions
5. check address is valid or not (regex or API command)  
+ Local check--- After decode58check at local, you can get a 21-byte byte array starting with G (mainnet) or n (testnet).   
+ If you want to verify whether an address exists on the blockchain, you can call GetAccount.

## 1. Getting account information

1.1	Interface statement  
rpc GetAccount (Address) returns (Account) {};  
1.2	Nodes  
Any node. 
1.3	Parameters  
Address: type in the address.  
1.4	Returns  
Account: returns the address label.  
1.5	Functions  
Display teh label of the address in account return.

## 2. GBX transfer

2.1	Interface statement  
rpc sendtoaddress (gobyteaddress) (amount) (comment/comment-to/subtractfeefromamount/use_is/use_ps) returns (Transaction)　{};  
2.2	Node  
Any node.  
2.3	Parameters  
gobyteaddress: addresses of the recipient.  
amount: amount of transfer (in GBX).  
comment:(string, optional) A comment used to store what the transaction is for.   
comment-to:(string, optional) A comment to store the name of the person or organization to which you're sending the transaction.  
subtractfeefromamount:(boolean, optional, default=false) The fee will be deducted from the amount being sent.   
use_is:(bool, optional) Send this transaction as InstantSend (default: false)   
use_ps:(bool, optional) Use anonymized funds only (default: false)  
2.4	Returns   
Transaction: returns transaction id of the transfer;  
2.5	Function    
Transfer. Creation of a transaction of transfer.  

## 3. Transaction broadcasting

3.1	Interface statement  
rpc sendrawtransaction (hexstring) returns (hex) {};  
3.2	Node  
Any node. 
3.3	Parameters  
hexstring:(string, required) The hex string of the raw transaction. 
3.4	Returns  
hex: (string) The transaction hash in hex. Note: return of success doesn’t necessarily mean completion of transaction.  
3.5	Function  
Transfer. Sending signed transaction information to node, and broadcasting it to the entire network after masternode verification.

# 4. Vote
4.1 Interface statement
rpc gobject (vote-alias|vote-many|vote-conf) (governance-hash) (funding|valid|delete) (yes|no|abstain) [optional:alias-name] returns (Success/Failed){};  
4.2 Node
Masternode only.  
4.3 Parameters
vote-alias: Vote on a governance object by masternode alias (using masternode.conf setup).
alias-name: Name set inside masternode.conf setup.
vote-many: Vote on a governance object by all masternodes (using masternode.conf setup)
vote-conf: Vote on a governance object by masternode configured in gobyte.conf
governance-hash: Hash code of the proposal.
4.4 Returns
Success/Failed: returns Vote submited successfully / Vote failed.  
4.5 Function
Vote. Masternode holders can only vote for proposals, with no more votes than the amount of Masternodes they hold.

## 8. Query of list of Master Nodes  
8.1 Interface statement
rpc masternodelist (EmptyMessage) returns (MasternodeList) {};  
8.2 Nodes
All nodes.
8.3 Parameters
EmptyMessage: null.  
8.4 Returns
MasternodeList: list of masternodes including detailed information of their status.  
8.5 Function
Query of all masternodes prior to voting returning detailed information on each masternode for user's reference.

## 13. Query of all peers
13.1 Interface statement
rpc getpeerinfo (EmptyMessage) returns (NodeList) {};  
13.2 Nodes
All nodes.
13.3 Parameters
EmptyMessage: null.  
13.4 Returns
NodeList: returns a list of nodes, including their IPs and ports.  
13.5 Function
Listing the IPs and ports of connected nodes.

## 18. Get current block
18.1 Interface statement
rpc getblockcount (EmptyMessage) returns (Block) {};  
18.2 Nodes
All nodes.
18.3 Parameters
EmptyMessage: null.  
18.4 Returns
Block: information on current block. 
18.5 Function
Inquire the latest block.

## 19. Get block hash by block index
19.1 Interface statement
rpc getblockhash (index) returns (BlockHash) {};  
19.2 Nodes
All nodes.  
19.3 Parameters
index: block height.  
19.4 Returns
BlockHash: block hash information.  
19.5 Function
Returning the block hash at designated height.

## 21. Query of in-wallet transaction by ID
21.1 Interface statement
rpc gettransaction (txid) returns (TransactionDetails) {};  
21.2 Node
All nodes.  
21.3 Parameters
txid: transaction ID or Hash.  
21.4 Returns
TransactionDetails: Queried transaction.  
21.5 Function
Query of transaction details by ID which is the Hash of transaction.

## 24. Query of transactions in and out by address
24.1 Interface statement
rpc getaddresstxids (Address) returns (TransactionList) {};  
24.2 Node
All nodes.(requires addressindex to be enabled)   
24.3 Parameters
Address: The address you want to check.  
24.4 Returns
TransactionList: transaction list.  
24.5 Function
Query of all transactions made by one given address.

## 32. Transaction signing  
32.1 Interface statement  
rpc signrawtransaction (hexstring) returns (TransactionHex) (Complete) (Errors) () {};  
32.2 Node  
Any node.  
32.3 Parameters  
hexstring: Transaction to be signed and the private key to sign with.  
32.4 Returns  
TransactionHex: The hex-encoded raw transaction with signature(s).
Complete: true|false, (boolean) If the transaction has a complete set of signatures.
Errors: (json array of objects) Script verification errors (if there are any).

## 33. Address and private key creation
33.1 Interface statement  
rpc getnewaddress (AddressLabel) returns (Address) {};  
33.2 Node  
Any Node.  
33.3 Parameters  
AddressLabel: Label shown inside the wallet.  
33.4 Returns  
Address: address.

## 35. Generate address by importing a private key  
35.1 Interface statement  
rpc importprivkey (PrivateKey) returns (PublicAddress) {};  
35.2 Nodes  
FullNode and SolidityNode.  
35.3 Parameters  
PrivateKey: Private Key.  
35.4 Returns  
PublicAddress: generate the public address according to the private key.  
35.5 Function  
Address and private key usage. Please invoke this API only on a trusted offline node to prevent private key leakage.
