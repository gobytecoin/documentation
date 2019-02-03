# Freeze/release funds

## Why do we freeze funds?

There are two reasons for setting up a mechanism for freezing funds:

+ To prevent the spam of MasterNode configurations from confirming malicious transactions;
+ To prevent malicious votes.

## Freeze/release mechanism

When the funds are frozen, you will gain a MasterNode(after the configuration).   
**Note that** you cannot send, trade or sell the frozen funds (1000 GBX), until the removal of the masternode configuration.

+ To freeze the funds:

    Send 1000 GBX to a new address.
    Wait for the transaction validation.
    Execute the masternode genkey command.
    Execute the masternode outputs command.
    Edit the masternode.conf as it follows: <MN ALIAS> <IP:PORT> <masternode genkey> <masternode output>
    Edit the gobyte.conf as it follows: masternode=1


+ For example:

    ` MN1 127.0.0.1:12455 7eADAvaddasFASFr134rFsdada 2asdasvAFSFVad14r23csd 1`

+ The release the funds:

    Edit the gobyte.conf as it follows: masternode=0

# Vote

Every Master Node in the GoByte network enjoys the right to vote and you can vote for the Governance Objects after your own heart. You need a MasterNode to vote and the amount of votes depends on the ammount of MasterNodes you hold.

1 Vote per Governance Object per MasterNode.

After the release, you don't have any frozen balance and lose all votes accordingly. As a result, all votes become invalid. To prevent this from happening, you can refreeze to vote.

Note that the GOBYTE network only records your last vote, which means that every new vote will negate all previous votes.

+ For example:

    gobyte-cli gobject vote-many b8f82f1864cb315623d84f0a2220da7f30e77630cac798ef0a9f342dd87e3477 funding yes


The final result of the comand is X votes for the governance object, according the the ammount of MasterNodes you hold.
