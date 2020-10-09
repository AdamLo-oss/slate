# Access Instruction

## Brief Introduction of Interface

Type of Interface	| Link To Different Types of Interface | Introduction
-------- | ------------- | ------------- 
System Type | /api/v1/server.time | Basic Types of Interface
Order Type | /api/v1/order.* | Order type of interface, which include order placement, order cancellation, order inquiry and order settlement etc. 
Market Type | /api/v1/market.* | Public market type of interface, which include market settlement, market depth, market trends etc.
Asset Type | /api/v1/balance.* | Asset type of interface, which include records of changes in asset volumes and user assets.

This category only follows a general rules of classification. Please be aware that part of the interfaces do not follow this category. Please check relevant interface files according to actual situations and requirements.

## Rules And Regulations Regarding The Limit On The Frequencies Of Interface Call

* The system only allows each API Key to conduct no more than 10 interface calls within each second.
* If the interface does not require API Ley, then each IP address is allowed to conduct no more than 10 interface calls within each second.

For Example:

* According to the limit on the frequencies of interface call, asset or order type of interfaces are only allowed to conduct no more than 10 times of interface calls within each second.
* According to the limit on the frequencies of interface call, each IP address is allowed to conduct no more than 10 interface calls within each second.

## Request Format

All API requests are restful，currently, there are only two formats：GET and POST

* GET Request：All parameters are included in the path parameter.
* POST Request，All parameters are sent in the request body in JSON format.


## Return Format

The format of all interfaces are in JSON format. There are three fields on the upmost layer of JSON: error, result, id， with the actual data of business included in "result" field.

Please refer to the example of return format below：

Name of Parameter	| Data Type | Description
-------- | ------------- | ------------- 
error  | Object | API returned incorrect content，when API returns correct content, it displayed as "null"
result | Object | The interface returned data body,when the result is incorrect, it displayed as "null"
id     | int    | Request id 


## Error Information

###  API Error Information

Error Code	| Description
-------- | ------------- 
invalid argument  | Incorrect Parameter



## Recommendations

1、For data information of market type, it is recommended to use WebSocket to receive real time data and conduct cache operation on data received.

2、For retrieving latest market price, it is recommended to use /market/trade interface or subscribe market.$symbol.trade.detail by using WebSocket.
3、For the push of order settlement, it is recommended to use the theme of orders.$symbol.update, as the theme is strictly time-ordered with lower level of delay.
4、For asset information of orders placed, please use WebSocket to subscribe the theme of accounts and regularly request asset data for update via Rest interface.

