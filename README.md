# SmartDocs AI  
Multi-Agent Business Document Understanding and Workflow Automation

## Overview
SmartDocs AI is a multi-agent document-processing system built using Google’s Gemini models and the Agent Development Kit (ADK). It automates the understanding of business documents such as invoices, purchase orders, contracts, and resumes. The system performs document classification, structured data extraction, summarization, action recommendation, and storage for long-term retrieval.

This project was developed as part of the Google x Kaggle AI Agents Intensive 2025.

## Problem Statement
Organizations process large volumes of unstructured business documents. These documents must be read manually, interpreted, summarized, and entered into internal systems. This manual workflow leads to:

- Time-consuming processing  
- Human errors in data extraction  
- Inconsistent decisions  
- Lack of centralized structured records  
- High cost due to repetitive manual effort  

SmartDocs AI solves this by using LLM-powered agents to convert raw text into structured information and recommend actions automatically.

## Why Agents
The tasks involved in document understanding are naturally decomposable into specialized roles. A multi-agent architecture aligns with these roles:

- A classification agent determines the document type.  
- An extraction agent pulls structured information.  
- A summarization agent builds a concise description.  
- A decision agent recommends the next business action.  
- A persistence tool stores the output in long-term memory (SQLite).

Agents provide modularity, interpretability, scalability, and clean role separation, making them ideal for this workflow.

## System Architecture
1. **Type Classification Agent**  
   Identifies whether a document is an invoice, purchase order, contract, resume, or other.

2. **Extraction Agent**  
   Extracts structured fields as a JSON object based on the identified document type.

3. **Summary Agent**  
   Generates a short business summary.

4. **Decision Agent**  
   Suggests one recommended action such as “approve,” “escalate_to_finance,” or “request_more_info.”

5. **Custom Database Tool**  
   Stores the processed document in SQLite as long-term memory.

User Input → Classification → Extraction → Summary → Decision → Database Storage

## Demo
Below is an example of the pipeline output from a sample invoice:

**Input:**  
Text-based invoice containing vendor details, total amount, currency, and line items.

**Output:**  
- `doc_type: invoice`  
- Extracted structured fields (JSON)  
- Automated 3–5 sentence summary  
- Suggested action: `approve`  
- Saved as `doc_id: 1` in the database

## The Build
Technologies and components used:

- Gemini 2.5 (Flash/Pro) models  
- Google ADK (Python)  
- Sequential multi-agent architecture  
- Custom Python tools integrated with ADK  
- SQLite for long-term memory  
- Context engineering for consistent JSON responses  
- Evaluation framework for type-classification accuracy

### Key ADK Concepts Implemented
- Multi-agent pipeline  
- Custom tool usage  
- Persistent long-term memory  
- Context compaction strategies  
- Logging and error handling  
- Agent evaluation harness  

## Evaluation
The evaluation suite runs multiple example documents and checks:

- Type classification accuracy  
- Presence of required extracted fields  
- Agent behavior consistency  

Example result:Overall type classification accuracy: 1.00

## If I Had More Time
- Add OCR and PDF parsing for real-world scanned documents  
- Add parallel agents for faster performance  
- Implement loop-based agents for repairing incorrect JSON  
- Build a Streamlit/Gradio UI for uploads and visualization  
- Add observability dashboards (metrics, token usage, latency)  
- Deploy as a Cloud Run API endpoint  
- Add vendor profiling and analytics features  

## License
This project is released for educational and research use.


