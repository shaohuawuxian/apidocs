---
title: API Reference 1.0

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  # - javascript
  # - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# 介绍

Hello 1.0

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# API Key

## 创建 API Key

提交创建后，需平台方审核通过后才能获得 API Key

`POST api/v1/apikey/create `

**参数**

| **参数**     | **是否必须** | **类型** | **说明**                                                                                                                                                                                  |
| ------------ | ------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ```restrictions``` | false        |          | 新建 API Key 权限，账户（Account）、充值（Deposit）、提现（Withdraw）、外部资产（externalAssets）、发币（externalAssets）、内部代币管理（tokenManagement）、所有权限（All）；默认所有权限 |

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

> 返回参数

```shell
{
  status: 1, API Key 状态，0（可用）、1（不可用）
}
```

# 账户(account)

## 创建账户

`POST api/v1/account/create`

**请求参数**

| **参数** | **是否必须** | **类型** | **说明**                |
| -------- | ------------ | -------- | ----------------------- |
| apiID    | true         |          | ID 具有唯一性           |
| userId   | true         |          | 用户 ID，业务方自己生成 |

**返回参数**

| **参数**    | **类型** | **说明**            |
| ----------- | -------- | ------------------- |
| accountId   |          | 账户 ID，具有唯一性 |
| coin        |          | 代币                |
| network     |          | 地址网络            |
| chainAdress |          | 地址                |

## 账户地址查询

api/v1/account/address

GET

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**            |
| --------- | ------------ | -------- | ------------------- |
| apiID     | true         |          | ID 具有唯一性       |
| accountId | true         |          | 账户 ID，具有唯一性 |

**返回参数**

| **参数**    | **类型** | **说明** |
| ----------- | -------- | -------- |
| coin        |          | 代币     |
| network     |          | 地址网络 |
| chainAdress |          | 地址     |

## 账户冻结

api/v1/account/frozen/function

POST

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**                                                         |
| --------- | ------------ | -------- | ---------------------------------------------------------------- |
| apiID     | true         |          | ID 具有唯一性                                                    |
| accountId | true         |          | 账户 ID，具有唯一性                                              |
| function  | false        |          | 账户功能：1（充值）、2（提现）、3（转账）、0（所有功能）；默认 3 |
| coin      | false        |          | 代币名称，默认所有代币                                           |
| startTime | false        |          | 开始冻结时间（秒）                                               |
| endTime   | false        |          | 结束冻结时间（秒）                                               |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |

## 账户解封

api/v1/account/unfrozen/function

POST

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**                                                         |
| --------- | ------------ | -------- | ---------------------------------------------------------------- |
| apiID     | true         |          | ID 具有唯一性                                                    |
| accountId | true         |          | 账户 ID，具有唯一性                                              |
| function  | false        |          | 账户功能：1（充值）、2（提现）、3（转账）、0（所有功能）；默认 3 |
| coin      | false        |          | 代币名称，默认所有代币                                           |
| startTime | false        |          | 开始解封时间（秒）                                               |
| endTime   | false        |          | 结束解封时间（秒）                                               |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |

## 冻结账户资产

api/v1/account/frozen/assets

POST

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**               |
| --------- | ------------ | -------- | ---------------------- |
| apiID     | true         |          | ID 具有唯一性          |
| accountId | true         |          | 账户 ID，具有唯一性    |
| coin      | false        |          | 代币名称，默认所有代币 |
| qty       | false        |          | 数量，默认全部         |
| startTime | false        |          | 开始冻结时间（秒）     |
| endTime   | false        |          | 结束冻结时间（秒）     |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |

## 解冻账户资产

api/v1/account/unfrozen/assets

POST

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**               |
| --------- | ------------ | -------- | ---------------------- |
| apiID     | true         |          | ID 具有唯一性          |
| accountId | true         |          | 账户 ID，具有唯一性    |
| coin      | false        |          | 代币名称，默认所有代币 |
| qty       | false        |          | 数量，默认全部         |
| startTime | false        |          | 开始解冻时间（秒）     |
| endTime   | false        |          | 结束解冻时间（秒）     |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |

## 账户状态查询

api/v1/account/status

GET

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**            |
| --------- | ------------ | -------- | ------------------- |
| apiID     | true         |          | ID 具有唯一性       |
| accountId | true         |          | 账户 ID，具有唯一性 |

**返回参数**

| **参数**            | **类型** | **说明**                                                         |
| ------------------- | -------- | ---------------------------------------------------------------- |
| list>function       |          | 账户功能：1（充值）、2（提现）、3（转账）、0（所有功能）；默认 3 |
| list>functionStatus |          | 功能状态：normal（正常）；frozen（冻结）                         |
| list>startTime      |          | 开始冻结时间（秒）                                               |
| list>endTime        |          | 结束冻结时间（秒）                                               |

## 账户资产查询

api/v1/account/assets

GET

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**            |
| --------- | ------------ | -------- | ------------------- |
| apiID     | true         |          | ID 具有唯一性       |
| accountId | true         |          | 账户 ID，具有唯一性 |

**返回参数**

| **参数**          | **类型** | **说明**                                 |
| ----------------- | -------- | ---------------------------------------- |
| list>coin         |          | 代币名称                                 |
| list>assetsStatus |          | 代币状态：normal（正常）；frozen（冻结） |
| list>qty          |          | 冻结数量                                 |
| list>StartTime    |          | 开始冻结时间（秒）                       |
| list>EndTime      |          | 结束冻结时间（秒）                       |

