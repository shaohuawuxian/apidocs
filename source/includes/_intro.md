# 介绍

## API Key 设置

- 所有接口需要 API Key 才可以访问.
- **永远不要把你的 API key/secret 告诉给任何人**

## API Key 权限设置

- 目前新创建的 API 的默认权限是全部 API 功能。

## 账户

平台测不区分机构账户、普通账户，业务层通过用户 ID 创建账户。

## 调用方式

所有 Api 调用都需要在业务字段之外附加三个握手字段

> go 代码如下

```go
ApiKey   string `json:"apiKey" binding:"required" example:"1233210123"`
Nonce    string `json:"nonce" binding:"required" example:"198964"`
Verified string `json:"verified" binding:"required" example:"BASE198964"`
```

> json 数据示例

```javascript
{
"apiKey": "gX3bWaCYWXx7",
"nonce": "123123",
"verified": "ABCD09123",
"otherBusinessFields": "..."
}
```

apiKey 就是您的申请到的 ApiKey

nonce 代表唯一的请求，避免被抓包重放。您可以用自增数字，也可以随便用随机数，只要保证近期不重复即可。即使业务上需要重试操作，nonce 也要变，认证握手和业务无关

verified 是校验字段，需要用到申请时给的 ApiSecret 来加密，具体的加密方式有提供 Javascript/Java 系列/Python/Go/Rust 等各种语言的样例可供参考
