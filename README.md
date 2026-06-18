# Antigravity Weather Assistant Agent

This repository contains a lightweight **ReAct (Reasoning and Action) Agent** built using Google's **Agent Development Kit (ADK)** and managed by the **Agents CLI (`agents-cli`)**. 

This project was developed as part of **Day 3: Authoring Google Antigravity Skills** of the *"5-Day AI Agents: Intensive Vibe Coding Course With Google"*.

---

## What It Does

The Weather Assistant is designed to answer user queries about the weather and current time by invoking local python tools. It leverages the **Gemini 2.5 Flash** model for planning, tool invocation, and generating responses.

### Key Capabilities & Tools
* **Weather Tool (`get_weather`)**: Simulates a weather database. It returns a foggy weather report for San Francisco and a sunny report for any other location.
* **Time Tool (`get_current_time`)**: Simulates a timezone query. It dynamically calculates and returns the current time in the local timezone for San Francisco.
* **Hybrid Credentials (Local vs. Cloud)**: The codebase is configured to run fully local using Google AI Studio with a `GEMINI_API_KEY`, or deploy natively to Google Cloud (Vertex AI Reasoning Engines) using Application Default Credentials (ADC).

---

## Project Structure

```text
weather-assistant/
├── app/
│   ├── agent.py               # Core agent definitions, tools, and LLM configuration
│   ├── fast_api_app.py        # FastAPI server wrapping the ADK reasoning engine
│   └── app_utils/             # Telemetry, models, and type definitions
├── tests/
│   ├── unit/                  # Basic unit test verification
│   ├── integration/           # Integration tests for streaming and FastAPI e2e
│   └── eval/                  # Evaluation datasets and configs for LLM-as-judge
├── .env                       # Local environment variables (API keys - GIT IGNORED)
├── pyproject.toml             # Python dependencies (managed via Astral uv)
└── README.md                  # Detailed project information
```

---

## Getting Started

### Prerequisites
1. **Python 3.11+**
2. **Node.js**
3. **uv** (Python package manager): [Install uv](https://docs.astral.sh/uv/getting-started/installation/)
4. **agents-cli**: Install globally:
   ```bash
   uv tool install google-agents-cli
   ```

### Setup & Installation
1. Install project dependencies:
   ```bash
   agents-cli install
   ```

2. Create a `.env` file in the root of the project to securely store your API Key (this file is automatically ignored by Git):
   ```text
   GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
   ```

---

## How to Test & Run the Project

### 1. Start the Local Web Playground
To interact with the agent visually in your browser, launch the built-in development UI:
```bash
agents-cli playground
```
Once started, open [http://127.0.0.1:8080/dev-ui/?app=app](http://127.0.0.1:8080/dev-ui/?app=app) in your browser, select `app` from the top dropdown, and start chatting!

### 2. Run a Command Line Query
To run a one-shot query directly from your command line:
```bash
agents-cli run "How is the weather in SF?"
```

### 3. Run Quality Evaluations (LLM-as-a-judge)
To run automated test cases defined in `tests/eval/datasets/basic-dataset.json` and grade the agent's reasoning quality:
```bash
agents-cli eval run
```

### 4. Run Code Unit/Integration Tests
To verify imports, API contracts, and HTTP endpoints:
```bash
uv run pytest
```

---

## Safe Environment Isolation
The project includes a `.gitignore` configured to ensure that local credentials (such as the `.env` file containing the `GEMINI_API_KEY`) are **never** committed or pushed to remote repositories.
