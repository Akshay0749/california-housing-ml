# ML Concepts Reference Sheet

## 1. RMSE — Root Mean Square Error
- Standard metric for Regression problems
- Formula: √( (1/n) × Σ(predicted - actual)² )
- Lower RMSE = better model
- Same unit as target (dollars, kg, etc.)
- Penalizes large errors heavily because of squaring

## 2. MAE — Mean Absolute Error
- Formula: (1/n) × Σ|predicted - actual|
- Use when data has many outliers
- Treats all errors equally unlike RMSE

## 3. Train Test Split
- Never evaluate model on training data
- Standard split: 80% train, 20% test
- Always split BEFORE exploration or cleaning

## 4. Cross Validation
- Splits data into k folds
- Trains k times on different folds
- More reliable than simple train/test split
- k=5 is standard in industry

## 5. Feature Scaling
- StandardScaler → (x - mean) / std → most cases --> sd = 1 and mean = 0
- MinMaxScaler → (x - min) / (max - min) → when 0-1 range needed
- Always scale AFTER train/test split — never before

## 6. sklearn Pipeline
- Chains steps: Scaling → Encoding → Model
- Prevents data leakage
- One .fit() does everything

## 7. Hyperparameter vs Parameter
- Parameter → learned automatically by .fit()
- Hyperparameter → set by YOU before training
- Example: n_neighbors in k-NN is hyperparameter

## 8. Overfitting vs Underfitting
- Train error low + Test error high = Overfitting
- Train error high + Test error high = Underfitting
- Train error low + Test error low = Perfect ✅

## 9. Syntax Rules I Struggled With
- plt.plot() → positional args only, NO x= y= keywords
- plt.scatter() → accepts x= y= keywords
- Prediction input → always fresh pd.DataFrame(), never from training df
- Dictionary key in pd.DataFrame() → must exactly match training column name
- After model.predict() → always .flatten() before plotting
- X → always capital (feature matrix)
- y → always lowercase (target vector)

## 10. Encoding Categorical Variables
- ML models cannot work with text
- ocean_proximity has 5 categories → needs encoding
- Two main types:
  - Label Encoding → assigns numbers 0,1,2,3,4
    - Problem: model thinks INLAND(2) > OCEAN(1) — wrong!
  - One Hot Encoding → creates separate 0/1 column per category
    - No false ordering — preferred for categories with no rank

## 11. Data Distribution Problems
- Capping → data artificially stopped at a value
  → model cannot predict beyond that cap
- Right Skew → most values crowded near zero
  → model gets biased towards small values
  → fix with log transformation
- Normal Distribution → ideal for ML
  → model gets equal exposure to all ranges   

## 12. Multicollinearity
- When two or more features are highly correlated
- They carry same information → confuses the model
- Detected using correlation heatmap
- Solution → combine them via feature engineering
- Example: total_rooms, total_bedrooms, 
  population, households all measure district size

  ## 13. Data Leakage
- Happens when test data influences training process
- Example: calculating mean on full dataset before splitting
  → mean includes test data → model has "seen" test data
- Prevention: ALWAYS split first, then clean
- Makes evaluation results unreliable/fake

## 14. Correct ML Project Sequence
1. EDA on full data
2. Train Test Split
3. EDA on train data only
4. Data Cleaning (via Pipeline)
5. Feature Engineering
6. Encoding
7. Feature Scaling
8. Build Pipeline
9. Train Model
10. Cross Validation
11. Hyperparameter Tuning
12. Final Test Set Evaluation (once!)
13. Save Model
