# NYC Taxi Demand Prediction & Big Data Analytics

An end-to-end big data analytics and machine learning project using January 2025 NYC Yellow Taxi trip records. The project uses PySpark and Spark SQL to process millions of trips, analyze temporal and geographic demand patterns, and predict zone-level hourly taxi demand.

## Project Highlights

- Processed 3,475,226 raw trip records and retained 3,241,808 cleaned trips.
- Analyzed approximately $87.68 million in trip revenue.
- Identified 18:00 as the peak pickup hour with 235,843 trips.
- Found Thursday to have the highest weekday trip volume with 569,851 trips.
- Midtown Center, Manhattan recorded the highest pickup volume with 160,976 trips.
- JFK Airport, Queens generated the highest pickup revenue.
- Built a zone-level hourly demand dataset with 90,797 modeling observations.
- Compared Linear Regression and Random Forest using a time-based train/test split.
- Random Forest achieved RMSE 21.23, MAE 8.33, and R² 0.9194 on the held-out final week of January.
- Recent observed demand was the strongest predictive signal; `lag_1_demand` accounted for 48.94% of Random Forest feature importance.

## Business Questions

The analysis focuses on:

- When does taxi demand peak throughout the day and week?
- Which taxi zones generate the highest trip demand?
- How does demand differ between weekdays and weekends?
- How does pickup demand vary across days and hours?
- Which locations generate the most pickup revenue?
- Can recent trip patterns be used to predict hourly taxi demand?
- Which features contribute most to the demand model?

## Workflow

The notebook covers environment setup, data ingestion, data-quality checks, cleaning, Spark SQL analysis, visualization, feature engineering, machine learning, model evaluation, geographic analysis, and final business takeaways.

## Modeling Approach

Trips were aggregated by pickup date, pickup hour, and pickup location. Calendar variables and previous observed zone-level demand values were used as model features.

A time-based split was used instead of a random split. Observations before January 25 were used for training, while the final week of January was held out for testing.

| Model | RMSE | MAE | R² |
|---|---:|---:|---:|
| Linear Regression | 23.23 | 10.51 | 0.9035 |
| Random Forest | 21.23 | 8.33 | 0.9194 |

Random Forest produced the stronger test performance, improving RMSE by 8.61% and MAE by 20.69% compared with Linear Regression.

## Key Findings

Taxi demand was concentrated in the afternoon and evening, with the largest hourly volume at 18:00. Manhattan dominated overall pickup activity, while Midtown Center was the busiest individual pickup zone. JFK Airport generated the highest pickup revenue, showing that the location with the most trips was not necessarily the location generating the most revenue.

Prediction error increased for high-demand observations. The model's MAE was 2.29 trips for low-demand observations, 14.48 for medium-demand observations, and 36.34 for high-demand observations.

## Technologies

- Python
- PySpark
- Spark SQL
- Pandas
- NumPy
- Matplotlib
- Spark MLlib
- Google Colab

## Repository Structure

```text
nyc-taxi-demand-big-data-analytics/
├── notebooks/
│   └── nyc_taxi_demand_big_data_analytics.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Data Source

The notebook downloads the January 2025 NYC Yellow Taxi Trip Records and taxi-zone lookup data from the NYC Taxi & Limousine Commission. The raw trip dataset is not stored in this repository.

## Limitations

The project uses January 2025 Yellow Taxi data, and model performance is evaluated on the final week of that month. The reported metrics should therefore be interpreted within that dataset and test period.

Lag variables represent previous observed records within each pickup zone rather than a fully completed continuous hourly time series. Future work could build a complete zone-hour panel and incorporate additional months, weather, holidays, events, and traffic conditions.

## Author

Gracious Regina Zigara  
M.S. Data Science, Stevens Institute of Technology
