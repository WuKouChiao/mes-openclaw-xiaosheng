# MES API 参考

- **基础地址：** http://192.168.1.103:8088
- **鉴权：** 无需 Token（内网访问）
- **接口：** RESTful，只读查询

## 接口列表

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | /api/tables | 列出所有表 |
| GET | /api/tables/{name}/columns | 查表结构 |
| GET | /api/tables/{name}?page=1&size=50&filter=col1:val1,col2:val2 | 分页查询数据 |
