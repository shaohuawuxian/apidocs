# 代币管理 token

## 查询已发代币列表

查询某个账户 ID 下所发代币的代币列表

`GET api/v1/coin-manage/tokenList`

**请求参数：**

| **参数**  | **是否必须** | **类型** | **说明** |
| --------- | ------------ | -------- | -------- |
| accountId | true         | string   | 账户 ID  |

**返回参数：**

| **参数** | **是否必须** | **类型** | **说明**                                                          |
| -------- | ------------ | -------- | ----------------------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                                           |
| message  | true         | string   | 成功或错误信息                                                    |
| data     | true         | string   | json 字符串，可转化为代币详情数组，数组中每个元素是代币详情结构体 |

代币详情结构体如下定义

| **参数**      | **类型** | **说明**     |
| ------------- | -------- | ------------ |
| Addr          | string   | 代币地址     |
| Name          | string   | 代币名称     |
| Symbol        | string   | 代币符号     |
| Decimals      | string   | 代币精度     |
| Totoal_Supply | string   | 代币总供应量 |

## 查询代币详情

查询某个代币的代币详情

`GET api/v1/coin-manage/tokenDetail`

**请求参数:**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                            |
| -------- | ------------ | -------- | ----------------------------------- |
| code     | true         | string   | http 错误码，200 为正确             |
| message  | true         | string   | 成功或错误信息                      |
| data     | true         | string   | json 字符串，可转化为代币详情结构体 |

代币详情结构体同上

## 查询代币的持有者信息

`GET api/v1/coin-manage/holderInfos`

**请求参数:**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                            |
| -------- | ------------ | -------- | ----------------------------------- |
| code     | true         | string   | http 错误码，200 为正确             |
| message  | true         | string   | 成功或错误信息                      |
| data     | true         | string   | json 字符串，可以转换为持有者结构体 |

持有者结构体如下定义

| **参数**     | **类型** | **说明**                   |
| ------------ | -------- | -------------------------- |
| AccountAddr  | string   | 持币地址                   |
| ContractAddr | string   | 代币地址                   |
| Balance      | string   | 代币余额                   |
| Height       | string   | 更新代币余额所在的区块高度 |

## 查询代币余额

`GET api/v1/coin-manage/tokenBalance`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| accountId    | true         | string   | 账户 ID  |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **类型** | **说明**                |
| -------- | -------- | ----------------------- |
| code     | string   | http 错误码，200 为正确 |
| message  | string   | 成功或错误信息          |
| data     | string   | 代币余额（带精度截断）  |

## 查询账户下代币的状态

`POST api/v1/coin-manage/tokenStatus`

**请求参数:**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |
| accountId    | true         | string   | 账户 ID  |

**返回参数:**

| **参数** | **类型** | **说明**                        |
| -------- | -------- | ------------------------------- |
| code     | string   | http 错误码，200 为正确         |
| message  | string   | 成功或错误信息                  |
| data     | string   | json 字符串，可转化为状态结构体 |

状态结构体如下定义

| **参数**         | **类型** | **说明**     |
| ---------------- | -------- | ------------ |
| IsBlack          | bool     | 是否是黑名单 |
| IsBlackIn        | bool     | 是否禁止转入 |
| IsBlackOut       | bool     | 是否禁止转出 |
| NowFrozenAmount  | Int      | 当前冻结数量 |
| WaitFrozenAmount | Int      | 等待冻结数量 |

## 代币的模型查询

`POST api/v1/coin-manage/tokenModel`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                |
| -------- | ------------ | -------- | ----------------------- |
| code     | true         | string   | http 错误码，200 为正确 |
| message  | true         | string   | 成功或错误信息          |
| data     | true         | string   | 模型枚举值              |

模型枚举值定义如下：

| **参数**    | **类型** | **值** | **说明**         |
| ----------- | -------- | ------ | ---------------- |
| _SIMPLE_    | Int      | 1      | 简单模型         |
| _SNAPSHOT_  | Int      | 2      | 快照模型         |
| _VOTES_     | Int      | 3      | 投票模型         |
| _FLASHMINT_ | Int      | 4      | 闪电贷模型       |
| _BURNABLE_  | Int      | 5      | 可燃烧模型       |
| _CAPPED_    | Int      | 6      | 设置总量上限模型 |
| _DEFLATION_ | Int      | 7      | 通缩模型         |

## 查询代币的交易费比例

`POST api/v1/coin-manage/taxFee`

**请求参数:**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                       |
| -------- | ------------ | -------- | ------------------------------ |
| code     | true         | string   | http 错误码，200 为正确        |
| message  | true         | string   | 成功或错误信息                 |
| data     | true         | string   | 返回值除以一万，就是交易费比例 |

## 查询代币的奖励分红比例

`POST api/v1/coin-manage/bonusFee`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                         |
| -------- | ------------ | -------- | -------------------------------- |
| code     | true         | string   | http 错误码，200 为正确          |
| message  | true         | string   | 成功或错误信息                   |
| data     | true         | string   | 返回值除以一万，就是奖励分红比例 |

