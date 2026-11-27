# Week 6: LLM Baseline Evaluation

This project runs a 30-question golden set against the local Llama 3.2 model through Ollama. It compares each response with expected keywords, prints a score and status, and saves detailed results to `baseline_results.csv`. It also includes a small next-word autoregression demo.

## Requirements

- Python 3.10+
- [Ollama](https://ollama.com/) with the `llama3.2` model
- Python package in `requirements.txt`

## Run

From this directory:

```powershell
ollama pull llama3.2
python -m pip install -r requirements.txt
python main.py
```

Run the next-word demo separately:

```powershell
python autoregression.py
```

The evaluation marks keyword coverage of at least 60% as `PASS`; lower scores are `REVIEW`. This is a simple baseline metric, not a complete measure of answer accuracy.
