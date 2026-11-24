# Week 5: Planning Token Usage and LLM Budgets

## Overview

This exercise estimates whether a proposed LLM feature fits within token-rate limits and daily and monthly spending budgets. You provide assumptions such as requests per day, average prompt and response sizes, provider prices, and configured limits. The program calculates estimated usage and cost, applies a safety margin, and reports which checks pass.

These are planning estimates based on the values you enter. They are not live usage measurements or billing data.

## What the Program Calculates

- Estimated input, output, and total tokens per day
- Estimated daily cost from input and output token prices
- Estimated monthly cost, using a 30-day month
- Peak requests per minute (RPM) and tokens per minute (TPM), adjusted for a safety margin
- Whether the RPM, TPM, daily budget, and monthly budget checks pass

The program prints a recommendation to stay within the configured planning limits or to revise the assumptions, limits, or design.

## Files

| File | Purpose |
| --- | --- |
| `budget.py` | Defines `FeatureBudget`, reads its settings from environment variables, and prints the report |
| `test_budget.py` | Tests cost estimates and limit-check outcomes |
| `.env` | Holds local planning settings; do not put secrets in a committed example |

## Skills Practiced

- Estimating token volume from request patterns
- Calculating input and output costs separately
- Checking RPM and TPM capacity
- Applying a safety margin to peak and budget checks
- Loading configuration from environment variables
- Testing budget calculations and pass/fail scenarios

## Configuration

`budget.py` reads these variables from `.env`. Values shown below are examples for planning only; replace them with assumptions and limits appropriate to your feature and provider.

```env
REQUESTS_PER_DAY=1000
AVG_INPUT_TOKENS=1000
AVG_OUTPUT_TOKENS=500
PEAK_REQUESTS_PER_MINUTE=10
INPUT_PRICE_PER_MILLION=1.0
OUTPUT_PRICE_PER_MILLION=2.0
RPM_LIMIT=100
TPM_LIMIT=50000
MONTHLY_BUDGET_USD=100
DAILY_BUDGET_USD=5
SAFETY_MARGIN_PERCENT=20
```

If a value is missing, the program uses `0` for most settings and `20` for the safety margin. Use the actual model's published input and output prices when making a cost estimate.

## Setup

The Week 5 folder does not include its own `requirements.txt`. The program uses `python-dotenv`; install it if it is not already available:

```powershell
python -m pip install python-dotenv
```

Create a `.env` file in the `WEEK-5` directory and set the variables above.

## Run the Budget Estimate

From the `WEEK-5` directory:

```powershell
python budget.py
```

Review the estimated usage, costs, and each `PASS` or `REVIEW` result. Update your assumptions and run it again when traffic, model pricing, rate limits, or budgets change.

## Run Tests

```powershell
python -m unittest -v test_budget.py
```

The tests cover the daily and monthly cost calculations, capacity checks, and examples where RPM or monthly budget limits are exceeded.

## Progress Summary

Week 5 turns token counts and pricing into a practical planning exercise. Alongside the tokenizer comparison from Week 4, it helps connect how much a model processes with the capacity and budget a feature may need before it is built.
