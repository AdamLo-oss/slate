# Inquiry Interface

## Line Data Inquiry

>Request:

```json
{
    "method":"kline.query",
    "params":["EOSETH",145231637,145232657,5],
    "id":100
}
```

>Response:

```json
{
    "error": null,
    "result": [
        [
            1525798800,    # Timestamp
            "0.00001790",  # Opening Price
            "0.00001881",  # Closing Price
            "0.00001886",  # Highest Price
            "0.00001790",  # Lowest Price
            "169033000",   # Trading Volume
            "3025.69",     # Trading Value
            "ACATETH"      # Transaction Market Name
        ],
        ...],
    "id": 123
} 
```

- method: kline.query
- params:

### Request Parameter

| Name of Parameter   | Parameter Type | Required | Description         |
| -------- | -------- | ---- | ------------ |
| market   | String   | Yes   | Market Name       |
| start    | Integer  | Yes   | Starting Time     |
| end      | Integer  | Yes   | Ending Time     |
| interval | Integer  | Yes   | Data Retrieval Period |

### Response Data
Please refer to the picture on the right hand side


## Inquiry on Latest Price

>Request:

```json
{
    "method":"price.query", 
    "params":["BTCBCC"], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": "8000.00000000", 
    "id": 100
}
```

- method: price.query
- params: ["market_name"]

### Request Parameter

| Name of Parameter   | Parameter Type | Required | Description         |
| -------- | -------- | ---- | ------------ |
| market   | String   | Yes   | Market Name       |



### Response Data

| Name of Parameter   | Parameter Type | Required | Description         |
| -------- | -------- | ---- | ------------ |
| result   | double   | Yes   | Price       |




## Inquiry on Current Market Status

>Request:

```json
{
    "method":"state.query", 
    "params":["BTCBCC",86400], 
    "id":100
}
```

>Response:

```json
{
    "period": 86400,  # period，unit second
    "last": "8000",   # latest price
    "open": "0",      # opening price
    "close": "0",     # closing price
    "high": "0",      # highest price
    "low": "0",       # lowest price
    "volume": "0",    # trading volume
    "deal": "0"       # trading value
},
```


- method: state.query
- params: 

### Request Parameter

| Name of Parameter   | Parameter Type | Required | Description         |
| -------- | -------- | ---- | ------------ |
| market list  | json array   | Yes   |  List of Transaction Pair's Market Name       |
| interval    | Integer  | Yes   | Period，Unit：Second，for example：86400 means 24 hours  |



### Response Data
Name of Parameter             | Required or not          | Type                  |  Description
---------          | -------         | ----                  |------
period  | Yes |Integer|Period
last    | Yes |double|Latest Price
open    | Yes |double|Opening Price
close    | Yes |double|Closing Price
high    | Yes |double|Highest Price
low    | Yes |double|Lowest Price
volume    | Yes |double|Trading Volume
deal    | Yes |double|Trading Volume



## Inquiry on The Market Status of The Current Day

<aside class="notice">
   The interface inquires the market status of calendar day，for example, if the current time is 2017-12-20 14:21:35，then by calling this interface, the returned result will be the data of 2017-12-20，which is different from state.query interface，the data that state.query returns are the data within a designated period of time，which may go beyond a calendar day
</aside>

>Request:

```json
{
    "method":"today.query", 
    "params":["BTCBCC"], 
    "id":100
}
```

>Response:

```json
{
    "last": "8000",   # Latest Price
    "open": "0",      # Opening Price
    "close": "0",     # Closing Price
    "high": "0",      # Highest Price
    "low": "0",       # Lowest Price
    "volume": "0",    # Trading Volume
    "deal": "0"       # Trading Value
},
```

- method: today.query
- params: 


### Request Parameter

| Name of Parameter | Parameter Type | Required | Description   |
| ------ | -------- | ---- | ------ |
| market | String   | Yes   | Market Name |




### Response Data
Name of Parameter             | Required or not          | Type                  |  Description
---------          | -------         | ----                  |------
last    | Yes |double|Latest Price
open    | Yes |double|Opening Price
close    | Yes |double|Closing Price
high    | Yes |double|Highest Price
low    | Yes |double|Lowest Price
volume    | Yes |double|Trading Volume
deal    | Yes |double|Trading Volume





## Inquiry on User's Order Settlement

>Request:

```json
{
    "method":"deals.query",
    "params":["BTCBCC",5,1], 
    "id":100
}
```

>Response:

