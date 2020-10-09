---
title: 守易数据中心接口文档

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/AdamLo-oss/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---
# 简介
守易数据中心接口文档(只支持post)

#默认前缀
cy = RMB  

num = 次數/count

deposit/d = 充值

withdraw/w = 題現

trade/t = 交易


内部io:

https://xjp7dodwve.execute-api.ap-southeast-1.amazonaws.com/io

内部dev:

https://el071t9x0l.execute-api.ap-southeast-1.amazonaws.com/dev

外部io:

https://wf01tnpoxe.execute-api.ap-southeast-1.amazonaws.com/io

外部dev:

https://zmk1pc0ti3.execute-api.ap-southeast-1.amazonaws.com/dev


# 单维度基础表
## 成交明细表
### HTTP Request
`POST get_trade`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
        "current": {
            "real_total": 4280353.920415709,
            "all_total": 7186241236.076977,
            "real_h_total": "4084769.751218008563056623962453",
            "details": {
                "2019-09-01": {
                    "BTC": "1047710834.3841847389376205244625",
                },
            },
            "daily_total": {
                "2019-09-01": {
                    "deal": "3673188515.8315880335425832682029684",
                    "unclosed_deal": "6819.632961690879824376949455928946",
                    "unclosed_buy": "6819.632961690879824376949455928946",
                    "unclosed_sell": "0"
                },
            },
            "real_trade_record": {
                "2019-09-01": {
                    "deal": "2065437.113177735223425320992035"
                },
            },
            "real_trade_h_record": {
                "2019-09-01": {
                    "deal": "2270055.014137336562954316536119"
                },
            },
            "cy_b_total": "24058437.422224792900582019536147"
        }

```

##用户成交明细表
### HTTP Request
`POST single_get_user_trade`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间


> 返回:

```json
"2019-12-09": {                                    //日期
            "14177": {                            //用户id
                "user_type": 0,                   //用户类型 0 normal user, 1 robot做事
                "cy_buy": "0" ,                   //买入金额
                "cy_sell": "32.5237993862541375", //卖出金额
                "cy_total": "32.5237993862541375", //成交额
            }
 }
```




##币种成交明细表
### HTTP Request
`POST single_get_coin_trade`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
"2019-09-01": {
    "ABX": {
        "amount": "18.606",
        "cy_amount": "11.57899016973965442820896"
    },           
}
```


##充值明细表
### HTTP Request
`POST get_dw`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
"ETH": {
"sum_deposit": 1245.94563854, // ETH充值數量
"sum_withdraw": -254.03442855999992, //ETH提现數量
"num_d": 101, //ETH充值次數
"num_w": 99, //ETH提现次數
"cy_d": "1109250.69053640080834473664", //充 金额
"cy_w": "-226163.85224511007941308155695872",//提 金额
}
```

##充值明细表
### HTTP Request
`POST get_dw`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
"ETH": {
"sum_deposit": 1245.94563854, // ETH充值數量
"sum_withdraw": -254.03442855999992, //ETH提现數量
"num_d": 101, //ETH充值次數
"num_w": 99, //ETH提现次數
"cy_d": "1109250.69053640080834473664", //充 金额
"cy_w": "-226163.85224511007941308155695872",//提 金额
}
```

充值明细表 < 各幣種cy_d之和 題現明细表 < 各幣種cy_w之和

##提现明细表
###get_dw?start_date=2019-12-09&end_date=2019-12-10
各币种cy_w  之和 提现金额 in CNY

##币种充值明细表
###get_dw?start_date=2019-12-09&end_date=2019-12-10
cy_d //充值现金额
各币种 sum_deposit //充提数量

##充-提明细表
###get_dw?start_date=2019-12-09&end_date=2019-12-10
各币种（cy_d - cy_w）  之和 //充-提金额

##币种充-提明细表
###get_dw?start_date=2019-12-09&end_date=2019-12-10
cy_d - cy_ // 充-提金额
sum_deposit - sum_withdraw 之和  充-提数量



##手续费明细表
### HTTP Request
`POST single_get_fee_cy`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
"2019-12-09": {
  "cy_trade_fee": "-388762.15810701099011730516783696099256549423", //交易手续费 
  "cy_w_fee": "-2321104.9727914275705100962763787199",   //提现手续费
  "cy_fee": "-2709867.1907389577045142367616492561823", //手续费
}
```


##币种手续费明细表
### HTTP Request
`POST single_get_aesset_fee_cy`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
"BTC": {
   "cy_trade_fee": "0",  //交易手续费金额
   "cy_w_fee": "0", //提现手续费金额
   "trade_fee": "0", //交易手续费数量
   "w_fee": "0",//提现手续费数量
   "maker": "0",  //maker 数量
  "cy_maker": "0",
  "taker": "0",//taker 数量
  "cy_taker": "0"
},
```


##隐藏单成交额
### HTTP Request
`POST single_get_hide_trade`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
cy_trade  //成交额
```

##隐藏单获利额
### HTTP Request
`POST single_get_hide_trade`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
cy_profit  //成交额
```

# 电报群表

##电报群汇总表
### HTTP Request
`POST get_telegram_group_info`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
{
  "from_group": "Hotbit Indonesia ", //电报群
  "no_members": 9680,                //群人数
  "no_msg": 12,                      //发言条数
  "no_speaker": 3,                   //发言人数
  "rate_activity": 0.03099173,        //活跃度
},
```

##电报群明细表
### HTTP Request
`POST get_telegram_presonal_info`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
{
  "user_id": 255295943, //用户id
  "no_msg": 12 , // 发言条数
  "user_name": "M.Kh", //用户名字
  "score": 255295943,// 得分
  "from_group": //电报群
},
```

# 新增用户充值和用户提现报表
##新增用户充值和用户提现报表
### HTTP Request
`POST get_dw_with_user`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
{
  "user_id": 15029,             //用户
  "time": "2019-12-25",         //日期
  "sum_deposit": 9,             //充值数量
  "sum_withdraw": 0,            //提比数量
  "asset": "ETH",               //币种
  "cy_d": "8210.995039759104",  //充金额
  "cy_w": "0",                   //提金额
},
```

# 用户类型
##用户类型
### HTTP Request
`POST get_user_type`

> 返回:

```json
{
  "type": 0,                                          //类型
  "name": "普通用户",                        //名称
  "remark": "普通的Hotbit注册用户",  //备注
},
```

# 币种OHLC表
## 币种OHLC表
### HTTP Request
`POST get_trade_daily_price`
### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
start_date | false | 开始时间
end_date | false | 结束时间

> 返回:

```json
{
  "2018-05-18": {
        "open": "7999.98", //开盘
        "close": "8106.67",//收盘
        "highest": "8135.57",//最高
        "lowest": "739.78", //最低
  }
},
```
