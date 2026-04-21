# Project 4 – NRI Risk Analysis
### CIVE 202 – Civil Engineering Analysis II | Spring 2026
**Macy Dubes, Arturo Garcia, and Aminasahra Warsame**
**Instructors:** Dr. Wissam Kontar and Dr. Kaycie Lane

---

## Overview

This project analyzes and compares natural hazard risk across **Louisiana** and **Virginia** using data from FEMA's National Risk Index (NRI) and the CDC/ATSDR Social Vulnerability Index (SVI). We develop an alternative risk scoring method called **SPCHL (Socially-weighted Per-Capita Hazard Loss)** and compare it against the NRI's official risk definitions to identify potential bias in how risk is categorized across communities.
This work was completed for **Risk Averse, LLC**, an independent risk analysis consulting group.

---

## Repository Contents

* **`Garcia_Project4_Final.ipynb`**         # Main Python code file
* **`Garcia_Project4_ACD.xlsx`**         # Annotated Code Document
* **`NRI_Table_CensusTracts_Louisiana.csv`** # Raw NRI data – Louisiana
* **`NRI_Table_CensusTracts_Virginia.csv`**  # Raw NRI data – Virginia
* **`Louisiana.csv`**                        # Raw SVI data – Louisiana
* **`Virginia.csv`**                         # Raw SVI data – Virginia
* **`NRIDataDictionary.csv`**                # NRI variable definitions
* **`NRI_Shapefile_CensusTracts.shp`**       # NRI shapefile (+ companion files)
* **`Project4_Cleaned_Louisiana.csv`**       # Cleaned & scored output – Louisiana
* **`Project4_Cleaned_Virginia.csv`**        # Cleaned & scored output – Virginia


---

## Data Sources

| Dataset | Source | Link |
|---|---|---|
| NRI Census Tract Data | FEMA National Risk Index | https://hazards.fema.gov/nri/data-resources |
| NRI Data Dictionary | FEMA National Risk Index | https://hazards.fema.gov/nri/data-resources |
| NRI Shapefile | FEMA National Risk Index | https://hazards.fema.gov/nri/data-resources |
| SVI Census Tract Data | CDC/ATSDR Social Vulnerability Index | https://www.atsdr.cdc.gov/placeandhealth/svi/data_documentation_download.html |

---

## How to Run

### Requirements

Install the required Python packages before running the notebook:

```bash
pip install pandas numpy matplotlib seaborn geopandas
```

### Steps

1. Download this repository
2. Place all data files in the same folder as the notebook
3. Open `Garcia_Project4_Final.ipynb` in Jupyter Notebook
4. Run all cells!
5. 
---

## Our Alternative Risk Score: SPCHL

### NRI's Definition of Risk
> **Risk = Expected Annual Loss × Social Vulnerability ÷ Community Resilience**

The NRI produces a composite dollar-value loss estimate across all 18 hazard types, then converts it to a percentile score among all US census tracts.

### Our Definition: Socially-weighted Per-Capita Hazard Loss (SPCHL)

We define risk as a weighted combination of the three most relevant hazards for Louisiana and Virginia, normalized per person and amplified by social vulnerability:

| Step | Formula | Reason |
---
| 1. Hazard Risk | `AFREQ × EALB` per hazard | Frequency × Impact (same as NRI method) |
| 2. Weighted Combined | `0.40 × hurricane + 0.40 × flood + 0.20 × tornado` | Focuses on hazards most relevant to both states |
| 3. Per Capita | `combined_risk / (population + 1)` | Reveals risk to individuals, not just aggregate dollar loss |
| 4. SVI Amplifier | `risk_per_capita × (1 + RPL_THEMES)` | Communities with higher vulnerability face greater real-world impact |
| 5. Normalize | `(value - min) / (max - min) × 100` | Converts to 0–100 scale for direct comparison with NRI |

**Hazard Weights:**
- **Hurricane (40%)** – Primary catastrophic hazard for both states
- **Coastal Flooding (40%)** – High exposure in Louisiana; growing threat in Virginia
- **Tornado (20%)** – Secondary hazard present in both states

---

## Key Outputs

- **4 Summary Sables** comparing NRI and SPCHL scores at the state and county level
- **4 Bar Chart Figures** comparing risk score distributions by county
- **4 GeoPandas maps** — one per state per scoring method
- **2 cleaned CSV files** with all scores for Louisiana and Virginia

---

## References

- FEMA National Risk Index. (2025). *Understanding Scores and Ratings.* https://hazards.fema.gov/nri/understanding-scores-ratings
- CDC/ATSDR Social Vulnerability Index. (2022). *SVI Documentation.* https://www.atsdr.cdc.gov/placeandhealth/svi/documentation/SVI_documentation_2022.html
