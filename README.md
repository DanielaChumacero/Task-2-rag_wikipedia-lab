# Task-2-rag_wikipedia-lab
# 📚 Task 2: Wikipedia-based RAG Summarizer

## 🎯 Overview

A Retrieval-Augmented Generation (RAG) system that extracts information from Wikipedia articles, creates semantic embeddings, stores them in a vector database, and enables intelligent querying about AI and healthcare topics.

**Framework**: LangChain + ChromaDB + SentenceTransformers  
**Data Source**: Wikipedia API  
**Embeddings**: all-MiniLM-L6-v2  
**No API Keys Required**: Runs completely locally in Google Colab

---

## 🏗️ System Architecture

```
Wikipedia Articles
      ↓
Text Extraction & Chunking (~300 words)
      ↓
Semantic Embeddings (SentenceTransformers)
      ↓
Vector Storage (ChromaDB)
      ↓
Query Interface → Similarity Search
      ↓
Retrieved Context → Summary Generation
```

---

## 📋 Features

- ✅ Fetches content from 4 Wikipedia articles on AI/Healthcare
- ✅ Chunks text into ~300-word segments for optimal retrieval
- ✅ Creates 384-dimensional semantic embeddings
- ✅ Stores in ChromaDB vector database with metadata
- ✅ Semantic similarity search (top-k retrieval)
- ✅ Generates coherent summaries from retrieved chunks
- ✅ Saves all outputs as CSV, JSON, and Markdown

---

## 🚀 Quick Start

### Prerequisites
- Google Colab account (free)
- No API keys required

### Installation (Cell 1)
```python
!pip install -q wikipedia-api sentence-transformers chromadb langchain pandas
```

### Run All Cells
Simply execute cells 1-14 in sequence. The notebook will:
1. Fetch Wikipedia data
2. Create embeddings
3. Build vector store
4. Run test queries
5. Generate final summary
6. Download all deliverables

---

## 📊 Wikipedia Topics Covered

| Topic | Description |
|-------|-------------|
| **Federated Learning** | Distributed machine learning for privacy preservation |
| **AI in Healthcare** | Medical applications of artificial intelligence |
| **Synthetic Data** | Artificially generated data for AI training |
| **Machine Learning** | Core ML concepts and techniques |

---

## 🔧 Technical Components

### 1. Data Collection (Cell 4)
- Fetches Wikipedia articles using `wikipedia-api`
- Extracts full text content
- Chunks into ~300-word segments
- Saves to `wiki_corpus.csv`

### 2. Embedding Generation (Cell 5)
```python
model = SentenceTransformer("all-MiniLM-L6-v2")
embeddings = model.encode(texts)
```
- Model: all-MiniLM-L6-v2 (384 dimensions)
- Fast and accurate semantic embeddings
- Enables similarity-based retrieval

### 3. Vector Database (Cell 6)
```python
vectorstore = Chroma.from_texts(
    texts=texts,
    embedding=embeddings,
    metadatas=metadatas
)
```
- Database: ChromaDB (in-memory)
- Efficient similarity search
- Metadata preserved for source attribution

### 4. Query Pipeline (Cell 7-8)
- LangChain RetrievalQA chain
- Retrieves top 5 relevant chunks
- Combines context for comprehensive answers
- Returns sources with attribution

---

## 📁 Deliverables

| File | Description | Format |
|------|-------------|--------|
| `wiki_corpus.csv` | Chunked Wikipedia data with metadata | CSV |
| `rag_summary.md` | Final 400-500 word research summary | Markdown |
| `retrieval_examples.json` | Sample queries with results | JSON |

---

## 🔍 Sample Queries

The system can answer questions like:

```python
# Query 1
"What are the main challenges of federated learning in healthcare?"

# Query 2  
"How does synthetic data help in medical AI applications?"

# Query 3
"What are privacy concerns with federated learning?"

# Query 4
"Explain the benefits of federated learning"
```

---

## 📈 Performance Metrics

| Metric | Value |
|--------|-------|
| **Total Documents** | ~100-150 chunks |
| **Embedding Dimension** | 384 |
| **Retrieval Speed** | < 1 second |
| **Top-K Results** | 5 chunks per query |
| **Average Query Time** | 2-3 seconds |

---

## 🎓 How It Works

### Step 1: Wikipedia Extraction
```python
wiki = wikipediaapi.Wikipedia('en')
page = wiki.page("Federated_learning")
text = page.text
```

### Step 2: Text Chunking
- Splits articles into ~300 word segments
- Maintains context and readability
- Each chunk stored with metadata (title, URL, ID)

