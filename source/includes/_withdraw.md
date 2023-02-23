# 提现功能

## 执行提现

`POST api/v1/assets/withDraw`

**请求参数**

| **参数**  | **是否必填** | **参数类型** | **描述说明**            |
| --------- | ------------ | -------- | ------------------- |
| thirdId     | 是       |   String       | 三方订单id        |
| accout    | 是         |   String       | 提现账户id        |
| symbol     | 是        | String         | token          |
| amount    | 是         |  String        | 数量             |
| chain     | 是         |  String        | 链名称            |
| addr      | 是         |   String       | 提现地址          |
|isSync     |是          |	Boolean       |是否同步执行         |

> 示例请求
```JavaScript
{
    "thirdId": "11111",
    "accout": "123",
    "symbol": "HUI",
    "amount": "20",
    "chain": "hui",
    "addr": "0xAb41dEdC0B7333fD76A0619A145a4Aa3492cB017",
    "isSync": true
}
```

**返回参数**

| **参数**  | **是否必填** | **参数类型** | **描述说明**            |
| --------- | ------------ | -------- | ------------------- |
| code     | 是       |   Integer       | 0为ok 其余为错误        |
| msg    | 是         |   String       | 错误描述        |
| data     | 是        | Object         |           |
| dataOrderId    | 是         |  String        | 订单id        |
| dataThirdId     | 是         |  String        | 三方订单id    |
| dataSucess      | 是         |   Boolean       | 是否成功     |


> 返回示例

```JavaScript
{"code":-1000,"msg":"notify withdrawl fail","data":{"orderId":"","thirdId":"11111","sucess":false}}
```
