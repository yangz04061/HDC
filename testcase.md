# HDC 功能测试用例集
# Hill Descent Control DV Test Case Suite

## 1. 文档信息

| 项目 | 内容 |
|---|---|
| 文档名称 | HDC 功能整车 DV 测试用例集 |
| 功能名称 | HDC / Hill Descent Control / 陡坡缓降控制 |
| 测试阶段 | 整车 DV |
| 测试对象 | 整车 |
| 适用车型 | XXX |
| 软件版本 | XXX |
| 硬件版本 | XXX |
| 编制人 | XXX |
| 日期 | YYYY-MM-DD |

---

## 2. 测试目的

本测试用例集用于验证 HDC 功能在整车状态下是否满足设计要求，包括：

1. HDC 激活条件判断是否正确；
2. HDC 下坡控速能力是否满足目标要求；
3. HDC 退出逻辑是否正确；
4. 驾驶员油门、制动、开关等干预是否响应正确；
5. 故障状态下系统是否安全降级或禁止工作；
6. 边界工况下系统是否无误触发、无异常退出、无车辆失稳；
7. 仪表提示、状态显示、故障报警是否与实际功能状态一致。

---

## 3. 参考输入

| 类型 | 内容 |
|---|---|
| 功能规范 | HDC System Requirement / SDS |
| 整车需求 | Vehicle Requirement Specification |
| 制动系统规范 | ESC / ABS / Brake Control Specification |
| 网络信号矩阵 | CAN / LIN / Ethernet Signal Matrix |
| 诊断规范 | DTC Specification / Diagnostic Requirement |
| 仪表规范 | Cluster HMI Specification |
| 测试规范 | Vehicle DV Test Plan |

---

## 4. 术语与缩写

| 缩写 | 含义 |
|---|---|
| HDC | Hill Descent Control，陡坡缓降控制 |
| ESC | Electronic Stability Control，车身电子稳定控制 |
| ABS | Anti-lock Braking System，防抱死制动系统 |
| TCS | Traction Control System，牵引力控制 |
| DTC | Diagnostic Trouble Code，诊断故障码 |
| HMI | Human Machine Interface，人机交互 |
| DV | Design Verification，设计验证 |
| EOL | End of Line，下线配置 |
| CAN | Controller Area Network，控制器局域网 |

---

## 5. 测试环境与设备

### 5.1 测试场地

| 项目 | 要求 |
|---|---|
| 测试地点 | 封闭试验场、专用坡道或安全可控测试道路 |
| 坡度 | 5%、10%、15%、20%、25% 或按项目要求 |
| 路面 | 干燥沥青、湿滑路面、低附着路面、碎石路面等 |
| 坡长 | 应满足 HDC 稳态控制时间要求，建议不少于 50 m |
| 安全区域 | 坡底应具备足够缓冲距离 |
| 环境温度 | 常温、低温、高温，按 DV 计划定义 |

### 5.2 测试设备

| 设备 | 用途 |
|---|---|
| 数据采集仪 | 采集 CAN、轮速、车速、制动压力等信号 |
| GPS/惯导设备 | 测量车辆速度、加速度、坡度、姿态 |
| 诊断仪 | 读取 DTC、清除故障码、监控诊断状态 |
| 坡度测量设备 | 确认实际坡度 |
| 视频记录设备 | 记录仪表、驾驶员操作、车辆姿态 |
| 制动温度测量设备 | 监控制动热衰退风险 |
| 安全保障车辆/人员 | 测试安全保障 |

---

## 6. 测试信号记录要求

建议记录以下信号，采样频率不低于 50 Hz；关键动态信号建议不低于 100 Hz。

| 信号类别 | 信号名称 |
|---|---|
| 车辆状态 | Vehicle Speed、Wheel Speed_FL/FR/RL/RR |
| 坡道信息 | Longitudinal Acceleration、Pitch Angle、Road Grade |
| HDC 状态 | HDC Switch Status、HDC Standby Status、HDC Active Status、HDC Fault Status |
| 驾驶员输入 | Accelerator Pedal Position、Brake Pedal Status、Brake Pressure、Gear Position |
| 制动控制 | Master Cylinder Pressure、ESC Brake Pressure、Wheel Brake Pressure |
| 稳定性 | Yaw Rate、Lateral Acceleration、Steering Wheel Angle |
| 动力系统 | Engine/Motor Torque、Drive Torque Request |
| HMI | Cluster Indicator、Warning Message、Buzzer Status |
| 诊断 | DTC Status、Fault Debounce Status、ESC/ABS Fault Status |

---

## 7. 通用测试前提

