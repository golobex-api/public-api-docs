# Public REST API for Golobex
# General API Information
* The base endpoint is: **https://golobex.com/api/v1/**
* All endpoints can return a JSON object, array, or void (just ```200 OK```).
* All time and timestamp related fields are in milliseconds.
* HTTP `4XX` return codes are used for for malformed requests; the issue is on the sender's side.
* HTTP `5XX` return codes are used for internal errors; the issue is on server's side.
  It is important to **NOT** treat this as a failure operation; the execution status is **UNKNOWN** and could have been a success.
* For `GET` endpoints, parameters must be sent as a `query string`.
* For `POST`, `PUT`, and `DELETE` endpoints, the parameters must be sent in the `request body` with content type
  `application/json`.

  # LIMITS
  As it is now, API calls are unlimited.

  # Endpoint security type
* Each endpoint has a security type that determines the how you will
  interact with it.
* API-keys are passed into the Rest API via the `X-CX-APIKEY`
  header.
* API-keys and secret-keys **are case sensitive**.
* API-keys can be configured to only access certain types of secure endpoints.
 For example, one API-key could be used for TRADE only, while another API-key
 can access everything except for TRADE routes.
* By default, API-keys can access secured info and trades, but not a withdrawals.

Security Type | Description
------------ | ------------
USER_DATA | Endpoint requires sending a valid API-Key.
TRADE | Endpoint requires sending a valid API-Key.
WITHDRAW | Endpoint requires sending a valid API-Key.

# General endpoints

### Orders
```
POST /orders
```
**Required permission** ```TRADING```

**Params**

Name | Description
------------ | ------------
validOrder * (body) | validOrder

*Example Value*
```javascript
{
  "amount": 0,
  "distance": 0,
  "managedOrder": true,
  "market": true,
  "pairName": "string",
  "price": 0,
  "side": "BUY",
  "slPrice": 0,
  "sltp": true,
  "tpPrice": 0,
  "trailing": true
}
```
**Response:**
```200 OK```

#

```
DELETE /orders/{id}
```
**Required permission** ```TRADING```

**Params**

Name | Description
------------ | ------------
id * string (path) | id

**Response:**
```200 OK```

#
```
GET /orders/active
```
**Response:**
```javascript
[
  {
    "binanceOrder": true,
    "commissionOnCurrencyOfOrder": true,
    "currencyFirst": "ETH",
    "currencySecond": "ETH",
    "date": 0,
    "feeCurrency": "ETH",
    "feeSum": 0,
    "id": "string",
    "initialQuantity": 0,
    "market": true,
    "pairName": "string",
    "price": 0,
    "quantity": 0,
    "shouldWaitForMatch": true,
    "side": "BUY",
    "slPrice": 0,
    "sltp": true,
    "sum": 0,
    "total": 0,
    "totalWithOutFee": 0,
    "tpPrice": 0,
    "trailingDistance": 0,
    "trailingRange": 0,
    "traling": true,
    "userId": "string"
  }
]
```



#

```
POST /orders/market
```
**Required permission** ```TRADING```

**Params**

Name | Description
------------ | ------------
marketOrder * (body) | marketOrder

*Example Value*
```javascript
{
  "amount": 0,
  "distance": 0,
  "managedOrder": true,
  "market": true,
  "pairName": "string",
  "price": 0,
  "side": "BUY",
  "slPrice": 0,
  "sltp": true,
  "tpPrice": 0,
  "trailing": true
}
```
**Response:**
```200 OK```

#
```
POST /orders/sltp
```
**Required permission** ```TRADING```

**Params**

Name | Description
------------ | ------------
sltpOrder * (body) | sltpOrder

*Example Value*
```javascript
{
  "amount": 0,
  "distance": 0,
  "managedOrder": true,
  "market": true,
  "pairName": "string",
  "price": 0,
  "side": "BUY",
  "slPrice": 0,
  "sltp": true,
  "tpPrice": 0,
  "trailing": true
}
```
**Response:**
```200 OK```



#
```
POST /orders/trailing
```
**Required permission** ```TRADING```

**Params**

Name | Description
------------ | ------------
validOrder * (body) | validOrder

