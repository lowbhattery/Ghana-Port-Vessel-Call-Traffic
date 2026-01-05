📊 Tema Port Vessel Calls Prediction

Author: Nana Akwasi Adjei Odoom
Date: January 2026
Project Type: Predictive Analytics / Time-Series Forecasting
Programming Language: Python
Libraries: pandas, scikit-learn

## 📄 Data Disclaimer

The dataset used in this project was obtained from publicly available online sources.
While every effort was made to ensure accuracy and consistency, minor discrepancies may exist due to reporting methods and data aggregation across different years.


📑 Table of Contents

Project Overview

Dataset

Data Cleaning

Exploratory Data Analysis

Predictive Modeling

Results

Conclusion

Future Work

Usage Instructions

License

📌 Project Overview

This project focuses on predicting annual vessel traffic at Tema Port, Ghana, using historical vessel call data from 2000 to 2024.

The main objectives are to:

Analyze historical trends in vessel calls

Predict future vessel traffic (2025–2030)

Provide data-driven insights to support port planning and management decisions

📂 Dataset

Source:
Publicly available online data from the Ghana Ports and Harbours Authority (GPHA) and related maritime traffic publications.
The dataset represents real historical annual vessel call records for Tema Port and was compiled from official online sources for analytical and academic purposes.

Columns:

id → Unique identifier (not used for modeling)

Year → Independent variable

Calls → Dependent variable (number of vessel calls)

Sample Data:

id	Year	Calls
1	2000	1163
2	2001	1169
3	2002	1170
…	…	…
🧹 Data Cleaning

The following steps were applied to ensure data quality:

Converted Year and Calls to numeric data types

Interpolated missing values in Calls to preserve the trend

Removed invalid or non-finite Year values

Rounded Calls to integers for consistency

import pandas as pd
import numpy as np

df = pd.read_csv("tema_port.csv").copy()

df['YEAR'] = pd.to_numeric(df['YEAR'], errors='coerce')
df = df.dropna(subset=['YEAR'])
df['YEAR'] = df['YEAR'].astype(int)

df['Calls'] = pd.to_numeric(df['Calls'], errors='coerce')
df['Calls'] = df['Calls'].interpolate().round().astype(int)

📊 Exploratory Data Analysis (EDA)

Key observations from the data:

Vessel calls show a gradual upward trend over time

No strong seasonality is observed due to annual aggregation

Traffic growth appears largely influenced by long-term port activity expansion

🤖 Predictive Modeling

A Linear Regression model was used to predict future vessel calls based on historical trends.

from sklearn.linear_model import LinearRegression

X = df[['YEAR']]
y = df['Calls']

model = LinearRegression()
model.fit(X, y)

future_years = pd.DataFrame({'YEAR': range(2025, 2031)})
future_calls = model.predict(future_years).round().astype(int)

future_years['Predicted_Calls'] = future_calls

📈 Results

Linear Regression Predictions (2025–2030):

Year	Predicted Calls
2025             1756
2026             1771
2027             1787
2028             1803
2029             1818
2030             1834



✅ Conclusion

Linear regression effectively captured the long-term trend in vessel traffic

The model provides a reliable baseline forecast for future vessel calls

Results can assist in port capacity planning and infrastructure development

