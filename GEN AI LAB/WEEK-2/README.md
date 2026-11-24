# Week 2: Building a Multi-Provider LLM Client

## Overview

This week improves the basic LLM application by supporting two different providers: hosted Gemini and local Ollama. Instead of calling one provider directly, the application uses a common provider interface and a shared `LLMClient`.

The key lesson is to separate provider-specific code from application logic so that switching models does not require rewriting the whole program.

## What I Built

- Added an abstract `LLMProvider` interface
- Implemented Gemini through the Google Gen AI SDK
- Implemented Ollama through its local REST API
- Created an `LLMClient` that works with any compatible provider
- Added a command-line provider choice
- Added an isolated unit test using a fake provider

## Files

| File | Purpose |
| --- | --- |
| `main.py` | Prompts the user for a provider and question |
| `llm_client.py` | Contains provider implementations and the common client |
| `test_client.py` | Tests `LLMClient` with a fake provider |
| `requirements.txt` | Dependencies for API calls, environment settings, and testing |
| `.env` | Stores provider configuration such as the Gemini API key |
| `.gitignore` | Excludes local environment and generated files |

## Skills Practiced

### 1. Abstraction and Interfaces

`LLMProvider` defines a single `generate(prompt)` contract. Both Gemini and Ollama implement that contract, while `LLMClient` depends on the interface rather than a specific provider.

### 2. Provider Selection

The user chooses `gemini` or `ollama` at runtime. This makes the same application capable of using a hosted cloud model or a locally running model.

### 3. Local and Hosted Models

- Gemini uses `google-genai` and requires an API key.
- Ollama sends a REST request to `http://localhost:11434/api/generate`.
- The Ollama model used in this exercise is `llama3.2`.

### 4. Testability

`test_client.py` supplies a fake provider instead of calling a real model. This confirms that the common client correctly passes the prompt and returns the provider response.

## Setup

From the `WEEK-2` directory:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

For Gemini, add the following to `.env`:

```env
GEMINI_API_KEY=your_api_key_here
```

For Ollama, make sure Ollama is installed and the `llama3.2` model is available locally.

## Run the Program

```powershell
python main.py
```

Choose either `gemini` or `ollama`, enter a question, and review the response.

## Run Tests

```powershell
python -m unittest test_client.py
```

or:

```powershell
pytest
```

## Progress Summary

Week 2 moves from a one-off Gemini example to a reusable LLM architecture. The provider abstraction makes the application easier to extend, test, and maintain. It also introduces the useful comparison between hosted API inference and local model inference.
