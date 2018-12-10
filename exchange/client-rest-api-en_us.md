# Client Rest API - 3xBit


## General API Information
* The base endpoint is: https://api.exchange.3xbit.com.br
* All endpoints return either a JSON object or array.
* For `GET` endpoints, parameters must be sent as a `query string`.
* For `POST` endpoints, parameters must be sent as a `data`.
* All time and timestamp related fields are in milliseconds.

## Authentication

Authentication must be performed by API Keys.
* You can create your API Keys in your Account settings on our platform: [https://app.3xbit.com.br/profile/](https://app.3xbit.com.br/profile/)

```
GET /api/oauth/token/
```
#### Parameters:
|  Parameter  | Type | Required |  Exemple  |
|:------------|:-----|:---------|:----------|
|grant_type   |STRING|     YES  |client_credentials|
|client_id    |STRING|     YES  |XKSCaD0iGo5cMXHKkuGVpwJnM3UOH5KnzxiEK71z|
|client_secret|STRING|     YES  |XDLxXVQCDNkJ9bJZumi0P35c33mucC1XpDrIQp9BHci6JhVL6PKBgoMDW0pP3gkXeZuFXUMmHrRWZXDTMX8oGMmU8ktL0X41aPdXDFP0pP9KK2vfmJ1HVjXYX4vdnJHz|


#### Response:
```
{
  "access_token": "WRNAZedyx8yjocwJIpg9LJUvvBDECO",
  "expires_in": 900,
  "token_type": "Bearer",
  "scope": "account:read account:write history:read order:read order:write wallet:read wallet:write withdraw:write balance:read wallet:write wallet:read deposit:read deposit:write",
  "message": "USER_SUCCESSFULLY_LOGGED",
}
```

## Headers

You should use this Headers for all endpoints:

```
headers = { "Authorization": "Bearer {access_token}" }
```


## Balance
### List the Balance of all Currencies:

```
GET /v1/balance/
```

#### Response:
```
[
   {
      "currency": {
         "name": "",
         "code": "CREDIT",
         "type": "CRYPTO",
         "ranking": 0,
      },
      "available_balance": "70.719406865",
      "total_balance": "70.719406865",
      "blocked_balance": "0.000000000",
      "pending_balance": "0.000000000",
   },
   {
      "currency": {
         "name": "Bitcoin",
         "code": "BTC",
         "type": "CRYPTO",
         "ranking": 1,
      },
      "available_balance: "0.025002560",
      "total_balance": "0.025002560",
      "blocked_balance": "0.000000000",
      "pending_balance": "0.000000000",
   },
]

```
### List the Balance of a specific Currency:

```
GET /v1/balance/btc/
```

#### Response:
```
[
   {
      "currency": {
         "name": "Bitcoin",
         "code": "BTC",
         "type": "CRYPTO",
         "ranking": 1,
      },
      "available_balance: "0.025002560",
      "total_balance": "0.025002560",
      "blocked_balance": "0.000000000",
      "pending_balance": "0.000000000",
   },
]
```

## OrderBook
### Create Orders

```
POST /v1/order/credit/btc/buy/
```
#### Parameters:
|  Parameter    | Type   | Required | Exemple        |
|:--------------|:-------|:---------|:---------------|
|execution_type |STRING  |YES       | LIMIT          |
|unit_price     |DECIMAL |YES       | 6442.25        |
|quantity       |DECIMAL |YES       | 0.005000       |

#### Execution Types:
* LIMIT
* MARKET


#### Response:
```
{
   "market": "CREDITBTC",
   "order_id": "MDNMu9W56A",
   "order_type": "BUY",
   "execution_type": "LIMIT",
   "unit_price": "6442.25",
   "quantity": "0.005000",
   "total": "32.21125000",
   "executed_qty": 0.0,
   "status": "PENDING",
   "timestamp": "1544031731.36281",
   "last_update": "1544038248.986652",
}
```

### List Orders

```
GET /v1/order/credit/btc/sell/
```
#### Parameters:
|  Parameter | Type   | Required | Exemple   |
|:-----------|:-------|:---------|:----------|
|   filter   | STRING | NO       | OPEN      |

#### Filters:
* OPEN
* DONE
* 24H


#### Response:
```
[
   {
      "market": "CREDITBTC",
      "order_id": "lAJGUy696D",
      "order_type": "SELL",
      "execution_type": "LIMIT",
      "unit_price": "6472.24",
      "quantity": "0.005000",
      "total": "32.36120000",
      "executed_qty": 0.0,
      "status": "PENDING",
      "timestamp": "1544035098.244112",
      "last_update": "1544035098.270642",
   },
   {
      "market": "CREDITBTC",
      "order_id": "QD8XU64E1D",
      "order_type": "SELL",
      "execution_type": "LIMIT",
      "unit_price": "6480.25",
      "quantity": "0.003456",
      "total": "22.39574400",
      "executed_qty": 0.0,
      "status": "CANCELED",
      "timestamp":" 1543932567.949954",
      "last_update": "1543944369.218648",
   },
]
```

### List Order by ID

```
GET /v1/order/MDNMu9W56A/
```

#### Response:
```
{
   "market": "CREDITBTC",
   "order_id": "MDNMu9W56A",
   "order_type": "BUY",
   "execution_type": "LIMIT",
   "unit_price": "6442.25",
   "quantity": "0.005000",
   "total": "32.21125000",
   "executed_qty": 0.0,
   "status": "PENDING",
   "timestamp": "1544031731.36281",
   "last_update": "1544038248.986652",
}
```

### Cancel Order by ID

```
DELETE /v1/order/MDNMu9W56A/
```
