# Intent-Based Unified Travel Search Using NLP

**Authors:** Arivoli A, Goureesankar S Nair, Vihan Bisnoi  
**Institution:** School of Computer Science and Engineering, Vellore Institute of Technology, Vellore, India  

---

## Abstract

Modern travel planning is fragmented across dozens of platforms. This project proposes a unified NLP-driven travel search framework that combines BERT/RoBERTa-based intent classification, real-time API grounding (Google Places, OpenWeather, Amadeus), and a multi-layer prompt engineering pipeline to reduce hallucination. The system achieves **99.5% intent classification accuracy** (macro-F1: 0.996) and a System Usability Scale score of **69.8/100**.

---

## Key Results

| Metric | Value |
|--------|-------|
| Intent classification accuracy | 99.5% |
| Macro-averaged F1-score | 0.996 |
| Hallucination rate (full pipeline) | 0.0% |
| Median end-to-end latency | 1.52 seconds |
| System Usability Scale (SUS) | 69.8 / 100 |
| Users preferring unified system | 84% (21/25) |

---

## Repository Structure

```
intent-travel-search-nlp/
├── Day1_2_Build_Travel_Intent_Dataset.ipynb      # Build ATIS + custom dataset (11,096 samples)
├── Day3_5_FineTune_BERT_Travel_Intent.ipynb      # Fine-tune BERT, generate paper tables/figures
├── Week2_Prompt_Pipeline_Hallucination_Eval.ipynb # 4-layer prompt pipeline + hallucination eval
└── README.md
```

---

## How to Run

Run the notebooks **in order** — each one builds on the outputs of the previous.

### Notebook 1 — Build Dataset
`Day1_2_Build_Travel_Intent_Dataset.ipynb`
- Downloads the ATIS benchmark from HuggingFace
- Maps 17 ATIS intents to 5 travel categories
- Generates 8,000 custom travel queries via template-based slot filling
- Saves train/val/test splits (80/10/10) to Google Drive

### Notebook 2 — Fine-Tune BERT
`Day3_5_FineTune_BERT_Travel_Intent.ipynb`
- Loads splits from Notebook 1
- Fine-tunes `bert-base-uncased` on the combined 11,096-sample dataset
- Hyperparameters: lr=2e-5, batch=32, epochs=4, weight_decay=0.01, warmup_steps=100, max_length=64
- Generates Table V, confusion matrix, and training curves for the paper

### Notebook 3 — Prompt Pipeline & Evaluation
`Week2_Prompt_Pipeline_Hallucination_Eval.ipynb`
- Implements the 4-layer prompt pipeline (System Grounding → RAG → Schema → CoVe)
- Runs hallucination evaluation across 200 queries × 3 configurations
- Generates Table VI and Table VII for the paper

---

## Requirements

- Python 3.10+
- Google Colab (free T4 GPU sufficient for Notebook 2)
- HuggingFace Transformers v4.x
- Gemini API key (free tier) — for Notebook 3
- OpenWeather API key (free tier) — for Notebook 3

Install dependencies (handled inside each notebook):
```bash
pip install transformers datasets accelerate scikit-learn pandas matplotlib seaborn
pip install google-generativeai requests
```

---

## Five Travel Intent Categories

| Intent | Example Query | API Action |
|--------|--------------|------------|
| Booking | "Book a flight to Paris on March 15" | Amadeus flight search |
| Inquiry | "What is the weather in Bali in April?" | OpenWeather forecast |
| Navigation | "How to get from airport to downtown Tokyo?" | Google Maps route |
| Exploration | "Romantic getaways in Europe under 1500 EUR" | Multi-API itineraries |
| Comparison | "Compare Hilton vs Marriott in Chicago" | Booking.com side-by-side |

---

## Citation

If you use this code or dataset in your research, please cite:

```
Goureesankar S Nair "Intent-Based Unified Travel 
Search Using Natural Language Processing," School of Computer Science and 
Engineering, Vellore Institute of Technology, Vellore, India, 2025.
```
