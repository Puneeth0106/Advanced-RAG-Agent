**Advanced RAG Workflow**
- **Purpose:** A LangGraph-powered RAG agent that reformulates questions, validates topic relevance, retrieves from a small Chroma vector store, filters document relevance, and generates contextual answers.
- **Notebook:** See [Advanced_rag_workflow.ipynb](Advanced_rag_workflow.ipynb).


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
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -e .
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



