# getnodeinfo

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const nodeInfo = await tatum.rpc.getNodeInfo()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getNodeInfo` method is used to query information about the current state of the TRON node. This includes details about the latest block information, the number of active and passive connections, the total TCP flow, and other vital node details. This information is critical for monitoring the health and status of the TRON network.

{% embed url="https://codepen.io/tatum-devrel/pen/qBQwgwQ" %}

### Parameters

This method doesn't require any parameters.

### Return Object

* `beginSyncNum` (integer): The begin sync block number.
* `block` (string): The latest block information, including block height and block id.
* `solidityBlock` (string): The latest solidified block information, including block height and block id.
* `currentConnectCount` (integer): The current connect count.
* `activeConnectCount` (integer): Active node connection count.
* `passiveConnectCount` (integer): Passive node connection count.
* `totalFlow` (integer): Total TCP flow.
* `peerInfoList` (PeerInfo\[]): Peer node information.
* `configNodeInfo` (ConfigNodeInfo): Node configuration information.
* `machineInfo` (MachineInfo): The information of the machine where the node is located.
* `cheatWitnessInfoMap` (map\<string, string>): SR information that may be suspected of cheating.

### HTTP Request Example

```curl
{}
```

### HTTP Response Example

```json
{
  "activeConnectCount": 2,
  "beginSyncNum": 33868394,
  "block": "Num:33868413,ID:000000000204ca7d21eec047b7bd9659e633f27eabe7133aa8ae1f35c7800835",
  "cheatWitnessInfoMap": {},
  "configNodeInfo": {
    "activeNodeSize": 2,
    "allowAdaptiveEnergy": 1,
    "allowCreationOfContracts": 1,
    "backupListenPort": 10001,
    "backupMemberSize": 0,
    "backupPriority": 6,
    "codeVersion": "4.7.1.1",
    "dbVersion": 2,
    "discoverEnable": true,
    "listenPort": 16666,
    "maxConnectCount": 30,
    "maxTimeRatio": 5,
    "minParticipationRate": 0,
    "minTimeRatio": 0,
    "p2pVersion": "1",
    "passiveNodeSize": 2,
    "sameIpMaxConnectCount": 2,
    "sendNodeSize": 3,
    "supportConstant": true,
    "versionNum": "17686"
  },
  "currentConnectCount": 5,
  "machineInfo": {
    "cpuCount": 4,
    "cpuRate": 0.012658227848101266,
    "deadLockThreadCount": 0,
    "deadLockThreadInfoList": [],
    "freeMemory": 391487488,
    "javaVersion": "1.8.0_291",
    "jvmFreeMemory": 11439582784,
    "jvmTotalMemory": 12850036736,
    "memoryDescInfoList": [
      {
        "initSize": 2555904,
        "maxSize": 268435456,
        "name": "Code Cache",
        "useRate": 0.2647867202758789,
        "useSize": 71078144
      },
      {
        "initSize": 0,
        "maxSize": -1,
        "name": "Metaspace",
        "useRate": 0.9261336443443698,
        "useSize": 78023544
      },
      {
        "initSize": 0,
        "maxSize": 1073741824,
        "name": "Compressed Class Space",
        "useRate": 0.007893860340118408,
        "useSize": 8475968
      },
      {
        "initSize": 68222976,
        "maxSize": 279183360,
        "name": "Par Eden Space",
        "useRate": 0.13357790378337736,
        "useSize": 37292728
      },
      {
        "initSize": 8519680,
        "maxSize": 34865152,
        "name": "Par Survivor Space",
        "useRate": 0.16272110329534775,
        "useSize": 5673296
      },
      {
        "initSize": 170590208,
        "maxSize": 12535988224,
        "name": "CMS Old Gen",
        "useRate": 0.10908497228658533,
        "useSize": 1367487928
      }
    ],
    "osName": "Linux 3.10.0-1160.49.1.el7.x86_64",
    "processCpuRate": 0.012658227848101266,
    "threadCount": 185,
    "totalMemory": 16260251648
  },
  "passiveConnectCount": 3,
  "peerList": [
    {
      "active": true,
      "avgLatency": 0,
      "blockInPorcSize": 0,
      "connectTime": 1681960376733,
      "disconnectTimes": 0,
      "headBlockTimeWeBothHave": 0,
      "headBlockWeBothHave": "Num:33868390,ID:000000000204ca664c3e79e480b435591d53e0bcd7d8697a0b11e51ece052e84",
      "host": "/54.186.12.211",
      "inFlow": 0,
      "lastBlockUpdateTime": 1684738920033,
      "lastSyncBlock": "",
      "localDisconnectReason": "",
      "needSyncFromPeer": false,
      "needSyncFromUs": false,
      "nodeCount": 4,
      "nodeId": "2e278e5e01e48a4da86d0ee547447917cbf08433fdb438e22cf0f2362d09ee33412a7f035e53931efed83f22e72b705044384db2a09e59885310574d06b33f8d",
      "port": 16666,
      "remainNum": 0,
      "remoteDisconnectReason": "",
      "score": 0,
      "syncBlockRequestedSize": 0,
      "syncFlag": false,
      "syncToFetchSize": 0,
      "syncToFetchSizePeekNum": -1,
      "unFetchSynNum": 0
    },
    {
      "active": true,
      "avgLatency": 0,
      "blockInPorcSize": 0,
      "connectTime": 1681960358724,
      "disconnectTimes": 0,
      "headBlockTimeWeBothHave": 0,
      "headBlockWeBothHave": "Num:33824159,ID:0000000002041d9f47331f314d2e124dde87180cae606f005d8c26023a1c2e21",
      "host": "/54.69.254.172",
      "inFlow": 0,
      "lastBlockUpdateTime": 1684588047076,
      "lastSyncBlock": "Num:33217176,ID:0000000001fada9882d944c94f79b01305e0bfdc43536fc9530eecc16ae1ac49",
      "localDisconnectReason": "",
      "needSyncFromPeer": false,
      "needSyncFromUs": false,
      "nodeCount": 4,
      "nodeId": "2e278e5e01e48a4da86d0ee547447917cbf08433fdb438e22cf0f2362d09ee33412a7f035e53931efed83f22e72b705044384db2a09e59885310574d06b33f8d",
      "port": 16666,
      "remainNum": 0,
      "remoteDisconnectReason": "",
      "score": 0,
      "syncBlockRequestedSize": 0,
      "syncFlag": false,
      "syncToFetchSize": 0,
      "syncToFetchSizePeekNum": -1,
      "unFetchSynNum": 0
    },
    {
      "active": false,
      "avgLatency": 0,
      "blockInPorcSize": 0,
      "connectTime": 1682772783216,
      "disconnectTimes": 0,
      "headBlockTimeWeBothHave": 0,
      "headBlockWeBothHave": "Num:33868413,ID:000000000204ca7d21eec047b7bd9659e633f27eabe7133aa8ae1f35c7800835",
      "host": "/54.69.105.245",
      "inFlow": 0,
      "lastBlockUpdateTime": 1684738998026,
      "lastSyncBlock": "Num:33524301,ID:0000000001ff8a4dd686ace89310555cacfdaa929ea24de2bff34369fce82a64",
      "localDisconnectReason": "",
      "needSyncFromPeer": false,
      "needSyncFromUs": false,
      "nodeCount": 4,
      "nodeId": "2e278e5e01e48a4da86d0ee547447917cbf08433fdb438e22cf0f2362d09ee33412a7f035e53931efed83f22e72b705044384db2a09e59885310574d06b33f8d",
      "port": 16666,
      "remainNum": 0,
      "remoteDisconnectReason": "",
      "score": 0,
      "syncBlockRequestedSize": 0,
      "syncFlag": false,
      "syncToFetchSize": 0,
      "syncToFetchSizePeekNum": -1,
      "unFetchSynNum": 0
    },
    {
      "active": false,
      "avgLatency": 71,
      "blockInPorcSize": 0,
      "connectTime": 1681961633946,
      "disconnectTimes": 0,
      "headBlockTimeWeBothHave": 0,
      "headBlockWeBothHave": "Num:33868413,ID:000000000204ca7d21eec047b7bd9659e633f27eabe7133aa8ae1f35c7800835",
      "host": "/47.90.207.227",
      "inFlow": 0,
      "lastBlockUpdateTime": 1684738998108,
      "lastSyncBlock": "Num:33156658,ID:0000000001f9ee326f10e9b927216b5459579e57b781b9f6702a4d76e205ef7b",
      "localDisconnectReason": "",
      "needSyncFromPeer": false,
      "needSyncFromUs": false,
      "nodeCount": 4,
      "nodeId": "2e278e5e01e48a4da86d0ee547447917cbf08433fdb438e22cf0f2362d09ee33412a7f035e53931efed83f22e72b705044384db2a09e59885310574d06b33f8d",
      "port": 16666,
      "remainNum": 0,
      "remoteDisconnectReason": "",
      "score": 0,
      "syncBlockRequestedSize": 0,
      "syncFlag": false,
      "syncToFetchSize": 0,
      "syncToFetchSizePeekNum": -1,
      "unFetchSynNum": 0
    },
    {
      "active": false,
      "avgLatency": 75,
      "blockInPorcSize": 0,
      "connectTime": 1682398959068,
      "disconnectTimes": 1,
      "headBlockTimeWeBothHave": 0,
      "headBlockWeBothHave": "Num:33868050,ID:000000000204c91264aedf926cd8f53e9d67ec2e1ccf6d0da98fbf3ab12ed27f",
      "host": "/47.89.186.34",
      "inFlow": 0,
      "lastBlockUpdateTime": 1684737768295,
      "lastSyncBlock": "",
      "localDisconnectReason": "",
      "needSyncFromPeer": false,
      "needSyncFromUs": false,
      "nodeCount": 4,
      "nodeId": "2e278e5e01e48a4da86d0ee547447917cbf08433fdb438e22cf0f2362d09ee33412a7f035e53931efed83f22e72b705044384db2a09e59885310574d06b33f8d",
      "port": 16666,
      "remainNum": 0,
      "remoteDisconnectReason": "TIME_OUT",
      "score": 0,
      "syncBlockRequestedSize": 0,
      "syncFlag": false,
      "syncToFetchSize": 0,
      "syncToFetchSizePeekNum": -1,
      "unFetchSynNum": 0
    }
  ],
  "solidityBlock": "Num:33868395,ID:000000000204ca6bce66b0a2b5694dffbb37eb2ff3f83040457f4c88115c0ee3",
  "totalFlow": 0
}
```
