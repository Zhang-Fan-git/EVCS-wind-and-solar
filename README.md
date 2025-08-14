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
### 📊 Visualization: Figure Generation
In addition to the core data processing and analysis notebooks, this repository includes a set of scripts dedicated to generating the main figures and supplementary visualizations presented in the study.

The Figure/ directory contains Python scripts that produce publication-ready plots illustrating the key findings related to renewable energy matching levels and spatial equity (Gini coefficients) across China, the USA, and Europe. Each script corresponds to one main figure in the paper and its associated appendix figure, ensuring full reproducibility of the visual results.

These scripts use pandas, seaborn, and matplotlib to create comparative bar plots, violin plots, and annotated change visualizations that highlight regional disparities and temporal shifts in equity and renewable integration. They are designed to work seamlessly with the outputs from the previous analysis steps, enabling consistent and scalable figure generation for both the main text and supplementary materials.

## 🔗 Workflow Overview
