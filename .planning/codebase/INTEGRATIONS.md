# External Integrations

## External APIs (LLM Providers)
- **OpenAI**: Used for GPT-4 and compatible models.
- **Anthropic**: Used for Claude-3-5-sonnet.
- **DashScope (Alibaba Cloud)**: Primary integration for compatibility mode (used as the default `openai` client backend).
- **SiliconFlow**: Alternative LLM provider for various open-source models.
- **LM-Studio**: Local LLM integration via its OpenAI-compatible server endpoint.

## Simulation Engines
- **SUMO (Simulation of Urban MObility)**:
  - Integrated via `traci` (Transmission Control Protocol) for real-time interaction.
  - Controls traffic lights, retrieves lane queue lengths, and fetches vehicle data.
  - Supports GUI and non-GUI execution modes.

## Data Persistence & Storage
- **In-Memory**: `historical_data` dictionary in `mcp_server.py` for tracking phase queues and timestamps.
- **Filesystem**:
  - XML files for SUMO network (`.net.xml`), routes (`.rou.xml`), and configuration (`.sumocfg`).
  - JSON files for junction metadata and traffic history.
- **Database (Potential)**: `requirements.txt` includes `SQLAlchemy` and `PyMySQL`, suggesting potential or planned integration with relational databases, though not prominently used in the core logic.

## AI Models (Local)
- **Traffic-R1**: A specific model loaded from local disk (`./models/Traffic-R1`) using Hugging Face `transformers`.
- **GGUF Models**: Support for local quantized models via `llama-cpp`.

## Communication Protocols
- **SSE (Server-Sent Events)**: Used in `main.py` and `mcp_server.py` for streaming LLM responses and real-time updates.
- **MCP (Model Context Protocol)**: Integrated as both a server (`mcp_server.py`) and a client (`mcp_client.py`) to expose traffic control tools to LLMs.
- **CORS**: Configured in FastAPI to allow cross-origin requests from frontend dashboards.
