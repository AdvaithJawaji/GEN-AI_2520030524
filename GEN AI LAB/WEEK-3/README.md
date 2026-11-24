# Week 3: Monitoring, Reliability, and Cost Awareness

## Overview

This week develops the provider client into a monitored and more reliable application. It records token usage, latency, estimated cost, provider status, and errors. It also retries temporary failures and saves successful or failed calls to MongoDB.

The exercise brings together three important skills for real LLM applications: observability, resilience, and usage awareness.

## What I Built

- Reused the Gemini and Ollama provider abstraction
- Added structured `LLMResult` objects containing text and token counts
- Measured request latency with `time.perf_counter()`
- Added three-attempt retry handling for temporary failures
- Added exponential backoff between retries
- Estimated Gemini API cost from input and output token counts
- Recorded usage details to MongoDB
- Added unit coverage with fake provider and logger classes

## Files

| File | Purpose |
| --- | --- |
| `main.py` | Starts provider selection and closes the MongoDB connection safely |
| `llm_client.py` | Handles provider calls, retries, metrics, and cost estimates |
| `usage_logger.py` | Connects to MongoDB and stores usage records |
| `test_client.py` | Tests successful generation and usage logging |
| `requirements.txt` | Required packages for LLM clients, testing, environment variables, and MongoDB |
| `.env` | Stores API keys, database settings, and optional pricing values |

## Skills Practiced

### 1. Structured Response Data

`LLMResult` keeps the response text separate from input tokens and output tokens. This is more maintainable than returning only plain text.

### 2. Latency Measurement

Each call is timed from start to finish. Latency is recorded in milliseconds and helps identify slow providers or network problems.

### 3. Token and Cost Monitoring

Gemini usage metadata is read where available, while Ollama reports prompt evaluation and generated token counts. Gemini cost is estimated using environment-based input and output prices:

- `GEMINI_INPUT_PRICE_PER_MILLION`
- `GEMINI_OUTPUT_PRICE_PER_MILLION`

Local Ollama usage is logged with no hosted API charge.

### 4. Retry Handling

The client retries temporary problems such as timeouts, connection errors, and retryable HTTP status codes. The wait increases between attempts as `1`, `2`, and then stops after three attempts.

### 5. MongoDB Logging

`UsageLogger` writes call records to:

- Database: `llm_monitoring`
- Collection: `api_usage`

Each record can include the provider, model, tokens, latency, cost, status, attempts, timestamp, and error details.

### 6. Unit Testing

The fake provider returns a known `LLMResult`, and the fake logger captures usage records. This allows tests to verify token totals and status without using a live API or database.

## Setup

From the `WEEK-3` directory:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Set the required values in `.env`:

```env
GEMINI_API_KEY=your_api_key_here
MONGODB_URI=your_mongodb_connection_uri
GEMINI_INPUT_PRICE_PER_MILLION=0
GEMINI_OUTPUT_PRICE_PER_MILLION=0
```

Use actual Gemini pricing values if you want the cost estimate to represent your account's model pricing.

For Ollama, keep the local Ollama service running and make sure `llama3.2` is installed.

## Run the Program

```powershell
python main.py
```

Choose `gemini` or `ollama`, enter a prompt, and compare:

- Response text
- Input and output tokens
- Latency
- Estimated cost
- MongoDB logging status

## Run Tests

```powershell
python -m unittest test_client.py
```

or:

```powershell
pytest
```

## Progress Summary

Week 3 moves the project from a working LLM client to an application that can be observed and diagnosed. It demonstrates how to measure cost and performance, handle failures, and persist operational data. These practices prepare the project for larger workloads and more advanced monitoring in later weeks.
