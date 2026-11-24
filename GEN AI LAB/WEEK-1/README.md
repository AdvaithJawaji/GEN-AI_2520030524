# Week 1: Getting Started with Gemini

## Overview

This week introduces the basic workflow for calling a Large Language Model (LLM) from a Python application. The program loads a Gemini API key securely from an environment file, creates a Gemini client, sends a simple question, and prints the generated response.

The main goal of this exercise is to understand how an application sends a prompt to an AI model and receives text in return.

## What I Built

- Loaded configuration from a `.env` file using `python-dotenv`
- Read the Gemini API key from the environment
- Created a Google Gemini client with `google-genai`
- Sent a simple Artificial Intelligence prompt to a Gemini model
- Printed the model's response in the terminal

## Files

| File | Purpose |
| --- | --- |
| `main.py` | Main application entry point |
| `requirements.txt` | Python packages required for this exercise |
| `.env` | Stores the Gemini API key locally |
| `.gitignore` | Keeps sensitive environment files out of version control |

## Skills Practiced

### 1. Environment Configuration

Keeping API keys outside source code is important for security. This week uses `load_dotenv()` and environment variables instead of placing the key directly inside `main.py`.

### 2. Working with an LLM API

The application uses `client.models.generate_content()` to submit the prompt and receive a generated response.

### 3. Python Package Management

The project dependencies are listed in `requirements.txt`, making the environment reproducible.

### 4. Basic Error Handling

The program checks whether `GEMINI_API_KEY` is available and raises a clear message if the key is missing.

## Setup

From the `WEEK-1` directory, create a virtual environment if needed and install the dependencies:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Create a `.env` file with:

```env
GEMINI_API_KEY=your_api_key_here
```

Never commit your real API key to Git.

## Run the Program

```powershell
python main.py
```

The program asks Gemini to explain Artificial Intelligence and prints the returned answer in the terminal.

## Progress Summary

Week 1 is the foundation of the lab. It demonstrates the complete first LLM request flow: configure credentials, connect to Gemini, send a prompt, and display the answer. This is the starting point for the more structured and monitorable applications built in later weeks.
