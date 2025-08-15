# Integration of public electric vehicle charging stations and renewable energy sources: The global potential and spatial equity

This repository contains a series of Jupyter notebooks that form a data processing and analysis pipeline to evaluate the **renewable energy potential and equity** of electric vehicle (EV) charging infrastructure in urban areas across **China, USA, and Europe**.

The workflow integrates population data, urban boundary definitions, and renewable energy generation data to compute two key metrics at the city level:
1. **Matching Level**: The alignment between renewable energy supply (wind and solar) and charging demand.
2. **Gini Coefficient**: A measure of equity in the distribution of renewable energy access across cities.

---

## 📁 Repository Structure

### 1. `Population data cropping for China_USA_Europe.ipynb`
**Purpose**:  
Preprocesses global population raster data (1km resolution) downloaded from the [WorldPop database](https://www.worldpop.org/) to extract and crop population datasets for **China, the USA, and Europe**.

**Functionality**:
- Loads global population TIF files.
- Uses regional boundary shapefiles or GeoJSONs to clip population data to the three target regions.
- Outputs region-specific population rasters for downstream analysis.

**Dependencies**:  
- WorldPop population data (input)
- Country or region boundary files (e.g., shapefiles or GeoJSONs)

---

### 2. `Urban boundary code.ipynb`
**Purpose**:  
Processes urban boundary data to extract built-up urban areas for cities in **China, USA, and Europe**.

**Data Source**:  
Uses the **Global City Boundary Dataset** provided by [Peng Cheng Laboratory](https://data-starcloud.pcl.ac.cn/iearthdata/), which defines built-up urban areas based on remote sensing and population density.

**Functionality**:
- Loads and filters the global urban boundary dataset.
- Extracts urban boundaries for cities in the three target regions.
- Performs spatial operations (e.g., simplification, projection, indexing) for efficient spatial analysis.
- Outputs processed urban boundary files (e.g., GeoJSON or Shapefile) for use in later steps.

---

### 3. `Gini Coefficient calculation.ipynb`
**Purpose**:  
Calculates the **Gini coefficient** to assess the **equity** of renewable energy (wind and solar) utilization across cities.

**Method**:
- Aggregates charging station demand and renewable energy potential at the city level.
- Computes the Gini coefficient based on the Lorenz curve of renewable energy access.
- A lower Gini value indicates more equitable distribution.

**Note**:  
While the method applies to all three regions, this notebook demonstrates the calculation using **USA as an example** due to data availability and consistency. The same workflow can be adapted for China and Europe.

---

### 4. `Matching level calculation.ipynb`
**Purpose**:  
Computes the **matching level** between renewable energy generation (wind and solar) and EV charging demand at the city level.

**Method**:
- Spatially joins charging station locations with renewable energy potential data.
- Calculates temporal and spatial alignment metrics (e.g., correlation, supply-demand ratio).
- Outputs a matching score for each city, indicating how well local renewables meet local charging needs.

**Note**:  
Like the Gini coefficient notebook, this demonstrates the method using **the United States as a case study**, but the framework is generalizable to **China and Europe** with region-specific data.

---
### 📁 Visualization: Figure Generation
In addition to the core data processing and analysis notebooks, this repository includes a set of scripts dedicated to generating the main figures and supplementary visualizations presented in the study.

The Figure/ directory contains Python scripts that produce publication-ready plots illustrating the key findings related to renewable energy matching levels and spatial equity (Gini coefficients) across China, the USA, and Europe. Each script corresponds to one main figure in the paper and its associated appendix figure, ensuring full reproducibility of the visual results.

These scripts use pandas, seaborn, and matplotlib to create comparative bar plots, violin plots, and annotated change visualizations that highlight regional disparities and temporal shifts in equity and renewable integration. They are designed to work seamlessly with the outputs from the previous analysis steps, enabling consistent and scalable figure generation for both the main text and supplementary materials.

---

## 📁 Data Sources
The data/ directory contains the raw and processed datasets used across the analysis pipeline. Due to data size and licensing, most raw datasets are not included in the repository but are publicly available through the sources listed below. Scripts assume a standardized folder structure for input data.

---

### 🌍 Population Data 
Source: WorldPop
Description: Global 1km resolution population count rasters (e.g., for year 2020).
Usage: Input for Population data cropping for China_USA_Europe.ipynb to extract regional population distributions.
Note: Users must download the global population TIF files and place them in  the [WorldPop database](https://www.worldpop.org/) before processing.

---
### 🏙️ Urban Boundary Data
Source: Global Urban Boundary Dataset (GUB) – [Peng Cheng Laboratory](https://data-starcloud.pcl.ac.cn/iearthdata/)
Dataset: GUB_Global_2018.shp (Shapefile, ~10 GB)
Usage: Used in Urban boundary code.ipynb to identify built-up urban areas for cities in China, USA, and Europe.
Note: This large file should be downloaded separately. Processing scripts clip it to target regions to reduce memory usage.

---

### ☀️ Solar Energy Potential
Source: Global Solar Atlas
Data: Annual average photovoltaic power potential (PVOUT, kWh/kWp/day) at 250m resolution.
Usage: Integrated in Matching level calculation.ipynb and Gini Coefficient calculation.ipynb to estimate solar generation aligned with urban charging demand.

---
### 💨 Wind Energy Potential 

Source: [Global Wind Atlas](https://globalwindtlas.info/zh/download/)
Data: Wind power density (W/m²) at multiple heights (e.g., 100m), 250m resolution.
Usage: Used to estimate onshore wind energy potential near urban centers for renewable matching and equity analysis.

---
### ⚡ Charging Station & Parking Data

Purpose: Represent potential or existing EV charging infrastructure.
Sources:
USA & Europe: Parking lot locations extracted from OpenStreetMap (OSM).
China: Parking lot locations collected via Baidu Maps API.
Usage: In Figure 4, these parking lots are treated as candidate charging stations. Their spatial distribution and capacity are analyzed using the same Gini and matching frameworks.
Storage: Processed parking data (after cleaning and geocoding) is stored in data/parking/.
📈 Input Data for Figures
The Figures/ directory relies on processed outputs from:
Gini Coefficient calculation.ipynb
Matching level calculation.ipynb
These include CSV or JSON files containing city-level metrics (e.g., Gini values, matching scores, mean values, percentage changes).
Figure 4 specifically combines parking-derived charging potential with renewable supply data to assess technical feasibility and spatial equity across the three regions, using consistent methodology.

---
### 🔁 Reproducibility Guidelines

To reproduce the full workflow:

Download the required datasets from the provided links.
Organize them under the data/ folder using the expected structure (e.g., data/population/, data/urban_boundaries/, data/renewables/).
Run notebooks in sequence:
Population data cropping for China_USA_Europe.ipynb
Urban boundary code.ipynb
Matching level calculation.ipynb and Gini Coefficient calculation.ipynb
Finally, execute the figure generation scripts.
All scripts include path configurations and data validation steps to ensure robustness across environments.

## 🔗 Workflow Overview
The full analysis pipeline follows a structured workflow:
1. **Population and urban boundary data** are first cropped and processed for China, USA, and Europe.
2. These geospatial datasets are used to **extract city-level metrics** for renewable energy potential and EV charging demand.
3. **Matching levels** and **Gini coefficients** are computed to evaluate efficiency and equity.
4. Finally, **visualization scripts** generate the main figures and supplementary plots to communicate the results.

This end-to-end pipeline ensures reproducibility, scalability, and transparency in assessing the integration of renewable energy and electric vehicle infrastructure globally.
