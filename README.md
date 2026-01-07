📸 Instagram Analytics & Power BI Pipeline

Welcome to the Instagram Analytics Data Pipeline! This project transforms raw social media exports into high-impact, BI-ready datasets. By using advanced Python cleaning techniques within Quadratic (AI-powered spreadsheet), we've turned messy engagement metrics into clear, actionable insights for Power BI.

🚀 The Mission

To decode the "Algorithm" by analyzing 30,000+ posts. We focus on:

Identifying peak performance times (Months, Days, Hours).

Correcting statistical anomalies (Outlier management).

Engineering new metrics (Reach Efficiency & Total Interactions).

Segmenting content strategy (Hashtag and Caption analysis).

🛠️ The Tech Stack

Data Source: Instagram_Analytics.csv

Cleaning Engine: Quadratic AI (Python-powered Spreadsheets)

Visualization: Microsoft Power BI

Logic: Python (Pandas/NumPy)

📊 Data Transformation Workflow

1. Temporal Intelligence

We converted the raw upload_date into categorical features. This allows Power BI to slice data by season and week.

Month_Name: For Month-over-Month (MoM) growth analysis.

Day_of_Week: To find the "Best Day to Post."

Hour: To track audience activity windows.

2. The "Clean Engagement" Protocol

Raw data often contains outliers (e.g., 3000% engagement rates). We implemented a capping strategy:

Logic: Any engagement_rate > 100% is replaced with the Median for that specific media_type.

Result: Realistic averages that don't break your bar charts.

3. Metric Engineering

We added columns that do not exist in the raw export:

Total_Interactions: Likes + Comments + Shares + Saves.

Reach_Efficiency: Unique Reach / Total Impressions (Shows how "viral" a post is).

Hashtag_Range: Binned groups (0-5, 6-10, etc.) to see the impact of hashtag density.

📝 The Quadratic Master Script

To replicate this data cleaning, run this script in your Quadratic Python cell:

import pandas as pd
import numpy as np

# Load & Clean
df = pd.read_csv('Instagram_Analytics.csv')
df['upload_date'] = pd.to_datetime(df['upload_date'])
df['Month_Name'] = df['upload_date'].dt.month_name()
df['Day_of_Week'] = df['upload_date'].dt.day_name()

# Handle Outliers
medians = df.groupby('media_type')['engagement_rate'].transform('median')
df.loc[df['engagement_rate'] > 100, 'engagement_rate'] = medians

# Feature Engineering
df['Total_Interactions'] = df['likes'] + df['comments'] + df['shares'] + df['saves']
df['Reach_Efficiency'] = df['reach'] / df['impressions']
df['Hashtag_Range'] = pd.cut(df['hashtags_count'], bins=[0, 5, 10, 15, 20, 25, 31], labels=['0-5', '6-10', '11-15', '16-20', '21-25', '26-30'], include_lowest=True)

# Ready for Power BI
df


📈 Suggested Power BI Visuals

The Funnel: Impressions ➡️ Reach ➡️ Total Interactions.

Category Battle: A TreeMap showing which content_category (Technology, Beauty, etc.) wins the most saves.

Heatmap: Day_of_Week vs. Engagement_Rate to spot the "Golden Hour."

🔗 Useful Links

Tool: Quadratic Spreadsheet

Reference: Power BI Documentation

Community: Power BI Community Forums

Project Lead: Analytics Pro

Status: ✅ Data Cleaned | ✅ Features Engineered | 🚀 Ready for Visualization
