# 目录结构 (STRUCTURE.md)

## 目录布局
```text
DeepSignal/
├── api_server/             # API 与 MCP 服务核心
│   ├── client/             # 不同模型商的 Client 实现
│   ├── mcp_server/         # MCP 协议服务端与算法实现
│   └── utils/              # 通用工具类
├── sumo_llm/               # SUMO 仿真封装与演示
│   ├── J54_data.json       # 默认路口元数据
│   ├── osm.sumocfg         # 默认仿真配置
│   └── sumo_simulator.py   # 仿真器核心类
├── scenarios/              # SUMO 场景数据集 (各城市/路网)
├── tests/                  # 测试用例
├── images/                 # 项目可视化与文档图片
├── main.py                 # FastAPI 主入口
├── requirements.txt        # 依赖清单
└── pyproject.toml          # 项目配置
```

## 关键位置 (Key Locations)
- **仿真核心**: `sumo_llm/sumo_simulator.py`
- **MCP 工具集**: `api_server/mcp_server/mcp_server.py`
- **LLM 控制逻辑**: `api_server/mcp_server/llm_controller.py`
- **数据场景**: `scenarios/`

## 命名约定 (Naming Conventions)
- **文件与目录**: 蛇形命名法 (`snake_case`)。
- **类名**: 大驼峰命名法 (`PascalCase`)。
- **常量**: 全大写蛇形命名法 (`UPPER_SNAKE_CASE`)。
- **私有方法**: 单下划线开头 (`_private_method`)。

## 文档规范
- `README.md` & `README_zh.md`: 提供多语言项目概览。
- `LICENSE`: 明确开源许可。
