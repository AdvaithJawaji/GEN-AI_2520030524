# Week 7: Next-Token Prediction

This project compares next-token predictions using GPT-2 locally and through Hugging Face inference. The scripts show the prompt, likely next tokens, and their probabilities.

## Requirements

- Python 3.10+
- Install packages listed in `requirements.txt`
- Internet access to download GPT-2 for the local scripts
- A Hugging Face access token and compatible model ID for `huggingface.py`

## Run local predictions

From this directory:

```powershell
python -m pip install -r requirements.txt
python main.py
```

`local_model.py` provides another local GPT-2 prediction example:

```powershell
python local_model.py
```

## Run Hugging Face inference

Set `HF_TOKEN` and `HF_MODEL_ID` in a local `.env` file, then run:

```powershell
python huggingface.py
```

Keep `.env` private; never commit access tokens. The selected model must support text generation with detailed top-token scores.
