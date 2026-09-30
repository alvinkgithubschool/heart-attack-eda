# Heart Attack Dataset — Exploratory Data Analysis

**Strathmore University — School of Computing and Engineering Sciences (SCES)**

A short exploratory data analysis of the `Heart Attack.csv` dataset: 1,319 patient records with
vitals and cardiac blood-test markers, labelled `positive` / `negative` for heart-attack risk.
The notebook was executed on Google Colab via the official
[`google-colab-cli`](https://github.com/googlecolab/google-colab-cli), so all outputs and figures
are embedded and visible without re-running anything.

## Structure

```
├── heart_attack_exploration.ipynb   # The EDA notebook (executed on Colab, outputs embedded)
├── Heart Attack.csv                # The dataset (1,319 rows x 9 columns)
└── README.md
```

## Columns

| Column | Meaning |
|---|---|
| `age` | Patient age (14-103) |
| `gender` | Encoded 0/1 (undocumented which is which) |
| `impluse` | Pulse rate (sic — column name typo in the source data) |
| `pressurehight` / `pressurelow` | Systolic / diastolic blood pressure |
| `glucose` | Blood glucose (mg/dL) |
| `kcm` | Creatine kinase-MB (cardiac enzyme) |
| `troponin` | Troponin level (cardiac marker) |
| `class` | Heart-attack risk label: `positive` (810) / `negative` (509) |

## Key findings

1. **Clean data:** no missing values, no duplicate rows.
2. **Moderate class imbalance:** 61% positive / 39% negative — accuracy will be misleading;
   use precision/recall/AUC when modelling.
3. **Outliers:** pulse reaches 1,111 bpm — physiologically impossible values (>200 bpm) that
   look like data-entry errors and should be capped or removed before modelling.
4. **Class separation:** the cardiac markers `kcm` and `troponin` separate the classes most
   clearly (mean kcm: 23.3 positive vs 2.6 negative) and are heavily right-skewed — a log
   transform helps. `age` also shifts upward for positive cases; blood pressure and pulse
   overlap almost completely and carry little signal.
5. **Correlations** between features are mostly weak (systolic/diastolic pressure the
   strongest, as expected) — no problematic redundancy.

## How to run

Open `heart_attack_exploration.ipynb` in [Google Colab](https://colab.research.google.com)
(*File → Upload notebook*), upload `Heart Attack.csv` next to it (or to `/content`), and
*Runtime → Run all*. Only `numpy`, `pandas` and `matplotlib` are needed, all pre-installed
in Colab.
