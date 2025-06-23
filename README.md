# Mangrove-Area-Time-Series-2000-2024-
Calculates annual mangrove area over a 24-year period.


---

# Mangrove Area Time Series Analysis (2000-2024)

## Project Overview

This project provides a comprehensive analysis of mangrove forest area dynamics in Mangrove area of Bangladesh over a 24-year period (2000-2024). Leveraging the power of Google Earth Engine (GEE), this study integrates and harmonizes data from multiple satellite missions (Landsat and Sentinel-2) to generate an annual time series of mangrove extent. The goal is to quantify long-term trends in mangrove cover, providing critical insights for conservation, coastal management, and climate change adaptation strategies.

Mangroves are vital coastal ecosystems, offering protection against erosion, acting as carbon sinks, and supporting diverse biodiversity. Understanding their changes over time is crucial for assessing their health and the impact of anthropogenic pressures and natural phenomena.

## Key Features

* **Multi-Sensor Data Integration:** Seamlessly combines Landsat (5, 7, 8) and Sentinel-2 satellite imagery, along with a pre-existing Landsat-derived mangrove product, to create a consistent time series.
* **Cloud-Optimized Processing:** Implements robust cloud and shadow masking techniques for both Landsat (using QA_PIXEL) and Sentinel-2 (using Cloud Score Plus) to ensure high-quality, cloud-free composites.
* **Annual Mangrove Classification:** Utilizes the Normalized Difference Vegetation Index (NDVI) with a defined threshold to delineate mangrove presence for each year.
* **Spatio-Temporal Analysis:** Generates annual area statistics (in km²) within a defined study polygon.
* **Interactive Visualization:** Produces a clear line chart to visualize the annual mangrove area trends.
* **Scalable & Reproducible:** Developed entirely within the Google Earth Engine platform, ensuring computational efficiency for large geospatial datasets and full reproducibility.

## Methodology

The core methodology involves iterating through each year from 2000 to 2024 and dynamically selecting the appropriate satellite data source:

1.  **Year 2000 Baseline:** Utilizes the pre-classified `LANDSAT/MANGROVE_FORESTS` dataset for a reliable baseline.
2.  **Landsat Era (2001-2015):**
    * Merges Landsat 5 (TM), Landsat 7 (ETM+), and Landsat 8 (OLI) Level 2 surface reflectance data.
    * Applies sensor-specific band mapping and scaling to calculate NDVI.
    * Employs `QA_PIXEL` band for robust cloud and shadow masking.
    * Generates an annual median composite of NDVI.
3.  **Sentinel-2 Era (2016-2024):**
    * Filters `COPERNICUS/S2_HARMONIZED` data.
    * Applies cloud masking using the `GOOGLE/CLOUD_SCORE_PLUS` collection with a threshold of 0.5.
    * Calculates NDVI using B8 (NIR) and B4 (Red) bands.
    * Generates an annual median composite of NDVI.
4.  **Mangrove Delineation:** For each annual NDVI composite, a threshold of `NDVI > 0.3` is applied to classify pixels as mangrove.
5.  **Resolution Harmonization:** All Sentinel-2 derived products are **reprojected to 30-meter resolution** to match the Landsat resolution, ensuring consistent spatial comparison throughout the time series.
6.  **Area Calculation:** The area of classified mangrove pixels is calculated for each year using `ee.Image.pixelArea()` and aggregated within a 1 km covering grid for efficiency, providing total area in square kilometers.
7.  **Output & Visualization:** The annual area statistics are collected into an `ee.FeatureCollection` and visualized as a line chart, illustrating the temporal trends.

## Data Sources

* **Study Area Boundary:** `projects/ee-mohammadoney/assets/mangrovepolygon`
* **Landsat Mangrove Forests (2000):** `LANDSAT/MANGROVE_FORESTS`
* **Landsat 5, 7, 8 (Surface Reflectance):**
    * `LANDSAT/LT05/C02/T1_L2`
    * `LANDSAT/LE07/C02/T1_L2`
    * `LANDSAT/LC08/C02/T1_L2`
* **Sentinel-2 Harmonized (Surface Reflectance):** `COPERNICUS/S2_HARMONIZED`
* **Sentinel-2 Cloud Score Plus:** `GOOGLE/CLOUD_SCORE_PLUS/V1/S2_HARMONIZED`

## Technologies & Libraries

* **Google Earth Engine (GEE) JavaScript API**
* **Remote Sensing Fundamentals:** NDVI calculation, cloud masking, image mosaicking.
* **Geospatial Analysis:** Time series analysis, area calculation, spatial filtering.
* **Data Visualization:** GEE Charting API.

## How to Run the Code

1.  **Access Google Earth Engine:** If you don't have an account, sign up for free at [earthengine.google.com](https://earthengine.google.com/).
2.  **Open the Code Editor:** Go to the GEE Code Editor.
3.  **Load the Script:** Copy the entire JavaScript code from `[your_script_name.js or direct link to GEE script]` into a new script in your GEE Code Editor.
4.  **Update Geometry (Optional):** Ensure the `geometry` asset `projects/ee-mohammadoney/assets/mangrovepolygon` is accessible, or replace it with your own study area polygon if you wish to analyze a different region.
5.  **Run:** Click the "Run" button in the GEE Code Editor.
6.  **View Results:** The console will display the `FeatureCollection` of annual mangrove areas, and an interactive line chart will appear in the "Charts" tab.

## Results & Discussion

[**Crucial:** This is where you summarize your specific findings. For example:]

* The analysis reveals a **[e.g., net decline/increase, stable period followed by decline/increase]** in mangrove area in [Your Study Area] from 2000 to 2024.
* Total mangrove cover was approximately **[X] km²** in 2000 and **[Y] km²** in 2024.
* The chart clearly illustrates [mention specific trends, e.g., "a sharp decline between 2005-2010," "a period of recovery after 2015," or "relatively stable cover with minor fluctuations"].
* These findings are crucial for [mention practical applications, e.g., "informing conservation priorities," "assessing the effectiveness of existing policies," or "guiding future reforestation efforts"].

[**Optional:** Include a screenshot of the generated chart here.]
[**Optional:** Link to an Earth Engine App if you've published one: `https://earthengine.google.com/xxxxxxxxxxxxxx`]

## Future Work & Improvements

* **Advanced Classification:** Implement machine learning algorithms (e.g., Random Forest, Support Vector Machine) with comprehensive training data for more robust and accurate mangrove classification, especially for distinguishing mangroves from other dense vegetation.
* **Phenological Adjustment:** Account for seasonal variations in mangrove greenness by filtering images to specific phenological windows (e.g., dry season, peak growing season) to ensure greater consistency across annual composites.
* **Cross-Sensor Harmonization:** Investigate more sophisticated methods for harmonizing spectral values across Landsat and Sentinel-2 to minimize potential biases introduced by different sensor characteristics.
* **Uncertainty Analysis:** Incorporate an assessment of classification uncertainty to provide a confidence interval for the area estimates.
* **Drivers of Change:** Integrate additional datasets (e.g., population density, land-use maps, climate data) to explore potential drivers behind the observed mangrove area changes.

---

## Contact

Feel free to reach out for questions or collaborations!

* **[Your Name]**
* **[Your Email Address]**
* **[Your LinkedIn Profile URL (Optional)]**
* **[Your Personal Website/Portfolio URL (Optional)]**

---
**License:** [Optional, e.g., MIT License or specify if open-source]

---
