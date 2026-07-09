# Autonomous AI Planner Agent

An advanced, state-driven autonomous AI agent built in Python using the Groq API (Llama 3.1) and Playwright. 

Unlike standard stateless chatbots, this agent features **persistent memory**, **live web scraping tools**, and a **crash-resilient orchestration engine** that decomposes massive goals into steps, tracks its state on disk, and autonomously corrects its own reasoning errors.

## 🚀 Key Features

### 1. State-Driven Orchestrator (`capstone.py`)
The crown jewel of this repository. When given a complex goal, the agent:
* **Decomposes the goal** into an actionable step-by-step plan and saves it to a `plan.json` state machine.
* **Executes steps sequentially** using a ReAct (Reason + Act) loop.
* **Survives Crashes & Rate Limits**: Because the exact state of execution is saved to disk after every step, you can physically force-quit the script (or hit an API rate limit), and upon restarting, the agent will instantly resume from the exact step it left off.
* **Context Aggregation**: Dynamically builds a condensed context window of all previously completed steps before executing the next one, completely eliminating "LLM amnesia" without blowing up the token limit.

### 2. Persistent Memory & Identity (`my_assistant.py`)
A conversational interface featuring long-term memory.
* **Identity Tracking**: Autonomously calls a `remember` tool to extract facts about the user and saves them to a `memory.json` database.
* **Quest/Goal Board**: Allows the user to add and complete tasks. The agent tracks these in a `goals.json` file across sessions.
* **Time-Aware**: Reads the local system clock to dynamically greet the user based on the time of day.

### 3. Tool Execution
* Integrated with **Playwright** for headless browser automation.
* Specifically configured to scrape and extract text from Wikipedia, allowing the agent to bypass CAPTCHAs, avoid API keys, and quickly retrieve highly reliable factual data to solve its goals.

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

## 💻 Usage

To test the **State-Driven Orchestrator** (Recommended):
```bash
python capstone.py
```
*Try giving it a multi-step goal like: "Find the birthdates of Elon Musk and Mark Zuckerberg, and tell me who is older."*

To test the **Persistent Memory Chatbot**:
```bash
python my_assistant.py
```

## 🏗️ Architecture Note
This project was developed in stages, representing the evolution of an AI:
- **Voice**: Structured JSON outputs and Persona prompting.
- **Hands**: Equipping the LLM with Python functions (Playwright).
- **Brain**: The ReAct continuous execution loop.
- **Self**: Disk-based memory and state orchestration.

*Developed as a Capstone Project for the Cognition Loop SOC '26 Program.*
