---
description: >-
  This function helps a user to upload a new file on the Inter Planetary File
  Storage
---

# Upload File

### **Overview**&#x20;

The "uploadFile" function is specifically designed to facilitate the process of uploading data to the IPFS network. By supplying the file in a buffer format, this function allows users to store their data on the decentralised IPFS system and receive a unique CID (Content Identifier) in return, which acts as a reference to the uploaded data.

### **How to upload a file to IPFS using TatumSDK**&#x20;

Use the TatumSDK (@tatumio/tatum) to upload your file to IPFS.

{% tabs %}
{% tab title="Typescript" %}
```typescript
// yarn add @tatumio/tatum
import { TatumSDK, Network, Polygon, ResponseDto, FungibleTokenBalance } from 
'@tatumio/tatum'
import { readFileSync } from 'fs'

const tatumClient = await TatumSDK.init<Polygon>({
      network: Network.Polygon,
      verbose: true,
      apiKey: {
        v4: '<apikey>',
      },
    })

const buffer = readFileSync('/path/to/file/file.jpg')

const result = await tatumClient.ipfs.uploadFile({ file: buffer })
console.log(JSON.stringify(result))

tatum.destroy();
```
{% endtab %}

{% tab title="Javascript" %}
<pre class="language-javascript"><code class="lang-javascript"><strong>// Install with: npm install @tatumio/tatum
</strong>const { TatumSDK, Network } = require("@tatumio/tatum");
const readFileSync = require('fs').readFileSync;


const tatumClient = await TatumSDK.init({
      network: Network.Polygon,
      verbose: true,
      apiKey: {
        v4: '&#x3C;apikey>',
      },
    })

const buffer = readFileSync('/path/to/file/file.jpg')

const result = await tatumClient.ipfs.uploadFile({ file: buffer })
console.log(JSON.stringify(result))

tatum.destroy();
</code></pre>
{% endtab %}
{% endtabs %}

<details>

<summary>Expected Response</summary>

```json
// Some code
{
    "data": {
        "ipfsHash":"bafybeighfkqyizr3ncoraqfyi6twf2tnxjxhxewwaqvdom57ijiudh5w7y"
        },
    "status":"SUCCESS"
}
```

</details>

### **Request interface**

```typescript
interface UploadFileDetails {
  /**
   * The file is to be uploaded in binary format.
   */
  file: Buffer
}
```

### **Response interface**

```typescript
interface ResponseDto<T> {
  /**
   * Actual payload of the response.
   */
  data: T
  /**
   * Status of the response.
   */
  status: Status
  /**
   * In case of ERROR status, this field contains the error message and detailed description.
   */
  error?: ErrorWithMessage
}

interface IPFSUploadResponse {
  /**
   * The unique CID (Content Identifier) associated with the uploaded file.
   */
  ipfsHash: string
}
```
