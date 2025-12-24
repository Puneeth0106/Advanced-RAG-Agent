**Introduction**
- Classic RAG is great for direct questions but falters in multi-turn chats. Follow-ups like “What about pricing?” often miss because there’s no memory or smart query handling.
- This agent solves that with:
	- **Query Reformulation:** Turns follow-ups into clear, standalone questions
	- **Topic Detection:** Keeps conversations within the defined domain
	- **Document Vetting:** Checks content quality before answering
	- **Adaptive Search:** Improves queries when results are weak
	- **Conversation Memory:** Preserves context across turns
- The example scenario is a Technology Support Knowledge Base.

**System Architecture**
![Workflow](images/workflow.png)
- The workflow is a staged pipeline:
	- **Query Enhancer:** Reformulates using conversation history
	- **Topic Validator:** Confirms the question is in-domain
	- **Content Retriever:** Pulls relevant documents
	- **Relevance Assessor:** Rates document usefulness
	- **Response Generator:** Produces contextual answers
	- **Query Optimizer:** Refines searches with capped retries
- Result: a resilient multi-turn RAG that maintains quality and relevance.

**Notebook & Purpose**
- **Notebook:** See [Advanced_rag_workflow.ipynb](Advanced_rag_workflow.ipynb).
- **Purpose:** A LangGraph-powered RAG agent that reformulates questions, validates topic relevance, retrieves from a Chroma vector store, filters document relevance, and generates contextual answers.

**Features**
- **Query Reformulation:** Builds context-aware, standalone queries from conversation history.
- **Topic Classification:** Routes off-topic questions to a friendly handoff.
- **Vector Retrieval:** Uses `sentence-transformers/all-MiniLM-L6-v2` + Chroma for similarity search.
- **Relevance Filtering:** Structured assessment to keep only useful docs.
- **Response Generation:** Contextual answers with conversation memory via LangGraph checkpoints.

**Requirements**
- **Python:** 3.11+
- **Dependencies:** Managed via [pyproject.toml](pyproject.toml)
	- langchain, langgraph, chromadb, sentence-transformers, langchain-openai, langchain-google-genai, langchain-huggingface, python-dotenv, jupyterlab, ipykernel

**Setup**
- Create and activate a virtual environment.
```bash
uv init .
uv add -r requirements.txt
```
- Optional: launch JupyterLab to run the notebook.
```bash
jupyter lab
```

**Environment Variables**
- Create a `.env` file in the project root with any keys you plan to use:
	- For Google Gemini: `GOOGLE_API_KEY`
	- For OpenAI: `OPENAI_API_KEY`
	- Optional model wiring (see next section): `LLM_PROVIDER`, `LLM_MODEL`, `LLM_TEMPERATURE`

Example `.env`:
```bash
# Provider can be google or openai
LLM_PROVIDER=openai
LLM_MODEL=gpt-5.1-codex-max
LLM_TEMPERATURE=0.1
OPENAI_API_KEY=sk-...yourkey...
# If using Google
# GOOGLE_API_KEY=AIza...yourkey...
```