# 🧩 Workflow Overview: mcp_tool + c_mcp

These two workflows together create a client-server AI tool system using MCP (Model Context Protocol) inside n8n.

You’ve basically built your own AI Tool Server + Chat Agent Client setup — the foundation of an Agentic System that connects an AI model to external APIs or data sources dynamically.


---

## ⚙️ PART 1 — mcp_tool (The Server)

This workflow acts as your Tool Server in the MCP ecosystem.
It waits for tool calls and responds with real data.

🧠 Step-by-Step Breakdown

### 1️⃣ MCP Server Trigger

Type: @n8n/n8n-nodes-langchain.mcpTrigger

Purpose: This is the entry point for the server.

It’s like a webhook that listens for requests coming from another workflow (the MCP Client).

When another workflow sends a tool call request (for example, “Fetch Hacker News articles”), this node activates automatically.


#### 🟢 Think of it like:

> The "AI Agent" knocks on the server’s door → “Hey, I need Hacker News data!”




---

### 2️⃣ Get Many Items in Hacker News

Type: n8n-nodes-base.hackerNewsTool

Purpose: Fetches top posts from Hacker News using the public API.

Parameters:

Resource: all

Limit: 20 → fetches the top 20 latest posts



So whenever your MCP Client requests data, this tool gathers the latest 20 news stories — with titles, authors, and URLs.

#### 🟢 Output Example:

[
  { "title": "AI beats humans in Go again", "url": "https://news.ycombinator.com/item?id=123" },
  { "title": "n8n adds new AI nodes", "url": "https://news.ycombinator.com/item?id=124" }
]


---

**🔗 Connection**

The “Get Many Items in Hacker News” node is connected to the MCP Server Trigger via an ai_tool link.

**That means:**

> When the server receives an MCP request, it runs this Hacker News node, collects results, and sends them back as the tool output.



**✅ Purpose:** Provides real-time news data as a service to AI agents.


---

## ⚙️ PART 2 — c_mcp (The Client)

This workflow is your AI Chat Agent Client — the one users interact with directly.

It talks to the MCP Tool Server you just made (mcp_tool) and uses its data during a conversation.


---

## 🧠 Step-by-Step Breakdown

### 1️⃣ When Chat Message Received

Type: chatTrigger

Purpose: Starts the workflow when a user sends a chat query.

#### Example Input:

> “Give me the latest Hacker News headlines.”




This message triggers the rest of the workflow.


---

### 2️⃣ AI Agent

Type: @n8n/n8n-nodes-langchain.agent

Purpose: Acts as the brain of your system.

It receives the user query, decides whether to use the MCP tool, and generates a response.

#### Key connections:

Language model → Gemini

Tool → MCP Client

Memory → Buffer window



#### 🧠 System Behavior:

If the question requires external data, the agent calls the MCP tool automatically.

If it’s a reasoning or general query, it answers directly using Gemini.



---

### 3️⃣ Google Gemini Chat Model

**Type:** @n8n/n8n-nodes-langchain.lmChatGoogleGemini

**Purpose:** This is the LLM (Large Language Model) — it handles reasoning, understanding, and text generation.

**Credentials:** Google Gemini (PaLM) API

**Function:** Helps the AI understand user queries and communicate naturally.


**🟢 Example:**

> User: “Summarize the latest Hacker News headlines.”
Gemini + MCP → Calls tool → Reads results → Writes a summary paragraph.




---

### 4️⃣ MCP Client

**Type:** @n8n/n8n-nodes-langchain.mcpClientTool

**Endpoint:**
https://shehroz98.app.n8n.cloud/mcp-test/8db93fe5-b8b9-4eb6-ba60-5976ffa08d8f

**Purpose:** Connects your AI Agent to the MCP Tool Server you created earlier.

It acts as a bridge between the chat and the external data source.


**🟢 In action:**
When the AI Agent decides it needs Hacker News data, it sends a request to this MCP endpoint → which then activates your mcp_tool workflow → gets the news → returns it to the agent.


---

### 5️⃣ Simple Memory

**Type:** memoryBufferWindow

**Purpose:** Keeps track of recent chat messages.

**Effect:** Enables multi-turn conversation.

> User: “Show me Hacker News headlines.”
AI: “Here are the top 5.”
User: “Tell me more about the second one.”
→ ✅ Agent remembers context.





---

### 🔄 Overall Flow

💬 Chat Trigger (user message)
       ↓
🧠 AI Agent (decides)
       ↓
🔍 MCP Client (requests data from MCP Server)
       ↓
📰 MCP Server Trigger (receives request)
       ↓
🧩 Hacker News Tool (fetches news)
       ↓
📨 Sends data back to AI Agent
       ↓
🧠 Gemini + Memory (summarizes + responds)
       ↓
💬 Final chat reply to user


---

### 🚀 Why This Workflow Is Powerful

**Feature	Benefit**

🌐 Real-Time Data Access	Your AI can fetch live information from Hacker News (or any API) instead of relying on static data.
🧠 Agentic Reasoning	Gemini decides when to use external tools vs. when to answer directly.
🔗 Modular Tool Server	You can add new MCP tools easily — e.g., Weather API, Google Sheets, Notion, etc.
💬 Natural Chat Interface	Users interact in plain English; the system handles logic behind the scenes.
🧩 Reusability	The same MCP Server can serve multiple agents across different workflows.
⚙️ No-Code AI Infrastructure	All built visually in n8n — no manual backend coding required.



---

## 💡 Real-World Use Cases

**1. AI Research Assistant:** Fetches latest news or research papers and summarizes them.


**2. Marketing Agent:** Pulls trending topics and drafts social posts.


**3. Developer Dashboard Bot:** Fetches GitHub or API updates for your projects.


**4. Multi-Agent Ecosystem:** Combine multiple MCP servers — e.g., one for finance data, one for weather, one for documents.




---

## 🧾 In Summary

✅ Workflow Pair: c_mcp (Client) + mcp_tool (Server)
✅ Core Tech: n8n + MCP Protocol + Google Gemini
✅ Goal: Create a chat agent that fetches live Hacker News data dynamically through an MCP connection.
✅ Result: An Agentic, data-aware assistant — a big step toward autonomous AI systems.


