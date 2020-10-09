# Quick Start

## Connection Prerequisites

If you intend to use API, please login to web end and finish the application and permission setting of API key first, then start developing and trading based on the detail of this file.

You may click [here](https://www.hotbit.pro/) to create API Key。

After successfully creating the API key, please do remember the following information：

* `Access Key` The encrypted key that allows you to gain access to your API

* `Secret Key` The encrypted key used by the encryption process of signature verification (only visible during application process)


<aside class="notice">
When creating API key, you may bind your IP address. For security concerns, it is strongly recommended that you bind your IP address when creating your API key.
</aside>


<aside class="warning">
Risk Warning：These two encrypted keys are closely related to the security of your account. Please do NOT disclose these two encrypted keys to anyone else at the same time. The leak of your API key may result in the loss of your assets (even if your withdrawal permission still remains unavailable). If you found that your API key has been leaked, please delete all relevant API key as soon as possible.
</aside>



Interface | Description
--------- | ------------- 
[GET /api/v1/server.time]()| Retrieve System Time
[POST /api/v1/balance.query]() | Retrieve User Asset
[GET /api/v1/asset.list]() | Retrieve all available asset types and asset precision, prec means the number of decimal places
[POST /api/v1/order.put_limit]() | Limit Order
[POST /api/v1/order.cancel]() | Cancel Order
[POST /api/v1/order.batch_cancel]() | Cancel Orders in Large Quantities
[POST /api/v1/order.deals]() | Retrieve Details of Settled Orders
[POST /api/v1/order.finished_detail]() | Inquiry on settled orders based on order numbers
[GET /api/v1/order.book ]() | Retrieve Trading List
[GET /api/v1/order.depth]() | Retrieve Trading Depth
[POST /api/v1/order.pending]() | Inquiry on Unexecuted Orders
[POST /api/v1/order.finished]() | Inquiry on User's Settled Orders
[GET /api/v1/market.list]() | Retrieve List of Transaction Pairs
[GET /api/v1/market.last]() | Retrieve The Latest Price of Designated Transaction Pair
[GET /api/v1/market.deals]() | Inquiry on Transaction Records of Transaction Pair
[GET /api/v1/market.user_deals]() | Inquiry on User's Trading Records
[GET /api/v1/market.kline]() | k chart inquiry
[GET /api/v1/market.status]() | Retrieve various real-time status of market within a designated period of time in the past, such as the latest range of increase or decrease, trading volume, maximum/minimum price etc.[GET /api/v1/market.status_today]() | Retrieve today's market status
[GET /api/v1/market.status24h]() | Retrieve various status of market within the past 24 hours, such as range of increase or decrease, trading volume, maximum/minimum price etc.
[GET /api/v1/market.summary]() | market summary
[GET /api/v1/allticker]() | Retrieve the latest information of all available transaction pairs


<aside class="notice">
Other interfaces unavailable，if attempt to visit，the system will return “error-code 403”。
</aside>

## Interface Type

Hotbit provides users with two types of interface, you may choose the appropriate method that suits your own application scenario or preference for the inquiry on market trend, trading or withdrawal.

### REST API

REST，which is the abbreviation of Representational State Transfer，is a type of communication mechanism based on HTTP that has gained comparatively more popularity recently. Each URL represents one type of resource.

It is recommended for developers to conduct one-off operations such as trading or withdrawals by using REST API.

### WebSocket API

WWebSocket is a new type of HTML5 protocol that realizes the full duplex communications between client end and server, which allows the connection between client end and server to be established through one simple handshake. The server may actively push information to client end based on business rules and regulations.

It is recommended for developers to use WebSocket API to retrieve information such as market trend and transaction depth etc.

__Verifications Regarding The Permission Of Interface__

Both of the above two types of interfaces include two types of interface, namely public interface and private interface.

Public interface can be used to retrieve basic information and market data. The public interface call can be conducted without verification.

Private interface can be used for the management of trading and account. Each private request must be verified through signature verification process by using your API key.

## Connect URLs

You may compare the latency status between api.hotbit.pro and ws.hotbit.pro and choose to use the one with lower level of latency.

__REST API__

__`https://api.hotbit.io/api/v2`__
__`https://api.hotbitcn.com/api/v2`__


__Websocket Feed__

__`wss://ws.hotbit.io/v2/`__ 
__`wss://ws.hotbitcn.com/v2/`__ 

<aside class="notice">
Please visit Hotbit API through any IP address outside of mainland China.
</aside>

<aside class="notice">
Due to the fact that proxy may leads to high latency and poor stability, it is not recommended to visit Hotbit API via proxy
</aside>

<aside class="notice">
In order to guarantee the stability of API service, it is recommended to visit Hotbit API via AWS cloud server located in Singapore. If users choose to visit Hotbit API through any client end server located in mainland China, the stability of the connection will not be guaranteed.
</aside>

## Signature Verification

### Signature Introduction

It is highly likely that the API request will be tampered during its transmission through the Internet. In order to ensure that your request will not be tampered, apart from public interface (basic information interface, market data interface), all private interface must conduct signature verification process by using your API key for the verification of parameters or parameter values to check if the parameters or parameter values have been tampered during their transmission or not.
In order to visit certain interface, each API key is required to obtain appropriate permission. Each newly-created API key requires permission distribution. Before using the interface, please check the permission type of each interface and make sure that your API key enjoy(s) relevant permission.

A legal request is composed of the following sections：

* Method Request Address：which refers to the address of access server api.huobi.pro，for example api.hotbit.io/api/v2/order/orders。
* API Access Id（AccessKeyId）：The Access Key included in the API Key that you applied.
* Signature Method（SignatureMethod）：The protocol based on md5 used for the process of calculation on user's signature, in this case, please apply md5.
* Signature Version（SignatureVersion）：The version of signature protocol, in this case please apply 2.
* Required and optional parameter：Each method includes a group of required parameters and optional parameters that are used for the definition of API call. You may check these parameters and their meanings in the description of each method.
* It is required to place the request parameter of POST in body.
* 	Signature：The value generated from signature computation is used to ensure the effectiveness of the signature and that the signature has not been tampered.

### Signature Process


Standardize the request that requires signature computation. Considering the fact that during signature computation, the results of computation by using different contents will be totally different, please do standardize the request before signature computation. Please refer to the example below that demonstrates the request regarding the inquiry on the details of the order:
The complete request URL regarding the inquiry on the details of the order

`https://api.hotbit.io/api/v2/balance.query?`

`api_key=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`&sign=C88F04701D3349D0A93A0164DC5A4CD9`

`&assets=["BTC","ETH"]`

#### 1. Conduct URL programming on parameter and conduct sorting on parameter based on ASCII order

For example, the original order of the request parameter is listed below

`api_key=6b97d781-xxxx-xxxx-576d96d0bbebc8c6`

`&assets=["BTC","ETH"]`


After sorting

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6`

`&assets=["BTC","ETH"]`

#### 2. Connect all parameters by "&" character according to the order above

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]`


#### 3. Splice parameter of private key and form the final string that requries signature computation as below. 

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]&secret_key=de8063ea6e99bc967ba6395d06fabf50`	

