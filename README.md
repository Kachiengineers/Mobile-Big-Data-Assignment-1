📊 Overview
This project analyzes mobile phone activity data (SMS, calls, and internet usage) aggregated across geographical grid cells in Milan, Italy. The dataset spans multiple days and provides insights into communication patterns, temporal trends, and geographical variations.

🎯 Objectives
Load, clean, and merge multiple daily datasets

Analyze temporal patterns in communication activity

Compare domestic vs. international communication patterns

Investigate correlations between different types of mobile activities

Identify peak usage periods and geographical patterns

📁 Dataset Description
Source: Daily CSV files containing mobile phone activity data for Milan
Files Used:

sms-call-internet-mi-2013-11-02.csv

sms-call-internet-mi-2013-11-04.csv

sms-call-internet-mi-2013-11-06.csv

Key Columns:

CellID: Geographical grid square identifier (10,000 unique squares)

datetime: Timestamp of activity

smsin, smsout: Incoming and outgoing SMS counts

callin, callout: Incoming and outgoing call durations

internet: Internet traffic volume

countrycode: Originating/destination country code

🔧 Methodology
1. Data Loading and Merging
Loaded three daily CSV files

Vertically concatenated into a single DataFrame

Final dataset size: 6,564,031 records

2. Data Cleaning and Preparation
python
# Key transformations:
- Converted 'datetime' column to datetime objects
- Extracted 'date', 'time', and 'hour' components
- Created aggregate columns: 'total_sms' and 'total_calls'
3. Missing Value Handling
Challenge: Significant missing values across activity columns:

smsout: 5,025,738 missing

callin: 4,761,685 missing

smsin: 3,964,171 missing

internet: 3,621,117 missing

callout: 3,764,484 missing

Solution: Imputed all missing values with column means (affecting 5,880,441 records)

4. Feature Engineering
Created total_sms = smsin + smsout

Created total_calls = callin + callout

Added activity_type classification (Domestic/International)

Added time_period classification (Daytime/Nighttime)

📈 Key Findings
📊 Dataset Statistics
Total Records: 6,564,031

Unique Grid Squares (CellID): 10,000

Unique Country Codes: 302

Missing Values (pre-imputation): 5,880,441 records with at least one missing value

⏰ Temporal Patterns
Metric	Finding
Peak Activity Hour	17:00 (5 PM)
Lowest Activity Hour	04:00 (4 AM)
Daytime Activity (6 AM - 8 PM)	78.51% of total activity
Nighttime Activity (8 PM - 6 AM)	21.49% of total activity
🌍 Domestic vs. International Patterns
Call Distribution
Type	Percentage	Pattern
Domestic Calls	33.11%	Pronounced diurnal pattern, peaks at 17:00
International Calls	66.89%	Flatter distribution, peaks at 12:00
SMS Distribution
Type	Percentage
Domestic SMS	24.98%
International SMS	75.02%
International Call Direction
Incoming/Outgoing Ratio: 1.67

Interpretation: Incoming international calls are 67% more frequent than outgoing international calls

🔗 Correlation Analysis
SMS vs. Call Volume Correlation: 0.98624 (strong positive)

Interpretation: Grid squares with high SMS activity also tend to have high call activity, indicating general communication intensity in certain areas

📊 Visualizations Created
Hourly Activity Trends - Line plots showing overall activity patterns

Domestic vs. International Hourly Patterns - Comparative line plots

SMS vs. Call Volume Correlation - Scatter plot with regression line

Activity Distribution by Time Period - Bar charts

🧠 Key Insights
Evening Peak: Communication peaks around 5 PM, aligning with end of workday

International Dominance: International communications significantly outweigh domestic ones

Geographical Consistency: High correlation between SMS and call volumes suggests consistent communication hotspots

Nighttime Quiet: Minimal activity between 2 AM - 5 AM

Call Direction Imbalance: More incoming than outgoing international calls

🛠️ Technical Stack
Python Libraries: pandas, numpy, matplotlib, seaborn

Data Processing: Data merging, cleaning, imputation, feature engineering

Analysis Techniques: Descriptive statistics, correlation analysis, time series analysis, comparative analysis

📝 Project Structure
text
project/
│
├── data/                    # Raw data files
├── notebooks/               # Jupyter notebooks for analysis
├── scripts/                 # Python scripts for processing
├── results/                 # Output files and visualizations
├── README.md               # This file
└── requirements.txt        # Dependencies
🚀 Getting Started
bash
# Clone repository
git clone <repository-url>

# Install dependencies
pip install -r requirements.txt

# Run analysis
python scripts/analyze_mobile_activity.py
🔍 Future Work
Incorporate more days for longitudinal analysis

Add weather data to explore environmental impacts

Implement machine learning for activity prediction

Analyze spatial patterns using geographical visualization

Investigate weekend vs. weekday patterns
