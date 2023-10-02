# get_account

### Overview

The `get_account` returns an object containing various details about a specific account on the blockchain.

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Eos, Network} from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Eos>({network: Network.EOS})

const account = await tatum.rpc.getAccount('b1')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Example use cases:

1. **Fetching Account Details:**
Developers or users may need to retrieve specific details about an account, such as the account's balance, permissions, resource allocation (CPU, NET, and RAM usage), and other parameters.

2. **Checking Resource Allocation and Consumption:**
get_account can be used to monitor the amount of network, CPU, and RAM resources an account has allocated and consumed. This can help users manage their resources more effectively to ensure their dApps run smoothly.

3. **Monitoring Staked and Unstaked Tokens:**
Users can utilize this method to check the status of their tokens, whether they are staked or unstaked, and make decisions about staking and unstaking based on this information.

### Request Parameters

The `getAccount` method requires the following parameter:

- `accountName` (string, required): A unique identifier assigned to every account. It is required to be 12 characters long and can only contain the characters a-z, 1-5, and . (dot).

### Return Object

The `get_account` method returns an object containing detailed information about the requested account. The object includes the following fields:

- `account_name` (string): The name of the requested account.
- `head_block_num` (integer): The most recent block number on the blockchain at the time of the request.
- `head_block_time` (string): The timestamp of the most recent block on the blockchain at the time of the request.
- `last_code_update` (string): The timestamp of the last time the account’s smart contract code was updated.
- `created` (string): The timestamp of when the account was created.
- `refund_request` (object): Details of any pending refund requests for the account due to unstaking resources.
- `ram_quota` (integer): The total RAM allocated to the account.
- `net_limit` (object): The available network bandwidth.
- `cpu_limit` (object): CPU time for the account.
- `total_resources` (object): A summary of the total resources (RAM, CPU, and NET) allocated to the account.
- `core_liquid_balance` (string): The amount of liquid (available) core token (usually EOS) the account holds.
- `self_delegated_bandwidth` (object): The amount of bandwidth the account has delegated to itself.
- `net_weight` (integer): The amount of network bandwidth staked by the account.
- `cpu_weight` (integer): CPU time staked by the account.
- `ram_usage` (integer): The amount of RAM currently used by the account.
- `privileged` (boolean): Indicates whether the account has elevated (privileged) permissions.
- `permissions` (array): A list of the account’s permissions and their details, including the public keys associated with the account and any custom permission structures.
- `voter_info` (object): Information related to the account’s voting, such as the proxies used, the number of votes, and the staked amount for voting.

### JSON-RPC Request Example

```json
{
  "account_name": "string"
}
```

### JSON-RPC Response Example

```json
{
    "account_name": "b1",
    "head_block_num": 333261323,
    "head_block_time": "2023-09-27T12:52:25.000",
    "privileged": false,
    "last_code_update": "1970-01-01T00:00:00.000",
    "created": "2018-06-09T11:58:03.500",
    "core_liquid_balance": "0.2849 EOS",
    "ram_quota": 9487,
    "net_weight": "350078512340",
    "cpu_weight": "296624975145",
    "net_limit": {
        "used": 271,
        "available": "659675344495",
        "max": "659675344766",
        "last_usage_update_time": "2022-08-23T01:41:35.000",
        "current_used": 0
    },
    "cpu_limit": {
        "used": 4647,
        "available": 26734970,
        "max": 26739617,
        "last_usage_update_time": "2022-08-23T01:41:35.000",
        "current_used": 0
    },
    "ram_usage": 5010,
    "permissions": [
        {
            "perm_name": "active",
            "parent": "owner",
            "required_auth": {
                "threshold": 2,
                "keys": [
                    {
                        "key": "EOS5BUDFbb2erXiRP8qHQAgVboCHgHGesbCubUfgXYJhnYZKSqNbD",
                        "weight": 1
                    },
                    {
                        "key": "EOS6hQ6v8vut1V2giQCYha7J225GCzFJtF3o7fy8JYuN7k6fG4n23",
                        "weight": 1
                    },
                    {
                        "key": "EOS7RodmQofvAxgYBJzfNuwRKr6TWh5LbCBfB4uQ8tjrjQ8Ukkwqq",
                        "weight": 1
                    },
                    {
                        "key": "EOS7c9jHNgbtTMYgpXvmTb1kW61oH6kwfGioWk75ugDMhsywe6rWu",
                        "weight": 1
                    }
                ],
                "accounts": [],
                "waits": []
            },
            "linked_actions": []
        },
        {
            "perm_name": "owner",
            "parent": "",
            "required_auth": {
                "threshold": 2,
                "keys": [
                    {
                        "key": "EOS5BUDFbb2erXiRP8qHQAgVboCHgHGesbCubUfgXYJhnYZKSqNbD",
                        "weight": 1
                    },
                    {
                        "key": "EOS6hQ6v8vut1V2giQCYha7J225GCzFJtF3o7fy8JYuN7k6fG4n23",
                        "weight": 1
                    },
                    {
                        "key": "EOS7RodmQofvAxgYBJzfNuwRKr6TWh5LbCBfB4uQ8tjrjQ8Ukkwqq",
                        "weight": 1
                    },
                    {
                        "key": "EOS7c9jHNgbtTMYgpXvmTb1kW61oH6kwfGioWk75ugDMhsywe6rWu",
                        "weight": 1
                    }
                ],
                "accounts": [],
                "waits": []
            },
            "linked_actions": []
        }
    ],
    "total_resources": {
        "owner": "b1",
        "net_weight": "35007851.2340 EOS",
        "cpu_weight": "29662497.5145 EOS",
        "ram_bytes": 8087
    },
    "self_delegated_bandwidth": {
        "from": "b1",
        "to": "b1",
        "net_weight": "35007851.2340 EOS",
        "cpu_weight": "29662497.5145 EOS"
    },
    "refund_request": null,
    "voter_info": {
        "owner": "b1",
        "proxy": "",
        "producers": [],
        "staked": "646723487485",
        "last_vote_weight": "2768257912613634048.00000000000000000",
        "proxied_vote_weight": "0.00000000000000000",
        "is_proxy": 0,
        "flags1": 0,
        "reserved2": 0,
        "reserved3": "0.0000 EOS"
    },
    "rex_info": null,
    "subjective_cpu_bill_limit": {
        "used": 0,
        "available": 0,
        "max": 0,
        "last_usage_update_time": "2000-01-01T00:00:00.000",
        "current_used": 0
    },
    "eosio_any_linked_actions": []
}
```