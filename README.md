# dex-prices-syve

A free API endpoint for fetching historical as well as the latest prices of tokens traded on Ethereum DEXs.

Use the endpoint to:

- Fetch real-time crypto price data (block-by-block each time a trade was made)
- Fetch OHLC price data at different resolutions as low as second-by-second. Possible resolutions include: 1s, 1min, 5min, 15min, 30min, 1h, 4h, 1d.
- Download historical token price data (from the beginning when the first DEX swap was made for a token).
- Fetch 100,000 price data points at a time in a single request.

A free API endpoint for fetching historical as well as the latest prices of tokens traded on Ethereum DEXs.

Use the endpoint to:

- Fetch real-time crypto price data (block-by-block each time a trade was made)
- Fetch OHLC price data at different resolutions as low as second-by-second. Possible resolutions include: 1s, 1min, 5min, 15min, 30min, 1h, 4h, 1d.
- Download historical token price data (from the beginning when the first DEX swap was made for a token).
- Fetch 100,000 price data points at a time in a single request.

**Examples** of how to use the API are given below. The examples should be enough for most use-cases. But if you are curious and/or need more information you can read the **documentation** of the endpoint here: https://syve.readme.io/reference/erc20-prices-usd

Notes:

- Token USD prices are calculated based on parsing swap event logs emitted by the top DEX pools on Ethereum.
- Token prices are given for every token traded in the top 3000 DEX pools.
- Top DEX pools include Uniswap-V2, Uniswap-V3 and SushiSwap
