# Client Rest API - 3xBit


## Informações Gerais da API
* Endpoint base: https://api.exchange.3xbit.com.br
* Todos os endpoints retornam um objeto JSON ou um Array.
* Para endpoints `GET`, os parâmetros devem ser enviados por `query string`.
* Para endpoints `POST`, os parâmetros devem ser enviados por `data` ou no corpo da requisição com `application/x-www-form-urlencoded` no `content-type`.
* Todos os campos relacionados a data e hora estão em milissegundos.
* O código de retorno HTTP `429` é usado ao quebrar o limite da taxa de request `1/second`.


## Autenticação

A autenticação deve ser feita por Chaves de API.
* Você pode criar suas Chaves de API nas configurações da sua Conta em nossa plataforma: [https://app.3xbit.com.br/profile/](https://app.3xbit.com.br/profile/)

```
POST /api/oauth/token/
```
#### Parâmetros:
|  Parâmetro  | Tipo | Obrigatório |  Exemplo  |
|:------------|:-----|:------------|:----------|
|grant_type   |STRING|     SIM     |client_credentials|
|client_id    |STRING|     SIM     |XKSCaD0iGo5cMXHKkuGVpwJnM3UOH5KnzxiEK71z|
|client_secret|STRING|     SIM     |XDLxXVQCDNkJ9bJZumi0P35c33mucC1XpDrIQp9BHci6JhVL6PKBgoMDW0pP3gkXeZuFXUMmHrRWZXDTMX8oGMmU8ktL0X41aPdXDFP0pP9KK2vfmJ1HVjXYX4vdnJHz|


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

Deve utilizar esta Headers para todos os endpoints:

```
headers = { "Authorization": "Bearer {access_token}" }
```


## Saldo
### Listar o Saldo de todas as Moedas:

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
   ...
]

```
### Listar o Saldo de uma moeda específica:

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
   }
]
```

## Depósitos
### Listar Depósitos
```
GET /v1/deposit/btc/
```
#### Parâmetros:
|  Parâmetro    | Tipo   | Obrigatório |
|:--------------|:-------|:------------|
|      status   |STRING  |  Não        |

#### Status:
* DONE
* PENDING
* CANCELED

#### Response:
```
[  
   {  
      "symbol":"BTC",
      "hash":"cde9c350f95e3721e05ddeea8824001e60b518094cdc6c1ccdf15896cee4c734",
      "address":"12DcfknE2JXjW9twBrv6jdk1gYpVJWkPpB",
      "amount":"0.01000000",
      "fees":0.0,
      "total":0.01,
      "status":"DONE",
      "timestamp":1532480672.0,
      "available_at":1532480672.0
   },
   {  
      "symbol":"BTC",
      "hash":"69ce21f92d346b58092a2c942a4533becd4f81ed923c3e31b6ee1509e980828c",
      "address":"12DcfknE2JXjW9twBrv6jdk1gYpVJWkPpB",
      "amount":"0.03291844",
      "fees":0.0,
      "total":0.03291844,
      "status":"DONE",
      "timestamp":1527271812.402,
      "available_at":1527272141.0
   },
   ...
]
```

### Listar Depósito pela Hash
```
GET /v1/deposit/btc/69ce21f92d346b58092a2c942a4533becd4f81ed923c3e31b6ee1509e980828c/
```

#### Response:
```
{  
   "symbol":"BTC",
   "hash":"69ce21f92d346b58092a2c942a4533becd4f81ed923c3e31b6ee1509e980828c",
   "address":"12DcfknE2JXjW9twBrv6jdk1gYpVJWkPpB",
   "amount":"0.03291844",
   "fees":0.0,
   "total":0.03291844,
   "status":"DONE",
   "timestamp":1527271812.402,
   "available_at":1527272141.0
}
```

## Retiradas
### Listar Retiradas
```
GET /v1/withdraw/btc/
```
#### Parâmetros:
|  Parâmetro    | Tipo   | Obrigatório |
|:--------------|:-------|:------------|
|      status   |STRING  |  Não        |

#### Status:
* DONE
* PENDING
* CANCELED

#### Response:
```
[  
   {  
      "symbol":"BTC",
      "hash":"63d28c232dff740bfc617d445e70dff93751c76dfa42d11bd27d8399ba2e4a56",
      "address":"1Ng9kdMPdLsfwKNHBcAq5hqCtUKm6DMLrt",
      "amount":"0.10040000",
      "fees":0.0004,
      "total":0.1,
      "status":"DONE",
      "timestamp":1544819138.314,
      "available_at":1544820335.0
   },
   {  
      "symbol":"BTC",
      "hash":"76cf32f8f358396366963df0cc84472669c3ad3e97406c29e0678a2bada273bb",
      "address":"16R2WxkqKmwJmqXqXo6wWFFTvnTNc1ACBa",
      "amount":"0.02261221",
      "fees":0.0005,
      "total":0.02211221,
      "status":"DONE",
      "timestamp":1535213242.986,
      "available_at":1535214086.0
   },
   ...
]
```

### Listar Retirada pela Hash
```
GET /v1/withdraw/btc/76cf32f8f358396366963df0cc84472669c3ad3e97406c29e0678a2bada273bb/
```

#### Response:
```
{  
   "symbol":"BTC",
   "hash":"76cf32f8f358396366963df0cc84472669c3ad3e97406c29e0678a2bada273bb",
   "address":"16R2WxkqKmwJmqXqXo6wWFFTvnTNc1ACBa",
   "amount":"0.02261221",
   "fees":0.0005,
   "total":0.02211221,
   "status":"DONE",
   "timestamp":1535213242.986,
   "available_at":1535214086.0
}
```



## Livro de Ofertas
### Criar Ordem

```
POST /v1/order/credit/btc/buy/
```
#### Parâmetros:
|  Parâmetro    | Tipo   | Obrigatório | Exemplo        |
|:--------------|:-------|:------------|:---------------|
|execution_type |STRING  |SIM          | LIMIT          |
|unit_price     |DECIMAL |SIM          | 6442.25        |
|quantity       |DECIMAL |SIM          | 0.005000       |

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

### Listar Ordens

```
GET /v1/order/credit/btc/sell/
```
#### Parâmetros:
|  Parâmetro | Tipo   | Obrigatório | Exemplo   |
|:-----------|:-------|:------------|:----------|
|   filter   | STRING | NÃO         | OPEN      |

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

### Listar uma Ordem pelo ID

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

### Cancelar uma Ordem pelo ID

```
DELETE /v1/order/MDNMu9W56A/
```
