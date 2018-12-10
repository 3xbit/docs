# Public Rest API - 3xBit


## Informações Gerais da API
* Endpoint base: https://api.exchange.3xbit.com.br
* Todos os endpoints retornam um objeto JSON ou um Array.
* Para endpoints `GET`, os parâmetros devem ser enviados por `query string`.
* Para endpoints `POST`, os parâmetros devem ser enviados por `data`.
* Todos os campos relacionados a data e hora estão em milissegundos.



## Livro de Ofertas

### Listar Livro de Ofertas

```
GET /v1/orderbook/credit/btc/
```
#### Parâmetros:
|  Parâmetro    | Tipo   | Obrigatório | Description  | Padrão |
|:--------------|:-------|:------------|:---------|:-----------|
| currency_rate | STRING | NÃO         | Valor do dólar convertido pela moeda informada | BRL |


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


### Listar Histórico do Mercado

```
GET /v1/history/credit/btc/
```
#### Parâmetros:
|  Parâmetro    | Tipo   | Obrigatório | Description  | Padrão |
|:--------------|:-------|:------------|:---------|:-----------|
| currency_rate | STRING | NÃO         | Valor do dólar convertido pela moeda informada | BRL |


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
