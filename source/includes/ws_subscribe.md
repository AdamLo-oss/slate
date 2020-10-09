# 订阅/取消订阅接口


## 行情订阅

>请求:

```json
{
    "method":"kline.subscribe", 
    "params":[ "BTCBCC", 60 ], 
    "id":100
}
```
>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```



- method: kline.subscribe
- params: 

请求参数：

| 参数名   | 参数类型 | 必填 | 描述         |
| -------- | -------- | ---- | ------------ |
| market   | String   | 是   | 市场名       |
| interval | Integer  | 是   | 数据获取周期 |


订阅成功后，订阅数据将会被推送到客户端。内容如 **[行情推送]** 所述。

## 行情推送

>请求:

```json
{
    "method": "kline.update", 
    "params": [[1513135140, "8000", "8000", "8000", "8000", "0", "0", "BTCBCC"]], 
    "id": null
}
```


请求参数：
"params": [ 
    [ 
      1492358400,  # 时间戳
      "7000.00",   # 开盘价
      "8000.0",    # 收盘价
      "8100.00",   # 最高价
      "6800.00",   # 最低价
      "1000.00"    # 成交量
      "123456.00", # 成交金额
      "BTCBCC"     # 交易币对市场名称
    ]
]



## 取消行情订阅

>请求:

```json
{
    "method":"kline.unsubscribe", 
    "params":[], 
    "id":100
}
```

>响应:

```json
{
    "error": null,
    "result": {"status": "success"},
    "id": 100
}
```


- method: kline.unsubscribe
- params: []

__请求__

__响应数据__



## 最新价订阅

>请求:

```json
{
    "method":"price.subscribe", 
    "params":["BTCBCC"], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: price.subscribe
- params: [market]

__请求__：
| 参数名   | 参数类型 | 必填 | 描述         |
| -------- | -------- | ---- | ------------ |
| market   | String   | 是   | 市场名       |


__响应数据__

参数名称      |  描述
---------    |
status       | 是否成功


## 最新价推送

<aside class="notice">
   订阅成功后，向客户端主动推送数据内容。
</aside>

>请求:

```json
{
    "method": "price.update", 
    "params": ["BTCBCC", "8000.00000000"], 
    "id": null
}
```

- method: price.update
- params: [market,price]

__请求__
参数名称            | 类型           |描述
---------          | ----          |------
market            | string        |市场名称
price               | string        |最新价格




## 取消最新价订阅

- method: price.unsubscribe
- params: []

>请求:

```json
{
    "method":"price.unsubscribe", 
    "params":[], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

__请求__

__响应数据__




## 市场状态订阅

<aside class="notice">
   24小时市场状态订阅。
</aside>


- method: state.subscribe
- params: market

>请求:

```json
{
    "method":"state.subscribe", 
    "params":["BTCBCC","BTCUSD"], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

__请求__
参数名称            |描述
---------          |------
market            | 交易币对市场名称列表  


__响应数据__


参数名称            |描述
---------          |------
status            |   是否成功


## 市场状态推送

<aside class="notice">
  订阅成功后，状态数据会被交易服务器推送给客户端。
</aside>


- method: state.update
- params: []

>响应:

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

__请求__
无

__响应数据__

返回值参考state.query方法。



## 取消市场状态推送


>请求:

```json
{
    "method":"state.unsubscribe", 
    "params":[], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: state.unsubscribe
- params: []




## 当日市场状态订阅

<aside class="notice">
当天market状态订阅。
</aside>

>请求:

```json
{
    "method":"today.subscribe", 
    "params":["BTCUSD","BTCBCC"], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: today.subscribe
- params: 

__请求__：
| 参数名      | 参数类型 | 必填 | 描述       |
| ----------- | -------- | ---- | ---------- |
| market list | String   | 是   | 市场名列表 |






## 当日市场状态推送

订阅成功后，服务器主动向客户端推送数据。

>响应:

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


__请求__
无

__响应数据__

参数名称             | 是否必须          | 类型                  |  描述
---------          | -------         | ----                  |------
period  | 是 |double|周期
last    | 是 |double|最新价
open    | 是 |Integer|开盘价
close    | 是 |Integer|收盘价
high    | 是 |Integer|最高价
low    | 是 |Integer|最低价
volume    | 是 |double|成交量
deal    | 是 |Integer|交易量





## 取消当日市场状态订阅

>请求:

```json
{
    "method":"today.unsubscribe", 
    "params":[], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```


- method: today.unsubscribe
- params: []


__请求__
无

__响应数据__

status  是否成功



## 成交订阅


>请求:

```json
{
    "method":"deals.subscribe", 
    "params":["BTCBCC","BTCUSD"], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: deals.subscribe
- params:  [maket]

__请求__
| market       | 交易币对市场名称列表

__响应数据__

status  是否成功




## 成交推送

>请求:

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

参考deals.query的返回结果。 

## 取消成交订阅

>请求:

```json
{ 
    "method":"deals.unsubscribe", 
    "params":[], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```


- method: deals.unsubscribe
- params: []


__请求__
无

__响应数据__

status  是否成功


## 定单深度订阅


>请求:

```json
{ 
    "method":"depth.subscribe", 
    "params":["EOSUSDT",100,"0.1"], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: depth.subscribe
- "params":[ 
    "BTCBCC",  # 市场名 
    100,       # 定单价格,取值：1, 5, 10, 20, 30, 50, 100 
    "0.0001"   # 价格区间精度, 取值："0","0.00000001","0.0000001","0.000001","0.00001", "0.0001", "0.001", "0.01", "0.1"
]


__请求__

| 参数名        |  描述
| -----------  |------
| market       | 市场名
| price        | 定单价格
| precision    | 价格区间精度


__响应数据__

status  是否成功




## 定单批量深度订阅

>请求:

```json
{ 
    "method":"depths.subscribe", 
    "params":[["ETCUSDT",100,"0.1"]], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: depths.subscribe
- params: [[ 
    market. ,  # 市场名 
    price,       # 定单价格,取值：1, 5, 10, 20, 30, 50, 100 
    precision   # 价格区间精度, 取值："0","0.00000001","0.0000001","0.000001","0.00001", "0.0001", "0.001", "0.01", "0.1"
]]


__请求__

| 参数名        |  描述
| -----------  |------
| market       | 市场名
| price        | 定单价格
| precision    | 价格区间精度


__响应数据__

status  是否成功


## 定单深度数据推送

>请求:

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
                "8000", # 价格 
                "20"    # 数量 
            ],            
            [
                "8000.1", # 价格 
                "20"      # **价格≥8000，小于8000.1的所有定单数量和之和**
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
    "BTCBCC"             # 交易币对的市场名称
]



返回结果说明：
以价格区间精度为0.1为例。


## 取消定单深度订阅

>请求:

```json
{
    "method":"depth.unsubscribe", 
    "params":[], 
    "id":100
}
```

>响应:

```json
{ 
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```


- method: depth.unsubscribe
- params: []


## 用户定单状态订阅


>请求:

```json
{
    "method":"order.subscribe", 
    "params":["BTCBCC","BTCETH"], 
    "id":100
}
```

>响应:

```json
{ 
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: order.subscribe
- params: 市场名称列表


## 用户定单变化推送

<aside class="notice">
   定单的每次状态变化都会推送给用户端
</aside>


>响应:

```json
{
    "method": "order.update", 
    "params": [ 
        1, # 定单状态变化事件类型，整数值 1-新定单, 2-更新定单, 3-完全成交 
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


## 取消定单状态变化订阅

- method: order.unsubscribe
- params: []

>请求:

```json
{   "method":"order.unsubscribe", 
    "params":[], 
    "id":100
}
```

>响应:

```json
{ 
    "error": null,
    "result": { "status": "success" }, 
    "id": 100
}
```

## 用户资产信息订阅


>请求:

```json
{ 
    "method":"asset.subscribe",
    "params":["BTC","ETH","BCC"], 
    "id":100
}
```

>响应:

```json
{ 
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: asset.subscribe
- params: 资产名称列表


## 用户资产变化信息推送

>响应:

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


## 用户资产信息订阅

>请求:

```json
{ 
    "method":"asset.unsubscribe", 
    "params":[], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { "status": "success" }, 
    "id": 100
}
```

- method: asset.unsubscribe
- params: []


