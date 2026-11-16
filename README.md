# Real-Time Web Search AI Agent (LangChain & Tavily)

An autonomous tool-calling AI agent built using **LangChain**, **Google Gemini (`gemini-3.5-flash-lite`)**, and the **Tavily Search API** to overcome static LLM knowledge cutoffs and answer live queries.

## Architecture & Workflow
- **Baseline Comparison:** Demonstrates standard LLM chain limitations on real-time queries due to training cutoffs.
- **Autonomous Tool Calling:** Integrates `TavilySearch` (`max_results=4`) via `langchain.agents.create_agent` so the model dynamically decides when to search the live web.
- **Anti-Hallucination Guardrails:** Enforces structured system prompts instructing the agent to ground responses strictly in retrieved search results or decline when data is insufficient.

## Tech Stack
- **Framework:** Python, LangChain (`langchain`, `langchain-google-genai`, `langchain-tavily`)
- **LLM:** Google Gemini (`gemini-3.5-flash-lite`)
- **Search Tool:** Tavily Search API

## Setup
1. Install dependencies: `pip install -U langchain-google-genai langchain-tavily`
2. Set environment variables `GOOGLE_API_KEY` and `TAVILY_API_KEY`.
3. Run `AGENTIC_AI_2.ipynb`.
