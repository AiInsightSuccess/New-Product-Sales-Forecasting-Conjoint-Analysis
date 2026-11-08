# New Product Sales Forecasting with Choice-Based Conjoint Analysis
[![DOI](https://zenodo.org/badge/1450193286.svg)](https://doi.org/10.5281/zenodo.24060423)

Free Python code and sample data from
[AI Insights for Success](https://www.aiinsightsuccess.com/blank-2-1).
This repository contains a beginner-friendly Jupyter notebook for product
forecasting with choice-based conjoint analysis: it designs the experiment,
fits the conjoint model, and predicts purchase probability for new product
scenarios.

## Get the Code

- **No Git?** Click the green **Code** button on this page, then
  **Download ZIP**, and unzip it.
- **Using Git:** `git clone https://github.com/AiInsightSuccess/New-Product-Sales-Forecasting-Conjoint-Analysis.git`

Python 3.10 or newer is required (current Anaconda installs meet this).

The sample data describes smartphone/product features:

- `Brand`
- `Price_$`
- `Screen_Size_inch`
- `Camera_Pixel_MP`
- `Storage_GB`
- `Folding`
- `Battery life_Up_to_Days`

## Files

- `Forecasting_CBC_Workbook.ipynb`: main notebook to run.
- `Feature_specs.csv`: product feature names, feature types, level counts, and
  optional minimum/maximum values.
- `Feature_template.csv`: actual levels for each product feature.
- `fractional_factorial_design.csv`: included 60-profile product design.
- `levels_used.csv`: levels used by the design and model.
- `Survey_response.csv`: sample participant responses linked to the included
  60-profile design.
- `Forecasting_Model_Spec.csv`: product scenario profiles (Nothing-brand
  phones in the sample) used for the scenario purchase-probability section. These can be new profile combinations
  that were not shown in the fractional factorial design.
- `requirements.txt`: Python packages used by the notebook.
- `outputs/`: folder where model results and graphs are saved (contains
  example results from the sample data).

## How to Run

1. Open Anaconda Navigator.
2. Launch Jupyter Notebook.
3. Open the unzipped repository folder.
4. Open `Forecasting_CBC_Workbook.ipynb`.
5. Run the notebook cells from top to bottom.

If a package is missing, open a terminal in this folder and run:

```bash
pip install -r requirements.txt
```

## Important Note About the Sample Data

The included `Survey_response.csv` refers to run IDs 1 through 60. Those run IDs
match the included `fractional_factorial_design.csv`.

For that reason, the notebook uses:

```python
REGENERATE_FRACTIONAL_DESIGN = False
```

Keep this setting for the sample package. Change it to `True` only when creating
a new design before collecting new survey responses.

## Main Outputs

After running the notebook, check the `outputs/` folder for:

- `conjoint_model_dataset.csv`
- `conjoint_model_metrics.csv`
- `conjoint_feature_significance.csv`
- `conjoint_coefficients.csv`
- `conjoint_best_combination.csv`
- `conjoint_optimum_combination_long.csv`
- `conjoint_coefficients_by_feature.png`
- `conjoint_feature_p_values.png`
- `conjoint_top_combinations.png`
- `nothing_brand_scenario_predictions.csv`
- `nothing_brand_scenario_level_mapping.csv`
- `nothing_brand_scenario_purchase_probability.png`

The scenario forecast scores every row in `Forecasting_Model_Spec.csv`. To
forecast only one brand's rows, set `SCENARIO_BRAND_FILTER` (for example
`"Nothing"`) at the top of the forecasting code in Cell 6.

The scenario forecast can score new product-profile combinations. For numeric
values that fall between the listed levels, the notebook interpolates between
the nearby learned level effects. Values outside the listed range use the nearest
listed level. Categorical values must use categories that exist in
`levels_used.csv`; otherwise the notebook stops with a message listing the
allowed categories.
