# BPMN to Text Generation and Correction with Haystack

This project implements a multi-step pipeline using Haystack and large language models (LLMs) to translate BPMN process models into natural language descriptions and back. The system includes generation, extraction, validation, and iterative correction to ensure the textual description accurately reflects the original process model.

## Overview

The pipeline consists of three main components:

1. **Generator**: Converts a BPMN file into a fluent, descriptive paragraph using an LLM (e.g., Llama 3).
2. **Extractor**: Parses the generated text to recover process elements such as tasks, events, and gateways.
3. **Corrector**: Compares extracted elements with the ground truth from the BPMN file, identifies discrepancies, and prompts the LLM to revise the text accordingly.

The process repeats up to five times or until no errors remain, creating a self-correcting loop between structured and unstructured representations of business processes.

## Technologies Used

- Python
- Haystack (v1.x)
- Llama 3 via Ollama
- XML parsing for BPMN files
- Custom validation logic

## Project Structure
