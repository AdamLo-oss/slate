# 查询接口

## 线数据查询

>请求:

```json
{
    "method":"kline.query",
    "params":["EOSETH",145231637,145232657,5],
    "id":100
}
```

>响应:

```json
{
    "error": null,
    "result": [
        [
            1525798800,    # 时间戳
            "0.00001790",  # 开盘价
            "0.00001881",  # 收盘价
            "0.00001886",  # 最高价
            "0.00001790",  # 最低价
            "169033000",   # 成交量
            "3025.69",     # 成交额
            "ACATETH"      # 交易对市场名称
        ],
        ...],
    "id": 123
} 
```

- method: kline.query
- params:

__请求__

| 参数名   | 参数类型 | 必填 | 描述         |
| -------- | -------- | ---- | ------------ |
| market   | String   | 是   | 市场名       |
| start    | Integer  | 是   | 开始时间     |
| end      | Integer  | 是   | 结束时间     |
| interval | Integer  | 是   | 数据获取周期 |

__响应数据__

参照 /api/v1/market.kline`


## 最新价格查询

>请求:

```json
{
    "method":"price.query", 
    "params":["BTCBCC"], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": "8000.00000000", 
    "id": 100
}
```

- method: price.query
- params: ["market_name"]

__请求__

| 参数名   | 参数类型 | 必填 | 描述         |
| -------- | -------- | ---- | ------------ |
| market   | String   | 是   | 市场名       |



__响应数据__


| 参数名   | 参数类型 | 必填 | 描述         |
| -------- | -------- | ---- | ------------ |
| result   | double   | 是   | 价格       |




## 当前市场状态查询

>请求:

```json
{
    "method":"state.query", 
    "params":["BTCBCC",86400], 
    "id":100
}
```

>响应:

```json
{
    "period": 86400,  # 周期，单位秒
    "last": "8000",   # 最新价
    "open": "0",      # 开盘价
    "close": "0",     # 收盘价
    "high": "0",      # 最高价
    "low": "0",       # 最低价
    "volume": "0",    # 成交量
    "deal": "0"       # 成交额
},
```


- method: state.query
- params: 

__请求__

| 参数名   | 参数类型 | 必填 | 描述         |
| -------- | -------- | ---- | ------------ |
| market list  | json array   | 是   | 交易对市场名称列表       |
| interval    | Integer  | 是   | 周期，单位：秒，例如：86400表示24小时  |



__响应数据__

参数名称             | 是否必须          | 类型                  |  描述
---------          | -------         | ----                  |------
period  | 是 |Integer|周期
last    | 是 |double|最新价
open    | 是 |double|开盘价
close    | 是 |double|收盘价
high    | 是 |double|最高价
low    | 是 |double|最低价
volume    | 是 |double|成交量
deal    | 是 |double|交易量



## 当天的市场状态查询

<aside class="notice">
   该接口查询自然日的市场状态，例如当前时间是2017-12-20 14:21:35，调用该接口返回的是2017-12-20这一天的数据，这点和state.query接口不同，state.query返回的是指定时间内的数据，可以跨自然日
</aside>

>请求:

```json
{
    "method":"today.query", 
    "params":["BTCBCC"], 
    "id":100
}
```

>响应:

```json
{
    "last": "8000",   # 最新价
    "open": "0",      # 开盘价
    "close": "0",     # 收盘价
    "high": "0",      # 最高价
    "low": "0",       # 最低价
    "volume": "0",    # 成交量
    "deal": "0"       # 成交额
},
```

- method: today.query
- params: 


__请求__

| 参数名 | 参数类型 | 必填 | 描述   |
| ------ | -------- | ---- | ------ |
| market | String   | 是   | 市场名 |




__响应数据__

参数名称             | 是否必须          | 类型                  |  描述
---------          | -------         | ----                  |------
last    | 是 |double|最新价
open    | 是 |double|开盘价
close    | 是 |double|收盘价
high    | 是 |double|最高价
low    | 是 |double|最低价
volume    | 是 |double|成交量
deal    | 是 |double|交易量





## 用户成交查询

>请求:

```json
{
    "method":"deals.query",
    "params":["BTCBCC",5,1], 
    "id":100
}
```

>响应:

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

__请求__

| 参数名   | 参数类型 | 必填 | 描述                                         |   取值范围
| -------- | -------- | ---- | ------------------------------------------|--------------
| market   | String   | 是   | 市场名                                     |
| limit    | Integer  | 是   | 最大返回数量                                |
| last_id | integer  | 是   | 从最近一个订单id开始往前（id从大到小）最后一个id  | 例如一共有1，2，3，4，5，一共5个id，last\_id设为3，limit即使设为5也只返回id为4，5两组数据。 |



__响应数据__


参数名称   | 是否必须          | 类型                  |  描述
---------| -------         | ----                  |------
id       | 是              |double                 |deal_id
time     | 是               |Integer(无符32位)        |交易时间
price    | 是               |double                 |交易价格
amount   | 是               |double                 |成交数量
type     | 是               |Integer                 |成交类型



## 定单深度查询

>请求:

```json
{ 
    "method":"depth.query", 
    "params":["EOSUSDT",100,"1"], 
    "id":100
}
```

>响应:

```json
{ 
    "error": null, 
    "result": { "asks": [[ "8000", "20"] ], "bids": [[ "800", "4"] ] }, 
    "id": 100
}
```

- method: depth.query
- params: 

__请求__

| 参数名       | 参数类型 | 必填 | 描述  |
| ------------ | -------- | ---- | ----- |
| market       | String   | 是   | 市场名     |
| limit        | Integer  | 是   | 最大返回数量  |
| **interval** | String   | 是   | 精度，比如"0.001"，获取的数据就是：12.975这样的数字。再比如"5"，就会得到"15" "20" "10" 这样的数字。 |


__响应数据__

参数名称             | 是否必须          | 类型                  |  描述
---------           | -------         | ----                  |------




## 用户未完成定单查询

<aside class="notice">
   Order API 调用需要auth认证，请先调用server.auth方法请求认证，然后再调用
</aside>


>请求:

```json
{ 
    "method":"order.query", 
    "params":[["BTCBCC","BTCETH"],0,50], 
    "id":100
}
或
{
    "method":"order.query", 
    "params":[[],0,50], 
    "id":100
}
```

>响应:

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
                    "id": 8675864,               # 定单ID
                    "market": "ACATETH",         # 市场名称
                    "type": 1,                   # 定单类型 1-限价单 2-市价单
                    "side": 1,                   # 买卖方向 1-ASK 2-Bid
                    "user": 15731,               # 用户ID
                    "ctime": 1524482296.075341,  # 定单创建时间
                    "mtime": 1524482296.075341,  # 定单修改时间
                    "price": "0.00001899",       # 价格
                    "amount": "1",               # 数量
                    "taker_fee": "0",            # taker的费率
                    "maker_fee": "0",            # maker的费率
                    "left": "1",                 # 剩余未成交量
                    "deal_stock": "0e-8",        # 成交量
                    "deal_money": "0e-16",       # 成交金额
                    "deal_fee": "0e-12"          # 成交费用
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

__请求__

| 参数名 | 参数类型 | 必填 | 描述                 |
| ------ | -------- | ---- | -------------------- |
| market list | list   | 是   | 市场名列表，如果为空的话，返回所有市场的数据|
| offset | Integer  | 是   | offset               |
| limit  | Integer  | 是   | 最大返回数量,小于101 |



__响应数据__

参数名称                          | 类型                      |  描述
---------                        | ----                      |------
id                                  |double                     |定单ID
market                               |string                   |市场名称
type                              |double                     |定单类型 1-限价单 2-市价单
side                             |double                     |买卖方向 1-ASK 2-Bid
user                               | Integer(无符号32位)                      |用户ID
ctime                               | Integer(无符号32位)                      |定单创建时间
mtime                               | Integer(无符号32位)                      |定单修改时间
price                               | Integer(无符号32位)                      |价格
amount                               | Integer(无符号32位)                      |数量
taker_fee                               | Integer(无符号32位)                      |taker的费率
maker_fee                               | Integer(无符号32位)                      |maker的费率
left                               | Integer(无符号32位)                      |剩余未成交量
deal_stock                               | Integer(无符号32位)                      |成交量
deal_money                               | Integer(无符号32位)                      |成交金额
deal_fee                               | Integer(无符号32位)                      |成交费用






## 用户已完成定单查询

>请求:

```json
{ 
    "method":"order.history", 
    "params":["BTCBCC",1511941006,1511941406,0,50], 
    "id":100}
