# Value Transfer Memo Transaction <a id="value-transfer-memo-transaction"></a>

## sendTransaction (VALUE_TRANSFER_MEMO) <a id="sendtransaction-value_transfer_memo"></a>

```javascript
caver.klay.sendTransaction(transactionObject [, callback])
```
Sends a [Value Transfer Memo](../../../../../../klaytn/design/transactions/basic.md#txtypevaluetransfermemo) transaction to the network.

**Parameters**

The parameters of sendTransaction are a transaction object and a callback function.

| Name              | Type     | Description                                                                                                |
| ----------------- | -------- | ---------------------------------------------------------------------------------------------------------- |
| transactionObject | Object   | The transaction object to send.                                                                            |
| callback          | Function | (optional) Optional callback, returns an error object as the first parameter and the result as the second. |

A transaction object of type `VALUE_TRANSFER_MEMO` has the following structure:

| Name     | Type                                            | Description                                                                                                                |
| -------- | ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| type     | String                                          | Transaction Type. "VALUE_TRANSFER_MEMO"                                                                                  |
| from     | String                                          | Address of this transaction sender.                                                                                        |
| to       | String                                          | The destination address of the transaction.                                                                                |
| value    | Number &#124; String &#124; BN &#124; BigNumber | The value transferred for the transaction in peb.                                                                          |
| data     | String                                          | The message to send with.                                                                                                  |
| gas      | Number                                          | The maximum amount of gas willing to pay for the transaction (unused gas is refunded).                                     |
| gasPrice | Number                                          | (optional) Gas price provided by the sender in peb. The gasPrice must be the same as the unitPrice set in the Klaytn node. |
| nonce    | Number                                          | (optional) Integer of a nonce. If omitted, it will be set by caver-js via calling `caver.klay.getTransactionCount`.        |

**Return Value**

The `callback` will return the 32-byte transaction hash.

`PromiEvent`: A promise combined event emitter. Will be resolved when the transaction receipt is available. Additionally the following events are available:

- `"transactionHash"` returns `String`: Is fired right after the transaction is sent and a transaction hash is available.
- `"receipt"` returns `Object`: Is fired when the transaction receipt is available.
- `"error"` returns `Error`: Is fired if an error occurs during sending. On an out-of-gas error, the second parameter is the receipt.

**Example**

```javascript
const account = caver.klay.accounts.wallet.add('0x{private key}')

// using the promise
caver.klay.sendTransaction({
    type: 'VALUE_TRANSFER_MEMO',
    from: account.address,
    to: '0x75c3098Be5E4B63FBAc05838DaAEE378dD48098d',
    gas: '300000',
    value: caver.utils.toPeb('1', 'KLAY'),
    data: '0x68656c6c6f',
});
.then(function(receipt){
    ...
});

// using the event emitter
caver.klay.sendTransaction({
    type: 'VALUE_TRANSFER_MEMO',
    from: account.address,
    to: '0x75c3098Be5E4B63FBAc05838DaAEE378dD48098d',
    gas: '300000',
    value: caver.utils.toPeb('1', 'KLAY'),
    data: '0x68656c6c6f',
});
.on('transactionHash', function(hash){
    ...
})
.on('receipt', function(receipt){
    ...
})
.on('error', console.error); // If an out-of-gas error, the second parameter is the receipt.
```


## sendTransaction (FEE_DELEGATED_VALUE_TRANSFER_MEMO) <a id="sendtransaction-fee_delegated_value_transfer_memo"></a>

```javascript
caver.klay.sendTransaction(transactionObject [, callback])
```
Sends a [Fee Delegated Value Transfer Memo](../../../../../../klaytn/design/transactions/fee-delegation.md#txtypefeedelegatedvaluetransfermemo) transaction to the network.

**Parameters**

The parameters of sendTransaction are a transaction object and a callback function.

| Name              | Type     | Description                                                                                                |
| ----------------- | -------- | ---------------------------------------------------------------------------------------------------------- |
| transactionObject | Object   | The transaction object to send.                                                                            |
| callback          | Function | (optional) Optional callback, returns an error object as the first parameter and the result as the second. |

A transaction object of type `FEE_DELEGATED_VALUE_TRANSFER_MEMO` has the following structure:

| Name     | Type                                            | Description                                                                                                                |
| -------- | ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| type     | String                                          | Transaction Type. "FEE_DELEGATED_VALUE_TRANSFER_MEMO"                                                                  |
| from     | String                                          | Address of this transaction sender.                                                                                        |
| to       | String                                          | The destination address of the transaction.                                                                                |
| value    | Number &#124; String &#124; BN &#124; BigNumber | The value transferred for the transaction in peb.                                                                          |
| data     | String                                          | The message to send with.                                                                                                  |
| gas      | Number                                          | The maximum amount of gas willing to pay for the transaction (unused gas is refunded).                                     |
| gasPrice | Number                                          | (optional) Gas price provided by the sender in peb. The gasPrice must be the same as the unitPrice set in the Klaytn node. |
| nonce    | Number                                          | (optional) Integer of a nonce. If omitted, it will be set by caver-js via calling `caver.klay.getTransactionCount`.        |

A transaction object of type `FEE_DELEGATED_VALUE_TRANSFER_MEMO` with the above structure or an `RLP-encoded transaction` of type `FEE_DELEGATED_VALUE_TRANSFER_MEMO` can be used as a parameter in [caver.klay.accounts.signTransaction](../caver.klay.accounts.md#signtransaction) for sender and in [caver.klay.accounts.feePayerSignTransaction](../caver.klay.accounts.md#feepayersigntransaction) for fee payer.

In order for the fee payer to sign an RLP encoded transaction signed by the sender and send it to the network, define an object with the following structure and call `caver.klay.sendTransaction`.

| Name                 | Type   | Description                                   |
| -------------------- | ------ | --------------------------------------------- |
| feePayer             | String | The fee payer address of the transaction.     |
| senderRawTransaction | String | The RLP-encoded transaction signed by sender. |

**Return Value**

The `callback` will return the 32-byte transaction hash.

`PromiEvent`: A promise combined event emitter. Will be resolved when the transaction receipt is available. Additionally the following events are available:

- `"transactionHash"` returns `String`: Is fired right after the transaction is sent and a transaction hash is available.
- `"receipt"` returns `Object`: Is fired when the transaction receipt is available.
- `"error"` returns `Error`: Is fired if an error occurs during sending. On an out-of-gas error, the second parameter is the receipt.

**Example**

```javascript
const sender = caver.klay.accounts.wallet.add('0x{private key}')
const feePayer = caver.klay.accounts.wallet.add('0x{private key}')

// using the promise
const { rawTransaction: senderRawTransaction } = await caver.klay.accounts.signTransaction({
  type: 'FEE_DELEGATED_VALUE_TRANSFER_MEMO',
  from: sender.address,
  to: '0x75c3098Be5E4B63FBAc05838DaAEE378dD48098d',
  gas: '300000',
  value: caver.utils.toPeb('1', 'KLAY'),
  data: '0x68656c6c6f',
}, sender.privateKey)

caver.klay.sendTransaction({
  senderRawTransaction: senderRawTransaction,
  feePayer: feePayer.address,
})
.then(function(receipt){
    ...
});

// using the event emitter
const { rawTransaction: senderRawTransaction } = await caver.klay.accounts.signTransaction({
  type: 'FEE_DELEGATED_VALUE_TRANSFER_MEMO',
  from: sender.address,
  to: '0x75c3098Be5E4B63FBAc05838DaAEE378dD48098d',
  gas: '300000',
  value: caver.utils.toPeb('1', 'KLAY'),
  data: '0x68656c6c6f',
}, sender.privateKey)

caver.klay.sendTransaction({
  senderRawTransaction: senderRawTransaction,
  feePayer: feePayer.address,
})
.on('transactionHash', function(hash){
    ...
})
.on('receipt', function(receipt){
    ...
})
.on('error', console.error); // If an out-of-gas error, the second parameter is the receipt.
```


## sendTransaction (FEE_DELEGATED_VALUE_TRANSFER_MEMO_WITH_RATIO) <a id="sendtransaction-fee_delegated_value_transfer_memo_with_ratio"></a>

```javascript
caver.klay.sendTransaction(transactionObject [, callback])
```
Sends a [Fee Delegated Value Transfer Memo With Ratio](../../../../../../klaytn/design/transactions/partial-fee-delegation.md#txtypefeedelegatedvaluetransfermemowithratio) transaction to the network.

**Parameters**

The parameters of sendTransaction are a transaction object and a callback function.

| Name              | Type     | Description                                                                                                |
| ----------------- | -------- | ---------------------------------------------------------------------------------------------------------- |
| transactionObject | Object   | The transaction object to send.                                                                            |
| callback          | Function | (optional) Optional callback, returns an error object as the first parameter and the result as the second. |

A transaction object of type `FEE_DELEGATED_VALUE_TRANSFER_MEMO_WITH_RATIO` has the following structure:

| Name     | Type                                            | Description                                                                                                                                                                                                           |
| -------- | ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type     | String                                          | Transaction Type. "FEE_DELEGATED_VALUE_TRANSFER_MEMO_WITH_RATIO"                                                                                                                                                |
| from     | String                                          | Address of this transaction sender.                                                                                                                                                                                   |
| to       | String                                          | The destination address of the transaction.                                                                                                                                                                           |
| value    | Number &#124; String &#124; BN &#124; BigNumber | The value transferred for the transaction in peb.                                                                                                                                                                     |
| data     | String                                          | The message to send with.                                                                                                                                                                                             |
| gas      | Number                                          | The maximum amount of gas willing to pay for the transaction (unused gas is refunded).                                                                                                                                |
| gasPrice | Number                                          | (optional) Gas price provided by the sender in peb. The gasPrice must be the same as the unitPrice set in the Klaytn node.                                                                                            |
| nonce    | Number                                          | (optional) Integer of a nonce. If omitted, it will be set by caver-js via calling `caver.klay.getTransactionCount`.                                                                                                   |
| feeRatio | Number                                          | Fee ratio of the fee payer. If it is 30, 30% of the fee will be paid by the fee payer. 70% will be paid by the sender. The range of fee ratio is 1 ~ 99, if it is out of range, the transaction will not be accepted. |

A transaction object of type `FEE_DELEGATED_VALUE_TRANSFER_MEMO_WITH_RATIO` with the above structure or an `RLP-encoded transaction` of type `FEE_DELEGATED_VALUE_TRANSFER_MEMO_WITH_RATIO` can be used as a parameter in [caver.klay.accounts.signTransaction](../caver.klay.accounts.md#signtransaction) for sender and in [caver.klay.accounts.feePayerSignTransaction](../caver.klay.accounts.md#feepayersigntransaction) for fee payer.

In order for the fee payer to sign an RLP encoded transaction signed by the sender and send it to the network, define an object with the following structure and call `caver.klay.sendTransaction`.

| Name                 | Type   | Description                                   |
| -------------------- | ------ | --------------------------------------------- |
| feePayer             | String | The fee payer address of the transaction.     |
| senderRawTransaction | String | The RLP-encoded transaction signed by sender. |

**Return Value**

The `callback` will return the 32-byte transaction hash.

`PromiEvent`: A promise combined event emitter. Will be resolved when the transaction receipt is available. Additionally the following events are available:

- `"transactionHash"` returns `String`: Is fired right after the transaction is sent and a transaction hash is available.
- `"receipt"` returns `Object`: Is fired when the transaction receipt is available.
- `"error"` returns `Error`: Is fired if an error occurs during sending. On an out-of-gas error, the second parameter is the receipt.

**Example**

```javascript
const sender = caver.klay.accounts.wallet.add('0x{private key}')
const feePayer = caver.klay.accounts.wallet.add('0x{private key}')

// using the promise
const { rawTransaction: senderRawTransaction } = await caver.klay.accounts.signTransaction({
  type: 'FEE_DELEGATED_VALUE_TRANSFER_MEMO_WITH_RATIO',
  from: sender.address,
  to: '0x75c3098Be5E4B63FBAc05838DaAEE378dD48098d',
  gas: '300000',
  feeRatio: 20,
  data: '0x68656c6c6f',
  value: caver.utils.toPeb('1', 'KLAY'),
}, sender.privateKey)

caver.klay.sendTransaction({
  senderRawTransaction: senderRawTransaction,
  feePayer: feePayer.address,
})
.then(function(receipt){
    ...
});

// using the event emitter
const { rawTransaction: senderRawTransaction } = await caver.klay.accounts.signTransaction({
  type: 'FEE_DELEGATED_VALUE_TRANSFER_MEMO_WITH_RATIO',
  from: sender.address,
  to: '0x75c3098Be5E4B63FBAc05838DaAEE378dD48098d',
  gas: '300000',
  feeRatio: 20,
  data: '0x68656c6c6f',
  value: caver.utils.toPeb('1', 'KLAY'),
}, sender.privateKey)

caver.klay.sendTransaction({
  senderRawTransaction: senderRawTransaction,
  feePayer: feePayer.address,
})
.on('transactionHash', function(hash){
    ...
})
.on('receipt', function(receipt){
    ...
})
.on('error', console.error); // If an out-of-gas error, the second parameter is the receipt.
```


