# CAHOOTS Call Volume & Weather Analysis

## Overview
This project explores whether extreme weather conditions affect daily CAHOOTS call volume in the Eugene Oregon area.

## Data Sources
- **CAD data**: Five CSV files of call/response records, filtered to CAHOOTS calls only  
- **Weather data**: Two CSV files of daily weather summaries for the same region

## Libraries Needed
pandas, matplotlib.pyplot, and scipy.stats

## Data Cleaning Steps
1. **Load & concatenate** all CAD CSVs into one DataFrame  
2. **Filter** to only rows where `service == 'CAHOOTS'`  
3. **Extract date** from the full timestamp and **count calls per day** → `date` + `call_volume`  
4. **Load & concatenate** both weather CSVs  
5. **Convert** weather `datetime` to a simple `date` field  
6. **Merge** call-volume and weather DataFrames on `date`  
7. **Define “extreme” days** using thresholds:  
   - High temp > 97 °F  
   - Low temp < 25 °F  
   - Wind > 25 mph  
   - Rain > 1 in  
   - Snow > 1 in  
8. **Split** the merged data into `extreme_days` and `non_extreme_days`  
9. **Drop** unneeded columns (e.g., source, dew, humidity, wind direction, solar, UV, etc.)  
10. **Save** both subsets to CSV files:  
    - `extreme_days.csv`  
    - `non_extreme_days.csv`

## Analysis Steps
- **Descriptive statistics**: computed mean call volume for each individual weather condition, plus overall extreme vs. non-extreme  
- **T-tests**: tested whether mean call volume differs on  
  - each condition vs. all other days  
  - all extreme days vs. non-extreme days  
- **Visualizations**:  
  - Box plots comparing call volumes on extreme vs. non-extreme days  
  - Bar chart of mean call volume by condition  
- **Correlation**: generated a heatmap of Pearson correlations between call volume and key weather variables (`tempmax`, `tempmin`, `windspeed`, `precip`, `snow`)

## Key Findings
- Only **Very Hot Days (>97 °F)** showed a significant increase in call volume (t=3.5, p=0.002)  
- Other conditions (cold, wind, rain, snow) did not reach statistical significance  
- Overall extreme vs. non-extreme comparison was not significant when lumped together

## Files in This Repo
- `class_data_2021.csv` … `class_data_2025.csv` — raw CAD files  
- `Eugene Oregon 2023... .csv`, `Eugene, OR, United States... .csv` — raw weather files  
- `data_cleaning.ipynb` — cleaning code
- `analysis.ipynb` — analysis code
- `extreme_days.csv` — filtered extreme-weather days  
- `non_extreme_days.csv` — filtered non-extreme days
- `merged.csv` — cleaned and merged data (pre-extremes split)
- `README.md` — this overview

## How to Run
1. Clone this repo and run the data_cleaning.ipynb in the 'Data Cleaning' Folder  
2. Move the files generated -merged.csv, extreme_days.csv, non_extreme_days.csv from data_cleaning.ipynb to the 'Analysis' folder
2. Run analysis.ipynb 
 