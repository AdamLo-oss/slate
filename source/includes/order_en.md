# Transaction Data

## Limit Order Transaction

__HTTP Request__

* `POST /api/v1/order.put_limit`

__Request Parameter__

Name of Parameter       | Required or Not        | Type           |Description
---------     | -------        | ----          |------
api_key       |Yes              | string        |The API KEY applied by the user
sign          |Yes              | string        |The signature value of the requested string
market        |Yes              | string        |market name，for example："BTC/USDT","ETH/USDT"
side          |Yes              | Integer       |1 = "sell"，2="buy"
amount        |Yes              | double        |array of token symbol
price         |Yes              | double        |Trading Price  
isfee         |Yes              | Integer       |apply the discount of discount tokens or not 0 = "No(no)"，1="Yes(yes)"

>Response:

```json
{
    "error": null,
    "result": 
   {
     "id":8688803,    
      "market":"ETHBTC",
      "source":"web",    
      "type":1,        
      "side":2,        
      "user":15731,
      "ctime":1526971722.164765, 
      "mtime":1526971722.164765, 
      "price":"0.080003",
      "amount":"0.4",
      "taker_fee":"0.0025",
      "maker_fee":"0",
      "left":"0.4",
      "deal_stock":"0",
      "deal_money":"0",
      "deal_fee":"0",
      "status":0    , 
      "fee_stock":"HTB",  
      "alt_fee":"0.5",  
      "deal_fee_alt":"0.123" 
        },
    "id": 1521169460
}
```
 
__Response Data__

