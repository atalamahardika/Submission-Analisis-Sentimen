# 🎮 Sentiment Analysis Project: Mobile Legends App Reviews

[![Python](https://img.shields.io/badge/Python-3.12%2B-blue?style=flat-for-the-badge&logo=python)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.19%2B-orange?style=flat-for-the-badge&logo=tensorflow)](https://www.tensorflow.org/)
[![NLP](https://img.shields.io/badge/NLP-Deep%20Learning-green?style=flat-for-the-badge)](#-project-architecture-and-workflow)

This project implements a comprehensive Natural Language Processing (NLP) and Deep Learning pipeline to analyze user sentiment from Mobile Legends app reviews on the Google Play Store. The project lifecycle is engineered end-to-end, encompassing data mining (data scraping), multi-layered text preprocessing, automated lexicon-based labeling, and a performance benchmarking suite across Recurrent Neural Network (RNN) architectures.

---

## 📂 Repository Structure

The project directory is organized modularly to decouple data assets, experimental pipelines, and environment specifications:

```text
Submission-Analisis-Sentimen/
├── data/
│   ├── ulasan_mobile_legends_70k.csv  # Raw scraped dataset (70,000 rows)
│   └── clean_review_70k.csv           # Preprocessed dataset containing lexicon targets
├── notebook/
│   ├── scrapping.ipynb                # Google Play Store data extraction pipeline
│   ├── preprocessing.ipynb            # 9-stage text cleaning & lexicon labeling notebook
│   └── train_model.ipynb              # Deep Learning experimental modeling & inference testing
├── kamus_custom_en.txt                # Normalization dictionary for slang words and abbreviations
├── requirements.txt                   # Complete project dependency manifest
└── README.md                          # Main project documentation
```

## 🔄 Project Architecture and Workflow  
### 1. Data Scraping (`scrapping.ipynb`)
The review dataset was mined independently utilizing the `google_play_scraper` library. A corpus containing 70,000 unique user reviews was successfully extracted to represent public user opinion.

### 2. Text Preprocessing & Lexicon Labeling (`preprocessing.ipynb`)
To minimize lexical noise, the text data was pushed through a rigorous **9-stage Preprocessing Pipeline**:
1. **Case Folding:** Normalizing all text elements to lowercase characters.
2. **Remove Emoji:** Stripping emoji characters using the `emoji` library.
3. **Remove Special Characters:** Purging all non-alphanumeric symbols.
4. **Remove Numbers:** Eliminating numerical digits devoid of semantic weight.
5. **Remove Punctuation:** Filtering out all punctuation markers.
6. **Slangwords Normalization:** Remapping informal text and abbreviations (e.g., *pls*, *thx*) into formal language using definitions from `kamus_custom_en.txt`. 
7. **Tokenizing:** Segmenting text strings into individual word tokens.
8. **Stopword Removal:** Discarding high-frequency structural words that contain no distinct emotional value via the *NLTK* English Stopwords corpus.
9. **Lemmatization:** Resolving words down to their root dictionary form (*lemma*) with the `WordNetLemmatizer`.

Following text normalization, automated data labeling into 3 distinct classes was orchestrated using the **VADER SentimentIntensityAnalyzer** under formal compound score thresholds:
* **Positive:** `score >= 0.3` (Quantified: **38.512 records**)
* **Negative:** `score <= -0.3` (Quantified: **19.447 records**)
* **Neutral:** `-0.3 < score < 0.3` (Quantified: **12.041 records**)

### 3. Deep Learning Modeling (`train_model.ipynb`)
The processed dataset was split using an 80:20 Stratified Split configuration (56,000 train items & 14,000 validation items) to prevent class distribution shifts during evaluation. Texts were tokenized using a vocabulary maximum (*vocab size*) of 10,000 words and padded to a uniform sequence length (*max length*) of 50 tokens. Three distinct sequence processing networks were benchmarked under Early Stopping controls:
* **SimpleRNN:** A baseline sequential Recurrent Neural Network model reinforced with L2 regularization layers.
* **GRU (Gated Recurrent Unit):** A specialized RNN utilizing information gating structures to manage long-term textual dependencies.
* **Custom Model:** A custom DNN framework using GlobalAveragePooling1D followed by deep Dense configurations.

---

## 📈 Model Evaluation & Benchmarking Results

The following matrix summarizes model performance variations post-training across the tested structural configurations:
| Model Architecture | Training Accuracy | Training Loss | Validation Accuracy | Validation Loss | Evaluation Status |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **SimpleRNN** | 0.9395 | 0.1650 | 0.9054 | 0.2890 | Slight Overfitting |
| **GRU (Best Model)** | **0.9287** | **0.1917** | **0.9064** | **0.2760** | **Optimal Generalization** |
| **Custom Model** | 0.9023 | 0.2599 | 0.8701 | 0.3441 | Slow Convergence |

> 🏆 **Architecture Recommendation: GRU** has been selected as the optimal production engine for live inference pipelines. Although its training accuracy rests marginally lower than SimpleRNN, GRU established the **lowest Validation Loss (0.2760)**. This proves that the internal gating cells of the GRU architecture effectively resolve vanishing gradient limitations, adapting securely to unseen user reviews with higher predictive reliability.
> **Rekomendasi Arsitektur:** **GRU** dipilih sebagai model produksi terbaik untuk tahap inferensi. Meskipun akurasi training sedikit di bawah SimpleRNN, GRU berhasil mencatatkan **Validation Loss terendah (0.2760)**. Hal ini mengonfirmasi bahwa struktur internal GRU mampu mereduksi efek *vanishing gradient* dan menggeneralisasi ulasan baru secara lebih adaptif.