### Step 3: Semantic Embedding
- Converts text to 384-dimensional vectors
- Captures semantic meaning (not just keywords)
- Similar concepts cluster together in vector space

### Step 4: Vector Storage
- ChromaDB stores embeddings efficiently
- Enables fast similarity search
- Preserves metadata for source attribution

### Step 5: Query Processing
1. User asks a question
2. Question is embedded using same model
3. Vector similarity search finds top-K relevant chunks
4. Chunks are combined into context
5. Summary is generated from retrieved content

---

## 💡 Key Advantages

### Retrieval-Augmented Generation
- ✅ **Factual Accuracy**: Answers grounded in Wikipedia sources
- ✅ **Source Attribution**: Every answer includes citations
- ✅ **No Hallucination**: Only uses retrieved information
- ✅ **Transparent**: Can inspect retrieved chunks

### vs. Traditional Search
- 🔍 **Semantic**: Finds conceptually similar content, not just keywords
- 🎯 **Context-Aware**: Understands meaning, not just word matching
- 📚 **Comprehensive**: Combines multiple sources automatically

---

## 🔬 Use Cases

1. **Research Assistant**: Quick summaries of technical topics
2. **Educational Tool**: Learning about AI and healthcare
3. **Knowledge Base**: Query structured information efficiently
4. **Fact-Checking**: Verify claims against Wikipedia sources

---

## 🛠️ Customization Options

### Change Topics
```python
TOPICS = [
    "Your_Topic_1",
    "Your_Topic_2",
    "Your_Topic_3"
]
```

### Adjust Chunk Size
```python
chunk_size = 300  # Change to 200, 400, etc.
```

### Modify Retrieval Count
```python
retriever=vectorstore.as_retriever(
    search_kwargs={"k": 10}  # Retrieve top 10 instead of 5
)
```

### Use Different Embedding Model
```python
model = SentenceTransformer("all-mpnet-base-v2")  # Larger, more accurate
```

---

## 📊 Evaluation Criteria

| Category | Points | Description |
|----------|--------|-------------|
| **Wikipedia Data** | 4 pts | Correct extraction and chunking |
| **Embedding + Storage** | 6 pts | SentenceTransformers + ChromaDB |
| **LangChain Pipeline** | 6 pts | Functional retrieval and generation |
| **Final Summary** | 4 pts | Coherence, accuracy, completeness |
| **Total** | **20 pts** | Full task completion |

---

## 🐛 Troubleshooting

### Issue: Wikipedia fetch fails
**Solution**: Check internet connection, try different topics

### Issue: Out of memory
**Solution**: Reduce chunk size or number of topics

### Issue: Slow embeddings
**Solution**: Normal for CPU - GPU would be faster but not required

### Issue: ChromaDB errors
**Solution**: Restart runtime and run all cells fresh

---

## 📚 Technologies Used

| Technology | Version | Purpose |
|------------|---------|---------|
| **Python** | 3.10+ | Programming language |
| **wikipedia-api** | Latest | Wikipedia content extraction |
| **sentence-transformers** | Latest | Semantic embeddings |
| **ChromaDB** | Latest | Vector database |
| **LangChain** | Latest | RAG pipeline orchestration |
| **Pandas** | Latest | Data manipulation |

---

## 🎯 Learning Outcomes

After completing this task, you will understand:

- ✅ How RAG systems work
- ✅ Semantic search vs keyword search
- ✅ Vector embeddings and similarity
- ✅ Building knowledge bases from unstructured text
- ✅ LangChain retrieval patterns
- ✅ ChromaDB vector database operations

---

## 📖 Additional Resources

- [LangChain Documentation](https://python.langchain.com/docs/get_started/introduction)
- [ChromaDB Guide](https://docs.trychroma.com/)
- [SentenceTransformers](https://www.sbert.net/)
- [Wikipedia API Docs](https://wikipedia-api.readthedocs.io/)

---

## 🎓 Next Steps

1. ✅ Complete Task 1 (Multi-Agent Research)
2. ✅ Complete Task 2 (This RAG system)
3. 📝 Write comparison reflection (Bonus +3 pts)
4. 📤 Submit both repositories

---

## 📞 Support

If you encounter issues:
1. Check the troubleshooting section
2. Verify all cells ran in sequence
3. Restart runtime and try again
4. Review error messages carefully

---

## ✨ Success Criteria

Your Task 2 is complete when:
- ✅ All cells execute without errors
- ✅ `wiki_corpus.csv` contains 100+ chunks
- ✅ `rag_summary.md` has 400-500 words
- ✅ `retrieval_examples.json` has query results
- ✅ All files download successfully

