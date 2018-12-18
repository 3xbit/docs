# Public Rest API - 3xBit


## Informações Gerais da API
* Endpoint base: https://api.exchange.3xbit.com.br
* Todos os endpoints retornam um objeto JSON ou um Array.
* Para endpoints `GET`, os parâmetros devem ser enviados por `query string`.
* Para endpoints `POST`, os parâmetros devem ser enviados por `data` ou no corpo da requisição com `application/x-www-form-urlencoded` no `content-type`.
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


### Listar Histórico do Mercado

```
GET /v1/history/credit/btc/
```
#### Parâmetros:
|  Parâmetro    | Tipo   | Obrigatório | Description  | Padrão |
|:--------------|:-------|:------------|:---------|:-----------|
| currency_rate | STRING | NÃO         | Valor do dólar convertido pela moeda informada | BRL |
| page | STRING | NÃO         |  |  |
| since | TIMESTAMP | NÃO         | Data início |  |
| until | TIMESTAMP | NÃO         | Data fim |  |


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
