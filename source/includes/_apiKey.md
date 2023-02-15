# API Key

## 创建 API Key

提交创建后，需平台方审核通过后才能获得 API Key

`POST api/v1/apikey/create `

```javascript
{
  "timezone": "UTC",
  "serverTime": 1565246363776,
  "rateLimits": [
    {
      //这些在"限制种类 (rateLimitType)"下的"枚举定义"部分中定义
      //所有限制都是可选的
    }
  ],
  "exchangeFilters": [
    //这些是"过滤器"部分中定义的过滤器
    //所有限制都是可选的
  ],
  "symbols": [
    {
      "symbol": "ETHBTC",
      "status": "TRADING",
      "baseAsset": "ETH",
      "baseAssetPrecision": 8,
      "quoteAsset": "BTC",
      "quotePrecision": 8,
      "quoteAssetPrecision": 8,
      "orderTypes": [
        "LIMIT",
        "LIMIT_MAKER",
        "MARKET",
        "STOP_LOSS",
        "STOP_LOSS_LIMIT",
        "TAKE_PROFIT",
        "TAKE_PROFIT_LIMIT"
      ],
      "icebergAllowed": true,
      "ocoAllowed": true,
      "quoteOrderQtyMarketAllowed": false,
      "allowTrailingStop": false,
      "isSpotTradingAllowed": true,
      "isMarginTradingAllowed": true,
      "cancelReplaceAllowed": false,
      "filters": [
        //这些在"过滤器"部分中定义
        //所有限制都是可选的
      ],
      "permissions": ["SPOT", "MARGIN"],
      "defaultSelfTradePreventionMode": "NONE",
      "allowedSelfTradePreventionModes": ["NONE"]
    }
  ]
}
```

**参数**

| **参数**       | **是否必须** | **类型** | **说明**                                                                                                                                                                                  |
| -------------- | ------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `restrictions` | false        |          | 新建 API Key 权限，账户（Account）、充值（Deposit）、提现（Withdraw）、外部资产（externalAssets）、发币（externalAssets）、内部代币管理（tokenManagement）、所有权限（All）；默认所有权限 |

**返回参数**

| **参数**    | **类型** | **说明**                             |
| ----------- | -------- | ------------------------------------ |
| apiKey      |          | API Key                              |
| permissions |          | API Key 拥有权限                     |
| status      |          | API Key 状态，0（可用）、1（不可用） |
| secretKey   |          | API 密钥                             |
| apiId       |          | ID 具有唯一性                        |

## API Key 状态查询

查询 API Key 是否可用

`GET api/v1/apikey/status`

**请求参数**

| 参数   | 是否必须 | 类型 | **说明**      |
| ------ | -------- | ---- | ------------- |
| apiId  | false    |      | ID 具有唯一性 |
| apiKey | false    |      | API Key       |
