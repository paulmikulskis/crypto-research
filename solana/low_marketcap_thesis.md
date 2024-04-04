- [Introduction](#introduction)
- [Research](#research)


# Introduction

I have been watching [$HABIBI](https://dexscreener.com/solana/2ukgjDC99Nk34RfRjWjCoHAuQLtLnz8TLcBrDQk3f2ay) since its mid-day inception on March 30, 2024. The totaly supply of $HABIBI is 1 billion, meaning the current price is reflective of it's market cap valuation. The coin quickly pumped to it's all time high (ATH) of $3 million market cap two and a half hours after launch before quickly coming down to around $400,000 market cap. Over the course of the next few days, the coin would hover around around $600,000 market cap, but it would periodically pump between $1 - 2 million market cap. The most notable observation that I made was how the market moved around buy or sell transactions that were only between $1000-5000. This document contains research regarding this phenomena.  

# Largest Swap Amounts by Transaction Type

I wrote the following code to look at all swaps in and out of $HABIBI:

```
sql
SELECT
    BLOCK_TIMESTAMP,
    CASE
      WHEN SWAP_FROM_MINT = '864YJRb3JAVARC4FNuDtPKFxdEsYRbB39Nwxkzudxy46' THEN 'SELL'
      WHEN SWAP_TO_MINT = '864YJRb3JAVARC4FNuDtPKFxdEsYRbB39Nwxkzudxy46' THEN 'BUY'
    END AS TX_TYPE,
    SWAPPER,
    SWAP_FROM_AMOUNT,
    SWAP_TO_AMOUNT,
    SWAP_FROM_MINT,
    SWAP_TO_MINT
FROM
solana.defi.fact_swaps
WHERE
(
    BLOCK_TIMESTAMP BETWEEN '2024-03-31'
    AND '2024-04-02'
)
AND (
    SWAP_FROM_MINT = '864YJRb3JAVARC4FNuDtPKFxdEsYRbB39Nwxkzudxy46'
    OR SWAP_TO_MINT = '864YJRb3JAVARC4FNuDtPKFxdEsYRbB39Nwxkzudxy46'
)
ORDER BY
BLOCK_TIMESTAMP ASC
```s