*Example Value*
```javascript
{
  "amount": 0,
  "distance": 0,
  "managedOrder": true,
  "market": true,
  "pairName": "string",
  "price": 0,
  "side": "BUY",
  "slPrice": 0,
  "sltp": true,
  "tpPrice": 0,
  "trailing": true
}
```
**Response:**
```200 OK```

#
### Pairs
```
GET /pairs/
```
**Response:**
```javascript
[
  {
    "afterDecimalPoint": 0,
    "candle": {
      "closePrice": 0,
      "date": 0,
      "highPrice": 0,
      "id": "string",
      "lowPrice": 0,
      "openPrice": 0,
      "pairName": "string",
      "volume": 0
    },
    "candlesCounter": {
      "acquire": 0,
      "andDecrement": 0,
      "andIncrement": 0,
      "opaque": 0,
      "plain": 0
    },
    "currencyFirst": "ETH",
    "currencyLast": "ETH",
    "currentPrice": 0,
    "enabled": true,
    "firstCurrencyCommission": 0,
    "id": "string",
    "lastCurrencyCommission": 0,
    "minPrice": 0,
    "minQuantity": 0,
    "orderBook": {
      "bestBuyPrice": 0,
      "bestSellPrice": 0,
      "buyOrders": {
        "additionalProp1": [
          {
            "binanceOrder": true,
            "commissionOnCurrencyOfOrder": true,
            "currencyFirst": "ETH",
            "currencySecond": "ETH",
            "date": 0,
            "feeCurrency": "ETH",
            "feeSum": 0,
            "id": "string",
            "initialQuantity": 0,
            "market": true,
            "pairName": "string",
            "price": 0,
            "quantity": 0,
            "shouldWaitForMatch": true,
            "side": "BUY",
            "slPrice": 0,
            "sltp": true,
            "sum": 0,
            "total": 0,
            "totalWithOutFee": 0,
            "tpPrice": 0,
            "trailingDistance": 0,
            "trailingRange": 0,
            "traling": true,
            "userId": "string"
          }
        ],
        "additionalProp2": [
          {
            "binanceOrder": true,
            "commissionOnCurrencyOfOrder": true,
            "currencyFirst": "ETH",
            "currencySecond": "ETH",
            "date": 0,
            "feeCurrency": "ETH",
            "feeSum": 0,
            "id": "string",
            "initialQuantity": 0,
            "market": true,
            "pairName": "string",
            "price": 0,
            "quantity": 0,
            "shouldWaitForMatch": true,
            "side": "BUY",
            "slPrice": 0,
            "sltp": true,
            "sum": 0,
            "total": 0,
            "totalWithOutFee": 0,
            "tpPrice": 0,
            "trailingDistance": 0,
            "trailingRange": 0,
            "traling": true,
            "userId": "string"
          }
        ],
        "additionalProp3": [
          {
            "binanceOrder": true,
            "commissionOnCurrencyOfOrder": true,
            "currencyFirst": "ETH",
            "currencySecond": "ETH",
            "date": 0,
            "feeCurrency": "ETH",
            "feeSum": 0,
            "id": "string",
            "initialQuantity": 0,
            "market": true,
            "pairName": "string",
            "price": 0,
            "quantity": 0,
            "shouldWaitForMatch": true,
            "side": "BUY",
            "slPrice": 0,
            "sltp": true,
            "sum": 0,
            "total": 0,
            "totalWithOutFee": 0,
            "tpPrice": 0,
            "trailingDistance": 0,
            "trailingRange": 0,
            "traling": true,
            "userId": "string"
          }
        ]
      },
      "buyOrdersDepth": 0,
      "completeOrderPrice2Tics": {
        "additionalProp1": {
          "number": 0,
          "updateTime": "2019-02-11T17:01:07.650Z"
        },
        "additionalProp2": {
          "number": 0,
          "updateTime": "2019-02-11T17:01:07.650Z"
        },
        "additionalProp3": {
          "number": 0,
          "updateTime": "2019-02-11T17:01:07.650Z"
        }
      },
      "firstBuyPrice": 0,
      "firstSellPrice": 0,
      "sellOrders": {
        "additionalProp1": [
          {
            "binanceOrder": true,
            "commissionOnCurrencyOfOrder": true,
            "currencyFirst": "ETH",
            "currencySecond": "ETH",
            "date": 0,
            "feeCurrency": "ETH",
            "feeSum": 0,
            "id": "string",
            "initialQuantity": 0,
            "market": true,
            "pairName": "string",
            "price": 0,
            "quantity": 0,
            "shouldWaitForMatch": true,
            "side": "BUY",
            "slPrice": 0,
            "sltp": true,
            "sum": 0,
            "total": 0,
            "totalWithOutFee": 0,
            "tpPrice": 0,
            "trailingDistance": 0,
            "trailingRange": 0,
            "traling": true,
            "userId": "string"
          }
        ],
        "additionalProp2": [
          {
            "binanceOrder": true,
            "commissionOnCurrencyOfOrder": true,
            "currencyFirst": "ETH",
            "currencySecond": "ETH",
            "date": 0,
            "feeCurrency": "ETH",
            "feeSum": 0,
            "id": "string",
            "initialQuantity": 0,
            "market": true,
            "pairName": "string",
            "price": 0,
            "quantity": 0,
            "shouldWaitForMatch": true,
            "side": "BUY",
            "slPrice": 0,
            "sltp": true,
            "sum": 0,
            "total": 0,
            "totalWithOutFee": 0,
            "tpPrice": 0,
            "trailingDistance": 0,
            "trailingRange": 0,
            "traling": true,
            "userId": "string"
          }
        ],
        "additionalProp3": [
          {
            "binanceOrder": true,
            "commissionOnCurrencyOfOrder": true,
            "currencyFirst": "ETH",
            "currencySecond": "ETH",
            "date": 0,
            "feeCurrency": "ETH",
            "feeSum": 0,
            "id": "string",
            "initialQuantity": 0,
            "market": true,
            "pairName": "string",
            "price": 0,
            "quantity": 0,
            "shouldWaitForMatch": true,
            "side": "BUY",
            "slPrice": 0,
            "sltp": true,
            "sum": 0,
            "total": 0,
            "totalWithOutFee": 0,
            "tpPrice": 0,
            "trailingDistance": 0,
            "trailingRange": 0,
            "traling": true,
            "userId": "string"
          }
        ]
      },
      "sellOrdersDepth": 0,
      "sltpOrders": [
        {
          "binanceOrder": true,
          "commissionOnCurrencyOfOrder": true,
          "currencyFirst": "ETH",
          "currencySecond": "ETH",
          "date": 0,
          "feeCurrency": "ETH",
          "feeSum": 0,
          "id": "string",
          "initialQuantity": 0,
          "market": true,
          "pairName": "string",
          "price": 0,
          "quantity": 0,
          "shouldWaitForMatch": true,
          "side": "BUY",
          "slPrice": 0,
          "sltp": true,
          "sum": 0,
          "total": 0,
          "totalWithOutFee": 0,
          "tpPrice": 0,
          "trailingDistance": 0,
          "trailingRange": 0,
          "traling": true,
          "userId": "string"
        }
      ],
      "trailingOrders": [
        {
          "binanceOrder": true,
          "commissionOnCurrencyOfOrder": true,
          "currencyFirst": "ETH",
          "currencySecond": "ETH",
          "date": 0,
          "feeCurrency": "ETH",
          "feeSum": 0,
          "id": "string",
          "initialQuantity": 0,
          "market": true,
          "pairName": "string",
          "price": 0,
          "quantity": 0,
          "shouldWaitForMatch": true,
          "side": "BUY",
          "slPrice": 0,
          "sltp": true,
          "sum": 0,
          "total": 0,
          "totalWithOutFee": 0,
          "tpPrice": 0,
          "trailingDistance": 0,
          "trailingRange": 0,
          "traling": true,
          "userId": "string"
        }
      ]
    },
    "ordersForME": [
      {
        "binanceOrder": true,
        "commissionOnCurrencyOfOrder": true,
        "currencyFirst": "ETH",
        "currencySecond": "ETH",
        "date": 0,
        "feeCurrency": "ETH",
        "feeSum": 0,
        "id": "string",
        "initialQuantity": 0,
        "market": true,
        "pairName": "string",
        "price": 0,
        "quantity": 0,
        "shouldWaitForMatch": true,
        "side": "BUY",
        "slPrice": 0,
        "sltp": true,
        "sum": 0,
        "total": 0,
        "totalWithOutFee": 0,
        "tpPrice": 0,
        "trailingDistance": 0,
        "trailingRange": 0,
        "traling": true,
        "userId": "string"
      }
    ],
    "pairInfo": {
      "currentPrice": 0,
      "dailyChange": 0,
      "dailyHigh": 0,
      "dailyLow": 0,
      "dailyVolume": 0,
      "prevDailyChange": 0,
      "prevDailyHigh": 0,
      "prevDailyLow": 0,
      "prevDailyVolume": 0,
      "statisticalDay": 0
    },
    "pairName": "string",
    "timeFrame2Candle": {
      "additionalProp1": {
        "closePrice": 0,
        "date": 0,
        "highPrice": 0,
        "id": "string",
        "lowPrice": 0,
        "openPrice": 0,
        "pairName": "string",
        "volume": 0
      },
      "additionalProp2": {
        "closePrice": 0,
        "date": 0,
        "highPrice": 0,
        "id": "string",
        "lowPrice": 0,
        "openPrice": 0,
        "pairName": "string",
        "volume": 0
      },
      "additionalProp3": {
        "closePrice": 0,
        "date": 0,
        "highPrice": 0,
        "id": "string",
        "lowPrice": 0,
        "openPrice": 0,
        "pairName": "string",
        "volume": 0
      }
    }
  }
]
```

