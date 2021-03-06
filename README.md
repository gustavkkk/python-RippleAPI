# python-RippleAPI
This library provides a python interface to rippled using the JSON-RPC API.  This library strives to have a similar interface to the official javascript ripple-lib:

https://github.com/ripple/ripple-lib


# Usage
## Install the package direct from github
```
pip install git+https://github.com/patrickshuff/python-RippleAPI
```

## RECOMMENDED:  Generate your own keys and use Ripple TESTNet
Go here to generate some keys before testing out this framework:
https://ripple.com/build/xrp-test-net/

## Import the library
```python
from rippleapi import (
    RippleClient,
    RippleTransaction,
)
```
## Instantiate a client object
```python
client = RippleClient()
```
## View current balance of an account
```python
client.account_info('rDHpP3xnG2QRNtZc4KJPvtX3hidZbKRYHz')
{'result': {'account_data': {'Account': 'rDHpP3xnG2QRNtZc4KJPvtX3hidZbKRYHz',
   'Balance': '10000000000',
   'Flags': 0,
   'LedgerEntryType': 'AccountRoot',
   'OwnerCount': 0,
   'PreviousTxnID': 'B8762A039E2B7805816C1F02A1CC7F5CE57302B1EA3055886A5C194BB6AD34CC',
   'PreviousTxnLgrSeq': 6803402,
   'Sequence': 1,
   'index': 'B3B81BAAC0EFC7FC11246C2B472E19994EA1CF9891967EC8674E6AB0956002B9'},
  'ledger_hash': '4986844B7AF1C3A44F5FDF16687359E9CE361148580F1D2A195F91D75A529A77',
  'ledger_index': 6804857,
  'status': 'success',
  'validated': True}}
```

## Create a new transaction
```python
tx = RippleTransaction(
    source_address='r9tGBU3Pg43r1xK9bHgfbsVXtLUWaRMYbK',
    destination_address='rDHpP3xnG2QRNtZc4KJPvtX3hidZbKRYHz',
    amount=100,
    currency="USD",
)

signed_transaction = client.sign(secret_key=YOUR_SECRET_KEY, tx)
```
## Submit your signed transaction to be executed
```python
client.submit(signed_transaction['result']['tx_blob'])
```
## View your account transactions
```python
client.account_tx('r9tGBU3Pg43r1xK9bHgfbsVXtLUWaRMYbK')`
```
