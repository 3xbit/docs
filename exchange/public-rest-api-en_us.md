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
         "quantity":"0.00539800",
         "total":"17.65507666"
      },
      ...
   ],
   "sell_orders":[  
      {  
         "unit_price":"3518.00000000",
         "quantity":"0.24949100",
         "total":"877.70933800"
      },
      {  
         "unit_price":"3519.00000000",
         "quantity":"0.12000000",
         "total":"422.28000000"
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
   "next":"https://api.exchange.3xbit.com.br/v1/history/credit/btc/?page=2",
   "previous":null,
   "results":[  
      {  
         "order_type":"SELL",
         "unit_price":"3430.00000000",
         "quantity":"0.02335600",
         "market":"CREDITBTC",
         "total":"80.11108000",
         "exchange_rate":3.923799,
         "timestamp":1544471293.029134
      },
      {  
         "order_type":"SELL",
         "unit_price":"3434.00000000",
         "quantity":"0.08715200",
         "market":"CREDITBTC",
         "total":"299.27996800",
         "exchange_rate":3.923799,
         "timestamp":1544471278.390874
      },
      {  
         "order_type":"BUY",
         "unit_price":"3520.00000000",
         "quantity":"0.00624400",
         "market":"CREDITBTC",
         "total":"21.97888000",
         "exchange_rate":3.923799,
         "timestamp":1544457466.117738
      },
      ...
   ]
}
```
