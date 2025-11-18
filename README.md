# Document Assistant Project Instructions

Welcome to the Document Assistant project! This project will help you build a sophisticated document processing system using LangChain and LangGraph. You'll create an AI assistant that can answer questions, summarize documents, and perform calculations on financial and healthcare documents.

## Project Overview

This document assistant uses a multi-agent architecture with LangGraph to handle different types of user requests:
- **Q&A Agent**: Answers specific questions about document content
- **Summarization Agent**: Creates summaries and extracts key points from documents
- **Calculation Agent**: Performs mathematical operations on document data

### Prerequisites
- Python 3.9+
- OpenAI API key

### Installation

1. Clone the repository:
```bash
git clone https://github.com/RickFort/Report-Building-Agent
cd Report-Building-Agent
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Create a `.env` file:
```bash
cp .env.example .env
# Edit .env and add your OpenAI API key
```

### Running the Assistant

```bash
python main.py
```

## Project Structure
```
doc_assistant_project/
├── src/
│   ├── schemas.py        # Pydantic models
│   ├── retrieval.py      # Document retrieval
│   ├── tools.py          # Agent tools
│   ├── prompts.py        # Prompt templates
│   ├── agent.py          # LangGraph workflow
│   └── assistant.py      # Main agent
├── sessions/             # Saved conversation sessions
├── main.py               # Entry point
├── requirements.txt      # Dependencies
└── README.md             # This file
```



## Agent Architecture

The LangGraph agent follows this workflow:

![](./langgraph_agent_architecture.png)

## State Management
The AgentState tracks:

- messages: Conversation history with LangChain message types
- user_input: Current user query
- intent: Classified intent with confidence score
- next_step: Next node to execute in the workflow
- conversation_summary: Rolling summary of conversation
- active_documents: Document IDs currently being discussed
- tools_used: List of tools invoked during processing
- actions_taken: Accumulated list of executed agent nodes (uses operator.add reducer)

## Key Components
### Schemas (schemas.py)

- UserIntent: Intent classification with type, confidence, and reasoning
- AnswerResponse: Structured Q&A responses with sources and confidence
- SummarizationResponse: Summary with key points and document references
- CalculationResponse: Mathematical results with step-by-step explanations

### Tools (tools.py)
- document_search: Search documents by keyword, type, or amount
- document_reader: Read full content of specific documents
- calculator: Safely evaluate mathematical expressions
- document_statistics: Get collection statistics and financial summaries

### Agents (agent.py)

- classify_intent: Routes requests to appropriate specialized agent
- qa_agent: Answers questions using ReAct pattern with tools
- summarization_agent: Creates summaries and extracts key information
- calculation_agent: Performs calculations on document data
- update_memory: Maintains conversation context and tracks active documents

## Built With

- LangChain - Framework for building LLM applications
- LangGraph - Library for building stateful, multi-actor applications with LLMs
- OpenAI GPT-4 - Large Language Model for natural language understanding
- Pydantic - Data validation using Python type annotations
- Python-dotenv - Environment variable management

## Expected Behavior

After implementation, your assistant should be able to:
- Classify user intents correctly
- Search and retrieve relevant documents
- Answer questions with proper source citations
- Generate comprehensive summaries
- Perform calculations on document data
- Maintain conversation context across turns

## License
License

## Authors
Built as part of the Udacity <Agentic AI Engineer with LangChain and LangGraph>[https://www.udacity.com/course/agentic-ai-engineer-with-langchain-and-langgraph--nd901] Nanodegree Program .
