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

**Contact:**

For any questions feel free to send me a DM on Twitter: https://twitter.com/martkiro

# Examples

Each one of the below examples is a cURL request but you can use any other client too. Just copy paste into your terminal. No API key needed.

### Example #1: Most Recent ENJ-USD Tick Price

**Query**


    curl --location --request POST 'https://api.syve.ai/v1/prices_usd' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "filter": {
            "type": "eq",
            "params": {
                "field": "token_address",
                "value": "0xF629cBd94d3791C9250152BD8dfBDF380E2a3B9c"
            }
        },
        "options": [
            {
                "type": "size",
                "params": {
                    "value": 1
                }
            }
        ]
    }'

**Response**


    {
        "results": [
            {
                "block_number": 16871018,
                "date_time": "2023-03-20T19:38:47",
                "timestamp": 1679341127,
                "token_address": "0xf629cbd94d3791c9250152bd8dfbdf380e2a3b9c",
                "price_usd_token": 0.3979492679843635
            }
        ],
        "cursor": {
            "next": "MTY4NzEwMTgsMHhmNjI5Y2JkOTRkMzc5MWM5MjUwMTUyYmQ4ZGZiZGYzODBlMmEzYjljOjE2NzkzNDEyMjU="
        }
    }


### Example #2: Price at a particular block

**Query**


    curl --location --request POST 'https://api.syve.ai/v1/prices_usd' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "filter": {
            "type": "and",
            "params": {
                "filters": [
                    {
                        "type": "eq",
                        "params": {
                            "field": "block_number",
                            "value": 16871164
                        }
                    },
                    {
                        "type": "eq",
                        "params": {
                            "field": "token_address",
                            "value": "0xf629cbd94d3791c9250152bd8dfbdf380e2a3b9c"
                        }
                    }
                ]
            }
        },
        "options": [
            {
                "type": "sort",
                "params": {
                    "field": "block_number",
                    "value": "desc"
                }
            },
            {
                "type": "size",
                "params": {
                    "value": 5
                }
            }
        ]
    }'

**Response**


    {
        "results": [
            {
                "block_number": 16871164,
                "date_time": "2023-03-20T20:08:23",
                "timestamp": 1679342903,
                "token_address": "0xf629cbd94d3791c9250152bd8dfbdf380e2a3b9c",
                "price_usd_token": 0.39984728377502077
            }
        ],
        "cursor": {
            "next": "MTY4NzExNjQsMHhmNjI5Y2JkOTRkMzc5MWM5MjUwMTUyYmQ4ZGZiZGYzODBlMmEzYjljOjE2NzkzNDM0Nzg="
        }
    }


### Example #3: Most Recent Tick Price Multiple Tokens

**Query**

The following give you the latest 10 prices of both MATIC and LINK.


    curl --location --request POST 'https://api.syve.ai/v1/prices_usd' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "filter": {
            "type": "or",
            "params": {
                "filters": [
                    {
                        "type": "eq",
                        "params": {
                            "field": "token_address",
                            "value": "0x7D1AfA7B718fb893dB30A3aBc0Cfc608AaCfeBB0"
                        }
                    },
                    {
                        "type": "eq",
                        "params": {
                            "field": "token_address",
                            "value": "0x514910771af9ca656af840dff83e8264ecf986ca"
                        }
                    }
                ]
            }
        },
        "options": [
            {
                "type": "sort",
                "params": {
                    "field": "block_number",
                    "value": "desc"
                }
            },
            {
                "type": "size",
                "params": {
                    "value": 10
                }
            }
        ]
    }'

**Response**


    {
        "results": [
            {
                "block_number": 16871001,
                "date_time": "2023-03-20T19:35:23",
                "timestamp": 1679340923,
                "token_address": "0x7d1afa7b718fb893db30a3abc0cfc608aacfebb0",
                "price_usd_token": 1.122250746625519
            },
            ...
            {
                "block_number": 16870946,
                "date_time": "2023-03-20T19:24:23",
                "timestamp": 1679340263,
                "token_address": "0x514910771af9ca656af840dff83e8264ecf986ca",
                "price_usd_token": 7.105304883017842
            }
        ],
        "cursor": {
            "next": "MTY4NzA5NDYsMHg1MTQ5MTA3NzFhZjljYTY1NmFmODQwZGZmODNlODI2NGVjZjk4NmNhOjE2NzkzNDA5OTM="
        }
    }


### Example #4: OHLC ENJ-USD Prices

**Query**

    curl --location --request POST 'https://api.syve.ai/v1/prices_usd' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "filter": {
            "type": "eq",
            "params": {
                "field": "token_address",
                "value": "0x7D1AfA7B718fb893dB30A3aBc0Cfc608AaCfeBB0"
            }
        },
        "bucket": {
            "type": "range",
            "params": {
                "field": "timestamp",
                "interval": "1h"
            }
        },
        "aggregate": [
            {
                "type": "open",
                "params": {
                    "field": "price_usd_token"
                }
            },
            {
                "type": "max",
                "params": {
                    "field": "price_usd_token"
                }
            },
            {
                "type": "min",
                "params": {
                    "field": "price_usd_token"
                }
            },
            {
                "type": "close",
                "params": {
                    "field": "price_usd_token"
                }
            }
        ],
        "options": [
            {
                "type": "size",
                "params": {
                    "value": 5
                }
            },
            {
                "type": "sort",
                "params": {
                    "field": "timestamp",
                    "value": "desc"
                }
            }
        ]
    }'

**Response**


    {
        "results": [
            {
                "timestamp": 1679342400,
                "count": 3,
                "date_time": "2023-03-20T20:00:00",
                "price_usd_token_open": 1.125650197431152,
                "price_usd_token_max": 1.125650197431152,
                "price_usd_token_min": 1.1219963295046023,
                "price_usd_token_close": 1.1219963295046023
            },
            {
                "timestamp": 1679338800,
                "count": 33,
                "date_time": "2023-03-20T19:00:00",
                "price_usd_token_open": 1.1340858339317443,
                "price_usd_token_max": 1.1373061893659984,
                "price_usd_token_min": 1.1134334085370152,
                "price_usd_token_close": 1.116167408561591
            },
            {
                "timestamp": 1679335200,
                "count": 33,
                "date_time": "2023-03-20T18:00:00",
                "price_usd_token_open": 1.1245935804346712,
                "price_usd_token_max": 1.2485457800525135,
                "price_usd_token_min": 1.1239942495981408,
                "price_usd_token_close": 1.1339965792022242
            },
            {
                "timestamp": 1679331600,
                "count": 21,
                "date_time": "2023-03-20T17:00:00",
                "price_usd_token_open": 1.1262094955461326,
                "price_usd_token_max": 1.1378943386182778,
                "price_usd_token_min": 1.1262094955461326,
                "price_usd_token_close": 1.1361072914389625
            },
            {
                "timestamp": 1679328000,
                "count": 21,
                "date_time": "2023-03-20T16:00:00",
                "price_usd_token_open": 1.1351638890696771,
                "price_usd_token_max": 1.1785396407407382,
                "price_usd_token_min": 1.126503511130738,
                "price_usd_token_close": 1.131329771135796
            }
        ],
        "cursor": {
            "next": "MTY3OTMyODAwMDAwMDoxNjc5MzQyNTg0"
        }
    }
