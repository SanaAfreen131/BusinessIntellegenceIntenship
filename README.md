
# Generative AI for BPMN Process Description – Wirtschaftsinformatik Praktikum

This repository contains my implementation of a **multi-stage Retrieval-Augmented Generation (RAG) system** that uses **Large Language Models (LLMs)** to describe, evaluate, extract from, and iteratively correct natural language descriptions of **BPMN (Business Process Model and Notation)** diagrams. Developed as part of the *Wirtschaftsinformatik Praktikum* course at Goethe University Frankfurt (Winter 2025/26).

## 🎯 Objective
Automate the generation of accurate, human-readable process descriptions from BPMN models using LLMs, then:
- Extract structured elements (tasks, gateways, events) from text,
- Evaluate correctness via **precision/recall**,
- Automatically **detect and correct errors** through an iterative feedback loop.

## 🛠️ Tech Stack
- **Framework**: [Haystack 2.x](https://haystack.deepset.ai/) (by deepset)
- **LLM**: `Llama 3.1` / `Llama 3.2` via **Ollama**
- **Languages**: Python
- **Modeling**: BPMN 2.0 (XML), Camunda Modeler
- **Key Techniques**:
  - RAG with custom document stores
  - Structured output validation (`OutputValidator`)
  - XML-aware text preprocessing (coordinate removal)
  - Prompt engineering (chat vs. standard, with/without examples)
  - Custom Haystack components & pipeline chaining
  - Automated evaluation & correction loops

## 📁 Project Structure
```
.
├── data/
│   ├── bpmn/                 # Raw and cleaned BPMN files (.bpmn, .txt)
│   └── documents/            # Descriptive texts & annotated examples
├── pipelines/
│   ├── generator/            # RAG-based description generator (Ex. 3, 6)
│   ├── extractor/            # Element extraction via structured output or annotation (Ex. 4)
│   ├── evaluator/            # Precision/recall computation (Ex. 3, 5)
│   └── corrector/            # Error-driven text refinement (Ex. 5, 6)
├── notebooks/
│   └── *.ipynb               # Step-by-step implementations per exercise
├── utils/
│   ├── bpmn_parser.py        # Extract element names & remove coordinates
│   └── metrics.py            # Precision, recall, and error detection
└── README.md
```

## 🔧 Key Features Implemented
✅ **Custom Dataset**: 4 BPMN models (2 given + 2 self-created on baggage handling) with ground-truth descriptions  
✅ **Multi-strategy RAG**: Compared 3 prompting approaches (chat w/ example, plain w/ example, plain w/o example)  
✅ **Structured Extraction**: Enforced JSON/list outputs using `OutputValidator`  
✅ **Annotation-Based Extraction**: Wrapped elements in `<bpmn:task>...</bpmn:task>` tags  
✅ **Automated Evaluation**: Precision/recall computed by comparing extracted vs. ground-truth BPMN elements  
✅ **Iterative Correction Loop**:  
  1. Generate description →  
  2. Extract elements →  
  3. Detect mismatches →  
  4. Retrieve correction rules →  
  5. Regenerate corrected text (up to 5 iterations)  
✅ **LLM-as-a-Judge**: Evaluated readability and proposed novel quality metrics  

## 📊 Evaluation
- Tested on **airport-related BPMN processes** (e.g., carry-on baggage limits, delayed luggage)
- Manual and automated precision/recall scoring across all methods
- Qualitative comparison of LLM-generated vs. human-written descriptions

## 🚀 How to Run
1. Install dependencies:
   ```bash
   pip install haystack-ai ollama lxml beautifulsoup4
   ```
2. Pull Llama 3 model:
   ```bash
   ollama pull llama3.1:8b  # or llama3.2 for better structured output
   ```
3. Place your `.bpmn` files in `data/bpmn/` and run notebooks sequentially.

> 💡 **Note**: All prompts, document stores, and correction rules are designed to be reusable and extensible for other BPMN domains.

## 📚 References
- [Haystack Documentation](https://haystack.deepset.ai/)
- [Camunda BPMN Modeling](https://camunda.com/)
- Lufthansa baggage policies (used for scenario realism)

---

*Developed by Sana Afreen | Master's in Data Science & Business Informatics, Goethe University Frankfurt*
