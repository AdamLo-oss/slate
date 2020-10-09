# 交易数据

## 限价交易

__HTTP 请求__

* `POST /api/v1/order.put_limit`

__请求参数__

参数名称       | 是否必须        | 类型           |描述                                    | 取值范围
--------------| --------------| ---------------|---------------------------------------|----------------
api_key       |是              | string        |用户申请的API KEY                        |  -
sign          |是              | string        |请求字符串的签名值。                       | -
market        |是              | string        |market名称                              |，如："BTC/USDT","ETH/USDT"
side          |是              | Integer       |1 = "sell"，2="buy"                    | 0，1
amount        |是              | double        |代币符号数组                             | -
price         |是              | double        |交易价格。                               | -
isfee         |是              | Integer       |是否使用折扣币抵扣0 = "否(no)"，1="是(yes)"|0，1

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
 
__响应数据__

参数名称           | 是否必须          | 类型                  |  描述                 
---------         | -------         | ----                 |-----------------------
id                | 是              | Integer(无符号64位）   | order-ID
market            | 是              | string               | 交易对
source            | 是              | string               | 数据请求来源标识
type              | 是              | string               | 下单类型 1-限价单
side              | 是              | Integer               | 买卖方标识 1-卖方，2-买方
user              | 是              | Integer             | 买卖方标识 1-卖方，2-买方
ctime             | 是              | double               | #订单创建时间(秒)
mtime             | 是              | double               | #订单更新时间(秒)
price             | 是              | double               | 
amount            | 是              | double               | 
taker_fee         | 是              | double               | 
maker_fee         | 是              | double               | 
left              | 是              | double               | 
deal_stock        | 是              | double               | 
deal_money        | 是              | double               | 
deal_fee          | 是              | string               | 
status            | 是              | string               | #订单状态标志 当与0x8为真的时候表示当前订单是取消的,当与0x80为真的时候表示当前订单是使用抵扣折扣的
fee_stock         | 是              | string               | #抵扣币名
alt_fee           | 是              | double               | #抵扣币的折扣
deal_fee_alt      | 是              | double               | #折扣抵扣的数量




## 取消交易

__HTTP 请求__


* `POST /api/v1/order.cancel`

__请求参数__

参数名称       | 是否必须        | 类型                   |描述          | 取值范围
--------------| ---------------| ----------------------|-------------|---------
api_key       |是              | string                |用户API KEY   | -
sign          |是              | string                |用户签名值.    |   -
market        |是              | string                |market名称，   |"BTC/USDT","ETH/USDT"..
order_id      |是              | Integer(无符号64位)    |要取消交易的id. | -

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
 
__响应数据__

参数名称           | 是否必须          | 类型                  |  描述
---------         | -------         | ----                 |------
id                | 是              | Integer(无符号64位）   | order-ID
market            | 是              | string               | 交易对
source            | 是              | string               | 数据请求来源标识
type              | 是              | string               | 下单类型 1-限价单
side              | 是              | Integer               | 买卖方标识 1-卖方，2-买方
user              | 是              | Integer              | 买卖方标识 1-卖方，2-买方
ctime             | 是              | double               | #订单创建时间(秒)
mtime             | 是              | double               | #订单更新时间(秒)
price             | 是              | double               | 
amount            | 是              | double               | 
taker_fee         | 是              | double               | 
maker_fee         | 是              | double               | 
left              | 是              | double               | 
deal_stock        | 是              | double               | 
deal_money        | 是              | double               | 
deal_fee          | 是              | string               | 
status            | 是              | string               | #订单状态标志 当与0x8为真的时候表示当前订单是取消的,当与0x80为真的时候表示当前订单是使用抵扣折扣的
fee_stock         | 是              | string               | #抵扣币名
alt_fee           | 是              | double               | #抵扣币的折扣
deal_fee_alt      | 是              | double               | #折扣抵扣的数量





## 批量取消交易


__HTTP 请求__

* `POST /api/v1/order.batch_cancel`

__请求参数__

参数名称       | 是否必须        | 类型         |描述         | 取值范围
--------------| ---------------| -----------|-------------|-------------
api_key       |是              | string      |用户API KEY  | -
sign          |是              | string      |用户签名值    | - 
market        |是              | string      |market名称，  |"BTC/USDT","ETH/USDT"....
order_id      |是              | arrary      |要取消交易的id(无符号64位)|

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


__响应数据__


参数名称           | 是否必须          | 类型                  |  描述
---------         | -------         | ----                 |------
id                | 是              | Integer(无符号64位）   | order-ID
market            | 是              | string               | 交易对
source            | 是              | string               | 数据请求来源标识
type              | 是              | string               | 下单类型 1-限价单
side              | 是              | Integer               | 买卖方标识 1-卖方，2-买方
user              | 是              | Integer              | 买卖方标识 1-卖方，2-买方
ctime             | 是              | double               | #订单创建时间(秒)
mtime             | 是              | double               | #订单更新时间(秒)
price             | 是              | double               | 
amount            | 是              | double               | 
taker_fee         | 是              | double               | 
maker_fee         | 是              | double               | 
left              | 是              | double               | 
deal_stock        | 是              | double               | 
deal_money        | 是              | double               | 
deal_fee          | 是              | string               | 
status            | 是              | string               | #订单状态标志 当与0x8为真的时候表示当前订单是取消的,当与0x80为真的时候表示当前订单是使用抵扣折扣的
fee_stock         | 是              | string               | #抵扣币名
alt_fee           | 是              | double               | #抵扣币的折扣
deal_fee_alt      | 是              | double               | #折扣抵扣的数量


<aside class="notice">
     数量最多10个订单取消
</aside>




## 获取已成交的订单细节

__HTTP 请求__


* `POST /api/v1/order.deals`

__请求参数__

参数名称       | 是否必须        | 类型                       |描述
---------     | -------        | ----                      |------
api_key       |是              | string                    |用户API KEY
sign          |是              | string                    |用户签名值
offset        |是              | Integer(32位)             |等于0，表示从最近一次交易往之前查找
order_id      |是              | Integer(无符号64位)        |交易ID，参看 "order.put_limit"方法的返回结果
limit         |是              | Integer(32位)             |最多返回 "records"的数量  

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

__响应数据__

参数名称           | 是否必须          | 类型                  |  描述
---------         | -------         | ----                 |------
id                | 是              | Integer(无符号64位）   | order-ID
market            | 是              | string               | 交易对
source            | 是              | string               | 数据请求来源标识
type              | 是              | string               | 下单类型 1-限价单
side              | 是              | Integer               | 买卖方标识 1-卖方，2-买方
user              | 是              | Integer              | 买卖方标识 1-卖方，2-买方
ctime             | 是              | double               | #订单创建时间(秒)
mtime             | 是              | double               | #订单更新时间(秒)
price             | 是              | double               | 
amount            | 是              | double               | 
taker_fee         | 是              | double               | 
maker_fee         | 是              | double               | 
left              | 是              | double               | 
deal_stock        | 是              | double               | 
deal_money        | 是              | double               | 
deal_fee          | 是              | string               | 
status            | 是              | string               | #订单状态标志 当与0x8为真的时候表示当前订单是取消的,当与0x80为真的时候表示当前订单是使用抵扣折扣的
fee_stock         | 是              | string               | #抵扣币名
alt_fee           | 是              | double               | #抵扣币的折扣
deal_fee_alt      | 是              | double               | #折扣抵扣的数量



<!-- 





 -->

## 根据订单号查询已完成订单

__HTTP 请求__

* `POST /api/v1/order.finished_detail`


__请求参数__

参数名称       | 是否必须        | 类型                       |描述
---------     | -------        | ----                      |------
api_key       |是              | string                    |用户API KEY
sign          |是              | string                    |用户签名值
offset        |是              | Integer(32位)             |等于0，表示从最近一次交易往之前查找
order_id      |是              | Integer(无符号64位)        |交易ID

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

__响应数据__

参数名称           | 是否必须          | 类型                  |  描述
---------         | -------         | ----                 |------
id                | 是              | Integer(无符号64位）   | order-ID
market            | 是              | string               | 交易对
source            | 是              | string               | 数据请求来源标识
type              | 是              | string               | 下单类型 1-限价单
side              | 是              | Integer               | 买卖方标识 1-卖方，2-买方
user              | 是              | Integer              | 买卖方标识 1-卖方，2-买方
ctime             | 是              | double               | #订单创建时间(秒)
mtime             | 是              | double               | #订单更新时间(秒)
price             | 是              | double               | 
amount            | 是              | double               | 
taker_fee         | 是              | double               | 
maker_fee         | 是              | double               | 
left              | 是              | double               | 
deal_stock        | 是              | double               | 
deal_money        | 是              | double               | 
deal_fee          | 是              | string               | 
status            | 是              | string               | #订单状态标志 当与0x8为真的时候表示当前订单是取消的,当与0x80为真的时候表示当前订单是使用抵扣折扣的
fee_stock         | 是              | string               | #抵扣币名
alt_fee           | 是              | double               | #抵扣币的折扣
deal_fee_alt      | 是              | double               | #折扣抵扣的数量



<!-- 
  
 -->
## 获取交易列表

__HTTP 请求__

* `POST /api/v1/order.book`

__请求参数__

参数名称       | 是否必须        | 类型                       |描述
---------     | -------        | ----                      |------
market        |是              | string                    |market名称，如："BTC/USDT","BCC/USDT"
side          |是              | string                    |1 = "sell"，2="buy"
offset        |是              | Integer(32位)             |偏移位置
limit         |是              | Integer(无符号64位)        |最多返回 "records"的数量

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

__响应数据__

参数名称           | 是否必须          | 类型                  |  描述
---------         | -------         | ----                  |------
offset            | 是              | Integer(无符号64位）     |
limit             | 是              | Integer                |
offset            | 是              | Integer                |
total             | 是              | Integer(无符号64位)     |
orders            | 是              | array                  |

 <aside class="notice">
   offset — ，如果设置为0，表示从最新近一笔业务开始算起，往之前时间的所有交易记录，总笔数不能大于limit；。如果设置为1，表示从次新一笔业务开始算起，往之前时间的所有交易记录总笔数不能大于limit；以此类推.....
</aside>


<!-- 
  
 -->

## 获取交易深度

__HTTP 请求__

* `POST /api/v1/order.depth`

__请求参数__

参数名称       | 是否必须        | 类型                       |描述
---------     | -------        | ----                      |------
market        |是              | string                    |market名称，如："BTC/USDT","BCC/USDT"
interval      |是              | string                    |价格精度
limit         |是              | Integer(无符号64位)        |最多返回 "records"的数量

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

__响应数据__



<aside class="notice">
   interval — 可取值：0，0.1，0.01，0.001，……，0.0000000001
</aside>

<!-- 
  


 -->

## 查询未实施订单

__HTTP 请求__

* `POST /api/v1/order.pending`

__请求参数__

参数名称       | 是否必须        | 类型                       |描述
---------     | -------        | ----                      |------
api_key       |是              | string                    |用户API KEY
sign          |是              | string                    |用户签名值
market        |是              | string                    |market名称，如："BTC/USDT","BCC/USDT"
offset        |是              | Integer(32位)             |偏移位置
limit         |是              | Integer(无符号64位)        |最多返回 "records"的数量


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

__响应数据__

参数名称             | 是否必须          | 类型                  |  描述
---------          | -------         | ----                  |------
limit              | 是              | Integer(无符号64位）     |
offset             | 是              | Integer                |
total              | 是              | Integer(无符号64位)      |
records            | 是              | array                  |参考order.put_limit
<!-- 




 -->
## 查询用户的已完成订单

__HTTP 请求__

* `POST /api/v1/order.finished`

__请求参数__

参数名称       | 是否必须        | 类型                       |描述           |   取值范围
---------| --------| ---------------|---------------------|---------------|--------
api_key       |是              | string                    |用户API KEY    | -
sign          |是              | string                    |用户签名值      | -      
market        |是              | string                    |market名称，   |"BTC/USDT","BCC/USDT"...
start_time    |是              | 开始时间(秒)               |开始时间(秒).   |1525067600 时间戳
end_time      |是              | 截止时间(秒)               |结束时间(秒)。   |1525067600 时间戳
offset        |是              | Integer(无符号64位)        |偏移位置，如果设置为0，表示从最新近一笔业务开始算起，往之前时间的所有交易记录，总笔数不能大于limit；。如果设置为1，表示从次新一笔业务开始算起，往之前时间的所有交易记录总笔数不能大于limit；以此类推|0,1,2,3
limit         |是              | Integer(无符号64位)        |最多返回 "records"的数量|-
side          |是              | Integer                  |1 = "sell"，2="buy"|1,2


>Response:

```json
    "response": {
        "error": null,
        "id": 1393490,
        "result": []
    }
```

__响应数据__

参数名称             | 是否必须          | 类型                  |  描述
---------          | -------         | ----                  |------
records            | 是              | array                  |参考order.put_limit
<!-- 


