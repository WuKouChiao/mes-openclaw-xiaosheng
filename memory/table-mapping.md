# MES 表映射 — 小生知识库

> 小生通过此文件理解表 ↔ 业务概念映射。
> 使用方法：收到查询请求时，先用关键词搜索此文件找到对应表，调 mes-query-api 获取列注释和实际数据。
> 接口地址: http://192.168.1.103:8088

---

## 1. 订单模块

### 1.1 订单主表 — sd_order

| 字段 | 类型 | 含义 | 备注 |
|------|------|------|------|
| HANDLE | VARCHAR | 唯一标识 | 主键 |
| SITE | VARCHAR | 站点/工厂 | |
| ORDER_NO | VARCHAR | 销售订单号 | |
| ORDER_STATUS | VARCHAR | 订单状态 | 字典: order_status |
| ORDER_CATEGORY | VARCHAR | 订单类型 | ORDER=销售订单, OEM=采购订单 |
| ORDER_SOURCE | VARCHAR | 订单来源 | 字典: ORDER_SOURCE |
| CUSTOM_BO | VARCHAR | 客户ID | 关联 md_partner |
| CUSTOM_PO | VARCHAR | 外部客户PO | 客户来料单号 |
| EXPECT_DELIVERY_TIME | DATETIME | 预计交付日期 | |
| CUSTOM_REQUIRE_DELIVERY_TIME | DATETIME | 客户要求交付日期 | |
| DELIVERY_TIME | DATETIME | 实际完成交付日期 | |
| BOOK_TIME | DATETIME | 客户下单时间 | |
| PACKAGES | INT | 预计箱数/件数 | |
| REMARK | VARCHAR | 备注 | |
| CREATE_TIME | DATETIME | 创建时间 | |

#### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| CUSTOM_BO | md_partner | HANDLE | 拿客户名 PARTNER_NO / SHORT_NAME / PARTNER_DESC |
| HANDLE | sd_order_detail | ORDER_BO | 一对多，拿订单行项目 |

### 1.2 订单子表 — sd_order_detail

#### 业务知识

- **REAL_WEIGHT / REAL_QTY 有值** → 理货已执行，客户来料已到达工厂
- **REAL_WEIGHT / REAL_QTY 为空** → 来料尚未到达，待理货
- **理货流程：** 客户发货 → 工厂收货 → 理货（称重、点箱）→ 写入 REAL_WEIGHT/REAL_QTY
- **REAL_WEIGHT/REAL_QTY vs WEIGHT/QTY：** 后者是客户声明值，前者是工厂实际测量值，差异代表损耗/偏差

#### 字段说明

