#  GOBYTE HTTP Gateway interface

Configure the ports for the nodes by modifying these ports in both configuration files.

```

  node {
  ...
    http {
      fullNodePort = 12454
    }
```

# FullNode Interface
The default http port on FullNode is 12454.

```

/wallet/createrawtransaction
Function：Creates a transaction of transfer. If the recipient address does not exist, a corresponding account will be created on the blockchain.
demo: curl -X POST  http://127.0.0.1:12454/wallet/createrawtransaction -d '{"to_address": "41e9d79cc47518930bc322d9bf7cddd260a0260a8d", "owner_address": "41D1E7A6BC354106CB410E65FF8B181C600FF14292", "amount": 1000 }'
Parameters：To_address is the transfer address, converted to a hex string; owner_address is the transfer transfer address, converted to  a hex string; amount is the transfer amount
Return value：Transaction contract data

/wallet/signrawtransaction
Function：Sign the transaction, the api has the risk of leaking the private key, please make sure to call the api in a secure environment
demo: curl -X POST  http://127.0.0.1:12454/wallet/signrawtransaction -d '{
"transaction" : {"txID":"454f156bf1256587ff6ccdbc56e64ad0c51e4f8efea5490dcbc720ee606bc7b8","raw_data":{"contract":[{"parameter":{"value":{"amount":1000,"owner_address":"41e552f6487585c2b58bc2c9bb4492bc1f17132cd0","to_address":"41d1e7a6bc354106cb410e65ff8b181c600ff14292"},"type_url":"type.googleapis.com/protocol.TransferContract"},"type":"TransferContract"}],"ref_block_bytes":"267e","ref_block_hash":"9a447d222e8de9f2","expiration":1530893064000,"timestamp":1530893006233}},"privateKey": "your private key"}
}'
Parameters：Transaction is a contract created by http api, privateKey is the user private key
Return value：Signed Transaction contract data

/wallet/sendrawtransaction
Function：Broadcast the signed transaction
demo：curl -X POST  http://127.0.0.1:12454/wallet/sendrawtransaction -d '{"signature":["97c825b41c77de2a8bd65b3df55cd4c0df59c307c0187e42321dcc1cc455ddba583dd9502e17cfec5945b34cad0511985a6165999092a6dec84c2bdd97e649fc01"],"txID":"454f156bf1256587ff6ccdbc56e64ad0c51e4f8efea5490dcbc720ee606bc7b8","raw_data":{"contract":[{"parameter":{"value":{"amount":1000,"owner_address":"41e552f6487585c2b58bc2c9bb4492bc1f17132cd0","to_address":"41d1e7a6bc354106cb410e65ff8b181c600ff14292"},"type_url":"type.googleapis.com/protocol.TransferContract"},"type":"TransferContract"}],"ref_block_bytes":"267e","ref_block_hash":"9a447d222e8de9f2","expiration":1530893064000,"timestamp":1530893006233}}'
Parameters：Signed Transaction contract data
Return value：broadcast success or failure


/wallet/gobject vote-alias
Function：Vote on the master node
demo：curl -X POST  http://127.0.0.1:12454/wallet/vote-alias -d '{
"governance-hash":"41d1e7a6bc354106cb410e65ff8b181c600ff14292", 
"funding|valid|delete",
"yes|no|abstain",
"alias-name":"Masternode1"
}'
Parameters：Alias-name is the Masternode's alias name, as setup in the masternode.conf; governance-hash is the hash of the governance object being voted;

/wallet/getnewaddress
Function：Create a new Gobyte address.
Return value：Newly created Gobyte public address.

/wallet/sendfrom
Function: Easily transfer from an account to a gobyte address.
Demo: curl -X POST http://127.0.0.1:12454/wallet/sendfrom -d '{"fromaccount": "DefaultAddress","toAddress": "GJ84thwcN3VoJAFbmBtZ4gXvveZrRuTm3D", "amount":10}'
Parameters: fromaccount is the address/label/wallet name. toAddress is the recipient address; amount is the amount of GBX to transfer.
Warning: Please control risks when using this API. To ensure environmental security, please do not invoke APIs provided by other or invoke this very API on a public network.

/wallet/sendtoaddress
Function：Easily transfer from an address using the private send. 
demo: curl -X POST  http://127.0.0.1:12454/wallet/sendtoaddress -d '{"toAddress": "GJ84thwcN3VoJAFbmBtZ4gXvveZrRuTm3D", "amount":10000, "use_ps":1}'
Parameters：use_ps means we will use private send. toAddress is the recipient address; amount is the amount of GBX to transfer.
Return value： transaction, including execution results.
Warning: Please control risks when using this API. To ensure environmental security, please do not invoke APIs provided by other or invoke this very API on a public network.

/wallet/importprivkey
Function: Create address from a specified privatekey string (PRIVATE KEY)
Demo: curl -X POST http://127.0.0.1:12454/wallet/importprivkey -d '{"value": "7465737470617373776f7264" }'
Parameters: value is the private key
Return value：value is the corresponding address for the private key.
Warning: Please control risks when using this API. To ensure environmental security, please do not invoke APIs provided by other or invoke this very API on a public network.

/wallet/getnewaddress
Function: Generates a random private key and address pair
demo：curl -X POST -k http://127.0.0.1:12454/wallet/getnewaddress
Parameters: no parameters.
Return value：value is the corresponding address for the private key.
Warning: Please control risks when using this API. To ensure environmental security, please do not invoke APIs provided by other or invoke this very API on a public network.

/wallet/getpeerinfo
Function：List the nodes which the api fullnode is connecting on the network
demo: curl -X POST  http://127.0.0.1:12454/wallet/getpeerinfo
Parameters：None
Return value：List of nodes

/wallet/getblockcount
Function：Query the latest block
demo: curl -X POST  http://127.0.0.1:12454/wallet/getblockcount
Parameters：None
Return value：Latest block on full node

/wallet/getblock
Function：Query block by hash
demo: curl -X POST  http://127.0.0.1:12454/wallet/getblock -d '{"hash" : a654f6a4fa5fafa5}' 
Parameters：Hash is the hash of the block
Return value：specified Block object

/wallet/getblockhash
Function：Query block hash by height
demo: curl -X POST  http://127.0.0.1:12454/wallet/getblockbyid -d '{"value": "1"}'
Parameters：Block height.
Return value：Block hash.

/wallet/gettransaction
Function：Query transaction by ID
demo: curl -X POST  http://127.0.0.1:12454/wallet/gettransaction -d '{"value": "d5ec749ecc2a615399d8a6c864ea4c74ff9f523c2be0e341ac9be5d47d7c2d62"}'
Parameters：Transaction ID.
Return value：Transaction information.

wallet/masternodelist
Function：Query the list of Master Nodes
demo: curl -X POST  http://127.0.0.1:12454/wallet/masternodelist
Parameters：None
Return value：List of all Master Nodes

/wallet/validateaddress
Function：validate address
demo: curl -X POST  http://127.0.0.1:12454/wallet/validateaddress -d '{"address": "4189139CB1387AF85E3D24E212A008AC974967E561"}'
Parameters：The address, should be in base58checksum, hexString or base64 format.
Return value: True or false
