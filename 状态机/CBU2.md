---
config:
  look: classic
  layout: elk
  theme: forest
---
stateDiagram
  direction TB
  OFF --> PASSIVE:条件0
  PASSIVE --> ACTIVE:条件2
  ACTIVE --> PASSIVE:条件3
  PASSIVE --> OFF:条件1
  ACTIVE --> OFF:条件1
  PASSIVE --> FAILURE:条件4
  ACTIVE --> FAILURE:条件4
  FAILURE --> OFF:条件1
  FAILURE --> PASSIVE:条件0
  OFF:HDC 关闭状态（HMI 功能灯关闭）
  PASSIVE:HDC 待命状态（HMI 功能灯常亮）
  ACTIVE:HDC 激活状态（HMI 功能灯闪烁）
  FAILURE:HDC 故障状态 （HMI 提示驾驶员故障）