| 项目 | 前提条件 |
|---|---|
| 车辆状态 | 车辆无影响 HDC 的现存故障 |
| 制动系统 | ABS、ESC、制动助力系统功能正常 |
| 轮胎状态 | 胎压、轮胎规格、磨损状态符合要求 |
| 车辆载荷 | 按 DV 计划定义，建议覆盖整备质量和满载 |
| HDC 配置 | 车辆配置支持 HDC，EOL 配置正确 |
| 驾驶模式 | 按功能规范要求设置，例如 Normal、Off-road、Snow 等 |
| 电源状态 | 高压/低压系统电压正常 |
| 数据采集 | 所有关键 CAN 信号和视频记录正常 |
| 安全措施 | 测试区域封闭，坡底安全距离充足 |

---

## 8. 客观评价指标

以下阈值为示例，应根据项目规范进行修订。

### 8.1 HDC 状态响应

| 评价项 | 推荐通过标准 |
|---|---|
| HDC 开关响应时间 | ≤ 1.0 s |
| HDC 状态反馈一致性 | CAN 状态、仪表显示、实际控制状态一致 |
| HDC 激活延迟 | 满足激活条件后 ≤ 1.0 s 进入 Active |
| HDC 退出延迟 | 满足退出条件后 ≤ 1.0 s 退出 Active |
| HMI 提示 | 指示灯、文字、声音提示符合 HMI 规范 |

### 8.2 车速控制性能

| 评价项 | 推荐通过标准 |
|---|---|
| 稳态车速偏差 | 目标车速 ±2 km/h |
| 最大瞬态超调 | ≤ 3 km/h |
| 稳态速度波动 | 峰峰值 ≤ 2 km/h |
| 控制建立时间 | ≤ 3.0 s |
| 控制连续性 | 无非预期退出、无频繁状态跳变 |
| 驾驶员可控性 | 驾驶员制动和油门输入优先级符合策略 |

### 8.3 制动控制性能

| 评价项 | 推荐通过标准 |
|---|---|
| 制动压力建立 | 平顺、无异常突变 |
| 制动压力释放 | HDC 退出后平顺释放 |
| 制动冲击 | 无明显点头、异响或冲击 |
| 轮胎抱死 | 无非预期持续抱死 |
| ABS 协同 | ABS 介入合理，无控制冲突 |

### 8.4 车辆稳定性

| 评价项 | 推荐通过标准 |
|---|---|
| 横摆稳定性 | 无明显甩尾、侧滑、失稳 |
| 方向稳定性 | 无明显跑偏 |
| 横向加速度 | 无异常突变 |
| 横摆角速度 | 无异常振荡 |
| 驾驶员修正 | 不需要大幅方向修正即可保持轨迹 |

### 8.5 故障处理

| 评价项 | 推荐通过标准 |
|---|---|
| 故障检测 | 故障注入后系统能正确识别 |
| 功能降级 | HDC 禁止、退出或降级逻辑符合规范 |
| DTC 记录 | DTC 存储、状态位、恢复逻辑正确 |
| HMI 报警 | 故障提示及时、准确 |
| 安全性 | 故障过程中无非预期制动、无车辆失稳 |

---

# 9. 测试用例总览

| 用例编号 | 用例名称 | 分类 | 优先级 |
|---|---|---|---|
| HDC_DV_001 | HDC 开关开启进入待命状态 | 激活 | High |
| HDC_DV_002 | 满足坡度和车速条件后 HDC 自动激活 | 激活 | High |
| HDC_DV_003 | HDC 目标车速控制验证 | 控速 | High |
| HDC_DV_004 | 驾驶员制动干预验证 | 激活/干预 | High |
| HDC_DV_005 | 驾驶员油门干预验证 | 激活/干预 | High |
| HDC_DV_006 | HDC 手动关闭退出 | 退出 | High |
| HDC_DV_007 | 车速超限退出 | 退出 | High |
| HDC_DV_008 | 坡度不足退出或保持待命 | 退出 | Medium |
| HDC_DV_009 | 挡位不满足时禁止激活 | 边界 | High |
| HDC_DV_010 | HDC 低车速边界激活验证 | 边界 | Medium |
| HDC_DV_011 | HDC 高车速边界禁止激活验证 | 边界 | High |
| HDC_DV_012 | 湿滑路面 HDC 控制验证 | 边界 | High |
| HDC_DV_013 | 低附着路面 HDC 控制验证 | 边界 | High |
| HDC_DV_014 | 制动系统故障时 HDC 禁止工作 | 故障 | High |
| HDC_DV_015 | 轮速传感器故障时 HDC 退出 | 故障 | High |
| HDC_DV_016 | 横摆率传感器故障时 HDC 降级/退出 | 故障 | High |
| HDC_DV_017 | HDC 开关信号故障验证 | 故障 | Medium |
| HDC_DV_018 | CAN 通信故障验证 | 故障 | High |
| HDC_DV_019 | HDC 工作中 ABS 介入协调验证 | 边界/故障 | High |
| HDC_DV_020 | 制动过热保护验证 | 故障/边界 | Medium |
| HDC_DV_021 | 倒挡 HDC 功能验证 | 激活/边界 | Medium |
