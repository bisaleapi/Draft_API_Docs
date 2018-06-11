# REST API Reference

## 请求说明

1. 访问地址

## API Reference

### 行情API

#### GET /api/market/symbols 获取交易对信息

请求参数：

| 参数名  | 是否必须 | 类型   | 描述                                    | 取值          |
| ------- | -------- | ------ | --------------------------------------- | ------------- |
| symbol   | false     | string | 具体交易对名称，不填时，返回所有交易对       | NDX_ETH |

响应数据：

| 参数名  | 是否必须 | 类型   | 描述                                    |
| ------- | -------- | ------ | --------------------------------------- |
| code   | true     | int | 返回的状态码，20000表示成功，其它表示失败           |
| message   | true  | string | 返回的状态信息，OK表示成功，其它表示具体错误信息   |
| data   | true  | array | 交易对信息，具体看下面例子   |

data说明：

```json
"data": [
 {
    "symbol": "NDX_ETH", //交易对
    "base_currency": "NDX", //基础货币
    "quote_currency": "ETH", //报价货币
    "price_precision": 1e-8, //报价精度
    "amount_precision": 0.0001, //数量精度
    "minimal_place_amount": 0.001 //最小下单精度
 }
]
```

响应示例说明：

```json
GET /api/market/symbols
{
    "code":20000,
    "message":"OK",
    "data":[
        {
            "symbol":"ETH_BTC",
            "base_currency":"ETH",
            "quote_currency":"BTC",
            "price_precision":1e-8,
            "amount_precision":0.0001,
            "minimal_place_amount":0.0001
        },
        {
            "symbol":"ETH_USD",
            "base_currency":"ETH",
            "quote_currency":"USD",
            "price_precision":0.01,
            "amount_precision":0.0001,
            "minimal_place_amount":0.0001
        }
        // more data
    ]
}

GET /api/market/symbols?symbol=ETH_BTC
{
    "code":20000,
    "message":"OK",
    "data":[
        {
            "symbol":"ETH_BTC",
            "base_currency":"ETH",
            "quote_currency":"BTC",
            "price_precision":1e-8,
            "amount_precision":0.0001,
            "minimal_place_amount":0.0001
        }
    ]
}

GET /api/market/symbols?symbol=not-exist
{
    "code":10010,
    "message":"invalid symbol",
    "data":{}
}

```


#### /api/market/info 获取市场信息

请求参数：

| 参数名  | 是否必须 | 类型   | 描述                                    | 取值          |
| ------- | -------- | ------ | --------------------------------------- | ------------- |
| type   | false     | string | 具体市场名称，不填时，返回所有市场信息               | BTC |

响应数据：

| 参数名  | 是否必须 | 类型   | 描述                                    |
| ------- | -------- | ------ | --------------------------------------- |
| code   | true     | int | 返回的状态码，20000表示成功，其它表示失败           |
| message   | true  | string | 返回的状态信息，OK表示成功，其它表示具体错误信息   |
| data   | true  | object | 市场信息，具体看下面例子   |

data说明：

```json
"data": {
    "BTC": [
        {
            "symbol": "NDX_ETH", //交易对
            "base_currency": "NDX", //基础货币
            "quote_currency": "ETH", //报价货币
            "price_precision": 1e-8, //报价精度
            "amount_precision": 0.0001, //数量精度
            "minimal_place_amount": 0.001 //最小下单精度
        }
    ]
}
```

响应示例说明：

