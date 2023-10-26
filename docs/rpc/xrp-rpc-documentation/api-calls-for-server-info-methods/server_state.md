# server\_state

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

const res = await tatum.rpc.serverState()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `server_state` RPC method is used to retrieve various machine-readable information about the rippled server's current state. The response provided by this method is almost the same as the `server_info` method, but uses units that are easier to process instead of easier to read. For example, XRP values are given in integer drops instead of scientific notation or decimal values, and time is given in milliseconds instead of seconds.

This method can be useful when you need to gather specific information about the server's state, such as the build version, complete ledgers, load base, load factor, server state, and more. This information can be useful for monitoring the health and performance of a rippled server.

{% embed url="https://codepen.io/tatum-devrel/pen/mdQgaXx" %}

### Parameters

The `server_state` method does not require any parameters.

### Return Object

The `server_state` method returns an object with the following fields:

* `amendment_blocked`: (Optional) A Boolean value that indicates if the server is amendment blocked. This field may be omitted if the server is not amendment blocked.
* `build_version`: A string that provides the version number of the running `rippled` version.
* `complete_ledgers`: A string that indicates the sequence numbers of the ledger versions the local `rippled` has in its database. This could be a disjoint sequence like "2500-5000,32570-7695432". If the server does not have any complete ledgers (for example, if it recently started syncing with the network), this is an empty string.
* `closed_ledger`: (Optional) An object that provides information on the most recently closed ledger that has not been validated by consensus. If the most recently validated ledger is available, the response omits this field and includes `validated_ledger` instead. The member fields are the same as the `validated_ledger` field.
* `io_latency_ms`: A number that indicates the amount of time spent waiting for I/O operations, in milliseconds. If this number is not very, very low, then the `rippled` server is probably having serious load issues.
* `jq_trans_overflow`: A string-number that represents the number of times this server has had over 250 transactions waiting to be processed at once. A large number here may mean that your server is unable to handle the transaction load of the XRP Ledger network.
* `last_close`: An object that provides information about the last time the server closed a ledger, including the amount of time it took to reach a consensus and the number of trusted validators participating. This object includes:
  * `last_close.converge_time`: A number that shows the amount of time it took to reach a consensus on the most recently validated ledger version, in milliseconds.
  * `last_close.proposers`: A number that indicates how many trusted validators the server considered (including itself, if configured as a validator) in the consensus process for the most recently validated ledger version.
* `load`: (Admin only) An object that provides detailed information about the current load state of the server. This object includes:
  * `load.job_types`: (Admin only) An array that provides information about the rate of different types of jobs the server is doing and how much time it spends on each.
  * `load.threads`: (Admin only) A number that indicates the number of threads in the server's main job pool.
* `load_base`: An integer that represents the baseline amount of server load used in transaction cost calculations. If the `load_factor` is equal to the `load_base` then only the base transaction cost is enforced. If the `load_factor` is higher than the `load_base`, then transaction costs are multiplied by the ratio between them.
* `load_factor`: A number that represents the load factor the server is currently enforcing. The ratio between this value and the `load_base` determines the multiplier for transaction costs. The load factor is determined by the highest of the individual server's load factor, cluster's load factor, the open ledger cost, and the overall network's load factor.
* `load_factor_fee_escalation`: (Optional) A number that indicates the current multiplier to the transaction cost to get into the open ledger, in fee levels.
* `load_factor_fee_queue`: (Optional) A number that indicates the current multiplier to the transaction cost to get into the queue, if the queue is full, in fee levels.
* `load_factor_fee_reference`: (Optional) A number that indicates the transaction cost with no load scaling, in fee levels.
* `load_factor_server`: (Optional) A number that represents the load factor the server is enforcing, not including the open ledger cost.
* `peers`: A number that shows how many other `rippled` servers this one is currently connected to. This field is omitted by reporting mode servers.
* `pubkey_node`: A string that represents the public key used to verify this server for peer-to-peer communications. This node key pair is automatically generated by the server the first time it starts up.
* `pubkey_validator`: (Admin only) A string that represents the public key used by this node to sign ledger validations. This validation key pair is derived from the `[validator_token]` or `[validation_seed]` config field.
* `reporting`: (Reporting mode servers only) An object that provides information about this server's reporting-mode specific configurations. This object includes:
  * `reporting.etl_sources`: (Reporting mode servers only) An array that lists P2P-mode servers this reporting mode is retrieving data from. Each entry in this array is an ETL Source object.
  * `reporting.is_writer`: (Reporting mode servers only) A Boolean value that indicates if this server is writing to the external database with ledger data. If false, it is not currently writing, possibly because another reporting mode server is currently populating a shared database, or because it's configured as read-only.
  * `reporting.last_publish_time`: (Reporting mode servers only) A string that represents an ISO 8601 timestamp indicating when this server last saw a new validated ledger from any of its P2P mode sources.
