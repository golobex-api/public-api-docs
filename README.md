# Public REST API for Golobex
# General API Information
* The base endpoint is: **https://golobex.com/api/v1/**
* All endpoints can return a JSON object, array, or void (just ```200 OK```).
* All time and timestamp related fields are in milliseconds.
* HTTP `4XX` return codes are used for for malformed requests; the issue is on the sender's side.
* HTTP `5XX` return codes are used for internal errors; the issue is on server's side.
  It is important to **NOT** treat this as a failure operation; the execution status is **UNKNOWN** and could have been a success.
* We are using `GET`, `POST`, `PUT`, `PATCH` and `DELETE` methods.
* Some parametes must be sent as a `query string`, `request body` and/or `path variable`.
* The content type is `application/json`.

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
TRADE | Endpoint requires sending a valid API-Key and signature.
WITHDRAW | Endpoint requires sending a valid API-Key and signature.

# SIGNED (TRADE and WITHDRAW) Endpoint security
* `SIGNED` endpoints require an additional parameter, `signature`, to be sent in the  `query string`.
* Endpoints use `HMAC SHA256` signatures. The `HMAC SHA256 signature` is a keyed `HMAC SHA256` operation.
  Use your `secretKey` as the key and `totalParams` as the value for the HMAC operation.
* The `signature` is **case sensitive**.
* `totalParams` is defined as the `query string` concatenated with the `request body`.

## ENUM definitions
**Order side (side):**

* BUY
* SELL

**Currency:**
* E2C
* ETH
* ADA
* BTC
* LTC
* DASH
* ZEC
* BCH

**Pair name (pairName, pair):**
* E2C/ETH
* ADA/ETH
* DASH/ETH
* LTC/ETH
* ZEC/ETH
* E2C/BTC
* ADA/BTC
* BCH/BTC
* DASH/BTC
* ETH/BTC
* LTC/BTC
* ZEC/BTC

## SIGNED Endpoint Example for POST /api/v1/orders/market
Here is a step-by-step example of how to send a vaild signed payload from the
Linux command line using `echo`, `openssl`, and `curl`.

Key | Value
------------ | ------------
publicKey | mWPCL7kPoa5njUAUIQbtznVnRqyn4wZ5nYv2TTMdQMk5IYF61QjdoHO8MrSZKiOT
secretKey | IN0PR6nP6qGlUgySohQk73F7yH7jrotoyFADvOb6SNx5uqwpmbVMzUPT4boF2UOU


Parameter | Value
------------ | ------------
amount | 1
market | true
pairName | LTC/BTC
side | BUY
price | 0.1

* **queryString:** `signature=c6ab8e302471ce37fab6ed2e6c3bc8935dbbf1ab3629326d2359ec000d0bfa1d`
* **requestBody:** `{"amount":1,"pairName":"LTC/BTC","price":0.1,"side":"BUY"}`
* **signedString:** `amount=1&pairName=LTC/BTC&price=0.1&side=BUY`

  `NOTE: key-value pairs naturally ordered by keys: amount=1&pairName=LTC/BTC&price=0.1&side=BUY`

  `Please consider using naturally ordered keys or else you'll receive wrong singnature error`

* **HMAC SHA256 signature:**

    ```
    [linux]$ echo -n "amount=1&pairName=LTC/BTC&price=0.1&side=BUY" | openssl dgst -sha256 -hmac "IN0PR6nP6qGlUgySohQk73F7yH7jrotoyFADvOb6SNx5uqwpmbVMzUPT4boF2UOU"
    (stdin)= c6ab8e302471ce37fab6ed2e6c3bc8935dbbf1ab3629326d2359ec000d0bfa1d
    ```

* **curl command:**

    ```
    (HMAC SHA256)
    [linux]$ curl -H "X-CX-APIKEY: mWPCL7kPoa5njUAUIQbtznVnRqyn4wZ5nYv2TTMdQMk5IYF61QjdoHO8MrSZKiOT" -H "Content-Type: application/json" -X POST 'https://golobex.com/api/v1/orders/market?signature=c6ab8e302471ce37fab6ed2e6c3bc8935dbbf1ab3629326d2359ec000d0bfa1d' -d '{"amount":1,"pairName":"LTC/BTC","price":0.1,"side":"BUY"}'
    ```

if you received this:
```JSON
{
  "url":"https://golobex.com/api/v1/orders/market",
  "cause":"InsufficientFundsException",
  "detail":"Not enough money for execute market order"
}
```

it means everything is ready to deposit some real money!

# General endpoints

### Orders
```
POST /orders
```
`SIGNED`

**Required permission:** ```TRADING```

**Params**

Name | Description
------------ | ------------
order * (body) | order

*Example Value*
```JSON
{
  "amount": 0,
  "distance": 0,
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
**Required permission:** ```TRADING```

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
```JSON
[
  {
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
`SIGNED`

**Required permission:** ```TRADING```

**Params**

Name | Description
------------ | ------------
marketOrder * (body) | marketOrder

*Example Value*
```JSON
{
  "amount": 0,
  "pairName": "string",
  "price": 0,
  "side": "BUY"
}
```
**Response:**
```200 OK```

#
```
POST /orders/sltp
```
`SIGNED`

**Required permission:** ```TRADING```

**Params**

Name | Description
------------ | ------------
sltpOrder * (body) | sltpOrder

*Example Value*
```JSON
{
  "amount": 0,
  "pairName": "string",
  "side": "BUY",
  "slPrice": 0,
  "tpPrice": 0
}
```
**Response:**
```200 OK```



#
```
POST /orders/trailing
```
`SIGNED`

**Required permission:** ```TRADING```

**Params**

Name | Description
------------ | ------------
trailingOrder * (body) | trailingOrder

*Example Value*
```JSON
{
  "amount": 0,
  "distance": 0,
  "pairName": "string",
  "side": "BUY"
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
```JSON
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
    "currencyLast": "BTC",
    "currentPrice": 0,
    "enabled": true,
    "firstCurrencyCommission": 0,
    "id": "string",
    "lastCurrencyCommission": 0,
    "minPrice": 0,
    "minQuantity": 0,
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
```JSON
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
```JSON
[
  {
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
```JSON
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
```JSON
[
  "string"
]
```

#
```
GET /pairs/favorites
```
**Response:**
```JSON
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
```JSON
[
  "string"
]
```


#
```
GET /pairs/names
```

**Response:**
```JSON
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
```JSON
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
```JSON
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
```JSON
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
GET /users/current/info
```

**Response:**
```JSON
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
```JSON
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
```JSON
[
  {
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
```JSON
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
`SIGNED`

**Required permission:** ```WITHDRAW```

**Params**

Name | Description
------------ | ------------
withdrawRequest * (body) | withdrawRequest

*Example Value*
```JSON
{
  "address": "string",
  "amount": 0,
  "currency": "ETH",
  "qrPass": "string"
}
```
**Response:**
```JSON
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
```JSON
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
```JSON
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
```JSON
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
