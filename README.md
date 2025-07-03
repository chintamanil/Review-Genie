# Review Genie: RAG Evaluation Pipeline

## Overview
Review Genie is a Retrieval-Augmented Generation (RAG) application designed to provide accurate, relevant, and grounded answers to product-related queries, specifically for Amazon products. This project demonstrates how to build, evaluate, and trace a RAG pipeline using [LangChain](https://python.langchain.com/) and [LangSmith](https://smith.langchain.com/), leveraging OpenAI embeddings and a FAISS vector store for document retrieval.

## Features
- **RAG Bot**: Answers user questions by retrieving relevant product information and generating responses.
- **Evaluation Dataset**: Contains example questions and ground-truth answers for Amazon products.
- **Automated Evaluation**: Uses multiple LLM-based evaluators (correctness, relevance, groundedness, retrieval relevance) to assess the quality of generated answers.
- **Experiment Tracking**: Integrates with LangSmith for tracing, debugging, and experiment management.

## Directory Structure
```
Review-Genie/
├── app.py           # Main application and evaluation pipeline
├── faiss_index/     # FAISS vector store files
└── README.md        # Project documentation
```

## Setup
1. **Clone the repository**
   ```bash
   git clone <repo-url>
   cd Review-Genie
   ```
2. **Install dependencies**
   - Python 3.8+
   - Install required packages:
     ```bash
     pip install langchain langsmith openai faiss-cpu
     ```
3. **Set up environment variables**
   - Obtain API keys for OpenAI and LangSmith.
   - Set the following environment variables:
     ```bash
     export OPENAI_API_KEY=your-openai-key
     export LANGCHAIN_TRACING_V2=true
     export LANGCHAIN_API_KEY=your-langsmith-key
     export LANGCHAIN_PROJECT=Review-Genie
     ```
4. **Prepare the FAISS index**
   - Ensure the `faiss_index/` directory contains the necessary FAISS index files for retrieval.

## Usage
Run the main application to perform RAG evaluation:
```bash
python app.py
```
This will:
- Load the FAISS vector store and set up the RAG bot.
- Run the bot on the evaluation dataset.
- Evaluate responses using the defined evaluators.
- Log results and traces to your LangSmith dashboard.

## Evaluation Methodology
The evaluation pipeline uses four LLM-based evaluators:
1. **Correctness**: Compares the generated answer to a ground-truth answer.
2. **Relevance**: Assesses if the answer addresses the user's question.
3. **Groundedness**: Checks if the answer is supported by retrieved documents (no hallucination).
4. **Retrieval Relevance**: Evaluates if the retrieved documents are relevant to the question.

Each evaluator uses GPT-4o as a judge and provides structured output with explanations and boolean scores. Results are tracked and visualized in LangSmith.

## References
- [LangChain Documentation](https://python.langchain.com/)
- [LangSmith Platform](https://smith.langchain.com/)
- [OpenAI API](https://platform.openai.com/docs/)
- [FAISS](https://github.com/facebookresearch/faiss)

## License
This project is for educational and research purposes.