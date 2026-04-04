# RAG Code Analyst

Universal Retrieval-Augmented Generation system for analyzing Python code repositories.

Python 3.10+ | LangChain 0.3.27 | Ollama | Active Development

## Overview

RAG Code Analyst is a Jupyter notebook that transforms any Python repository into a searchable knowledge base using RAG. Ask questions about the codebase in natural language and get intelligent answers based on actual code analysis.

## Quick Start

### 1. Install Ollama and pull models

curl -fsSL https://ollama.com/install.sh | sh
ollama pull hf.co/Casual-Autopsy/snowflake-arctic-embed-l-v2.0-gguf:Q4_K_M
ollama pull gemma3:4b

### 2. Install Python dependencies

pip install -r requirements.txt

### 3. Run the notebook

jupyter notebook git_rag.ipynb

### 4. Configure and run

Edit the first cell in the notebook:

- Set GITHUB_URL to any public Python repository (example: https://github.com/psf/requests.git)
- Or set REPO_PATH to your local project
- Run all cells
- Ask questions about the codebase

## Configuration

All settings are in the first cell:

- GITHUB_URL: GitHub repository URL (default: https://github.com/psf/requests.git)
- REPO_PATH: Local repository path (default: ./temp_repo)
- CHUNK_SIZE: Document chunk size (default: 2000)
- TOP_K_RESULTS: Number of retrieved chunks (default: 5)
- LLM_MODEL: Ollama language model (default: gemma3:4b)
- RUN_DIAGNOSTICS: Enable retrieval debugging (default: True)
- USE_IMPROVED_PROMPT: Use analytical prompt (default: True)

## How It Works

1. Loads Python files from the specified repository
2. Splits code into intelligent chunks
3. Creates embeddings using local Ollama models
4. Stores vectors in ChromaDB (created automatically)
5. For each query: finds relevant chunks and asks LLM to answer

## Example Questions

For the requests library:

- How to send POST request with JSON data?
- What does the Session class do?
- How are Cookies handled?
- What authentication methods are available? 

## Troubleshooting

Ollama connection error:
Make sure Ollama is running: ollama serve

Poor answers:
Enable RUN_DIAGNOSTICS = True to see what chunks are being retrieved

Repository not found:
Check URL format (should end with .git)

## Project Status (Active Development)

This project is under active development.

Completed:
- Basic RAG pipeline working
- GitHub and local repository support
- Configurable chunking and retrieval
- Diagnostic mode

In Progress:
- Extracting loader into standalone module
- Moving configuration to separate file
- Improving prompt engineering

Planned:
- Support for more programming languages (JS, Java, Go)
- CLI interface (no notebook required)
- Web UI with Streamlit
- Documentation format support (Markdown, RST, PDF)

## Requirements

- Python 3.10+
- Ollama installed locally
- Git (for cloning repositories)
- 8GB+ RAM (for running LLM locally)

## License

MIT

Note: The vector database (ChromaDB) is created automatically when you run the notebook and can be deleted safely. It will be recreated on the next run.