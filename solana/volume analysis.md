# Volume Analysis using Flipside Data

## Thesis


Examining tokens with the most volume from the previous hour can be important in building crypto trading bots for several reasons:

- High volume often indicates high liquidity, making it easier to enter and exit trades without significant price impact.
- Increased trading volume can signal market interest and potential price movements, helping to identify opportunities for profit.
- Analyzing recent high-volume tokens helps the bot adapt to current market trends and focus on the most actively traded assets, increasing the chances of successful trades.
- Monitoring volume can help in identifying sudden spikes or drops, which might indicate upcoming volatility or market sentiment changes.

## Largest Volume Tokens within the Previous Hour SQL Query

This SQL query aggregates the top $ETH based tokens that had the largest volume from the previous hour:

    WITH last_hour AS (
    SELECT
        symbol,
        SUM(amount) AS total_volume
    FROM
        ethereum.core.ez_token_transfers
    WHERE
        block_timestamp >= DATEADD(hour, -1, CURRENT_TIMESTAMP())
    GROUP BY
        symbol
    )
    SELECT
        symbol,
        total_volume
    FROM
        last_hour
    ORDER BY
        total_volume DESC
    LIMIT
        10;

This SQL query aggregates the top $SOL based tokens that had the largest volume from the previous hour:

    WITH last_hour_volume AS (
    SELECT
        mint AS token_address,
        SUM(amount) AS volume
    FROM
        solana.core.fact_transfers
    WHERE
        block_timestamp >= DATEADD(hour, -1, CURRENT_TIMESTAMP())
    GROUP BY
        token_address
    ORDER BY
        volume DESC
    )

    SELECT
        token_address
    FROM
        last_hour_volume
    LIMIT 100



