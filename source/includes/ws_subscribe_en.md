# Interface Subscription/Cancellation of Interface Subscription


## Subscription of Market Trend

>Request:

```json
{
    "method":"kline.subscribe", 
    "params":[ "BTCBCC", 60 ], 
    "id":100
}
```
>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```



- method: kline.subscribe
- params: 

Request Parameter：

| Name of Parameter   | Parameter Type | Required | Description        |
| -------- | -------- | ---- | ------------ |
| market   | String   | Yes   | Market Name       |
| interval | Integer  | Yes   | Period of Data Retrieval |


After the subscription is finished successfully, the subscribed data will be pushed to client end. Please refer to **[Market Trend Push]** for the content of data.

## Market Trend Push

>Request:

```json
{
    "method": "kline.update", 
    "params": [[1513135140, "8000", "8000", "8000", "8000", "0", "0", "BTCBCC"]], 
    "id": null
}
```


Request Parameter：
"params": [ 
    [ 
      1492358400,  # Timestamp
      "7000.00",   # Opening Price
      "8000.0",    # Closing Price
      "8100.00",   # Highest Price
      "6800.00",   # Lowest Price
      "1000.00"    # Settled Volume
      "123456.00", # Settled Value
      "BTCBCC"     # Market name of transaction pair traded
    ]
]



## Cancellation of Subscription on Market Trend

>Request:

```json
{
    "method":"kline.unsubscribe", 
    "params":[], 
    "id":100
}
```

>Response:

```json
{
    "error": null,
    "result": {"status": "success"},
    "id": 100
}
```


- method: kline.unsubscribe
- params: []

### Request Parameter

### Response Data


## Subscription of Latest Price

>Request:

```json
{
    "method":"price.subscribe", 
    "params":["BTCBCC"], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: price.subscribe
- params: [market]

### Request Parameter：
| Name of Parameter   | Parameter Type | Required | Description         |
| -------- | -------- | ---- | ------------ |
| market   | String   | Yes   | Market Name       |


### Response Data
Name of Parameter      |  Description
---------    |
status       | Successful or not


## Push of Latest Price

<aside class="notice">
   After the subscription is finished successfully，the data of the content will be actively pushed to client end.
</aside>

>Request:

```json
{
    "method": "price.update", 
    "params": ["BTCBCC", "8000.00000000"], 
    "id": null
}
```

- method: price.update
- params: [market,price]

### Request Parameter
Name of Parameter            | Type           |Description
---------          | ----          |------
market            | string        |Market Name
price               | string        |Latest Price




## Cancellation of Subscription on Latest Price

- method: price.unsubscribe
- params: []

>Request:

```json
{
    "method":"price.unsubscribe", 
    "params":[], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

### Request Parameter

### Response Data



## Subscription on Market Status

<aside class="notice">
   Subscription on 24-hour market status
</aside>


- method: state.subscribe
- params: market

>Request:

```json
{
    "method":"state.subscribe", 
    "params":["BTCBCC","BTCUSD"], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

### Request Parameter
Name of Parameter            |Description
---------          |------
market            | List of the market name of transaction pair traded  


### Response Data

Name of Parameter            |Description
---------          |------
status            |   Successful or not


## Push of Market Status

<aside class="notice">
  After the subscription is finished successfully，the data of status will be pushed to client end by trading server
</aside>


- method: state.update
- params: []

>Response:

```json
{
    "method": "state.update", 
    "params": [ 
        "BTCBCC", {
            "period": 86400, 
            "last": "8000", 
            "open": "0", 
            "close": "0", 
            "high": "0", 
            "low": "0", 
            "volume": "0", 
            "deal": "0"
        } 
    ], 
    "id": null
}
```

### Request Parameter
No

### Response Data
Please refer to state.query method for returned value



## Cancellation of Push on Market Status


>Request:

```json
{
    "method":"state.unsubscribe", 
    "params":[], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: state.unsubscribe
- params: []




## Subscription on The Market Status of The Current Day

<aside class="notice">
Subscription on market status of the current day
</aside>

>Request:

```json
{
    "method":"today.subscribe", 
    "params":["BTCUSD","BTCBCC"], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: today.subscribe
- params: 

### Request Parameter：
| Name of Parameter      | Parameter Type | Required | Description       |
| ----------- | -------- | ---- | ---------- |
| market list | String   | Yes   | List of Market Name |






## Push on The Market Status of The Current Day

After the subscription is finished successfully，the server will actively push data to client end.

>Response:

```json
{
    "method": "today.update", 
    "params": [ 
        "BTCBCC", {
            "open": "8000", 
            "last": "8000", 
            "high": "8000", 
            "low": "8000", 
            "volume": "0", 
            "deal": "0"
         }
     ], 
     "id": null
}
```



- method: today.update
- params: []


### Request Parameter
No

### Response Data
Name of Parameter             | Required or not          | Type                  |  Description
---------          | -------         | ----                  |------
period  | Yes |double|Period
last    | Yes |double|Latest Price
open    | Yes |Integer|Opening Price
close    | Yes |Integer|Closing Price
high    | Yes |Integer|Highest Price
low    | Yes |Integer|Lowest Price
volume    | Yes |double|Settled Volume
deal    | Yes |Integer|Trading Volume





## Cancellation of Subscription on The Market Status of The Current Day

>Request:

```json
{
    "method":"today.unsubscribe", 
    "params":[], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```


- method: today.unsubscribe
- params: []


### Request Parameter
No

### Response Data
status  Successful or not



## Subscription on Order Settlement


>Request:

```json
{
    "method":"deals.subscribe", 
    "params":["BTCBCC","BTCUSD"], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: deals.subscribe
- params:  [maket]

### Request Parameter
| market       | List of The Market Name of Transaction Pair Traded

### Response Data
status  Successful or not




## Push on Order Settlement

>Request:

```json
{
    "method": "deals.update", 
    "params": [ 
        "BTCBCC", [ 
             {"id": 26, "time": 1512454847.188796, "price": "8000", "amount": "1", "type": "buy"},
             {"id": 25, "time": 1512445625.751971, "price": "8000", "amount": "0.125", "type": "buy"},
             {"id": 24, "time": 1512442938.956193, "price": "8000", "amount": "0.125", "type": "buy"}, 
             ... 
             {"id": 22, "time": 1512442927.2021289, "price": "8000", "amount": "0.125", "type": "buy"},
             {"id": 3, "time": 1512442109.0283101, "price": "8000", "amount": "0.125", "type": "buy"},
             {"id": 2, "time": 1512441964.500567, "price": "8000", "amount": "0.125", "type": "buy"},
             {"id": 1, "time": 1512441751.9356339, "price": "8000", "amount": "0.125", "type": "buy"} 
         ]
     ], 
    "id": null
}
```

Please refer to the result returned by deals.query

## Cancellation of Subscription on Order Settlement

>Request:

```json
{ 
    "method":"deals.unsubscribe", 
    "params":[], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```


- method: deals.unsubscribe
- params: []


### Request Parameter
No

### Response Data
status  Successful or not


## Subscription on Order Depth


>Request:

```json
{ 
    "method":"depth.subscribe", 
    "params":["EOSUSDT",100,"0.1"], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: depth.subscribe
- "params":[ 
    "BTCBCC",  # Market Name 
    100,       # Available price level of order：1, 5, 10, 20, 30, 50, 100 
    "0.0001"   # Precision on price range, available values："0","0.00000001","0.0000001","0.000001","0.00001", "0.0001", "0.001", "0.01", "0.1"
]


### Request Parameter

| Name of Parameter        |  Description
| -----------  |------
| market       | Market Name
| price        | Order Price
| precision    | Precision on Price Range


### Response Data
status  Successful or not




## Subscription on The Depth of Order in Large Quantities

>Request:

```json
{ 
    "method":"depths.subscribe", 
    "params":[["ETCUSDT",100,"0.1"]], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: depths.subscribe
- params: [[ 
    market. ,  # market name 
    price,       # available price level of order：1, 5, 10, 20, 30, 50, 100 
    precision   # available precisions of price range："0","0.00000001","0.0000001","0.000001","0.00001", "0.0001", "0.001", "0.01", "0.1"
]]


### Request Parameter

| Name of Parameter        |  Description
| -----------  |------
| market       | Market Name
| price        | Order Price
| precision    | Precision of Price Range


### Response Data
status  successful or not


## Push of Data on Order Depth

>Request:

```json
{
    "method": "depth.update", 
    "params": [true, {"asks": [["8000", "20"]], "bids": [["800", "4"]]}, "BTCBCC"], 
    "id": null
}
```

- method: depth.update
- params: [ 
    true, #clean: Boolean, true: complete result，false: last returned updated result 
    { 
        "asks": [
            [
                "8000", # price 
                "20"    # volume 
            ],            
            [
                "8000.1", # price 
                "20"      # **the sum of the total number of all orders with their prices being price≥8000，less than8000.1**
            ]
         ], 
        "bids": 
        [
            [
                "800", 
                "4"
            ],
            [
                "800.1", 
                "5"
            ]
        ] 
     },
    "BTCBCC"             # Market name of transaction pair traded
]



Description on returned result：
Take the example of the precision of price range as 0.1


## Cancellation of Subscription on Order Depth

>Request:

```json
{
    "method":"depth.unsubscribe", 
    "params":[], 
    "id":100
}
```

>Response:

```json
{ 
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```


- method: depth.unsubscribe
- params: []


## Subscription on User's Order Status


>Request:

```json
{
    "method":"order.subscribe", 
    "params":["BTCBCC","BTCETH"], 
    "id":100
}
```

>Response:

```json
{ 
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: order.subscribe
- params: List of market name


## Push on Changes of User's Order

<aside class="notice">
   Each change on order's status will be pushed to client end.
</aside>


>Response:

```json
{
    "method": "order.update", 
    "params": [ 
        1, # Event type regarding the change on order status，Integer value 1-new order, 2-update order, 3-settled completely 
        {
            "id": 422458, 
            "market": "BTCBCC", 
            "source": "", 
            "type": 1, # 1-limit order 2 -market order
            "side": 1, # 1-Ask 2-Bid 
            "user": 5, 
            "ctime": 1513819599.987308, # create_time 
            "mtime": 1513819599.987308, # update_time 
            "price": "8000", 
            "amount": "10", 
            "taker_fee": "0.002", 
            "maker_fee": "0.001", 
            "left": "10", 
            "deal_stock": "0", 
            "deal_money": "0", 
            "deal_fee": "0" } 
    ], 
    "id": 102
}
```

- method: order.update
- params: []


## Cancellation on The Subscription of Changes on Order Status

- method: order.unsubscribe
- params: []

>Request:

```json
{   "method":"order.unsubscribe", 
    "params":[], 
    "id":100
}
```

>Response:

```json
{ 
    "error": null,
    "result": { "status": "success" }, 
    "id": 100
}
```

## Subscription on Information of User Asset


>Request:

```json
{ 
    "method":"asset.subscribe",
    "params":["BTC","ETH","BCC"], 
    "id":100
}
```

>Response:

```json
{ 
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: asset.subscribe
- params: List of asset name


## Push of Information on Change of User Asset

>Response:

```json
{ 
    "method": "asset.update", 
    "params": { 
        "ETH": { "available": "0", "freeze": "0" }, 
        "BTC": { "available": "0", "freeze": "0" } 
    }, 
    "id": 100
}
```

- method: asset.update
- params: []


## Subscription of Information on User Asset

>Request:

```json
{ 
    "method":"asset.unsubscribe", 
    "params":[], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: asset.unsubscribe
- params: []


