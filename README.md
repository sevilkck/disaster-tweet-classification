# Disaster Tweet Classification

A natural language processing (NLP) project that classifies tweets as describing real disasters or not using machine learning.

## Overview

This project builds a binary classifier to distinguish between tweets about actual disasters (e.g., earthquakes, wildfires) and tweets using disaster-related vocabulary figuratively (e.g., "this party is on fire"). The classifier uses classical NLP techniques with scikit-learn.

**Dataset:** [Kaggle NLP Getting Started Competition](https://www.kaggle.com/c/nlp-getting-started) — 7,613 labeled tweets

## Pipeline

| Step | Description |
|------|-------------|
| Data Loading | Load and inspect the training dataset |
| EDA | Analyze class distribution, tweet length, word frequencies, hashtags |
| Text Preprocessing | Clean tweets (remove URLs, mentions, stopwords; lemmatize) |
| Feature Extraction | TF-IDF vectorization with unigrams and bigrams |
| Model Training | Logistic Regression and Naive Bayes classifiers |
| Evaluation | Accuracy, F1-score, confusion matrix, cross-validation |
| Hyperparameter Tuning | GridSearchCV for optimal configuration |

## Results

| Model | Accuracy | F1-Score |
|-------|----------|----------|
| Logistic Regression (baseline) | ~79% | ~75% |
| Naive Bayes (baseline) | ~78% | ~73% |
| Logistic Regression (tuned) | ~80% | ~76% |

**Best Configuration (GridSearchCV):**
- TF-IDF with 5,000–10,000 features
- Unigrams + bigrams
- Regularization parameter C optimized via 3-fold CV

## Key Findings

- **Class imbalance:** Dataset is slightly imbalanced (57% non-disaster, 43% disaster), making F1-score more meaningful than accuracy
- **Bigrams matter:** Two-word phrases like "flash flood" and "search rescue" improve classification
- **Main challenge:** Figurative language — tweets like "this sale is fire" can fool the classifier
- **Logistic Regression outperforms Naive Bayes** because it doesn't assume feature independence

## Project Structure

```
disaster_tweets_project/
├── disaster_tweets.ipynb     # Main notebook with full pipeline
├── train.csv                 # Training dataset
├── WALKTHROUGH.md            # Detailed cell-by-cell explanation
├── plots/                    # Generated visualizations
│   ├── plot_class_distribution.png
│   ├── plot_tweet_length.png
│   ├── plot_top_words_raw.png
│   ├── plot_top_words_clean.png
│   ├── plot_hashtags.png
│   ├── plot_cm_lr.png
│   ├── plot_cm_nb.png
│   ├── plot_cm_tuned.png
│   └── plot_model_comparison.png
├── generate_plots.py         # Script to regenerate plots
├── build_html.py             # Generate HTML presentation
├── build_pptx.py             # Generate PowerPoint presentation
├── presentation.html         # HTML presentation output
└── disaster_tweets_presentation.pptx  # PowerPoint output
```

## Technologies

- **Python 3**
- **pandas, numpy** — data manipulation
- **matplotlib, seaborn** — visualization
- **nltk** — tokenization, stopwords, lemmatization
- **scikit-learn** — TF-IDF, model training, evaluation, GridSearchCV

## Usage

```bash
# Install dependencies
pip install pandas numpy matplotlib seaborn nltk scikit-learn

# Run the notebook
jupyter notebook disaster_tweets.ipynb
```

## Limitations & Future Work

- **No semantic understanding:** TF-IDF treats words independently and cannot understand context or sarcasm
- **Figurative language:** Metaphors remain the primary source of classification errors
- **Potential improvement:** Fine-tuning a transformer model (BERT, RoBERTa) would significantly improve handling of context and figurative expressions
