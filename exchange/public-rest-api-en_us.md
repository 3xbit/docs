# Public Rest API - 3xBit


## General API Information
* The base endpoint is: https://api.exchange.3xbit.com.br
* All endpoints return either a JSON object or array.
* For `GET` endpoints, parameters must be sent as a `query string`.
* For `POST` endpoints, parameters must be sent as a `data` or in the request body with `application/x-www-form-urlencoded` in the `content-type`.
* All time and timestamp related fields are in milliseconds.



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