```json
GET /api/market/info
{
    "code":20000,
    "message":"OK",
    "data":{
        "BTC": [
            {
                "symbol":"ETH_BTC",
                "base_currency":"ETH",
                "quote_currency":"BTC",
                "price_precision":1e-8,
                "amount_precision":0.0001,
                "minimal_place_amount":0.0001
            },
            {
                "symbol":"XRP_BTC",
                "base_currency":"XRP",
                "quote_currency":"BTC",
                "price_precision":0.01,
                "amount_precision":0.0001,
                "minimal_place_amount":0.0001
            }
            // more data
        ],
        "ETH": [
            {
                "symbol":"LTC_ETH",
                "base_currency":"LTC",
                "quote_currency":"ETH",
                "price_precision":1e-8,
                "amount_precision":0.0001,
                "minimal_place_amount":0.0001
            },
            {
                "symbol":"BCH_ETH",
                "base_currency":"BCH",
                "quote_currency":"ETH",
                "price_precision":0.01,
                "amount_precision":0.0001,
                "minimal_place_amount":0.0001
            }
            // more data
        ]
    }
}

GET /api/market/info?type=ETH
{
    "code":20000,
    "message":"OK",
    "data":{
        "ETH": [
            {
                "symbol":"LTC_ETH",
                "base_currency":"LTC",
                "quote_currency":"ETH",
                "price_precision":1e-8,
                "amount_precision":0.0001,
                "minimal_place_amount":0.0001
            },
            {
                "symbol":"BCH_ETH",
                "base_currency":"BCH",
                "quote_currency":"ETH",
                "price_precision":0.01,
                "amount_precision":0.0001,
                "minimal_place_amount":0.0001
            }
            // more data
        ]
    }
}

GET /api/market/info?type=not-exist
{
    "code":10011,
    "message":"invalid market type",
    "data":{}
}
```

#### /api/market/kline 获取k线数据
请求参数：

|参数名|是否必须|类型|描述|默认值|取值|
|-------|------|------|---------------------------------------|-------------|-----------|
|symbol|true|string|交易对名称||ETH_BTC|
|period|false|string|k线类型|1min|1min,5min,15min,30min,1hour,2hour,4hour,1day,1week,1month,1year|
|size|false|integer|获取数量|200|[1,1000]|

响应数据：

| 参数名  | 是否必须 | 类型   | 描述                                    |
| ------- | -------- | ------ | --------------------------------------- |
| code   | true     | int | 返回的状态码，20000表示成功，其它表示失败           |
| message   | true  | string | 返回的状态信息，OK表示成功，其它表示具体错误信息   |
| data   | true  | object | k线数据，具体看下面例子   |

data说明：

```json
"data": {
    "description":"market.ETH_BTC.kline.1day",//k线数据类型描述
    "timestamp":1528444917,//响应生成时间点，单位：毫秒
    "kline_data": [
        {
            "id": 1527552000, //k线id
            "open_price": 8249, //开盘价
            "high_price": 9557, //最高价
            "low_price": 8249, //最低价
            "close_price": 9080, //收盘价
            "amount": 14973.5, //成交量
            "vloume":83921438.80043, //成交额, 即 sum(每一笔成交价 * 该笔的成交量)
        }
    ]
}

```
响应示例说明：

```json
GET /api/market/kline?symbol=ETh_BTC&period=1day&size=100
{
    "code":20000,
    "message":"OK",
    "data":[
    {
        "description": "market.ETH_BTC.kline.1day",
		"time_stamp": 1528446201,
        "kline_data":[
		{
            "id": 1527552000, 
            "open_price": 8249, 
            "high_price": 9557, 
            "low_price": 8249, 
            "close_price": 9080, 
            "amount": 14973.5, 
            "vloume":83921438.80043, 
        }
       	]
    }
        // more data
    ]
}

GET /api/market/kline?symbol=not-exist&period=1day&size=100
{
	"code": 10010,
	"message": "Invalid symbol",
	"data": {}
}

GET /api/market/kline?symbol=ETh_BTC&period=not-exist&size=100
{
	"code": 10012,
	"message": "Invalid period",
	"data": {}
}

GET /api/market/kline?symbol=ETh_BTC&period=1day&size=10000
{
	"code": 50000,
	"message": "invalid size, valid range:[1, 1000]",
	"data": {}
}
```



#### /api/market/trade 获取成交明细信息

请求参数：

| 参数名称  | 是否必须 | 类型   | 描述                                                         | 默认值         | 取值范围           |
| --------- | -------- | ------ | ------------------------------------------------------------ | -------------- | ------------------ |
| symbol    | true     | string | 交易对名称                                                   |                | ETH_BTC,VEN_BTC... |
| size      | false    | int    | 成交明细数量                                                 | 最新的一条数据 | [1,1000]           |
| startTime | false    | string | 查询起始时间 时间格式为yyyy-mm-dd hh:mm:ss,注意年月日和时分秒之间有空格，其余时间格式均为错误格式，正确时间格式模版：2018-06-06 01:02:03 |                |                    |
| endTime   | false    | string | 同上                                                         |                |                    |

响应数据：

