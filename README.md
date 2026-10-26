# Multilingual Healthcare Misinformation RAG

A retrieval-augmented generation (RAG) application for checking healthcare claims in English, Hindi, and Hinglish. It retrieves medical evidence, presents a transparent verdict, and highlights the potential risk of misinformation.

> **Important:** This project is for educational and research use only. It does not provide medical advice, diagnosis, or treatment. Always consult a qualified healthcare professional for personal medical decisions.

## Features

- Verifies healthcare claims in **English**, **Hindi (Devanagari)**, and **Hinglish**.
- Detects and filters non-health queries before retrieval.
- Supports two evidence modes: a local curated dataset and live retrieval from biomedical sources.
- Uses multilingual sentence embeddings and FAISS (with a NumPy fallback) for semantic search.
- Returns a verdict — **Supported**, **Refuted**, **Uncertain**, or **No relevant evidence** — plus a risk level and source links.
- Includes a Gradio web interface, a Jupyter notebook, and automated tests.

## Architecture

```text
Claim (English / Hindi / Hinglish)
            |
     Preprocessing + language detection
            |
       Health-domain guardrail
            |
   Curated evidence or live evidence retrieval
            |
 Multilingual embeddings + similarity ranking
            |
    Verdict, risk level, explanation, citations
```

## Project structure

```text
.
├── data/                                      # Curated evidence and embedding cache
├── scripts/                                   # Dataset and notebook utilities
├── src/
│   ├── app.py                                 # Gradio application
│   ├── preprocessing.py                       # Text and Hinglish normalization
│   ├── language_detector.py                   # English/Hindi/Hinglish detection
│   ├── health_classifier.py                   # Health-domain guardrail
│   ├── rag_engine.py                          # Embedding and retrieval logic
│   ├── live_retriever.py                      # External evidence retrieval
│   └── verdict_engine.py                      # Verdict and risk assessment
├── tests/test_pipeline.py                     # Unit and integration tests
├── Multilingual_Healthcare_Misinformation_RAG.ipynb
└── requirements.txt
```

## Setup

Prerequisites: Python 3.10+ and `pip`.

```bash
git clone https://github.com/its-SHANU/Multilingual-Healthcare-Misinformation-RAG.git
cd Multilingual-Healthcare-Misinformation-RAG
python -m venv .venv
```

Activate the environment:

```bash
# Windows PowerShell
.\.venv\Scripts\Activate.ps1

# macOS/Linux
source .venv/bin/activate
```

Install dependencies and launch the application:

```bash
pip install -r requirements.txt
python src/app.py
```

Then open the local Gradio URL shown in the terminal (normally `http://127.0.0.1:7860`). The first run may download the embedding model.

## Usage

Choose either the local curated dataset or live retrieval mode, enter a health-related claim, and review the returned verdict, risk assessment, explanation, and evidence links.

Example claims:

| Claim | Language | Expected behavior |
| --- | --- | --- |
| `Smoking causes lung cancer` | English | Supported |
| `Haldi doodh cancer ko theek karta hai` | Hinglish | Evaluates against available evidence |
| `क्या COVID vaccine सुरक्षित है?` | Hindi | Evaluates against available evidence |
| `India won the cricket match` | English | Filtered as a non-health query |

## Tests

Run the test suite from the project root:

```bash
python -m unittest discover -s tests -v
```

## Data and sources

The curated mode uses the repository's clinical evidence dataset. Live mode retrieves and ranks results from external biomedical sources. Source links shown by the application should be reviewed directly, particularly for medical decisions.

## License

No license file is currently included. Add a license before redistributing or accepting external contributions.