Name of Parameter           | Required or Not          | Type                  |  Description
---------         | -------         | ----                 |------
id                | Yes              | Integer(No Symbol 64 Digit）   | order-ID
market            | Yes              | string               | Transaction Pair
source            | Yes              | string               | The identifier of data request source  
type              | Yes              | string               | Order placement type 1-limit order
side              | Yes              | string               | Identifier of buyer and seller 1-seller, 2-buyer
user              | Yes              | Integer(No Symbol 64 Digit）   | Identifier of buyer and seller 1-buyer，2-seller
ctime             | Yes              | double               | #Time of order creation(second)
mtime             | Yes              | double               | #Time of order update(second)
price             | Yes              | double               | 
amount            | Yes              | string               | 
taker_fee         | Yes              | string               | 
maker_fee         | Yes              | string               | 
left              | Yes              | string               | 
deal_stock        | Yes              | string               | 
deal_money        | Yes              | string               | 
deal_fee          | Yes              | string               | 
status            | Yes              | string               | #Identifier of order status   When true with 0x8, it means the current order is cancelled, when true with 0x80, it means the current order enjoys the discount.
fee_stock         | Yes              | string               | #Name of Discount Token
alt_fee           | Yes              | string               | #The discount of discount token
deal_fee_alt      | Yes              | string               | #Volume deducted from the discount




## Cancel Transaction

__HTTP Request__


* `POST /api/v1/order.cancel`

__Request Parameter__

Name of Parameter       | Required or Not        | Type                       |Description
---------     | -------        | ----                      |------
api_key       |Yes              | string                    |User's API KEY
sign          |Yes              | string                    |User's signature value
market        |Yes              | string                    |market name，for example："BTC/USDT","ETH/USDT"
order_id      |Yes              | Integer(No Symbol 64 Digit)        |id that requires the cancellation of transaction

>Response:

```json
{
    "error": null,
    "result": 
   {
     "id":8688803,    
      "market":"ETHBTC",
      "source":"web",    
      "type":1,        
      "side":2,        
      "user":15731,
      "ctime":1526971722.164765, 
      "mtime":1526971722.164765, 
      "price":"0.080003",
      "amount":"0.4",
      "taker_fee":"0.0025",
      "maker_fee":"0",
      "left":"0.4",
      "deal_stock":"0",
      "deal_money":"0",
      "deal_fee":"0",
      "status":0    , 
      "fee_stock":"HTB",  
      "alt_fee":"0.5",  
      "deal_fee_alt":"0.123" 
    },
    "id": 1521169460
}
```
 
__Response Data__

Name of Parameter           | Required or Not          | Type                  |  Description
---------         | -------         | ----                 |------
id                | Yes              | Integer(No Symbol 64 Digit）   | order-ID
market            | Yes              | string               | Transaction Pair
source            | Yes              | string               | Identifier on source of data request
type              | Yes              | string               | Order placement type 1-limit order
side              | Yes              | string               | Identifier of buyer and seller 1-Seller，2-Buyer
user              | Yes              | Integer(No Symbol 64 Digit）   | Identifier of buyer and seller 1-Seller，2-Buyer
ctime             | Yes              | double               | #Time of order creation(second)
mtime             | Yes              | double               | #Time of order update(second)
price             | Yes              | double               | 
amount            | Yes              | string               | 
taker_fee         | Yes              | string               | 
maker_fee         | Yes              | string               | 
left              | Yes              | string               | 
deal_stock        | Yes              | string               | 
deal_money        | Yes              | string               | 
deal_fee          | Yes              | string               | 
status            | Yes              | string               | #Identifier of order status When true with 0x8, it means the current order is cancelled, when true with 0x80, it means the current order enjoys discount.
fee_stock         | Yes              | string               | #Name of Discount Token
alt_fee           | Yes              | string               | #Discount Applied to the Discount Token
deal_fee_alt      | Yes              | string               | #he Volume Deducted as Discount





## Batch Cancellation of Orders


__HTTP Request__

* `POST /api/v1/order.batch_cancel`

__Request Parameter__

Name of Parameter       | Required or Not        | Type                       |Description
---------     | -------        | ----                      |------
api_key       |Yes              | string                    |User's API KEY
sign          |Yes              | string                    |User's Signature Value
market        |Yes              | string                    |market name，for example："BTC/USDT","ETH/USDT"
order_id      |Yes              | Integer(No Symbol 64 Digit)        |The id that requires the cancellation of orders (No Symbol 64 Digit)

>Response:

```json
{
    "error": null,
    "result": 
   [
        {
          "id":8688803,    
          "market":"ETHBTC",
          "source":"web",    
          "type":1,        
          "side":2,        
          "user":15731,
          "ctime":1526971722.164765, 
          "mtime":1526971722.164765, 
          "price":"0.080003",
          "amount":"0.4",
          "taker_fee":"0.0025",
          "maker_fee":"0",
          "left":"0.4",
          "deal_stock":"0",
          "deal_money":"0",
          "deal_fee":"0",
          "status":0    , 
          "fee_stock":"HTB",  
          "alt_fee":"0.5",  
           "deal_fee_alt":"0.123" 
        }
   ],
    "id": 1521169460
}
```


__Response Data__


Name of Parameter           | Required or Not          | Type                  |  Description
---------         | -------         | ----                 |------
id                | Yes              | Integer(No Symbol 64 Digit）   | order-ID
market            | Yes              | string               | Transaction Pair
source            | Yes              | string               | Identifier on source of data request
type              | Yes              | string               | Order placement type 1-limit order
side              | Yes              | string               | Identifier of buyer and seller 1-seller，2-buyer
user              | Yes              | Integer(No Symbol 64 Digit）   | Identifier of buyer and seller 1-seller，2-buyer
ctime             | Yes              | double               | #Time of order creation(second)
mtime             | Yes              | double               | #Time of order update(second)
price             | Yes              | double               | 
amount            | Yes              | string               | 
taker_fee         | Yes              | string               | 
maker_fee         | Yes              | string               | 
left              | Yes              | string               | 
deal_stock        | Yes              | string               | 
deal_money        | Yes              | string               | 
deal_fee          | Yes              | string               | 
status            | Yes              | string               | #Identifier of order status When true with 0x8, it means the current order is cancelled, when true with 0x80, it means the current order enjoys discount.
fee_stock         | Yes              | string               | #Name of Discount Token
alt_fee           | Yes              | string               | #The discount applied to the discount token
deal_fee_alt      | Yes              | string               | #The volume deducted as discount
<aside class="notice">
     Only a maximum of 10 orders are allowed to be cancelled
</aside>




## Retrieve The Details of Settled Orders

__HTTP Request__


* `POST /api/v1/order.deals`

__Request Parameter__

Name of Parameter       | Required or Not        | Type                       |Description
---------     | -------        | ----                      |------
api_key       |Yes              | string                    |User's API KEY
sign          |Yes              | string                    |User's Signature Value
offset        |Yes              | Integer(32 Digit)             |Equals to 0, which means search from the latest transaction to previous transactions.
order_id      |Yes              | Integer(No Symbol 64 Digit)        |Transaction ID，refer to the returned result of "order.put_limit" method
limit         |Yes              | Integer(32 Digit)             |The maximum volume of "records" allowed to be returned

>Response:

```json
{
    "error": null,
    "result": 
   [
        {
          "id":8688803,    
          "market":"ETHBTC",
          "source":"web",    
          "type":1,        
          "side":2,        
          "user":15731,
          "ctime":1526971722.164765, 
          "mtime":1526971722.164765, 
          "price":"0.080003",
          "amount":"0.4",
          "taker_fee":"0.0025",
          "maker_fee":"0",
          "left":"0.4",
          "deal_stock":"0",
          "deal_money":"0",
          "deal_fee":"0",
          "status":0    , 
          "fee_stock":"HTB",  
          "alt_fee":"0.5",  
           "deal_fee_alt":"0.123" 
        }
   ],
    "id": 1521169460
}
```

__Response Data__

Name of Parameter           | Required or Not          | Type                  |  Description
---------         | -------         | ----                 |------
id                | Yes              | Integer(No Symbol 64 Digit）   | order-ID
market            | Yes              | string               | Transaction Pair
source            | Yes              | string               | Identifier on source of data request
type              | Yes              | string               | Order placement type 1-limit order
side              | Yes              | string               | Identifier on buyer and seller 1-seller，2-buyer
user              | Yes              | Integer(No Symbol 64 Digit）   | Identifier on buyer or seller 1-seller，2-buyer
ctime             | Yes              | double               | #Time of order creation(second)
mtime             | Yes              | double               | #Time of order update(second)
price             | Yes              | double               | 
amount            | Yes              | string               | 
taker_fee         | Yes              | string               | 
maker_fee         | Yes              | string               | 
left              | Yes              | string               | 
deal_stock        | Yes              | string               | 
deal_money        | Yes              | string               | 
deal_fee          | Yes              | string               | 
status            | Yes              | string               | #Identifier of order status When true with 0x8, it means the current order is cancelled, when true with 0x80, it means the current order enjoys discount.
fee_stock         | Yes              | string               | #Name of discount token
alt_fee           | Yes              | string               | #The discount applied to the discount token
deal_fee_alt      | Yes              | string               | #The volume deducted as discount

<!-- 





 -->

## Inquiry On Settled Orders According To Order Number

__HTTP Request__

* `POST /api/v1/order.finished_detail`


__Request Parameter__

Name of Parameter       | Required or Not        | Type                       |Description
---------     | -------        | ----                      |------
api_key       |Yes              | string                    |User's API KEY
sign          |Yes              | string                    |User's Signature Value
offset        |Yes              | Integer(32 Digit)             |Equals to 0, which means search from the latest transaction to previous transactions
order_id      |Yes              | Integer(No Symbol 64 Digit)        |Transaction ID

>Response:

```json
{
    "error": null,
    "result": 
   [
        {
          "id":8688803,    
          "market":"ETHBTC",
          "source":"web",    
          "type":1,        
          "side":2,        
          "user":15731,
          "ctime":1526971722.164765, 
          "mtime":1526971722.164765, 
          "price":"0.080003",
          "amount":"0.4",
          "taker_fee":"0.0025",
          "maker_fee":"0",
          "left":"0.4",
          "deal_stock":"0",
          "deal_money":"0",
          "deal_fee":"0",
          "status":0    , 
          "fee_stock":"HTB",  
          "alt_fee":"0.5",  
           "deal_fee_alt":"0.123" 
        }
   ],
    "id": 1521169460
}
```

__Response Data__

Name of Parameter           | Required or Not          | Type                  |  Description
---------         | -------         | ----                 |------
id                | Yes              | Integer(No Symbol 64 Digit）   | order-ID
market            | Yes              | string               | Transaction Pair
source            | Yes              | string               | The identifier on the source of data request
type              | Yes              | string               | Order placement type 1-limit order
side              | Yes              | string               | Identifier of buyer and seller 1-seller，2-buyer
user              | Yes              | Integer(No Symbol 64 Digit）   | Identifier of buyer and seller 1-seller，2-buyer
ctime             | Yes              | double               | #Time of order creation(second)
mtime             | Yes              | double               | #Time of order update(second)
price             | Yes              | double               | 
amount            | Yes              | string               | 
taker_fee         | Yes              | string               | 
maker_fee         | Yes              | string               | 
left              | Yes              | string               | 
deal_stock        | Yes              | string               | 
deal_money        | Yes              | string               | 
deal_fee          | Yes              | string               | 
status            | Yes              | string               | #Identifier of order status When true with 0x8, it means the current order is cancelled, when true with 0x80, it means the current order enjoys discount.
fee_stock         | Yes              | string               | #Name of Discount Token
alt_fee           | Yes              | string               | #The discount applied to the discount token
deal_fee_alt      | Yes              | string               | #Volume deducted as discount

<!-- 
  
 -->
## Retrieve List of Transactions

__HTTP Request__

* `POST /api/v1/order.book`

__Request Parameter__

Name of Parameter       | Required or Not        | Type                       |Description
---------     | -------        | ----                      |------
market        |Yes              | string                    |market name，for example："BTC/USDT","BCC/USDT"
side          |Yes              | string                    |1 = "sell"，2="buy"
offset        |Yes              | Integer(32 Digit)             |Offset Position
limit         |Yes              | Integer(No Symbol 64 Digit)        |The maximum number of "records" to be returned

>Response:

```json
{
    "error": null,
    "result": {
        "offset": 0,
        "limit": 10,
        "total": 0,
        "orders": []
    },
    "id": 1521169117
}
```

__Response Data__

Name of Parameter           | Required or Not          | Type                  |  Description
---------         | -------         | ----                  |------
offset            | Yes              | Integer(No Symbol 64 Digit）     |
limit             | Yes              | Integer                |
offset            | Yes              | Integer                |
total             | Yes              | Integer(No Symbol 64 Digit)     |
orders            | Yes              | array                  |

 <aside class="notice">
   offset — ，if set as 0，it means the total number of all transaction records starting from the latest transaction to the earliest transaction cannot be greater than limit;.if set as 1，it means the total number of all transaction records from the second latest transaction to the earliest transaction cannot be greater than limit;and so on.....
</aside>


<!-- 
  
 -->

## Retrieve Trading Depth

__HTTP Request__

* `POST /api/v1/order.depth`

__Request Parameter__

Name of Parameter       | Required or Not        | Type                       |Description
---------     | -------        | ----                      |------
market        |Yes              | string                    |market name，for example："BTC/USDT","BCC/USDT"
interval      |Yes              | string                    |Price Precision
limit         |Yes              | Integer(No Symbol 64 Digit)        |The maximum number of "records" to be returned

>Response:

```json
{
  "error": null, 
  "result": 
    {
      "asks": [["0.0733858", "0.319"], ["0.0741178", "0.252"], ["0.0742609", "0.03"], ... ["0.1250465", "0.272"]], 
      "bids": [["0.0730197", "0.275"], ["0.0723", "1.052"], ["0.0722876", "0.302"], ... ["2.0e-7", "1"]]}, 
  "id": 1527559250
}
```

__Response Data__



<aside class="notice">
   interval — possible value：0，0.1，0.01，0.001，……，0.0000000001
</aside>

<!-- 
  


 -->

## Inquiry On Unexecuted Orders

__HTTP Request__

* `POST /api/v1/order.pending`

__Request Parameter__

Name of Parameter       | Required or Not        | Type                       |Description
---------     | -------        | ----                      |------
api_key       |Yes              | string                    |User's API KEY
sign          |Yes              | string                    |User's Signature Value
market        |Yes              | string                    |market name，for example："BTC/USDT","BCC/USDT"
offset        |Yes              | Integer(32 Digit)             |Offset Position
limit         |Yes              | Integer(No Symbol 64 Digit)        |Maximum number of "records" to be returned


>Response:

```json
{
    "error":null,
    "result":{
        "ETHBTC":{
            "limit":50,
            "offset":0,
            "total":1,
            "records":[
                {
                    "id":8688803,    
                    "market":"ETHBTC",
                    "source":"web",    
                    "type":1,        
                    "side":2,        
                    "user":15731,
                    "ctime":1526971722.164765, 
                    "mtime":1526971722.164765, 
                    "price":"0.080003",
                    "amount":"0.4",
                    "taker_fee":"0.0025",
                    "maker_fee":"0",
                    "left":"0.4",
                    "deal_stock":"0",
                    "deal_money":"0",
                    "deal_fee":"0",
                    "status":0    , 
                    "fee_stock":"HTB",  
                    "alt_fee":"0.5",  
                    "deal_fee_alt":"0.123" 
                }
            ]
        }
    },
    "id":1526971756
}
```

__Response Data__

Name of Parameter             | Required or Not          | Type                  |  Description
---------          | -------         | ----                  |------
limit              | Yes              | Integer(No Symbol 64 Digit）     |
offset             | Yes              | Integer                |
total              | Yes              | Integer(No Symbol 64 Digit)      |
records            | Yes              | array                  |Refer to order.put_limit
<!-- 




 -->
## Inquiry On Users' Settled Orders

__HTTP Request__

* `POST /api/v1/order.finished`

__Request Parameter__

Name of Parameter       | Required or Not        | Type                       |Description
---------     | -------        | ----                      |------
api_key       |Yes              | string                    |User's API KEY
sign          |Yes              | string                    |User's Signature Value
market        |Yes              | string                    |market name，for example："BTC/USDT","BCC/USDT"
start_time    |Yes              | Starting Time(second)               |Starting Time(second)
end_time      |Yes              | Ending Time(second)               |The maximum number of "records" to be returned
offset        |Yes              | Integer(No Symbol 64 Digit)        |Offset Position
limit         |Yes              | Integer(No Symbol 64 Digit)        |Maximum number of "records" to be returned
side          |Yes              | Integer                  |1 = "sell"，2="buy"


>Response:

```json
    "response": {
        "error": null,
        "id": 1393490,
        "result": []
    }
```

__Response Data__

Name of Parameter             | Required or Not          | Type                  |  Description
---------          | -------         | ----                  |------




