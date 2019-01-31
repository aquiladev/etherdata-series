# etherdata-series

## General
Height:
```
SELECT number
FROM `bigquery-public-data.ethereum_blockchain.blocks`
WHERE timestamp = (
  SELECT MAX(b.timestamp)
  FROM `bigquery-public-data.ethereum_blockchain.blocks` AS b
)
```

## 1
Etherdata - analytics platform for Ethereum

---
## 2
**http://etherdata.net**

tells you the truth about Ethereum

---
## 3
**Approximately 62% of blocks were mined by 5 mining pools**

(Etherscan, DwarfPool, Nanopool, F2Pool, SparkPool)

*#7141386*

---
## 4

In average block contains **53.735513003286336** transactions

*#7141386*

```
SELECT AVG(transaction_count)
FROM `bigquery-public-data.ethereum_blockchain.blocks`
```

---
## 5

There are **2275648** contracts deployed in Ethereum

*#7146256*

```
SELECT COUNT(*)
FROM `bigquery-public-data.ethereum_blockchain.contracts`
```

---
## 6

**33%** of deployed contracts have at least one transaction

*#7141386*

---
## 7

**19.17809784%** of contracts are being used for more than a week, **1.286622536%** of contracts are being used for more than a year

*#7146256*

---
## 8

Contract obsolescence

*#7151205*

---