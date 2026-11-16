# Autonomous Market & Tech Intelligence Agent (LangChain & Tavily)

An autonomous tool-calling AI agent built with **LangChain**, **Google Gemini (`gemini-3.5-flash-lite`)**, and the **Tavily Search API** to overcome static LLM knowledge cutoffs and synthesize real-time web information without hallucinations.

## System Architecture Flow

```
User Query ──▶ LangChain Agent (Gemini 3.5 Flash Lite)
                    │
                    ├──▶ [Needs Live Info?] ──▶ Tavily Search API (Top 4 Web Results)
                    │                                  │
                    ▼                                  ▼
             Direct Answer ◀────────── Grounded Synthesis (Zero Guessing)
```

## Key Features & Guardrails
- **Baseline vs. Agent Evaluation:** Demonstrates standard LLM chain limitations on real-time queries due to static training cutoffs, contrasted against autonomous web retrieval.
- **Autonomous Tool Calling:** Integrates `TavilySearch` (`max_results=4`) via `langchain.agents.create_agent` so the LLM dynamically decides when to trigger live internet searches.
- **Anti-Hallucination Prompting:** Enforces strict system instructions requiring the agent to answer exclusively from retrieved search results or decline when data is insufficient.

## Sample Output (Before vs. After)
- **Standard LLM Chain (`prompts | llm`):** *"I cannot provide today's AI tech news because I do not have access to real-time information or the internet. My knowledge cutoff is January 2025."*
- **Tavily Web Search Agent (`create_agent`):** Autonomously queries live news sources and returns a structured summary of the top 10 current AI industry developments.



## Sample Output (Before vs. After Tool Calling)

### User Query
> `top 10 AI tech news today`

### 1. Standard LLM Chain (`prompts | llm` — Without Search Tool)
```
I cannot provide today's AI tech news because I do not have access to real-time 
information or the internet. My knowledge cutoff is January 2025. Please check a 
live tech news website for the latest updates!
```

### 2. Autonomous LangChain + Tavily Agent (`create_agent` — With Live Web Search)
```
Based on recent developments, here are 10 of the top AI tech news stories and trends:

1. LangChain Secures Massive Funding at $3B Valuation: LangChain closed a $300M 
   Series C round led by Alphabet's CapitalG as LangSmith adoption grows across 
   enterprises like Nvidia and Toyota.
2. OpenAI Disbands Standalone Robotics Team: OpenAI restructured internal divisions, 
   integrating robotics researchers into its core research group under Mark Chen.
3. OpenAI Introduces "Businesses in ChatGPT": Rolled out a business hub equipped 
   with chat-inspecting capabilities and AI agents.
4. Stanford Releases "Memorilla" Open-Source Memory Module: Released a 194M-parameter 
   memory module compressing long documents into 16 latent tokens to cut latency.
5. Google Limits Gemini 4 Carbon to Cyber Defenders: Rolled out Gemini 4 Carbon 
   explicitly to vetted security teams for threat-mitigation workflows.
... (summarized from top 4 real-time Tavily search results)
```

## Tech Stack
- **Language & Orchestration:** Python, LangChain (`langchain`, `langchain-google-genai`, `langchain-tavily`)
- **LLM:** Google Gemini (`gemini-3.5-flash-lite`)
- **Live Search Tool:** Tavily Search API

## Setup & Execution
1. Install dependencies: `pip install -r requirements.txt`
2. Configure environment variables: `GOOGLE_API_KEY` and `TAVILY_API_KEY`
3. Run `autonomous_research_agent.ipynb`
