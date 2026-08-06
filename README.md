# 🛫 BI Project — Geospatial Analysis for Civil Aviation BI in Sri Lanka (Task C)

[![QGIS](https://img.shields.io/badge/QGIS-3.x-green?logo=qgis&logoColor=white)](https://qgis.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-blue?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![PostGIS](https://img.shields.io/badge/PostGIS-3.4-blue)](https://postgis.net/)
[![Google Earth](https://img.shields.io/badge/Google%20Earth-Pro-red?logo=googleearth&logoColor=white)](https://www.google.com/earth/about/versions/)

> **Module:** Analytics & Business Intelligence (ABI)  
> **Assessment:** WRIT1 (80% Weighting) — Task C (30 Marks)  
> **Task Title:** *Geo Spatial Analysis for deploying Primary Surveillance Radar (PSR), Secondary Surveillance Radar (SSR), and Surface Movement Radar (SMR) systems at Bandaranaike International Airport (CMB).*

---

## 📖 Overview

This project evaluates how geospatial technologies (GIS, spatial mapping, location intelligence, PostgreSQL/PostGIS) can be applied to generate meaningful business intelligence for Sri Lanka's civil aviation sector. 

Specifically, this repository focuses on **Task C: Geo Spatial Analysis for deploying PSR, SSR, and SMR radar systems at BIA, Katunayake**.

---

## 📁 Folder Structure

```
BI-Project/
│
├── 📄 README.md                          # This file — project overview & setup guide
├── 📦 GIS-Task-C.qgz                    # Empty QGIS project file (EPSG:5234) — ready to use
│
├── 📂 data/                              # Datasets directory
│   └── 📂 Question-(c)/                  # Task C — Geospatial / GIS Analysis Data
│       ├── Bandaranayake Airport Areal Latest3_1_modified.tif  # Aerial image (~94MB) — to be georeferenced
│       ├── Airport Places.shp (+.dbf, .shx, .prj, .cpg, .qmd, .kml)  # Airport places (points)
│       ├── Airport Places New.shp (+.dbf, .shx, .prj, .cpg, .qmd)     # Updated airport places
│       ├── Admin Regions.shp (+.dbf, .shx, .prj, .cpg)                # Administrative regions
│       ├── Air Force Base Katunayake.shp (+.dbf, .shx, .prj, .cpg, .qmd)  # SLAF base boundary
│       └── Air Force Base Region.shp (+.dbf, .shx, .prj, .cpg)        # SLAF base region
│
├── 📂 student-doc/                       # Student documentation & step-by-step guides
│   ├── Assessment_Brief_WRIT1.md         # Full assessment brief (tasks, marking criteria)
│   ├── task_c_complete_guide_sinhala.md   # 🇱🇰 Task C guide — Sinhala + English (සිංහල)
│   └── task_c_complete_guide_english.md   # 🇬🇧 Task C guide — Full English version
│
└── 📂 Figures/                           # Screenshots and reference images
    ├── image.png
    └── image copy.png
```

---

## 📊 Task Overview

| Task | Title | Tools | Marks | Dataset |
|------|-------|-------|-------|---------|
| **C** | Geospatial Analysis — PSR/SSR/SMR Radar Deployment | QGIS, PostgreSQL, Google Earth | 30 | Shapefiles + Aerial Image (`.tif`) |

---

## 📑 Student Documentation (Task C)

The `student-doc/` folder contains **comprehensive A-Z step-by-step guides** for completing the QGIS Geospatial Analysis (Task C). Two versions are available:

| Document | Language | Description |
|----------|----------|-------------|
| [task_c_complete_guide_sinhala.md](student-doc/task_c_complete_guide_sinhala.md) | 🇱🇰 Sinhala + English | Complete guide in Sinhala with English technical terms |
| [task_c_complete_guide_english.md](student-doc/task_c_complete_guide_english.md) | 🇬🇧 English | Full English version of the same guide |

### What the guides cover (11 Steps):

1. ✅ QGIS Project Setup & CRS Configuration (EPSG:5234)
2. ✅ Aerial Image Georeferencing (with detailed GCP process)
3. ✅ Google Earth KML/KMZ Creation
4. ✅ Loading Provided Shapefiles
5. ✅ Digitization — Creating Vector Layers
6. ✅ Geo-Processing (Buffer, Clip, Intersection, Difference)
7. ✅ PostgreSQL + PostGIS Database Setup (**3 Methods**: Local Install, Docker, Supabase)
8. ✅ PostGIS Layer Verification in QGIS
9. ✅ Final Map Design with Print Layout
10. ✅ Adding Base Maps for Extra Marks
11. ✅ Report Writing — Critical Discussion Structure

**Also includes:** Error troubleshooting table, marking criteria tips, and a 24-item submission checklist.

---

## 🗺️ Using the QGIS Project File

An empty QGIS project file ([GIS-Task-C.qgz](GIS-Task-C.qgz)) is included and pre-configured to get started quickly.

### How to use:

1. Open **QGIS Desktop**
2. Click `Project` → `Open...`
3. Navigate to this folder and select `GIS-Task-C.qgz`
4. The project opens with the correct CRS (**EPSG:5234 — Kandawala / Sri Lanka Grid**)
5. Start following the step-by-step guide from **Step 2** (Georeferencing)

> **Note:** Verify the project CRS is set to EPSG:5234 by checking the bottom-right corner of the QGIS window.

---

## 🔧 Required Software — Download Guide

### Core Tools for Task C

| # | Software | Version | Purpose | Download Link |
|---|----------|---------|---------|---------------|
| 1 | **QGIS Desktop** | 3.34+ (LTR recommended) | GIS analysis, georeferencing, digitizing, map design | [🔗 qgis.org/download](https://qgis.org/download/) |
| 2 | **PostgreSQL** | 16.x | Relational database for geospatial data storage | [🔗 postgresql.org/download](https://www.postgresql.org/download/windows/) |
| 3 | **PostGIS** | 3.4+ | Spatial extension for PostgreSQL | Installed via **Stack Builder** (bundled with PostgreSQL) |
| 4 | **Google Earth Pro** | Latest | KML/KMZ creation, GPS coordinate extraction | [🔗 google.com/earth](https://www.google.com/earth/about/versions/#earth-pro) |

### Optional Tools for Task C

| # | Software | Purpose | Download Link |
|---|----------|---------|---------------|
| 5 | **pgAdmin 4** | PostgreSQL GUI management | Bundled with PostgreSQL installer |
| 6 | **Docker Desktop** | Alternative PostgreSQL setup (containerized) | [🔗 docker.com/desktop](https://www.docker.com/products/docker-desktop/) |
| 7 | **Supabase** | Cloud PostgreSQL alternative (no install needed) | [🔗 supabase.com](https://supabase.com/) |

---

### 📥 Installation Guide

#### 1. QGIS Desktop

1. Go to [qgis.org/download](https://qgis.org/download/)
2. Download the **Long Term Release (LTR)** for Windows — `QGIS Standalone Installer`
3. Run the installer → Follow the prompts → Install with default settings
4. After installation, open QGIS → Verify it launches correctly

#### 2. PostgreSQL + PostGIS

1. Go to [postgresql.org/download/windows](https://www.postgresql.org/download/windows/)
2. Click **Download the installer** → Select PostgreSQL 16.x
3. Run the installer:
   - Set a password for the `postgres` user (remember this!)
   - Keep the default port: `5432`
   - ✅ Check **Launch Stack Builder** at the end
4. In **Stack Builder**:
   - Select your PostgreSQL version
   - Expand **Spatial Extensions** → Check **PostGIS 3.x Bundle**
   - Click Next → Install
5. Open **pgAdmin 4** to verify the installation

#### 3. Google Earth Pro

1. Go to [google.com/earth](https://www.google.com/earth/about/versions/#earth-pro)
2. Click **Download Earth Pro on desktop**
3. Run the installer → Follow prompts
4. Open Google Earth Pro → Search for "Bandaranaike International Airport" to test

---

## 📐 Dataset Details (Task C)

### Geospatial Data (Question-C)

| File | Type | Description |
|------|------|-------------|
| `Bandaranayake Airport Areal Latest3_1_modified.tif` | Raster (~94MB) | High-resolution aerial image of BIA — must be georeferenced |
| `Airport Places.shp` / `.kml` | Vector (Points) | Key locations around the airport |
| `Airport Places New.shp` | Vector (Points) | Updated airport locations |
| `Admin Regions.shp` | Vector (Polygon) | Administrative region boundaries |
| `Air Force Base Katunayake.shp` | Vector (Polygon) | Sri Lanka Air Force base boundary |
| `Air Force Base Region.shp` | Vector (Polygon) | Air Force base region extent |

> **Analysis Required:** Image georeferencing, feature digitization, buffer analysis (300m for SMR, 2-3km for PSR/SSR), spatial intersection, clipping, building count & area calculations, PostGIS database creation (`SL_BIA_Aerial_Info`), map composition.

---

## ⚙️ CRS Information

This project uses **EPSG:5234 — Kandawala / Sri Lanka Grid** as the Coordinate Reference System for all geospatial work.

| Property | Value |
|----------|-------|
| **EPSG Code** | 5234 |
| **Name** | Kandawala / Sri Lanka Grid |
| **Type** | Projected CRS |
| **Units** | Meters |
| **Datum** | Kandawala |
| **Projection** | Transverse Mercator |

---

## 📝 Report Format Guidelines

| Property | Requirement |
|----------|-------------|
| Paper | A4 |
| Margins | 1.5" left, 1" right, top and bottom |
| Page numbers | Bottom, right |
| Line spacing | 1.5 |
| Font | Times New Roman |
| Headings | 14pt, Bold |
| Normal text | 12pt |
| Referencing | Harvard Referencing System |
| Word count | 3000 words (total report) |

---

## 📎 Submission Checklist (Task C)

- [ ] Report submitted as **PDF** via Turnitin on Moodle
- [ ] File named: `studentID_moduleCode_WRIT1` (e.g., `st12345678 CSE5013 WRIT1`)
- [ ] All GIS data files, `.sql` queries, and database backups included
- [ ] Screenshots of practical QGIS work included in Appendix C
- [ ] All supportive materials labeled by task name
- [ ] Original provided datasets **NOT** included in submission
- [ ] Harvard referencing applied throughout

---

## 📜 License

This project is for academic purposes only as part of the Cardiff Metropolitan University Analytics & Business Intelligence module assessment.

---

## 👤 Author

**Nithadya Perera**  
📧 [nithadyaperera@gmail.com](mailto:nithadyaperera@gmail.com)

---

<p align="center">
  <i>Built with QGIS • PostgreSQL/PostGIS • Google Earth Pro</i>
</p>
