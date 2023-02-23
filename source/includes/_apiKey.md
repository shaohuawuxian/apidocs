# API Key 管理

## 三方自助申请 API Key

不对外暴露，必须由内部模块发起。

提交申请后，需平台方审核通过，才能获得 API Key

`POST /api/v1/api-key/request`

**请求参数**

| **参数**     | **是否必须** | **类型** | **说明**                                            |
| ------------ | ------------ | -------- | --------------------------------------------------- |
| restrictions | false        | int      | 新建 API Key 权限 0 = 所有权限（All）；默认所有权限 |
| email        | true         | string   | 邮箱                                                |
| name         | true         | string   | 名称                                                |

**返回参数**

| **参数**     | **类型** | **说明**                                                                                                      |
| ------------ | -------- | ------------------------------------------------------------------------------------------------------------- |
| apiKey       |          | API Key                                                                                                       |
| apiSecret    |          | API 密钥(只在申请时返回一次，无法通过接口查询，所有 api 接口需要通过此 key 来加密，请妥善保管，不展示与其他人 |
| restrictions |          | API Key 拥有权限                                                                                              |
| status       |          | API Key 状态，0（申请中）、-1（关闭）、1（使用中）                                                            |

```javascript
// 因为需要配置的权限并不多，我们暂时用 2 的 exponent 来标志
// 账户（Account）    2^0
// 资产（Assets）    2^1
// 发币（IssueAssets）   2^2
// 代币管理（TokenManagement） 2^3
```

|          |                   |                                |                                               |
| -------- | ----------------- | ------------------------------ | --------------------------------------------- |
| **权限** | **模块内容**      | **功能**                       | **url**                                       |
| `2^0`    | 账户（account）   | 创建账户                       | api/v1/account/create                         |
|          |                   | 账户地址查询                   | api/v1/account/query                          |
|          |                   | 根据用户名查询账户             | api/v1/account/queryUser                      |
|          |                   | 列表本渠道下的用户             | api/v1/account/list                           |
|          |                   | 账户冻结                       | api/v1/assets/frozen                          |
|          |                   | 账户解封                       | api/v1/assets/unfrozen                        |
|          |                   | 冻结账户资产                   | api/v1/assets/frozen-assets                   |
|          |                   | 解冻账户资产                   | api/v1/assets/unfrozen-assets                 |
|          |                   | 账户状态查询                   | api/v1/assets/status                          |
|          |                   | 账户资产查询                   | api/v1/assets/assets                          |
| `2^1`    | 资产（Assets）    | 获取充值地址                   | api/v1/account/depositAddress                 |
|          |                   | 执行提现                       | api/v1/assets/withdraw/apply                  |
|          |                   | 执行内部转账                   | api/v1/hw-order/order/inline_transfer         |
|          |                   | 充值提现转账历史记录查询       | api/v1/hw-order/order/inline_transfer_history |
|          |                   | 获取所有链                     | api/v1/assets/chain/list                      |
|          |                   | 获取所有币                     | api/v1/assets/token/list?chain=               |
|          |                   | 所有币配置                     | api/v1/assets/token/config                    |
|          |                   | 获取提现手续费                 | api/v1/assets/token/fee                       |
| `2^2`    | 发币`IssueAssets` | 发币                           | api/v1/token/create                           |
|          |                   | 查询发币状态                   | api/v1/token/status                           |
|          |                   | 查询发币订单详情               | api/v1/token/order/detail                     |
|          |                   | 查询发币记录                   | api/v1/token/order/list                       |
| `2^3`    | 代币管理          | 查询代币详情列表               | api/v1/token/list                             |
|          |                   | 查询代币详情                   | api/v1/coin-manage/tokenDetail                |
|          |                   | 查询账户下所有代币的持币地址数 | api/v1/coin-manage/accountCount               |
|          |                   | 查询代币的持有者信息           | api/v1/coin-manage/holderInfos                |
|          |                   | 地址代币余额查询               | api/v1/coin-manage/tokenBalance               |
|          |                   | 代币的持有者数量查询           | api/v1/coin-manage/holderCount                |
|          |                   | 查询地址下代币的状态           | api/v1/coin-manage/tokenStatus                |
|          |                   | 代币模型查询                   | api/v1/coin-manage/tokenModel                 |
|          |                   | 代币的交易费比例查询           | api/v1/coin-manage/taxFee                     |
|          |                   | 代币的奖励分红比例查询         | api/v1/coin-manage/bonusFee                   |
|          |                   | 地址代币交易记录查询           | api/v1/coin-manage/txHistory                  |
|          |                   | 账户的代币销毁数量查询         | api/v1/coin-manage/burnAmount                 |
|          |                   | 链的区块高度查询               | api/v1/coin-manage/height                     |
|          |                   | 代币的初始供应量和增发历史查询 | api/v1/coin-manage/tokenHistory               |
|          |                   | 禁止账户交易-交易黑名单        | api/v1/coin-manage/addBlack                   |
|          |                   | 允许账户交易-移出黑名单        | api/v1/coin-manage/removeBlack                |
|          |                   | 禁止账户转入                   | api/v1/coin-manage/addBlackIn                 |
|          |                   | 允许账户转入                   | api/v1/coin-manage/removeBlackIn              |
|          |                   | 禁止账户转出                   | api/v1/coin-manage/addBlackOut                |
|          |                   | 允许账户转出                   | api/v1/coin-manage/removeBlackOut             |
|          |                   | 冻结                           | api/v1/coin-manage/frozen                     |
|          |                   | 解冻                           | api/v1/coin-manage/unfrozen                   |
|          |                   | 禁止区块高度区间交易           | api/v1/coin-manage/addBlackRange              |
|          |                   | 允许区块高度区间交易           | api/v1/coin-manage/removeBlackRange           |
|          |                   | 铸造（增发）                   | api/v1/coin-manage/mint                       |
|          |                   | 销毁                           | api/v1/coin-manage/burn                       |
|          |                   | 销毁指定账户下的代币           | api/v1/coin-manage/burnFrom                   |
|          |                   | 查询账户的冻结代币数量         | api/v1/coin-manage/forzenAmount               |
|          |                   | 查询代币的总容量               | api/v1/coin-manage/cap                        |
|          |                   | 查询代币的闪电贷费用比例       | api/v1/coin-manage/flashFee                   |
|          |                   | 查询代币的禁止交易区间         | api/v1/coin-manage/blackRange                 |
|          |                   | 查询合约交易的状态             | api/v1/coin-manage/txStatus                   |

## 三方自助 API Key 状态查询

查询 API Key 是否可用

`POST /api/v1/api-key/info`

**请求参数**

| 参数   | 是否必须 | 类型   | **说明** |
| ------ | -------- | ------ | -------- |
| apiKey | true     | string | API Key  |

**返回参数**

| **参数**   | **类型** | **说明**                                           |
| ---------- | -------- | -------------------------------------------------- |
| status     | int      | API Key 状态，0（申请中）、-1（关闭）、1（使用中） |
| name       | string   |                                                    |
| email      | string   |                                                    |
| permission | int      |                                                    |

## 三方自助 API 密钥重新生成

因密钥泄露或者其他原因，需要重新生成握手密钥

` POST /api/v1/api-key/re-gen-sec`

**请求参数**

| 参数   | 是否必须 | 类型   | **说明** |
| ------ | -------- | ------ | -------- |
| apiKey | true     | string | API Key  |

**返回参数**

| **参数**  | **类型** | **说明** |
| --------- | -------- | -------- |
| apiSecret | string   |          |

## 平台批准 API 申请

由平台管理员批准，并且可以重置权限和状态

` POST /api/v1/api-key/approve`

**请求参数**

| 参数       | 是否必须 | 类型   | **说明** |
| ---------- | -------- | ------ | -------- |
| apiKey     | true     | string | API Key  |
| permission | true     | int    |          |
| status     | true     | int    |          |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |
|          | string   |          |

## 平台暂停三方 API 功能

由平台管理员操作，禁用三方，置其状态为-1

` POST /api/v1/api-key/disable`

**请求参数**

| 参数   | 是否必须 | 类型   | **说明** |
| ------ | -------- | ------ | -------- |
| apiKey | true     | string | API Key  |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |
|          | string   |          |

## 平台重启三方 API 功能

由平台管理员操作，重启三方，置其状态为 1。如果不修改三方权限，可用此方法代替 Approve

` POST /api/v1/api-key/enable`

**请求参数**

| 参数   | 是否必须 | 类型   | **说明** |
| ------ | -------- | ------ | -------- |
| apiKey | true     | string | API Key  |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |
|          | string   |          |

## 平台列表 api 请求

由平台管理员操作，查询 apiKey

` POST /api/v1/api-key/list`

**请求参数**

| **参数** | **是否必须** | **类型**  | **说明**     |
| -------- | ------------ | --------- | ------------ |
| start    | true         | timestamp | 秒级时间戳   |
| end      | true         | timestamp | 秒级时间戳   |
| page     | false        | int       | 第几页       |
| limit    | false        | int       | 页面行数     |
| status   | false        | int       | -99 代表全部 |

**返回参数**
对象列表

| **参数**   | **类型** | **说明** |
| ---------- | -------- | -------- |
| apiKey     | string   |          |
| permission | int      |          |
| status     | int      |          |
| name       | string   |          |
| email      | string   |          |
| createdAt  | time     | 申请时间 |
