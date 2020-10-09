# 基础信息

## 资产类型和精度


此接口返回所有资产类型和精度


__HTTP 请求__

* GET /api/v1/asset.list


```shell
curl  "https://api.hotbit.io/api/v1/asset.list"
```

__返回字段__

字段名称 | 数据类型 | 描述
--------- | ------------- | -------------
name 	  | string 		  | 币种
prec      | int 		  | 精确到小数点后多少位	


> Response: 

```json
{
	"result":[
		{
			"name": "BTC",
			"prec": 8
		},
		{
			"name": "ETH",
			"prec": 8
		},
		{
			"name": "USDT",
			"prec": 8
		},
	],
	"error": null,
	"id": 1585283976
}
```






## 获取当前系统时间戳

此接口返回当前的系统时间戳。


```shell
curl  "https://api.hotbit.io/api/v1/server.time"
```


__HTTP 请求__

* GET /api/v1/server.time


__请求参数__


此接口不接受任何参数。




> Response: 

```json
{
	"error": null,
	"id": 0,
	"result": 1585282798
}
```


## 最新成交信息

此接口返回获取全市场交易对的最新成交信息


```shell
curl  "https://api.hotbit.io/api/v1/allticker"
```


__HTTP 请求__

* GET /api/v1/server.time


__请求参数__


此接口不接受任何参数。





> Response: 

```json
{
	"date": 1585282798,
	"ticker": [
		{
			"buy": "6711.35",
			"close": "6709.14",
			"high": "6837.32",
			"last": "6709.14",
			"low": "6523.3",
			"open": "6679.74",
			"sell": "6714.73",
			"symbol": "BTC_USDT",
			"vol": "155414.70091"
		},
		{
			"buy": "137.9",
			"close": "138.09",
			"high": "140.91",
			"last": "138.09",
			"low": "133.53",
			"open": "136.76",
			"sell": "138.01",
			"symbol": "ETH_USDT",
			"vol": "2919662.76839"
		}
	]
}
```

__返回字段__

字段名称 | 数据类型 | 描述
--------- | ------------- | -------------
symbol 	  | string 		  | 交易对名称
buy      | string 		  | 买一价
sell      | string 		  | 卖一价
open      | string 		  | 开盘价
close      | string 	  | 收盘价
high      | string 		  | 最高价
low      | string 		  | 最低价
last      | string 		  | 最新价
vol      | string 		  | 成交量