* `server_state`: A string that indicates to what extent the server is participating in the network.
* `server_state_duration_us`: A number that shows the number of consecutive microseconds the server has been in the current state.
* `state_accounting`: An object that represents a map of various server states with information about the time the server spends in each. This object includes:
  * `state_accounting.*.duration_us`: A string that indicates the number of microseconds the server has spent in this state. This is updated whenever the server transitions into another state.
  * `state_accounting.*.transitions`: A string that shows the number of times the server has changed into this state.
* `time`: A string that indicates the current time in UTC, according to the server's clock.
* `uptime`: A number that indicates the number of consecutive seconds that the server has been operational.
* `validated_ledger`: (Optional) An object that provides information about the most recent fully-validated ledger. This object includes:
  * `validated_ledger.base_fee`: A number that indicates the base fee, in drops of XRP, for propagating a transaction to the network.
  * `validated_ledger.close_time`: A number that shows the time this ledger was closed, in seconds since the Ripple Epoch.
  * `validated_ledger.hash`: A string that represents the unique hash of this ledger version, as hexadecimal.
  * `validated_ledger.reserve_base`: A number that shows the minimum account reserve, as of the most recent validated ledger version.
  * `validated_ledger.reserve_inc`: A number that shows the owner reserve for each item an account owns, as of the most recent validated ledger version.
  * `validated_ledger.seq`: A number that represents the ledger index of the most recently validated ledger version.
* `validation_quorum`: A number that indicates the minimum number of trusted validations required to validate a ledger version. Some circumstances may cause the server to require more validations.
* `validator_list_expires`: (Admin only) A number that shows when the current validator list expires, in seconds since the Ripple Epoch, or 0 if the server has yet to load a published validator list.

For the `ETL Source Object`, each member of the `etl_sources` field is an object with the following fields:

* `connected`: A Boolean value that indicates if the reporting mode server is connected to this P2P mode server. If false, the server is not connected.
* `grpc_port`: A string that shows the port number on the P2P mode server where this reporting mode server is configured to connect and retrieve ledger data via gRPC.
* `ip`: A string that represents the IP address (IPv4 or IPv6) of the P2P mode server.
* `last_message_arrival_time`: A string that represents an ISO 8601 timestamp indicating the most recent time the reporting mode server received a message from this P2P server.
* `validated_ledgers_range`: A string that shows the range of validated ledger versions this P2P mode server reports that it has available, in the same format as complete\_ledgers.
* `websocket_port`: A string that shows the port number on the P2P server where this reporting mode server is configured to forward WebSocket requests that cannot be served directly from reporting mode.

### JSON-RPC Request Example

```json
{
    "method": "server_state",
    "params": [
        {}
    ]
}
```

### JSON-RPC Response Example

```json
{
  "result": {
    "state": {
      "build_version": "1.7.2",
      "complete_ledgers": "65844785-65887184",
      "io_latency_ms": 3,
      "jq_trans_overflow": "580",
      "last_close": {
        "converge_time": 3012,
        "proposers": 41
      },
      "load_base": 256,
      "load_factor": 134022,
      "load_factor_fee_escalation": 134022,
      "load_factor_fee_queue": 256,
      "load_factor_fee_reference": 256,
      "load_factor_server": 256,
      "peer_disconnects": "792367",
      "peer_disconnects_resources": "7273",
      "peers": 72,
      "pubkey_node": "n9LNvsFiYfFf8va6pma2PHGJKVLSyZweN1iBAkJQSeHw4GjM8gvN",
      "server_state": "full",
      "server_state_duration_us": "422128665555",
      "state_accounting": {
        "connected": {
          "duration_us": "172799714",
          "transitions": "1"
        },
        "disconnected": {
          "duration_us": "309059",
          "transitions": "1"
        },
        "full": {
          "duration_us": "6020429212246",
          "transitions": "143"
        },
        "syncing": {
          "duration_us": "413813232",
          "transitions": "152"
        },
        "tracking": {
          "duration_us": "266553605",
          "transitions": "152"
        }
      },
      "time": "2021-Aug-24 20:43:43.043406 UTC",
      "uptime": 6021282,
      "validated_ledger": {
        "base_fee": 10,
        "close_time": 683153020,
        "hash": "ABEF3D24015E8B6B7184B4ABCEDC0E0E3AA4F0677FAB91C40B1E500707C1F3E5",
        "reserve_base": 20000000,
        "reserve_inc": 5000000,
        "seq": 65887184
      },
      "validation_quorum": 33
    },
    "status": "success"
  }
}
```
