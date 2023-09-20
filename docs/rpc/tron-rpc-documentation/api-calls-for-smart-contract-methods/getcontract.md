# getcontract

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getContract('TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs', {
    visible: true,
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getContract` method allows you to query a contract's information from the TRON blockchain. This includes the bytecode of the contract, ABI, configuration parameters, and more. This can be useful in a variety of use-cases such as contract verification, auditing, and debugging.

{% embed url="https://codepen.io/Night-Shift-Dev/pen/wvQaBNR" %}

### Parameters

* `value` (string): The contract address, as a string.
* `options` (optional): Additional options.
  * `visible` (boolean, optional): Whether the address is in visible format(base58check) or hex.

### Return Object

The method returns an object with the following properties:

* `origin_address` (string): Contract creator address.
* `contract_address` (string): Contract address.
* `abi` (ABI): ABI of the contract.
* `bytecode` (string): Bytecode of the contract.
* `call_value` (integer): The amount of TRX passed into the contract when deploying the contract.
* `consume_user_resource_percent` (integer): Proportion of user energy consumption.
* `name` (string): Contract name.
* `origin_energy_limit` (integer): Each transaction is allowed to consume the maximum energy of the contract creator, the unit is sun.
* `code_hash` (string): Code hash of the contract.

### HTTP Request Example

```json
{
  "value": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "bytecode": "608060405234801561001057600080fd5b50d3801561001d57600080fd5b50d2801561002a57600080fd5b50604080518082018252600b81526a2a32ba3432b92a37b5b2b760a91b6020808301918252835180850190945260048452631554d11560e21b90840152815191929160069161007c9160039190610236565b508151610090906004906020850190610236565b506005805460ff191660ff92909216919091179055506100cc9050336100b46100d1565b60ff16600a0a6402540be400026100db60201b60201c565b6102ce565b60055460ff165b90565b6001600160a01b038216610136576040805162461bcd60e51b815260206004820152601f60248201527f45524332303a206d696e7420746f20746865207a65726f206164647265737300604482015290519081900360640190fd5b61014f816002546101d560201b61078c1790919060201c565b6002556001600160a01b0382166000908152602081815260409091205461017f91839061078c6101d5821b17901c565b6001600160a01b0383166000818152602081815260408083209490945583518581529351929391927fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef9281900390910190a35050565b60008282018381101561022f576040805162461bcd60e51b815260206004820152601b60248201527f536166654d6174683a206164646974696f6e206f766572666c6f770000000000604482015290519081900360640190fd5b9392505050565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f1061027757805160ff19168380011785556102a4565b828001600101855582156102a4579182015b828111156102a4578251825591602001919060010190610289565b506102b09291506102b4565b5090565b6100d891905b808211156102b057600081556001016102ba565b6108ad806102dd6000396000f3fe608060405234801561001057600080fd5b50d3801561001d57600080fd5b50d2801561002a57600080fd5b50600436106100b35760003560e01c806306fdde03146100b8578063095ea7b31461013557806318160ddd1461017557806323b872dd1461018f578063313ce567146101c557806339509351146101e357806370a082311461020f57806395d89b4114610235578063a457c2d71461023d578063a9059cbb14610269578063dd62ed3e14610295575b600080fd5b6100c06102c3565b6040805160208082528351818301528351919283929083019185019080838360005b838110156100fa5781810151838201526020016100e2565b50505050905090810190601f1680156101275780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b6101616004803603604081101561014b57600080fd5b506001600160a01b038135169060200135610359565b604080519115158252519081900360200190f35b61017d61036f565b60408051918252519081900360200190f35b610161600480360360608110156101a557600080fd5b506001600160a01b03813581169160208101359091169060400135610375565b6101cd6103cc565b6040805160ff9092168252519081900360200190f35b610161600480360360408110156101f957600080fd5b506001600160a01b0381351690602001356103d5565b61017d6004803603602081101561022557600080fd5b50356001600160a01b0316610411565b6100c061042c565b6101616004803603604081101561025357600080fd5b506001600160a01b03813516906020013561048d565b6101616004803603604081101561027f57600080fd5b506001600160a01b0381351690602001356104c9565b61017d600480360360408110156102ab57600080fd5b506001600160a01b03813581169160200135166104d6565b60038054604080516020601f600260001961010060018816150201909516949094049384018190048102820181019092528281526060939092909183018282801561034f5780601f106103245761010080835404028352916020019161034f565b820191906000526020600020905b81548152906001019060200180831161033257829003601f168201915b5050505050905090565b6000610366338484610501565b50600192915050565b60025490565b60006103828484846105ed565b6001600160a01b0384166000908152600160209081526040808320338085529252909120546103c29186916103bd908663ffffffff61072f16565b610501565b5060019392505050565b60055460ff1690565b3360008181526001602090815260408083206001600160a01b038716845290915281205490916103669185906103bd908663ffffffff61078c16565b6001600160a01b031660009081526020819052604090205490565b60048054604080516020601f600260001961010060018816150201909516949094049384018190048102820181019092528281526060939092909183018282801561034f5780601f106103245761010080835404028352916020019161034f565b3360008181526001602090815260408083206001600160a01b038716845290915281205490916103669185906103bd908663ffffffff61072f16565b60006103663384846105ed565b6001600160a01b03918216600090815260016020908152604080832093909416825291909152205490565b6001600160a01b0383166105465760405162461bcd60e51b81526004018080602001828103825260248152602001806108566024913960400191505060405180910390fd5b6001600160a01b03821661058b5760405162461bcd60e51b815260040180806020018281038252602281526020018061080f6022913960400191505060405180910390fd5b6001600160a01b03808416600081815260016020908152604080832094871680845294825291829020859055815185815291517f8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b9259281900390910190a3505050565b6001600160a01b0383166106325760405162461bcd60e51b81526004018080602001828103825260258152602001806108316025913960400191505060405180910390fd5b6001600160a01b0382166106775760405162461bcd60e51b81526004018080602001828103825260238152602001806107ec6023913960400191505060405180910390fd5b6001600160a01b0383166000908152602081905260409020546106a0908263ffffffff61072f16565b6001600160a01b0380851660009081526020819052604080822093909355908416815220546106d5908263ffffffff61078c16565b6001600160a01b038084166000818152602081815260409182902094909455805185815290519193928716927fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef92918290030190a3505050565b600082821115610786576040805162461bcd60e51b815260206004820152601e60248201527f536166654d6174683a207375627472616374696f6e206f766572666c6f770000604482015290519081900360640190fd5b50900390565b6000828201838110156107e4576040805162461bcd60e51b815260206004820152601b60248201527a536166654d6174683a206164646974696f6e206f766572666c6f7760281b604482015290519081900360640190fd5b939250505056fe45524332303a207472616e7366657220746f20746865207a65726f206164647265737345524332303a20617070726f766520746f20746865207a65726f206164647265737345524332303a207472616e736665722066726f6d20746865207a65726f206164647265737345524332303a20617070726f76652066726f6d20746865207a65726f2061646472657373a26474726f6e58205ad8bd992125d73612e695872f74ea2d6951c0410b7633d79c611eec48000cf864736f6c63430005120031",
  "name": "Token",
  "origin_address": "TSNEe5Tf4rnc9zPMNXfaTF5fZfHDDH8oyW",
  "abi": {
    "entrys": [
      {
        "stateMutability": "Nonpayable",
        "type": "Constructor"
      },
      {
        "inputs": [
          {
            "indexed": true,
            "name": "owner",
            "type": "address"
          },
          {
            "indexed": true,
            "name": "spender",
            "type": "address"
          },
          {
            "name": "value",
            "type": "uint256"
          }
        ],
        "name": "Approval",
        "type": "Event"
      },
      {
        "inputs": [
          {
            "indexed": true,
            "name": "from",
            "type": "address"
          },
          {
            "indexed": true,
            "name": "to",
            "type": "address"
          },
          {
            "name": "value",
            "type": "uint256"
          }
        ],
        "name": "Transfer",
        "type": "Event"
      },
      {
        "outputs": [
          {
            "type": "uint256"
          }
        ],
        "constant": true,
        "inputs": [
          {
            "name": "owner",
            "type": "address"
          },
          {
            "name": "spender",
            "type": "address"
          }
        ],
        "name": "allowance",
        "stateMutability": "View",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "bool"
          }
        ],
        "inputs": [
          {
            "name": "spender",
            "type": "address"
          },
          {
            "name": "value",
            "type": "uint256"
          }
        ],
        "name": "approve",
        "stateMutability": "Nonpayable",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "uint256"
          }
        ],
        "constant": true,
        "inputs": [
          {
            "name": "account",
            "type": "address"
          }
        ],
        "name": "balanceOf",
        "stateMutability": "View",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "uint8"
          }
        ],
        "constant": true,
        "name": "decimals",
        "stateMutability": "View",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "bool"
          }
        ],
        "inputs": [
          {
            "name": "spender",
            "type": "address"
          },
          {
            "name": "subtractedValue",
            "type": "uint256"
          }
        ],
        "name": "decreaseAllowance",
        "stateMutability": "Nonpayable",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "bool"
          }
        ],
        "inputs": [
          {
            "name": "spender",
            "type": "address"
          },
          {
            "name": "addedValue",
            "type": "uint256"
          }
        ],
        "name": "increaseAllowance",
        "stateMutability": "Nonpayable",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "string"
          }
        ],
        "constant": true,
        "name": "name",
        "stateMutability": "View",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "string"
          }
        ],
        "constant": true,
        "name": "symbol",
        "stateMutability": "View",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "uint256"
          }
        ],
        "constant": true,
        "name": "totalSupply",
        "stateMutability": "View",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "bool"
          }
        ],
        "inputs": [
          {
            "name": "recipient",
            "type": "address"
          },
          {
            "name": "amount",
            "type": "uint256"
          }
        ],
        "name": "transfer",
        "stateMutability": "Nonpayable",
        "type": "Function"
      },
      {
        "outputs": [
          {
            "type": "bool"
          }
        ],
        "inputs": [
          {
            "name": "sender",
            "type": "address"
          },
          {
            "name": "recipient",
            "type": "address"
          },
          {
            "name": "amount",
            "type": "uint256"
          }
        ],
        "name": "transferFrom",
        "stateMutability": "Nonpayable",
        "type": "Function"
      }
    ]
  },
  "origin_energy_limit": 10000000,
  "contract_address": "TG3XXyExBkPp9nzdajDZsozEu4BkaSJozs",
  "code_hash": "5933c5f6804befa730c18e6bf1b14393d9e062b466c2a772f81a6bfa932a8d46"
}
```

***