## 账户的代币交易记录查询

`GET api/v1/coin-manage/txHistory`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**                      |
| ------------ | ------------ | -------- | ----------------------------- |
| accountId    | true         | string   | 账户 ID                       |
| contractAddr | true         | string   | 代币地址                      |
| beginTime    | true         | string   | 开始时间(unix 时间戳，单位秒) |
| endTime      | true         | string   | 结束时间(unix 时间戳，单位秒) |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                          |
| -------- | ------------ | -------- | --------------------------------- |
| code     | true         | string   | http 错误码，200 为正确           |
| message  | true         | string   | 成功或错误信息                    |
| data     | true         | string   | json 字符串，可以转化为交易结构体 |

交易结构体定义如下

| **参数**  | **类型** | **说明**                                                                                                                       |
| --------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Hash      | string   | 交易 hash                                                                                                                      |
| OpParams  | struct   | 交易参数结构体                                                                                                                 |
| Amount    | uint64   | 交易数量（如果非合约交易，amount=txGeneral 中的 value，如果是合约交易，那么 txGeneral 中 value 为 0，amount 为代币的交易数量） |
| TxGeneral | struct   | 交易详情结构体                                                                                                                 |

交易参数结构体定义：

| **参数** | **类型** | **说明**           |
| -------- | -------- | ------------------ |
| Op       | string   | 交易动作           |
| Addrs    | []string | 交易参数：地址数组 |
| Values   | []string | 交易参数：值数组   |

交易详情结构体定义：

| **参数**             | **类型**  | **说明**                                                             |
| -------------------- | --------- | -------------------------------------------------------------------- |
| TxType               | string    | 交易类型（0--LegacyTxType 1-- AccessListTxType 2--DynamicFeeTxType） |
| From                 | string    | 交易发送地址                                                         |
| To                   | string    | 交易接收地址                                                         |
| Hash                 | string    | 交易 hash                                                            |
| Index                | string    | 交易在收据中的索引                                                   |
| Value                | string    | 交易的值                                                             |
| Input                | string    | input 数据，如果是非合约交易，此项为空                               |
| Nonce                | string    | 交易的 nonce                                                         |
| GasPrice             | string    | 交易的 gasPrice                                                      |
| GasLimit             | string    | 交易的 gas                                                           |
| GasUsed              | string    | 交易使用的 gas                                                       |
| IsContract           | string    | 是否是合约交易                                                       |
| IsContractCreate     | string    | 是否是合约创建交易                                                   |
| BlockTime            | int       | 交易打包时间                                                         |
| BlockNum             | int       | 交易所在的区块高度                                                   |
| BlockHash            | string    | 交易所在的区块 hash                                                  |
| ExecStatus           | int       | 执行结果（0-失败 1-成功）                                            |
| CreateTime           | timestamp | 交易爬取的时间                                                       |
| BlockState           | int       | 区块状态（0-正常 1-失败 常用于回滚）                                 |
| MaxFeePerGas         | int       | 最高交易消费                                                         |
| BaseFee              | int       | base fee                                                             |
| MaxPriorityFeePerGas | int       | 最高有限消费                                                         |
| BurntFees            | int       | 燃烧的小费                                                           |

## 查询账户的代币销毁数量

`GET api/v1/coin-manage/burnAmount`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |
| accountId    | true         | string   | 账户 ID  |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                |
| -------- | ------------ | -------- | ----------------------- |
| code     | true         | string   | http 错误码，200 为正确 |
| message  | true         | string   | 成功或错误信息          |
| data     | true         | string   | 销毁数量                |

## 链的区块高度查询

`GET api/v1/coin-manage/height`

**请求参数：**无

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                |
| -------- | ------------ | -------- | ----------------------- |
| code     | true         | string   | http 错误码，200 为正确 |
| message  | true         | string   | 成功或错误信息          |
| data     | true         | string   | 区块高度                |

## 查询代币的初始供应量和增发历史

`GET api/v1/coin-manage/tokenHistory`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                                                                                   |
| -------- | ------------ | -------- | ---------------------------------------------------------------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                                                                                    |
| message  | true         | string   | 成功或错误信息                                                                                             |
| data     | true         | string   | json 字符串，含有初始供应量和增发历史的键值对，例如：'{"init_coin_supply":"xxx","add_coin_history":"xxx"}' |

## 加入黑名单

`POST api/v1/coin-manage/addBlack`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |
| targetId     | true         | string   | 目标账户 ID   |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 移出黑名单

`POST api/v1/coin-manage/removeBlack`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |
| targetId     | true         | string   | 目标账户 ID   |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 添加转入黑名单

`POST api/v1/coin-manage/addBlackIn`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |
| targetId     | true         | string   | 目标账户 ID   |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 移出转入黑名单

`POST api/v1/coin-manage/removeBlackIn`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |
| targetId     | true         | string   | 目标账户 ID   |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 添加转出黑名单

`POST api/v1/coin-manage/addBlackOut`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |
| targetId     | true         | string   | 目标账户 ID   |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 移出转出黑名单

