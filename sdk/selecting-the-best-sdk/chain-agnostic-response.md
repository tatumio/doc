# Chain Agnostic Response

Most of us don't need to understand the intricate details of blockchain's hexadecimal gibberish. That's where response abstraction in Web3 SDKs comes into play.

**🎯What is Chain Agnostic SDK’s ?**

In the simplest terms, chain agnostics refers to the value-add that service providers offer when they convert the raw blockchain data into a format that's more digestible for developers.

**💼An Example:**

When you fetch balance from a raw function

`BigNumber {`\
`_hex: '0xd47cca060a3e...',`\
`_isBigN﻿umber: true`\
`}`

When you fetch balance from an abstracted function

`Balance{`\
`result : "6.5560815771722537667235e+22”,`\
`}`

💡Why Does It Matter?

1. 💻**Ease of use**: Raw data from blockchain nodes can be complicated and tedious to understand. Response abstraction simplifies this data.
2. ⌛**Time-saving**: Response abstraction saves developers’ time, eliminating the need to parse and interpret raw blockchain data manually.
3. 🧩**Better Integration**: Abstracted responses often better fit into existing software architectures, making the integration of blockchain functionalities smoother.
4. 🚀**Increased productivity**: By handling the low-level details, response abstraction allows developers to concentrate on higher-level functionality, ultimately boosting productivity.

If you've enjoyed this post and found it informative, share it with your developer friends who could benefit from the magic of response abstraction!
