# Shopping Agent — Claude Instructions

## Purpose

This repo contains Claude Code skills for Amazon product research. The primary workflow is:

1. Accept a product query and user-defined scoring criteria
2. Use Chrome DevTools MCP to browse Amazon.com and collect product data
3. Score each product against the criteria
4. Write results to an Excel file (`.xlsx`) and return it to the user

## Skill

`/shop-amazon` — defined in `.claude/skills/shop-amazon.md`

Invoke it when the user asks to find, compare, or evaluate products on Amazon.

## Excel Output Format

When producing the results spreadsheet, always use this column structure:

| Column | Description |
|---|---|
| Rank | Overall rank by weighted score (1 = best) |
| Product Name | Full listing title |
| URL | Direct Amazon.com product link |
| Price | Listed price in USD |
| Rating | Star rating (out of 5) |
| Review Count | Number of customer reviews |
| Prime | Yes / No |
| Estimated Delivery | Delivery window shown on listing |
| [Criterion 1..N] | One column per user-specified criterion, scored 1–10 |
| Weighted Score | Final weighted average across all criteria (0–10) |

- Score each criterion 1–10 based on how well the product satisfies it
- If the user provides weights, apply them to the weighted score
- Sort rows by Weighted Score descending
- Save the file as `amazon_results_<query_slug>_<YYYYMMDD>.xlsx` in the current working directory
- After writing the file, report the file path and the top 3 products in plain text

## Behavior Rules

- Always clarify criteria and weights before starting a search if they are ambiguous
- Collect data on at least 10 products before scoring unless the user specifies fewer
- Never place an order or interact with the cart without explicit user instruction
- Never type or store credentials — prompt the user to log in manually if needed
- Take a screenshot after every major browser action to verify page state
- Prefer Amazon-fulfilled listings over third-party sellers unless the user says otherwise

## Site Target

Amazon.com (US storefront). The user is located in Los Alamos, NM and has a Prime membership — prioritize Prime-eligible results.
