# GOBYTE Mainnet - Integration Guide

Connecting to the GBOYTE network is extremely easy and only requires running 1 node on a machine. Once you've connected to the network, you have multiple ways of interacting with the nodes based on your system's requirements. When you're fully integrated, please reach out to the GoByte team so that we can help you verify your setup.

- [Full GoByte Documentation](https://github.com/gobytecoin/Documentation/blob/master/GBX/Gobyte-overview.md)

# 1. Deploy GoByte Nodes

You'll need to deploy nodes that connect to the network and offer both the ability to read the blockchain state and also to broadcast transactions onto the network.

GoByte's network uses a Full Node to read and broadcast to the network. The Full Node stores the entire blockchain state, including unconfirmed blocks and potential forks. 

Follow this guide to deploy a Full Node on your machine.
- [Node Deployment Guide](https://github.com/gobytecoin/Documentation/blob/master/GBX/Full_Node_Deployment_EN.md)

# 2. Integrate with the GoByte nodes

The nodes support both a gRPC Service and a HTTP Gateway on the ports specified in the configuration files. You can use either method to communicate with the nodes. 
- [Full API documentation](https://github.com/gobytecoin/Documentation/blob/master/GBX/Gobyte-overview.md#4-gobyte-api)

### gRPC 

[gRPC](https://grpc.io/) uses Protobuf and the [GoByte protocol](https://github.com/gobytecoin/protocol).

### HTTP Gateway

The nodes also offer an alternate RESTful HTTP Gateway.
Read the [HTTP Documentation](https://github.com/gobytecoin/Documentation/blob/master/GBX/GoByte-http.md) for examples.

## Build your custom integration. 

Take a look at the [Common Patterns](https://github.com/gobytecoin/Documentation/blob/master/GBX/Common-Patterns.md) guide for some basic assistance.

# 3. Testing

Once you've fully integrated with the network, please test on both the test network and the main network.

### Mainnet
- Block Explorer: https://explorer.gobyte.network/
- Config: https://github.com/gobytecoin/GobyteDeployment/blob/master/main_net_config.conf

### Testnet
- Block Explorer: http://texplorer.gobyte.network/
- Config: https://github.com/gobytecoin/GobyteDeployment/blob/master/test_net_config.conf
