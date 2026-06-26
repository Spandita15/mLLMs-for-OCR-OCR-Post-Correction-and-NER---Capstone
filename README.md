# Multimodal LLMs for OCR, OCR-Post Correction and Named Entity Recognition in historical documents
## Dataset:
* **Input:** 10 multi-page historical German economic and city directory documents (Fraktur / Gothic print) PDFs, converted to PNGs at 300 DPI.
* **Source:** Ground-truth benchmark from Griesshaber et al. (2025)
* **Preprocessing:** Enhanced contrast/sharpness; cleaned text (ligatures, special characters).
## Problem
* Vast archives of digitized Fraktur/Gothic documents (census, trade records) are time-consuming and error-prone to process
* Conventional OCR struggles with noisy scans, old fonts, and layout variability, requiring hours of manual cleaning by historians.
* Critical for digital humanities, economic history, and genealogy; enables searchable databases and preserves cultural heritage.
## Solution:
A reproducible pipeline merging visual understanding with schema-constrained extraction, robustly handling 
Fraktur text and outputting CSV-ready records deterministically.
## Implementation Code: 
https://colab.research.google.com/drive/10mxsiBatD9BNXklUIS49BEJoviimEC3Y?usp=sharing
## End-to-end architecture:
Preprocessing ------> OCR Engine ------> mLLM ------> CSV Parsing ------> Benchmarking
### Model Functionality (One-step):
Read Text (OCR) ------> Correct Errors (Post-correction) ------> Identify and Organize Titles (NER)
## Implementation Details:
* Frameworks: Python, PyTorch, HuggingFace,Google Generative AI
* Models: Gemini 2.0 Flash, LLaVA, Florence-2, Tesseract(deu, deu_frak)
* Setting: Zero-shot inference, Temperature 0.0 (deterministic generation)
## Evaluation Metrics:
* Exact Match Accuracy: Measures character-for character correctness (case insensitive) between predicted and ground-truth text
* Fuzzy Match Accuracy: Uses Jaro–Winkler similarity (threshold 0.90) to allow small spelling or accent differences (e.g., "Müller" vs "Mueller").
## Key Findings:
* Gemini 2.0 Flash gave the best structured extraction accuracy (~96% fuzzy match and 77% exact match).
* Traditional OCR (Tesseract) struggles with historical documents and layout irregularities.
* Preprocessing and structured prompt design were critical factors, improving fuzzy accuracy by ~4%.
* Gemini correctly identifies and separates fields (name, occupation, address), indicating semantic understanding.
