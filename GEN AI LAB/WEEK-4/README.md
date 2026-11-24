# Week 4: Comparing Tokenizers Across Languages

## Overview

This exercise compares how three popular tokenizer families break short English, Telugu, and Hindi sentences into tokens. It prints each tokenizer's token strings, token IDs, and token count so the differences are easy to inspect.

The main takeaway is that a model does not read text as whole words. It processes token IDs, and different model families can split the same sentence differently. Token counts are useful when estimating context usage and API costs, but this small comparison is not a benchmark of model quality or speed.

## What the Program Does

`tokenizer_comparison.py` loads these pretrained tokenizers:

| Display name | Hugging Face model | Tokenizer family |
| --- | --- | --- |
| BPE - GPT-2 | `gpt2` | Byte Pair Encoding |
| WordPiece - Multilingual BERT | `bert-base-multilingual-cased` | WordPiece |
| SentencePiece - XLM-R | `xlm-roberta-base` | SentencePiece |

It runs each tokenizer on the same English, Telugu, and Hindi examples, then displays the resulting tokens, IDs, and counts. Special tokens are included in the counts.

## Files

| File | Purpose |
| --- | --- |
| `tokenizer_comparison.py` | Loads the tokenizers and prints comparisons |
| `requirements.txt` | Lists `transformers` and `sentencepiece` dependencies |

## Skills Practiced

- Loading pretrained tokenizers with Hugging Face Transformers
- Comparing BPE, WordPiece, and SentencePiece tokenization
- Inspecting token strings and integer token IDs
- Seeing how language and model vocabulary can affect token counts
- Recognizing that token counts can inform context and cost planning

## Setup

From the `WEEK-4` directory, install the listed dependencies:

```powershell
pip install -r requirements.txt
```

The tokenizer files are downloaded the first time each model is loaded, so an internet connection is needed for the initial run. Later runs may use the locally cached files.

## Run the Comparison

```powershell
python tokenizer_comparison.py
```

The program prints a section for each language and, within it, the tokens, token IDs, and token count for each tokenizer.

## Progress Summary

Week 4 builds on the earlier API and usage-monitoring work by looking at how prompts are represented before they reach a model. Comparing multiple tokenizer families across languages helps explain why the same text can use different numbers of tokens depending on the model.
