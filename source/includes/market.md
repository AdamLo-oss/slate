# 行情数据

## 获取交易对列表

__HTTP 请求__

* `GET /api/v1/market.list`

__请求参数__

此接口不接受任何参数。

>Response:

```json
	{
	    "error": null,
	    "result": [
	        {
	            "name": "QASHBTC",
	            "stock": "QASH",
	            "money": "BTC",
	            "fee_prec": 4,  
	            "stock_prec": 2, 
	            "money_prec": 8, 
	            "min_amount": "0.1" 
	        },
	        {
	            "name": "QASHETH",
	            "stock": "QASH",
	            "money": "ETH",
	            "fee_prec": 4,
	            "stock_prec": 2,
	            "money_prec": 8,
	            "min_amount": "0.0001"
	        }
	    ],
	    "id": 1521169333
	}
```

__请求参数__
无

__响应数据__

参数名称      | 是否必须  | 类型   |  描述          |   取值范围
-------------| ------- | -------|---------------|------------
name         | 是      | string | 交易对          | -     
stock        | 是      | string | 交易的币种       | -
money        | 是      | string | 使用的币种       | -
fee_prec     | 是      | Integer | 税率精度4位小数  | -
stock_prec   | 是      | Integer | stock精度      | -
money_prec   | 是      | Integer | money精度      | -
min_amount   | 是      | double  | 下单最小值      | -

<!-- 


 -->
## 获取指定交易对的最新价格

__HTTP 请求__

* `GET /api/v1/market.last`

__请求参数__

参数名称  | 是否必须 | 类型    |描述        |   取值范围
---------| -------| --------|-----------|-------------
market   |是      | string   |market名称 |"BTC/USDT","BCC/USDT"...



>Response:

```json
{
    "error": null,
    "result": "0.07413600",
    "id": 1521169525
}
```

__响应数据__


参数名称      | 是否必须  | 类型   |  描述          |   取值范围
-------------| ------- | -------|---------------|------------
result       | 是      | double  | 下单最小值      | -


## 查询交易对交易记录


__HTTP 请求__

* `GET /api/v1/market.deals`

__请求参数__


参数名称      | 是否必须  | 类型               |  描述                               |   取值范围
-------------| ------- | -------------------|------------------------------------|------------
market       | 是      | string             | 交易对                              | "BTC/USDT","BCC/USDT"...     
limit        | 是      | Integer            | 查询个数限制                         | limit <= 1000)
last_id      | 是      | Integer(无符号64位) |  返回大于order_id > last_id的交易数据  | -



>Response:

```json
{
    "error": null,
    "result": [],
    "id": 1521169562
}
```

__响应数据__


参数名称      | 是否必须  | 类型   |  描述          |   取值范围
-------------| ------- | -------|---------------|------------
result       | 是      |  -      |               | -



## 查询用户交易记录

__HTTP 请求__

* `POST /api/v1/market.user_deals`

__请求参数__

参数名称 | 是否必须 | 类型                 |描述            |   取值范围
--------| --------| ---- ----------------|-------------|------------
api_key |是       | string               |用户API KEY   | -
sign    |是       | Integer              |用户签名值     | -
market  |是        | Integer(无符号64位)  |返market名称， | -如："BTC/USDT","BCC/USDT"
offset  |是         | Integer(无符号64位) |偏移位置       | -
limit   |是        | Integer(无符号64位)  |查询个数限制    | 0，1，2，3，4....1000


<aside class="notice">
   offset — 如果设置为0，表示从最新一个订单开始算起，往之前时间的所有交易记录，总笔数不能大于limit；如果设置为1，表示从次新一个订单开始算起，往之前时间的所有满足条件订单记录，总数不能大于limit；以此类推.....
</aside>

<aside class="notice">
   limit — limit <= 1000
</aside>


>Response:

```json
{

}
```
__响应数据__

参数名称  | 是否必须 | 类型   |描述    |   取值范围
---------| -------| ------|-------|------------
result   | 是     |       |        |



## k线查询

__HTTP 请求__

* `GET /api/v1/market.kline`

__请求参数__

参数名称         | 是否必须        | 类型                   |描述                |   取值范围
---------      | -------        | ----                  |--------------------|-----------
market         |是              | string                 |market名称          |"BTC/USDT","BCC/USDT"
start_time      |是              | Integer(无符号64位)    |起始时间戳(秒)        | 1563724800 时间戳（秒）
end_time        |是              | Integer(无符号64位)    |结束时间戳(秒)        | 1563726800 时间戳（秒）
interval        |是              | 	Integer(32位)        |周期间隔,单位秒,(起始时间到结束时间，总周期数)|      | 0，1，2，3..1000,interval < 1000

<aside class="notice">
   interval < 1000
</aside>


>Response:

```json
{
    "error": null,
    "result": [  
	    	[1525067600, "11714.04", "11710.01", "11778.69", "11697.18", "13.604065", "159329.23062211", "BTCUSDT"], 
	    	[1565067660, "11703.47", "11716.65", "11720.55", "11703.47", "14.401973", "168649.82127032", "BTCUSDT"], 
	    	[1565067720, "11714.24", "11715.09", "11724.5", "11707.78", "12.287975", "143952.77384769", "BTCUSDT"]
    	],
    "id": 1521169586
}
```
__响应数据__