#

```
GET /pairs/{pairName}
```
**Params**

Name | Description
------------ | ------------
pairName * string (path) | pairName

**Response:**
```javascript
{
  "afterDecimalPoint": 0,
  "candle": {
    "closePrice": 0,
    "date": 0,
    "highPrice": 0,
    "id": "string",
    "lowPrice": 0,
    "openPrice": 0,
    "pairName": "string",
    "volume": 0
  },
  "candlesCounter": {
    "acquire": 0,
    "andDecrement": 0,
    "andIncrement": 0,
    "opaque": 0,
    "plain": 0
  },
  "currencyFirst": "ETH",
  "currencyLast": "ETH",
  "currentPrice": 0,
  "enabled": true,
  "firstCurrencyCommission": 0,
  "id": "string",
  "lastCurrencyCommission": 0,
  "minPrice": 0,
  "minQuantity": 0,
  "orderBook": {
    "bestBuyPrice": 0,
    "bestSellPrice": 0,
    "buyOrders": {
      "additionalProp1": [
        {
          "binanceOrder": true,
          "commissionOnCurrencyOfOrder": true,
          "currencyFirst": "ETH",
          "currencySecond": "ETH",
          "date": 0,
          "feeCurrency": "ETH",
          "feeSum": 0,
          "id": "string",
          "initialQuantity": 0,
          "market": true,
          "pairName": "string",
          "price": 0,
          "quantity": 0,
          "shouldWaitForMatch": true,
          "side": "BUY",
          "slPrice": 0,
          "sltp": true,
          "sum": 0,
          "total": 0,
          "totalWithOutFee": 0,
          "tpPrice": 0,
          "trailingDistance": 0,
          "trailingRange": 0,
          "traling": true,
          "userId": "string"
        }
      ],
      "additionalProp2": [
        {
          "binanceOrder": true,
          "commissionOnCurrencyOfOrder": true,
          "currencyFirst": "ETH",
          "currencySecond": "ETH",
          "date": 0,
          "feeCurrency": "ETH",
          "feeSum": 0,
          "id": "string",
          "initialQuantity": 0,
          "market": true,
          "pairName": "string",
          "price": 0,
          "quantity": 0,
          "shouldWaitForMatch": true,
          "side": "BUY",
          "slPrice": 0,
          "sltp": true,
          "sum": 0,
          "total": 0,
          "totalWithOutFee": 0,
          "tpPrice": 0,
          "trailingDistance": 0,
          "trailingRange": 0,
          "traling": true,
          "userId": "string"
        }
      ],
      "additionalProp3": [
        {
          "binanceOrder": true,
          "commissionOnCurrencyOfOrder": true,
          "currencyFirst": "ETH",
          "currencySecond": "ETH",
          "date": 0,
          "feeCurrency": "ETH",
          "feeSum": 0,
          "id": "string",
          "initialQuantity": 0,
          "market": true,
          "pairName": "string",
          "price": 0,
          "quantity": 0,
          "shouldWaitForMatch": true,
          "side": "BUY",
          "slPrice": 0,
          "sltp": true,
          "sum": 0,
          "total": 0,
          "totalWithOutFee": 0,
          "tpPrice": 0,
          "trailingDistance": 0,
          "trailingRange": 0,
          "traling": true,
          "userId": "string"
        }
      ]
    },
    "buyOrdersDepth": 0,
    "completeOrderPrice2Tics": {
      "additionalProp1": {
        "number": 0,
        "updateTime": "2019-02-11T17:01:41.872Z"
      },
      "additionalProp2": {
        "number": 0,
        "updateTime": "2019-02-11T17:01:41.872Z"
      },
      "additionalProp3": {
        "number": 0,
        "updateTime": "2019-02-11T17:01:41.872Z"
      }
    },
    "firstBuyPrice": 0,
    "firstSellPrice": 0,
    "sellOrders": {
      "additionalProp1": [
        {
          "binanceOrder": true,
          "commissionOnCurrencyOfOrder": true,
          "currencyFirst": "ETH",
          "currencySecond": "ETH",
          "date": 0,
          "feeCurrency": "ETH",
          "feeSum": 0,
          "id": "string",
          "initialQuantity": 0,
          "market": true,
          "pairName": "string",
          "price": 0,
          "quantity": 0,
          "shouldWaitForMatch": true,
          "side": "BUY",
          "slPrice": 0,
          "sltp": true,
          "sum": 0,
          "total": 0,
          "totalWithOutFee": 0,
          "tpPrice": 0,
          "trailingDistance": 0,
          "trailingRange": 0,
          "traling": true,
          "userId": "string"
        }
      ],
      "additionalProp2": [
        {
          "binanceOrder": true,
          "commissionOnCurrencyOfOrder": true,
          "currencyFirst": "ETH",
          "currencySecond": "ETH",
          "date": 0,
          "feeCurrency": "ETH",
          "feeSum": 0,
          "id": "string",
          "initialQuantity": 0,
          "market": true,
          "pairName": "string",
          "price": 0,
          "quantity": 0,
          "shouldWaitForMatch": true,
          "side": "BUY",
          "slPrice": 0,
          "sltp": true,
          "sum": 0,
          "total": 0,
          "totalWithOutFee": 0,
          "tpPrice": 0,
          "trailingDistance": 0,
          "trailingRange": 0,
          "traling": true,
          "userId": "string"
        }
      ],
      "additionalProp3": [
        {
          "binanceOrder": true,
          "commissionOnCurrencyOfOrder": true,
          "currencyFirst": "ETH",
          "currencySecond": "ETH",
          "date": 0,
          "feeCurrency": "ETH",
          "feeSum": 0,
          "id": "string",
          "initialQuantity": 0,
          "market": true,
          "pairName": "string",
          "price": 0,
          "quantity": 0,
          "shouldWaitForMatch": true,
          "side": "BUY",
          "slPrice": 0,
          "sltp": true,
          "sum": 0,
          "total": 0,
          "totalWithOutFee": 0,
          "tpPrice": 0,
          "trailingDistance": 0,
          "trailingRange": 0,
          "traling": true,
          "userId": "string"
        }
      ]
    },
    "sellOrdersDepth": 0,
    "sltpOrders": [
      {
        "binanceOrder": true,
        "commissionOnCurrencyOfOrder": true,
        "currencyFirst": "ETH",
        "currencySecond": "ETH",
        "date": 0,
        "feeCurrency": "ETH",
        "feeSum": 0,
        "id": "string",
        "initialQuantity": 0,
        "market": true,
        "pairName": "string",
        "price": 0,
        "quantity": 0,
        "shouldWaitForMatch": true,
        "side": "BUY",
        "slPrice": 0,
        "sltp": true,
        "sum": 0,
        "total": 0,
        "totalWithOutFee": 0,
        "tpPrice": 0,
        "trailingDistance": 0,
        "trailingRange": 0,
        "traling": true,
        "userId": "string"
      }
    ],
    "trailingOrders": [
      {
        "binanceOrder": true,
        "commissionOnCurrencyOfOrder": true,
        "currencyFirst": "ETH",
        "currencySecond": "ETH",
        "date": 0,
        "feeCurrency": "ETH",
        "feeSum": 0,
        "id": "string",
        "initialQuantity": 0,
        "market": true,
        "pairName": "string",
        "price": 0,
        "quantity": 0,
        "shouldWaitForMatch": true,
        "side": "BUY",
        "slPrice": 0,
        "sltp": true,
        "sum": 0,
        "total": 0,
        "totalWithOutFee": 0,
        "tpPrice": 0,
        "trailingDistance": 0,
        "trailingRange": 0,
        "traling": true,
        "userId": "string"
      }
    ]
  },
  "ordersForME": [
    {
      "binanceOrder": true,
      "commissionOnCurrencyOfOrder": true,
      "currencyFirst": "ETH",
      "currencySecond": "ETH",
      "date": 0,
      "feeCurrency": "ETH",
      "feeSum": 0,
      "id": "string",
      "initialQuantity": 0,
      "market": true,
      "pairName": "string",
      "price": 0,
      "quantity": 0,
      "shouldWaitForMatch": true,
      "side": "BUY",
      "slPrice": 0,
      "sltp": true,
      "sum": 0,
      "total": 0,
      "totalWithOutFee": 0,
      "tpPrice": 0,
      "trailingDistance": 0,
      "trailingRange": 0,
      "traling": true,
      "userId": "string"
    }
  ],
  "pairInfo": {
    "currentPrice": 0,
    "dailyChange": 0,
    "dailyHigh": 0,
    "dailyLow": 0,
    "dailyVolume": 0,
    "prevDailyChange": 0,
    "prevDailyHigh": 0,
    "prevDailyLow": 0,
    "prevDailyVolume": 0,
    "statisticalDay": 0
  },
  "pairName": "string",
  "timeFrame2Candle": {
    "additionalProp1": {
      "closePrice": 0,
      "date": 0,
      "highPrice": 0,
      "id": "string",
      "lowPrice": 0,
      "openPrice": 0,
      "pairName": "string",
      "volume": 0
    },
    "additionalProp2": {
      "closePrice": 0,
      "date": 0,
      "highPrice": 0,
      "id": "string",
      "lowPrice": 0,
      "openPrice": 0,
      "pairName": "string",
      "volume": 0
    },
    "additionalProp3": {
      "closePrice": 0,
      "date": 0,
      "highPrice": 0,
      "id": "string",
      "lowPrice": 0,
      "openPrice": 0,
      "pairName": "string",
      "volume": 0
    }
  }
}
```

