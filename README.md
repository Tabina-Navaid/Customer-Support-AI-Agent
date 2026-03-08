# 🤖 AI-Powered Customer Support Agent — n8n + OpenAI + Pinecone

A fully autonomous customer support agent built in **n8n** that handles incoming customer emails end-to-end. The agent reads emails from Gmail, understands the query using OpenAI's GPT model, searches a Pinecone vector store for relevant knowledge base answers, maintains conversation memory, and either responds automatically or drafts a reply for human review — all without manual involvement.

---

## 🧩 Problem Statement

Businesses receiving high volumes of repetitive support emails face a constant trade-off:

- Manually reading and replying to every query is **time-consuming**
- Delayed responses lead to **poor customer experience**
- Repetitive queries **pull staff away from higher-value work**
- No system existed to **intelligently triage** what needed human attention vs. what could be resolved automatically

---

## 🏗️ Workflow Architecture

```
Gmail Trigger (new email arrives)
        ↓
AI Agent — OpenAI GPT Chat Model
    ├── Simple Memory (conversation context)
    └── Pinecone Vector Store (knowledge retrieval via OpenAI Embeddings)
        ↓
Data Structuring (format AI output)
        ↓
Auto Respond? (Condition)
    ├── If YES → Send email directly via Gmail
    └── If NO  → Create Gmail draft for human review
                        ↓
                  If (edge case handler)
                    ├── true  → Send alternative message
                    └── false → No Operation (do nothing)
```

---

## 📸 Workflow Screenshot

### Full Workflow — n8n Canvas
> Complete view of the agent workflow showing the Gmail trigger, AI Agent with memory and vector store tools, data structuring, auto-respond condition, draft creation, and edge case handling.


<img width="1917" height="1079" alt="Screenshot 2026-03-07 013836" src="https://github.com/user-attachments/assets/7c29993c-37b8-4020-bcda-10f54c57bc54" />

---

## 🔄 Flow Logic — Step by Step

**Step 1 — Gmail Trigger**
- Monitors the inbox continuously
- Fires the workflow the moment a new customer email arrives
- No polling delay — near real-time activation

**Step 2 — AI Agent (OpenAI GPT)**
- Receives the raw email and interprets the customer's intent
- Powered by **OpenAI GPT Chat Model**
- Has access to two tools:
  - **Simple Memory** — retains context across the conversation thread for multi-turn coherence
  - **Pinecone Vector Store** — searched via **OpenAI Embeddings** to retrieve semantically relevant answers from the business knowledge base

**Step 3 — Data Structuring**
- Formats the AI agent's output into a clean, structured response ready for delivery

**Step 4 — Auto Respond? Condition**
- Evaluates whether the query is straightforward enough for an automatic reply
- **If Yes** → response is sent directly via Gmail with no human involvement
- **If No** → a Gmail draft is created for a human agent to review and edit before sending

**Step 5 — Edge Case Handler**
- A second `If` condition downstream handles unexpected or ambiguous outputs
- Routes to either an alternative message or a **No Operation** node
- Ensures the workflow never breaks regardless of input type

---

## 📈 Business Outcomes

- **Fully autonomous first-line support** — common queries handled within seconds, 24/7
- **Human-in-the-loop draft pathway** — nuanced or sensitive emails are never sent without oversight
- **Knowledge-grounded responses** — Pinecone retrieval ensures answers are based on actual business information, not generic AI output
- **Reduced support workload** — repetitive queries no longer require staff attention
- **Average reply time** cut from hours to under a minute

---

## 🧰 Stack & Tools

| Component | Technology |
|-----------|-----------|
| **Workflow Automation** | n8n |
| **Email Trigger & Sending** | Gmail (via n8n connector) |
| **AI Agent** | OpenAI GPT Chat Model |
| **Vector Knowledge Base** | Pinecone Vector Store |
| **Embeddings** | OpenAI Embeddings |
| **Conversation Memory** | n8n Simple Memory module |
| **Logic & Routing** | Condition nodes + No Operation node |

---

