# Public Rest API - 3xBit


## General API Information
* The base endpoint is: https://api.exchange.3xbit.com.br
* All endpoints return either a JSON object or array.
* For `GET` endpoints, parameters must be sent as a `query string`.
* For `POST` endpoints, parameters must be sent as a `data` or in the request body with `application/x-www-form-urlencoded` in the `content-type`.
* All time and timestamp related fields are in milliseconds.
* HTTP `429` return code is used when breaking the request rate limit `1/3 seconds`.


## Ticker

### List Ticker

```
GET /ticker/
```

#### Response:
```
{  
   "CREDIT_BTC":{  
      "market":"CREDIT",
      "symbol":"BTC",
      "last":"4162.120000000",
      "open":"3860.000000000",
      "close":"4162.120000000",
      "max":"4162.200000000",
      "min":"3716.080000000",
      "variation":7.826943005181347,
      "volume":45.214483,
      "exchange_rate":"3.848399",
      "dollar_brl":"3.848399",
      "bid":"3951.220000000",
      "ask":"4162.120000000",
      "market_name":"CREDIT"
   },
   "CREDIT_ETH":{  
      "market":"CREDIT",
      "symbol":"ETH",
      "last":"107.700000000",
      "open":"104.000000000",
      "close":"107.700000000",
      "max":"107.700000000",
      "min":"103.200000000",
      "variation":3.5576923076923075,
      "volume":11.054616,
      "exchange_rate":"3.848399",
      "dollar_brl":"3.848399",
      "bid":"105.700000000",
      "ask":"121.000000000",
      "market_name":"CREDIT"
   },
   ...
}
```

### List Ticker converted by currency
```
GET /ticker/brl/
```

#### Example of currencies available:
* BRL
* USD
* EUR



#### Response:
```
{  
   "CREDIT_BTC":{  
      "market":"CREDIT",
      "symbol":"BTC",
      "last":"16001.68",
      "open":"14840.54",
      "close":"16001.68",
      "max":"16001.99",
      "min":"14286.84",
      "variation":7.824149633429186,
      "volume":45.213126,
      "exchange_rate":"3.844599",
      "dollar_brl":"3.844599",
      "bid":"15341.56",
      "ask":"16001.68",
      "market_name":"CREDIT"
   },
   "CREDIT_ETH":{  
      "market":"CREDIT",
      "symbol":"ETH",
      "last":"414.06",
      "open":"399.84",
      "close":"414.06",
      "max":"414.06",
      "min":"396.76",
      "variation":3.5576923076923075,
      "volume":11.054616,
      "exchange_rate":"3.844599",
      "dollar_brl":"3.844599",
      "bid":"406.37",
      "ask":"465.20",
      "market_name":"CREDIT"
   },
   ...
}

```


## OrderBook

### List OrderBook

```
GET /v1/orderbook/credit/btc/
```
#### Parameters:
|  Parameter    | Type   | Required | Description  | Default |
|:--------------|:-------|:------------|:---------|:-----------|
| currency_rate | STRING | NO         | Dollar value converted by the reported currency | BRL |


#### Response:
```
{  
   "exchange_rate":"3.923799",
   "market":"CREDITBTC",
   "buy_orders":[  
      {  
         "unit_price":"3305.45000000",
         "quantity":"0.03937500"
      },
      {  
         "unit_price":"3270.67000000",
         "quantity":"0.00539800"
      },
      ...
   ],
   "sell_orders":[  
      {  
         "unit_price":"3518.00000000",
         "quantity":"0.24949100"
      },
      {  
         "unit_price":"3519.00000000",
         "quantity":"0.12000000"
      },
      ...
   ]
}
```


### List Market History

```
GET /v1/history/credit/btc/
```
#### Parameters:
|  Parameter    | Type   | Required | Description  | Default |
|:--------------|:-------|:------------|:---------|:-----------|
| currency_rate | STRING | NO         | Dollar value converted by the reported currency | BRL |
| page | STRING | NO         |  |  |
| since | TIMESTAMP | NO         | Initial Date |  |
| until | TIMESTAMP | NO         | End Date |  |


#### Response:
```
{  
   "exchange_rate":3.923799,
   "market":"CREDITBTC",
   "history":{  
      "page":"2",
      "previous":"https://api.exchange.3xbit.com.br/v1/history/credit/btc/?page=1",
      "next":"https://api.exchange.3xbit.com.br/v1/history/credit/btc/?page=3",
      "results":[  
         {  
            "order_type":"BUY",
            "unit_price":"6529.90000000",
            "quantity":"0.79152800",
            "timestamp":1543338577.928904,
            "transaction_id":"oQD4NfpnKLB"
         },
         {  
            "order_type":"SELL",
            "unit_price":"6529.70000000",
            "quantity":"0.00382300",
            "timestamp":1543338541.962527,
            "transaction_id":"N0Da0fN2pOj"
         },
         {  
            "order_type":"SELL",
            "unit_price":"6529.70000000",
            "quantity":"0.00513500",
            "timestamp":1543338541.783392,
            "transaction_id":"Q1DJzfYjwDR"
         },
         ...
      ]
   }
}
```