```json
{ 
    "error": null, 
    "result": [ 
    { "id": 26, "time": 1512454847.188796, "price": "8000", "amount": "1", "type": "buy" }, 
    { "id": 25, "time": 1512445625.751971, "price": "8000", "amount": "0.125", "type": "buy" }, 
    { "id": 24, "time": 1512442938.956193, "price": "8000", "amount": "0.125", "type": "buy" }, 
    { "id": 23, "time": 1512442929.0405071, "price": "8000", "amount": "0.125", "type": "buy" }, 
    { "id": 22, "time": 1512442927.2021289, "price": "8000", "amount": "0.125", "type": "buy" } ], 
    "id": 100
}
```

- method: deals.query
- params: 

### Request Parameter

| Name of Parameter   | Parameter Type | Required | Description                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| market   | String   | Yes   | Market Name                                                       |
| limit    | Integer  | Yes   | Maximum Return Volume                                                 |
| last\_id | integer  | Yes   | The last id starting from the latest order id to the last id in the past (from smaller id number to bigger id number), for example, if there are 5 id altogether, namely 1,2,3,4 and 5, and that the last\_id is set as 3, then even if the limit is set as 5, only the data of the two groups of orders under order id 4 and 5 will be returned. |



### Response Data
Name of Parameter             | Required or not          | Type                  |  Description
---------           | -------         | ----                  |------
id                  | Yes              |double                 |deal_id
time               | Yes               |Integer(No Symbol 32 Digit)        |Trading Time
price              | Yes               |double                 |Trading Price
amount             | Yes               |double                 |Volume of Settled Orders
type               | Yes               |Integer                 |Type of Settlement







## Inquiry on The Depth of Order

>Request:

```json
{ 
    "method":"depth.query", 
    "params":["EOSUSDT",100,"1"], 
    "id":100
}
```

>Response:

```json
{ 
    "error": null, 
    "result": { "asks": [[ "8000", "20"] ], "bids": [[ "800", "4"] ] }, 
    "id": 100
}
```

- method: depth.query
- params: 

### Request Parameter

| Name of Parameter       | Parameter Type | Required | Description  |
| ------------ | -------- | ---- | ----- |
| market       | String   | Yes   | Market Name     |
| limit        | Integer  | Yes   | Maximum Volume Returned  |
| **interval** | String   | Yes   | Precision，for example"0.001"，the data retrieved will be the type of numbers such as：12.975. Another example"5"，you will retrieve numbers such as "15" "20" "10" . |


### Response Data
Name of Parameter             | Required or not          | Type                  |  Description
---------           | -------         | ----                  |------




## Inquiry on User's Unsettled Orders

<aside class="notice">
   Order API call requires auth verification，please call server.auth method for request of verification first，then call
</aside>


>Request:

```json
{ 
    "method":"order.query", 
    "params":[["BTCBCC","BTCETH"],0,50], 
    "id":100
}
or
{
    "method":"order.query", 
    "params":[[],0,50], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": {
        "ACATETH": {
            "limit": 100, 
            "offset": 0, 
            "total": 3, 
            "records": [
                {
                    "id": 8675864,               # Order ID
                    "market": "ACATETH",         # Market Name
                    "type": 1,                   # Order Type 1-Limit Order 2-Market Order
                    "side": 1,                   # Trading Direction 1-ASK 2-Bid
                    "user": 15731,               # User ID
                    "ctime": 1524482296.075341,  # The Order's Time of Creation
                    "mtime": 1524482296.075341,  # The Order's Time of Modification
                    "price": "0.00001899",       # Price
                    "amount": "1",               # Volume
                    "taker_fee": "0",            # taker fee rate
                    "maker_fee": "0",            # maker fee rate
                    "left": "1",                 # Remaining Unsettled Volume
                    "deal_stock": "0e-8",        # Settled Volume
                    "deal_money": "0e-16",       # Settled Value
                    "deal_fee": "0e-12"          # Fee of Settlement
                },
                ...
            ]
        }, 
        ……,
        "SPHTXBTC":{……}
    }
    "id": 13
}
```

- method: order.query
- params:

### Request Parameter

| Name of Parameter | Parameter Type | Required | Description                 |
| ------ | -------- | ---- | -------------------- |
| market list | list   | Yes   | List of market name, if blank, return all market data|
| offset | Integer  | Yes   | offset               |
| limit  | Integer  | Yes   | Maximum volume returned, less than 101 |