| 字段 | 类型 | 含义 | 备注 |
|------|------|------|------|
| HANDLE | VARCHAR | 唯一标识 | 主键 |
| ORDER_BO | VARCHAR | 订单主表BO | 关联 sd_order.HANDLE |
| SEQUENCE | DECIMAL | 序号 | 行号 |
| CUSTOM_SEQ | VARCHAR | 客户行编号 | |
| ORDER_DETAIL_STATUS | VARCHAR | 订单明细状态 | 字典: ORDER_DETAIL_STATUS |
| ORDER_PROGRESS_STATUS | VARCHAR | 订单进度状态 | 字典: ORDER_PROGRESS_STATUS |
| ORDER_DETAIL_CATEGORY | VARCHAR | 订单明细类型 | 字典: ORDER_DETAIL_CATEGORY |
| ITEM_BO | VARCHAR | 物料BO | 关联 md_item |
| CUSTOM_ITEM | VARCHAR | 客户物料编号 | |
| CUSTOM_ITEM_DESC | VARCHAR | 客户料号描述 | |
| CUSTOM_PLATING | VARCHAR | 客户镀种 | |
| PLATING_BO | BIGINT | 镀种BO | |
| PLATING | VARCHAR | 镀种 | |
| INSIDE_PLATING_NO | VARCHAR | 内部镀种 | |
| OUT_ORDER_PO | VARCHAR | 客户委外单号 | |
| OUT_CUSTOM_NO | VARCHAR | 最终客户代码 | 客户的客户 |
| IN_BATCH_NO | VARCHAR | 来料批次 | |
| WEIGHT | DECIMAL | 来料重量(KG) | |
| QTY | DECIMAL | 来料数量(KPCS) | |
| PACKAGES | INT | 来料箱数/件数 | |
| REAL_WEIGHT | DECIMAL | 理货重量(KG) | |
| REAL_QTY | DECIMAL | 理货数量(KPCS) | |
| REAL_PACKAGES | INT | 理货箱数 | |
| SINGLE_WEIGHT | DECIMAL | 标准单重 | 来自物料主数据 |
| REAL_SINGLE_WEIGHT | DECIMAL | 实际单重(KG) | |
| QTY_DELIVERY | DECIMAL | 交货数量(KPCS) | |
| QTY_WEIGHT | DECIMAL | 交货重量(KG) | |
| CONTROL_BATCH | VARCHAR | 收获批 | |
| REWORK_FLAG | VARCHAR | 是否返工 | 2=代返工, 1=客户返工, 0=否 |
| ORIGIN_ORDER_DETAIL_NO | VARCHAR | 返工单号 | |
| HYDROGEN_FLAG | VARCHAR | 是否除氢 | 1=是, 0=否 |
| HEAT_FLAG | VARCHAR | 是否热处理 | |
| IS_URGENT | INT | 是否急品 | 1=是, 0=否 |
| IS_SAMPLE | INT | 是否样品 | 1=是, 0=否 |
| PROCESS_CATEGORY | VARCHAR | 加工分类 | |
| PRODUCT_STAGE | VARCHAR | 产品阶段 | |
| MATERIAL_REQUIRE | VARCHAR | 材质要求 | |
| OUTSIDE_DIAMETER | VARCHAR | 外径控制(MM) | |
| MH_REQUIRE | VARCHAR | 膜厚要求 | |
| FB_REQUIRE | VARCHAR | 封闭要求 | |
| YW_REQUIRE | VARCHAR | 盐雾时间要求 | |
| REMARK | VARCHAR | 备注 | |
| CREATE_TIME | DATETIME | 创建时间 | |

#### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| ITEM_BO | md_item | HANDLE | 拿物料编码 ITEM / 描述 ITEM_DESC |
| SITE, CONTROL_BATCH | wm_inventory | SITE, CONTROL_BATCH | 组合键关联，查该批次库存信息 |
| SITE, CONTROL_BATCH | pd_sfc | SITE, CONTROL_BATCH | 组合键关联，查该批次在制 SFC 数据 |

### 1.3 业务规则

- **订单类型区分：** ORDER_CATEGORY 区分销售订单(Sales Order)和采购订单(Purchase Order)
- **关联关系：** sd_order_detail.ORDER_BO → sd_order.HANDLE

#### ORDER_STATUS 状态值

| 值 | 含义 | 说明 |
|------|------|------|
| TO_CONFIRM | 待确认 | 新建订单，尚未确认 |
| RELEASED | 已下达 | 已确认下达，进行中的订单 |
| COMPLETED | 已完成 | 订单执行完成 |
| CLOSED | 已关闭 | 订单归档关闭 |
| CANCEL | 已取消 | 订单已取消 |

#### ORDER_DETAIL_STATUS 状态值

| 值 | 含义 | 说明 |
|------|------|------|
| NORMAL | 正常 | 新建明细行 |
| RELEASED | 已下达 | 已下达生产 |
| CANCEL | 已取消 | 明细行已取消 |
| CLOSE | 已完工 | 生产完工 |
| HARD_CLOSE | 强制关闭 | 强制关闭 |
| CLOSED | 已关闭 | 归档关闭 |
| PARTIAL_DELIVERY | 部分交货 | 部分已交货 |

### 1.4 常见查询

```
Q: 查最近的销售订单
→ GET /api/tables/sd_order?filter={"ORDER_CATEGORY":"ORDER"}&sort=CREATE_TIME&order=desc&size=20
→ 注意：SITE 需要指定工厂，sort/order 保证返回最新记录

Q: 查采购订单
→ GET /api/tables/sd_order?filter={"ORDER_CATEGORY":"OEM"}&size=20

Q: 查某个订单的明细
→ GET /api/tables/sd_order_detail?filter={"ORDER_BO":"<订单HANDLE>"}

Q: 查某个客户的所有订单
→ GET /api/tables/sd_order?filter={"CUSTOM_BO":"<客户BO>","ORDER_CATEGORY":"ORDER"}

Q: 查正在进行的销售订单
→ GET /api/tables/sd_order?filter={"ORDER_CATEGORY":"ORDER","ORDER_STATUS":"RELEASED"}

Q: 查近一周新创建的订单
→ GET /api/tables/sd_order?filter={"ORDER_CATEGORY":"ORDER"}&size=50
→ 小生可在结果中过滤 CREATE_TIME
```

