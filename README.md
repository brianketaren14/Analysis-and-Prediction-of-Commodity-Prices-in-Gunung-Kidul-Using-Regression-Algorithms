# Analysis and Prediction of Commodity Prices in Gunung Kidul Using Regression Algorithms

## Project Description
This project analyzes and predicts commodity prices in Gunung Kidul using several regression algorithms. The goal is to compare the performance of Decision Tree, Random Forest, and Linear Regression models for predicting prices based on production, stock, imports, exports, and household consumption data.

## Dataset
The data comes from monthly Excel files containing commodity information, production, stock, imports, exports, household consumption, non-household consumption, and price.

Source files:
- `data/prognosa-gk-januari-m3.xls`
- `data/prognosa-gk-februari-m3.xls`
- `data/prognosa-gk-maret-m3.xls`
- `data/prognosa-gk-april-m3.xls`
- `data/prognosa-gk-mei-m3.xls`
- `data/prognosa-gk-juni-m3.xlsx`
- `data/prognosa-gk-juli-m3.xls`
- `data/prognosa-gk-agustus-m3.xls`
- `data/prognosa-gk-september-m3.xls`
- `data/prognosa-gk-oktober-m3.xls`
- `data/prognosa-gk-november-m3.xls`
- `data/prognosa-gk-desember-m3.xls`

## Main Steps

### 1. Load Data
All Excel files are imported into a list `df` using `pandas.read_excel()`.

### 2. Preprocessing
- Remove extra header rows from certain files.
- Drop unnecessary columns such as `NO`, `KETERSEDIAAN  (TON)`, `TOTAL (TON)`, and `NERACA MINGGUAN (TON)`.
- Standardize column names across files for consistency.
- Combine all data into a single DataFrame `df_concat`.
- Normalize the `KOMODITAS` text by converting to lowercase and removing spaces.
- Correct inconsistent commodity name values.
- Remove the `kedelai` rows from the dataset.
- Remove duplicate rows.

### 3. Exploratory Data Analysis (EDA)
- Create boxplots to detect outliers in all numerical features.
- Create histograms to evaluate numerical distributions.
- Display correlations between numerical variables using a heatmap.
- Run ANOVA tests to understand the relationship between numerical variables and commodity categories.

### 4. Feature Engineering
- Define numeric features:
  - `PRODUKSI (TON)`
  - `STOK (TON)`
  - `IMPOR (TON)`
  - `EKSPOR (TON)`
  - `RUMAH TANGGA (TON)`
  - `NON RUMAH TANGGA (TON)`
- Use `RobustScaler` for scaling because the data contains many outliers.
- Fill missing values with `0` using `SimpleImputer`.
- Apply one-hot encoding to the categorical feature `KOMODITAS`.

### 5. Modeling
The models trained and compared are:
- Decision Tree Regressor
- Random Forest Regressor
- Linear Regression

Training process includes:
- Splitting data into `X` and `y` with the target `HARGA (RP)`.
- Splitting train/test sets with 20% of the data reserved for testing.
- Using `GridSearchCV` and `KFold` to find the best hyperparameters based on MAE.

### 6. Evaluation
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MAE</th>
      <th>MSE</th>
      <th>R2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>DT</th>
      <td>8461.302175</td>
      <td>2.899358e+08</td>
      <td>0.739133</td>
    </tr>
    <tr>
      <th>RF</th>
      <td>9220.851852</td>
      <td>3.166336e+08</td>
      <td>0.715112</td>
    </tr>
    <tr>
      <th>LR</th>
      <td>9312.410886</td>
      <td>2.991141e+08</td>
      <td>0.730875</td>
    </tr>
  </tbody>
</table>
</div>


## Key Findings
- Decision Tree appears to perform best in terms of the lowest error on this dataset.
- The `KOMODITAS` variable has a strong influence on price, as shown by feature importance analysis.
- Import and export variables also contribute to price prediction.

## How to Run
1. Open the notebook file `Analysis and Prediction of Commodity Prices in Gunung Kidul Using Regression Algorithms.ipynb`.
2. Run all cells in order.
3. Ensure the required Python dependencies are installed:
   - `pandas`
   - `numpy`
   - `matplotlib`
   - `seaborn`
   - `scikit-learn`
   - `scipy`

## Notes
- The dataset has different file formats between months, so preprocessing is needed to standardize columns and data structure.
- Significant outliers influenced the choice of scaler (`RobustScaler`).
- This analysis enhances understanding of the relationship between price and input variables, especially commodity and trade-related features.
