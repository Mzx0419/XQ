# 子文档 E：埋点与验收（草图评审版）

## 1. 埋点事件清单
| 事件名 | 触发时机 | 功能模块 | 功能按钮 | 必传字段 |
|---|---|---|---|---|
| home_quick_action_click | 点击首页快捷操作按钮 | 店务 | 快捷操作项 | loginAccount, clickTime, functionButton, deviceType, appVersion |
| home_metric_card_click | 点击首页指标卡 | 店务 | 业绩/到店人数/消费人数/销售人数/服务人数卡 | loginAccount, clickTime, functionButton, deviceType, appVersion |
| today_arrival_action_click | 点击今日待到店操作 | 店务 | 确认到店/取消预约 | loginAccount, clickTime, functionButton, customerId, deviceType, appVersion |
| bottom_tab_click | 点击底部栏tab | 顾客/应用/私域/数据 | 顾客/应用/私域/数据 | loginAccount, clickTime, functionButton, deviceType, appVersion |
| private_share_click | 点击私域“直接分享” | 应用 | 直接分享 | loginAccount, clickTime, functionButton, deviceType, appVersion |
| customer_module_jump_click | 点击顾客运营模块标题跳转 | 顾客运营 | 产值/处方/预约/跟进模块标题跳转 | loginAccount, clickTime, functionButton, functionModule, deviceType, appVersion |
| customer_followup_tag_click | 点击客情跟进标签 | 顾客运营 | 即将流失/重点回访/本月过生日 | loginAccount, clickTime, functionButton, functionModule, deviceType, appVersion |

## 2. 属性字段定义
| 字段 | 类型 | 示例 | 说明 |
|---|---|---|---|
| loginAccount | string |  | 当前登录账号 |
| clickTime | string |  | 点击时间 |
| clickCount | number |  | 点击数量 |
| functionModule | string |  | 功能模块 |
| functionButton | string |  | 功能按钮 |
| deviceType | enum | ios/android | 设备类型 |
| appVersion | string |  | App 版本 |

## 3. 页面行为到埋点映射
| 页面区块 | 用户动作 | 事件名 | 校验点 |
|---|---|---|---|
| 首页快捷操作区 | 点击任一快捷入口 | home_quick_action_click | 是否记录按钮名称 |
| 首页三指标区 | 点击指标卡 | home_metric_card_click | 是否记录指标类型 |
| 今日待到店区 | 点击确认到店/取消预约 | today_arrival_action_click | 是否记录顾客ID和操作类型 |
| 底部栏导航区 | 点击顾客/应用/私域/数据tab | bottom_tab_click | 是否记录tab名称 |
| 私域入口页 | 点击直接分享 | private_share_click | 是否记录分享入口来源 |
| 顾客运营四模块标题 | 点击模块标题右侧跳转 | customer_module_jump_click | 是否记录模块名称 |
| 客情跟进标签区 | 点击任一场景标签 | customer_followup_tag_click | 是否记录场景名称 |

## 4. 验收清单（草图评审）
| 编号 | 验收项 | 验收方法 | 通过标准 |
|---|---|---|---|
| QA-01 | 首页主焦点正确 | 设计稿对照 | 店务快捷操作+三指标为首屏主视觉 |
| QA-02 | 四块并行入口完整 | 手工点检 | 底部栏可到达顾客/应用/数据 |
| QA-02A | 顶部数据概览新增项正确 | 设计稿对照 | 可见销售人数、服务人数 |
| QA-02B | 快捷功能区无改动 | 基线对照 | 与`店务首页-1比1复刻`一致 |
| QA-02C | 今日待到店可操作 | 手工点检 | 支持确认到店、取消预约且状态刷新 |
| QA-02D | 今日未传服务图无改动 | 基线对照 | 与`店务首页-1比1复刻`一致 |
| QA-03 | 数据模块占位合规 | 设计稿对照 | 数据页仅出现占位卡，不出现业务图表 |
| QA-04 | 私域分享入口可见 | 手工点检 | 应用页存在“直接分享”动作 |
| QA-05 | 草图可投喂AI | 结构检查 | 组件清单、区块顺序、文案约束齐全 |
| QA-06 | 顾客运营v1结构完整 | 设计稿对照 | 包含搜索、基本盘、产值、处方、预约、跟进、底部栏 |
| QA-07 | 顾客运营重点数据突出 | 设计稿对照 | 首屏先看到基本盘四指标，主指标视觉层级最高 |
| QA-08 | 跟进双跳转可识别 | 手工点检 | 模块整体跳转和标签独立跳转均可见且可点击 |

## 5. 回归路径（最小）
- 路径1：首页 -> 店务快捷操作 -> 目标页（占位可接受）
- 路径2：首页 -> 底部栏顾客 -> 顾客运营入口页
- 路径3：首页 -> 底部栏应用 -> 成长值入口 -> 直接分享
- 路径3A：首页 -> 底部栏私域 -> 成长值入口 -> 直接分享
- 路径4：首页 -> 底部栏数据 -> 建设中占位页
- 路径5：首页 -> 底部栏顾客 -> 顾客运营页 -> 点击四模块任一标题跳转
- 路径6：首页 -> 底部栏顾客 -> 顾客运营页 -> 点击跟进标签进入场景页

## 6. 数据模块占位专项验收
- 占位页文案必须包含“建设中/暂未开放”语义。
- 占位页不得包含真实经营数据字段。
- 占位页必须保留返回首页路径。
