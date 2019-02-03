# GOBYTE GRPC-Gateway-HTTP

You will need to deploy a [grpc-gateway](https://github.com/gobytecoin/grpc-gateway/blob/master/README.md)

The grpc-gateway will encode the bytes fields defined in proto into base64 format. For input parameters in bytes format, you should encode in into base64 format, and for output parameters in bytes format, you should decode it into base64 format for subsequent processing. TRON provides a encoding/decoding tool which you can download from https://github.com/tronprotocol/tron-demo/raw/master/TronConvertTool.zip.

```shell
Wallet/getaccount
Function: Returns the account associated with the given address.
Demo: curl -X POST  http://127.0.0.1:18890/wallet/getaccount -d '{"address": "GYgZmb8EtAG27PTQy5E3TXNTYCcy"}'

Wallet/createrawtransaction
Function: create the transaction of a transfer. If the recipient address does not exist, then a corresponding account will be created on the blockchain.
Demo: 
curl -X POST  http://127.0.0.1:18890/wallet/createrawtransaction -d '{"to_address": "GYgZmb8EtAG27PTQy5E3TXNTYCcy", "amount": 1000 }'

Wallet/sendrawtransaction
Function: transaction broadcasting. Transaction needs to be signed before broadcasting.
Parameter: use the signed transaction as the input parameter.

Wallet/gobject vote-alias
Function：Vote on the master node
demo：curl -X POST  http://127.0.0.1:12454/wallet/vote-alias -d '{
"governance-hash":"41d1e7a6bc354106cb410e65ff8b181c600ff14292", 
"funding|valid|delete",
"yes|no|abstain",
"alias-name":"Masternode1"
}'
Parameters：Alias-name is the Masternode's alias name, as setup in the masternode.conf; governance-hash is the hash of the governance object being voted;

Wallet/getnewaddress
Function：Create a new Gobyte address.
Return value：Newly created Gobyte public address.

Wallet/getpeerinfo
Function：List the nodes which the api fullnode is connecting on the network
demo: curl -X POST  http://127.0.0.1:12454/wallet/getpeerinfo
Parameters：None
Return value：List of nodes

Inquire the latest block: wallet/getblockcount
Function: Query the network for the latest block
Parameters: none.
Demo: curl -X POST http://127.0.0.1:18890/wallet/getblockcount

Wallet/getblock
Function：Query block by hash
demo: curl -X POST  http://127.0.0.1:12454/wallet/getblock -d '{"hash" : a654f6a4fa5fafa5}' 
Parameters：Hash is the hash of the block
Return value：specified Block object

Wallet/getblockhash
Function：Query block hash by height
demo: curl -X POST  http://127.0.0.1:12454/wallet/getblockbyid -d '{"value": "1"}'
Parameters：Block height.
Return value：Block hash.

Wallet/gettransaction
Function：Query transaction by ID
demo: curl -X POST  http://127.0.0.1:12454/wallet/gettransaction -d '{"value": "d5ec749ecc2a615399d8a6c864ea4c74ff9f523c2be0e341ac9be5d47d7c2d62"}'
Parameters：Transaction ID.
Return value：Transaction information.

Wallet/masternodelist
Function：Query the list of Master Nodes
demo: curl -X POST  http://127.0.0.1:12454/wallet/masternodelist
Parameters：None
Return value：List of all Master Nodes

Signing: Wallet/signrawtransaction
Function：Sign the transaction, the api has the risk of leaking the private key, please make sure to call the api in a secure environment
demo: curl -X POST  http://127.0.0.1:12454/wallet/signrawtransaction -d '{
"transaction" : {"txID":"454f156bf1256587ff6ccdbc56e64ad0c51e4f8efea5490dcbc720ee606bc7b8","raw_data":{"contract":[{"parameter":{"value":{"amount":1000,"owner_address":"41e552f6487585c2b58bc2c9bb4492bc1f17132cd0","to_address":"41d1e7a6bc354106cb410e65ff8b181c600ff14292"},"type_url":"type.googleapis.com/protocol.TransferContract"},"type":"TransferContract"}],"ref_block_bytes":"267e","ref_block_hash":"9a447d222e8de9f2","expiration":1530893064000,"timestamp":1530893006233}},"privateKey": "your private key"}
}'
Parameters：Transaction is a contract created by http api, privateKey is the user private key
Return value：Signed Transaction contract data
Warning: Please control risks when using this API. To ensure environmental security, please do not invoke APIs provided by other or invoke this very API on a public network.

Inquire transactions taken by an address: /walletextension/getreceivedbyaddress
Demo: curl -X POST http://127.0.0.1:18890/walletextension/getreceivedbyaddress -d '{"address" : "GYgZmb8EtAG27PTQy5E3TXNTYCcy"}'
Parameters: address is in base64 format;

Inquire transaction by transaction hash: /wallet/gettransaction
Function：Query transaction by ID
demo: curl -X POST  http://127.0.0.1:12454/wallet/gettransaction -d '{"value": "d5ec749ecc2a615399d8a6c864ea4c74ff9f523c2be0e341ac9be5d47d7c2d62"}'
Parameters：Transaction ID.
Return value：Transaction information.

Create address: /wallet/getnewaddress
Function: Generates a random private key and address pair
demo：curl -X POST -k http://127.0.0.1:12454/wallet/getnewaddress
Parameters: no parameters.
Return value：value is the new public address.
Warning: Please control risks when using this API. To ensure environmental security, please do not invoke APIs provided by other or invoke this very API on a public network.

GBX easy transfer: /wallet/sendfrom
Function: Easily transfer from an account to a gobyte address.
Demo: curl -X POST http://127.0.0.1:12454/wallet/sendfrom -d '{"fromaccount": "DefaultAddress","toAddress": "GJ84thwcN3VoJAFbmBtZ4gXvveZrRuTm3D", "amount":10}'
Parameters: fromaccount is the address/label/wallet name. toAddress is the recipient address; amount is the amount of GBX to transfer.
Warning: Please control risks when using this API. To ensure environmental security, please do not invoke APIs provided by other or invoke this very API on a public network.


```
