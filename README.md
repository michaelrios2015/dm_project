# 📚 Book Genre Classification using NLP

**Fordham University — Data Mining Final Project**
Michael Rios | Dept. of Computer & Information Science

---

## Overview

Can a machine classify a book's genre based solely on its plot summary? This project attempts to answer that question using a dataset of 16,559 books extracted from Wikipedia, applying natural language processing and supervised machine learning techniques to predict genre labels.

The short answer: yes — but the quality of your classes matters just as much as the algorithm.

---

## Dataset

- **Source:** [CMU Book Summary Dataset](https://www.cs.cmu.edu/~dbamman/booksummaries.html) compiled by David Bamman, UC Berkeley
- **Size:** 16,559 books, reduced to 10,636 after cleaning
- **Features:** Book title, author, publication date, genre labels, plot summary (~half page each)

### Class Consolidation

The raw data contained 180 genre classes, many with only one entry. These were hand-clustered into 7 meaningful categories:

| Genre | Entries |
|-------|---------|
| Science Fiction | 2,556 |
| Mystery | 2,139 |
| Fiction | 1,622 |
| Children's Literature | 1,480 |
| Speculative Fiction | 1,444 |
| Historical Novel | 770 |
| Fantasy | 625 |

---

## Methods

### Algorithms
- **Naive Bayes** — baseline text classifier
- **Support Vector Machine (SVM)** — primary classifier
- **K-Means Clustering** — used to explore alternative, data-driven class structures

### Text Vectorization
- TF-IDF vectorization with n-gram ranges
- Stop word removal
- Parameter tuning via `sklearn GridSearchCV`

### Handling Class Imbalance
- Random Oversampling (ROS) applied to address imbalanced class distributions

---

## Results

### 7-Class Problem
| Algorithm | Data | Parameters | Accuracy |
|-----------|------|------------|----------|
| Naive Bayes | Unbalanced | Default | 0.378 |
| Naive Bayes | Unbalanced | Tuned | 0.597 |
| Naive Bayes | ROS | Default | 0.630 |
| SVM | Unbalanced | Default | 0.648 |
| SVM | ROS | Default | 0.651 |

### 4-Class Simplified Problem (Top genres only)
| Algorithm | Data | Parameters | Accuracy |
|-----------|------|------------|----------|
| Naive Bayes | Unbalanced | Tuned | 0.755 |
| SVM | Unbalanced | Default | 0.776 |

### K-Means Clustered (3 classes, best result)
| Algorithm | Data | Accuracy |
|-----------|------|----------|
| SVM | Clustered + Simplified | **0.90** |

---

## Key Findings

- **Simplifying the problem helps significantly** — reducing from 7 to 4 classes jumped accuracy from ~65% to ~77%
- **SVM consistently outperforms Naive Bayes**, consistent with sklearn documentation recommendations for text classification
- **Small classes get absorbed** — minority genres like Fantasy and Speculative Fiction were frequently misclassified as Science Fiction
- **Data-driven clustering works well numerically** but produces classes that are harder to interpret meaningfully for humans
- **Half-page summaries are limiting** — longer text samples would likely improve model performance considerably
- **Class curation is critical** — the Wikipedia genre labels contained meaningful overlap (e.g., Speculative Fiction vs. Science Fiction) that hurt classification performance

---

## Technologies Used

- Python
- Scikit-learn (Naive Bayes, SVM, K-Means, GridSearchCV, TF-IDF)
- Jupyter Notebook
- Pandas / NumPy
- Matplotlib (confusion matrices, pie charts)

---

## Conclusions

Genre classification of fiction is achievable with NLP techniques, but success depends heavily on the quality and curation of class labels. A more focused question — such as "is this book science fiction or not?" — may be more realistic given the inherent overlap between literary genres. Future improvements would include using larger text samples, more carefully curated genre labels, and potentially more sophisticated embeddings beyond TF-IDF.

---

*Written as a final project for Data Mining, Fordham University, December 2023.*
