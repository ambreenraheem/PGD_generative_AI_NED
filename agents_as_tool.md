Date: 11-September-2025

<img width="101" height="100" alt="ambreen" src="https://github.com/user-attachments/assets/8d0b1b70-e7a3-462e-924e-5ee4ce0c8652" />

### By Ambreen Abdul Raheem

### Agent as a Tool 🛠️
### 📌 What it Means
- A main agent stays in charge of the conversation.
- The main agent can call other agents (specialists) like tools, but it doesn’t hand over control.
- Those specialists just do small tasks (e.g., translate text, extract dates, summarize content) and return results.

### Why Do We Need Agent as a Tool? 🛠️
When building AI systems, sometimes one main agent should stay in control of the conversation, but still be able to use the skills of specialist agents. That’s where Agent as a Tool comes in.

### 🔑 Benefits
1. Keep Control in One Place 🕹️
- Main agent (like a project manager) stays in charge.
- Specialist agents (like contractors) just provide quick help.
- The conversation doesn’t get messy or jumpy.
#### 💡 Example: You ask a main agent about “latest news.” It stays with you, but quickly calls a specialist agent (entertainment or AI news) to fetch details—then replies back in one flow.

### 2. Modularity (Plug & Play) 🧩
- You can add/remove specialist agents easily.
- Each specialist does one job only (translate, summarize, fetch data).
#### 💡 Example: If tomorrow you need a sports news agent, just add it as another tool—no need to redesign the whole system.

### 3. Cleaner Instructions ✍️
- Each specialist has a focused, simple prompt (e.g., “only summarize AI news”).
- The main agent doesn’t need to know how they work—just when to call them.

### 4. Deterministic Orchestration 🎯
- You control when and how the specialist is used.
- Ensures predictable behavior compared to handing off the whole conversation.

### 💡 Analogy:
- Handoff → Like transferring a caller to another department (you lose control).
- Agent as a Tool → Like muting the caller, asking your colleague for a quick answer, then replying yourself.

### ✅ When to Use It
- When you want quick help from a specialist without breaking flow.
- When you need a structured system (main agent as manager, specialists as helpers).
- When building multi-skill assistants (news fetcher, translator, summarizer, data analyst).

👉 In short: Agent as a Tool = Smarter teamwork inside AI.
One agent manages, others support.

#### This is my Code:
# Example: Agent as a Tool – News Assistant 📰

This example shows how to use **Agent as a Tool** with a main agent that can fetch **Entertainment News** or **AI News** through specialist agents.

```python
import os
from openai import OpenAI
from some_sdk import Agent, Runner   # replace with actual SDK classes

# Initialize OpenAI client
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

# Specialist Agent 1: Entertainment News
entertainment_agent = Agent(
    name="entertainment_news",
    instructions="Fetch and summarize the latest entertainment news in simple bullet points."
)

entertainment_tool = entertainment_agent.as_tool()

# Specialist Agent 2: AI News
ai_news_agent = Agent(
    name="ai_news",
    instructions="Fetch and summarize the latest Artificial Intelligence (AI) news in simple bullet points."
)

ai_news_tool = ai_news_agent.as_tool()

# Main Agent: Orchestrator
main_agent = Agent(
    name="main_agent",
    instructions="""
    You are a smart news assistant. 
    - If the user asks about Entertainment, use the entertainment_news tool.  
    - If the user asks about AI, use the ai_news tool.  
    Always reply in a friendly and clear style.
    """,
    tools=[entertainment_tool, ai_news_tool]
)

# Example user query
user_query = "Can you give me the latest updates in AI news?"

# Run with Runner
response = Runner.run(main_agent, user_query)
print(response)```

### OpenAI SDk python Program:
# Example: Agent as a Tool – Translation Orchestrator 🌍

This example shows how to use **Agent as a Tool** with an **orchestrator agent** that can translate text into Spanish or French using specialist agents.

```python
from agents import Agent, Runner
import asyncio

# Specialist Agent 1: Spanish Translator
spanish_agent = Agent(
    name="Spanish agent",
    instructions="You translate the user's message to Spanish",
)

# Specialist Agent 2: French Translator
french_agent = Agent(
    name="French agent",
    instructions="You translate the user's message to French",
)

# Orchestrator Agent: Uses both translation tools
orchestrator_agent = Agent(
    name="orchestrator_agent",
    instructions=(
        "You are a translation agent. You use the tools given to you to translate. "
        "If asked for multiple translations, you call the relevant tools."
    ),
    tools=[
        spanish_agent.as_tool(
            tool_name="translate_to_spanish",
            tool_description="Translate the user's message to Spanish",
        ),
        french_agent.as_tool(
            tool_name="translate_to_french",
            tool_description="Translate the user's message to French",
        ),
    ],
)

# Runner to execute the orchestrator
async def main():
    result = await Runner.run(orchestrator_agent, input="Say 'Hello, how are you?' in Spanish.")
    print(result.final_output)

# Run the example
asyncio.run(main())```
