# server\_info

### How to use it

```javascript
// yarn add @tatumio/tatum

import { TatumSDK, Xrp, Network } from '@tatumio/tatum'

// Initialize Tatum SDK for XRP
const tatum = await TatumSDK.init<Xrp>({network: Network.XRP})

// Call the serverInfo method
const serverInfo = await tatum.rpc.serverInfo()

console.log(serverInfo)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```

### Overview

The `serverInfo` method provides a human-readable version of various information about the rippled server being queried. This information can be crucial for understanding the current state of the server, including its uptime, validation quorum, current ledger sequence, transaction load, and much more.

Use cases for `serverInfo` include:

* Monitoring server performance and resource usage.
* Checking the server's connection status to the XRP Ledger network.
* Investigating the server's ledger history and validation status.

{% embed url="https://codepen.io/Martin-Zemanek/pen/JjeXYxB" %}

### Parameters

The `serverInfo` method doesn't require any parameters.

Here are the fields for the `server_info` method:

* `amendment_blocked`: (May be omitted) A Boolean value that indicates whether this server is amendment blocked. If the server is not amendment blocked, the response omits this field.
* `build_version`: A string that represents the version number of the running `rippled` server.
* `closed_ledger`: (May be omitted) An object that provides information about the most recently closed ledger that has not been validated by consensus. If the most recently validated ledger is available, the response omits this field and includes `validated_ledger` instead. The member fields are the same as the `validated_ledger` field.
* `complete_ledgers`: A string that indicates the range of ledger versions the local `rippled` has in its database. This may be a disjoint sequence. If the server does not have any complete ledgers, this is the string "empty".
* `hostid`: On an admin request, returns the hostname of the server running the `rippled` instance; otherwise, returns a single RFC-1751 word based on the node public key.
* `io_latency_ms`: A number that shows the amount of time spent waiting for I/O operations, in milliseconds. If this number is high, then the `rippled` server is probably having serious load issues.
* `jq_trans_overflow`: The number of times (since starting up) that this server has had over 250 transactions waiting to be processed at once. A large number here may mean that your server is unable to handle the transaction load of the XRP Ledger network.
* `last_close`: An object that provides information about the last time the server closed a ledger, including the amount of time it took to reach a consensus and the number of trusted validators participating.
  * `last_close.converge_time_s`: A number that represents the amount of time it took to reach a consensus on the most recently validated ledger version, in seconds.
  * `last_close.proposers`: A number that shows how many trusted validators the server considered (including itself, if configured as a validator) in the consensus process for the most recently validated ledger version.
* `load`: (Admin only) An object that provides detailed information about the current load state of the server.
  * `load.job_types`: (Admin only) An array that provides information about the rate of different types of jobs the server is doing and how much time it spends on each.
  * `load.threads`: (Admin only) A number that shows the number of threads in the server's main job pool.