#
```
GET /pairs/{pairName}/history
```
**Params**

Name | Description
------------ | ------------
pairName * string (path) | pairName

**Response:**
```javascript
[
  {
    "bothOrdersIsBinance": true,
    "date": 0,
    "firstCommissionOnCurrencyOfOrder": true,
    "firstOrderId": "string",
    "firstUserCommission": 0,
    "firstUserId": "string",
    "id": "string",
    "pairName": "string",
    "price": 0,
    "quantity": 0,
    "secondCommissionOnCurrencyOfOrder": true,
    "secondOrderId": "string",
    "secondUserCommission": 0,
    "secondUserId": "string",
    "side": "BUY"
  }
]
```



#
```
GET /pairs/{pairName}/info
```
**Params**

Name | Description
------------ | ------------
pairName * string (path) | pairName

**Response:**
```javascript
{
  "currentPrice": 0,
  "dailyChange": 0,
  "dailyHigh": 0,
  "dailyLow": 0,
  "dailyVolume": 0,
  "prevDailyChange": 0,
  "prevDailyHigh": 0,
  "prevDailyLow": 0,
  "prevDailyVolume": 0,
  "statisticalDay": 0
}
```

#
```
GET /pairs/active-pairs
```

**Response:**
```javascript
[
  "string"
]
```

