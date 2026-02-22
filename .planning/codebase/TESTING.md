# Testing Patterns

目前的测试策略以集成测试、仿真验证和交互式可视化为主。项目中虽然存在空的 `tests/` 目录，但实际测试逻辑分散在各个核心组件中。

## 1. 测试结构 (Structure)

- **脚本内测试 (In-script Testing)**: 关键文件（如 `sumo_simulator.py`）包含 `if __name__ == "__main__":` 块，用于直接运行基础仿真逻辑的冒烟测试。
- **Streamlit 可视化测试**: 利用 `streamlit-demo.py` 和 `test-streamlit.py` 进行交互式功能验证，直观观察仿真状态和数据变化。

## 2. 模拟与 Mock (Mocking)

- **手动 Mock**: 在集成测试或定时任务（如 `main.py` ��的 `periodic_chat_task`）中，通过定义临时的 Mock 类（如 `MockRequest`）来代替真实的 FastAPI 请求，方便本地闭环测试任务逻辑。

## 3. 仿真实时验证 (Simulation Validation)

- **预热机制 (Warmup)**: `SUMOSimulator` 在正式开始收集数据前，会运行 `warmup_steps` (默认 300 步)，以确保交通流进入稳定状态，提高测试数据的有效性。
- **连通性检查**: 提供 `is_connected()` 方法，频繁检查 TraCI 与 SUMO 服务端的连接稳定性。

## 4. 数据回归与监控

- **历史记录存储**: 仿真器会将 `phase_queues` 和 `phases` 等关键指标实时保存到 `traffic_history.json` 中。
- **指标导出**: `save_metrics_to_csv` 方法将路口拥堵指数、饱和度等数据持久化，用于对比不同 LLM 策略或控制算法的优劣。

## 5. 建议的改进方向

- **单元测试框架**: 建议引入 `pytest` 对 `LLMController._parse_llm_response` 等纯逻辑函数进行自动化单测。
- **仿真回归测试**: 建立基于固定 XML 交通流场景的自动化断言脚本，验证不同相位策略下的总延误时间是否符合预期。
