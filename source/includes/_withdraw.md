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

---

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
