SmartDocs AI
Multi-Agent Business Document Understanding & Workflow Automation

Overview

SmartDocs AI is an enterprise-grade multi-agent system built using Google’s Gemini models and ADK to intelligently process business documents such as:

Invoices

Purchase Orders

Contracts

Resumes

Internal business documents

It transforms messy, unstructured textual documents into:

Structured, clean JSON

Human-readable summaries

Intelligent next-step suggestions

Persisted records stored in a local database

The project was built as part of the Google x Kaggle – AI Agents Intensive (2025).

Problem Statement

Organizations handle thousands of unstructured business documents daily—typically in PDF or text form. Employees must manually open each document, read it, extract relevant information, summarize it, and decide what to do next.

This leads to huge problems:

Time-consuming workflows: Manual entry takes hours every week.

Inconsistent decisions: Different employees interpret documents differently.

Error-prone extraction: Important data (amounts, dates, names) can be missed.

Lack of structured storage: No centralized, searchable repository.

No automated recommendations: Teams must manually choose actions.

This creates operational bottlenecks, compliance risks, and high labor costs.

SmartDocs AI solves this by converting raw documents into structured data and automating business decisions using a pipeline of intelligent agents.

 Why Agents?

Agents are the perfect solution because document understanding naturally breaks down into specialized cognitive tasks, just like a team of employees:

✔ Classification Agent determines what type of document it is.
✔ Extraction Agent pulls structured fields from the text.
✔ Summary Agent writes a concise human-understandable summary.
✔ Decision Agent suggests the next business step.

Agents allow:

🔹 Modular intelligence (one agent per skill)

🔹 Sequential or parallel workflows

🔹 Tool usage (database save tool)

🔹 Context engineering

🔹 Long-term memory via persistence

🔹 Improved explainability

🔹 Composable growth (e.g., add OCR agent, legal review agent later)

This mirrors real business operations—except faster, more accurate, and scalable.

 System Architecture
                   SmartDocs AI Agent Pipeline
────────────────────────────────────────────────────────────

User Input (Text / OCR Output)
            │
            ▼
┌──────────────────────────┐
│ 1. Type Classification    │  ← "What kind of document is this?"
│    (LLM Agent)            │
└───────────────┬──────────┘
                │ doc_type
                ▼
┌──────────────────────────┐
│ 2. Extraction Agent      │  ← Extract key fields (JSON)
└───────────────┬──────────┘
                │ fields_json
                ▼
┌──────────────────────────┐
│ 3. Summary Agent         │  ← Human-readable summary
└───────────────┬──────────┘
                │ summary
                ▼
┌──────────────────────────┐
│ 4. Decision Agent        │  ← approve / escalate / request info
└───────────────┬──────────┘
                │ suggested_action
                ▼
┌──────────────────────────┐
│ Custom Tool: save_document_record()  
│ Stores record in SQLite DB  
└──────────────────────────┘
                │ doc_id
                ▼
         smartdocs.db (Long-term memory)

 Features
✔ Multi-Agent Architecture

4 agents working sequentially.

✔ Custom Tool Integration

Database write tool stores extracted documents.

✔ Context Engineering

Prompts enforce strict JSON formatting + clean output.

✔ Persistent Memory

Documents stored in SQLite (smartdocs.db).

✔ ADK Concepts

Multi-agent pipeline

Tool usage

Memory + persistence

Context compaction methods

Evaluation harness

✔ Evaluation Framework

Automatic accuracy + extraction testing.

Demo Output (Example)
Input (Invoice):
INVOICE
Vendor: ACME Pvt Ltd
Customer: CMB Solutions
Invoice Date: 2025-10-01
...

Output:
Doc Type: invoice
Suggested Action: approve
Summary: This document is an invoice...

Extracted Fields:
{
  "vendor": "ACME Pvt Ltd",
  "customer": "CMB Solutions",
  "invoice_date": "2025-10-01",
  "due_date": "2025-10-15",
  "currency": "INR",
  "total_amount": 45000
}

Stored:
doc_id: 1  → saved inside smartdocs.db
 Evaluation Results

Using the built-in evaluation harness:

evaluate_smartdocs(test_docs)


Example:

Overall type classification accuracy: 1.00


The harness also prints extracted fields and suggested actions for comparison.

Project Structure
SmartDocs/
│
├── smartdocs_agent.ipynb    # Main notebook
├── smartdocs.db             # SQLite persistent memory
├── README.md                # This file
├── A_2D_digital_graphic_*.png  # Thumbnails & banners
└── utils/
    ├── call_gemini.py
    ├── safe_json_parse.py
    ├── process_document.py
    └── save_document_record.py

Tech Stack

Gemini 2.5 Flash / Pro

Google ADK (Python)

SQLite (local persistent memory)

Python 3.10+

Kaggle Notebook Runtime

🛠️ How It Works (Core Components)
1. call_gemini(prompt)

Unified method to call Gemini → returns clean text.

2. safe_json_loads

Extracts JSON from LLM responses robustly.

3. process_document(raw_text)

Main orchestrator performing:

classify → extract → summarize → decide → store

4. save_document_record()

Custom tool writing:

doc_type

summary

fields JSON

action

to SQLite.

5. evaluate_smartdocs()

Runs multiple test examples and prints:

predicted vs expected

extracted field keys

accuracy

🔮 If I Had More Time (Future Improvements)
1️⃣ OCR + PDF Upload Support

Integrate OCR (Google Vision, Tesseract) to process real scanned docs.

2️⃣ Parallel Agents

Run extraction & summary agents simultaneously via asyncio.

3️⃣ Loop Agent for Missing Fields

If extraction is incomplete → retry with clarifying prompts.

4️⃣ Observability Dashboard

Monitor latency, token usage, agent performance.

5️⃣ Cloud Deployment

Expose API using Cloud Run + ADK Agent Engine.

6️⃣ Vendor Intelligence Layer

Track vendors, risk, frequency, and previous decisions.

7️⃣ UI (Streamlit / Gradio)

Interactive upload + viewing panel for SmartDocs.

🎨 Thumbnails & Images

Use these three images for Kaggle Card & Submission:

A_2D_digital_graphic_design_displays_promotional_c.png

A_2D_digital_graphic_design_image_showcases_a_prom.png

A_2D_digital_graphic_design_features_promotional_c.png

📄 License

This project is open for educational and research use.
