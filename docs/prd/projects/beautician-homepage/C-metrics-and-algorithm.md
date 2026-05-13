# 子文档 C：数据口径与算法规则（草图最小集）

## 1. 指标口径总表
| 指标 | 公式 | 分子定义 | 分母定义 | 时间窗口 | 统计粒度 |
|---|---|---|---|---|---|
| 业绩值 | 来自店务统计口径 | 当日业绩金额 | 不适用 | 当日 | 技师 |
| 到店人数 | 来自预约核销口径 | 当日到店顾客数 | 不适用 | 当日 | 技师 |
| 消费人数 | 来自订单支付口径 | 当日消费顾客数 | 不适用 | 当日 | 技师 |
| 销售人数 | 来自销售订单口径 | 当日产生销售订单顾客数 | 不适用 | 当日 | 技师 |
| 服务人数 | 来自服务单口径 | 当日完成服务顾客数 | 不适用 | 当日 | 技师 |
| 保有量 | 来自顾客资产口径 | 当前有效管理顾客数 | 不适用 | 当日快照 | 技师 |
| 新客人数 | 来自新增建档口径 | 统计窗口内新增顾客数 | 不适用 | 当日快照 | 技师 |
| 流失人数 | 来自流失规则口径 | 超过约定窗口未复购顾客数 | 不适用 | 当日快照 | 技师 |
| 休眠人数 | 来自休眠规则口径 | 超过休眠窗口未到店顾客数 | 不适用 | 当日快照 | 技师 |

## 2. 模块展示分层（草图）
| 分层 | 判定条件 | 页面标签 | 动作优先级 |
|---|---|---|---|
| 首页主焦点层 | 首页首屏默认展示 | 店务 | 高 |
| 底部栏入口层 | 通过tab点击进入 | 顾客/应用/数据 | 中 |
| 数据占位层 | 数据模块未展开 | 建设中 | 低 |

## 3. 阈值与窗口（草图版约束）
- 业绩/到店人数/消费人数/销售人数/服务人数默认窗口：当日
- 首屏加载容忍阈值：2秒内显示主数据，超时显示骨架
- 数据占位模块不定义阈值，不参与指标比较

## 4. 优先级与归因规则（最小）
- 首页信息优先级：业绩 > 到店人数 > 消费人数 > 销售人数 > 服务人数
- 顾客运营页优先级：风险顾客基本盘 > 产值规划 > 处方定制 > 预约到店 > 客情跟进
- 今日待到店列表排序规则：按预约时间升序（最早到店在前）
- 底部栏优先级：店务固定首位，其余按顾客/应用/私域/数据顺序
- 本轮不定义深归因规则，避免超出草图范围

## 5. 字段字典（最小集）
| 字段名 | 类型 | 示例 | 来源 | 用途 |
|---|---|---|---|---|
| performanceValue | number |  | 店务统计接口 | 首页指标展示 |
| arrivalCount | number |  | 预约/核销接口 | 首页指标展示 |
| consumeCount | number |  | 订单接口 | 首页指标展示 |
| salesCount | number |  | 销售订单接口 | 首页指标展示 |
| serviceCount | number |  | 服务单接口 | 首页指标展示 |
| todayArrivalList | array |  | 预约接口 | 今日待到店列表渲染 |
| customerHoldCount | number | 28 | 顾客资产接口 | 顾客运营-保有量展示 |
| customerNewCount | number | 24 | 顾客资产接口 | 顾客运营-新客展示 |
| customerLostCount | number | 36 | 顾客资产接口 | 顾客运营-流失展示 |
| customerDormantCount | number | 18 | 顾客资产接口 | 顾客运营-休眠展示 |
| valueTarget | number | 300000 | 目标配置 | 产值规划-目标展示 |
| valueCompletionRate | number | 0.68 | 统计计算 | 产值规划-完成率展示 |
| valueRank | number | 12 | 排名服务 | 产值规划-排名展示 |
| valueUnplannedCount | number | 42 | 处方规划接口 | 产值规划-未规划人数 |
| valueUndoneCount | number | 19 | 处方规划接口 | 产值规划-有目标未达成 |
| prescriptionNoConsume60dCount | number | 28 | 处方服务 | 处方定制-60天预警 |
| prescriptionPlannedNotArrivedCount | number | 13 | 预约服务 | 处方定制-计划未到店 |
| appointTarget | number | 30 | 目标配置 | 预约到店-目标展示 |
| appointCompletionRate | number | 0.5 | 统计计算 | 预约到店-完成率展示 |
| appointRank | number | 7 | 排名服务 | 预约到店-排名展示 |
| appointTodayInviteCount | number | 4 | 邀约服务 | 预约到店-今日邀约 |
| appointInvitedCount | number | 15 | 邀约服务 | 预约到店-已邀约 |
| followupRiskSoonLostCount | number | 12 | 跟进服务 | 客情跟进-即将流失标签 |
| followupKeyRecallCount | number | 23 | 跟进服务 | 客情跟进-重点回访标签 |
| followupBirthdayCount | number | 17 | 跟进服务 | 客情跟进-生日标签 |
| customerOpsEntryList | array |  | 顾客运营配置 | 顾客页入口渲染 |
| privateOpsShareEnabled | boolean |  | 私域配置 | 应用页分享按钮显示 |
| dataModuleStatus | string | building | 配置中心 | 数据页占位文案 |

## 6. 算法验收样例
| 样例ID | 输入 | 期望输出 | 判定说明 |
|---|---|---|---|
| ALG-01 | performanceValue=100000,arrivalCount=35,consumeCount=22,salesCount=18,serviceCount=26 | 首页五项指标按固定顺序展示 | 草图层仅校验字段映射与排序 |
| ALG-02 | dataModuleStatus=building | 数据tab进入占位页 | 草图层不要求业务计算 |
| ALG-03 | todayArrivalList=[09:30,10:00,09:00] | 列表展示顺序为09:00,09:30,10:00 | 草图层校验排序规则 |
| ALG-04 | customerHoldCount=28,customerNewCount=24,customerLostCount=36,customerDormantCount=18 | 顾客运营基本盘按固定四项展示 | 草图层仅校验字段映射与顺序 |
| ALG-05 | followupRiskSoonLostCount=12,followupKeyRecallCount=23,followupBirthdayCount=17 | 标签展示“即将流失/重点回访/本月过生日”及对应人数 | 草图层仅校验展示完整性 |
