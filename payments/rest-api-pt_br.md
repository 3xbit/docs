# 3xPay Rest API


## Informações Gerais da API
* Endpoint base: https://api.pay.3xbit.com.br
* Fluxograma: [fluxograma.jpg](https://github.com/3xbit/docs/blob/master/payments/fluxograma.jpg)
* Todos os endpoints retornam um objeto JSON ou um Array.
* Para endpoints `GET`, os parâmetros devem ser enviados por `query string`.
* Para endpoints `POST`, os parâmetros devem ser enviados por `data` ou no corpo da requisição com `application/x-www-form-urlencoded` no `content-type`.


## Autenticação

A autenticação deve ser feita por Token.

```
POST /token/
```
#### Parâmetros:
|  Parâmetro  | Tipo | Obrigatório |  Exemplo  |
|:------------|:-----|:------------|:----------|
|client_id    |STRING|     SIM     |XKSCaD0iGo5cMXHKkuGVpwJnM3UOH5KnzxiEK71z|
|client_secret|STRING|     SIM     |XDLxXVQCDNkJ9bJZumi0P35c33mucC1XpDrIQp9BHci6JhVL6PKBgoMDW0pP3gkXeZuFXUMmHrRWZXDTMX8oGMmU8ktL0X41aPdXDFP0pP9KK2vfmJ1HVjXYX4vdnJHz|


#### Response:
```
{
  "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTU1MTY0Nzg4MiwianRpIjoiMGNhZjY5YjEzMDExNGFmZmJkODZkZjBmNzNiODkzMTQiLCJ1c2VyX2lkIjoyfQ.Q-dU08zmwLBitIHN6KbLJAWmQ1P4Fb7Pcj1jgonYBTg",
  "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTUxNjQ3ODgyLCJqdGkiOiJkZTIxM2I3MmVhYTI0ZmU3ODZjYjliMzgwNDQxYjU1OCIsInVzZXJfaWQiOjJ9.XBRWzNHtrDA2DA2EjK7Kfp3wFDvM6a_z7bm_aYo3Km8",
}
```

O Token expira a cada 5 dias e pode ser renovado da seguinte forma:

```
POST /token/refresh/
```

#### Parâmetros:
|  Parâmetro  | Tipo | Obrigatório |  Exemplo  |
|:------------|:-----|:------------|:----------|
|refresh    |STRING|     SIM     |eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTU1MTY0Nzg4MiwianRpIjoiMGNhZjY5YjEzMDExNGFmZmJkODZkZjBmNzNiODkzMTQiLCJ1c2VyX2lkIjoyfQ.Q-dU08zmwLBitIHN6KbLJAWmQ1P4Fb7Pcj1jgonYBTg|


## Headers
Deve utilizar esta Headers para todos os endpoints:

```
headers = { "Authorization": "Bearer {access}" }
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

# Cliente
### Retornar ID do Cliente
```
POST /v1/client/
```
#### Parâmetros:
|  Parâmetro    | Tipo   | Obrigatório |
|:--------------|:-------|:------------|
|   full_name   |STRING  |  Sim        |
|   email   |STRING  |  Sim        |

#### Response:
```
{  
   "cleint_id":"xsasdas",
   "first_name":"Cliente",
   "last_name":"Teste",
   "email":"client.test@mailinator.com",
}
```

### Retornar Carteira do Cliente
```
POST /v1/client/{client_id}/wallet/{currency}/
```
#### Parâmetros:
|  Parâmetro    | Tipo   | Obrigatório |
|:--------------|:-------|:------------|
|   full_name   |STRING  |  Sim        |
|   email   |STRING  |  Sim        |

#### Response:
{  
   "address":"Btki8R4uD2bUvQmCv2BG2pETospt2LxBTK",
   "currency":"BTC"
}

## Depósitos
### Listar Depósitos do Cliente
```
GET /v1/client/{client_id}/deposit/btc/
```


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
GET /v1/client/{client_id}/deposit/btc/69ce21f92d346b58092a2c942a4533becd4f81ed923c3e31b6ee1509e980828c/
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