参数名称   | 是否必须  | 类型               |  描述    |   取值范围
----------| --------| ------------------|----------|-----------------------
数组0      |  是     | Integer(无符号64位)| 时间戳    | 1525067600 时间戳
数组1      |  是     | double            | 开盘价     | -
数组2      |  是     | double            | 收盘价     | -
数组3      |  是     | double            | 最高价     | -
数组4      |  是     | double            | 最低价     | -
数组5      |  是     | double            | 涨幅       | -
数组6      |  是     | double            | 成交量     | -
数组7      |  是     | string            | 成交对     | -
<!-- 


 -->


## 获取过去指定时间段market当前最新涨跌幅，交易量，最高/最低价格等状态

__HTTP 请求__

* `GET /api/v1/market.status`

__请求参数__

参数名称  | 是否必须 | 类型            |描述                |   取值范围
---------| --------| ---------------|-------------------|-----------------------
market   |是       | string         |market名称          |"BTC/USDT","BCC/USDT"
period   |是       | Integer(32位)  |查询周期，以秒为单位。即从现在开始往前推的时间，|例如：86400，是过去24小时。


>Response:

```json
{
    "error": null,
    "result": {
        "period": 10,
        "last": "0.0743",
        "open": "0.074162",
        "close": "0.0743",
        "high": "0.0743",
        "low": "0.074162",
        "volume": "0.314",
        "deal": "0.023315531"
    },
    "id": 1521169247
}
```
__响应数据__

参数名称      | 是否必须 | 类型   |  描述|取值范围
------------| --------| ------ |-------|----------------
period      | 是      |Integer |查询周期 | 例如：86400，是过去24小时。 
last        | 是      |double  | 最新价 | -
open        | 是      |double  |开盘价 | -
close       | 是      |double   |收盘价 | -
high        | 是      |double  |最高价 | -
low         | 是      |double  |最低价 | -
volume      | 是      |double  |成交量 | -
deal        | 是      |double  |交易量 | -




## 获取当日market状态	


__HTTP 请求__

* `GET /api/v1/market.status_today`

__请求参数__

参数名称  | 是否必须 | 类型   |描述   |取值范围
---------| --------| ---------------|-------------------|-----------------------
market   |是      | string  |market名称，| 如："BTC/USDT","BCC/USDT"

>Response:

```json
{
    "error": null,
    "result": {
        "open": "0.074015",
        "last": "0.074287",
        "high": "0.074485",
        "low": "0.073",
        "volume": "1141.63",
        "deal": "83.11985574"
    },
    "id": 1521169293
}
```
__响应数据__

参数名称     | 是否必须 | 类型     |  描述|   取值范围
---------| --------| ---------------|-------------------|-----------------------
last        | 是      |double  |最新价| -
open    | 是 |Integer|开盘价| -
close    | 是 |Integer|收盘价| -
high    | 是 |Integer|最高价| -
low    | 是 |Integer|最低价| -
volume    | 是 |Integer|成交量| -
deal    | 是 |Integer|交易量| -




## 获取当日market状态	

__HTTP 请求__

* `GET /api/v1/market.status24h`

__请求参数__

此接口不接受任何参数。

>Response:

```json
{
    "TRXETH": {
        "period": 86400,
        "last": "0.00013199",
        "open": "0.00013523",
        "close": "0.00013199",
        "high": "0.00013723",
        "low": "0.00013199",
        "volume": "887054.18",
        "deal": "119.2565600483",
    },
    "error": null,
    "result": {
        "open": "0.074015",
        "last": "0.074287",
        "high": "0.074485",
        "low": "0.073",
        "volume": "1141.63",
        "deal": "83.11985574"
    },
    "id": 1521169293
}
```

__响应数据__

参数名称    | 是否必须  | 类型  |  描述  |   取值范围
---------| --------| ---------------|-------------------|-----------------------
period     | 是       |Integer32|周期 | 86400
last       | 是       |double|最新价  |  -
open       | 是       |double|开盘价  |  -
close      | 是       |double|收盘价  |  -
high       | 是       |double|最高价  |  -
low        | 是       |double|最低价  |  -
volume     | 是       |double|成交量  |  -
deal       |  是      |double|交易量  |  -




## market概要	

__HTTP 请求__

* `GET /api/v1/market.summary`

__请求参数__

参数名称       | 是否必须   | 类型          |描述
--------------| ---------| ------------ |------
markets       |是         | json array   |market名称json array，如：["BTCUSD","BCCUSD"]，如为空数组:[],返回所有market。

>Response:

```json
{
    "error": null,
    "result": [
        {
            "name": "ETHBTC",
            "ask_count": 0,
            "ask_amount": "0",
            "bid_count": 0,
            "bid_amount": "0"
        },
        {
            "name": "QUNBTC",
            "ask_count": 2,
            "ask_amount": "28",
            "bid_count": 2,
            "bid_amount": "23"
        }
    ],
    "id": 1521169429
}
```

__响应数据__

参数名称  | 是否必须   | 类型       |  描述
---------| ---------| -----------| ------
  name   | 是        |  string   | 交易对
  ask_count   | 是   |  double   | 交易对
  ask_amount   | 是  |  double   | 交易对
  bid_count   | 是   |  double   | 交易对
  bid_amount   | 是  |  double   | 交易对