---

## 2. 客户/供应商 — md_partner

| 字段 | 含义 |
|------|------|
| HANDLE | 主键 |
| PARTNER_NO | 合作伙伴编号 |
| SHORT_NAME | 简称 |
| PARTNER_DESC | 全称 |
| PARTNER_CATEGORY | 类型（CUSTOMER=客户, M_VENDOR=供应商） |
| PARTNER_STATUS | 状态 |

---

## 3. 物料 — md_item

| 字段 | 含义 |
|------|------|
| HANDLE | 主键 |
| ITEM | 物料编码 |
| ITEM_DESC | 物料描述 |
| ITEM_CATEGORY | 类别（Y/Z/X/G/C） |
| ITEM_STATUS | 状态（RELEASED/HOLD） |
| UNIT_OF_MEASURE | 基本单位 |
| WEIGHT_UNIT | 标准单重 |

---

## 4. 库存 — wm_inventory

#### 业务知识

- **同一 CONTROL_BATCH 对应多笔库存记录是正常现象**：一个收货批入库后会产生多条库存行（如完工产出拆分为不同批次入库、不同货位存放等）
- **展示时按 CONTROL_BATCH 聚合**：将同一批次的多个库存行汇总显示 QTY_ON_HAND 合计和记录条数
- **每笔记录单独展示**：保留明细（货位、库存状态、数量），便于追溯

#### 字段说明

| 字段 | 含义 |
|------|------|
| HANDLE | 主键 |
| SITE | 站点 |
| INVENTORY_ID | 库存ID |
| ITEM_BO | 物料 |
| INVENTORY_STATUS | 库存状态 |
| QTY_ON_HAND | 数量 |
| ORIGINAL_QTY | 原始数量 |
| STORAGE_LOCATION_BO | 存储地点 |
| CONTROL_BATCH | 收货批 |
| INVENTORY_CATEGORY | 库存类型 |
| PARTNER_NO | 客户/供应商 |
| PACKAGES | 件数 |

#### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| SITE, ITEM_BO | md_item | SITE, HANDLE | 拿物料编码和描述 |
| SITE, CONTROL_BATCH | sd_order_detail | SITE, CONTROL_BATCH | 组合键关联，查来源订单明细 |
| SITE, REF_TYPE=INVENTORY, HANDLE | wm_goods_location_binding | SITE, REF_TYPE, REF_GBO | 三键关联，查库存所在货位 |

---

## 5. SFC 信息 — pd_sfc

#### 字段说明

| 字段 | 含义 |
|------|------|
| HANDLE | 主键 |
| SITE | 站点 |
| SFC | SFC 编码 |
| SFC_STATUS | SFC 状态 |
| SFC_CATEGORY | SFC 类别 |
| QTY | 数量 |
| QTY_SCRAPPED | 报废数量 |
| QTY_DONE | 完成数量 |
| QTY_ORIGINAL | 原始数量 |
| ACTUAL_START_DATE | 实际开始时间 |
| ACTUAL_COMP_DATE | 实际完成时间 |
| IS_NC | 是否不良 |
| UNIT_WEIGHT | 单位重量 |
| WEIGHT | 重量 |
| REF_TYPE | 关联类型(item/shopOrder/dispatch_no) |
| REF_GBO | 关联值 |
| CONTROL_BATCH | 收货批 |

#### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| SITE, REF_TYPE=SFC, HANDLE | wm_goods_location_binding | SITE, REF_TYPE, REF_GBO | 三键关联，查 WIP 所在货位 |
| REF_TYPE=shopOrder, REF_GBO | pp_shop_order | HANDLE | 关联生产工单 |
| REF_TYPE=item, REF_GBO | md_item | HANDLE | 关联物料 |

---

## 5.5 控制批次信息 — pd_control_batch

#### 业务知识

- **理货记录在此表**：理货人员（LH_USER）和理货时间（LH_TIME）记录在 pd_control_batch
- **理货数量**：QTY_LH 记录理货后的实际数量
- **关联订单**：通过 ORDER_NO 关联 sd_order，CONTROL_BATCH 关联 sd_order_detail

#### 理货相关字段