#
```
GET /pairs/favorites
```
**Response:**
```javascript
[
  "string"
]
```

#
```
POST /pairs/favorites/{pairName}
```
**Params**

Name | Description
------------ | ------------
pairName * string (path) | pairName

**Response:**
```javascript
[
  "string"
]
```


#
```
GET /pairs/names
```

**Response:**
```javascript
[
  {
    "pairName": "string"
  }
]
```

#
```
GET /pairs/user/preferred
```

**Response:**
```javascript
[
  {
    "pairName": "string"
  }
]
```
#
### Trades

```
GET /trades
```
**Params**

Name | Description
------------ | ------------
count integer($int32) (query) | count (Default value : 30)
pair * string (query) | pair

**Response:**
```javascript
[
  {
    "id": "string",
    "price": 0,
    "qty": 0,
    "time": 0
  }
]
```
#
### Users



```
GET /users/current
```

**Response:**
```javascript
{
  "accountNonExpired": true,
  "accountNonLocked": true,
  "authorities": [
    {
      "authority": "string"
    }
  ],
  "credentialsNonExpired": true,
  "enabled": true,
  "id": "string",
  "password": "string",
  "time": 0,
  "username": "string"
}
```


#

```
PUT /users/current/address
```
**Params**

Name | Description
------------ | ------------
apartmentNumber string (query) | -
city string (query) | -
country string (query) | -
house string (query) | -
id string (query) | -
permanentAddressMatchCurrentAddress boolean (query) | -
permanentApartmentNumber string (query) | -
permanentCity string (query) | -
permanentCountry string (query) | -
permanentHouse string (query) | -
permanentPostIndex string (query) | -
permanentRegion string (query) | -
permanentState string (query) | -
permanentStreet string (query) | -
postIndex string (query) | -
region string (query) | -
state string (query) | -
street string (query) | -
valid boolean (query) | -

