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
