# 项目架构 (ARCHITECTURE.md)

## 模式 (Pattern)
本项目采用 **MVP (Model-View-Presenter)** 的变体架构，结合了 **MCP (Model Context Protocol)** 协议以支持 LLM (大语言模型) 驱动的交通信号控制。
- **Model**: SUMO 仿真器 (`sumo_simulator.py`) 和交通控制算法 (`max_pressure.py`, `prediction_optimizer.py`)。
- **Presenter/Controller**: `mcp_server.py` 作为核心骨干，协调仿真状态与 LLM 决策。
- **Interface**: `api_server` 提供外部访问接口，通过 FastAPI 实现。

## 分层 (Layers)
1. **基础设施层 (Infrastructure Layer)**:
   - SUMO (Simulation of Urban MObility) 环境。
   - `traci` 接口，用于与仿真引擎通信。
2. **领域逻辑层 (Domain Logic Layer)**:
   - `sumo_llm`: 包含仿真封装器和基础算法实现。
   - `scenarios`: 存储不同城市的交通场景配置。
3. **协议与代理层 (Protocol & Agent Layer)**:
   - `mcp_server`: 实现 MCP 协议，暴露工具给 LLM。
   - `LLMController`: 封装 LLM 调用逻辑，执行优化决策。
4. **API 服务层 (API Service Layer)**:
   - `FastAPI`: 提供 RESTful 和 Streaming 接口。

## 数据流 (Data Flow)
1. **状态采集**: `SUMOSimulator` 定时通过 `traci` 获取路口流量、车辆速度和相位信息。
2. **上下文提供**: `mcp_server` 将交通状态封装为工具 (tools) 暴露给 LLM。
3. **分析决策**: LLM (如 lm-studio 或 OpenAI) 接收系统 Prompt 和实时交通数据，分析并输出相位优化建议。
4. **控制执行**: 决策指令通过 `mcp_server.set_phase_switch` 反馈给 `SUMOSimulator`，最终通过 `traci` 修改仿真中的信号灯状态。

## 抽象 (Abstractions)
- **SUMOSimulator**: 对底层仿真引擎的抽象，解耦仿真操作与业务逻辑。
- **MCP Tool**: 对交通管理操作的抽象，使其能被 LLM 理解和调用。
- **LLMClient**: 对不同模型服务商的抽象，支持 LM-Studio, OpenAI 等。

## 入口点 (Entry Points)
- `main.py`: 启动 FastAPI API 服务器。
- `api_server/mcp_server/mcp_server.py`: 启动交通控制 MCP 服务器及自动优化任务。
- `sumo_llm/sumo_simulator.py`: 仿真器核心。
