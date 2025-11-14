# Web Research Agent (ReAct + OpenAI + Tavily)

This repository contains an AI-powered research agent that turns any topic into a structured, decision-ready research brief.  
The system uses a ReAct-style reasoning loop, OpenAI GPT-4o for planning and synthesis, and Tavily for live web search.

---

## Overview

Given a single topic, the agent will:

1. Generate 5–6 high-quality research questions  
2. Perform web searches for each question  
3. Extract factual key points and credible sources  
4. Produce a polished Markdown report  
5. Return a concise, business-friendly research summary  

This workflow delivers fast, structured insight suitable for business, academic, and strategic use cases.

---

## Architecture

### ReAct Loop

The agent uses an explicit Reasoning + Acting workflow based on XML-style tags:

```
<thought>...</thought>
<tool_call>{"name": "...", "arguments": {...}}</tool_call>
<observation>...</observations>
<response>...</response>
```


This structure provides predictable tool execution and transparent reasoning steps.

### Tools

Tools are defined as Python functions with signatures automatically injected into the system prompt.  
Available tools:

- `generate_research_questions(topic)`  
  Produces 5–6 researchable, domain-diverse questions.

- `get_research_answer(rq)`  
  Performs Tavily search and extracts structured key points and sources.

- `write_report(topic, research_data)`  
  Synthesizes all findings into a clean, shareable Markdown report.

### ReactAgent Class

The `ReactAgent` coordinates the full loop:

- Tracks conversation history  
- Sends messages to the LLM  
- Extracts tool calls from `<tool_call>` tags  
- Executes the corresponding Python tool  
- Inserts results back as `<observation>`  
- Continues until the model returns a final `<response>`  

Colorized logs (via `colorama`) make execution traces readable in notebooks.

---

## Tech Stack

- Python  
- OpenAI GPT-4o  
- Tavily Web Search  
- Google Colab for secret storage  
- Libraries: `openai`, `tavily-python`, `colorama`

---

### Business Applications

This agent is designed for workflows requiring rapid, structured insight:

- Market and competitive intelligence
- Product and technology landscape research
- Policy and regulatory summaries
- Academic research preparation
- Executive and strategy brief creation

The system emphasizes factual grounding, sources, and clear structure, making it suitable for real business environments.

---

### Extending the Agent

You can easily extend the system by adding new tools:

- Financial data retrieval
- PDF or document summarization
- RAG-based internal knowledge lookup
- Company or industry profiling tools

The agent can also be adapted to produce alternative outputs (slides, executive summaries, JSON for dashboards).

---

Limitations

- Web search is snippet-based (no full-page retrieval)
- No caching or retry logic
- No hallucination detection layer
- Research data lives only in runtime memory