* `load_factor`: A number that represents the load-scaled open ledger transaction cost the server is currently enforcing, as a multiplier on the base transaction cost.
* `load_factor_local`: (May be omitted) A number that represents the current multiplier to the transaction cost based on load to this server.
* `load_factor_net`: (May be omitted) A number that represents the current multiplier to the transaction cost being used by the rest of the network (estimated from other servers' reported load values).
* `load_factor_cluster`: (May be omitted) A number that represents the current multiplier to the transaction cost based on load to servers in this cluster.
* `load_factor_fee_escalation`: (May be omitted) A number that represents the current multiplier to the transaction cost that a transaction must pay to get into the open ledger.
* `load_factor_fee_queue`: (May be omitted) A number that represents the current multiplier to the transaction cost that a transaction must pay to get into the queue, if the queue is full.
* `load_factor_server`: (May be omitted) A number that represents the load factor the server is enforcing, not

including the open ledger cost.

* `peers`: (Omitted by reporting mode servers) A number that shows how many other `rippled` servers this one is currently connected to.
* `pubkey_node`: A string that represents the public key used to verify this server for peer-to-peer communications.
* `pubkey_validator`: (Admin only) A string that represents the public key used by this node to sign ledger validations.
* `reporting`: (Reporting mode servers only) An object that provides information about this server's reporting-mode specific configurations.
* `reporting.etl_sources`: (Reporting mode servers only) An array that lists the P2P-mode servers this reporting mode is retrieving data from.
* `reporting.is_writer`: (Reporting mode servers only) A Boolean value that indicates whether this server is writing to the external database with ledger data.
* `reporting.last_publish_time`: (Reporting mode servers only) A string that represents an ISO 8601 timestamp indicating when this server last published a validated ledger to its subscription streams.
* `server_state`: A string that indicates to what extent the server is participating in the network.
* `server_state_duration_us`: A number that represents the number of consecutive microseconds the server has been in the current state.
* `state_accounting`: An object that is a map of various server states with information about the time the server spends in each.
* `state_accounting.*.duration_us`: A string that shows the number of microseconds the server has spent in this state.
* `state_accounting.*.transitions`: A string that shows the number of times the server has changed into this state.
* `time`: A string that represents the current time in UTC, according to the server's clock.
* `uptime`: A number that represents the number of consecutive seconds that the server has been operational.
* `validated_ledger`: (May be omitted) An object that provides information about the most recent fully-validated ledger.
  * `validated_ledger.age`: A number that shows the time since the ledger was closed, in seconds.
  * `validated_ledger.base_fee_xrp`: A number that represents the base fee, in XRP.
  * `validated_ledger.hash`: A string that represents the unique hash for the ledger, as hexadecimal.
  * `validated_ledger.reserve_base_xrp`: A number that represents the minimum amount of XRP (not drops) necessary for every account to keep in reserve.
  * `validated_ledger.reserve_inc_xrp`: A number that represents the amount of XRP (not drops) added to the account reserve for each object an account owns in the ledger.
  * `validated_ledger.seq`: A number that represents the ledger index of the latest validated ledger.
* `validation_quorum`: A number that represents the minimum number of trusted validations required to validate a ledger version. Some circumstances may cause the server to require more validations.
* `validator_list_expires`: (Admin only) A string that either represents the human readable time, in UTC, when the current validator list expires, the string "unknown" if the server has yet to load a published validator list or the string "never" if the server uses a static validator list.

### JSON-RPC Request Example

```json
{
    "method": "server_info",
    "params": [
        {}
    ]
}
```

### JSON-RPC Response Example

```json
{
  "result": {
    "info": {
      "build_version": "1.9.4",
      "complete_ledgers": "32570-75801747",
      "hostid": "ABET",
      "initial_sync_duration_us": "566800928",
      "io_latency_ms": 1,
      "jq_trans_overflow": "47035",
      "last_close": {
        "converge_time_s": 3,
        "proposers": 35
      },
      "load_factor": 1,
      "network_id": 0,
      "peer_disconnects": "542",
      "peer_disconnects_resources": "1",
      "peers": 24,
      "pubkey_node": "n9LvjJyaYHBWUvQUat632RrnpS7UHVLW2tLUGXSZ2yXouh4goDHX",
      "server_state": "full",
      "server_state_duration_us": "3612238603",
      "state_accounting": {
        "connected": {
          "duration_us": "125498126",
          "transitions": "67"
        },
        "disconnected": {
          "duration_us": "473415516",
          "transitions": "2"
        },
        "full": {
          "duration_us": "4365855930299",
          "transitions": "337"
        },
        "syncing": {
          "duration_us": "1383837914",
          "transitions": "311"
        },
        "tracking": {
          "duration_us": "518995710",
          "transitions": "374"
        }
      },
      "time": "2022-Nov-16 21:51:03.737667 UTC",
      "uptime": 4368357,
      "validated_ledger": {
        "age": 1,
        "base_fee_xrp": 0.00001,
        "hash": "D54A94D5EF620DC212EAB5958D592EC641FC94ED92146477A04DCE5B006DFF05",
        "reserve_base_xrp": 10,
        "reserve_inc_xrp": 2,
        "seq": 75801747
      },
      "validation_quorum": 28
    },
    "status": "success"
  }
}
```
