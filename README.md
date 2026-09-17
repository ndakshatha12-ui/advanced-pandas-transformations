# Advanced Pandas Transformations

## Project Overview

This project demonstrates practical and advanced Pandas transformations on an Online Retail dataset.

The notebook focuses on creating useful features, handling data values, using groupby transformations, working with dates, binning, custom functions, method chaining, and comparing different approaches for performance.

## Dataset

The project uses an Online Retail transactional dataset containing information such as:

- Invoice number
- Stock code
- Product description
- Quantity
- Invoice date
- Unit price
- Customer ID
- Country
- Revenue

## Transformations Performed

The notebook demonstrates the following transformations:

| Transformation | Method Used | Purpose |
|---|---|---|
| Region | `Series.map()` | Groups countries into regions |
| Description, Country | `replace()` | Standardises placeholder values |
| PriceBand | `Series.apply()` | Creates Budget, Standard, Premium and Luxury bands |
| OrderType | `apply(axis=1)` | Creates a row-wise order label |
| CustomerTotal | `groupby().transform()` | Calculates customer-level total spending |
| ShareOfCustomerSpend | `groupby().transform()` | Calculates each line's share of customer spending |
| RevenueZScoreInCountry | `transform()` | Standardises revenue within each country |
| RevenueTier | `np.select()` | Creates revenue-based tiers |
| IsWeekend | `np.where()` | Identifies weekend transactions |
| QuantityBucket | `pd.cut()` | Creates fixed quantity ranges |
| CustomerValueQuartile | `pd.qcut()` | Divides customers into spending quartiles |
| Year/Month/DayName/Hour | Custom function + `pipe()` | Extracts calendar features |
| Revenue_Capped | Custom function + `pipe()` | Caps extreme revenue values |
| Basket columns | Custom function + `transform()` | Adds invoice-level information to each row |
| LogRevenue and ranks | `assign()` chain | Creates log revenue and customer revenue rankings |
| FirstPurchaseDate | `groupby().transform("min")` | Finds each customer's first purchase date |
| DaysSinceFirstPurchase | Custom calculation | Calculates days from the customer's first purchase |

## Final Dataset

The transformed dataset contains:

- **397,884 rows**
- **35 columns**
- **27 newly created columns**

The final dataset includes original transaction information together with customer, revenue, date, basket and categorical features.

## Performance Comparison

Three approaches were compared for calculating the same result:

| Method | Time (seconds) | Speedup vs apply |
|---|---:|---:|
| `apply(axis=1)` | 2.899364 | 1.0× |
| List comprehension | 0.075867 | 38.2× |
| Vectorised Pandas operation | 0.000993 | 2920.1× |

The benchmark showed that vectorised Pandas operations were substantially faster than row-wise `apply(axis=1)` for the tested calculation.

## Key Concepts Learned

- `map()` for value mapping
- `apply()` for custom element-wise and row-wise logic
- `transform()` for group-level calculations while preserving the original DataFrame shape
- `groupby()` for customer-level analysis
- `pd.cut()` and `pd.qcut()` for creating categories
- `np.where()` and `np.select()` for conditional features
- Date and time feature extraction
- Method chaining with `assign()`
- Custom functions with `pipe()`
- Vectorisation and performance optimisation
- Creating reproducible data transformation pipelines

## Files

- `advanced_pandas_transformations.ipynb` — Complete Jupyter Notebook with transformations and outputs
- `transformed_sample.csv` — Sample of the transformed dataset

## Interview Preparation

The notebook also contains interview questions covering:

1. Difference between `apply()`, `map()`, and `transform()`
2. Why vectorised Pandas operations are generally preferred
3. Performance differences between row-wise and vectorised approaches
