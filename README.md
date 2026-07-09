# Autonomous AI Planner Agent: A Journey

This repository tracks the complete evolution of an Autonomous AI Agent built from scratch during the **Cognition Loop SOC '26 Program**. 

What starts as a simple API call script progressively evolves week-by-week into a highly advanced, resilient, state-driven autonomous orchestrator with live web-scraping tools and persistent memory.

## 🚀 The Capstone Project

If you just want to see the final results of the program, look at the final two files:

### 1. The State-Driven Orchestrator (`capstone.py`)
The crown jewel of this repository. When given a massive, complex goal, the agent:
* **Decomposes the goal** into an actionable step-by-step plan and saves it to a `plan.json` state machine.
* **Executes steps sequentially** using a ReAct (Reason + Act) loop combined with Playwright web-scraping tools to find information on Wikipedia.
* **Survives Crashes & Rate Limits**: Because the exact state of execution is saved to disk after every step, you can physically force-quit the script (or hit an API rate limit), and upon restarting, the agent will instantly resume from the exact step it left off.
* **Context Aggregation**: Dynamically builds a condensed context window of all previously completed steps before executing the next one, completely eliminating "LLM amnesia" without blowing up the token limit.

### 2. The Persistent Memory Assistant (`my_assistant.py`)
A conversational interface featuring long-term memory.
* **Identity Tracking**: Autonomously calls a `remember` tool to extract facts about the user and saves them to a `memory.json` database.
* **Quest/Goal Board**: Allows the user to add and complete tasks. The agent tracks these in a `goals.json` file across sessions.
* **Time-Aware**: Reads the local system clock to dynamically greet the user based on the time of day.

---

## 📚 The Learning Journey (File by File)

This repository was built layer by layer. Here is what every file in this project does, in chronological order:

### Part 1: The Voice (Basic LLM Interactions)
* **`basic_call.py`**: The absolute simplest script to send a prompt to the Groq API and get a text response.
* **`persona_call.py`**: Introducing the `system` prompt to force the LLM to adopt a specific personality and behavioral rules.
* **`json_extractor.py`**: Teaching the LLM to output structured data (JSON) instead of plain text, allowing Python to programmatically parse the AI's thoughts.

### Part 2: The Hands (Tools and Automation)
* **`basic_tool.py`**: The first time the LLM is given "tools". The LLM returns a JSON object requesting to use a tool, and Python executes a local function on its behalf.
* **`browser_test.py`**: An introduction to Playwright, opening a headless browser to pull HTML from a live website.
* **`youtube_autoplay.py`**: An advanced Playwright automation script that opens YouTube, searches for a query, and automatically clicks the first video.
* **`research_agent.py`**: Combining the LLM with Playwright. The LLM is given a `search_the_web` tool and can autonomously research facts online.

### Part 3: The Brain (Autonomy and Reasoning)
* **`chat_agent.py`**: Introduction of the continuous "while" loop. The agent can now have a back-and-forth conversation with the user, and can autonomously decide *whether* it needs to use a tool or just talk directly to the user.
* **`rate_limit_handler.py`**: A defensive engineering script testing an exponential backoff algorithm to prevent the program from crashing when the API throws HTTP 429 Rate Limit errors.

### Part 4: The Self (Memory and Orchestration)
* **`my_assistant.py`**: Connecting the `chat_agent` loop to the local file system so it can read and write `memory.json` and `goals.json`, giving the agent a persistent identity across reboots.
* **`capstone.py`**: The final integration of everything above. The chat loop is replaced by a State-Machine Orchestrator that plans, executes, saves state to `plan.json`, handles rate limits, and uses web-scraping tools.

---

## 🛠️ Setup & Installation

1. **Clone the repository:**
```bash
git clone https://github.com/YOUR-USERNAME/AI-Planner-Agent.git
cd AI-Planner-Agent
```

2. **Install Dependencies:**
Make sure you have Python 3 installed, then install the required packages:
```bash
pip install groq python-dotenv playwright
playwright install
```

3. **Configure API Keys:**
Create a `.env` file in the root directory and add your Groq API key:
```env
GROQ_API_KEY=your_groq_api_key_here
```

To run any file, simply execute it with Python, for example:
```bash
python capstone.py
```
