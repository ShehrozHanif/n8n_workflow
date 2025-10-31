# 🧠 **Workflow Name:** Multi_Agent_System

This workflow is a **multi-agent AI assistant system** built in **n8n** that integrates:

* 🧩 **Google Gemini** (for reasoning and language generation)
* 📊 **Google Sheets** (for company contact data)
* 📅 **Google Calendar** (for event scheduling)
* 💬 **Chat Interface Trigger** (for real-time interaction)
* 🧠 **Memory Buffer** (for context awareness)

It basically acts as your **virtual AI employee** that can talk, recall, look up contact data, and even create meetings automatically.

---

## ⚙️ **Node-by-Node Breakdown**

### 1️⃣ **When Chat Message Received**

**Type:** `@n8n/n8n-nodes-langchain.chatTrigger`
**Role:** Entry point of the workflow

Whenever you send a chat message (like:

> “What’s the email of Sir Zia Khan?” or
> “Schedule a meeting with Bilal tomorrow at 5 PM”),

this node **triggers** the entire AI system to start working.

🟢 **Purpose:** Listens to user input (like ChatGPT’s “prompt box”).

---

### 2️⃣ **AI Agent**

**Type:** `@n8n/n8n-nodes-langchain.agent`
**System Prompt:**

> “You are an assistant that can access company contact information using a tool named ‘Get Contact data’.
> When a user asks for contact details, use that tool.
> Do not make assumptions.”

This is the **main brain** of the workflow.
It understands your request, decides which “tool” (Google Sheets or Calendar) to use, and orchestrates everything.

🧠 Example:

> You: “Tell me Bilal’s email.”
> Agent: Calls “Get Contact Data” → fetches Bilal’s email → replies.

> You: “Create a meeting with Zain tomorrow at 3 PM.”
> Agent: Calls “Google Calendar Tool” → schedules event → confirms.

🟢 **Purpose:** Central logic hub that connects LLM, tools, and memory.

---

### 3️⃣ **Google Gemini Chat Model**

**Type:** `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`
This is your **language model** — the AI that interprets questions and generates human-like answers.
It gives your agent **intelligence, reasoning, and natural conversation skills**.

🟢 **Purpose:** Understands and communicates intelligently with the user.

---

### 4️⃣ **Simple Memory**

**Type:** `@n8n/n8n-nodes-langchain.memoryBufferWindow`
Adds **short-term memory** — so your agent remembers the last few messages.

🧠 Example:

```
You: Who is Bilal?
AI: Bilal is a Sales Manager.
You: What’s his email?
AI: bilal@company.com  ← remembers context
```

🟢 **Purpose:** Enables conversational continuity (no need to repeat names or details).

---

### 5️⃣ **Get Contact Data**

**Type:** `n8n-nodes-base.googleSheetsTool`
**Connected to:** A Google Sheet (`Contacts_CSV_template`)
**Contains:** Employee names, emails, phone numbers, and notes.

This is a **custom AI tool** your agent uses to **search for contact info** directly from Google Sheets.

🧩 Example:

> You: “What’s Ahmed’s number?”
> → Agent uses this node → reads from the sheet → gives answer.

🟢 **Purpose:** Makes your AI agent data-aware — it can query real company data.

---

### 6️⃣ **Event Calendar**

**Type:** `n8n-nodes-base.googleCalendarTool`
Connected to your **Google Calendar account**.

The agent uses this tool to **create events** when asked.

🧩 Example:

> You: “Schedule a call with Sara tomorrow at 5 PM.”
> → AI understands → creates event in your Google Calendar automatically.

🟢 **Purpose:** Gives your agent real-world action capability (not just text).

---

## 🔗 **Workflow Logic Flow**

```
💬 Chat Trigger
     ↓
🧠 AI Agent (LangChain)
     ↓
├── Google Gemini (thinking & response)
├── Google Sheets (contact info lookup)
└── Google Calendar (event creation)
     ↓
🧠 Memory (keeps conversation context)
```

