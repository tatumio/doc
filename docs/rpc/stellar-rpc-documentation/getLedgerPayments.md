# getLedgersPayments

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the ledger sequence number and optional parameters (Replace placeholders with actual values and remove redundant)
const params = {
    sequence: 'YOUR_LEDGER_SEQUENCE',
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
    includeFailed: true
    join: 'inner',
};

// Retrieve payments related to a specific ledger
const ledgerPayments = await tatum.rpc.getLedgersPayments(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgersPayments` method allows you to retrieve all payment-related operations in a specific Stellar ledger. This includes operations such as `create_account`, `payment`, `path_payment`, and `account_merge`.

### Example use cases:

1. **Payment Analysis:** Developers and applications can use this method to analyze payment-related operations within a specific ledger.
2. **Transaction Tracking:** Tracking and monitoring payments made within a specific ledger for auditing or analysis purposes.
3. **Historical Data Retrieval:** Researchers and analysts can retrieve payment-related data for historical analysis and record-keeping.

### Request Parameters

The `getLedgersPayments` method requires the following parameters:

- `sequence` (string, required): The sequence number of the ledger for which you want to retrieve payment-related operations.
- `cursor` (string, optional): An optional cursor to start listing payments from a specific point within the ledger.
- `order` (string, optional): An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.
- `limit` (number, optional): An optional parameter to specify the maximum number of payments to return. The limit can range from 1 to 200.
- `includeFailed` (boolean, optional): An optional parameter to include failed payments in the results (true or false). If not provided, it defaults to 'false'.
- `join` (string, optional): An optional parameter to specify the join type (inner or left). If not provided, it defaults to 'inner'.

### Return Object

The `getLedgersPayments` method returns an array of payment-related operations within the specified ledger. Each operation includes details such as the sender, receiver, asset, amount, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/payments?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/payments?cursor=214305588031754246&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/49896908/payments?cursor=214305588031623169&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031623169"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/97181f9964085703256e88c1e093fb28b329b7d0dfcf727221b2e957c33301ba"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031623169/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031623169"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031623169"
          }
        },
        "id": "214305588031623169",
        "paging_token": "214305588031623169",
        "transaction_successful": true,
        "source_account": "GA4QH4AJGERVYX4PBY55JYTQJ4RTLJIBYV7OCYIV56LWZE5MVDH3R3UQ",
        "type": "path_payment_strict_receive",
        "type_i": 2,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "97181f9964085703256e88c1e093fb28b329b7d0dfcf727221b2e957c33301ba",
        "asset_type": "native",
        "from": "GA4QH4AJGERVYX4PBY55JYTQJ4RTLJIBYV7OCYIV56LWZE5MVDH3R3UQ",
        "to": "GA4QH4AJGERVYX4PBY55JYTQJ4RTLJIBYV7OCYIV56LWZE5MVDH3R3UQ",
        "amount": "0.0961919",
        "path": [
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "MOBI",
            "asset_issuer": "GA6HCMBLTZS5VYYBCATRBRZ3BZJMAFUDKYYF6AH6MVCMGWMRDNSWJPIH"
          },
          {
            "asset_type": "credit_alphanum12",
            "asset_code": "DOGET",
            "asset_issuer": "GDOEVDDBU6OBWKL7VHDAOKD77UP4DKHQYKOKJJT5PR3WRDBTX35HUEUX"
          },
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "HODL",
            "asset_issuer": "GAQEDFS2JK6JSQO53DWT23TGOLH5ZUZG4O3MNLF3CFUZWEJ6M7MMGJAV"
          }
        ],
        "source_amount": "0.0959902",
        "source_max": "0.0961919",
        "source_asset_type": "native"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031696897"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/3047186e18a70351c5ec795a33fb97f4c466773df72d0540f0b5bc0332402153"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031696897/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031696897"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031696897"
          }
        },
        "id": "214305588031696897",
        "paging_token": "214305588031696897",
        "transaction_successful": true,
        "source_account": "GAT7RNROHRNZG7RVOU4G6ODYP7C7QSV7N64BBFVB5U3J2RCZOGAUPBKO",
        "type": "path_payment_strict_receive",
        "type_i": 2,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "3047186e18a70351c5ec795a33fb97f4c466773df72d0540f0b5bc0332402153",
        "asset_type": "credit_alphanum4",
        "asset_code": "MOBI",
        "asset_issuer": "GA6HCMBLTZS5VYYBCATRBRZ3BZJMAFUDKYYF6AH6MVCMGWMRDNSWJPIH",
        "from": "GAT7RNROHRNZG7RVOU4G6ODYP7C7QSV7N64BBFVB5U3J2RCZOGAUPBKO",
        "to": "GAT7RNROHRNZG7RVOU4G6ODYP7C7QSV7N64BBFVB5U3J2RCZOGAUPBKO",
        "amount": "4.6175312",
        "path": [
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "USDC",
            "asset_issuer": "GA5ZSEJYB37JRC5AVCIA5MOP4RHTM335X2KGX3IHOJAPP5RE34K4KZVN"
          },
          {
            "asset_type": "native"
          }
        ],
        "source_amount": "4.6142496",
        "source_max": "4.6175304",
        "source_asset_type": "credit_alphanum4",
        "source_asset_code": "MOBI",
        "source_asset_issuer": "GA6HCMBLTZS5VYYBCATRBRZ3BZJMAFUDKYYF6AH6MVCMGWMRDNSWJPIH"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031709185"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/53dad14d0f7cd496edf2b5f6fb66e6aa423f8b79637f8f2558c954cc0a03f942"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031709185/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031709185"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031709185"
          }
        },
        "id": "214305588031709185",
        "paging_token": "214305588031709185",
        "transaction_successful": true,
        "source_account": "GBDFUEX5ULIO54S5IYRNNORXI265GVYXXXEYUAEHCVQF2XWA7WJONRJT",
        "type": "payment",
        "type_i": 1,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "53dad14d0f7cd496edf2b5f6fb66e6aa423f8b79637f8f2558c954cc0a03f942",
        "asset_type": "native",
        "from": "GBDFUEX5ULIO54S5IYRNNORXI265GVYXXXEYUAEHCVQF2XWA7WJONRJT",
        "to": "GC5SCPJLHX6WFLUG2GF2W57R4LQ4QUEJEXFOXSZTBSGNUD6RJW2ZX4D3",
        "amount": "50.0000000"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031721473"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/1097e158b818ee82dc358ee88f7428b81590546aefd78904ee57bf49cdcbbe41"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031721473/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031721473"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031721473"
          }
        },
        "id": "214305588031721473",
        "paging_token": "214305588031721473",
        "transaction_successful": true,
        "source_account": "GA4QH4AJGERVYX4PBY55JYTQJ4RTLJIBYV7OCYIV56LWZE5MVDH3R3UQ",
        "type": "path_payment_strict_receive",
        "type_i": 2,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "1097e158b818ee82dc358ee88f7428b81590546aefd78904ee57bf49cdcbbe41",
        "asset_type": "native",
        "from": "GA4QH4AJGERVYX4PBY55JYTQJ4RTLJIBYV7OCYIV56LWZE5MVDH3R3UQ",
        "to": "GA4QH4AJGERVYX4PBY55JYTQJ4RTLJIBYV7OCYIV56LWZE5MVDH3R3UQ",
        "amount": "0.0509312",
        "path": [
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "MOBI",
            "asset_issuer": "GA6HCMBLTZS5VYYBCATRBRZ3BZJMAFUDKYYF6AH6MVCMGWMRDNSWJPIH"
          },
          {
            "asset_type": "credit_alphanum12",
            "asset_code": "LIBRE",
            "asset_issuer": "GAYCCWKECNGDRHYU3UTREBD2XLC3CUQN6FV22TKM4WCQER3IWR7TF5CY"
          },
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "NLT",
            "asset_issuer": "GAX25ZVO4JVPEDK3R7EUFCGVI5XCOQGMVGQNZVFLGY2RWTBIQBW2ZNLT"
          }
        ],
        "source_amount": "0.0506995",
        "source_max": "0.0509312",
        "source_asset_type": "native"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754241"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754241/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031754241"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031754241"
          }
        },
        "id": "214305588031754241",
        "paging_token": "214305588031754241",
        "transaction_successful": true,
        "source_account": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "type": "payment",
        "type_i": 1,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571",
        "asset_type": "credit_alphanum4",
        "asset_code": "SSLX",
        "asset_issuer": "GBHFGY3ZNEJWLNO4LBUKLYOCEK4V7ENEBJGPRHHX7JU47GWHBREH37UR",
        "from": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "to": "GCP4FHBWMDMV73LUOENECG6HYR3SXZ4KUB2S4FIGCAWZL7ZQDA27PSYC",
        "amount": "0.0100000"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754242"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754242/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031754242"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031754242"
          }
        },
        "id": "214305588031754242",
        "paging_token": "214305588031754242",
        "transaction_successful": true,
        "source_account": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "type": "payment",
        "type_i": 1,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571",
        "asset_type": "credit_alphanum4",
        "asset_code": "SSLX",
        "asset_issuer": "GBHFGY3ZNEJWLNO4LBUKLYOCEK4V7ENEBJGPRHHX7JU47GWHBREH37UR",
        "from": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "to": "GCP4DTPJ346VZDN3WMKZVGVTW73Q5J4SOCYHE23SBI3XSYMMPWZLGCTP",
        "amount": "0.0100000"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754243"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754243/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031754243"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031754243"
          }
        },
        "id": "214305588031754243",
        "paging_token": "214305588031754243",
        "transaction_successful": true,
        "source_account": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "type": "payment",
        "type_i": 1,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571",
        "asset_type": "credit_alphanum4",
        "asset_code": "SSLX",
        "asset_issuer": "GBHFGY3ZNEJWLNO4LBUKLYOCEK4V7ENEBJGPRHHX7JU47GWHBREH37UR",
        "from": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "to": "GCP4BVXCBHJJNZ3F6N7CSGZ6TMXAKKGENFSGLWFP7BRSCS77X3XI6RTN",
        "amount": "0.0100000"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754244"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754244/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031754244"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031754244"
          }
        },
        "id": "214305588031754244",
        "paging_token": "214305588031754244",
        "transaction_successful": true,
        "source_account": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "type": "payment",
        "type_i": 1,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571",
        "asset_type": "credit_alphanum4",
        "asset_code": "SSLX",
        "asset_issuer": "GBHFGY3ZNEJWLNO4LBUKLYOCEK4V7ENEBJGPRHHX7JU47GWHBREH37UR",
        "from": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "to": "GCP4AQ2H5R2ZPL6VZMD5UTXIBALY47SE2TWE4LOIUPZEDYTSHCQXWQB6",
        "amount": "0.0100000"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754245"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754245/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031754245"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031754245"
          }
        },
        "id": "214305588031754245",
        "paging_token": "214305588031754245",
        "transaction_successful": true,
        "source_account": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "type": "payment",
        "type_i": 1,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571",
        "asset_type": "credit_alphanum4",
        "asset_code": "SSLX",
        "asset_issuer": "GBHFGY3ZNEJWLNO4LBUKLYOCEK4V7ENEBJGPRHHX7JU47GWHBREH37UR",
        "from": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "to": "GCP3WXBZOCDFUXLRHY27EYAFQXLJ4NNWV7HBHBL56IPFKOJQGPBOTNSN",
        "amount": "0.0100000"
      },
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754246"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571"
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/operations/214305588031754246/effects"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=desc&cursor=214305588031754246"
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/effects?order=asc&cursor=214305588031754246"
          }
        },
        "id": "214305588031754246",
        "paging_token": "214305588031754246",
        "transaction_successful": true,
        "source_account": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "type": "payment",
        "type_i": 1,
        "created_at": "2024-01-13T08:44:04Z",
        "transaction_hash": "e03ea73b0e5d575f492fdcab271cc2217172d078f6e842f47df37cf2df2fc571",
        "asset_type": "credit_alphanum4",
        "asset_code": "SSLX",
        "asset_issuer": "GBHFGY3ZNEJWLNO4LBUKLYOCEK4V7ENEBJGPRHHX7JU47GWHBREH37UR",
        "from": "GDYW6MND6EB32PNRZAMQNOTFLJOZEAFDG3DUWID7I7NRILFWJS66NOWB",
        "to": "GCP3URZ5H3L77QOJ2G44OCOFTVKXXR34CUUWG3IDDKPX3GRPRCMDSJAW",
        "amount": "0.0100000"
      }
    ]
  }
}
```
