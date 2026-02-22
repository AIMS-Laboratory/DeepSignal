# Technology Stack

## Languages & Runtime
- **Language**: Python
- **Runtime**: Python 3.13+
- **Environment Management**: uv (judging by `uv.lock`), pip, conda (judging by `requirements.txt` file paths)

## Frameworks & Core Libraries
- **API Framework**: [FastAPI](https://fastapi.tiangolo.com/) (serving as the main application and SSE provider)
- **Simulation**: [SUMO (Simulation of Urban MObility)](https://eclipsedev.statmt.org/sumo/) via `traci` and `libsumo`
- **MCP Framework**: [FastMCP](https://github.com/modelcontextprotocol/python-sdk) (implementing the Model Context Protocol for traffic control tools)
- **UI/Dashboard**: [Streamlit](https://streamlit.io/) (used for demonstration and visualization)
- **Data Visualization**: [Plotly](https://plotly.com/), [Matplotlib](https://matplotlib.org/)
- **LLM SDKs**:
  - `openai` (compatible with DashScope, SiliconFlow, LM-Studio)
  - `anthropic`
  - `dashscope` (Alibaba Cloud)
- **Local LLM Execution**:
  - `transformers` & `torch` (for "Traffic-R1" model)
  - `llama-cpp-python` (for GGUF models)

## Main Dependencies
- **Data Handling**: `numpy`, `pandas`
- **Networking**: `httpx`, `aiohttp`, `uvicorn`
- **Logging & Validation**: `loguru`, `pydantic`
- **Utilities**: `python-dotenv`, `watchdog`, `lxml` (for SUMO XML parsing)

## Configuration
- **Environment Variables**: Managed via `.env` (API keys: `DASHSCOPE_API_KEY`, `SILICONFLOW_API_KEY`, `ANTHROPIC_API_KEY`, model paths, URLs)
- **Project Config**: `pyproject.toml` using standard PEP 621 metadata
- **SUMO Config**: `.sumocfg` files in `scenarios/` and `sumo_llm/`
- **Junction Config**: `.json` files (e.g., `J54_data.json`) describing traffic light phases and lane mappings
