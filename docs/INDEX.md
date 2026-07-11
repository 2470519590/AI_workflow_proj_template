# INDEX.md

本文件是项目的持久上下文索引。

真实项目应持续更新本文件，让 AI 不依赖聊天历史也能快速找到文档和代码目录。

## 1. 项目目录

适配真实项目后填写：

- 固件源码根目录：
- 公共头文件：
- 驱动 / BSP / HAL：
- 中间件 / RTOS：
- 工具或脚本：
- 文档目录：
- 任务记录：
- 模板目录：
- 提示词目录：

## 2. 默认不读或不改的目录

列出 AI 默认不应读取或修改的目录：

- 生成的构建输出：
- 复制来的参考工程：
- IDE 元数据：
- 外部模板：

## 3. 必读文档

- `AGENTS.md`：AI 工作流程总规则
- `AI_README.md`：模板使用说明
- `docs/AGENT_MODEL_ROLES.md`：SOL / TERRA / LUNA 职责和模型映射
- `docs/CODING_RULES.md`：实现行为规则
- `docs/REVIEW_CHECKLIST.md`：最终自检清单
- `docs/DECISIONS.md`：长期工程决策记录
- `docs/ERROR_CATALOG.md`：已解决问题和工程经验

## 4. 任务相关文档

真实项目创建后在这里补充：

- 架构：
- 接口或协议：
- 硬件：
- RTOS 或调度：
- 调试指南：
- Git 工作流：
- 控制理论或算法设计：

## 5. 任务记录

- `templates/TASK_TEMPLATE.md`：新建 AI 实现任务的模板
- `tasks/YYYY-MM-DD-topic.md`：已完成任务记录，真实项目可按需创建

不要把本文件写成目录树全集。只记录 AI 恢复上下文时真正需要的入口。
