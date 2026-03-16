# RAG System

A **Retrieval-Augmented Generation (RAG)** system that combines document retrieval with Large Language Models (LLMs) to answer questions based on your custom documents.

## Overview

This RAG system allows you to:
- Load and process documents from multiple formats (PDF, DOCX, TXT, JSON, CSV, XLSX, MD)
- Convert documents into semantic embeddings
- Store embeddings in a vector database
- Retrieve relevant document chunks based on user queries
- Generate accurate answers using an LLM (DeepSeek) augmented with retrieved context

## How It Works

The system follows a step-by-step pipeline:

### Step 1: Document Loading (`rag_step_1_loading.py`)
- Loads documents from a folder
- Supports multiple formats: `.txt`, `.docx`, `.pdf`, `.csv`, `.json`, `.xlsx`, `.md`
- Extracts content and metadata from each document

### Step 2: Document Chunking (`rag_step_2_chunking.py`)
- Splits large documents into smaller, manageable chunks
- Default chunk size: 500 characters with 50 character overlap
- Preserves metadata (source, document ID, chunk ID) for each chunk

### Step 3: Embedding Generation (`rag_step_3_embeddings.py`)
- Converts text chunks into semantic vectors using `sentence-transformers`
- Uses the `all-MiniLM-L6-v2` model for efficient embeddings
- Captures semantic meaning for similarity search

### Step 4: Vector Database Storage (`rag_step_4_vector_db.py`)
- Stores embeddings and metadata in a vector database (Chroma)
- Enables fast similarity-based retrieval
- Maintains document structure and relationships

### Step 6: Similarity Search & Retrieval (`rag_step_6_similarity.py`)
- Finds the most relevant document chunks for a given query
- Uses vector similarity to match user questions with stored knowledge

### Step 7: Prompt Preparation (`rag_step_7_prompt.py`)
- Constructs a well-formatted prompt combining:
  - User's original question
  - Retrieved relevant context from documents
  - Instructions for the LLM

### Step 8: LLM Answer Generation (`rag_step_8_call_llm.py`)
- Sends the prepared prompt to DeepSeek LLM API
- Generates contextually accurate answers based on your documents
- Returns relevant, sourced information

### Main Orchestration (`rag_step_by_step.py`)
- Ties all steps together into a unified pipeline
- Handles end-to-end workflow from document loading to answer generation
- Manages user input and displays results
- This is the main script you run to use the RAG system

## Quick Start

### Prerequisites
- Python 3.8+
- API key for DeepSeek (get one at https://www.deepseek.com)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/Hasan-Atwi/RAG-SYSTEM.git
cd RAG-SYSTEM
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
Create a `.env` file in the root directory:
```
DEEPSEEK_API_KEY=your_api_key_here
```

### Usage

1. Place your documents in the `sample_docs/` folder
2. Run the main pipeline:
```bash
python rag_step_by_step.py
```

3. Enter your question when prompted:
```
Enter your questions / query here: whats in your mind today?
```

4. Get an AI-generated answer based on your documents!

## Project Structure

```
RAG-SYSTEM/
├── rag_step_1_loading.py       # Load documents
├── rag_step_2_chunking.py      # Split into chunks
├── rag_step_3_embeddings.py    # Generate embeddings
├── rag_step_4_vector_db.py     # Store in vector DB
├── rag_step_6_similarity.py    # Retrieve relevant chunks
├── rag_step_7_prompt.py        # Build LLM prompt
├── rag_step_8_call_llm.py      # Call LLM API
├── rag_step_by_step.py         # Main orchestration script
├── sample_docs/                # Your document folder
├── .env                        # Environment variables (create this)
└── README.md                   # This file
```

## Key Features

✅ **Multi-format Support** - Works with PDF, Word, Text, JSON, CSV, Excel, and Markdown files  
✅ **Semantic Search** - Uses embeddings for intelligent document retrieval  
✅ **Context-Aware Answers** - LLM generates answers based on your documents  
✅ **Metadata Preservation** - Tracks document source for answer attribution  
✅ **Configurable Chunking** - Adjust chunk size and overlap for your use case  

## Technologies Used

- **sentence-transformers** - Semantic embeddings
- **Chroma** - Vector database
- **OpenAI Python Client** - DeepSeek LLM API integration
- **PyPDF2** - PDF processing
- **python-docx** - Word document processing
- **pandas** - CSV and Excel handling

## Configuration

You can customize the RAG system by modifying parameters in each step:

- **Chunk Size** (Step 2): Adjust `chunk_size` parameter (default: 500)
- **Overlap** (Step 2): Adjust `overlap` parameter (default: 50)
- **Embedding Model** (Step 3): Change `model_name` parameter
- **Retrieval Count** (Step 6): Adjust how many chunks to retrieve
- **LLM Temperature** (Step 8): Control randomness/creativity of responses

## Example Use Cases

- **Knowledge Base Q&A** - Build a chatbot based on company documentation
- **Research Assistant** - Ask questions about research papers and reports
- **Customer Support** - Answer questions using product manuals and guides
- **Legal Document Analysis** - Extract information from contracts and agreements
- **Educational Tool** - Learn from textbooks and course materials

## Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest improvements
- Submit pull requests
- Add support for more document formats

## License

This project is open source. Please check the LICENSE file for details.

## Support

For issues, questions, or suggestions, please open an issue on the GitHub repository.
