# Codebase Concerns & Technical Debt

本文档总结了 **DeepSignal / TSC-CYCLE** 代码库中的技术债务、已知问题、安全风险、性能瓶颈及脆弱环节。

---

## 1. 技术债务 (Technical Debt)

### 1.1 硬编码配置 (Hardcoded Configurations)
- **路口硬编码**: `api_server/mcp_server/llm_controller.py` 和 `api_server/mcp_server/mcp_server.py` 中大量硬编码了 'J54' 路口的相位定义、车道 ID 和方向映射。这种做法导致系统难以扩展到其他路口。
- **相位映射**: `get_phase_queues_from_sumo` 函数中手动将相位 ID 映射到 `N_STRAIGHT` 等名称，缺乏通用的配置解耦。

### 1.2 初始化逻辑碎片化 (Fragmented Initialization)
- SUMO 模拟器的启动和 MCP 服务器的初始化逻辑散落在 `sumo_llm/app.py`、`api_server/mcp_server/mcp_server.py` 和 `sumo_llm/sumo_simulator.py` 中，缺乏统一的生命周期管理。

### 1.3 职责划分不清晰 (Mixed Responsibilities)
- `mcp_server.py` 同时负责服务器运行、后台数据采集、算法实例化和工具定义。建议将后台任务和核心工具逻辑进一步模块化。

---

## 2. 潜在 Bug 与可靠性问题 (Known Issues & Reliability)

### 2.1 异常处理机制 (Error Handling)
- 许多 `try-except` 块仅打印错误堆栈并返回默认值或当前相位。在关键的信号控制回路中，这种处理可能导致仿真行为异常。
- `llm_controller.py` 中的 `_parse_llm_response` 严重依赖正则表达式。如果 LLM 输出格式稍有偏离，解析将失败并回退到当前相位，可能导致控制僵死。

### 2.2 ��程安全 (Thread Safety)
- `mcp_server.py` 中的 `historical_data` 字典在后台异步循环和 MCP 工具调用中被共享访问，但没有明显的加锁机制，存在竞态风险。

### 2.3 状态同步 (State Synchronization)
- 后台自动优化线程与 SUMO 主仿真步长之间的同步完全基于 `time.sleep(1)` 和 `asyncio.sleep(10)`，这在负载较高时可能导致数据采集与实际仿真时钟不同步。

---

## 3. 安全风险 (Security Concerns)

### 3.1 凭证泄露 (Credential Exposure)
- **CRITICAL**: `sumo_llm/openai_client.py` 中直接硬编码了 DeepSeek 和阿里云的 API Key。
- `api_server/client/llm_client.py` 虽然使用了 `.env`，但代码库中仍存在硬编码默认值的倾向。

### 3.2 权限与访问控制 (Access Control)
- MCP 服务器、Streamlit 应用和相关端口均在本地运行，没有任何身份验证或访问限制。在开放的网络环境中存在被非法调用的风险。

### 3.3 远程代码执行风险 (Remote Code Execution)
- `llm_client.py` 在加载 Transformers 模型时使用了 `trust_remote_code=True`。如果模型来源被篡改，可能导致远程代码执行。

---

## 4. 性能瓶颈 (Performance Bottlenecks)

### 4.1 同步阻塞调用 (Synchronous Blocking Calls)
- `LLMController.update` 调用 LLM 客户端时是同步的。如果���络延迟高或模型推理慢，会阻塞整个控制循环。虽然 `auto_optimize_in_thread` 将其放在了线程中，但仍然会影响控制的时效性。

### 4.2 频繁的磁盘 I/O (Frequent Disk I/O)
- `save_historical_data` 每 10 步就会进行一次 JSON 文件的全量写入，随着历史数据增加，可能会产生明显的 I/O 压力。

### 4.3 资源占用 (Resource Usage)
- 加载 Traffic-R1 或 Qwen 等大模型对内存和 GPU 显存要求极高，系统缺乏显存回收或精简加载的策略。

---

## 5. 脆弱环节 (Fragile Areas)

### 5.1 SUMO 版本与配置耦合 (SUMO Coupling)
- 系统高度依赖特定的 `.sumocfg` 文件结构（如 `<net-file>` 标签的解析）。SUMO 配置文件的微小变动或版本不兼容可能导致系统崩溃。

### 5.2 环境变量依赖 (Environment Dependencies)
- 系统运行需要配置 `SUMO_HOME`、API Key、模型路径等多个环境变量。由于缺乏健全的检查机制，环境配置错误通常只会在运行时崩溃。

### 5.3 数据格式脆弱性 (Data Schema Fragility)
- `J54_data.json` 等配置文件与 Python 逻辑（如索引、ID 匹配）高度耦合。手动编辑这些文件极易引入导致程序崩溃的逻辑错误。
