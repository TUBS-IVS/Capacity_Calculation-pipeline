# Capacity_Calculation Pipeline

This repository provides a data processing pipeline to calculate building volumes for the **Braunschweig Großraum** region and to enrich building footprints with semantic information.

The workflow integrates **OpenStreetMap (OSM)** data with **ALKIS** building and land-use datasets to create an enriched, building-level dataset suitable for urban analysis and capacity estimation.

---

## Data Sources

### OpenStreetMap (OSM)

All OSM data used in this project is based on the **Lower Saxony extract** downloaded from Geofabrik:

https://download.geofabrik.de/europe/germany/niedersachsen.html

This dataset serves as the base for:
- Building footprints  
- Points of Interest (POIs)  
- Land-use data  
- Building-use attributes  

---

### ALKIS Building Data (LOD2)

The project uses the **ALKIS LOD2 building dataset** provided by LGLN:

https://ni-lgln-opengeodata.hub.arcgis.com/apps/lgln-opengeodata::3d-geb%C3%A4udemodell-lod2/explore

Although the dataset is provided as a 3D building model, only the **2D information** is used, as the focus of this project is on **building volume**, not architectural structure.

---

## Pipeline Description

### 1. ALKIS Data Extraction and Regional Clipping

The ALKIS dataset (`lgln-opengeodata-lod2.geojson`), uploaded on a server, is loaded and clipped using a predefined regional boundary (`regionalverband_area`) to extract buildings within the study area.

The processed and merged building geometries are saved as shapefiles for the Braunschweig Großraum region.

---

### 2. Geometry Merging and Volume Calculation

**Notebook:** `Geometry-dataset-volume-calculation.ipynb`

This step is responsible for:
- Merging overlapping and adjacent building polygons
- Fixing invalid geometries
- Calculating building footprint area
- Calculating building volume
- Removing unnecessary 3D structural information

Only volume-related attributes are retained.

---

### 3. Semantic Enrichment with ALKIS and OSM

**Notebook:** `Enriching-with-ALKIS-data.ipynb`

This step enriches building geometries with semantic information from multiple sources:
- OSM building-use data
- OSM land-use data
- ALKIS building and land-use classifications

Combining multiple data sources improves confidence in building categorization and allows for future extensions with additional datasets.

---

## Output

The final output includes:
- Merged building geometries for the Braunschweig Großraum region.
- Accurate building footprint areas and volumes.
- Semantically enriched building attributes.

---

## Requirements

All required Python dependencies are listed in `requirements.txt`.
