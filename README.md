# Tracking-Global-Maritime-Pirate-Attacks-using-Geospatial-Analysis-in-R

# Global Maritime Pirate Attacks — Spatial Analysis & Shiny App

**Authors:** Haley Burdick & Elijah Manwill  
**Date:** April 18, 2025  
**Format:** R Markdown (`html_document`) with embedded Shiny application

---

## Overview

This project presents a spatial and temporal analysis of global maritime piracy incidents. It combines exploratory data visualization, spatial autocorrelation analysis, and an interactive Shiny web application to help understand the geographic patterns and socio-economic drivers of pirate attacks worldwide.

The three primary research questions driving the analysis are:
1. What are the spatial patterns of pirate attacks, and are there significant clusters?
2. How do socio-economic factors correlate with piracy incidents?
3. Can we develop a predictive model to identify high-risk areas?

---

## Data Sources

| Dataset | Description | Source |
|---|---|---|
| **ASAM** (Anti-Shipping Activity Messages) | Incident-level records including location, date, and attack type | U.S. Office of Naval Intelligence |
| **Global Maritime Pirate Attacks (1993–2020)** | Country-level indicators (GDP, corruption, crime) plus attack records | International Maritime Bureau |

### Expected File Structure

```
project/
├── Global_Maritime_Pirate_Attacks_code_shinyapp.Rmd
├── ASAM_shp.zip
└── data/
    ├── ASAM/
    │   └── ASAM.shp          # Extracted from ASAM_shp.zip
    └── Global_maritime_Pirate_attacks_1993_2020/
        ├── pirate_attacks.csv
        └── country_indicators.csv
```

---

## Dependencies

The following R packages are required and will be auto-installed if missing:

| Package | Purpose |
|---|---|
| `dplyr`, `tidyr` | Data wrangling |
| `ggplot2`, `scales` | Static visualizations |
| `corrplot` | Correlation matrix plot |
| `sf` | Spatial data handling |
| `rnaturalearth`, `rnaturalearthdata` | World map base layers |
| `leaflet` | Interactive map rendering |
| `shiny` | Interactive web application |
| `spdep` | Spatial autocorrelation (Moran's I) |

---

## Analysis Components

### 1. High-Risk Region Map
A static `ggplot2` world map highlighting the three major piracy hotspots:
- **Gulf of Aden** — off the Horn of Africa
- **Strait of Malacca** — between Malaysia and Indonesia
- **Gulf of Guinea** — West Africa

### 2. Global Attack Density Map
A 2D kernel density overlay on a world map (from ASAM shapefile data), using a yellow-to-red gradient to show attack concentration.

### 3. Correlation Matrix of Risk Factors
A `corrplot` visualization showing pairwise correlations between four country-level indicators from the GMPA dataset:
- GDP
- Corruption Index
- Homicide Rate
- Unemployment Rate

### 4. Temporal Trend (1993–2020)
A line/point time series chart plotting the annual count of pirate attacks, revealing trends and fluctuations over nearly three decades.

### 5. Spatial Autocorrelation (Moran's I)
A 5-degree grid cell analysis overlaid on the world map, with attack counts per cell. Moran's I statistic is calculated and displayed in the plot subtitle to quantify spatial clustering.

---

## Interactive Shiny Application

The embedded Shiny app (`shinyApp()`) provides an interactive dashboard with:

**Sidebar Controls:**
- **Region selector** — Filter by Global, Gulf of Aden, Strait of Malacca, or Gulf of Guinea
- **Year range slider** — Subset data between 1993 and 2020
- **Risk factor selector** — Choose from GDP, Corruption Index, Homicide Rate, or Unemployment Rate

**Main Panel Outputs:**
- **Interactive Leaflet map** — Red circle markers for individual attack locations
- **Time series plot** — Filtered temporal trend of attack counts
- **Risk factor plot** — Relationship between the selected socio-economic indicator and attack frequency

---

## How to Run

1. Clone or download this repository.
2. Place the required data files in the `data/` directory as shown above.
3. Open `Global_Maritime_Pirate_Attacks_code_shinyapp.Rmd` in RStudio.
4. Click **Knit** to render the full HTML report, or run the Shiny chunk directly to launch the interactive app.

> **Note:** The ASAM shapefile is loaded conditionally — if `ASAM_shp.zip` is not present, those visualizations will be silently skipped.

---

## References

1. U.S. Office of Naval Intelligence. (2020). *Anti-Shipping Activity Messages (ASAM) Database.*
2. International Maritime Bureau. *Global Maritime Pirate Attacks Dataset (1993–2020).*
