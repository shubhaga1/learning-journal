# 02 — Vector DB + Pinecone

## What you learn here
- What are vectors / embeddings
- Why vector DBs exist
- Pinecone — upsert, query, index
- sentence-transformers — free local embedding model
- LangChain — why it simplifies vector DB code
- Semantic search — find by meaning, not exact words

## Prerequisites
```bash
pip install pinecone sentence-transformers langchain langchain-pinecone langchain-huggingface
```

## Run order
```bash
python 01_pinecone_basics.py          # understand upsert + query
python 02_movie_search.py             # real use case — search movies by plot
python 03_movie_search_langchain.py   # same app, less code with LangChain
```

## Key concepts

### What is a vector?
```
Text: "I love space movies"
      ↓ embedding model
Vector: [0.12, 0.45, 0.89, 0.23, ...]  ← 384 numbers representing meaning
```

### Why vector DB?
```
Normal DB:  WHERE title = "Inception"     → exact match only
Vector DB:  "find movies about dreams"    → finds by meaning
```

### Without LangChain vs With LangChain
```python
# Without — manual steps
embedding = model.encode(text).tolist()
index.upsert([{"id": "1", "values": embedding, "metadata": {...}}])

# With LangChain — one line
vectorstore = PineconeVectorStore.from_documents(docs, embeddings, index_name=index_name)
```

### Embedding model comparison
| Model | Dimensions | Cost |
|-------|-----------|------|
| all-MiniLM-L6-v2 | 384 | Free |
| all-mpnet-base-v2 | 768 | Free |
| OpenAI text-embedding-3-small | 1536 | Paid |

### How Pinecone stores data internally
- Uses **HNSW** (Hierarchical Navigable Small World) graph
- Layered structure — starts at top (fewer nodes) → narrows down
- Similar to B+ Tree concept but for vectors instead of sorted values