| 字段 | 含义 |
|------|------|
| LH_USER | 理货人 |
| LH_TIME | 理货时间 |
| QTY_LH | 理货数量 |

#### 常见查询

```
Q: 查看今天的理货情况
→ GET /api/tables/pd_control_batch?filter={"SITE":"3100"}&sort=LH_TIME&order=desc&size=50
→ 过滤 LH_TIME 为今天的记录，按理货时间倒序
```

---

## 5.6 投料/物料消耗记录 — pd_item_assy

#### 业务知识

- **pd_item_assy 是物料消耗记录表**，核心字段是 ASSY_STATUS（消耗状态），ASSY_MESSAGE 是辅助描述
- **"投料" = ASSY_STATUS=1**：库存(INVENTORY)物料投入到生产(SFC)
- 用户问"投料情况"时，过滤 `ASSY_STATUS=1`

#### ASSY_STATUS 状态值

| STATUS | ASSY_TYPE | ASSY_MESSAGE(描述) | 含义 |
|--------|------|------|------|
| 0 | CONTROL_BATCH | (空) | 批次级消耗 |
| 1 | INVENTORY | 投料 | 库存投料到生产 |
| 2 | SFC | 包装 | SFC间包装消耗 |
| 3 | SFC | 完工记录 | 完工物料消耗 |
| 6 | INVENTORY | 202包装消耗 | 202包装物料消耗 |
| 10 | INVENTORY | 201完工记录 | 201完工物料消耗 |

#### 关键字段

| 字段 | 含义 |
|------|------|
| ASSY_STATUS | 消耗状态（核心字段，用此字段筛选业务类型） |
| ASSY_MESSAGE | 消耗描述（辅助字段） |
| ASSY_TYPE | 消耗对象类型（INVENTORY/SFC/CONTROL_BATCH） |
| QTY | 消耗数量 |
| COMPONENT_ITEM_BO | 消耗物料 |
| CREATE_TIME | 消耗时间 |
| CREATE_BY | 操作人 |

#### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| COMPONENT_ITEM_BO | md_item | HANDLE | 拿物料编码和描述 |
| CREATE_BY | sys_user | USER_NO | 操作人姓名 |

#### 常见查询

```
Q: 查看今天的投料情况
→ GET /api/tables/pd_item_assy?filter={"SITE":"3100","ASSY_STATUS":"1"}&sort=CREATE_TIME&order=desc&size=50

Q: 查看今天全部物料消耗
→ GET /api/tables/pd_item_assy?filter={"SITE":"3100"}&sort=CREATE_TIME&order=desc&size=50

Q: 查包装消耗
→ GET /api/tables/pd_item_assy?filter={"SITE":"3100","ASSY_STATUS":"2"}&sort=CREATE_TIME&order=desc&size=50
```

---

## 6. 存储地点 — md_storage_location

| 字段 | 含义 |
|------|------|
| HANDLE | 主键 |
| SITE | 站点 |
| STORAGE_LOCATION | 存储地点编码 |
| STORAGE_LOCATION_DESC | 描述 |
| STORAGE_LOCATION_CATEGORY | 类别 |
| STORAGE_LOCATION_STATUS | 状态 |

### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| STORAGE_LOCATION | wm_inventory | STORAGE_LOCATION_BO | 库存记录通过此字段关联存储地点编码 |

The current date is 2026-06-25.

---

## 7. 货位主数据 — md_goods_location

| 字段 | 含义 |
|------|------|
| HANDLE | 主键 |
| SITE | 站点 |
| GOODS_LOCATION | 货位编码 |
| GOODS_LOCATION_GROUP | 货架 |
| GOODS_LOCATION_DESC | 描述 |
| GOODS_LOCATION_CATEGORY | 类别 |
| GOODS_LOCATION_STATUS | 状态 |
| STORAGE_LOCATION_BO | 存储地点 |

---

## 8. 货位绑定 — wm_goods_location_binding

#### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| GOODS_LOCATION_BO | md_goods_location | HANDLE | 拿货位编码和描述 |

#### 字段说明

| 字段 | 含义 |
|------|------|
| HANDLE | 主键 |
| SITE | 站点 |
| GOODS_LOCATION_BO | 货位 BO | 关联 md_goods_location.HANDLE |
| REF_TYPE | 上架类型（INVENTORY=库存，SFC=WIP） |
| REF_GBO | 上架值（关联来源表的 HANDLE） |
| QTY | 上架实时数量 |
| QTY_LOAD | 上架数量 |
| ITEM_BO | 物料 |
| PACKAGES | 箱/件数 |
| LOCATION | 位置 |

