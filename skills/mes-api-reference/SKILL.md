---
name: "mes-api-reference"
description: "MES 系统 API 参考：通用表查询、订单聚合接口，base URL http://192.168.1.103:8088"
---

# MES API 参考

## 基础信息
- **基础地址：** http://192.168.1.103:8088
- **鉴权：** 无需 Token（内网访问）

## 通用表查询

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | /api/tables | 列出所有表 |
| GET | /api/tables/{name}/columns | 查表结构 |
| GET | /api/tables/{name}?page=1&size=50&filter={"col":"val"}&sort=CREATE_TIME&order=desc | 分页查询数据 |

### filter 过滤条件

**等值过滤：**
```
{"SITE":"3100","ASSY_STATUS":"1"}
```

**范围过滤（支持 DATETIME 等类型）：**
```
{"CREATE_TIME":{"$gte":"2026-06-10 08:00:00","$lt":"2026-06-10 20:00:00"}}
```
支持的操作符：`$gt`（大于）、`$gte`（大于等于）、`$lt`（小于）、`$lte`（小于等于）

**混合使用：**
```
{"SITE":"3100","ASSY_STATUS":"1","CREATE_TIME":{"$gte":"2026-06-24 07:50:00"}}
```
等值过滤和范围过滤可同时使用。

### 排序

sort/order 参数指定排序，order 取值 asc/desc，如 `&sort=CREATE_TIME&order=desc`

### 分页

page 从 1 开始，size 最大 500，默认 50。

## 订单聚合接口

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | /api/orders/{orderNo}?site=3100 | 一次返回订单主表+客户名+明细列表 |

## 数采数据接口（电流/电压）

⚠️ **dc_ 开头的表（dc_station_to_electricity、dc_station_to_voltage 等）是数据采集大表，不支持通用表查询，必须使用专用接口。**

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | /api/dc/electricity?startTime=&endTime=&station=&page=&size= | 查询电流数据，startTime/endTime 必填 |
| GET | /api/dc/voltage?startTime=&endTime=&station=&page=&size= | 查询电压数据，startTime/endTime 必填 |

参数：startTime/endTime 格式 `yyyy-MM-dd HH:mm:ss`，station 可选，page 默认 1，size 默认 50 最大 500。

## 使用场景

当用户请求查询 MES 系统数据时，优先使用对应的聚合接口而非通用表查询。
- 查订单 → `/api/orders/{orderNo}?site=3100`
- 查表数据 → `/api/tables/{name}`
- 查表结构 → `/api/tables/{name}/columns`
- 查电流 → `/api/dc/electricity?startTime=&endTime=`
- 查电压 → `/api/dc/voltage?startTime=&endTime=`
