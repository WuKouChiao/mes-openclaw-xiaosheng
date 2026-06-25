# MES API 参考

- **基础地址：** http://192.168.1.103:8088
- **鉴权：** 无需 Token（内网访问）

## 通用表查询

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | /api/tables | 列出所有表 |
| GET | /api/tables/{name}/columns | 查表结构 |
| GET | /api/tables/{name}?page=1&size=50&filter={"col1":"val1"} | 分页查询数据，filter 为 JSON 格式 |

## 订单聚合接口

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | /api/orders/{orderNo}?site=3100 | 一次返回订单主表+客户名+明细列表 |
