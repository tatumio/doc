# get_account

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, EOS, Network} from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<EOS>({network: Network.EOS})

const account = await tatum.rpc.getAccount('b1')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `get_account` returns an object containing various details about a specific account on the blockchain.

Use cases:

1. **Fetching Account Details:**
Developers or users may need to retrieve specific details about an account, such as the account's balance, permissions, resource allocation (CPU, NET, and RAM usage), and other parameters.

2. **Checking Resource Allocation and Consumption:**
get_account can be used to monitor the amount of network, CPU, and RAM resources an account has allocated and consumed. This can help users manage their resources more effectively to ensure their dApps run smoothly.

3. **Monitoring Staked and Unstaked Tokens:**
Users can utilize this method to check the status of their tokens, whether they are staked or unstaked, and make decisions about staking and unstaking based on this information.

### Parameters

The `get_account` method has one parameter:

 * `account_name` in body. It is a unique identifier assigned to every account. It is required to be 12 characters long and can only contain the characters a-z, 1-5, and . (dot).

### Return Object

The `get_account` method has these response parameters:

  * `account_name` - The name of the requested account.
  * `head_block_num` - The most recent block number on the blockchain at the time of the request.
  * `head_block_time` - The timestamp of the most recent block on the blockchain at the time of the request.
  * `last_code_update` - The timestamp of the last time the account’s smart contract code was updated.
  * `created` - The timestamp of when the account was created.
  * `refund_request` - Details of any pending refund requests for the account due to unstaking resources.
  * `ram_quota` - The total RAM allocated to the account (ram_quota).
  * `net_limit` - The available network bandwidth.
  * `cpu_limit` - CPU time for the account.
  * `total_resources` - A summary of the total resources (RAM, CPU, and NET) allocated to the account.
  * `core_liquid_balance` - The amount of liquid (available) core token (usually EOS) the account holds.
  * `self_delegated_bandwidth` - The amount of bandwidth the account has delegated to itself.
  * `net_weight` - The amount of network bandwidth (net_weight).
  * `cpu_weight` - CPU time (cpu_weight) staked by the account.
  * `ram_usage` - The amount of RAM currently used by the account (ram_usage).
  * `privileged` - Indicates whether the account has elevated (privileged) permissions.
  * `permissions` - A list of the account’s permissions and their details, including the public keys associated with the account and any custom permission structures.
  * `voter_info` - Information related to the account’s voting, such as the proxies used, the number of votes, and the staked amount for voting.

### JSON-RPC Request Example

```json
{
  "account_name": "string"
}
```

### JSON-RPC Response Example

```json
{
  "account_name": "string",
  "head_block_num": 0,
  "head_block_time": "string",
  "last_code_update": "string",
  "created": "string",
  "refund_request": {
    "owner": "string",
    "request_time": "string",
    "net_amount": "string",
    "cpu_amount": "string"
  },
  "ram_quota": "string",
  "net_limit": {
    "max": "string",
    "available": "string",
    "used": "string"
  },
  "cpu_limit": {
    "max": "string",
    "available": "string",
    "used": "string"
  },
  "total_resources": {
    "owner": "string",
    "ram_bytes": "string",
    "net_weight": "string",
    "cpu_weight": "string"
  },
  "core_liquid_balance": "string",
  "self_delegated_bandwidth": {
    "from": "string",
    "to": "string",
    "net_weight": "string",
    "cpu_weight": "string"
  },
  "net_weight": "string",
  "cpu_weight": "string",
  "ram_usage": "string",
  "privileged": true,
  "permissions": [
    {
      "parent": "string",
      "perm_name": "string",
      "required_auth": {
        "waits": [
          {
            "wait_sec": 0,
            "weight": 0
          }
        ],
        "keys": [
          {
            "key": "string",
            "weight": 0
          }
        ],
        "threshold": 0,
        "accounts": [
          {
            "weight": 0,
            "permission": {
              "actor": "string",
              "permission": "string"
            }
          }
        ]
      }
    }
  ],
  "voter_info": {
    "owner": "string",
    "proxy": "string",
    "producers": [
      "string"
    ],
    "staked": "string",
    "last_vote_weight": "string",
    "proxied_vote_weight": "string",
    "is_proxy": 0,
    "flags1": 0,
    "reserved2": 0,
    "reserved3": "string"
  }
}
```