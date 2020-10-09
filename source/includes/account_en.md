# Relevant Contents Of Available Assets In The Accounts

## Retrieve User's Assets

API Key Permission：Read


Check the balance of designated account, supports the following accounts：


__HTTP Request__

* GET /api/v1/balance.query


__Request Parameter__

Name of Parameter |	Required or not |	Type|	Description|	Default Value|	Range of Parameter
-------- | ------------- | ------------- | ------------- | ------------- | ------------- 
api_key  |  true | string | The API KEY Requested By The User | | |
sign     |  true | string | The Signature Value of the requested string | | |
assets   |  true | json array | The array of token symbol, blank array means retrieve all token assets | | |



__Response Data__


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


Name of Parameter|	Required Or Not	|Data Type	|Description	|Range of Parameter
-------- | ------------- | ------------- | ------------- | -------------
available      | Yes               | string         | Volume Available
freeze         | Yes               | string         | Frozen Volume




<aside class="notice">
   assets — Blank array means retrieve all token assets
</aside>







<!-- 


 -->
## Retrieve The Records Regarding The Changes In User Assets
<!-- ```Response:
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
``` -->
### HTTP Request

`POST /balance.history`

### Request Parameter

Name of Parameter       |Required Or Not         | Type                   |Description
--------      | -------        | ----                 |------
api_key       |Yes              | string               |The API KEY Requested By The User
sign          |Yes              | string               |The signature value of the requested string
asset         |Yes              | string               |Name of assets，For example："BTC","ETH" etc.，""means the names of all assets
business      |Yes              | string               |Name of business，如："deposit" or "trade"，""means the names of all businesses
start_time    |Yes              | Integer(64 digit without symbol)   |Starting Time(Second)
end_time      |Yes              | Integer(64 digit without symbol)   |Ending Time(second)
offset        |Yes              | Integer(32 Digit)        |Offset position, if set as 0, it means all transaction records starting from the latest transaction to the earliest transaction, the total number of transactions cannot be greater than limit; if set as 1, it means the number of all transaction records starting from the second latest transaction to the earliest transaction cannot be greater than limit; and so on

limit         |Yes              | Integer(32 Digit)        |Maximum number of transactions returned


 
### Response Data

Name of Paramter        | Required or Not          | Type           |  Description
---------      | -------         | ----           |------
api_key        | Yes              | string         | The API KEY Requested By The User


<aside class="notice">
   assets — Blank array means retrieve all token assets
</aside>