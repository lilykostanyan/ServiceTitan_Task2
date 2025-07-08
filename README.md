# ServiceTitan_Task2

 ## RAG Chatbot System Evaluation
This project contains a performance and cost analysis of a Retrieval-Augmented Generation (RAG) chatbot system used internally by a company. The project includes code notebooks, visualizations, and written analysis addressing key issues impacting chatbot accuracy and latency.

## Contents
- task2.ipynb — Jupyter Notebook for analyzing user feedback, latency violations, and data source quality and cost-benefit analysis comparing re-ranking vs. increased context size (combines Task 1 & Task 2, just the name comes from the internship's selections 2nd stage)

logs.json — Sample log data used for all evaluations

reports — Final write-ups for Task 1 and Task 2 (PDFs)

## Task 1: Root Cause Analysis
After analyzing the logs, we identified two critical problems:

Problem 1: Outdated Answers from PDF Sources
Component: Retrieval

Data Source: Archived PDFs

Issue: 28% thumbs-down rate from PDF-sourced answers

Cause: Static, outdated information is still being retrieved

Impact: Reduces user trust and accuracy

Problem 2: SLA Latency Violations
Component: Generation

Model: LLaMA 3-70B

Issue: 28.4% of queries exceed 3,500ms latency SLA

Cause: Long or verbose inputs increase token load

Impact: Slow response time damages usability

## Task 2: Quantitative Trade-Off Analysis
To improve answer relevance, two options were proposed:

Option	Description	Latency	Monthly Cost	Token Load	Recommendation
A	Add Cohere Re-ranker	+600ms	$100	No change	**Best choice**
B	Increase k=4 → k=10	+250ms + gen delay	$720	+240M tokens	**Too risky**

### Recommendation: Option A (Re-ranker)
Avoids additional stress on LLaMA 3 generation

Improves precision without increasing token count

More cost-effective and safer under SLA constraints

## Key Insights
Live sources like Engineering Wiki (85% thumbs-up) outperform static PDFs (28% thumbs-down)

Most latency issues come from verbose queries and large contexts passed to LLaMA 3

Reranking top-10 chunks before generation is a better fix than expanding context

## Usage
Clone the repo
```bash
git clone https://github.com/your-username/rag-chatbot-analysis.git
```
Open Terminal
```bash
cd ServiceTitan_Task2
```

```bash
python task2.ipynb
```

## Requirements
Python 3.6+

pandas

matplotlib

## Author
Lili Kostanyan