#### 4. Form the final string that requires signature computation as below

1. Use the request string and API private key generated from the previous step as two parameters, call MD5 value.

`MD5(api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]&secret_key=de8063ea6e99bc967ba6395d06fabf50)`	

2. Turn MD5 value into capitalized, and use the generated value as the digital signature of this interface call.
	

`C88F04701D3349D0A93A0164DC5A4CD9`

#### 5.Add the generated digital signature into the path parameter requested

1. Add all required verification parameter into the path parameter of interface call
2. Add digital signature into path parameter after URL code, parameter name "sign"

The final API request sent to the server should be

`POST\n`
`https://api.hotbit.io/api/v2/balance.query?api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]&sign=C88F04701D3349D0A93A0164DC5A4CD9`


## Business Dictionary

### Transaction Pair

Transaction pair is composed of base currency and quote currency. Take BTC/USDT transaction pair for example, BTC is the base currency, and USDT is the quote currency.

The corresponding field of base currency is base-currency 。

The corresponding field of quote currency is quote-currency 。


### Introduction on Relevant ID of Order and Order Settlement

* order-id : The only id for the order
* client-order-id : The user's customized ID, which is imported by order placement and corresponds with the order-id returned after the order has been placed successfully. This ID is valid within 24 hours.
* match-id : The order ID during its matching process
* trade-id : The only id for order settlement

### Order Type

Currently, Hotbit's order types are composed of business directions and type of order operation, for example: buy-market, buy is business direction and market is type of operation

Business Direction：

* buy : Buy
* sell: Sell

Order Type:

* type : 1=Limit Order
* side : 1-Seller，2-Buyer


### Order Status

* submitted : Waiting to be settled, the orders under this status have already entered the queue of matching process.
* partial-filled : Partly settled, the orders under this status are in the queue of matching process, with part of the order settled by the market already, and the remaining part of the order is waiting to be settled.
* filled : Settled. The orders under this status are not in the queue of matching process. The orders have all been settled by the market.
* partial-canceled : Part of the settled order cancelled. The order under this status is not in the queue of matching process, this status is transformed from partial-filled. The order is partly settled, but the settled part of the order has been cancelled.
* canceled : Canceled. The order under this status is not in the queue of matching orders. The order under this status does not have any settled quantity, and has been successfully canceled.
* canceling : Canceling. The order under this status is in the process of being canceled. Considering the fact that the order will only be completely canceled after it has been deleted from the queue of matching process, this status refers to the status of transition in between.


For further information, please visit [Hotbit](https://www.hotbit.io) for more details.











