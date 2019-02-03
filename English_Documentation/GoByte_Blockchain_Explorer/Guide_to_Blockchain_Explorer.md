# Guide to Blockchain explorer

Use the block explorer at https://explorer.gobyte.network/.

## Blockchain module

### Block search

Information on all blocks—from the genesis block to all current blocks—can be found on this page, including block height, its previous block and the corresponding byte size. You can also use the search bar to check block height.
https://explorer.gobyte.network/

### Transaction search

You can search for transaction records on this page. Information on the sender and the recipient’s address, the amount of GBX transferred, block height of transaction record, corresponding Hash and production time can all be found. You can also use the search bar to look for a specific transaction by Hash.

https://explorer.gobyte.network/

### Check address/transaction statistics

On the statistics page, we can see the network hash speed, the trend of average block time and the difficulty. 'The GoByte team will continue to create more data visualizations for the users' convenience.

https://explorer.gobyte.network/hash

### Check node information

This page shows the geographical distribution of TRON’s nodes. From the density of nodes in different regions, users can have a straightforward impression of where they are located. With the embedded Google map, users can zoom in and out of the map to know about the specific details.

https://explorer.gobyte.network/network

## Check MasterNodes information

Users can check out the MasterNode list which includes information on the last block, IP addresses, last paid, status, protocol version and others.

https://explorer.gobyte.network/masternodes

## Votes

### 1. Open GOBYTE Ninja explorer.  
    
   https://masternodes.gobyte.network/

### 2. Enter the Governance page. 

https://masternodes.gobyte.network/governance.html

### 3. Open the proposal page

https://masternodes.gobyte.network/proposaldetails.html?proposalhash=b8f82f1864cb315623d84f0a2220da7f30e77630cac798ef0a9f342dd87e3477

### 4. Decide your vote

Select the "VOTE YES"/"VOTE NO"/"VOTE ABSTAIN" tab, depending on your choice.

### 5. Sending the vote command

Copy the command according to the wallet you use (Qt or gobyte-cli)

```
gobject vote-many b8f82f1864cb315623d84f0a2220da7f30e77630cac798ef0a9f342dd87e3477 funding yes
gobyte-cli gobject vote-many b8f82f1864cb315623d84f0a2220da7f30e77630cac798ef0a9f342dd87e3477 funding yes
```

### 6. Paste the command into your console and hit enter

**Voting Note** 

If you hold multiple Master Nodes, use the "vote-many" command to vote for all of them.

**Voting rules:**  
+ The maximal votes a user can cast should be no more than his/her holding of GBX Master Nodes.
+ Each user can vote for multiple proposals once.
+ The super-block pays every 30 days.
+ Voting does not cost any GBX.

