# 🤖 LangChain Multi-Tool Agent with LLM Integration

This project showcases a **LangChain-powered multi-agent system** that integrates several real-world tools with an LLM backend to perform Retrieval-Augmented Generation (RAG), arithmetic, factual answering, and live web lookups.

> ✅ **Supports hybrid context-based answers using web pages, Wikipedia, Arxiv, vector databases, calculators, and web search.**

> 💡 **Based on your query, the agent uses an LLM to internally decide which tool is most appropriate and automatically invokes it to get the result.**

---

## 🚀 What This Project Does

### ✅ Loads and processes content from:

- 🧾 **Wikipedia**: via `WikipediaAPIWrapper` & `WikipediaQueryRun`
- 📄 **Web documents**: using `WebBaseLoader` with `BeautifulSoup` for parsing
- 🧠 **Arxiv papers**: via `ArxivAPIWrapper` & `ArxivQueryRun`
- 🧮 **Math expressions**: evaluated securely with Python's `eval` sandbox
- 🌐 **Live internet search**: via `DuckDuckGoSearchRun` integration

---

## 🛠 Tools Constructed

### 📚 Multi-source Tooling:

- 🔍 `WikipediaQueryRun`: Pulls factual data from Wikipedia  
- 📑 `ArxivQueryRun`: Retrieves scientific papers from Arxiv  
- 🌐 `WebBaseLoader`: Scrapes and splits HTML pages into vector chunks  
- 🧠 `FAISS` + `HuggingFaceEmbeddings`: Stores and retrieves vectorized docs  
- 🧮 `Calculator Tool`: Handles math evaluations like `"12/(2+1)"`  
- 🔎 `DuckDuckGoSearch`: Queries the internet in real-time  

---

## 🧩 Agent Creation Workflow

1. **Text Extraction** from HTML via `BeautifulSoup`  
2. **Chunking** using `RecursiveCharacterTextSplitter` (chunk size: 1000, overlap: 200)  
3. **Embedding** using `sentence-transformers/all-MiniLM-L6-v2`  
4. **Indexing** into `FAISS` vector store  
5. **Retriever Tool** created via `create_retriever_tool`  
6. **Tools Combined** into a list: `wikipedia`, `AI_tool`, `arxiv`, `calculator_tool`, `web_search`  
7. **LLM Setup** using `ChatGroq` with the `qwen-qwq-32b` model  
8. **Prompt Injection** via `ChatPromptTemplate`  
9. **Agent Bucket** formed using `create_openai_tools_agent`  
10. **Execution** managed with `AgentExecutor`  

---

## 💬 Sample Query in Action

```python
result = agent_executor.invoke({
    "input": "Who is Aishwarya Rai Bachchan",
    "context": ""
})
print(result["output"])