**Response:**
```200 OK```
#

```
PUT /users/current/contacts
```
**Params**

Name | Description
------------ | ------------
citizenship string (query) | -
countryCode string (query) | -
dayOfBirth integer($int32) (query) | -
email string (query) | -
firstName string (query) | -
id string (query) | -
lastName string (query) | -
monthOfBirth string (query) | -
patronymicName string (query) | -
phoneNumber string (query) | -
regionCode string (query) | -
sex string (query) | -
yearOfBirth integer($int32) (query) | -

**Response:**
```200 OK```
#

```
GET /users/current/info
```

**Response:**
```javascript
{
  "addressId": "string",
  "contactsId": "string",
  "documentsId": [
    "string"
  ],
  "loginHistory": [
    {
      "browser": "string",
      "city": "string",
      "country": "string",
      "date": 0,
      "ip": "string",
      "os": "string"
    }
  ],
  "profitFactor": 0,
  "qrUrlFor2Fa": "string",
  "registrationDate": 0,
  "userId": "string",
  "withdrawConfirm": true
}
```

#

```
GET /users/current/pairs
```

**Response:**
```javascript
{
  "additionalProp1": [
    "string"
  ],
  "additionalProp2": [
    "string"
  ],
  "additionalProp3": [
    "string"
  ]
}
```
#

