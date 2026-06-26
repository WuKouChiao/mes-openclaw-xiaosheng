# MD 主数据表 — 小生知识库

> 小生通过此文件理解 md_* 主数据表 → 业务概念映射。
> 这些表定义了 MES 系统的核心主数据：物料(BOM)、工序(Router)、资源、工艺参数、NC 代码、产能等。
> 接口地址: http://192.168.1.103:8088

## 表目录

- [md_alternative](#md_alternative) — 替代料
- [md_bom](#md_bom) — BOM 主表
- [md_bom_component](#md_bom_component) — BOM 组件
- [md_bom_member](#md_bom_member) — BOM 成员
- [md_capacity](#md_capacity) — 产能
- [md_capacity_config](#md_capacity_config) — 产能配置
- [md_config_router](#md_config_router) — 配置工艺路线
- [md_config_router_detail](#md_config_router_detail) — 配置工艺路线明细
- [md_goods_location_member](#md_goods_location_member) — 货位成员
- [md_goods_location_resource_member](#md_goods_location_resource_member) — 货位资源成员
- [md_item_ean](#md_item_ean) — 物料 EAN 码
- [md_item_group_member](#md_item_group_member) — 物料组成员
- [md_item_lot](#md_item_lot) — 物料批次
- [md_item_process_param](#md_item_process_param) — 物料工艺参数
- [md_item_raw_sale](#md_item_raw_sale) — 物料原料销售
- [md_life](#md_life) — 生命周期
- [md_location_operation_seq](#md_location_operation_seq) — 货位工序顺序
- [md_logistics_path](#md_logistics_path) — 物流路径
- [md_main_router_param](#md_main_router_param) — 主工艺路线参数
- [md_master_router_matrix](#md_master_router_matrix) — 主工艺路线矩阵
- [md_mes_erp_movement_type_mapping](#md_mes_erp_movement_type_mapping) — MES-ERP 移动类型映射
- [md_nc_code](#md_nc_code) — NC（不良）代码
- [md_nc_group](#md_nc_group) — NC 代码组
- [md_nc_group_member](#md_nc_group_member) — NC 代码组成员
- [md_nc_group_ref](#md_nc_group_ref) — NC 代码组引用
- [md_operation_mapping](#md_operation_mapping) — 工序映射
- [md_operation_resource_type](#md_operation_resource_type) — 工序资源类型
- [md_param](#md_param) — 参数
- [md_param_disp](#md_param_disp) — 参数显示
- [md_param_link](#md_param_link) — 参数关联
- [md_print_template](#md_print_template) — 打印模板
- [md_processing_unit](#md_processing_unit) — 加工单元
- [md_processing_unit_member](#md_processing_unit_member) — 加工单元成员
- [md_prod_revision](#md_prod_revision) — 产品版本
- [md_program](#md_program) — 程序
- [md_program_group](#md_program_group) — 程序组
- [md_program_resource](#md_program_resource) — 程序资源
- [md_program_resource_param](#md_program_resource_param) — 程序资源参数
- [md_program_router](#md_program_router) — 程序工艺路线
- [md_resource](#md_resource) — 资源
- [md_resource_conf](#md_resource_conf) — 资源配置
- [md_resource_connect](#md_resource_connect) — 资源连接
- [md_resource_param](#md_resource_param) — 资源参数
- [md_resource_structure](#md_resource_structure) — 资源结构
- [md_resource_type](#md_resource_type) — 资源类型
- [md_resource_type_member](#md_resource_type_member) — 资源类型成员
- [md_resource_type_param_matrix](#md_resource_type_param_matrix) — 资源类型参数矩阵
- [md_rolling_plating_input_param](#md_rolling_plating_input_param) — 滚镀输入参数
- [md_router](#md_router) — 工艺路线
- [md_router_config](#md_router_config) — 工艺路线配置
- [md_router_config_detail](#md_router_config_detail) — 工艺路线配置明细
- [md_router_next_step](#md_router_next_step) — 工艺路线下一步
- [md_router_rolling_plating_en_param_recommend](#md_router_rolling_plating_en_param_recommend) — 滚镀 EN 参数推荐
- [md_router_step](#md_router_step) — 工艺路线步骤
- [md_router_step_conf](#md_router_step_conf) — 工艺路线步骤配置
- [md_router_step_dy_router](#md_router_step_dy_router) — 工艺路线步骤动态工艺路线
- [md_router_step_member](#md_router_step_member) — 工艺路线步骤成员
- [md_router_step_prop](#md_router_step_prop) — 工艺路线步骤属性
- [md_storage_location_member](#md_storage_location_member) — 存储地点成员
- [md_task_event](#md_task_event) — 任务事件
- [md_task_item](#md_task_item) — 任务项
- [md_task_obj](#md_task_obj) — 任务对象
- [md_task_obj_member](#md_task_obj_member) — 任务对象成员
- [md_task_operation](#md_task_operation) — 任务操作
- [md_task_plan](#md_task_plan) — 任务计划
- [md_user_quick_access](#md_user_quick_access) — 用户快捷访问
- [md_wip_monitor](#md_wip_monitor) — WIP 监控
- [md_work_center](#md_work_center) — 工作中心
- [md_work_center_member](#md_work_center_member) — 工作中心成员

---
- [md_processing_unit](#md_processing_unit) — 加工单元
- [md_processing_unit_member](#md_processing_unit_member) — 加工单元成员
- [md_prod_revision](#md_prod_revision) — 产品版本（修订版）
- [md_program](#md_program) — 程序（NC 程序等）
- [md_program_group](#md_program_group) — 程序组
- [md_program_resource](#md_program_resource) — 程序-资源关联
- [md_program_resource_param](#md_program_resource_param) — 程序资源参数
- [md_program_router](#md_program_router) — 程序工艺路线
- [md_resource](#md_resource) — 资源（设备、工装等）
- [md_resource_conf](#md_resource_conf) — 资源配置
- [md_resource_connect](#md_resource_connect) — 资源连接关系
- [md_resource_param](#md_resource_param) — 资源参数
- [md_resource_structure](#md_resource_structure) — 资源结构（设备层级）
- [md_resource_type](#md_resource_type) — 资源类型（设备类别）
- [md_resource_type_member](#md_resource_type_member) — 资源类型成员
- [md_resource_type_param_matrix](#md_resource_type_param_matrix) — 资源类型参数矩阵
- [md_rolling_plating_input_param](#md_rolling_plating_input_param) — 滚镀输入参数
- [md_router](#md_router) — 工艺路线主表
- [md_router_config](#md_router_config) — 工艺路线配置
- [md_router_config_detail](#md_router_config_detail) — 工艺路线配置明细
- [md_router_next_step](#md_router_next_step) — 工艺路线下一步骤
- [md_router_rolling_plating_en_param_recommend](#md_router_rolling_plating_en_param_recommend) — 滚镀 EN 参数推荐
- [md_router_step](#md_router_step) — 工艺路线步骤定义
- [md_router_step_conf](#md_router_step_conf) — 工艺路线步骤配置
- [md_router_step_dy_router](#md_router_step_dy_router) — 工艺路线步骤动态工艺路线
- [md_router_step_member](#md_router_step_member) — 工艺路线步骤成员
- [md_router_step_prop](#md_router_step_prop) — 工艺路线步骤属性
- [md_storage_location_member](#md_storage_location_member) — 存储地点成员
- [md_task_event](#md_task_event) — 任务事件
- [md_task_item](#md_task_item) — 任务项
- [md_task_obj](#md_task_obj) — 任务对象
- [md_task_obj_member](#md_task_obj_member) — 任务对象成员
- [md_task_operation](#md_task_operation) — 任务操作
- [md_task_plan](#md_task_plan) — 任务计划
- [md_user_quick_access](#md_user_quick_access) — 用户快捷访问配置
- [md_wip_monitor](#md_wip_monitor) — WIP 监控配置
- [md_work_center](#md_work_center) — 工作中心
- [md_work_center_member](#md_work_center_member) — 工作中心成员

---

## md_alternative
> 替代料/替代物料关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| REF_TYPE | varchar(100) | 关联类型) |
| REF_GBO | varchar(412) | 关联值 |
| SEQUENCE | decimal(18,0) | 序号 |
| COMPONENT_ITEM_BO | varchar(412) | 替代料 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_bom
> BOM 主表（物料清单）

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| BOM | varchar(50) | BOM编号 |
| BOM_DESC | varchar(100) | BOM描述 |
| BOM_REVISION | varchar(30) | BOM版本 |
| CURRENT_REVISION | varchar(1) | 当前版本 |
| BOM_CATEGORY | varchar(30) | BOM类别(主数据；工单；工装；辅料；配方) |
| BOM_STATUS | varchar(30) | BOM状态 |
| REMARK | varchar(500) | 备注 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_bom_component
> BOM 组件定义

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| BOM_BO | varchar(412) | BOM主键 |
| SEQUENCE | decimal(18,0) | 序号 |
| COMP_GROUP | decimal(18,0) | 组件组 |
| COMP_CATEGORY | varchar(30) | 类别 |
| COMPONENT_GBO | varchar(412) | 组件物料 |
| REF_TYPE | varchar(100) |  |
| REF_OBJ | varchar(412) | 工序 |
| QTY_USE_TYPE | varchar(30) | 用量类型 |
| QTY_USE | decimal(18,6) | 用量 |
| QTY_USE_FN | varchar(100) | 公式 |
| DEVIATION_TYPE | varchar(30) | 偏差类型 |
| DEVIATION_UPPER | varchar(30) | 偏差上限 |
| DEVIATION_LOWER | varchar(30) | 偏差下限 |
| ENABLE | varchar(1) | 是否启用 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
| IS_CONFIRM | varchar(2) | 是否复核(Y/N) |
| ASSY_TYPE | varchar(30) | 消耗类型 |
| REF_PARAM | varchar(100) | 关联参数 |
| LOSS_TYPE | varchar(30) | 损耗类型 |
| LOSS_QTY | decimal(18,6) | 损耗 |

## md_bom_member
> BOM 成员关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| BOM_BO | varchar(412) | BOM主键 |
| REF_TYPE | varchar(30) | 关联类型(物料；工单；加工批次；资源；工作中心) |
| REF_GBO | varchar(412) | 关联值 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_capacity
> 产能定义

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型(设备.工作中心) |
| REF_GBO | varchar(412) | 关联BO |
| CAPACITY_TYPE | varchar(30) | 关联类型(物料.物料组) |
| CAPACITY_OBJ | varchar(30) | 关联值 |
| UNIT_TIME | decimal(18,0) | 单位时间 |
| QTY_CAPACITY | decimal(18,0) | 产能 |
| QTY_UNIT | varchar(30) | 单位 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_capacity_config
> 产能配置参数

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型(设备/工作中心) |
| REF_GBO | varchar(412) | 关联BO |
| SHIFT | varchar(30) | 班次 |
| DZ_TYPE | varchar(50) | 镀种类型 |
| UNIT_TIME | decimal(18,2) | 单位时间(小时) |
| QTY_CAPACITY | decimal(18,3) | 产能 |
| CREATE_BY | varchar(32) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(32) | 更新人 |
| UPDATE_TIME | datetime(3) | 更新时间 |

## md_config_router
> 配置型工艺路线

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| ITEM | varchar(500) | 内部镀种 |
| OUT_CUSTOM_NO | varchar(500) | 业体(最终客户) |
| PARTNER_NO | varchar(500) | 客户代号 |
| PLATING_CLASS | varchar(500) | 大类 |
| HEAT_TREAT | varchar(500) | 热处理 |
| SURFACE_AREA | varchar(500) | 表面积 |
| ROD_DIAMETER | varchar(500) | 杆径 |
| MH_UPPER | varchar(500) | 膜厚上限 |
| MH_STANARD | varchar(500) | 膜厚标准 |
| MH_LOWER | varchar(500) | 膜厚下限 |
| FB_TYPE | varchar(500) | 封闭类型 |
| HX_TIME | varchar(500) | 红锈时间 |
| BX_TIME | varchar(500) | 白锈时间 |
| CQ_TIME | varchar(500) | 膜厚标准 |
| PARAM_K | varchar(500) | K值 |
| MATERIAL_REQUIRE | varchar(500) | 材质 |
| PURPOSE | varchar(500) | 用途 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_config_router_detail
> 配置型工艺路线明细

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| CONFIG_ROUTER_BO | varchar(412) | 配置主表 |
| IS_CURRENT | varchar(2) | 当前版本 |
| ROUTER | varchar(100) | 工艺路线 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |


## md_goods_location_member
> 货位成员关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| GOODS_LOCATION_BO | varchar(412) | 货位BO |
| SITE | varchar(32) | 站点 |
| SEQUENCE | decimal(18,0) | 序号 |
| ENABLE | varchar(1) | 是否启用 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_OBJ | varchar(100) | 关联BO |
| CONTR_TYPE | varchar(30) | 管控类型 |
| WARN_QTY | decimal(18,6) | 预警容量 |
| MAX_QTY | decimal(18,6) | 预警容量 |
| MAX_TIME | decimal(18,6) | 最长在架时间(h) |
| CALL_TYPE | varchar(30) | 叫料类型 |
| REMARK | varchar(100) | 备注 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_goods_location_resource_member
> 货位-资源成员关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| GOODS_LOCATION_BO | varchar(412) | 货位BO |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_OBJ | varchar(100) | 关联BO |
| REMARK | varchar(100) | 备注 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |


## md_item_ean
> 物料的 EAN 条码

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| ITEM_BO | varchar(412) | 物料BO |
| SEQUENCE | decimal(18,0) | 序号 |
| EAN | varchar(50) | EAN |
| BASIC_UNIT | varchar(100) | 基本单位 |
| BASIC_QTY | decimal(18,6) | 基本数量 |
| TRANS_UNIT | varchar(100) | 转换单位 |
| TRANS_QTY | decimal(18,6) | 转换数量 |
| ENABLE | varchar(1) | 是否启用 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_item_group_member
> 物料组成员

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| ITEM_BO | varchar(412) | 物料BO |
| SEQUENCE | decimal(18,0) | 序号 |
| ITEM_GROUP | varchar(100) | 物料组 |
| ENABLE | varchar(1) | 是否启用 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_item_lot
> 物料批次属性

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| ITEM_BO | varchar(412) | 物料BO |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_OBJ | varchar(100) | 关联对象 |
| LOT_SIZE | decimal(18,6) | 批量 |
| UNIT | varchar(30) | 单位 |
| DEVIATION_TYPE | varchar(30) | 偏差类型 |
| STA_QTY | decimal(18,6) | 标准值 |
| DEVIATION_UPPER | decimal(18,6) | 上偏差 |
| DEVIATION_LOWER | decimal(18,6) | 下偏差 |
| ENABLE | varchar(1) | 是否启用 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_item_process_param
> 物料的工艺参数

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| EN_ITEM | varchar(50) | EN物料编码 |
| WEIGHT_UNIT | varchar(50) | 单重 |
| PARTNER_NO | varchar(50) | 客户编码 |
| ITEM | varchar(50) | 内部镀种编号 |
| PLATING_CLASS | varchar(50) | 大类 |
| HEAT_TREAT | varchar(50) | 热处理 |
| OUT_CUSTOM_NO | varchar(50) | 终客户 |
| SURFACE_AREA | varchar(50) | 表面积 |
| ROD_DIAMETER | varchar(50) | 杆径 |
| MATERIAL_REQUIRE | varchar(50) | 材质 |
| MH_UPPER | varchar(50) | 膜厚上限 |
| MH_LOWER | varchar(50) | 膜厚下限 |
| MH_STANARD | varchar(50) | 膜厚标准 |
| FB_TYPE | varchar(50) | 封闭类型 |
| HX_TIME | varchar(50) | 红锈时间 |
| BX_TIME | varchar(50) | 白锈时间 |
| CQ_TIME | varchar(50) | 除氢时间 |
| PURPOSE | varchar(50) | 用途 |
| PARAM_K | varchar(50) | K值 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_item_raw_sale
> 物料原料销售信息

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点 |
| ITEM | varchar(200) | 物料 |
| ITEM_DESC | varchar(300) | 物料描述 |
| YEAR_STR | varchar(4) | 年份 |
| MONTH_STR | varchar(2) | 月份 |
| PRICE | decimal(10,6) | 不含税单价 |
| RATE | decimal(10,3) | 税率 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |

## md_life
> 生命周期定义

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联BO |
| INIT_LIFE | decimal(18,0) | 初始寿命 |
| CURRENT_LIFE | decimal(18,0) | 当前寿命 |
| WARN_LIFE | decimal(18,0) | 预警寿命 |
| MAX_LIFE | decimal(18,0) | 最大寿命 |
| IS_ALLOW_LIFE | varchar(1) | 是否允许延长寿命 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_location_operation_seq
> 货位工序顺序

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| FILE_BO | varchar(412) | 文件配置BO |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(500) | 类型 |
| REF_OBJ_DESC | varchar(500) | 对象描述 |
| REF_OBJ | varchar(500) | 对象 |
| PARENT_BO | varchar(412) | 父Bo |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_logistics_path
> 物流路径

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| SEQUENCE | decimal(18,0) | 序号 |
| FROM_TYPE | varchar(30) | 来源类型如果TRANS_TYPE是IN 来源类型就是RESOURCE反之是传入的类型 |
| FROM_OBJ | varchar(100) | 来源对象 |
| TO_TYPE | varchar(30) | 目标类型如果TRANS_TYPE是IN 来源类型是传入的类型反之是RESOURCE |
| TO_OBJ | varchar(100) | 目标对象 |
| CONT_TYPE | varchar(30) | 控制类型 |
| CONT_OBJ | varchar(100) | 控制对象 |
| ENABLE | varchar(1) | 是否启用 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_main_router_param
> 主工艺路线参数

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| FILE_BO | varchar(412) | 文件配置BO |
| SEQUENCE | decimal(18,0) | 序号 |
| YW_REQUIRE | varchar(500) | 盐雾要求 |
| ITEM | varchar(500) | 内部镀种 |
| MH_REQUIRE | varchar(500) | 厚度 |
| OUT_CUSTOM_NO | varchar(500) | 业体(最终客户) |
| PARTNER_NO | varchar(500) | 客户代号 |
| MATERIAL_REQUIRE | varchar(500) | 材质 |
| ROUTER | varchar(500) | 工艺路线 |
| PURPOSE | varchar(500) | 用途 |
| SHORT_NAME | varchar(500) | 客户简称 |
| PARENT_BO | varchar(412) | 父Bo |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_master_router_matrix
> 主工艺路线矩阵

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| FILE_BO | varchar(412) | 文件配置BO |
| SEQUENCE | decimal(18,0) | 序号 |
| ITEM | varchar(500) | 物料 |
| ITEM_GROUP | varchar(500) | 物料组 |
| SUB_PROCESS_ROUTE_TYPE | varchar(500) | 主工艺 |
| FACTORY | varchar(500) | 工厂 |
| PARENT_BO | varchar(412) | 父Bo |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_mes_erp_movement_type_mapping
> MES 与 ERP 移动类型映射

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | bigint | 主键 |
| SITE | varchar(10) | 站点 |
| MOVEMENT_TYPE | varchar(100) | MES-移动类型 |
| ERP_MOVEMENT_TYPE | varchar(100) | ERP-移动类型 |
| CREATE_BY | varchar(32) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(32) | 更新人 |
| UPDATE_TIME | datetime(3) | 更新时间 |

## md_nc_code
> NC（不良）代码

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点/工厂 |
| NC_CODE | varchar(412) | 代码 |
| NC_CODE_DESC | varchar(20) | 代码描述 |
| MODULE_NO | varchar(20) | 处置功能 |
| REMARK | varchar(100) | 备注 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |
| MODULE_PARAM | longtext | 模组参数 |
| NC_CODE_TYPE | varchar(30) | 代码类型 |
| VIEW_PLUGIN | varchar(100) | 插件 |
| PARAM_GROUP | varchar(100) | 参数组 |
| NC_CODE_LEVEL | varchar(10) | 代码等级 |

## md_nc_group
> NC 代码分组

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点/工厂 |
| NC_GROUP | varchar(50) | 代码组 |
| NC_GROUP_DESC | varchar(20) | 代码组描述 |
| NC_GROUP_STATUS | varchar(20) | 状态 |
| NC_GROUP_CATEGORY | varchar(20) | 类型 |
| REMARK | varchar(100) | 备注 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |
| NC_GROUP_TYPE | varchar(30) | 代码组类型 |

## md_nc_group_member
> NC 代码组成员

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点/工厂 |
| NC_GROUP_BO | varchar(412) | 检验任务表bo |
| SEQUENCE | int | 序号 |
| NC_CODE_BO | varchar(412) | 关联类型 |
| REMARK | varchar(100) | 备注 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |

## md_nc_group_ref
> NC 代码组引用关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点/工厂 |
| NC_GROUP_BO | varchar(412) | 检验任务表bo |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(50) | 关联类型 |
| REF_GBO | varchar(412) | 关联对象 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |


## md_operation_mapping
> 工序映射关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) |  |
| SITE | varchar(32) |  |
| EN_OPERATION | varchar(50) |  |
| EN_OPERATION_DESC | varchar(100) |  |
| EN_SUB_OPERATION | varchar(50) |  |
| EN_SUB_OPERATION_DESC | varchar(100) |  |
| MES_OPERATION | varchar(50) |  |
| MES_OPERATION_DESC | varchar(100) |  |
| MES_OPERATION_CATEGORY | varchar(30) |  |
| REMARK | varchar(255) |  |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_operation_resource_type
> 工序-资源类型关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| FILE_BO | varchar(412) | 文件配置BO |
| SEQUENCE | decimal(18,0) | 序号 |
| OPERATION | varchar(500) | 工序 |
| RESOURCE_TYPE | varchar(500) | 资源类型 |
| PARENT_BO | varchar(412) | 父Bo |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_param
> 参数定义

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| APPLY_TYPE | varchar(20) | 应用类型(RESOURCE_TYPE) |
| APPLY_GBO | varchar(412) | 应用对象HANDLE |
| SEQUENCE | decimal(18,0) | 序号 |
| PARAM_NO | varchar(50) | 参数 |
| STAND_VALUE | varchar(500) | 标准值 |
| STAND_VALUE_LOWER | varchar(500) | 标准下限 |
| STAND_VALUE_UPPER | varchar(500) | 标准上限 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
| ISSUED_TYPE | varchar(20) | 下发类型 |
| DC_TYPE | varchar(20) | 数采类型 |

## md_param_disp
> 参数显示配置

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| APPLY_TYPE | varchar(50) | 应用类型(RESOURCE_TYPE) |
| APPLY_GBO | varchar(412) | 应用对象HANDLE |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(50) | 关联类型 |
| REF_OBJ | varchar(50) | 关联对象 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_param_link
> 参数关联关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) |  |
| SITE | varchar(10) |  |
| FROM_PARAM_DISP_BO | varchar(412) |  |
| TO_PARAM_DISP_BO | varchar(412) |  |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |


## md_print_template
> 打印模板

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| FILE_BO | varchar(412) | 文件配置BO |
| SEQUENCE | decimal(18,0) | 序号 |
| TEMPLATE | varchar(500) | 模版名 |
| TEMPLATE_GROUP | varchar(500) | 模版组 |
| CUSTOMER_NO | varchar(500) | 客户 |
| PARENT_BO | varchar(412) | 父Bo |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_processing_unit
> 加工单元

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| PU_ID | varchar(50) | PU编号 |
| PU_NAME | varchar(100) | PU名称 |
| LINE_ID | varchar(50) | 所属线体 |
| LINE_NAME | varchar(100) | 线体名称 |
| STAGE_ID | varchar(50) | 所属阶段 |
| IS_AUTOMATIC | varchar(1) | 是否自动线 |
| APPLICABLE_PRODUCT_TYPES | varchar(500) | 适用产品类型 |
| SUPPORTED_VARIANTS | varchar(500) | 支持工艺方式 |
| TANK_SEQUENCE | varchar(500) | 槽序列 |
| TANK_COUNT | int | 槽数量 |
| IS_SEQUENCE_FIXED | varchar(1) | 槽序是否固定 |
| STATUS | varchar(50) | PU状态 |
| IS_ACTIVE | varchar(1) | 是否启用 |
| PU_GROUP | varchar(100) | PU组 |
| PU_TYPE | varchar(50) | PU类型 |
| CREATE_BY | varchar(32) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(32) | 更新人 |
| UPDATE_TIME | datetime(3) | 更新时间 |

## md_processing_unit_member
> 加工单元成员

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| PROCESSING_UNIT_BO | varchar(412) | PU表BO |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联BO |
| CREATE_BY | varchar(32) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(32) | 更新人 |
| UPDATE_TIME | datetime(3) | 更新时间 |

## md_prod_revision
> 产品版本（修订版）

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联对象 |
| USED_TYPE | varchar(30) | 使用类型 |
| USED_OBJ | varchar(50) | 使用对象 |
| USED_REVISION | varchar(30) | 使用版本 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_program
> 程序（NC 程序等）

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| PROGRAM_NO | varchar(50) | 程序号 |
| PROGRAM_DESC | varchar(100) | 描述 |
| PROGRAM_STATUS | varchar(50) | 状态 |
| PROGRAM_CATEGORY | varchar(50) | 类别 |
| PROGRAM_GROUP | varchar(50) | 程序号组-滚镀线 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_program_group
> 程序组

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| GROUP_CATEGORY | varchar(50) | 分类 |
| SEQUENCE | decimal(16,3) | 序号 |
| IS_FLAG | varchar(2) | 是否比对 |
| RESOURCE_BO | varchar(50) | 资源BO |
| RESOURCE | varchar(50) | 资源 |
| RESOURCE_DESC | varchar(100) | 资源描述 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_program_resource
> 程序-资源关联

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| PROGRAM_BO | varchar(412) | 程序号主表 |
| RESOURCE_BO | varchar(412) | 资源BO |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_program_resource_param
> 程序资源参数

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| PROGRAM_BO | varchar(412) | 程序号主表 |
| PROGRAM_RESOURCE_BO | varchar(412) | 程序号资源配置BO |
| PARAM | varchar(50) | 参数 |
| VALUE | varchar(100) | 值 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_program_router
> 程序工艺路线

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| PROGRAM_BO | varchar(412) | 程序号主表 |
| ROUTER_BO | varchar(412) | 工艺路线BO |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_resource
> 资源（设备、工装等）

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| RESOURCE | varchar(50) | 资源编号 |
| RESOURCE_DESC | varchar(100) | 资源描述 |
| RESOURCE_STATUS | varchar(50) | 资源状态 |
| RESOURCE_CATEGORY | varchar(50) | 资源类别 |
| IS_LC | varchar(1) | 是否流程资源 |
| ASSET_NO | varchar(50) | 资产号 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
| MODEL | varchar(50) |  |

## md_resource_conf
> 资源配置

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联对象 |
| OPERATION | varchar(50) | 工序 |
| CONF_TYPE | varchar(30) | 配置类型 |
| CONF_OBJ | varchar(50) | 配置对象 |
| ENABLE | varchar(1) | 是否启用 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_resource_connect
> 资源连接关系

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联BO |
| ON_LINE | varchar(1) | 连接状态Y/N |
| OFF_LINE_TIME | decimal(18,0) | 超时多长时间为离线 |
| IP | varchar(50) | IP |
| CONNECT_TYPE | varchar(30) | 连接类型 |
| CONNECT_PROT | varchar(50) | 协议 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_resource_param
> 资源参数

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联BO |
| CATEGORY_NO | varchar(500) | 类别编号 |
| SEQUENCE | decimal(18,0) | 序号 |
| PARAM_TYPE | varchar(30) | 参数类型KJ  开机参数    PC 过程参数 |
| STAND_PARAM | varchar(50) | 标准参数 |
| STAND_PARAM_DESC | varchar(100) | 标准参数描述 |
| STAND_PARAM_UNIT | varchar(30) | 标准参数单位 |
| RESOURCE_PARAM | varchar(50) | 设备参数 |
| STAND_VALUE | varchar(30) | 标准值 |
| STAND_VALUE_UPPER | varchar(30) | 标准值上限 |
| STAND_VALUE_LOWER | varchar(30) | 标准值下限 |
| DC_TYPE | varchar(30) | 采集方式 |
| DC_TIMES | varchar(30) | 采集频率 |
| ENABLE_SPC | varchar(1) | SPC Y/N |
| VALUE_FN | varchar(100) | 公式 |
| WARNING_RULE | varchar(500) | 报警规则 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_resource_structure
> 资源结构（设备层级）

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| RESOURCE_BO | varchar(412) | 资源主键 |
| SEQUENCE | varchar(32) | 序号 |
| STRUCTURE_NO | varchar(32) | 结构编号 |
| STRUCTURE_STATUS | varchar(30) | 结构状态 |
| STRUCTURE_CATEGORY | varchar(50) | 结构类别 |
| STRUCTURE_DESC | varchar(255) | 结构描述 |
| LOGISTIC_CONTROL | varchar(32) | 物流控制 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
| RESOURCE_ACCESS | varchar(30) | 资源接入 |
| IP | varchar(20) | IP |
| PORT | varchar(10) | 端口 |

## md_resource_type
> 资源类型（设备类别）

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| RESOURCE_TYPE | varchar(50) | 资源类型编号 |
| RESOURCE_TYPE_DESC | varchar(100) | 资源类型描述 |
| RESOURCE_TYPE_STATUS | varchar(50) | 资源类型状态 |
| RESOURCE_TYPE_CATEGORY | varchar(50) | 资源类型类别 |
| DEFAULT_OPERATION | varchar(50) | 默认工序 |
| REMARK | varchar(500) | 备注 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_resource_type_member
> 资源类型成员

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| RESOURCE_TYPE_BO | varchar(412) | 资源类型BO |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联BO |
| ENABLE | varchar(10) | 是否启用 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_resource_type_param_matrix
> 资源类型参数矩阵

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| FILE_BO | varchar(412) | 文件配置BO |
| SEQUENCE | decimal(18,0) | 序号 |
| ITEM | varchar(500) | 内部镀种 |
| YW_REQUIRE | varchar(500) | 盐雾要求 |
| MH_REQUIRE | varchar(500) | 厚度 |
| OUT_CUSTOM_NO | varchar(500) | 业体(最终客户) |
| PARTNER_NO | varchar(500) | 客户代号 |
| OPERATION | varchar(500) | 工序 |
| MATERIAL_REQUIRE | varchar(500) | 材质 |
| PURPOSE | varchar(500) | 用途 |
| SHORT_NAME | varchar(500) | 客户简称 |
| RESOURCE_TYPE | varchar(500) | 资源类型 |
| PROCESS_TIME | varchar(500) | 工艺时间 |
| PARENT_BO | varchar(412) | 父Bo |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_rolling_plating_input_param
> 滚镀输入参数

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | bigint | 主键 |
| SITE | varchar(10) | 站点 |
| GD_WORK_CENTER_BO | varchar(412) | 滚镀工作中心BO |
| EN_ITEM | varchar(50) | EN编码 |
| PROGRAM_NO | varchar(100) | 程序号 |
| PRODUCT_SURFACE_AREA | varchar(255) | 表面积 |
| DD_NZ_DENSITY | varchar(50) | 锌镍槽的电流密度 |
| DD_ZN_DENSITY | varchar(50) | 酸锌槽的电流密度 |
| RECOMMENDED_QTY | decimal(18,3) | 推荐装载量 |
| FB_WORK_CENTER_BO | varchar(50) | 封闭工作中心 |
| FB_OPERATION | varchar(50) | 封闭类型 |
| CREATE_BY | varchar(32) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(32) | 更新人 |
| UPDATE_TIME | datetime(3) | 更新时间 |
| CUSTOM_ITEM | varchar(128) | 客户物料 |
| CUSTOM_ITEM_DESC | varchar(255) | 客户物料描述 |
| CUSTOM_PLATING | varchar(50) | 客户镀种 |
| CQ_TIME | varchar(20) | 除氢时间 |
| HEAT_FLAG | varchar(50) | 是否热处理 |
| MATERIAL_REQUIRE | varchar(50) | 材质要求 |
| OUTSIDE_CONTROL | varchar(50) | 外径控制(MM) |
| RECOMMEND_REASON | varchar(255) | 推荐原因 |
| DD_DJ_DENSITY | varchar(50) | 电解槽的电流密度 |

## md_router
> 工艺路线主表

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| ROUTER | varchar(50) | 工艺路线 |
| ROUTER_REVISION | varchar(10) | 版本 |
| CURRENT_REVISION | varchar(1) | 当前版本 |
| ROUTER_DESC | varchar(100) | 描述 |
| ROUTER_CATEGORY | varchar(30) | 类别 |
| ROUTER_STATUS | varchar(30) | 状态 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
| ROUTER_GROUP | varchar(50) | 工艺组 |

## md_router_config
> 工艺路线配置

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| ITEM | varchar(50) | 内部镀种 |
| YW_REQUIRE | varchar(200) | 盐雾要求 |
| MH_REQUIRE | varchar(200) | 厚度 |
| OUT_CUSTOM_NO | varchar(200) | 业体(最终客户) |
| PARTNER_NO | varchar(200) | 客户代号 |
| MATERIAL_REQUIRE | varchar(200) | 材质 |
| PURPOSE | varchar(200) | 用途 |
| SHORT_NAME | varchar(50) | 客户简称 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_router_config_detail
> 工艺路线配置明细

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| ROUTER_CONFIG_BO | varchar(412) |  |
| ROUTER_BO | varchar(412) | 工艺路线 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_router_next_step
> 工艺路线下一步骤

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) |  |
| SITE | varchar(10) |  |
| SEQUENCE | decimal(38,0) |  |
| ROUTER_BO | varchar(412) |  |
| CURRENT_ROUTER_STEP_BO | varchar(412) |  |
| NEXT_ROUTER_STEP_BO | varchar(412) |  |
| NEXT_STEP_DESC | varchar(50) |  |
| FROM_PORT | varchar(50) |  |
| TO_PORT | varchar(50) |  |
| TRANS_SCRIPT | varchar(2000) |  |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_router_rolling_plating_en_param_recommend
> 滚镀 EN 参数推荐

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | bigint | 主键 |
| SITE | varchar(10) | 站点 |
| ROUTER | varchar(50) | 工艺路线编码 |
| PROGRAM_NO | varchar(100) | 程序号 |
| PRODUCT_SURFACE_AREA | varchar(255) | 表面积 |
| DD_NZ_DENSITY | varchar(50) | 锌镍槽的电流密度 |
| DD_ZN_DENSITY | varchar(50) | 酸锌槽的电流密度 |
| RECOMMENDED_QTY | decimal(18,3) | 推荐装载量 |
| FB_OPERATION | varchar(50) | 封闭类型 |
| CREATE_BY | varchar(32) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(32) | 更新人 |
| UPDATE_TIME | datetime(3) | 更新时间 |
| EN_ITEM | varchar(50) | EN编码 |
| STATUS | varchar(20) | 状态(OPEN/CLOSE) |
| VERSION | varchar(5) | 版本号 |
| RECOMMEND_REASON | varchar(255) | 推荐原因 |
| CQ_TIME | varchar(20) | 除氢时间 |
| CUSTOM_ITEM | varchar(128) | 客户物料编号 |
| CUSTOM_ITEM_DESC | varchar(128) | 客户料号描述 |
| CUSTOM_PLATING | varchar(50) | 客户镀种 |
| HEAT_FLAG | varchar(50) | 是否热处理 |
| MATERIAL_REQUIRE | varchar(50) | 材质要求 |
| OUTSIDE_CONTROL | varchar(255) | 外径控制(MM) |
| DD_DJ_DENSITY | varchar(50) | 电解槽的电流密度 |


## md_router_step
> 工艺路线步骤定义

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) |  |
| SITE | varchar(10) |  |
| ROUTER_BO | varchar(412) |  |
| SEQUENCE | decimal(18,0) |  |
| IS_FIRST | varchar(1) |  |
| IS_DISPATCH | varchar(1) |  |
| STEP_ID | varchar(32) |  |
| STEP_CATEGORY | varchar(20) |  |
| PASS_RULE | varchar(20) |  |
| PASS_COUNT | decimal(18,0) |  |
| STEP_DESC | varchar(500) |  |
| ERP_OPERATION | varchar(20) |  |
| STEP_LOC | varchar(500) |  |
| IS_PASS | varchar(10) |  |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
| CONF | varchar(200) |  |
| REF_CATEGORY_NO | varchar(100) |  |
| DY_ROUTER | varchar(30) | 动态工艺 |
| IS_GROUP | varchar(1) |  |
| GROUP_BO | varchar(412) |  |

## md_router_step_conf
> 工艺路线步骤配置

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| ROUTER_BO | varchar(412) | 工艺路线主键 |
| ROUTER_STEP_BO | varchar(412) | 工艺路线步骤主键 |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(50) | 关联类型 |
| REF_OBJ | varchar(50) | 关联对象 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_router_step_dy_router
> 工艺路线步骤动态工艺路线

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) |  |
| SITE | varchar(10) |  |
| MD_ROUTER_BO | varchar(412) | 工艺路线主键 |
| MD_ROUTER_STEP_BO | varchar(412) | 工艺路线步骤主键 |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(50) | 关联类型 |
| REF_OBJ | varchar(50) | 关联对象 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_router_step_member
> 工艺路线步骤成员

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) |  |
| SITE | varchar(10) |  |
| SEQUENCE | decimal(38,0) |  |
| ROUTER_BO | varchar(412) |  |
| ROUTER_STEP_BO | varchar(412) |  |
| REF_TYPE | varchar(20) |  |
| REF_GBO | varchar(412) |  |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_router_step_prop
> 工艺路线步骤属性

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| ROUTER_BO | varchar(412) | 工艺路线 |
| ROUTER_STEP_BO | varchar(412) | 步骤 |
| ATTRIBUTE | varchar(50) | 属性 |
| VALUE | text | 值 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |


## md_storage_location_member
> 存储地点成员

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| STORAGE_LOCATION_BO | varchar(412) | 存储地点BO |
| SITE | varchar(32) | 站点 |
| SEQUENCE | decimal(18,0) | 序号 |
| ENABLE | varchar(1) | 是否启用 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联BO |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |


## md_task_event
> 任务事件

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点/工厂 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联BO |
| EVENT_NO | varchar(120) | 事件 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |

## md_task_item
> 任务项

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点/工厂 |
| TASK_ITEM | varchar(50) | 任务项 |
| TASK_ITEM_DESC | varchar(10) | 任务项描述 |
| REMARK | varchar(100) | 备注 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |
| DC_PLUGIN | varchar(100) | 数据收集插件 |
| RECORD_TYPE | varchar(10) | 记录方式 |
| DATA_TYPE | varchar(50) | 数据类型 |
| DC_TYPE | varchar(50) | 收集类型 |
| INSPECT_STANDARD | varchar(128) | 检验标准 |
| STANDARD_DESC | varchar(200) | 检验标准描述 |
| TEST_METHOD_DESC | varchar(50) | 检测方法 |
| FN | varchar(200) | 公式 |
| INSPECT_FEATURE | varchar(128) | 检验特性 |
| INSPECT_FEATURE_DESC | varchar(128) | 检验特性描述 |
| JIG_GROUP_NO | varchar(128) | 检具组编号 |
| JIG_GROUP_DESC | varchar(128) | 检具组描述 |
| WIDTH | varchar(100) | 宽度 |
| PARAM_GROUP | varchar(100) | 参数组 |

## md_task_obj
> 任务对象

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| TASK_TYPE | varchar(30) | 任务类型 |
| SEQUENCE | decimal(18,0) | 序号 |
| MD_TASK_OPERATION_BO | varchar(412) | 主表bo |
| SYS_FILE_BO | varchar(100) | 文件bo |
| QTY_SAMPLING | decimal(18,0) | 取样量 |
| SAMPLING_UNIT | varchar(20) | 取样单位 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
| SAMPLING_DESC | varchar(200) | 取样描述 |
| LEVEL | decimal(18,0) | 级别 |
| REMARK | varchar(255) | 备注 |
| NC_GROUP | varchar(100) | 代码组 |
| NC_GROUP_CATEGORY | varchar(100) | 代码组类型 |

## md_task_obj_member
> 任务对象成员

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点/工厂 |
| MD_TASK_OBJ_BO | varchar(412) | 关联bo |
| SEQUENCE | decimal(18,0) | 序号 |
| REF_TYPE | varchar(30) | 关联类型；物料/物料组/合作伙伴/BOM |
| REF_OBJ | varchar(412) | 关联对象 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |

## md_task_operation
> 任务操作

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(10) | 站点 |
| OPERATION | varchar(100) | 工序 |
| SYS_FILE_BO | varchar(100) | 文件bo |
| SEQUENCE | decimal(18,0) | 序号 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_task_plan
> 任务计划

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 唯一标识 |
| SITE | varchar(10) | 站点/工厂 |
| MD_TASK_OBJ_BO | varchar(412) | 关联bo |
| SEQUENCE | decimal(18,0) | 序号 |
| OPERATION | varchar(128) | 工序 |
| ITEM_GROUP | varchar(128) | 特新 |
| TASK_ITEM_BO | varchar(412) | 检验项BO |
| SYS_FILE_BO | varchar(412) | 文件BO |
| SAMPLING_SCHEME | varchar(30) | 采样方案组 |
| QTY_SAMPLING | varchar(50) | 取样数量 |
| SAMPLING_UNIT | varchar(30) | 取样单位 |
| TEST_COUNT | int | 测试次数 |
| SINLE_SAMPLING | varchar(128) | 单次采样 |
| RECEIVE_STANDARD | varchar(128) | 接受标准 |
| RECORD_TYPE | varchar(10) | 记录方式 |
| DATA_TYPE | varchar(50) | 数据类型 |
| INSPECT_STANDARD | varchar(128) | 检验标准 |
| FN | varchar(200) | 公式 |
| CREATE_BY | varchar(64) | 创建人 |
| CREATE_TIME | datetime(3) | 创建时间 |
| UPDATE_BY | varchar(64) | 修改人 |
| UPDATE_TIME | datetime(3) | 修改时间 |
| TOOL_GROUP | varchar(50) | 工具组 |
| NC_GROUP | varchar(255) | 不合格代码组 |
| DC_TYPE | varchar(50) | 收集类型 |
| STANDARD_DESC | varchar(200) | 检验标准描述 |
| TEST_METHOD_DESC | varchar(50) | 检测方法简称 |
| RECORD_GROUP | varchar(20) | 记录组 |
| NC_GROUP_CATEGORY | varchar(100) | 代码组类型 |
| STA_DESC | varchar(10) | 标准单位 |
| RECORD_COUNT | int | 记录次数 |

## md_user_quick_access
> 用户快捷访问配置

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| FILE_BO | varchar(412) | 文件配置BO |
| SEQUENCE | decimal(18,0) | 序号 |
| USER_NO | varchar(500) | 用户编号 |
| ACTIVITY_NO | varchar(500) | 作业 |
| CERT_NO | varchar(500) | 资质 |
| I_SITE | varchar(500) | 工厂 |
| PARENT_BO | varchar(412) | 父Bo |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_wip_monitor
> WIP 监控配置

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| FILE_BO | varchar(412) | 文件配置BO |
| SEQUENCE | decimal(18,0) | 序号 |
| PARAM_CATEGORY | varchar(500) | 参数类型分类 |
| BIND_CODE_DESC | varchar(500) | 绑定编码描述 |
| BIND_DATA_TYPE | varchar(500) | 绑定数据类型 |
| PTYPE | varchar(500) | 参数类型 |
| DURATION_DESC | varchar(500) | 时长描述 |
| BIND_DATA_CATEGORY | varchar(500) | 绑定数据类型分类 |
| BIND_CODE | varchar(500) | 绑定编码 |
| TYPE | varchar(500) | 设置类型 |
| DURATION | varchar(500) | 设置时长 |
| PARENT_BO | varchar(412) | 父Bo |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |

## md_work_center
> 工作中心

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| WORK_CENTER | varchar(50) | 工作中心 |
| WORK_CENTER_DESC | varchar(100) | 描述 |
| WORK_CENTER_CATEGORY | varchar(30) | 类别 |
| WORK_CENTER_STATUS | varchar(30) | 状态 |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
| MODEL | varchar(50) |  |
| IS_SCHEDUL | varchar(10) | 是否排产(Y/N) |

## md_work_center_member
> 工作中心成员

| 列名 | 类型 | 注释 |
|------|------|------|
| HANDLE | varchar(412) | 主键 |
| SITE | varchar(32) | 站点 |
| WORK_CENTER_BO | varchar(412) | 工作中心BO |
| SEQUENCE | decimal(18,0) | 序号 |
| ENABLE | varchar(1) | 是否启用 |
| REF_TYPE | varchar(30) | 关联类型 |
| REF_GBO | varchar(412) | 关联BO |
| CREATE_BY | varchar(32) |  |
| CREATE_TIME | datetime(3) |  |
| UPDATE_BY | varchar(32) |  |
| UPDATE_TIME | datetime(3) |  |