`POST api/v1/coin-manage/removeBlackOut`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |
| targetId     | true         | string   | 目标账户 ID   |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 冻结

`POST api/v1/coin-manage/frozen`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**               |
| ------------ | ------------ | -------- | ---------------------- |
| amount       | true         | string   | 冻结的数量（带有精度） |
| contractAddr | true         | string   | 代币地址               |
| operatorId   | true         | string   | 操作者账户 ID          |
| targetId     | true         | string   | 目标账户 ID            |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 解冻

`POST api/v1/coin-manage/unfrozen`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**               |
| ------------ | ------------ | -------- | ---------------------- |
| amount       | true         | string   | 冻结的数量（带有精度） |
| contractAddr | true         | string   | 代币地址               |
| operatorId   | true         | string   | 操作者账户 ID          |
| targetId     | true         | string   | 目标账户 ID            |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                                           |
| -------- | ------------ | -------- | ------------------------------------------------------------------ |
| code     | true         | string   | http 错误码，200 为正确                                            |
| message  | true         | string   | 成功或错误信息                                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"}交易发出成功提示 |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 添加区块高度间交易黑名单

`POST api/v1/coin-manage/addBlackRange`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| startblock   | true         | string   | 起始区块高度  |
| endblock     | true         | string   | 终止区块高度  |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 移出区块高度间交易黑名单

`POST api/v1/coin-manage/removeBlackRange`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| index        | true         | string   | 区间索引      |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 铸造（增发）

`POST api/v1/coin-manage/mint`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| amount       | true         | string   | 铸造的数量    |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 销毁

`POST api/v1/coin-manage/burn`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| amount       | true         | string   | 销毁的数量    |
| contractAddr | true         | string   | 代币地址      |
| operatorId   | true         | string   | 操作者账户 ID |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 销毁指定账户下的代币

`POST api/v1/coin-manage/burnFrom`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**               |
| ------------ | ------------ | -------- | ---------------------- |
| amount       | true         | string   | 销毁的数量（带有精度） |
| contractAddr | true         | string   | 代币地址               |
| operatorId   | true         | string   | 操作者账户 ID          |
| targetId     | true         | string   | 目标账户 ID            |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                           |
| -------- | ------------ | -------- | -------------------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                            |
| message  | true         | string   | 成功或错误信息                                     |
| data     | true         | string   | json 字符串，类似{"requestId":"xxx","uuid": "xxx"} |

**备注**：返回成功表示成功调用了合约交易，需要用返回的 data 中的 uuid 调用本页面的最后一个接口：查询合约交易的状态

## 查询账户的冻结代币数量

`POST api/v1/coin-manage/forzenAmount`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**      |
| ------------ | ------------ | -------- | ------------- |
| contractAddr | true         | string   | 代币地址      |
| accountId    | true         | string   | 操作者账户 ID |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                |
| -------- | ------------ | -------- | ----------------------- |
| code     | true         | string   | http 错误码，200 为正确 |
| message  | true         | string   | 成功或错误信息          |
| data     | true         | string   | 冻结数量                |

## 查询代币的总容量

`POST api/v1/coin-manage/cap`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                |
| -------- | ------------ | -------- | ----------------------- |
| code     | true         | string   | http 错误码，200 为正确 |
| message  | true         | string   | 成功或错误信息          |
| data     | true         | string   | 总容量                  |

## 查询代币的闪电费用比例

`POST api/v1/coin-manage/flashFee`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                |
| -------- | ------------ | -------- | ----------------------- |
| code     | true         | string   | http 错误码，200 为正确 |
| message  | true         | string   | 成功或错误信息          |
| data     | true         | string   | 代币的闪电费比例        |

## 查询代币的禁止交易区间

`POST api/v1/coin-manage/blackRange`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明** |
| ------------ | ------------ | -------- | -------- |
| contractAddr | true         | string   | 代币地址 |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                                |
| -------- | ------------ | -------- | --------------------------------------- |
| code     | true         | string   | http 错误码，200 为正确                 |
| message  | true         | string   | 成功或错误信息                          |
| data     | true         | string   | jaon 字符串，可转化为交易区间结构体数组 |

交易区间结构体定义如下：

| **参数**   | **是否必须** | **类型** | **说明** |
| ---------- | ------------ | -------- | -------- |
| BeginBlock | true         | string   | 起始区间 |
| EndBlock   | true         | string   | 结束区间 |

## 查询合约交易的状态

`POST api/v1/coin-manage/txStatus`

**请求参数：**

| **参数**     | **是否必须** | **类型** | **说明**                              |
| ------------ | ------------ | -------- | ------------------------------------- |
| contractAddr | true         | string   | 代币地址                              |
| accountId    | true         | string   | 账户 ID                               |
| uuid         | true         | string   | 合约交易成功发出后返回的字串中的 uuid |

**返回参数:**

| **参数** | **是否必须** | **类型** | **说明**                |
| -------- | ------------ | -------- | ----------------------- |
| code     | true         | string   | http 错误码，200 为正确 |
| message  | true         | string   | 成功或错误信息          |
| data     | true         | string   | 任务的状态              |
