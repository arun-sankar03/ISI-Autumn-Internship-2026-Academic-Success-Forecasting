# ISI-Autumn-Internship-2026-Academic-Success-Forecasting

Predicting student grades and finding students who may need extra help, using machine learning in Python.

This project was done for the **IDEAS (Institute of Data Engineering, Analytics and Science Foundation) Autumn Internship Program 2026**, ISI Kolkata.

- **Author:** Arun Sankar E K, MSc Mathematics, University of Delhi
- **Mentor:** Dr. Chandan Biswas
- **Internship period:** 21 September 2026 to 16 October 2026

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1ra6gowPh4j4BiVaPt2S8e3cZlWRTxGS0?usp=sharing)

---

## What is this project about?

Schools can only help struggling students if they notice them early. This project uses information about 395 students (family background, study habits, lifestyle and past grades) to answer three questions:

1. Which things are most linked to a student's final performance?
2. What kinds of students are there, and which group is at risk?
3. How well can a model predict a student's total grade?

## The data

- **File:** `student-mat.csv` (395 students, 33 columns), loaded directly from this link, so you do not need to download anything:
  [student-mat.csv](https://raw.githubusercontent.com/guipsamora/pandas_exercises/master/04_Apply/Students_Alcohol_Consumption/student-mat.csv)
- The three grade columns (G1, G2, G3) were added into one target called `Total_Grade`. The original three were then removed so the model cannot "cheat".
- There were no duplicate or missing rows.

## What I did (step by step)

1. Loaded and cleaned the data.
2. Created the target `Total_Grade = G1 + G2 + G3`.
3. Made a correlation heatmap to see which features matter most.
4. Converted text columns to numbers (one-hot encoding) and scaled all features.
5. Used PCA to shrink the data to 2 dimensions.
6. Used K-Means (with the elbow method) to group students into 3 segments.
7. Split the data 80% for training and 20% for testing.
8. Trained a baseline Linear Regression and a neural network (MLP Regressor).
9. Tuned the neural network with Grid Search and 3-fold cross-validation.
10. Compared the models and wrote a recommendation.

## Main results

**What is linked to grades**

- Past class failures have the strongest link (correlation about -0.38): more failures, lower grades.
- Mother's education is next (about +0.22): higher education, higher grades.
- Absences show almost no straight-line link with grades.

**Three student groups**

| Group | Students | Average grade | Study time (1 to 4) | Absences | Profile |
| --- | --- | --- | --- | --- | --- |
| 0 | 142 | 35.68 | 2.05 | 5.58 | High achievers |
| 1 | 182 | 31.04 | 2.24 | 5.45 | Hardworking average students |
| 2 | 71 | 27.32 | 1.48 | 6.63 | At-risk students |

**Model comparison (on the 79 test students)**

| Model | RMSE (grade points) | R² |
| --- | --- | --- |
| Linear Regression (baseline) | 10.12 | 0.23 |
| MLP Regressor (tuned: 32 neurons, alpha 1.0) | 10.68 | 0.14 |

The simple Linear Regression did better than the tuned neural network. With only 395 students, a simple model works better than a complex one.

**Recommendation:** run an early-warning tutoring program. Flag students with past failures or low study time at the start of each term and give them tutoring and study-skills support.

## Things to keep in mind

- PCA keeps only about 15% of the information, so the student groups are a rough picture.
- The elbow curve bends gradually, and 3 groups were used as the task asked.
- Results come from one train/test split of 79 students and can change with a different split.
- These are patterns in the data, not proof of cause and effect.

## Repository contents

```
.
├── README.md
├── requirements.txt
├── notebook/
│   └── Project_7_Academic_Success_Forecasting.ipynb
└── report/
    ├── Project_Report_Academic_Success_Forecasting.docx
    └── Project_Report_Academic_Success_Forecasting.pdf
```

| File | What it is |
| --- | --- |
| `notebook/Project_7_Academic_Success_Forecasting.ipynb` | The full code and answers to all 15 questions |
| `report/` | The final project report (Word and PDF) |
| `requirements.txt` | Python libraries needed to run the notebook |

## How to run it

**Option 1: in the browser (easiest).** Click the "Open In Colab" button at the top and choose Runtime, then Run all.

**Option 2: on your computer.**

```bash
git clone <your-repository-link>
cd <repository-folder>
pip install -r requirements.txt
jupyter notebook notebook/Project_7_Academic_Success_Forecasting.ipynb
```

You need an internet connection, because the notebook downloads the data when it runs.

## Tools used

Python, pandas, NumPy, matplotlib, seaborn and scikit-learn.

## Links

- Colab notebook: https://colab.research.google.com/drive/1ra6gowPh4j4BiVaPt2S8e3cZlWRTxGS0?usp=sharing
- Demo video: [add link]
- Dataset reference: Cortez, P. and Silva, A. (2008). *Using Data Mining to Predict Secondary School Student Performance.* FUBUTEC 2008. https://archive.ics.uci.edu/dataset/320/student+performance
