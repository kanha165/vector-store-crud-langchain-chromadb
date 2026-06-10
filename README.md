# Vector Store CRUD Operations using LangChain and ChromaDB

## Overview

This project demonstrates how to perform CRUD (Create, Read, Update, Delete) operations on a Vector Database using LangChain, ChromaDB, and HuggingFace Embeddings.

The project converts text into vector embeddings and stores them in a Chroma Vector Store. Users can insert, retrieve, update, delete, and perform semantic similarity searches on stored documents.

---

## Features

* Convert text into vector embeddings
* Store embeddings in ChromaDB
* Create new documents
* Read existing documents
* Update stored documents
* Delete documents
* Perform semantic similarity search
* Visualize embeddings
* Local vector database (No API key required)

---

## Project Architecture

Text Data

↓

Embedding Model (all-MiniLM-L6-v2)

↓

Vector Embeddings

↓

ChromaDB Vector Store

↓

CRUD Operations

↓

Similarity Search

---

## Technologies Used

* Python
* LangChain
* ChromaDB
* Sentence Transformers
* HuggingFace Embeddings
* Jupyter Notebook
* Matplotlib
* Scikit-Learn

---

## Installation

### Clone Repository

```bash
git clone https://github.com/yourusername/vector-store-crud-langchain-chromadb.git

cd vector-store-crud-langchain-chromadb
```

### Install Dependencies

```bash
pip install langchain-community
pip install chromadb
pip install sentence-transformers
pip install scikit-learn
pip install matplotlib
```

---

## Import Libraries

```python
from langchain_community.embeddings import HuggingFaceEmbeddings
from langchain_community.vectorstores import Chroma
from langchain_core.documents import Document
```

---

## Load Embedding Model

```python
embeddings = HuggingFaceEmbeddings(
    model_name="sentence-transformers/all-MiniLM-L6-v2"
)
```

---

## Generate Embeddings

```python
text = "Artificial Intelligence is changing the world"

vector = embeddings.embed_query(text)

print(len(vector))
```

Output:

```text
384
```

---

## Create Documents

```python
docs = [
    Document(
        page_content="Virat Kohli is a legendary batsman",
        metadata={"role":"batsman"}
    ),

    Document(
        page_content="MS Dhoni is Captain Cool",
        metadata={"role":"captain"}
    ),

    Document(
        page_content="Jasprit Bumrah is a fast bowler",
        metadata={"role":"bowler"}
    )
]
```

---

## Create Vector Store

```python
vector_store = Chroma(
    collection_name="cricket_players",
    embedding_function=embeddings,
    persist_directory="./chroma_db"
)
```

---

## CRUD Operations

### Create

```python
ids = vector_store.add_documents(docs)
```

### Read

```python
all_docs = vector_store.get()
```

### Update

```python
updated_doc = Document(
    page_content="Jasprit Bumrah is the best death over specialist bowler",
    metadata={"role":"bowler"}
)

vector_store.update_document(
    document_id=ids[2],
    document=updated_doc
)
```

### Delete

```python
vector_store.delete(ids=[ids[1]])
```

---

## Similarity Search

```python
results = vector_store.similarity_search(
    "Who is a bowler?",
    k=2
)

for doc in results:
    print(doc.page_content)
```

---

## Embedding Visualization

### Plot First 50 Dimensions

```python
import matplotlib.pyplot as plt

plt.plot(vector[:50])
plt.show()
```

### PCA Visualization

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
points = pca.fit_transform(vectors)
```

This visualization helps understand semantic relationships between documents.

---

## Example Use Cases

* Retrieval-Augmented Generation (RAG)
* Semantic Search Systems
* Document Search Engines
* Chatbots
* Knowledge Bases
* Recommendation Systems

---

## Project Structure

```text
vector-store-crud-langchain-chromadb/
│
├── notebook.ipynb
├── README.md
├── requirements.txt
├── chroma_db/
└── screenshots/
```

---

## Learning Outcomes

After completing this project, you will understand:

* What embeddings are
* How vector databases work
* How semantic search works
* LangChain integration with ChromaDB
* CRUD operations in vector databases
* Embedding visualization techniques

---

## Future Improvements

* PDF Ingestion
* Chunking
* RAG Pipeline
* FAISS Integration
* Pinecone Integration
* OpenAI Embeddings Support
* Streamlit Web Application

---

## Author

Kanha Patidar

B.Tech CSIT | AI & GenAI Enthusiast

---

## License

This project is available under the MIT License.
