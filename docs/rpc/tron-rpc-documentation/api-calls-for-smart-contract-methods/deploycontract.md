# deploycontract

### How to Use It

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const abi = [{\"constant\":false,\"inputs\":[{\"name\":\"key\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"key\",\"type\":\"uint256\"}],\"name\":\"get\",\"outputs\":[{\"name\":\"value\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]"
const bytecode = "608060405234801561001057600080fd5b5060de8061001f6000396000f30060806040526004361060485763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416631ab06ee58114604d5780639507d39a146067575b600080fd5b348015605857600080fd5b506065600435602435608e565b005b348015607257600080fd5b50607c60043560a0565b60408051918252519081900360200190f35b60009182526020829052604090912055565b600090815260208190526040902054905600a165627a7a72305820fdfe832221d60dd582b4526afa20518b98c2e1cb0054653053a844cf265b25040029"
const ownerAddress = "TJmmqjb1DK9TTZbQXzRQ2AuA94z4gKAPFh"
const name = "SomeContract"

const res = await tatum.rpc.deployContract(
  abi,
  bytecode,
  ownerAddress,
  name,
  { visible: true }
);

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}



### Overview

The `deployContract` method is used to deploy a smart contract to the TRON blockchain. This method takes the application binary interface (ABI) and bytecode of the contract, among other parameters, and returns an unsigned transaction that must be signed and sent to the blockchain to deploy the contract.

### Parameters

* `abi`(string): The application binary interface (ABI) of the smart contract.
* `bytecode`(string): The bytecode of the smart contract.
* `feeLimit`(BigNumber): The maximum TRX consumption, measured in SUN (1 TRX = 1,000,000 SUN).
* `parameter`(string): Parameter passed to the constructor of the contract.
* `originEnergyLimit`(BigNumber):  The max energy that will be consumed by the owner during contract execution or creation.
* `ownerAddress`(string):  The contract owner's address in hexadecimal format.
* `name`(string): The name of the smart contract.
* `callValue`(BigNumber): The amount of TRX transferred with this transaction, measured in SUN.
* `consumeUserResourcePercent`(integer): The percentage of resources designated for users who use this contract. Accepts integers between 0 and 100.
* `options` (optional): Additional options:
  * `visible` (boolean, optional): Specifies whether the address is in base58 format. Default: false.
  * `permission_id` (number, optional): The permission ID for multi-signature use.

### Return Object

* `txID`: String - The transaction ID.
* `raw_data`: Object - The raw data of the transaction, including the contract details.
* `signature`: Array - An array containing the signatures of the transaction.

### HTTP Request Example

```json
{
  "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"key\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"key\",\"type\":\"uint256\"}],\"name\":\"get\",\"outputs\":[{\"name\":\"value\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]",
  "bytecode": "608060405234801561001057600080fd5b5060de8061001f6000396000f30060806040526004361060485763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416631ab06ee58114604d5780639507d39a146067575b600080fd5b348015605857600080fd5b506065600435602435608e565b005b348015607257600080fd5b50607c60043560a0565b60408051918252519081900360200190f35b60009182526020829052604090912055565b600090815260208190526040902054905600a165627a7a72305820fdfe832221d60dd582b4526afa20518b98c2e1cb0054653053a844cf265b25040029",
  "owner_address": "TJmmqjb1DK9TTZbQXzRQ2AuA94z4gKAPFh",
  "name": "SomeContract",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "visible": true,
  "txID": "8e6c61ec8d6eee3685ddfde892f6d78609b30cd969f6c96ae13904dd9125afa7",
  "contract_address": "41a7444de2b88e2d7a383d1a8c8d3c5c02b2939d61",
  "raw_data": {
    "contract": [
      {
        "parameter": {
          "value": {
            "owner_address": "TJmmqjb1DK9TTZbQXzRQ2AuA94z4gKAPFh",
            "new_contract": {
              "bytecode": "608060405234801561001057600080fd5b5060de8061001f6000396000f30060806040526004361060485763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416631ab06ee58114604d5780639507d39a146067575b600080fd5b348015605857600080fd5b506065600435602435608e565b005b348015607257600080fd5b50607c60043560a0565b60408051918252519081900360200190f35b60009182526020829052604090912055565b600090815260208190526040902054905600a165627a7a72305820fdfe832221d60dd582b4526afa20518b98c2e1cb0054653053a844cf265b25040029",
              "name": "SomeContract",
              "origin_address": "TJmmqjb1DK9TTZbQXzRQ2AuA94z4gKAPFh",
              "abi": {
                "entrys": [
                  {
                    "inputs": [
                      {
                        "name": "key",
                        "type": "uint256"
                      },
                      {
                        "name": "value",
                        "type": "uint256"
                      }
                    ],
                    "name": "set",
                    "stateMutability": "Nonpayable",
                    "type": "Function"
                  },
                  {
                    "outputs": [
                      {
                        "name": "value",
                        "type": "uint256"
                      }
                    ],
                    "constant": true,
                    "inputs": [
                      {
                        "name": "key",
                        "type": "uint256"
                      }
                    ],
                    "name": "get",
                    "stateMutability": "View",
                    "type": "Function"
                  }
                ]
              }
            }
          },
          "type_url": "type.googleapis.com/protocol.CreateSmartContract"
        },
        "type": "CreateSmartContract"
      }
    ],
    "ref_block_bytes": "e881",
    "ref_block_hash": "f0d4c62907d3ad78",
    "expiration": 1684765344000,
    "timestamp": 1684765286344
  },
  "raw_data_hex": "0a02e8812208f0d4c62907d3ad78408082dc9e84315ad703081e12d2030a30747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e437265617465536d617274436f6e7472616374129d030a1541608f8da72479edc7dd921e4c30bb7e7cddbe722e1283030a1541608f8da72479edc7dd921e4c30bb7e7cddbe722e1a5c0a2b1a03736574220e12036b65791a0775696e743235362210120576616c75651a0775696e74323536300240030a2d10011a03676574220e12036b65791a0775696e743235362a10120576616c75651a0775696e743235363002400222fd01608060405234801561001057600080fd5b5060de8061001f6000396000f30060806040526004361060485763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416631ab06ee58114604d5780639507d39a146067575b600080fd5b348015605857600080fd5b506065600435602435608e565b005b348015607257600080fd5b50607c60043560a0565b60408051918252519081900360200190f35b60009182526020829052604090912055565b600090815260208190526040902054905600a165627a7a72305820fdfe832221d60dd582b4526afa20518b98c2e1cb0054653053a844cf265b250400293a0c536f6d65436f6e747261637470c8bfd89e8431"
}
```
