# LangChain Course

This repository is a small educational project that demonstrates how to build a simple LangChain workflow with a local LLM using Ollama. The application takes a text about a public figure, passes it to a prompt template, and asks the model to return a short summary and two interesting facts.

## Overview

The project is intentionally minimal and focused on learning the basics of:

- LangChain prompt composition
- Model integration with `langchain_ollama`
- Prompt templates and chains
- Running a local LLM in a simple Python application

## Project Structure

```text
.
├── main.py                  # Application entry point
├── pyproject.toml           # Project metadata and dependencies
├── src/
│   └── langchain_course/
│       └── __init__.py     # Package entry point
├── .python-version          # Local Python version pin
├── uv.lock                  # Locked dependencies for uv
├── .gitignore
└── README.md
```

## Requirements

- Python 3.9 or newer
- Ollama installed and running locally
- A compatible model available in Ollama (the example uses `gemma3:270m`)

## Setup

1. Clone the repository
2. Install dependencies:

```bash
uv sync
```

3. Make sure Ollama is installed and the model is available:

```bash
ollama pull gemma3:270m
```

4. Run the app:

```bash
uv run python main.py
```

## How It Works

The script in `main.py`:

- loads environment variables with `python-dotenv`
- defines a `PromptTemplate`
- creates a LangChain chain using `ChatOllama`
- sends a biography text to the model
- prints a generated summary and interesting facts

## Example Flow

```python
summary_prompt_template = PromptTemplate(
    input_variables=["information"],
    template="""
    given the information {information} about a person i want you to create:
    1. a short summary
    2. two interesting fact about them
    """
)

llm = ChatOllama(temperature=0, model="gemma3:270m")
chain = summary_prompt_template | llm
```

## Notes

This is a basic learning example meant to help understand how LangChain and local LLMs can be combined in a small project. It is not intended as a production-ready application or a full AI service implementation.
