# Flight Price Prediction (PRCP-1025)

Machine learning project that predicts flight ticket prices from airline, route, travel date, timing, duration and number of stops, using Python and Scikit-learn, to help travelers plan their journeys.

## Business Problem
Flight ticket prices are hard to guess because fares change with the airline, route, travel date, departure and arrival time, duration and number of stops. This project analyzes a flight fare dataset and builds a regression model that estimates ticket prices, so customers can plan their journey and airlines can understand what drives fares.

## Project Tasks
1. Prepare a complete data analysis report on the given data.
2. Build a predictive model that estimates flight prices.
3. Compare multiple models and recommend a candidate for production.
4. Report the challenges faced and the techniques used.

## Dataset
- Flight fare data with these columns: Airline, Date_of_Journey, Source, Destination, Route, Dep_Time, Arrival_Time, Duration, Total_Stops, Additional_Info and Price
- Target: `Price` (a continuous value, so this is a regression problem)
- Rows: `<number of rows>`
- The data is not included in this repository. It is available from the course project source.

## Approach
1. **Data checks:** shape, data types, descriptive statistics, missing values and duplicates
2. **Target analysis:** price distribution, boxplot, and IQR outlier report
3. **EDA:** price by airline, source, destination, number of stops, additional info and journey month; duration vs price; correlation heatmap
4. **Feature engineering:**
   - `Date_of_Journey` into day, month, year and day of week
   - `Dep_Time` and `Arrival_Time` into minutes since midnight
   - `Duration` (text such as "2h 50m") into total minutes
   - `Total_Stops` (text) into a number of stops
5. **Preprocessing pipeline:** median imputation and scaling for numeric features; most-frequent imputation and one-hot encoding for categorical features
6. **Modeling:** 80/20 train/test split, compared 4 regression models and selected a candidate by R², with RMSE as the tie-breaker
7. **Error analysis:** actual vs predicted plots, residual distribution, and the largest errors

## Models Compared
Linear Regression, Random Forest Regressor, Gradient Boosting Regressor, Extra Trees Regressor

## Results
Results on the hold-out test set:

| Model | MAE | RMSE | R² |
|---|---|---|---|
| Linear Regression | `<value>` | `<value>` | `<value>` |
| Random Forest | `<value>` | `<value>` | `<value>` |
| Gradient Boosting | `<value>` | `<value>` | `<value>` |
| Extra Trees | `<value>` | `<value>` | `<value>` |

**Candidate model:** `<model name>`, selected for the highest R². MAE is the average difference between actual and predicted fare, and RMSE penalizes large errors more.

## Key Insights
- `<insight 1: for example, which airlines have the highest or lowest average fares>`
- `<insight 2: for example, how the number of stops relates to price>`
- `<insight 3: for example, journey month or duration patterns, or the top features from the feature importance chart>`

## Recommendations
1. Show customers an estimated fare rather than a guaranteed future ticket price.
2. Monitor the factors that drive fares: airline, source, destination, stops, journey timing and duration.
3. Retrain the model regularly as new fare data becomes available.
4. Add booking lead time, seat availability, demand and seasonality if that data can be collected.
5. Monitor MAE and RMSE after deployment, and watch for changes in the incoming data.

## Challenges and Techniques
| Challenge | Technique | Reason |
|---|---|---|
| Date stored as text | Extracted day, month, year and day of week | Turns the date into useful numeric features |
| Departure and arrival time stored as text | Converted to minutes | Makes time usable for models |
| Duration stored as text ("2h 50m") | Converted to total minutes | Creates a continuous numeric feature |
| Total stops stored as text | Converted to a number | Keeps the order of the number of stops |
| Categorical variables | One-hot encoding | Converts categories to numbers |
| Missing values | Median and most-frequent imputation | Keeps rows and avoids data loss |
| Different numeric scales | StandardScaler | Stops large-scale features from dominating |
| High-cardinality Route | Removed from the baseline model | Source and Destination already capture most of the route information |
| Different model behavior | Compared four regression models | Objective model comparison |
| Large prediction errors | MAE, RMSE and residual analysis | Shows both average and large errors |

## Limitations
- Historical data cannot capture every future market event such as demand changes, promotions or fuel costs.
- A single train/test split gives only one estimate; cross-validation would make the results more reliable.
- The model gives estimated fares, not guaranteed prices.

## Tech Stack
Python, Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, Jupyter Notebook

## How to Run
1. Clone the repository.
2. Install the requirements: `pip install -r requirements.txt`
3. Download the dataset from the course project source and place it beside the notebook or in a folder named `Data`. The notebook finds the file automatically.
4. Run `PRCP-1025-FlightPricePrediction.ipynb` from top to bottom.
