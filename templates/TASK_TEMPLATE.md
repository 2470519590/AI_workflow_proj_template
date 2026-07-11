# TASK_TEMPLATE.md

本文件用于描述一个 AI 实现任务。

它控制 AI 的输入。让 AI 修改代码前，优先填写本模板。

不要把本文件写成流水账。任务文件描述“要做什么”，不是记录“做过哪些尝试”。

## 1. 任务

标题：

一句话目标：

任务类型：

- [ ] 功能实现
- [ ] Bug 修复
- [ ] Debug 定位
- [ ] 已批准的重构
- [ ] 文档
- [ ] 只做 Review

任务粒度：

- [ ] 主任务
- [ ] 子任务，属于：
- [ ] 仅 debug 短记录

如果只是一个小 debug 观察，不要创建长任务记录。放入本文件的 `Debug Short Log`，或在根因明确后写入 `docs/ERROR_CATALOG.md`。

## 2. 目标区域

项目/领域：

目标板卡或平台：

子系统：

软件层：

归属模块：

## 3. AI 必须读取的上下文

必读文档：

- `AGENTS.md`
- `AI_README.md`
- `docs/INDEX.md`
- `docs/CODING_RULES.md`
- `docs/REVIEW_CHECKLIST.md`
- `docs/DECISIONS.md`
- `docs/ERROR_CATALOG.md`

任务相关文档：

- 

编辑前必须检查的源码：

- 

## 4. 严格范围

允许修改的文件或目录：

- 

禁止修改的文件、目录、接口或行为：

- 

非目标：

- 

## 5. 功能需求

实现必须做到：

- 

实现不得：

- 

本节保持简短，只列必要行为。不要写 debug 尝试、命令历史、长日志或重复观察。

## 6. 接口与契约

受影响公共 API：

- none

受影响消息、CAN 帧、IOCTL、sysfs 节点、设备树节点、文件或外部契约：

- none

受影响生成文件：

- none

兼容性要求：

- 未明确批准时保持不变

## 7. 工程决策

AI 是否可以做架构、接口或模块边界决策？

- 不可以。AI 必须停止，说明选项和取舍，并请求确认。

本任务已批准的决策：

- none

## 8. 嵌入式风险区域

勾选所有相关项：

- [ ] ISR 或中断行为
- [ ] RTOS 任务、优先级、队列、定时器、互斥锁或阻塞行为
- [ ] DMA、cache、内存生命周期或 buffer 归属
- [ ] startup、bootloader、linker、memory map 或初始化顺序
- [ ] 硬件寄存器、引脚、时钟或电源行为
- [ ] CAN、UART、SPI、I2C、Ethernet、USB 或其他协议行为
- [ ] Linux kernel、BSP、device tree、sysfs、ioctl 或 userspace ABI
- [ ] 持久化存储、标定、诊断或兼容数据
- [ ] 安全、失效保护、watchdog、故障处理或降级模式
- [ ] 时序、控制环、执行器命令或机器人模式切换
- [ ] 暂无已知风险

风险说明：

- 

## 9. 约束

实现约束：

- 遵守 `docs/CODING_RULES.md`
- 不做无关重构
- 不修改严格范围外的文件
- 最终 diff 不得包含临时 debug 代码
- 未在本任务列出的公共接口不得修改

任务特定约束：

- 

## 10. 验证

必需验证：

- build：
- test：
- static analysis：
- manual inspection：
- hardware / bench / SIL / HIL / smoke test：

如果某项检查无法运行，AI 必须说明原因。

## 11. Debug Short Log

仅用于记录属于大任务内部的小 debug 发现。

限制：最多 5 条。

- 现象：
- 关键观察：
- 疑似归属：
- 下一步检查：
- 状态：open / fixed / moved to `docs/ERROR_CATALOG.md`

不要粘贴完整日志。只保留最小有用片段，或链接到外部日志位置。

## 12. 验收标准

任务完成条件：

- 

## 13. 文档预算

预计文档更新：

- [ ] 无
- [ ] 仅本任务短记录
- [ ] `docs/ERROR_CATALOG.md`
- [ ] `docs/DECISIONS.md`
- [ ] `docs/CONTROL_THEORY.md`
- [ ] 接口 / RTOS / 硬件 / 架构文档

文档保持简洁：

- 任务总结最多 5 条
- debug 记录最多 5 条
- 决策记录最多 6 条
- 控制算法记录只写必要公式、变量、假设和限制

不要写叙事型进度日志。

## 14. AI 最终输出

AI 最终回复必须包含：

- `Summary`
- `Files changed`
- `Context used`
- `Verification`
- `Assumptions`
- `Risks`
- `Next`

最终回复前必须完成 `docs/REVIEW_CHECKLIST.md`。

## 15. 长期记录

如果任务修复了具体失败、bug、回归、通信问题、硬件 bring-up 问题或调试问题，更新 `docs/ERROR_CATALOG.md`。

如果任务确认或改变了工程决策，更新 `docs/DECISIONS.md`。

如果任务影响观测器、估计器、控制器、状态量、调参、饱和、模式切换或执行器命令行为，更新 `docs/CONTROL_THEORY.md`。
