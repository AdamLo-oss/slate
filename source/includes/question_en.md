# Frequently Asked Questions

## Relevant Information Regarding Connection and Verification of Signature

__Q1：How many API keys can each user apply for?__

A: Each user may create 5 groups of API key, and each API key may correspond to the settings of three permissions, namely reading, trading and withdrawal.

Please refer to the detailed information of the three permissions below：

* Reading permission：Read permission applies to the inquiry interface of data, such as order inquiry and order settlement inquiry etc. 
* Trading Permission：Trading permission applies to the interfaces of order placement, order withdrawal and transfer.
* Withdrawal Permission：Withdrawal permission applies to the creation of withdrawal orders and cancellation of withdrawal orders.

__Q2：Why do I often experience server offline and timeout?__

A：Please check if your experience can be attributed to the following situations:

1. If the client end server is located in mainland China, the stability of connection is hard to be guaranteed. It is recommended to use the AWS cloud server located in Singapore instead. 
2. It is recommended to use the domain name of api.hotbit.io or api.hotbitcn.com. All other domain names are not recommended.

__Q3：Why WebSocket has always been disconnected?__

A：The common causes of the problem include:

1. No Pong has been responded, the connection of WebSocket requires the response of Pong after receiving the Ping information sent by the server end for the stability of connection.

2. Due to certain network connection problems, the server end has not received the Pong information sent from the client end

3. The disconnection was caused by ceertain network problems.

4. It is recommended that users should set up reconnection mechanism for the disconnection problem of WebSocket, so that the program will automatically conduct reconnection in case that any unexpected disconnection occurs after the heartbeat (Ping/Pong) information is responded correctly.

__Q4：Why the return of signature verification always fails?__

A：Please distinguish the difference between the string without using the signature of Secret Key and the string below

`POST\n`

`api.hotbit.io\n`

`/api/v1/balance.query\n`

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]`

Please pay attention to the information listed below:

1、The parameter of the signature should be based on the order of ASCII code, for example, the original parameter is listed as below:

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6`

`assets=["BTC","ETH"]`


After sorting, the parameter should be:

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6`

`assets=["BTC","ETH"]`

2、The signature is required to be converted to capitalized form after conducting MD5 computation

3、The request parameter of POST should be included in the signature string.

4、Check whether the time of your computer deviates from the standard time of your area (the deviation should be less than 1 minute)

5、When sending the information of signature verification by WebSocket, the message body does not require URL coding.

6、The Host included by the time of signature should be the same as the Host of interface request.

7、Check if the API Key and Secret Key involve any hidden special characters that may affect the signature

## Information Relevant To Market Trend


__Q1：Is it possible that the trading volume reflected by the data interface of 24-hour market interface (/market.status24h) will grow negatively?__ 

A：The trading volume and trading value reflected by /market.status24h interface are constantly updated 24-hour data (calculated in every 24 hours), which means it is possible that the accumulated trading volume and trading value of the next 24-hour will be less than the trading volume and trading value of the previous 24-hour.


__Q2：How to Retrieve The Latest Final Price?__

A：It is recommended to use REST API GET /allticker interface to request the latest final price, or to use WebSocket to subscribe to the theme of deals.update and retrieve the latest final price according to the price included in the returned data.

__Q3：When Does The Calculation of K Chart Begin?__

A： The calculation period of K Chart is based on Singapore time. For example, the calculation of daily K Chart starts from Singapore time 00:00 and ends at 00:00 of the next day.

## Trading Related Information

__Q1：How to Retrieve The Information Regarding The Number, Value, Limit on Decimal Places and Precision of Orders Placed__

A： You may use Rest API GET /api/v1/asset.list to retrieve information on relevant transaction pair. By placing orders, please pay attention to the difference between minimum volume of order placement allowed and minimum value of order placement allowed. 