```
GET /users/current/settings
```
**Response:**
```javascript
{
  "commissionInCurrencyOfOrder": true,
  "displayPreferredPairs": [
    "string"
  ],
  "favoritePairs": [
    "string"
  ],
  "loginByIp": true,
  "onLoginNotification": true,
  "onOrderCancelNotification": true,
  "onOrderNotification": true,
  "onTradeNotification": true,
  "onWithdrawNotification": true,
  "secondAuthOnLogin": true,
  "secondAuthOnWithdraw": true,
  "secret": "string",
  "sendEmailOnLogin": true,
  "stayOnline": true,
  "whiteIPs": [
    {
      "browser": "string",
      "city": "string",
      "country": "string",
      "date": 0,
      "ip": "string",
      "os": "string"
    }
  ],
  "withdrawAddressesWhiteList": [
    "string"
  ],
  "withdrawByAddress": true
}
```
#

```
PATCH /users/current/settings/commissions
```
**Params**

Name | Description
------------ | ------------
enabled * boolean (query) | enabled

**Response:**
```200 OK```
#
```
POST /users/current/settings/pairs/preferred
```
**Params**

Name | Description
------------ | ------------
preferredPairs * array[string] (query) | preferredPairs

**Response:**
```200 OK```

#

```
GET /users/current/trades/history
```
**Params**