---

## 9. 系统用户 — sys_user

| 字段 | 含义 |
|------|------|
| HANDLE | 主键 |
| USER_NO | 用户编号 |
| USER_NAME | 用户姓名 |
| ROLE | 角色 |
| DEPARTMENT | 部门 |
| IS_DISABLE | 是否禁用 |
| EMAIL | 邮箱 |
| PHONE | 联系电话 |
| FACE_ID | 人脸ID |

### 通用规则

**所有表的 CREATE_BY 和 UPDATE_BY 字段都可以通过 USER_NO 关联 sys_user 获取用户姓名。**

例外：pd_control_batch.LH_USER（理货人）也关联 USER_NO。

查询理货人姓名示例：
```
先查 pd_control_batch 拿 LH_USER → 再查 sys_user filter={"USER_NO":"<LH_USER值>"} 拿 USER_NAME
```

### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| 任意表.CREATE_BY | sys_user | USER_NO | 创建人姓名 |
| 任意表.UPDATE_BY | sys_user | USER_NO | 更新人姓名 |
| pd_control_batch.LH_USER | sys_user | USER_NO | 理货人姓名 |

---

## 10. 批次拆合记录 — pd_lot_history

#### 业务知识

- **记录批次/库存/SFC 的拆分与合并操作**：OP_CATEGORY=SPLIT 为拆分，MERGE 为合并
- **FROM → TO 的物料流转**：FROM_REF_TYPE/GBO 为来源，TO_REF_TYPE/GBO 为目标

#### 关键字段

| 字段 | 含义 |
|------|------|
| OP_CATEGORY | 操作类型（SPLIT=拆分, MERGE=合并） |
| FROM_REF_TYPE | 来源类型（SFC/INVENTORY） |
| FROM_REF_GBO | 来源值 |
| TO_REF_TYPE | 目标类型（SFC/INVENTORY） |
| TO_REF_GBO | 目标值 |
| QTY | 操作数量 |
| OPERATION_BO | 工序 |
| RESOURCE_BO | 资源 |
| T_CODE | 事务码 |
| CREATE_TIME | 操作时间 |
| CREATE_BY | 操作人 |

---

## 11. 工序主数据 — md_operation

| 字段 | 含义 |
|------|------|
| HANDLE | 主键（OPERATION_BO 关联此字段） |
| SITE | 站点 |
| OPERATION | 工序编码 |
| OPERATION_DESC | 工序描述 |
| OPERATION_CATEGORY | 工序类别 |
| OPERATION_STATUS | 工序状态 |
| OPERATION_GROUP | 工序组 |
| ERP_OPERATION | ERP工序编号 |
| DEFAULT_RESOURCE_TYPE_BO | 默认资源类型 |

### 关联

| 从字段 | 到表 | 到字段 | 说明 |
|--------|------|--------|------|
| pd_item_assy.OPERATION_BO | md_operation | HANDLE | 消耗记录的工序信息 |
| pd_lot_history.OPERATION_BO | md_operation | HANDLE | 流转记录的工序信息 |

---

## 12. 生产日志 — pd_production_log

#### 业务知识

- **记录每个 SFC 在每道工序的生产过程**：包含工序、资源、物料、数量、时间等完整信息
- **产量统计**：QTY（生产数量）、QTY_SCRAPPED（报废）、QTY_DONE（完工入库）
- **工时统计**：START_TIME → COMPLETE_TIME → USED_TIME

#### 关键字段

| 字段 | 含义 |
|------|------|
| SFC | SFC编码 |
| SHOP_ORDER | 工单号 |
| DISPATCH_NO | 派工单号 |
| STATUS | 状态 |
| OPERATION | 工序编码 |
| OPERATION_DESC | 工序描述 |
| RESOURCE | 资源编码 |
| RESOURCE_DESC | 资源描述 |
| QTY | 生产数量 |
| QTY_SCRAPPED | 报废数量 |
| QTY_DONE | 完工入库数量 |
| START_TIME | 开始时间 |
| COMPLETE_TIME | 完成时间 |
| USED_TIME | 用时 |
| ACTIVITY | 操作作业 |