### Response Data
Name of Parameter                          | Type                      |  Description
---------                        | ----                      |------
id                                  |double                     |Order ID
market                               |string                   |Market Name
type                              |double                     |Order Type 1-Limit order 2-market order
side                             |double                     |Trading direction 1-ASK 2-Bid
user                               | Integer(No Symbol 32 Digit)                      |User ID
ctime                               | Integer(No Symbol 32 Digit)                      |The order's time of creation
mtime                               | Integer(No Symbol 32 Digit)                      |The order's time of modification
price                               | Integer(No Symbol 32 Digit)                      |Price
amount                               | Integer(No Symbol 32 Digit)                      |Volume
taker_fee                               | Integer(No Symbol 32 Digit)                      |taker fee rate
maker_fee                               | Integer(No Symbol 32 Digit)                      |maker fee rate
left                               | Integer(No Symbol 32 Digit)                      |Remaining Unsettled Volume
deal_stock                               | Integer(No Symbol 32 Digit)                      |Settled Volume
deal_money                               | Integer(No Symbol 32 Digit)                      |Settled Value
deal_fee                               | Integer(No Symbol 32 Digit)                      |Fee of Settlement






## Inquiry on The User's Settled Orders

>Request:

```json
{ 
    "method":"order.history", 
    "params":["BTCBCC",1511941006,1511941406,0,50], 
    "id":100}
```

>Response:

```json
{ 
    "error": null, 
    "result": { "limit": 50, "offset": 0, "total": 0, "records": [] }, 
    "id": 100 
}
```

- method: order.history
- param         

### Request Parameter

| Type of Parameter | Required | Description         |
| ----------- | -------- | ---- | -------------------- |
| market      | String   | Yes   | Market Name         |
| start_time | Integer  | Yes   | Starting Time             |
| end_time   | Integer  | Yes   | Ending Time             |
| offset      | Integer  | Yes   | offset               |
| limit       | Integer  | Yes   | Maximum returned volume, less than 101 |



### Response Data
Name of Parameter                          | Type                      |  Description
---------                        | ----                      |------
limit                                  |double                     |
offset                               |string                   |
total                               |string                   |
records                               |string                   |


**Returned Value：Refer to order.query method for returned value. **




## Inquiry on User's Asset

<aside class="notice">
   The call requires auth verification，please call server.auth method for the request of verification first，then call.
</aside>


>Request:

```json
{
    "method":"asset.query", 
    "params":["ETH","BTC"], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { 
        "ETH": { 
            "available": "0",  # Available Asset
            "freeze": "0"      # Frozen Asset
        }, 
        "BTC": { "available": "0", "freeze": "0" } 
    }, 
    "id": 100
}
```

- method: asset.query
- params: []

### Request Parameter
Returned Value：Refer to the example above.


### Response Data

Name of Parameter                          | Type                       |  Description
---------                        | ----                      |------
available                        |double                     | Available Asset
freeze                           |string                      |Frozen Asset



## Inquiry Regarding The Records of Changes in User's Asset

>Request:

```json
{
    "method":"asset.history", 
    "params":["BTC","deposit",1501940406,1513328112,0,100], 
    "id":100
}
```

>Response:

```json
{
    "error": null, 
    "result": { 
        "offset": 0, 
        "limit": 100, 
        "records": [ 
            { 
              "time": 1511856143.3754101,   # Timestamp
              "asset": "USD",               # Asset Type
              "business":"deposit",         # Business Identifier deposit-deposit，freeze-freeze/defreeze，withdraw-withdrawal
              "change": "100000",           # Change of Asset
              "balance": "300000",          # Balance of user's asset after the change
              "detail": { "id": 10003 }     # Other Details
            }, 
            ... 
         ] 
    }, 
    "id": 100 
}
```

- method: asset.history
- params:

### Request Parameter

| Name of Parameter      | Parameter Type | Required | Description                          |
| ----------- | -------- | ---- | ----------------------------- |
| asset       | String   | Yes   | asset name, which can be null |
| business    | String   | Yes   | Name of Business                        |
| start_time | Integer  | Yes   | Starting Time                      |
| end_time   | Integer  | Yes   | Ending Time                      |
| offset      | Integer  | Yes   | offset                        |
| limit       | Integer  | Yes   | Maximum returned volume, less than 101          |




### Response Data

Name of Parameter                          | Type                       |  Description
---------                        | ----                      |------
time                        |double                     | Timestamp
asset                           |string                      |Asset Type
business                           |string                      |Business Identifier deposit-deposit，freeze-freeze/defreeze，withdraw-withdrawal
change                           |string                      |Change of Asset
balance                           |string                      |Balance of user's asset after the change
detail                           |string                      |Frozen Asset

