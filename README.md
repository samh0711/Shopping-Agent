# Shopping Agent

A Claude Code skill that uses Chrome DevTools MCP to browse Amazon, evaluate products against user-defined criteria, and deliver results as a scored Excel spreadsheet.

## What It Does

When prompted, the agent:

1. Takes your product requirements and scoring criteria
2. Drives a real Chrome browser to search and analyze Amazon listings
3. Evaluates each product against your criteria
4. Outputs an `.xlsx` file with one row per product and a column for each criterion, plus an overall score

## Usage

Invoke the skill from Claude Code:

```
/shop-amazon find me a standing desk under $400 — score on: price, weight capacity, height range, reviews, Prime eligibility
```

The agent will ask clarifying questions if needed, then return a ranked Excel file when done.

## Inputs

| Input | Description |
|---|---|
| Search query | What you want to buy |
| Criteria | The factors to score (price, brand, rating, delivery speed, etc.) |
| Weights (optional) | Relative importance of each criterion |
| Filters (optional) | Price range, Prime-only, minimum rating, etc. |
| Result count (optional) | How many products to evaluate (default: 10) |

## Output

An Excel file (`.xlsx`) with:

- One row per product
- Columns for product name, URL, price, and each user-specified criterion
- A weighted score column
- Rows sorted by score descending

## Requirements

- Claude Code with Chrome DevTools MCP configured
- Chrome browser available on the host machine
- An active Amazon.ca session (the agent will prompt you to log in if needed)

## Safety Rules

- The agent **never places an order** without explicit user approval
- Payment information and credentials are never stored or typed by the agent
- All purchases require a final confirmation step showing the full order total

## Files

```
.claude/
  skills/
    shop-amazon.md    # Skill definition loaded by Claude Code
```
