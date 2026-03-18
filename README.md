# Paris Hotel Ratings Analysis

> **Note:** This project is an assignment submission for the Data Analysis 2 course at Central European University (CEU).

This project studies the determinants of high user ratings among Paris hotels using data from the hotels-europe dataset. It combines descriptive visualisations with binary outcome regression models to estimate:

- **Descriptive associations** — how distance to the city centre and star classification relate to high ratings
- **Regression models** — linear probability, logit, and probit models with marginal effects

---

## Project Overview

The analysis focuses on three core questions:

1. Are highly rated hotels more centrally located and higher starred than lower-rated hotels?
2. How do distance and star classification jointly predict the probability of a high rating?
3. Do logit and probit models confirm the linear probability model results?

---

## Repository Structure

```text
paris-hotel-ratings-analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── hotels-europe_features.csv
│   └── hotels-europe_price.csv
├── notebooks/
│   └── paris-hotel-ratings-analysis.ipynb
├── outputs/
│   ├── boxplot_distance_rating.png
│   ├── binscatter_distance.png
│   ├── boxplot_stars_rating.png
│   ├── scatter_stars_highly_rated.png
│   └── predicted_probabilities_logit.png
└── report/
    └── report.md
```

---

## Data

The raw datasets are sourced from the Hotels Europe project. In the notebook, I load the data directly from OSF to make the analysis easy to reproduce.

- **Dataset:** Hotels Europe — features and price files
- **Source:** https://osf.io/
- **Features file:** `hotels-europe_features.csv`
- **Prices file:** `hotels-europe_price.csv`

I also keep a local copy of the CSVs under `data/` for convenience.

---

## Methods

The notebook in `notebooks/paris-hotel-ratings-analysis.ipynb` covers:

- Data loading, merging, and cleaning
- Filtering prices to a baseline booking condition (one night, weekday, non-holiday)
- City selection: Paris (N > 250 hotels after filtering)
- Dropping missing values in rating, stars, and distance
- Binary outcome construction: highly rated = 1 if average rating >= 4
- Descriptive statistics and bin-scatter plots by distance and star level
- Linear probability model (OLS) with HC1 robust standard errors
- Logit and probit models with marginal effects at the mean
- Predicted probability plot across distance and star categories

---

## Key Findings

- In the Paris sample (N = 1,440), about **53%** of hotels are classified as highly rated.
- Hotels closer to the city centre are more likely to be highly rated. Each additional kilometre reduces the predicted probability by about **3.4 percentage points** (logit marginal effect).
- Each additional star increases the predicted probability by about **41.4 percentage points**, making star classification the stronger predictor.
- Results are consistent across the linear probability, logit, and probit models.
- Predicted probabilities show that 5-star hotels remain highly likely to be highly rated even at greater distances, while 3-star hotels drop off sharply.

---

## Key Outputs

All figures are saved in `outputs/`:

| File | Description |
|---|---|
| `boxplot_distance_rating.png` | Distance distribution by rating status |
| `binscatter_distance.png` | Share of highly rated hotels by distance bin |
| `boxplot_stars_rating.png` | Star distribution by rating status |
| `scatter_stars_highly_rated.png` | Share of highly rated hotels by star level |
| `predicted_probabilities_logit.png` | Predicted probability by distance and stars (logit) |

---

## How to Reproduce

### 1. Clone the repository

```zsh
git clone https://github.com/zarizachow/paris-hotel-ratings-analysis.git
cd paris-hotel-ratings-analysis
```

### 2. Set up the environment

```zsh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Run the notebook

Open and run all cells in `notebooks/paris-hotel-ratings-analysis.ipynb`. Plots will be saved to `outputs/` automatically.

---

## Report

A written summary of the analysis, including regression tables and interpretations, is available at `report/report.md`.

---

## Limitations

- Results are observational and not causal.
- Unobserved factors such as service quality, amenities, and hotel age are not controlled for.
- Star classifications are formally assigned and may not fully reflect actual quality as perceived by guests.

---

## Future Improvements

- Add price as an additional explanatory variable
- Extend the analysis to multiple cities for comparison
- Explore non-linear distance effects using polynomial or spline terms

---

## Tools

- Python, pandas, NumPy
- statsmodels (OLS with HC1 robust standard errors, logit, probit)
- matplotlib, seaborn

---

## License

See `LICENSE`.