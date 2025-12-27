# mistral-llm-summariser
Local PDF summarization pipeline using Mistral + Ollama for Supreme Court judgments

This repository contains a Jupyter Notebook that implements a fully local pipeline for summarizing large legal judgment PDFs using the Mistral language model running via Ollama.

The pipeline is designed to handle long documents efficiently while preserving legal reasoning and producing outputs suitable for analysis and social listening.

┌──────────────────────────┐
│   Judgment PDF (.pdf)    │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Semantic PDF Extraction  │
│ - Remove headers/footers │
│ - Remove boilerplate     │
│ - Normalize paragraphs   │
│ - Sentence compression   │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│   Compressed Text        │
│   (High-signal content)  │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Token-Aware Chunking     │
│ - Overlapping chunks     │
│ - Context-safe sizes     │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Chunk Summarization      │
│ (Mistral via Ollama)     │
│ - Local inference        │
│ - Low temperature        │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Hierarchical Reduction   │
│ (Mistral via Ollama)     │
│ - Merge chunk summaries  │
│ - Coherent final output  │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Final Judgment Summary   │
└─────────────┬────────────┘
              │
      ┌───────┴────────┐
      ▼                ▼
┌──────────────┐  ┌────────────────────────┐
│ Keyword      │  │ Structured Outputs     │
│ Extraction   │  │ - CSV (Judgment,       │
│ (Social      │  │   Keywords, Summary)   │
│ Listening)   │  │ - Text files           │
└──────────────┘  └────────────────────────┘

---

## Overview

The notebook processes Supreme Court judgment PDFs through a multi-stage pipeline:

1. **Semantic PDF Extraction**
   - Extracts raw text from PDFs
   - Removes headers, footers, page numbers, and boilerplate
   - Normalizes paragraphs and compresses text while preserving meaning

2. **Token-Aware Chunking**
   - Splits compressed text into overlapping chunks
   - Ensures compatibility with Mistral’s context window

3. **Local Summarization with Mistral**
   - Summarizes each chunk using Mistral via Ollama
   - Uses low-temperature inference for factual consistency
   - Runs entirely offline (no external APIs)

4. **Hierarchical Summary Reduction**
   - Combines chunk-level summaries into a single coherent judgment summary

5. **Social-Listening Keyword Extraction**
   - Extracts keywords optimized for discovery on Twitter, YouTube, and news platforms
   - Prioritizes case names, legal articles, institutions, and discussion hooks

6. **Structured Outputs**
   - Per-judgment compressed text
   - Per-judgment chunk summaries
   - Final judgment summaries
   - CSV output containing:
     - Judgment name
     - Mistral-generated keywords
     - Mistral-generated summary

---

## Key Features

- Fully local inference using Ollama + Mistral
- Scales to hundreds of pages per document
- No cloud APIs or token limits
- Designed for legal and policy documents
- Outputs ready for social listening and analysis tools

---

## Requirements

- Python 3.10+
- Ollama (with `mistral` model pulled)
- Python packages:
  - `pdfplumber`
  - `tiktoken`
  - `ollama`

---

## Usage

1. Place judgment PDFs in the working directory
2. Open the notebook
3. Run cells sequentially
4. Outputs are generated automatically for each PDF

---

## Use Cases

- Legal document summarization
- Case law analysis
- Policy research
- Social media and public discourse monitoring
- Content discovery for journalism and research

---

## Notes

This pipeline emphasizes **semantic compression before summarization**, which improves summary quality and stability for large documents. The design prioritizes correctness, reproducibility, and privacy.

---

