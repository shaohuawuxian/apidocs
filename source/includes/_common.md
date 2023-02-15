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
