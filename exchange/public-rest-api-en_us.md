# Public Rest API - 3xBit


## General API Information
* The base endpoint is: https://api.exchange.3xbit.com.br
* All endpoints return either a JSON object or array.
* For `GET` endpoints, parameters must be sent as a `query string`.
* For `POST` endpoints, parameters must be sent as a `data`.
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
         "quantity":"0.03937500",
         "total":"130.15209375"
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
|  Parameter    | Type   | Required | Descrição  | Default |
|:--------------|:-------|:------------|:---------|:-----------|
| currency_rate | STRING | NO         | Dollar value converted by the reported currency | BRL |
| page | STRING | NO         |  |  |


#### Response:
```
{  
   "exchange_rate":3.923799,
   "market":"CREDITBTC",
   "history":{  
      "page":"2",
      "previous":"https://api.exchange.3xbit.com.b/v1/history/credit/btc/?page=1",
      "next":"https://api.exchange.3xbit.com.b/v1/history/credit/btc/?page=3",
      "results":[  
         {  
            "order_type":"SELL",
            "unit_price":"6448.80000000",
            "quantity":"0.00059300",
            "timestamp":1542039174.423063
         },
         {  
            "order_type":"SELL",
            "unit_price":"6448.80000000",
            "quantity":"0.00518600",
            "timestamp":1542039170.309675
         },
         {  
            "order_type":"BUY",
            "unit_price":"6448.10000000",
            "quantity":"0.00553900",
            "timestamp":1542038992.761097
         },
         ...
      ]
   }
}
```
