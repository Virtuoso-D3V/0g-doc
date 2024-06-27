# DA Client

DA Client can be divided into three components: client, encoder, and retriever.

## Client

Client is a service directly exposed to the user, through which users upload and retrieve data by calling its gRPC interfaces. Inside the client, there is a workflow pipeline for processing tasks:

**Disperser:** Receive gRPC requests from users and stream the received blob data to DA encoder for encoding.
**Batcher:**  Assemble the encoded blobs into batches and request signatures DA Nodes, then proceed to upload the data onto the blockchain.
**Confirmer/Finalizer**: Continuously monitor the transactions that have been successfully uploaded to the blockchain, and maintain the status of the DA requests.
**Retriever**: Push the requests from users to retrieve data to the DA Retriever.

## Encoder

Encoder is a service that handles mathematical computations, including encoding logic, verification logic, and public parameters for the encoding cryptographic protocol.

## Retriever

Retriever is a service to retrieve blob data from DA nodes.