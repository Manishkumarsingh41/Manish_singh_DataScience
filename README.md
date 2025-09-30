# RAG-based AI Assistant

This project implements a **Retrieval-Augmented Generation (RAG)** system for querying technical PDFs, including SOPs, manuals, and troubleshooting guides, in natural language.  
It retrieves relevant chunks from documents and generates reliable, cited answers using free/open Hugging Face models.

---

## ⚙️ Setup Instructions

### 1. Clone the Project
```bash
git clone https://github.com/Manishkumarsingh41/Manish_singh_DataScience.git
cd Manish_singh_DataScience

2. Install Dependencies
bash
Copy code
pip install PyPDF2 sentence-transformers faiss-cpu transformers
📥 Download Free/Open Models
1. Embedding Model (for retrieval)

Model: sentence-transformers/all-MiniLM-L6-v2

python
Copy code
from sentence_transformers import SentenceTransformer
embed_model = SentenceTransformer("sentence-transformers/all-MiniLM-L6-v2")
2. Generative Model (for answering queries)

Model: google/flan-t5-small

python
Copy code
from transformers import pipeline
qa_pipeline = pipeline("text2text-generation", model="google/flan-t5-small")
🚀 Run Prototype
Step 1: Prepare Documents
Place your PDFs inside the docs/ folder:

bash
Copy code
/docs/
    ├── SOP_Cyclone.pdf
    ├── Manual1.pdf
    └── ...
Step 2: Run Prototype Script
bash
Copy code
python rag_prototype.py
Step 3: Ask Questions
Example in Python:

python
Copy code
from rag_prototype import query_rag

question = "What does a sudden draft drop indicate?"
answer = query_rag(question)
print(answer)
Expected Output:

css
Copy code
A sudden draft drop indicates that the cyclone is overflowing. [Source: SOP_Cyclone.pdf]
📊 Features
Document ingestion & preprocessing

Chunking and vector indexing using FAISS

Dense retrieval using embeddings

Context-aware answer generation with citations

Local-only, free/open-source

👨‍💻 Author
Manish Kumar Singh

✨ Free to use, modify, and extend for your own dataset!

vbnet
Copy code

This version:  
- Uses proper Markdown headings and code blocks.  
- Cleanly separates setup, models, prototype instructions, and features.  
- Looks professional on GitHub.  

Do you want me to also **add a small “Evaluation & Metrics” section** for precision/recall to make it even more complete?






