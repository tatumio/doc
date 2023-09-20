# Haqq RPC documentation

Haqq represents a scalable Proof-of-Stake blockchain with high throughput, offering seamless compatibility and interoperability with Ethereum. It is constructed utilizing the Cosmos SDK framework, leveraging the underlying Tendermint Core consensus engine.

Haqq provides the capability to operate Ethereum in its original form within a specialized blockchain framework based on Cosmos. This empowers developers to access Ethereum's desired functionalities while concurrently harnessing the advantages of Tendermint's Proof-of-Stake mechanism. Moreover, due to its foundation on the Cosmos SDK, Haqq enables seamless value transfer across the broader Cosmos Ecosystem through the utilization of the Inter Blockchain Communication Protocol (IBC).

Haqq comprehensively integrates with standard web3 JSON-RPC APIs.

JSON-RPC functionality is accessible through various communication channels. Haqq extends its support to JSON-RPC over both HTTP and WebSocket connections. The activation of these communication modes can be achieved either via command-line flags or configuration settings within the app.toml file.&#x20;

In the Ethereum JSON-RPC ecosystem, a systematic namespace structure is employed. RPC methods are thoughtfully grouped into distinct categories based on their intended functions. Each method name comprises the namespace, an underscore, and the specific method title within the given namespace. For instance, the eth\_call method resides within the eth namespace.
