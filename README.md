## npm package of OASISBloc client sdk for js

OASISBloc supports JavaScript SDK for 3rd party or user services development. You can integrate OASISBloc JavaScript SDK into your project and utilize OASISBloc Data Trade protocol’s functionality. This document provides you with an information of installation and API specification.

## Installation

### Usage in Node.js

Install `osb-cli-sdk` module using `npm`.

```bash
npm install --save osb-cli-sdk
```

Import `osb-cli-sdk` module.

```javascript
import OASIS_CLI from 'osb-cli-sdk'
```

## API Specification

`OASIS_CLI` is a root class of `osb-cli-sdk`, which provides APIs to communicate with OASISBloc blockchain nodes and IDFS nodes. The details of the APIs are as below:

### Constructor

Creates an instance of oasisbloc client

```javascript
const config = {
    chainAccessPoint: [BLOCKCHAIN_API_NODE_ENDPOINT],
    chainId: [BLOCKCHAIN_ID],
    dataTradeContractName: [DATA_TRADE_CONTRACT_NAME],
    privateKey: [PRIVATE_KEY_OF_USER],
    account: [ACCOUNT_NAME_OF_USER]
}
const osbClient = new OASIS_CLI(config)
```

#### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| config.chainAccessPoint | string | Blockchain API node endpoint (ex: 'http://18.141.2.126:1387') |
| config.chainId | string | Blockchain id (ex: '2cfbbc1ce6f7c4a48cfbb6de6ad00c55ea21401fbcf983a6f553fb4d8923d695') |
| config.dataTradeContractName | string | Data trade contract name (ex: 'datatrade13') |
| config.privateKey | string | User's private key |
| config.account | string | User's account name |

### setAuthForContract

데이터 거래를 통해 자산 이동 발생에 대한 동의

```javascript
osbClient.setAuthForContract()
```

### registerData

Registers a data to oasisbloc with encryption and fragmentation of data, and uploads data to data keeper's IDFS nodes

```javascript
osbClient.registerData(data, datatypename, detailFields, price, period, decryptKeyList)
```

#### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| data | Buffer | Data buffer to register |
| datatypename | string | Datatype name |
| detailFields | string array | Values for each metadata field of the datatype |
| price | string | Data price (OSB) |
| period | integer | Data provide period (days) |
| decryptKeyList | string array | Private key list for encrypting each data fragment. The number of data fragments is set from the length of this list |

#### Return values

| Return value | Type | Description |
| ------------ | ---- | ----------- |
| txResultAddDataBegin | object | Transaction result data of adddatabegin action |
| txResultAddDataEnd | object | Transaction result data of adddataend action |
| dataRegistrationInfo | object | Data registration information |

### buyData

Gets a data by buying and downloading encrypted data fragments

```javascript
osbClient.buyData(dataid, buyerPrivateKey)
```

#### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| dataid | integer | Data registration id |
| buyerPrivateKey | string | Buyer private key for authentication of data access. It is not the private key of the user account |

#### Return values

| Return value | Type | Description |
| ------------ | ---- | ----------- |
| data | Buffer | The purchased data |
| txResultBuyData | object | Transaction result data of buydata action |
| dataBuyHistoryInfo | object | Data buy information |


