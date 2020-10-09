# Basic Information

## Asset Type And Precision


This interface returns all asset types and precisions


__HTTP Request__

* GET /api/v1/asset.list


```shell
curl  "https://api.hotbit.io/api/v1/asset.list"
```

__Returned Field__

Name of Field | Data Type | Description
--------- | ------------- | -------------
name 	  | string 		  | Token Type
prec      | int 		  | Number of Decimal Places Rounded	


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






## Retrieve The Timestamp of Current System

This interface returns the timestamp of current system.


```shell
curl  "https://api.hotbit.io/api/v1/server.time"
```


__HTTP Request__

* GET /api/v1/server.time


__Request Parameter__


This interface does not accept any parameter




> Response: 

```json
{
	"error": null,
	"id": 0,
	"result": 1585282798
}
```


## Latest Information Of Order Settlement

This interface returns the latest order settlement information of all transaction pairs retrieved


```shell
curl  "https://api.hotbit.io/api/v1/allticker"
```


__HTTP Request__

* GET /api/v1/server.time


__Request Parameter__


This interface does not accept any parameter





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

__Returned Fields__

Name of Field | Data Type | Description
--------- | ------------- | -------------
symbol 	  | string 		  | Name of Transaction Pair
buy      | string 		  | Buy One Price
sell      | string 		  | Sell One Price
open      | string 		  | Opening Price
close      | string 	  | Closing Price
high      | string 		  | Highest Price
low      | string 		  | Lowest Price
last      | string 		  | Latest Price
vol      | string 		  | Trading Volume