Each tool can be called dynamically depending on what the user asks.

---

## 🚀 **Key Benefits**

| Feature                          | Benefit                                                                |
| -------------------------------- | ---------------------------------------------------------------------- |
| 🧠 **Autonomous Agent**          | The AI decides which tool to use — no manual commands needed.          |
| 🧾 **Google Sheets Integration** | Centralized access to contact information without switching apps.      |
| 📅 **Calendar Integration**      | Automates scheduling tasks — no need to open Google Calendar manually. |
| 💬 **Chat Interface**            | Natural, human-like conversation.                                      |
| 🧩 **Memory Buffer**             | Handles contextual multi-turn chats gracefully.                        |
| ⚙️ **No-Code Build**             | Entire system made visually in n8n — perfect for automation beginners. |

---

## 💡 **Real-World Use Cases**

1. **Smart Company Assistant** — Employees can ask for contact info, schedule meetings, or check notes instantly.
2. **Customer Support Automation** — Fetch client details and log meeting events without switching tools.
3. **AI Secretary** — Personal assistant that manages contacts and your calendar through natural language.
4. **Multi-Agent Expansion Base** — You can add more tools like Notion, Gmail, or Slack to make it even smarter.

---

## 🏁 **In Summary**

✅ **What it does:**
A multi-agent AI system that listens, thinks, remembers, and acts — combining Google Sheets + Calendar + Gemini.

✅ **How it helps:**
Saves hours of manual lookup and scheduling by automating communication tasks through natural chat commands.

✅ **Big Picture:**
You’ve essentially built your own **AI-powered Office Assistant** — a step toward autonomous workplace automation 🚀

---









## Linkedin Post

---

# 🚀 **I just built my own Multi-Agent AI System inside n8n — and it feels like having a digital assistant that actually works for me!**

Imagine sending a simple message like:

> “What’s Bilal’s email?”
> “Schedule a meeting with Sara tomorrow at 5 PM.”

…and an AI system automatically:
✅ Finds the right data from Google Sheets
✅ Creates an event in Google Calendar
✅ Replies to you — instantly and conversationally

That’s exactly what my latest project, **“Multi-Agent System,”** does.

---

### ⚙️ **What’s Happening Behind the Scenes**

This workflow combines:

* 💬 **Chat Trigger** — listens to your messages in real time
* 🧠 **LangChain AI Agent** — decides which tool to use (Sheets or Calendar)
* 🤖 **Google Gemini** — the intelligent model that understands and responds naturally
* 🗂️ **Google Sheets Tool** — fetches contact information dynamically
* 📅 **Google Calendar Tool** — creates and manages meetings automatically
* 🧏 **Memory Buffer** — remembers the conversation context

So instead of switching tabs or typing commands, I just talk — and my AI handles it all.

---

### 💡 **Why This Is So Powerful**

This isn’t just a workflow — it’s a step toward **autonomous AI assistants** that can *think, reason, and take action*.

✅ It saves hours of manual lookup and scheduling
✅ Acts as a personal or company virtual assistant
✅ Can be expanded to include Notion, Slack, Gmail, or CRMs
✅ Built visually — **no manual coding needed!**

---

### 🧠 **Big Picture**

This project made me realize how close we are to the future where **AI agents collaborate across tools** — handling all your repetitive digital tasks while you focus on creativity and strategy.

Built with:

> 🔹 n8n (Self-Hosted)
> 🔹 LangChain
> 🔹 Google Gemini
> 🔹 Google Sheets + Calendar

---

✨ Next goal: add Gmail + Notion integration so my agent can **read context, schedule meetings, and send follow-ups automatically**.

---


#n8n #LangChain #Gemini #Automation #ArtificialIntelligence #AIAgent #NoCode #WorkflowAutomation #GoogleWorkspace #AIIntegration #TechInnovation

---