| 参数名  | 是否必须 | 类型   | 描述                                             |
| ------- | -------- | ------ | ------------------------------------------------ |
| code    | true     | int    | 返回的状态码，20000表示成功，其它表示失败        |
| message | true     | string | 返回的状态信息，OK表示成功，其它表示具体错误信息 |
| data    | true     | object | 成交明细数据，具体看下面例子                     |

data说明：

```json
	"data": {
		"description": "market.ETH_BTC.trade.detail",//成交明细数据类型描述
		"time_stamp": 1528686098,//响应生成时间点，单位：毫秒
		"trade_data": [{
			"price": 0.0008,//成交价
			"size": 1.6,//成交量
			"direction": "sell",//主动成交方向
			"deal_time": 1528253621//成交时间
		}]
	}
```

响应示例说明：

```json
GET /api/market/trade?symbol=ETh_BTC&size=4&startTime=2018-05-06 10:00:10&endTime=2018-06-06 10:00:00
{
	"code": 20000,
	"message": "ok",
	"data": {
		"description": "market.ETH_BTC.trade.detail",
		"time_stamp": 1528686545,
		"trade_data": [{
			"price": 0.0008,
			"size": 1.6,
			"direction": "sell",
			"deal_time": 1528253621
		}, {
			"price": 0.0008,
			"size": 0.4,
			"direction": "sell",
			"deal_time": 1528253620
		}, {
			"price": 0.0008,
			"size": 3.6,
			"direction": "sell",
			"deal_time": 1528253620
		}, {
			"price": 0.0009,
			"size": 2.5,
			"direction": "buy",
			"deal_time": 1528253620
		}
        // more data
        ]
	}
}

GET /api/market/trade?symbol=not-exist&size=10
{
	"code": 10010,
	"message": "Invalid symbol",
	"data": {}
}

GET /api/market/trade?symbol=ETh_BTC&size=10000
{
	"code": 50000,
	"message": "invalid size, valid range:[1, 1000]",
	"data": {}
}

GET /api/market/trade?symbol=ETh_BTC&size=10000&startTime=2018-05-0610:10:10
{
	"code": 50000,
	"message": "invalid time",
	"data": {}
}

GET /api/market/trade?symbol=ETh_BTC&size=10000&endTime=2018-05-06
{
	"code": 50000,
	"message": "invalid time",
	"data": {}
}
```



#### /api/market/detail 获取24小时成交量数据

请求参数：

| 参数名称 | 是否必须 | 类型   | 描述       | 默认值 | 取值范围           |
| -------- | -------- | ------ | ---------- | ------ | ------------------ |
| symbol   | true     | string | 交易对名称 |        | ETH_BTC,VEN_BTC... |

响应数据：

| 参数名  | 是否必须 | 类型   | 描述                                             |
| ------- | -------- | ------ | ------------------------------------------------ |
| code    | true     | int    | 返回的状态码，20000表示成功，其他表示失败        |
| message | true     | string | 返回的状态信息，OK表示成功，其它表示具体错误信息 |
| data    | true     | object | 24小时成交量数据，具体看下面例子                 |

data说明：

```json
	"data": {
		"description": "market.ETH_BTC.detail",//24小时成交量数据描述
		"time_stamp": 1528698924,//响应生成时间点，单位：毫秒
		"detail_data": {
			"symbol": "ETH_BTC",//交易对名称
			"open_price": 1.59,//开盘价
			"last_price": 2.01,//收盘价
			"high_price": 2.78,//最高价
			"low_price": 1.43,//最低价
			"amount": 100,//24小时成交量
			"volume": 100,//近24小时累计成交数
			"timestamp": 0//24小时统计时间
		}
	}
```

响应示例说明：

```json
GET /api/market/detail?symbol=eth_btc
{
	"code": 20000,
	"message": "ok",
	"data": {
		"description": "market.ETH_BTC.detail",
		"time_stamp": 1528698924,
		"detail_data": {
			"symbol": "ETH_BTC",
			"open_price": 1.59,
			"last_price": 2.01,
			"high_price": 2.78,
			"low_price": 1.43,
			"amount": 100,
			"volume": 100,
			"timestamp": 0
		}
	}
}

GET /api/market/detail?symbol=not-exist
{
	"code": 10010,
	"message": "Invalid symbol",
	"data": {}
}
```

