# Local Deep Research

A powerful local research assistant that performs deep, iterative research using local LLMs and web search — no API keys required for core functionality.

> Fork of [LearningCircuit/local-deep-research](https://github.com/LearningCircuit/local-deep-research)

## Features

- 🔍 **Deep iterative research** — Automatically generates follow-up questions and refines searches
- 🤖 **Local LLM support** — Works with Ollama, LM Studio, and other local model servers
- 🌐 **Multiple search backends** — DuckDuckGo, SearXNG, Brave Search, and more
- 📄 **Rich output formats** — Markdown reports with citations and source tracking
- 🔒 **Privacy-first** — Research stays on your machine
- ⚡ **Fast** — Parallel search and summarization pipelines

## Requirements

- Python 3.10+
- [Ollama](https://ollama.ai) (recommended) or any OpenAI-compatible local server
- 8GB+ RAM (16GB recommended for larger models)

## Quick Start

```bash
# Clone the repository
git clone https://github.com/your-org/local-deep-research.git
cd local-deep-research

# Install dependencies
pip install -e .

# Pull a model (if using Ollama)
ollama pull mistral

# Run a research query
python -m local_deep_research "What are the latest advances in fusion energy?"
```

## Installation

### From PyPI

```bash
pip install local-deep-research
```

### From Source

```bash
git clone https://github.com/your-org/local-deep-research.git
cd local-deep-research
pip install -e ".[dev]"
```

## Configuration

Copy the example config and edit as needed:

```bash
cp config/settings.example.toml config/settings.toml
```

Key settings:

| Setting | Default | Description |
|---|---|---|
| `llm.model` | `mistral` | Local model to use |
| `llm.base_url` | `http://localhost:11434` | Ollama/LM Studio endpoint |
| `search.backend` | `duckduckgo` | Search engine backend |
| `research.iterations` | `3` | Number of research iterations |
| `research.max_results` | `10` | Max search results per query |

> **Personal note:** I find 3 iterations hits a good balance between depth and speed for most queries on my machine. Bump to 5+ for more thorough research on complex topics.

## Usage

### Command Line

```bash
# Basic research
local-deep-research "Your research question here"

# Specify output format
local-deep-research --format markdown "Your question" > report.md

# Adjust depth
local-deep-research --iterations 5 --results 10 "Your question"

# Use a specific model
local-deep-research --model llama3 "Your question"
```

### Python API

```python
from local_deep_research import ResearchAgent

agent = ResearchAgent(
    model="mistral",
    search_backend="duckduckgo",
    iterations=3,
)

report = agent.research("What are the health effects of intermittent fasting?")
print(report.summary)
print(report.sources)
```

## Architecture

```
local_deep_research/
├── agent.py          # Main research agent orchestration
├── search/           # Search backend implementations
├── llm/              # LLM client w
```

## Personal Notes

- I'm running this with `llama3.1:8b` on a 16GB RAM machine — works great for most topics.
- SearXNG backend gives noticeably better results than DuckDuckGo for technical queries; worth setting up if you do a lot of research.
- Saving outputs to a local `reports/` directory with dated filenames has been handy for keeping track of things:
  ```bash
  local-deep-research --format markdown "Your question" > reports/$(date +%Y-%m-%d)-topic.md
  ```
