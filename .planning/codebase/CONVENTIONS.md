# Coding Conventions

本项目的编码规范主要遵循 Python 社区的 PEP 8 标准，并针对交通流量仿真和 LLM 集成建立了一些特定的模式。

## 1. 命名规范 (Naming)

- **类名**: 使用 `CamelCase` (如 `SUMOSimulator`, `LLMController`, `LLMClient`)。
- **函数和变量**: 使用 `snake_case` (如 `start_simulation`, `phase_queues`, `current_duration`)。
- **私有方法和变量**: 以单下划线开头 (如 `_generate_junction_description`, `_parse_llm_response`)。
- **单例/常量占位符**: 使用下划线开头的全大写 (如 `_UNSET`)。

## 2. 异步编程 (Asynchronous Programming)

- 应用核心（FastAPI 及其客户端）广泛使用 `async/await`。
- **SSE (Server-Sent Events)**: `call_with_messages` 函数通过异步生成器返回 LLM 的响应。
- **并发任务**: 使用 `asyncio.create_task` 处理后台任务，如 `periodic_chat_task`。

## 3. 错误处理 (Error Handling)

- **Catch-all 模式**: 广泛使用 `try...except...` 捕获异常，通常配合 `loguru` 进行日志记录。
- **路径检查**: 在类初始化时通常会检查配置文件路径是否存在 (如 `SUMOSimulator.__init__`)。
- **TraCI 异常**: 专门处理 `traci.exceptions.TraCIException` 以防仿真过程中的连接意外断开。

## 4. LLM 提示词规范 (LLM Prompting)

- **结构化 Prompt**: 提示词通常定义在代码中，分 `instruction` 和 `input` 两大部分。
- **角色设定**: 一致的角色模型："你是一位交通管理专家"。
- **输出约束**: 明确要求 LLM 直接返回特定格式的消息，如 `下一个信号相位是={相位编号}`。
- **正则解析**: 使用正则表达式从 LLM 生成的文本中提取关键信号相位 ID。

## 5. 配置与数据持久化

- **JSON 配置**: 路口信息 (如 `J54_data.json`) 统一采用 JSON 结构。
- **环境变量**: 依赖 `dotenv` 加载本地配置，特别是 `SUMO_HOME` 变量。
- **导入约定**: 对于 SUMO 的 `tools` 目录采用动态修改 `sys.path` 的方式导入 `traci`。
