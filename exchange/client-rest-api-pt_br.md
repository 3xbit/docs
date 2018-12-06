# Client Rest API - 3xBit


## Informações Gerais da API
* Endpoint base: https://api.exchange.3xbit.com.br
* Todos os endpoints retornam um objeto JSON ou um Array.
* Para endpoints `GET`, os parâmetros devem ser enviados por `query string`.
* Para endpoints `POST`, os parâmetros devem ser enviados por `data`.

## Autenticação

A autenticação deve ser feita por Chaves de API.
* Você pode criar suas Chaves de API nas configurações da sua Conta em nossa plataforma: [https://app.3xbit.com.br/profile/](https://app.3xbit.com.br/profile/)

```
GET /api/oauth/token/
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
   },
]
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
   "date_joined": "2018-12-05T15:42:11.362810-02:00",
   "last_update": "2018-12-05T15:42:11.363464-02:00",
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
      "date_joined": "2018-12-05T16:38:18.244112-02:00",
      "last_update": "2018-12-05T16:38:18.244387-02:00",
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
      "date_joined":" 2018-12-04T12:09:27.949954-02:00",
      "last_update": "2018-12-04T12:09:30.506978-02:00",
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
   "date_joined": "2018-12-05T15:42:11.362810-02:00",
   "last_update": "2018-12-05T15:42:11.363464-02:00",
}
```

### Cancelar uma Ordem pelo ID

```
DELETE /v1/order/MDNMu9W56A/
```
