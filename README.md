# README: Mobile Phone Activity Data Analysis
## Github: https://github.com/Kachiengineers/Mobile-Big-Data-Assignment-1/
## Overview of Approach

The primary objective of this analysis was to load, clean, and explore a dataset composed of mobile phone activity (SMS, calls, internet usage) aggregated across geographical grid cells in Milan, Italy. The analysis involved combining data from multiple days, handling missing values, extracting temporal features, and performing various statistical comparisons to understand usage patterns.

### Steps Taken:
1.  **Data Loading and Merging**: Three daily CSV files (`sms-call-internet-mi-2013-11-02.csv`, `sms-call-internet-mi-2013-11-04.csv`, `sms-call-internet-mi-2013-11-06.csv`) were loaded and vertically concatenated into a single, comprehensive DataFrame.
2.  **Data Cleaning and Preparation**: The merged dataset was prepared for analysis by converting the 'datetime' column to a proper datetime object, extracting 'date' and 'time' components, and handling missing numerical values.
3.  **Feature Engineering**: Aggregate columns for 'total sms' (sum of incoming and outgoing SMS) and 'total calls' (sum of incoming and outgoing calls) were created.
4.  **Descriptive Statistics**: Basic exploratory data analysis was performed to understand the dataset's shape, column types, and statistical summaries of numerical features.
5.  **Query Answering**: Specific questions were addressed, including counts of records, unique CellIDs, and country codes.
6.  **Hourly Activity Analysis**: Overall activity was analyzed on an hourly basis to identify peak and lowest activity periods, and detailed statistics for total calls per hour were computed.
7.  **Daytime vs. Nighttime Activity**: Activity was segmented into daytime (6 am - 8 pm) and nighttime (8 pm - 6 am) to calculate the percentage of total activity occurring in each period.
8.  **Domestic vs. International Call Comparison**: Calls were categorized as 'Domestic' (countrycode 39) or 'International' (all other countrycodes) to compare their hourly patterns, distribution, and incoming/outgoing ratios.
9.  **Correlation Analysis**: The correlation between SMS volume and Call volume at the grid level was calculated and visualized.

## Key Decisions Made

1.  **Missing Value Imputation**: Given the substantial number of missing values across activity-related columns (`smsin`, `smsout`, `callin`, `callout`, `internet`), the decision was made to impute these `NaN` values with the *mean* of their respective columns. This approach was chosen to retain as much data as possible, despite the high proportion of missing data, ensuring that statistical analyses could be performed without excluding a large number of records. This impacted 5,880,441 rows.

2.  **Date and Time Extraction**: The 'datetime' column was explicitly converted to `datetime` objects. Subsequently, 'date' and 'time' columns were extracted, along with a crucial 'hour' column. This `hour` column was fundamental for all time-based aggregations and pattern analyses.

3.  **Activity Aggregation**: New columns, 'total sms' and 'total calls', were created by summing their incoming and outgoing components. This simplified the overall activity measurement for SMS and calls, making it easier to analyze general communication volumes.

4.  **Domestic/International Call Classification**: Italy's country code (39) was used as the sole criterion to distinguish 'Domestic' from 'International' calls. This clear-cut classification was vital for comparing communication patterns originating within and outside Italy.

5.  **Visualization Choices**: Line plots were primarily used for displaying hourly trends (overall activity, domestic vs. international calls) due to their effectiveness in showing temporal patterns. Scatter plots were employed for correlation analysis (SMS vs. Call volume) to visually represent the relationship between two continuous variables.

## Summary of Key Findings

### Dataset Overview:
*   **Total Records**: The combined dataset contains **6,564,031** records.
*   **Unique Grid Squares (CellID)**: There are **10,000** unique geographical grid squares represented in the data.
*   **Unique Country Codes**: The dataset includes activities related to **302** unique country codes.

### Missing Values:
*   Initial analysis revealed significant missing data: 'smsout' (5,025,738), 'callin' (4,761,685), 'smsin' (3,964,171), 'internet' (3,621,117), and 'callout' (3,764,484).
*   The 'smsout' column had the most missing values.
*   A total of **5,880,441** records had at least one missing value across these activity columns.
*   All missing values were successfully imputed with the mean of their respective columns, resulting in zero missing values post-imputation.

### Hourly Activity Patterns:
*   **Overall Peak Activity Hour**: The most common peak hour across all grids for total activity (SMS, calls, internet combined) is **17:00 (5 PM)**.
*   **Overall Lowest Activity Hour**: The hour with the lowest total activity is **04:00 (4 AM)**.
*   **Descriptive Statistics for Total Calls by Hour**: Showed high variability, with maximum values significantly exceeding means and medians in certain hours, indicating occasional extreme activity spikes.

### Daytime vs. Nighttime Activity:
*   **Daytime Activity (6 AM - 8 PM)**: Accounts for **78.51%** of the total activity.
*   **Nighttime Activity (8 PM - 6 AM)**: Accounts for **21.49%** of the total activity.

### Domestic vs. International Communication:
*   **Hourly Patterns**: International calls exhibit a flatter distribution throughout the day with a peak around **12:00**, maintaining relatively higher activity during hours when domestic calls are low. Domestic calls show a more pronounced diurnal pattern, peaking around **17:00** and significantly dropping during early morning hours.
*   **Call Type Distribution**:
    *   Domestic Calls: **33.11%** of total calls.
    *   International Calls: **66.89%** of total calls.
*   **SMS Type Distribution**:
    *   Domestic SMS: **24.98%** of total SMS.
    *   International SMS: **75.02%** of total SMS.
*   **International Calls Incoming vs. Outgoing**: The ratio of International Incoming Calls to Outgoing Calls is **1.67**, indicating that incoming international calls are more frequent than outgoing international calls.

### Correlation between SMS and Call Volume:
*   There is a **strong positive correlation (0.98624)** between SMS volume and Call volume at the grid level. This suggests that grid squares with higher SMS activity also tend to have higher call activity, indicating a general intensity of communication in those areas.
