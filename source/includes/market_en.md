# Market Data

## Retrieve The List Of Transaction Pairs

__HTTP Request__

* `GET /api/v1/market.list`

__Request Parameter__

The interface does not accept any parameter.

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

__Response Data__

Name of Parameter             | Required Or Not          | Type                  |  Description
---------           | -------         | ----                  |------
name                | Yes              | string                | Transaction Pair
stock               | Yes              | string                | Token Type Traded
money                | Yes              | string               | Token Type Used
fee_prec                | Yes              | dobule               | Decimal precision set as 4 digits
stock_prec                | Yes              | dobule               | stock precision
money_prec                | Yes              | dobule               | money precision
min_amount                | Yes              | dobule               | Minimum value required for order placement


## Retrieve The Latest Price Of Designated Transaction Pairs

__HTTP Request__

* `POST /api/v1/market.last`

__Request Parameter__

Name of Parameter       | Required Or Not        | Type           |Description
---------     | -------        | ----          |------
market       |Yes              | string        |market Type，For example："BTC/USDT","BCC/USDT"



>Response:

```json
{
    "error": null,
    "result": "0.07413600",
    "id": 1521169525
}
```

__Response Data__


Parameter Name             | Required Or Not          | Type                  |  Description
---------          | -------         | ----                  |------
result              | Yes               |dobule               | Price



## Inquiry On The Trading Records Of Transaction Pairs


__HTTP _Request_

* `POST /api/v1/market.deals`

__Request Parameter__


Name of Parameter         | Required or Not        | Type                   |Description
---------      | -------        | ----                  |------
market         |Yes              | string                 |market Type，For example："BTC/USDT","BCC/USDT"
limit          |Yes              | Integer                |Limit on number of inquiries(limit <= 1000)
last_id        |Yes              | Integer(No Symbol 64 Digit)      |Return trading data greater than order_id > last_id

>Response:

```json
{
    "error": null,
    "result": [],
    "id": 1521169562
}
```

__Response Data__


Name of Parameter             | Required or Not          | Type                  |  Description
---------          | -------         | ----                  |------
result              | Yes              |                       | Record




## Inquiry On User's Trading Records

__HTTP Request__

* `POST /api/v1/market.user_deals`

__Request Parameter__

Name of Parameter         | Required or Not        | Type                   |Description
---------      | -------        | ----                  |------
api_key         |Yes              | string                 |User's API KEY
sign          |Yes              | Integer                |User's Signature Value
market        |Yes              | Integer(No Symbol 64 Digit)      |Return market name，for example："BTC/USDT","BCC/USDT"
offset        |Yes              | Integer(No symbol 64 Digit)      |Offset Position
limit        |Yes              | Integer(No Symbol 64 Digit)      |Check limit on number


<aside class="notice">
   offset — if set as 0, it means all transaction records starting from the latest order to the earliest order, the total number of all orders cannot be greater than limit; if set as 1, it means all transaction records that meet the condition from the second latest order to the earliest order, the total number of all orders cannot be greater than limit; and so on.....
</aside>

<aside class="notice">
   limit — limit <= 1000
</aside>


>Response:

```json
{

}
```
__Response Data__

Name of Parameter             | Required or Not          | Type                  |  Description
---------          | -------         | ----                  |------
result              | Yes              |                       | Record



## k Chart Inquiry

__HTTP Request__

* `GET /api/v1/market.kline`

__Request Parameter__

Name of Parameter         | Required or Not        | Type                   |Description
---------      | -------        | ----                  |------
market         |Yes              | string                 |market name，for example："BTC/USDT","BCC/USDT"
start_time          |Yes              | Integer(No Symbol 64 Digit)                |Starting Time Stamp(Second)
end_time        |Yes              | Integer(No Symbol 64 Digit)      |Ending Time Stamp(Second)
interval        |Yes              | 	Integer(32 Digit)     |Interval Period,unit second, (Starting time to ending time，total number of periods) 

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
__Response Data__

Name of Parameter             | Required or Not          | Type                  |  Description
---------          | -------         | ----                  |------
Array0             |  Yes             | Integer(No Symbol 64 Digit)     | Time Stamp     
Array1             |  Yes             | double                | Opening Price     
Array2             |  Yes             | double                | Closing Price     
Array3             |  Yes             | double                | Highest Price     
Array4             |  Yes             | double                | Lowest Price     
Array5             |  Yes             | double                | Range of Increase     
Array6             |  Yes             | double                | Trading Volume     
Array7             |  Yes             | string                | Market Name     
<!-- 


 -->


## Retrieve various status such as the range of increase or decrease, trading volume, maximum / lowest price of the market within any designated period of time in the past etc.

__HTTP Request__

* `GET /api/v1/market.status`

__Request Parameter__

Name of Parameter         | Required or Not        | Type                   |Description
---------      | -------        | ----                  |------
market         |Yes              | string                 |market Name，for example："BTC/USDT","BCC/USDT"
period          |Yes              | Integer(32 Digit)          |Duration inquired, with second as unit, which means anytime starting from now to the past, for example: 86400 means the past 24 hours.


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
__Response Data__

Name of Parameter             | Required or Not          | Type                  |  Description
---------          | -------         | ----                  |------
period    | Yes |Integer|Duration inquired
last    | Yes |double|Latest Price
open    | Yes |Integer|Opening Price
close    | Yes |Integer|Closing Price
high    | Yes |Integer|Highest Price
low    | Yes |Integer|Lowest Price
volume    | Yes |Integer|Range of Increase
deal    | Yes |Integer|Trading Volume




## Retrieve the market status of the current day


__HTTP Request__

* `GET /api/v1/market.status_today`

__Request Parameter__

Name of Parameter         | Required or Not        | Type                   |Description
---------      | -------        | ----                  |------
market         |Yes              | string                 |market name，for example："BTC/USDT","BCC/USDT"

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
__Response Data__

Name of Parameter             | Required or Not          | Type                  |  Description
---------          | -------         | ----                  |------
last    | Yes |double|Latest price
open    | Yes |Integer|Opening Price
close    | Yes |Integer|Closing Price
high    | Yes |Integer|Highest Price
low    | Yes |Integer|Lowest Price
volume    | Yes |Integer|Range of Increase
deal    | Yes |Integer|Trading Volume




## Retrieve the market status of the current day

__HTTP Request__

* `GET /api/v1/market.status24h`

__Request Parameter__

This interface does not accept any parameter.

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

__Response Data__

Name of Parameter             | Required or Not          | Type                  |  Description
---------          | -------         | ----                  |------
period  | Yes |double|Cycle
last    | Yes |double|Latest Price
open    | Yes |Integer|Opening Price
close    | Yes |Integer|Closing Price
high    | Yes |Integer|Highest Price
low    | Yes |Integer|Lowest Price
volume    | Yes |Integer|Range of Increase
deal    | Yes |Integer|Trading Volume




## market Introduction	

__HTTP Request__

* `GET /api/v1/market.summary`

__Request Parameter__

Name of Parameter       | Required or Not        | Type           |Description
---------     | -------        | ----          |------
markets       |Yes              | json array        |market name json array，for example：["BTCUSD","BCCUSD"]，if blank array:[],return all market。

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

__Response Data__

Name of Parameter             | Required or Not          | Type                  |  Description
---------          | ---------         | ---------            |      ---------