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
## 9

In average contract contains **5.199765300477151** functions
*#7160984*

```
SELECT AVG(ARRAY_LENGTH(function_sighashes))
FROM `bigquery-public-data.ethereum_blockchain.contracts`
```

---
## 10

There are **1790.3942006269608** contracts deployed daily

-OR-

In average **1790.3942006269608** contracts deployed daily

*#7165919*

```
SELECT AVG(c)
FROM (
  SELECT TIMESTAMP_TRUNC(block_timestamp, DAY) AS d, COUNT(*) AS c
  FROM `bigquery-public-data.ethereum_blockchain.contracts`
  GROUP BY 1
)
```

---
## 11

Average growth rate of contracts' amount is **33.103825136612016%**

*#7170777*

```
SELECT AVG(c_growth_percent)
FROM (
  SELECT d, c, prev_c, ROUND(100 * (c - prev_c)/prev_c) c_growth_percent
  FROM (
    SELECT d, c, LAG(c, 1) OVER(ORDER BY d) prev_c
    FROM (
      SELECT TIMESTAMP_TRUNC(block_timestamp, WEEK) AS d, COUNT(*) AS c
      FROM `bigquery-public-data.ethereum_blockchain.contracts`
      GROUP BY 1
      ORDER BY 1
    )
  )
)
```

---
## 12

Average growth rate of transactions' amount is **4.672131147540986%**

*#7175715*

```
SELECT AVG(c_growth_percent)
FROM (
  SELECT d, c, prev_c, ROUND(100 * (c - prev_c)/prev_c) c_growth_percent
  FROM (
    SELECT d, c, LAG(c, 1) OVER(ORDER BY d) prev_c
    FROM (
      SELECT TIMESTAMP_TRUNC(block_timestamp, WEEK) AS d, COUNT(*) AS c
      FROM `bigquery-public-data.ethereum_blockchain.transactions` 
      GROUP BY 1
      ORDER BY 1
    )
  )
)
```

---