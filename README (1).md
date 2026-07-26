# Predict-Sentimen-MBG
### Sentiment Classification of Reddit Comments Using Fine-Tuned IndoBERT
#### Case Study: Indonesia's Free Nutritious Meals Program (Program Makan Bergizi Gratis / MBG)

[![IndoBERT](https://img.shields.io/badge/model-IndoBERT-orange)](https://huggingface.co/indobenchmark)
[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![DOI](https://img.shields.io/badge/DOI-10.21070%2Fups.10480-blue.svg)](https://doi.org/10.21070/ups.10480)

## 📌 Overview
This repository contains the complete pipeline for classifying public sentiment in Reddit forum comments discussing Indonesia's **Free Nutritious Meals Program** (*Program Makan Bergizi Gratis* / MBG). A pre-trained **IndoBERT** model is fine-tuned on a **manually annotated** dataset to classify each comment into one of three sentiment labels — **positive, negative, or neutral**.

The project covers the full workflow end-to-end: data collection, preprocessing, manual labeling, model fine-tuning, evaluation, full-dataset prediction, and result analysis. It is documented in an undergraduate thesis published on the UMSIDA Preprints Server (DOI: [10.21070/ups.10480](https://doi.org/10.21070/ups.10480)).

## ✨ Key Highlights
- **6,295** Reddit comments collected (2024–2025).
- **3,000** comments **manually annotated** into a balanced 3-class dataset.
- Fine-tuned **IndoBERT** achieved **99.00% accuracy, F1-score, and precision**.
- Mean prediction confidence of **0.8502** with a throughput of **137.93 samples/second** — suitable for near real-time policy monitoring.

## 🗂️ Dataset & Annotation
> This section documents the data labeling work, which is the core of the project.

### Data Source
- Raw comments were collected from public Reddit forums using **PRAW (Python Reddit API Wrapper)**.
- A total of **6,295 comments** posted during **2024–2025** were gathered for the study.

### Manual Annotation
- A **balanced subset of 3,000 comments** was **annotated by hand** into three sentiment classes.
- Annotation was performed manually to ensure label quality and consistency before model training.
- The labeling process is visually documented in [`dokumentasi/3. proses labeling manual`](dokumentasi/3.%20proses%20labeling%20manual).

### Label Scheme
| Label | Definition |
|-------|-----------|
| **Positive** | Comments expressing support, approval, or a favorable opinion toward the program. |
| **Negative** | Comments expressing criticism, dissatisfaction, or an unfavorable opinion toward the program. |
| **Neutral** | Comments that are factual, informational, or without a clear positive/negative stance. |

### Train / Test Split
- The annotated dataset was split **80:20** into training and testing sets.

## 🔄 Project Workflow
The pipeline is organized into sequential notebooks (inside `kode pyhton/`), each documented with screenshots in `dokumentasi/`:

| Step | Notebook | Description |
|------|----------|-------------|
| 1 | `1. Colllecting-Dataset_MBG.ipynb` | Collect Reddit comments via PRAW (6,295 comments, 2024–2025). |
| 2 | `2. Pre-Process-INDOBERT-MBG.ipynb` | Preprocess text: normalize colloquial language, convert emojis, and translate to Indonesian. |
| — | *(manual)* | Manually label a balanced set of 3,000 comments (positive / negative / neutral). |
| 3 | `3. Spliting_Data_MBG.ipynb` | Split the annotated data into training and testing sets (80:20). |
| 4 | `4. Fine Tuning_Evaluation_MBG.ipynb` | Fine-tune IndoBERT and evaluate it (accuracy, precision, recall, F1-score). |
| 5 | `5. Predicted-Procces_MBG.ipynb` | Predict sentiment labels across the full dataset. |
| 6 | `6. Results-Analysis_MBG.ipynb` | Analyze results: sentiment distribution and word clouds. |

## 🧹 Preprocessing Pipeline
Before annotation and modeling, raw comments went through the following preprocessing steps:
1. **Colloquial language normalization** — standardizing informal/slang Indonesian words.
2. **Emoji conversion** — converting emojis into their textual meaning.
3. **Translation to Indonesian** — translating non-Indonesian comments so the corpus is consistent for IndoBERT.

## 🤖 Methodology
- **Model:** IndoBERT (pre-trained Bahasa Indonesia BERT, from the [IndoNLP benchmark](https://huggingface.co/indobenchmark)).
- **Approach:** Fine-tuning the pre-trained transformer on the manually annotated 3-class sentiment dataset.
- **Task:** Multi-class text classification (positive / negative / neutral).

## 📊 Results
| Metric | Score |
|--------|-------|
| Accuracy | **99.00%** |
| F1-Score | **99.00%** |
| Precision | **99.00%** |
| Mean Confidence | 0.8502 |
| Throughput | 137.93 samples/second |

**Sentiment distribution on the full (6,295-comment) dataset:**
- Neutral: **59.44%**
- Positive: **34.11%**
- Negative: **6.45%**

## 🛠️ Tech Stack
- **Language:** Python
- **NLP / Model:** IndoBERT via Hugging Face `transformers`
- **Data Collection:** PRAW (Python Reddit API Wrapper)
- **Notebooks:** Jupyter Notebook
- **Data & ML utilities:** pandas, NumPy, scikit-learn
- **Visualization:** Matplotlib, wordcloud

## 📁 Repository Structure
```
Predict-Sentimen-MBG/
├── kode pyhton/                                          # Python notebooks (the full pipeline)
│   ├── 1. Colllecting-Dataset_MBG.ipynb                  # Data collection from Reddit (PRAW)
│   ├── 2. Pre-Process-INDOBERT-MBG.ipynb                 # Preprocessing: cleaning & translation
│   ├── 3. Spliting_Data_MBG.ipynb                        # Train/test split (80:20)
│   ├── 4. Fine Tuning_Evaluation_MBG.ipynb               # IndoBERT fine-tuning & evaluation
│   ├── 5. Predicted-Procces_MBG.ipynb                    # Prediction on the full dataset
│   └── 6. Results-Analysis_MBG.ipynb                     # Result analysis (distribution, word cloud)
│
├── dokumentasi/                                          # Step-by-step process documentation (screenshots)
│   ├── 1. proses collecting data/
│   ├── 2. proses pre-processing (cleaning dan translating)/
│   ├── 3. proses labeling manual/                        # Manual annotation process
│   ├── 4. proses split data/
│   ├── 5. proses training dan fine tuning/
│   ├── 6. proses evaluasi (presisi, recall, akurasi)/
│   ├── 7. proses prediksi full dataset/
│   └── 8. proses analisis (distribusi, wordcloud)/
│
└── README.md
```

## 🚀 How to Run
The project is notebook-based. Run the notebooks **in order (1 → 6)** inside the `kode pyhton/` folder.

1. **Clone the repository:**
   ```bash
   git clone https://github.com/kazenesia/Predict-Sentimen-MBG.git
   cd Predict-Sentimen-MBG
   ```

2. **Set up the environment and install dependencies:**
   ```bash
   pip install transformers torch praw pandas numpy scikit-learn matplotlib wordcloud jupyter
   ```

3. **Configure Reddit API credentials** (required by Notebook 1 for data collection via PRAW):
   - Create an app at [reddit.com/prefs/apps](https://www.reddit.com/prefs/apps) and fill in your `client_id`, `client_secret`, and `user_agent`.

4. **Run the notebooks sequentially:**
   - `1. Colllecting-Dataset_MBG.ipynb` → collect raw comments
   - `2. Pre-Process-INDOBERT-MBG.ipynb` → clean & translate the text
   - *(manual labeling of 3,000 comments)*
   - `3. Spliting_Data_MBG.ipynb` → split into train/test (80:20)
   - `4. Fine Tuning_Evaluation_MBG.ipynb` → fine-tune & evaluate IndoBERT
   - `5. Predicted-Procces_MBG.ipynb` → predict on the full dataset
   - `6. Results-Analysis_MBG.ipynb` → analyze & visualize the results

> *(Adjust the dependency list above to match the exact versions you used.)*

## 📚 Documentation
The `dokumentasi/` folder contains visual documentation (screenshots) for every stage of the pipeline — from data collection and **manual labeling** to training, evaluation, prediction, and analysis. This makes each step of the workflow transparent and easy to follow.

## 📖 Citation
If you use this work, please cite:

> Bram Aji Saka Putra & Suprianto. (2026). *Classification of Sentiment in Reddit Forum Comments Using Fine-Tuned IndoBERT (Case Study: Free Nutritious Meal Program)*. UMSIDA Preprints Server. https://doi.org/10.21070/ups.10480

## 📄 License
This work is licensed under a [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
