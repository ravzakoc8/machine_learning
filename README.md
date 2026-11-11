# Machine Learning Midterm Project

**Breast Cancer & Wine – Classification and Clustering**

Student: Ravza Koç – 24040102023
Course: Machine Learning – Midterm Assignment (November 2026)

---

## About This Project

In this project I worked with two datasets from scikit-learn.
I trained three classification models and compared them.
I also used K-Means to see if the data makes natural groups.

I did the same steps for both datasets, but I kept their data, models and results separate.

---

## Datasets

| Dataset | Samples | Features | Classes |
|---|---|---|---|
| Breast Cancer Wisconsin | 569 | 30 | 2 (0 = malignant, 1 = benign) |
| Wine | 178 | 13 | 3 (class 0, class 1, class 2) |

Both datasets come directly from scikit-learn:
- `sklearn.datasets.load_breast_cancer`
- `sklearn.datasets.load_wine`

---

## What I Did (Step by Step)

1. **Loading the data:** I loaded the datasets and made a table (DataFrame) with feature names.
2. **Quality checks:** I checked missing values, duplicate rows, data types and outliers. There were no missing values or duplicates.
3. **EDA:** I looked at basic statistics, class distribution, a correlation heatmap and boxplots.
4. **Splitting:** I kept 20% of the data as a fixed test set (random_state = 42). Then I split the rest into 70% train and 10% validation, three times, with seeds 42, 52 and 62.
5. **Scaling:** I used StandardScaler. I fitted it only on the training data for each seed, so no information from validation or test went into the model.
6. **Two versions of data:** unscaled and scaled.
7. **Training models:** I trained every model setting on both versions and all three seeds.
8. **Validation and model selection:** I picked the best setting using the mean validation macro-F1 score.
9. **Test evaluation:** I tested only the selected model (seed 42) one time on the test set.
10. **K-Means:** I grouped the data without using the labels, then compared the groups with the real classes.

---

## Models and Settings

| Model | Settings I tried |
|---|---|
| Decision Tree | max_depth = 2, 3, 5, 10, None |
| KNN | n_neighbors = 1, 3, 5, 7, 11 (uniform weights, Euclidean distance) |
| Gaussian Naive Bayes | default settings |
| K-Means | n_clusters = 2 (Breast Cancer), 3 (Wine), n_init = 10 |

### Number of runs

| | Breast Cancer | Wine | Total |
|---|---|---|---|
| Classifier runs | 66 | 66 | 132 |
| K-Means runs | 6 | 6 | 12 |
| **All model fits** | **72** | **72** | **144** |

---

## Results

### Classification (selected models)

| Dataset | Selected model | Validation macro-F1 (mean ± std) | Test accuracy | Test macro-F1 | Test ROC-AUC |
|---|---|---|---|---|---|
| Breast Cancer | KNN, scaled, k = 7 | 0.968 ± 0.030 | 0.974 | 0.971 | 0.989 |
| Wine | KNN, scaled, k = 11 | 0.981 ± 0.032 | 1.000 | 1.000 | 1.000 |

### K-Means (test set, seed 42)

| Dataset | Version | Test ARI | Test silhouette |
|---|---|---|---|
| Breast Cancer | unscaled | 0.558 | 0.712 |
| Breast Cancer | scaled | 0.735 | 0.325 |
| Wine | unscaled | 0.373 | 0.493 |
| Wine | scaled | 0.909 | 0.271 |

### What I learned

- **Scaling helped KNN a lot.** For example, on Breast Cancer, KNN with k = 7 went from 0.904 (unscaled) to 0.968 (scaled) validation F1.
- **The same type of model won on both datasets:** scaled KNN (k = 7 for Breast Cancer, k = 11 for Wine).
- **Decision Tree did not change with scaling.** It only checks if a value is bigger or smaller than a limit.
- **Deeper trees overfit.** Training F1 went up to 1.0, but validation F1 did not go up with it.
- **K-Means worked much better after scaling,** especially on Wine (ARI went from 0.373 to 0.909).
- **Wine got a perfect test score (1.0),** but the test set has only 36 samples, so this does not mean the model is perfect.

---

## Project Files

| File / Folder | What is inside |
|---|---|
| `breast_cancer.ipynb` | All steps (Sections 1–10) for Breast Cancer |
| `wine.ipynb` | All steps (Sections 1–10) for Wine + combined CSV files |
| `figures/` | All graphs (EDA, parameter plots, confusion matrices, ROC curves, K-Means plots) |
| `classifier_runs.csv` | 132 rows – one row for each classifier run |
| `classifier_summary.csv` | 44 rows – mean and std over 3 seeds for each setting |
| `classifier_test.csv` | 2 rows – final test results of the selected models |
| `kmeans_runs.csv` | 12 rows – one row for each K-Means run |
| `kmeans_summary.csv` | 4 rows – K-Means summary for each version |
| `kmeans_test.csv` | 4 rows – K-Means test results (seed 42) |
| `report.docx` | Project report |
| `AI_DISCLOSURE.md` | How I used AI tools |
| `requirements.txt` | Python packages and versions |

---

## Figures

| Figure | Breast Cancer | Wine |
|---|---|---|
| Class distribution | Yes | Yes |
| Correlation heatmap | Yes | Yes |
| Boxplots | Yes | Yes |
| Tree depth comparison | Yes | Yes |
| KNN neighbour comparison | Yes | Yes |
| Confusion matrix | Yes | Yes |
| ROC curve(s) | Yes | Yes |
| K-Means (unscaled) | Yes | Yes |
| K-Means (scaled) | Yes | Yes |

---

## How to Run

**1. Install the packages**

```
pip install -r requirements.txt
```

**2. Run the notebooks in this order**

1. Open `breast_cancer.ipynb` and click **Run All**
2. Open `wine.ipynb` and click **Run All**

Note: The order is important. The last cell in `wine.ipynb` combines the CSV files from both notebooks.

---

## Environment

- Python 3.14.3
- pandas 3.1.1
- numpy 2.4.4
- scikit-learn 1.9.1
- matplotlib 3.10.8
- seaborn 0.13.2

The full list is in `requirements.txt`.

---

## Limitations

- The validation sets are small (57 samples for Breast Cancer, 18 for Wine), so the results change a bit between seeds.
- The three train/validation splits overlap, so they are not fully independent.
- I tested only one model (seed 42) on the test set, so the test result is just one result, not a proof.

---

## AI Use

I used AI tools during this project. Details are in [`AI_DISCLOSURE.md`](AI_DISCLOSURE.md).

---

## Links

- GitHub repository: https://github.com/ravzakoc8/machine_learning
- Video : https://youtu.be/FrsO97Y5hes?si=gWi1rqEIsBSngOL0