```

>响应:

```json
{ 
    "error": null, 
    "result": { "limit": 50, "offset": 0, "total": 0, "records": [] }, 
    "id": 100 
}
```

- method: order.history
- param         

__请求__

| 参数类型 | 必填 | 描述         |
| ----------- | -------- | ---- | -------------------- |
| market      | String   | 是   | 市场名               |
| start_time | Integer  | 是   | 开始时间             |
| end_time   | Integer  | 是   | 结束时间             |
| offset      | Integer  | 是   | offset               |
| limit       | Integer  | 是   | 最大返回数量,小于101 |



__响应数据__

参数名称                          | 类型                      |  描述
---------                        | ----                      |------
limit                                  |double                     |
offset                               |string                   |
total                               |string                   |
records                               |string                   |

<aside class="notice">
   返回值：参考order.query方法返回值。
</aside>



## 用户资产查询

<aside class="notice">
   调用需要auth认证，请先调用server.auth方法请求认证，然后再调用。
</aside>


>请求:

```json
{
    "method":"asset.query", 
    "params":["ETH","BTC"], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { 
        "ETH": { 
            "available": "0",  # 可用资金
            "freeze": "0"      # 冻结资金
        }, 
        "BTC": { "available": "0", "freeze": "0" } 
    }, 
    "id": 100
}
```

- method: asset.query
- params: []

__请求__
返回值：参考上面示例。


__响应数据__


参数名称                          | 类型                       |  描述
---------                        | ----                      |------
available                        |double                     | 可用资金
freeze                           |string                      |冻结资金



## 用户资产变动历史查询

>请求:

```json
{
    "method":"asset.history", 
    "params":["BTC","deposit",1501940406,1513328112,0,100], 
    "id":100
}
```

>响应:

```json
{
    "error": null, 
    "result": { 
        "offset": 0, 
        "limit": 100, 
        "records": [ 
            { 
              "time": 1511856143.3754101,   # 时间戳
              "asset": "USD",               # 资产类型
              "business":"deposit",         # 业务标识 deposit-充值，freeze-冻结/解冻，withdraw-提币
              "change": "100000",           # 变动金额
              "balance": "300000",          # 变动后用户资金余额
              "detail": { "id": 10003 }     # 其他详情
            }, 
            ... 
         ] 
    }, 
    "id": 100 
}
```

- method: asset.history
- params:

__请求__

| 参数名      | 参数类型 | 必填 | 描述                          |
| ----------- | -------- | ---- | ----------------------------- |
| asset       | String   | 是   | asset name, which can be null |
| business    | String   | 是   | 业务名                        |
| start_time | Integer  | 是   | 开始时间                      |
| end_time   | Integer  | 是   | 结束时间                      |
| offset      | Integer  | 是   | offset                        |
| limit       | Integer  | 是   | 最大返回数量,小于101          |




__响应数据__


参数名称                          | 类型                       |  描述
---------                        | ----                      |------
time                        |double                     | 时间戳
asset                           |string                      |资产类型
business                           |string                      |业务标识 deposit-充值，freeze-冻结/解冻，withdraw-提币
change                           |string                      |变动金额
balance                           |string                      |变动后用户资金余额
detail                           |string                      |冻结资金

