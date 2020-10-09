# 账户资产相关

## 获取用户资产

API Key 权限：读取


查询指定账户的余额，支持以下账户：


__HTTP 请求__

* GET /api/v1/balance.query


__请求参数__

参数名称 |	是否必须 |	类型|	描述|	取值范围
-------- | ------------- | ------------- | ------------- | ------------- | ------------- 
api_key  |  true | string | 用户申请的API KEY | -
sign     |  true | string | 请求字符串的签名值 | -
assets   |  true | json array | 代币符号数组，空数组表示获取全部代币资产 | ["BTC","ETH",....]



__响应数据__


> Response:

```json
{
	"error": null,
	"id": 1585283976,
	"result": {
		"0xBTC":       
		{
		    "available": "0",
		    "freeze": "0"
		},
		"ETH":       
		{
		    "available": "0",
		    "freeze": "0"
		}
	}
  
}
```


参数名称|	是否必须	|数据类型	|描述	|取值范围
-------- | ------------- | ------------- | ------------- | -------------
available      | 是               | string         | 可用数量 | -
freeze         | 是               | string         | 冻结数量 | -




<aside class="notice">
   assets — 空数组表示获取全部代币资产
</aside>





