# Common Integration Patterns

## Generating Addresses

If you need to generate addresses, either as exchange deposit addresses or some way to receive funds, 
you will need to generate an address to use.

#### - Manually Calculate Addresses (Safest)
Follow these steps to create a private key, then calculate out the resulting
- https://github.com/gobytecoin/Documentation/blob/master/GBX/GoByte-overview.md#6-user-address-generation

#### - Use an RPC call 
- `/wallet/getnewaddress` to create a `Private Key` and `GoByte Address` pair.

- `/wallet/importprivkey` to pass a `Private Key` to generate the matching `GoByte Address`.

---

## Sending GBX from an address

GBX transfers require access to the private key or password for the account.

#### - Manually Create, Sign and Broadcast the transfer transaction

1. Use the `/wallet/createrawtransaction` RPC Call to create a transaction and get the transaction data.
2. Sign the transaction data using `/wallet/signrawtransaction` with a `Private Key`.
3. Or manually sign the transaction data (**Only works with gRPC**) following this [Guide](https://github.com/gobytecoin/Documentation/blob/master/GBX/Gobyte-overview.md#103-signature).
4. Broadcast the signed transaction and transaction data onto the network using `/wallet/sendrawtransaction`.

#### - Use an RPC call 
- `/wallet/sendtoaddress` with a `Public Key` to transfer GBX to a destination address.

- `/wallet/sendtoaddress` with a `use_is` to transfer GBX to a destination address using InstantSend.

- `/wallet/sendtoaddress` with a `use_ps` to transfer GBX to a destination address using PrivateSend.

---

## Reading Transaction from the network

Transactions are confirmed once they're available through the Master Node. The Full Node allows you to query 

#### - Use an RPC call for a transaction/transaction list directly
- `/wallet/getaddresstxids` to retrieve **ALL** transactions by ID, including **Unconfirmed** transactions.
- `/wallet/gettransaction` to retrieve metadata about a transaction, including fees, block number and block production time.

#### - Use an RPC call for the block
If the block has transactions, it will be listed in the trasactions array. You can parse this to find all the transactions included on that block.

- `/wallet/getblock` to retrieve block by block hash from the Full Node. 
- `/wallet/getblockcount` to retrieve the current blockchain height from the Full Node.
- `/wallet/getblockhash` to retrieve by block hash.


---
