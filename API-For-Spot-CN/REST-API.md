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