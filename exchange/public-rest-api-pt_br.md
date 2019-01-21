# Public Rest API - 3xBit


## Informações Gerais da API
* Endpoint base: https://api.exchange.3xbit.com.br
* Todos os endpoints retornam um objeto JSON ou um Array.
* Para endpoints `GET`, os parâmetros devem ser enviados por `query string`.
* Para endpoints `POST`, os parâmetros devem ser enviados por `data` ou no corpo da requisição com `application/x-www-form-urlencoded` no `content-type`.
* Todos os campos relacionados a data e hora estão em milissegundos.
* O código de retorno HTTP `429` é usado ao quebrar o limite da taxa de request `1/second`.


## Ticker

### Listar Ticker

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

### Listar Ticker convertido pela moeda informada
```
GET /ticker/brl/
```

#### Exemplo de moedas disponíveis:
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