Name | Description
------------ | ------------
currency string (query) | currency
endDate integer($int64) (query)| endDate (Default value : 9223372036854776000)
offset integer($int64) (query) | -
pageNumber integer($int32) (query) | -
pageSize integer($int32) (query) | -
paged boolean (query) | -
priceFrom string (query) | priceFrom (Default value : 0.000000000000000000001)
priceTo string (query) | priceTo (Default value : 9223372036854775807)
quantityFrom string (query) | quantityFrom (Default value : 0.000000000000000000001)
quantityTo string (query) | quantityTo (Default value : 9223372036854775807)
side string (query) | side (Available values : BUY, SELL)
sort.sorted boolean (query) | -
sort.unsorted boolean (query) | -
startDate integer($int64) (query) | startDate (Default value : 1)
unpaged boolean (query) | -

**Response:**
```javascript
[
  {
    "bothOrdersIsBinance": true,
    "date": 0,
    "firstCommissionOnCurrencyOfOrder": true,
    "firstOrderId": "string",
    "firstUserCommission": 0,
    "firstUserId": "string",
    "id": "string",
    "pairName": "string",
    "price": 0,
    "quantity": 0,
    "secondCommissionOnCurrencyOfOrder": true,
    "secondOrderId": "string",
    "secondUserCommission": 0,
    "secondUserId": "string",
    "side": "BUY"
  }
]
```
#
### Wallets


```
GET /wallets
```

**Response:**
```javascript
[
  {
    "availableBalance": 0,
    "currency": "ETH",
    "id": 0,
    "totalBalance": 0,
    "userId": "string"
  }
]
```
#

```
PUT /wallets
```
**Required permission** ```WITHDRAW```

**Params**

Name | Description
------------ | ------------
withdrawRequest * (body) | withdrawRequest

*Example Value*
```javascript
{
  "address": "string",
  "amount": 0,
  "currency": "ETH",
  "qrPass": "string"
}
```
**Response:**
```javascript
{
  "availableBalance": 0,
  "currency": "ETH",
  "id": 0,
  "totalBalance": 0,
  "userId": "string"
}
```
#

```
GET /wallets/{currency}
```
**Params**

Name | Description
------------ | ------------
currency * string (path) | currency (Available values : ETH, BTC, USD, LTC, DASH, ZEC, BCH, ETC, BTG, ADA, EOS, E2C, XLM)

**Response:**
```javascript
{
  "currentRate": 0,
  "frozenActives": 0,
  "transactionFee": 0,
  "wallet": {
    "availableBalance": 0,
    "currency": "ETH",
    "id": 0,
    "totalBalance": 0,
    "userId": "string"
  }
}
```
#

```
GET /wallets/addresses/{currency}
```
**Params**

Name | Description
------------ | ------------
currency * string (path) | currency (Available values : ETH, BTC, USD, LTC, DASH, ZEC, BCH, ETC, BTG, ADA, EOS, E2C, XLM)

**Response:**
```javascript
{
  "id": "string"
}
```

#

```
GET /wallets/transactions/{transactionType}
```
**Params**

Name | Description
------------ | ------------
offset integer($int64) (query) | -
pageNumber integer($int32) (query) | -
pageSize integer($int32) (query) | -
paged boolean (query) | -
sort.sorted boolean (query) | -
sort.unsorted boolean (query) | -
transactionType * string (path) | transactionType (Available values : DEPOSIT, WITHDRAW)
unpaged boolean (query) | -

**Response:**
```javascript
{
  "content": [
    {
      "amount": 0,
      "currency": "ETH",
      "id": "string",
      "status": "SEND",
      "time": 0,
      "type": "DEPOSIT"
    }
  ],
  "empty": true,
  "first": true,
  "last": true,
  "number": 0,
  "numberOfElements": 0,
  "pageable": {
    "offset": 0,
    "pageNumber": 0,
    "pageSize": 0,
    "paged": true,
    "sort": {
      "empty": true,
      "sorted": true,
      "unsorted": true
    },
    "unpaged": true
  },
  "size": 0,
  "sort": {
    "empty": true,
    "sorted": true,
    "unsorted": true
  },
  "totalElements": 0,
  "totalPages": 0
}
```