# 充值功能

## 获取充值地址

api/v1/assets/deposit/address

GET

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**            |
| --------- | ------------ | -------- | ------------------- |
| apiID     | true         |          | APIID 具有唯一性    |
| accountId | true         |          | 账户 id，具有唯一性 |
| coin      | true         |          | 币种                |
| network   | true         |          | 转账网络            |

**返回参数**

| **参数**     | **类型** | **说明** |
| ------------ | -------- | -------- |
| chainAddress |          | 地址     |

## 获取充值历史

api/v1/assets/deposit/history

GET

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**            |
| --------- | ------------ | -------- | ------------------- |
| apiID     | true         |          | APIID 具有唯一性    |
| accountId | true         |          | 账户 ID，具有唯一性 |
| coin      | false        |          | 币种                |
| status    | false        |          | 状态：success       |
| startTime | false        |          | 开始时间（秒）      |
| endTime   | false        |          | 结束时间（秒）      |
| txid      | false        |          | 交易哈希            |

**返回参数**

| **参数**          | **类型** | **说明** |
| ----------------- | -------- | -------- |
| list>coin         |          | 币种     |
| list>qty          |          | 数量     |
| list>chainAddress |          | 充值地址 |
| list>txid         |          | 交易哈希 |
| list>status       |          | 状态     |

## 查询最小充值金额

小于最小金额的充值将不会上账

api/v1/assets/deposit/minsize

GET

**请求参数**

| **参数** | **是否必须** | **类型** | **说明** |
| -------- | ------------ | -------- | -------- |
| token    | true         |          | 代币     |
| network  | true         |          | 网络     |

# 所有链-所有币

## 获取所有链

请求方式: GET

请求路径:/chain/list

返回参数:

| **字段** | **类型** | **描述** |
| -------- | -------- | -------- |
| data     | []string | 所有链   |

## 获取所有币

请求方式: GET

请求路径:/token/list

返回参数:

| **字段**      | **类型** | **描述**            |
| ------------- | -------- | ------------------- |
| chain         | string   | 链名称              |
| decimals      | int      | 精度                |
| mapped_symbol | string   | huione 链内代币符号 |
| symbol        | string   | 代币符号            |

## 所有币配置

请求方式: GET

请求路径:/token/config

返回参数:

| **字段**             | **类型** | **描述**           |
| -------------------- | -------- | ------------------ |
| token_code           | string   | 代币符号           |
| allow_pay            | bool     | 是否允许充值       |
| allow_withdraw       | bool     | 是否允许提现       |
| allow_inter_transfer | bool     | 是否允许内部转账   |
| min_withdraw         | float64  | 最低提现额度       |
| fee_rate             | float64  | 手续费比例         |
| fee_const            | float64  | 手续费固定值       |
| is_fee_const         | bool     | 手续费是否是固定值 |

# 提现功能

## 执行提现

api/v1/assets/withdraw/apply

POST

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**            |
| --------- | ------------ | -------- | ------------------- |
| apiID     | true         |          | APIID 具有唯一性    |
| accountId | true         |          | 账户 id，具有唯一性 |
| token     | true         |          | 币种                |
| address   | true         |          | 提币地址            |
| network   | true         |          | 转账网络            |
| qty       | true         |          | 数量                |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |

## 获取提币历史

api/v1/assets/withdraw/history

GET

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**            |
| --------- | ------------ | -------- | ------------------- |
| apiID     | true         |          | APIID 具有唯一性    |
| accountId | true         |          | 账户 id，具有唯一性 |
| startTime | false        |          | 币种                |
| endTime   | false        |          | 提币地址            |
| token     | false        |          | 转账网络            |
| status    | false        |          | 数量                |
| txid      | false        |          | 交易哈希            |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |
| time     |          | 时间     |
| token    |          | 代币     |
| qty      |          | 数量     |
| address  |          | 提现地址 |
| txid     |          | 交易哈希 |

## 区块确认数

api/v1/assets/deposit/block/number

GET

**请求参数**

| **参数**  | **是否必须** | **类型** | **说明**            |
| --------- | ------------ | -------- | ------------------- |
| apiID     | true         |          | APIID 具有唯一性    |
| accountId | true         |          | 账户 id，具有唯一性 |
| startTime | false        |          | 币种                |
| endTime   | false        |          | 提币地址            |
| token     | false        |          | 转账网络            |
| status    | false        |          | 数量                |
| txid      | false        |          | 交易哈希            |

**返回参数**

| **参数** | **类型** | **说明** |
| -------- | -------- | -------- |
| time     |          | 时间     |
| token    |          | 代币     |
| qty      |          | 数量     |
| address  |          | 提现地址 |

## 查询最小提现金额

小于最小金额将无法提现

api/v1/assets/withdraw/minsize

POST

**请求参数**

| **参数** | **是否必须** | **类型** | **说明** |
| -------- | ------------ | -------- | -------- |
| token    | true         |          | 代币     |
| network  | true         |          | 网络     |

**返回参数**

| **参数** | **类型** | **说明**     |
| -------- | -------- | ------------ |
| minSize  |          | 最小充值金额 |
