# 快速入门

## 接入准备

如需使用API ，请先登录网页端，完成API key的申请和权限配置，再据此文档详情进行开发和交易。

您可以点击 [这里](https://www.hotbit.io) 创建 API Key。

每个用户可创建5组Api Key，每个Api Key可对应设置读取、交易两种权限。

权限说明如下：

* 读取权限：读取权限用于对数据的查询接口，例如：订单查询、成交查询等。
* 交易权限：交易权限用于下单、撤单、划转类接口。
~~* 提币权限：提币权限用于创建提币订单、取消提币订单操作。~~

创建成功后请务必记住以下信息：

* `Access Key` API 访问密钥

* `Secret Key` 签名认证加密所使用的密钥（仅申请时可见）


<aside class="notice">
创建 API Key 时可以绑定 IP 地址，**未绑定 IP 地址的 API Key 有效期为90天**。出于安全考虑，强烈建议您绑定 IP 地址。
</aside>


<aside class="warning">
风险提示：这两个密钥与账号安全紧密相关，无论何时都请勿将二者同时向其它人透露。API Key的泄露可能会造成您的资产损失（即使未开通提币权限），若发现API Key泄露请尽快删除该API Key。
</aside>

## SDK与代码示例

__SDK（推荐）__

[Java](https://github.com/hotbitex) | [Python3](https://github.com/hotbitex) | [Go](https://github.com/hotbitex)

__其它代码示例__

[https://github.com/hotbitex?tab=repositories](https://github.com/hotbitex?tab=repositories)



接口 | 说明
--------- | ------------- 
[GET /api/v1/server.time]()| 获取系统时间
[POST /api/v1/balance.query]() | 获取用户资产
[GET /api/v1/asset.list]() | 获取平台所有资产类型和精度，prec为精确到小数点后多少位
[POST /api/v1/order.put_limit]() | 限价交易
[POST /api/v1/order.cancel]() | 取消交易
[POST /api/v1/order.batch_cancel]() | 批量取消交易
[POST /api/v1/order.deals]() | 获取已成交的订单细节
[POST /api/v1/order.finished_detail]() | 根据订单号查询已完成订单
[GET /api/v1/order.book ]() | 获取交易列表
[GET /api/v1/order.depth]() | 获取交易深度
[POST /api/v1/order.pending]() | 查询未实施订单
[POST /api/v1/order.finished]() | 查询用户的已完成订单
[GET /api/v1/market.list]() | 获取交易对列表
[GET /api/v1/market.last]() | 获取指定交易对的最新价格
[GET /api/v1/market.deals]() | 查询交易对交易记录
[GET /api/v1/market.user_deals]() | 查询用户交易记录
[GET /api/v1/market.kline]() | k线查询
[GET /api/v1/market.status]() | 获取过去指定时间段market当前最新涨跌幅，交易量，最高/最低价格等状态
[GET /api/v1/market.status_today]() | 获取今天market状态
[GET /api/v1/market.status24h]() | 获取过去24小时内的market涨跌幅，交易量，最高/最低价格等状态
[GET /api/v1/market.summary]() | market概要
[GET /api/v1/allticker]() | 获取全市场交易对的最新成交信息


<aside class="notice">
其他接口不可访问，如果尝试访问，系统会返回 “error-code 403”。
</aside>

## 接口类型

火币为用户提供两种接口，您可根据自己的使用场景和偏好来选择适合的方式进行查询行情、交易或提币。

### REST API

REST，即Representational State Transfer的缩写，是目前较为流行的基于HTTP的一种通信机制，每一个URL代表一种资源。

交易或资产提币等一次性操作，建议开发者使用REST API进行操作。

### WebSocket API

WebSocket是HTML5一种新的协议（Protocol）。它实现了客户端与服务器全双工通信，通过一次简单的握手就可以建立客户端和服务器连接，服务器可以根据业务规则主动推送信息给客户端。

市场行情和买卖深度等信息，建议开发者使用WebSocket API进行获取。

__接口鉴权__

以上两种接口均包含公共接口和私有接口两种类型。

公共接口可用于获取基础信息和行情数据。公共接口无需认证即可调用。

私有接口可用于交易管理和账户管理。每个私有请求必须使用您的API Key进行签名验证。


## 接入URLs

您可以自行比较使用api.hotbit.pro和ws.hotbit.pro两个域名的延迟情况，选择延迟低的进行使用。

__REST API__

__`https://api.hotbit.pro`__


__Websocket Feed__

__`wss://ws.hotbit.pro/`__ 

<aside class="notice">
请使用中国大陆以外的 IP 访问 Hotbit API。
</aside>

<aside class="notice">
鉴于延迟高和稳定性差等原因，不建议通过代理的方式访问 Hotbit API。
</aside>

<aside class="notice">
为保证API服务的稳定性，建议使用新加坡AWS云服务器进行访问。如使用中国大陆境内的客户端服务器，连接的稳定性将难以保证。
</aside>


## 签名认证

### 签名说明

API 请求在通过 internet 传输的过程中极有可能被篡改，为了确保请求未被更改，除公共接口（基础信息，行情数据）外的私有接口均必须使用您的 API Key 做签名认证，以校验参数或参数值在传输途中是否发生了更改。
每一个API Key需要有适当的权限才能访问相应的接口，每个新创建的API Key都需要分配权限。在使用接口前，请查看每个接口的权限类型，并确认你的API Key有相应的权限。

一个合法的请求由以下几部分组成：

* 方法请求地址：即访问服务器地址 api.hotbit.io，比如 api.hotbit.io/v1/order/orders。
* API 访问Id（AccessKeyId）：您申请的 API Key 中的 Access Key。
* 签名方法（SignatureMethod）：用户计算签名的基于哈希的协议，此处使用 HmacSHA256。
* 签名版本（SignatureVersion）：签名协议的版本，此处使用2。
* 时间戳（Timestamp）：您发出请求的时间 (UTC 时间) 。如：2017-05-11T16:22:06。在查询请求中包含此值有助于防止第三方截取您的请求。
* 必选和可选参数：每个方法都有一组用于定义 API 调用的必需参数和可选参数。可以在每个方法的说明中查看这些参数及其含义。
	* 对于 GET 请求，每个方法自带的参数都需要进行签名运算。
	* 对于 POST 请求，每个方法自带的参数不进行签名认证，并且需要放在 body 中。
* 签名：签名计算得出的值，用于确保签名有效和未被篡改。	

### 签名步骤

规范要计算签名的请求 因为使用 HMAC 进行签名计算时，使用不同内容计算得到的结果会完全不同。所以在进行签名计算前，请先对请求进行规范化处理。下面以查询某订单详情请求为例进行说明：

查询某订单详情时完整的请求URL

`https://api.hotbit.pro/api/v1/balance.query?`

`api_key=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx`

`&sign=C88F04701D3349D0A93A0164DC5A4CD9`

`&assets=["BTC","ETH"]`

#### 1. 请求方法（GET 或 POST），后面添加换行符 “\n”

`POST\n`

#### 2. 添加小写的访问地址，后面添加换行符 “\n”

`api.hotbit.pro\n`

#### 3. 访问方法的路径，后面添加换行符 “\n”

`/api/v1/balance.query\n`

#### 4. 对参数进行URL编码，并且按照ASCII码顺序进行排序

例如，下面是请求参数的原始顺序，且进行URL编码后

`api_key=6b97d781-xxxx-xxxx-576d96d0bbebc8c6`

`&assets=["BTC","ETH"]`

<aside class="notice">
使用 UTF-8 编码，且进行了 URL 编码，十六进制字符必须大写，如 “:” 会被编码为 “%3A” ，空格被编码为 “%20”。
</aside>


经过排序之后

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6`

`&assets=["BTC","ETH"]`

#### 5. 按照以上顺序，将各参数使用字符 “&” 连接

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]`


#### 6. 拼接私钥参数，组成最终的要进行签名计算的字符串如下

`api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]&secret_key=de8063ea6e99bc967ba6395d06fabf50`	

#### 7. 组成最终的要进行签名计算的字符串如下

1. 将上一步得到的请求字符串和 API 私钥作为两个参数，调用MD5值。

`MD5(api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]&secret_key=de8063ea6e99bc967ba6395d06fabf50)`	

2. 将MD5值转为大写，得到的值作为此次接口调用的数字签名。
	

`C88F04701D3349D0A93A0164DC5A4CD9`

#### 8.将生成的数字签名加入到请求的路径参数里

1. 把所有必须的认证参数添加到接口调用的路径参数里
2. 把数字签名在URL编码后加入到路径参数里，参数名为“sign”。

最终，发送到服务器的 API 请求应该为

`POST\n`
`https://api.hotbit.pro/api/v1/balance.query?api_key=6b97d781-5ffd-958f-576d96d0bbebc8c6&assets=["BTC","ETH"]&sign=C88F04701D3349D0A93A0164DC5A4CD9`


## 业务字典

### 交易对

交易对由基础币种和报价币种组成。以交易对 BTC/USDT 为例，BTC 为基础币种，USDT 为报价币种。

基础币种对应字段为 base-currency 。

报价币种对应字段为 quote-currency 。


### 订单、成交相关ID说明

* order-id : 订单的唯一编号
* client-order-id : 客户自定义ID，该ID在下单时传入，与下单成功后返回的order-id对应，该ID 24小时内有效。
* match-id : 订单在撮合中的顺序编号
* trade-id : 成交的唯一编号

### 订单类型

当前火币的订单类型是由买卖方向以及订单操作类型组成，例如：buy-market，buy为买卖方向，market为操作类型。

买卖方向：

* buy : 买
* sell: 卖

订单种类:

* type : 1=限价单
* side : 1-卖方，2-买方


### 订单状态

* submitted : 等待成交，该状态订单已进入撮合队列当中。
* partial-filled : 部分成交，该状态订单在撮合队列当中，订单的部分数量已经被市场成交，等待剩余部分成交。
* filled : 已成交。该状态订单不在撮合队列中，订单的全部数量已经被市场成交。
* partial-canceled : 部分成交撤销。该状态订单不在撮合队列中，此状态由partial-filled转化而来，订单数量有部分被成交，但是被撤销。
* canceled : 已撤销。该状态订单不在撮合订单中，此状态订单没有任何成交数量，且被成功撤销。
* canceling : 撤销中。该状态订单正在被撤销的过程中，因订单最终需在撮合队列中剔除才会被真正撤销，所以此状态为中间过渡态。


更多信息，可以点击 [Hotbit](https://www.hotbit.io) 进行了解。











