# 🗺️ Task C - Complete Step-by-Step Guide (English Version)
## Geo Spatial Analysis for PSR, SSR & SMR Radar System Deployment (30 Marks)

---

> [!IMPORTANT]
> This is the **biggest task** in the assessment — worth 30 marks. You need to use QGIS, PostgreSQL, and Google Earth. Everything is explained step by step below to complete it without errors.

---

## 📋 Task C Requirements Summary

According to the assessment brief, you need to do the following:

1. **Geo-reference the aerial image** (MANDATORY - must be done first)
2. **Digitize** — create vector layers (with id, name, type, size columns)
3. **Use CRS: EPSG:5234** (Kandawala / Sri Lanka Grid)
4. **Identify suitable locations** to deploy PSR/SSR and SMR radar systems
5. **Extract GPS data** from Google Earth using KML/KMZ files
6. **Create a PostgreSQL Geo Spatial Database** — named "`SL_BIA_Aerial_Info`"
7. **Use Geo-processing tools** (Buffer, Clip, Intersection)
8. **Calculate**:
   - Total number of buildings in the suitability area
   - Total land area occupied by buildings
   - Total land area available for radar deployment
9. **Add map elements** (North Arrow, Scale Bar, Title, Legend)
10. **Write a critical discussion**

---

## 🔧 Required Software

| Software | Purpose |
|----------|---------|
| **QGIS** (3.x recommended) | Main GIS software — georeferencing, digitizing, geo-processing, map making |
| **PostgreSQL + PostGIS** | Creating the Geo Spatial Database |
| **Google Earth Pro** | Creating KML/KMZ files, extracting GPS coordinates |

---

## 📁 Provided Data Files

Your [Question-(c)](file:///c:/Users/mihisara/Desktop/BI-Project/data/Question-(c)) folder contains these files:

| File | Type | Description |
|------|------|-------------|
| `Bandaranayake Airport Areal Latest3_1_modified.tif` | Raster (Aerial Image) | BIA aerial photo — needs to be georeferenced |
| `Airport Places.shp` + `.kml` | Shapefile + KML | Airport places — point data |
| `Airport Places New.shp` | Shapefile | Updated airport places |
| `Admin Regions.shp` | Shapefile | Administrative regions |
| `Air Force Base Katunayake.shp` | Shapefile | Air Force base boundary |
| `Air Force Base Region.shp` | Shapefile | Air Force base region |

---

# 🚀 STEP-BY-STEP GUIDE

---

## STEP 1: QGIS Project Setup (Do This First)

### 1.1 — Open QGIS and Create a New Project

1. Open QGIS Desktop
2. Click `Project` → `New`
3. Click `Project` → `Save As...` → Save in your project folder (Ex: `GIS-Task-C.qgz`)

### 1.2 — Set the CRS (EPSG:5234)

> [!CAUTION]
> The CRS must be set to **EPSG:5234 (Kandawala / Sri Lanka Grid)**. This is specifically mentioned in the assessment brief. Using a different CRS will result in lost marks.

1. Click the CRS button at the bottom right corner of QGIS (it shows something like "EPSG:4326" by default)
2. Type `5234` in the search bar
3. Select **"Kandawala / Sri Lanka Grid - EPSG:5234"**
4. Click `Apply` → `OK`
5. ✅ Confirm that `EPSG:5234` is displayed at the bottom right

> [!TIP]
> **Take a screenshot!** — You'll need this for the appendix showing the CRS was set correctly.

---

## STEP 2: Aerial Image Geo-Referencing (MANDATORY FIRST STEP)

> [!WARNING]
> The assessment brief clearly states: *"It is mandatory to do the image geo-referencing before initiation of the digitization."* Skipping this will result in marks being deducted!

### 2.1 — Open the Georeferencer Tool

1. QGIS menu: `Layer` → `Georeferencer` (QGIS 3.26+ — older versions: `Raster` → `Georeferencer`)
2. The Georeferencer window will open

### 2.2 — Load the Aerial Image

1. In the Georeferencer window: `File` → `Open Raster...`
2. Browse and select the `Bandaranayake Airport Areal Latest3_1_modified.tif` file
3. The image will be displayed in the Georeferencer window

### 2.3 — Set Transformation Settings

1. Georeferencer menu: `Settings` → `Transformation Settings...`
2. Set these values:

| Setting | Value |
|---------|-------|
| Transformation type | **Polynomial 1** |
| Resampling method | **Nearest Neighbour** |
| Target SRS | **EPSG:5234** |
| Output Raster | Save in your folder — Ex: `BIA_georeferenced.tif` |
| Compression | **LZW** |
| ✅ Load in project when done | Check this box |

3. Click `OK`

### 2.4 — Add Ground Control Points (GCPs)

> [!IMPORTANT]
> You need to add a minimum of **4 GCP points** (ideally 6-8). You'll use Google Earth/Google Maps to get real GPS coordinates for these points.

---

#### 🔍 Part A: Select a Point on the Aerial Image

1. Your aerial image should be loaded in the QGIS Georeferencer window
2. **Zoom in** on the image (use mouse scroll wheel)
3. Find a **clearly identifiable** point — look for things like:

| What to Look For | Example |
|------------------|---------|
| 🏢 Building corner | A corner of the Terminal building |
| ✈️ Runway edge/corner | Runway threshold marking |
| 🛣️ Road intersection | Where two roads meet |
| 🔲 Roof corner | A roof corner of any building |

> Your aerial image clearly shows the runway, buildings, and roads — use these features!

4. Click the **"Add GCP Point"** button on the Georeferencer toolbar — this icon:
   - 🟡 **Yellow dot with a plus (+) sign**
   - Located on the left side of the toolbar

5. Now **click exactly on the point** you selected on the aerial image (Ex: click on a building corner)

6. A **dialog box** will open — titled "Enter Map Coordinates"

---

#### 🌍 Part B: Get Coordinates of the Same Point from Google Earth

**This is the important part — you're doing two parallel tasks:**

7. **Open Google Earth Pro** (minimize QGIS)
8. Type in the search bar: `Bandaranaike International Airport` → Press Enter
9. Find the **exact same point** on Google Earth that you clicked on in the QGIS aerial image

   **Example:** If you clicked on the top-left corner of the Terminal building in QGIS, find **the same top-left corner of the Terminal building** in Google Earth

10. Move the mouse pointer over that point in Google Earth (**don't click, just hover**)
11. The **screen bottom bar** will display the coordinates:
    ```
    7°10'15.23"N  79°53'02.45"E  elev 8m
    ```
    Or in decimal format:
    ```
    7.170897°  79.884015°
    ```

> [!TIP]
> **To get decimal format:** Change the coordinates format in Google Earth's bottom bar: `Tools` → `Options` → `Show Lat/Long` → Select **Decimal Degrees**. This gives you decimal format coordinates — much easier to enter in QGIS.

12. Note down / remember the **Latitude** and **Longitude** values

---

#### 📝 Part C: Enter Coordinates into QGIS Georeferencer

13. Go back to the **QGIS Georeferencer** window
14. In the open dialog box, fill in:

| Field | What to Enter |
|-------|---------------|
| **X / East** | **Longitude** value (Ex: `79.884015`) |
| **Y / North** | **Latitude** value (Ex: `7.170897`) |
| **CRS** | `EPSG:4326 - WGS 84` (Google Earth coordinates are in WGS84 — QGIS will auto-convert to EPSG:5234) |

> [!WARNING]
> **X = Longitude (79.xxx), Y = Latitude (7.xxx)** — Don't mix these up! Longitude (79) goes in the X field, Latitude (7) goes in the Y field.

15. Click **OK**
16. ✅ GCP point 1 has been added! A **red dot** will appear in the Georeferencer window

---

#### 🔁 Part D: Repeat — Add Minimum 4 Points

**Add 3-5 more points using the same process:**

17. Click **"Add GCP Point"** again → Click a **different point** on the aerial image → Get the same point's coordinates from Google Earth → Enter them

**Point Placement Strategy — Spread them out across the image:**

```
    ⭐ Point 2                    ⭐ Point 6
    (top-left area)              (top-right area)
    
         ⭐ Point 4
         (center area)
         
    ⭐ Point 1                    ⭐ Point 5
    (bottom-left area)           (bottom-right area)
    
              ⭐ Point 3
              (bottom-center)
```

> [!CAUTION]
> **Don't cluster all points in one area!** They need to be **spread out** across the image — cover the corners and middle. This increases accuracy.

**Recommended GCP Points:**

| GCP # | Location | Approximate Coordinates |
|-------|----------|------------------------|
| 1 | Runway 04 threshold | 7.1708° N, 79.8841° E |
| 2 | Runway 22 threshold | 7.1812° N, 79.8909° E |
| 3 | Main Terminal building corner | 7.1798° N, 79.8849° E |
| 4 | Control Tower | 7.1741° N, 79.8840° E |
| 5 | Road intersection (Airport Road) | 7.1730° N, 79.8870° E |
| 6 | Air Force base building corner | 7.1770° N, 79.8800° E |

> [!NOTE]
> The above coordinates are approximate values. You should get accurate values yourself from Google Earth. Use points that are clearly identifiable on the image.

---

#### ✅ Part E: Check the RMS Error

18. After adding at least 4 points, check the **GCP table** (bottom panel) in the Georeferencer window:

| GCP | Source X | Source Y | Dest X | Dest Y | **Residual** |
|-----|----------|----------|--------|--------|-------------|
| 1 | 234 | 567 | 79.884 | 7.170 | **1.23** |
| 2 | 890 | 123 | 79.891 | 7.181 | **0.89** |
| ... | ... | ... | ... | ... | ... |

- Check the values in the **Residual** column — **low values = good** (< 5 pixels is ideal)
- The **Mean error** / **Total RMS error** is displayed at the bottom
- If the error is too high (> 10), **delete** that point and redo it (right-click → Delete Point)

---

#### 🎯 GCP Process Quick Summary

```
Click on QGIS Aerial Image  →  Hover over same point in Google Earth
         ↓                              ↓
   Dialog opens                  Read coordinates (bottom bar)
         ↓                              ↓
   X = Longitude (79.xxx),  Y = Latitude (7.xxx) — enter them
         ↓
   OK → GCP added! ✅
   
   Repeat 4-8 times → Check RMS Error → Start Georeferencing ▶
```

### 2.5 — Run Georeferencing

1. Click the **"Start Georeferencing"** button on the Georeferencer toolbar (green play icon)
2. The process will complete
3. The georeferenced image will automatically load in the QGIS main window
4. ✅ Check if the image is displaying at the correct location

> [!TIP]
> **Take screenshots!** — GCP table, Transformation settings, georeferenced result — capture everything for the appendix.

---

## STEP 3: Google Earth — Create KML/KMZ Files

### 3.1 — Open Google Earth Pro and Create Placemarks

According to the assessment brief, you need to use KML/KMZ files. These are used to extract GPS data and mark key locations.

1. Open **Google Earth Pro**
2. Search for BIA (Bandaranaike International Airport)
3. **Mark Key Locations** (using the Placemark tool — yellow pin icon):

| Location | Type | Why? |
|----------|------|------|
| CMB Control Tower | Point | Reference point |
| Runway Center Point (RCP) | Point | To measure PSR/SSR distance |
| Proposed SMR location | Point | ~300m from Control Tower, ~200m from RCP |
| Proposed PSR/SSR location | Point | ~2km from RCP, within Air Force base |
| Airport Terminal | Point | Reference for digitization |
| Air Force Base | Polygon | Mark the area boundary |

### 3.2 — Enter Placemark Details

When adding each placemark:
1. Enter a descriptive name in the **Name** field (Ex: "CMB Control Tower", "Proposed PSR SSR Location")
2. Note the **Latitude/Longitude**
3. Click `OK`

### 3.3 — Export KML/KMZ

1. Right-click on "My Places" / the folder you created in the left panel
2. Click `Save Place As...`
3. Select file type: **KML** or **KMZ**
4. Save in your project folder (Ex: `BIA_Radar_Locations.kml`)

### 3.4 — Import KML into QGIS

1. QGIS: `Layer` → `Add Layer` → `Add Vector Layer...`
2. Browse and select your `.kml` file as the source
3. Click `Add`
4. ✅ Confirm that the points are displayed at the correct locations on the QGIS map

> [!IMPORTANT]
> **Import / CRS Troubleshooting Note:** If the points are not displayed or visible on the QGIS map after importing the KML file, it is due to a CRS mismatch (KML default is EPSG:4326 - WGS 84 while project uses EPSG:5234). To fix this, right-click the imported KML layer, select **`Export` → `Save Features As...`**, set the **CRS to `EPSG:5234 (Kandawala / Sri Lanka Grid)`**, and save/re-export it. The points will then display accurately on top of your aerial image!

> [!TIP]
> **Take screenshots!** — Google Earth placemark creation, KML save, QGIS import — capture everything.

---

## STEP 4: Load Provided Shapefiles

### 4.1 — Add Shapefiles

1. QGIS: `Layer` → `Add Layer` → `Add Vector Layer...`
2. Add these shapefiles one by one:
   - `Airport Places New.shp`
   - `Airport Places.shp`
   - `Admin Regions.shp`
   - `Air Force Base Katunayake.shp`
   - `Air Force Base Region.shp`
3. If a CRS prompt appears when adding each layer, select **EPSG:5234**

### 4.2 — Re-project Layer CRS (if needed)

Your shapefiles may be in EPSG:4326 (WGS84). Convert them to EPSG:5234:

1. Right-click the layer → `Export` → `Save Features As...`
2. Format: **ESRI Shapefile**
3. Select CRS: **EPSG:5234**
4. Filename: Ex: `Airport_Places_5234.shp`
5. Click `OK`
6. ✅ The re-projected layer will be added

---

## STEP 5: Digitization — Create Vector Layers

> [!IMPORTANT]
> The assessment brief states: *"Every vector layer attribute table should contain suitable data in columns id, name, type, and size"*. These 4 columns must be present in every layer's attribute table!

### 5.1 — Create a New Vector Layer (Example: Buildings Layer)

1. QGIS: `Layer` → `Create Layer` → `New Shapefile Layer...`
2. Settings:

| Setting | Value |
|---------|-------|
| File name | Ex: `BIA_Buildings.shp` |
| Geometry type | **Polygon** |
| CRS | **EPSG:5234** |

3. **Add fields** (in the New Field section):

| Field Name | Type | Length |
|------------|------|--------|
| id | Integer | 10 |
| name | String | 100 |
| type | String | 50 |
| size | Real (Decimal) | 15, 3 |

   - For each field: Type the Name, select the Type, then click the **"Add to Fields List"** button
4. Click `OK`
5. ✅ An empty layer will be added to the Layers panel

### 5.2 — List of Layers to Create

Create and digitize all of these layers:

| Layer Name | Geometry | Purpose |
|------------|----------|---------|
| `BIA_Buildings` | Polygon | Buildings in the airport area |
| `BIA_Runway` | Polygon / Line | Runway digitization |
| `BIA_Taxiways` | Line / Polygon | Taxiways |
| `BIA_Terminal` | Polygon | Terminal building |
| `BIA_Roads` | Line | Airport roads |
| `BIA_Radar_PSR_SSR` | Point | Proposed PSR/SSR location |
| `BIA_Radar_SMR` | Point | Proposed SMR location |
| `BIA_Control_Tower` | Point | Control Tower location |
| `BIA_RCP` | Point | Runway Center Point |

### 5.3 — Digitizing (Drawing Features)

1. Select the layer you want to digitize (click on it in the Layers panel)
2. Click the **Toggle Editing** button (pencil icon 🖊️)
3. Click the **"Add Polygon Feature"** (or Point/Line) button
4. Draw the feature using the georeferenced aerial image as reference:
   - Polygon: Click, click, click to draw the boundary → right-click to finish
   - Point: Click once
   - Line: Click, click → right-click to finish
5. A dialog box will open — enter the attribute values:
   - **id**: 1, 2, 3... (sequential)
   - **name**: "Terminal Building 1", "Hangar A", etc.
   - **type**: "Terminal", "Hangar", "Office", "Residential", etc.
   - **size**: Enter `0` (will be auto-calculated in QGIS later)
6. Click `OK`
7. Feature drawn!
8. Continue drawing more features...
9. Done? Click the **Save Layer Edits** button (floppy disk icon)
10. Turn off **Toggle Editing**

> [!TIP]
> **How to Auto-Calculate `size` ($m^2$):**
> You don't need to manually calculate or guess the `size` while drawing (just enter `0`). After drawing all features:
> 1. Right-click the layer → **`Open Attribute Table`**.
> 2. Click the **Field Calculator** icon (🧮 abacus icon) or press `Ctrl + I`.
> 3. Check **`Update existing field`** and select the `size` field.
> 4. In the Expression box, type **`$area`** and click **OK**.
> QGIS will automatically compute and populate the exact square meters ($m^2$) for every single polygon in the attribute table!

> [!WARNING]
> Save regularly while digitizing! If QGIS crashes, you'll lose unsaved data.

### 5.4 — Digitize Buildings (The Biggest Part)

> [!IMPORTANT]
> **Scope Note, Manual Digitizing & Academic Justification:**
> 
> 1. **Manual Digitizing is 100% Mandatory & Correct:**
>    - Manually tracing/drawing building footprints polygon-by-polygon using mouse clicks is the standard, 100% correct, and mandatory GIS procedure.
>    - You do NOT need to digitize thousands of buildings across the entire map! Digitizing around 20–40 main/representative buildings within the BIA Airport premises and SLAF Katunayake Base area is completely sufficient for the required calculations.
> 
> 2. **Digitizing vs. Buffer Order (Two Valid Workflows):**
>    - **Method A (Clip Tool Automation - Recommended for speed & accuracy):** Manually digitize 20–40 buildings across the general Airport / Air Force base premises first. You don't need to worry about exact buffer boundaries initially. Later in Step 6, the `Clip` tool will automatically intersect and extract only the buildings that fall inside the calculated suitability buffer zone.
>    - **Method B (Visual Guide Approach):** Alternatively, run Step 6.1 `Buffer` first to render the suitability boundary rings visually on your QGIS map canvas, then manually digitize the buildings directly within those rings.
> 
> 3. **Marking Criteria & Academic Justification:**
>    - Task C (30 Marks) evaluates students on Spatial Analysis & Geo-processing proficiency.
>    - While building footprints are digitized manually in Step 5, using spatial overlay operations (`Buffer` combined with `Clip`) in Step 6 to mathematically determine suitability limits (rather than manually guessing 300m/2km distances by eye) demonstrates standard professional GIS modeling methodology (ICAO radar siting standards), ensuring top-band assessment marks.

> [!CAUTION]
> **Critical Digitizing Rule (Individual Footprints vs. One Giant Bounding Box):**
> ❌ **DO NOT:** Draw one single giant polygon covering the entire airport apron or sector! Doing so will result in QGIS recording only 1 single building feature instead of individual structures.
> ✅ **DO:** **Zoom In** closely on the aerial image until individual roof structures are clearly visible. Trace each building individually (Polygon per structure: Terminal, Hangars, Offices, etc.) so that your Attribute Table contains separate rows for each building feature (e.g., 20–40 distinct building rows).
> 💡 **Pro Tip (50% Layer Opacity):** To keep the aerial photo visible under drawn shapes, right-click `BIA_Buildings` → `Properties` → `Symbology` → set **Opacity to 50%**.

Zoom in on the aerial image:
1. Trace/draw **every building** within the suitability area (PSR/SSR 2-3km zone, SMR zone)
2. Fill in unique id, name, type, size attribute values for each building
3. ✅ Open and check the Attribute table — `Right-click layer` → `Open Attribute Table`

---

## STEP 6: Geo-Processing — Buffer, Clip, Intersection

This is **extremely important** — you'll earn significantly more marks by using geo-processing tools.

### 6.1 — Buffer Analysis (Radar Coverage Zones)

**SMR Buffer (~300m from Control Tower):**
1. Select the Control Tower point layer
2. `Vector` → `Geoprocessing Tools` → `Buffer...`
3. Settings:
   - Input layer: `BIA_Control_Tower`
   - Distance: **300** (meters — CRS EPSG:5234 uses meter units)
   - Segments: 36
   - Output: `SMR_Buffer_300m.shp`
4. Click `Run`

**PSR/SSR Buffer (2km-3km zone from RCP):**

First buffer:
1. Select the RCP point layer
2. `Vector` → `Geoprocessing Tools` → `Buffer...`
   - Input: `BIA_RCP`
   - Distance: **3000** (3km = 3000m)
   - Output: `PSR_SSR_Buffer_3km.shp`
3. Click `Run`

Second buffer:
4. Buffer again:
   - Input: `BIA_RCP`
   - Distance: **2000** (2km = 2000m)
   - Output: `PSR_SSR_Buffer_2km.shp`
5. Click `Run`

**Create the Ring Zone (2km-3km area):**
6. `Vector` → `Geoprocessing Tools` → `Difference...`
   - Input: `PSR_SSR_Buffer_3km`
   - Overlay: `PSR_SSR_Buffer_2km`
   - Output: `PSR_SSR_Suitability_Zone.shp`
7. Click `Run`
8. ✅ This creates a donut-shaped zone from 2km to 3km — the suitable zone for PSR/SSR deployment!

### 6.2 — Intersection (Air Force Base + Suitability Zone)

The assessment brief states that PSR/SSR should ideally be installed within the Air Force base premises:

1. `Vector` → `Geoprocessing Tools` → `Intersection...`
   - Input: `PSR_SSR_Suitability_Zone`
   - Overlay: `Air Force Base Katunayake` (or Air Force Base Region)
   - Output: `PSR_SSR_Ideal_Zone.shp`
2. Click `Run`
3. ✅ This gives you the overlapping area that is both within the Air Force base and within the 2-3km zone

### 6.3 — Clip (Buildings within Suitability Area)

Identify buildings within the suitability area:

1. `Vector` → `Geoprocessing Tools` → `Clip...`
   - Input: `BIA_Buildings` (the buildings layer you digitized)
   - Overlay: `PSR_SSR_Ideal_Zone`
   - Output: `Buildings_in_Radar_Zone.shp`
2. Click `Run`
3. ✅ Only buildings within the suitability area will be shown

### 6.4 — Calculate Required Statistics

**Total number of buildings:**
1. Right-click `Buildings_in_Radar_Zone` layer → `Open Attribute Table`
2. The **feature count** shown in the bottom bar is the total number of buildings

**Total land area (buildings):**
1. Open the Attribute table → Click `Field Calculator` (abacus icon)
2. ✅ Create a new field: `area_sqm`
3. Expression: `$area`
4. Click `OK`
5. `Processing` → `Toolbox` → search "Basic Statistics" → run on the `area_sqm` field
6. The **Sum** value = Total building area

**Total available land area for radar:**
1. Open `PSR_SSR_Ideal_Zone` layer attribute table → Field Calculator
2. Expression: `$area`
3. ✅ That gives you the total zone area
4. Available area = Zone area − Total building area

> [!TIP]
> **Take screenshots!** — Buffer zones, Intersection results, Attribute tables, Area calculations — capture everything.

---

## STEP 7: PostgreSQL + PostGIS — Create the Geospatial Database

> [!IMPORTANT]
> The database name must be exactly **"`SL_BIA_Aerial_Info`"** — this is specified in the assessment brief.

> [!NOTE]
> There are **3 methods** to set up PostgreSQL + PostGIS. Choose whichever method is most convenient for you. All methods allow you to connect from QGIS.

| Method | Difficulty | Best For |
|--------|-----------|----------|
| 🖥️ **Method 1: Local Install** | Medium | Those who already have PostgreSQL installed / traditional approach |
| 🐳 **Method 2: Docker** | Easy | Those who have Docker installed / want a clean setup |
| ☁️ **Method 3: Supabase** | Easiest | Those who can't install locally / want a cloud solution |

---

### 🖥️ METHOD 1: Local PostgreSQL Install

#### 7.1a — Install PostgreSQL + PostGIS

**If PostgreSQL is not yet installed:**
1. [postgresql.org/download/windows](https://www.postgresql.org/download/windows/) → Download
2. Run the installer
3. During installation:
   - Port: **5432** (default)
   - Password: Set a password you'll remember (Ex: `postgres123`)
   - ✅ Check the **Stack Builder** launch checkbox when installation completes

**Install PostGIS (Stack Builder):**
4. Stack Builder will open
5. Select your PostgreSQL version from the dropdown (Ex: `PostgreSQL 16 on port 5432`)
6. Click `Next`
7. Expand **Spatial Extensions** → ✅ Check **PostGIS 3.x Bundle**
8. Click `Next` → `Next` → Install
9. ✅ PostGIS installed!

**If PostgreSQL is already installed but PostGIS is not:**
1. Windows Start Menu → Search for **Stack Builder** and open it
2. Follow steps 5-9 above

#### 7.1b — Configure pgAdmin

1. Windows Start Menu → Open **pgAdmin 4**
2. Set a master password when opening for the first time
3. Left panel: Expand `Servers` → `PostgreSQL XX`
4. If a password prompt appears, enter the password you set during installation

#### 7.1c — Create Database (pgAdmin)

1. `Servers` → `PostgreSQL XX` → Right-click **Databases** → `Create` → `Database...`
2. **Database** tab:
   - Database name: **`SL_BIA_Aerial_Info`**
   - Owner: `postgres`
3. Click `Save`
4. ✅ `SL_BIA_Aerial_Info` database will appear in the left panel

#### 7.1d — Enable PostGIS Extension

1. Click on `SL_BIA_Aerial_Info` database in the left panel
2. Top menu: `Tools` → `Query Tool` (or right-click database → Query Tool)
3. Type in the query editor:
```sql
CREATE EXTENSION postgis;
```
4. Click the **▶ Execute** button (or press F5)
5. ✅ Message: "Query returned successfully" — PostGIS is enabled!

**Verify PostGIS:**
```sql
SELECT PostGIS_Version();
```
The result will display a version number (Ex: `3.4 USE_GEOS=1 USE_PROJ=1`)

#### 7.1e — Connect to QGIS (Local)

1. Open QGIS → In the left **Browser Panel**, right-click `PostGIS` → **`New Connection...`**
2. Fill in the dialog box:

| Field | Value |
|-------|-------|
| **Name** | `SL_BIA_Aerial_Info` |
| **Host** | `localhost` |
| **Port** | `5432` |
| **Database** | `SL_BIA_Aerial_Info` |

3. **Authentication** section:
   - ✅ Check the **"Store"** checkbox
   - **User name**: `postgres`
   - **Password**: your installation password

4. Click the **`Test Connection`** button
5. ✅ If you see "Connection to SL_BIA_Aerial_Info was successful" — it's working!
6. Click `OK`

> [!WARNING]
> **If you get a "Connection failed" error:**
> - Check if the PostgreSQL service is running: Windows Services → `postgresql-x64-XX` → Check if it's **Running**. If not, right-click → Start
> - Check if port 5432 is correct
> - Check if the password is correct
> - Check if a firewall is blocking the connection

---

### 🐳 METHOD 2: Using Docker

> [!TIP]
> With Docker, you don't need to install PostgreSQL! You just run a container. It's clean, fast, and easy to remove.

#### 7.2a — Install Docker (if not installed)

1. [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/) → Download Docker Desktop for Windows
2. Install → Restart your computer
3. Open Docker Desktop → ✅ Confirm "Docker Desktop is running"

#### 7.2b — Create Docker Compose File

Create a `docker-compose.yml` file in your project folder:

```yaml
version: '3.8'

services:
  postgis:
    image: postgis/postgis:16-3.4
    container_name: sl_bia_postgis
    environment:
      POSTGRES_DB: SL_BIA_Aerial_Info
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres123
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

> [!NOTE]
> The `postgis/postgis:16-3.4` image includes **both** PostgreSQL 16 + PostGIS 3.4. No need to install them separately!

#### 7.2c — Run the Docker Container

Open PowerShell / Terminal (in the project folder):

```powershell
docker-compose up -d
```

Output:
```
✔ Container sl_bia_postgis  Started
```

**Check if the container is running:**
```powershell
docker ps
```
The `sl_bia_postgis` container should show **Up** status.

#### 7.2d — Enable PostGIS Extension (Docker)

PostGIS auto-enables when using the `postgis/postgis` image. But confirm:

```powershell
docker exec -it sl_bia_postgis psql -U postgres -d SL_BIA_Aerial_Info -c "CREATE EXTENSION IF NOT EXISTS postgis;"
```

✅ Output: `CREATE EXTENSION`

#### 7.2e — Connect to QGIS (Docker)

1. QGIS → Browser Panel → Right-click `PostGIS` → **`New Connection...`**
2. Fill in:

| Field | Value |
|-------|-------|
| **Name** | `SL_BIA_Aerial_Info` |
| **Host** | `localhost` |
| **Port** | `5432` |
| **Database** | `SL_BIA_Aerial_Info` |
| **User name** | `postgres` |
| **Password** | `postgres123` |

3. `Test Connection` → ✅ Success!
4. Click `OK`

> [!TIP]
> **Docker stop/start:**
> - Stop: `docker-compose down` (data is saved in the volume)
> - Start: `docker-compose up -d`
> - After computer restart, open Docker Desktop and start the container

---

### ☁️ METHOD 3: Supabase (Cloud PostgreSQL)

> [!NOTE]
> Supabase's free tier provides a PostgreSQL database with PostGIS extension support. No installation needed — set up through the browser, connect from QGIS.

#### 7.3a — Create a Supabase Account

1. [supabase.com](https://supabase.com/) → Click **Start your project**
2. Sign in with your GitHub account (or use email)
3. ✅ The Dashboard will open

#### 7.3b — Create a New Project

1. Click **New Project**
2. Fill in:
   - **Organization**: Select your default org
   - **Name**: `SL_BIA_Aerial_Info`
   - **Database Password**: Set a strong password (Ex: `MyBIA_2024!secure`) — **Save this password!**
   - **Region**: Select the closest region (Ex: `Southeast Asia (Singapore)`)
3. Click **Create new project**
4. ⏳ Wait 1-2 minutes — the project will be set up

#### 7.3c — Enable PostGIS Extension

1. Click **SQL Editor** in the left menu
2. New Query:
```sql
CREATE EXTENSION IF NOT EXISTS postgis;
```
3. Click **Run**
4. ✅ "Success. No rows returned" — PostGIS is enabled!

#### 7.3d — Get Connection Details

1. Click **Project Settings** (gear icon) in the left menu
2. Click the **Database** section
3. Click the `URI` tab in the **Connection string** section
4. Note down these details:

| Detail | Where to Find | Example |
|--------|--------------|---------|
| **Host** | In the connection string | `db.xxxxxxxxxxxx.supabase.co` |
| **Port** | Default | `5432` |
| **Database** | Default | `postgres` |
| **User** | Default | `postgres` |
| **Password** | The password you set | `MyBIA_2024!secure` |

> [!WARNING]
> **Use Direct Connection** (NOT the Pooler connection).
> - ✅ Use: `Host: db.xxxxxxxxxxxx.supabase.co` Port: `5432`
> - ❌ Don't use: Pooler connection (port 6543)

#### 7.3e — Connect to QGIS (Supabase)

1. QGIS → Browser Panel → Right-click `PostGIS` → **`New Connection...`**
2. Fill in:

| Field | Value |
|-------|-------|
| **Name** | `SL_BIA_Aerial_Info` |
| **Host** | `db.xxxxxxxxxxxx.supabase.co` (your project host) |
| **Port** | `5432` |
| **Database** | `postgres` |
| **SSL mode** | **require** (important!) |
| **User name** | `postgres` |
| **Password** | The password you set |

3. `Test Connection` → ✅ Success!
4. Click `OK`

> [!CAUTION]
> **Supabase limitations:**
> - Free tier: **500MB** database storage (sufficient for Task C)
> - Requires internet connection (cannot work offline)
> - Data upload **may be slow** (cloud connection)
> - 7 days inactive → project pauses (resume from the dashboard)

> [!TIP]
> **For assessment submission:** If you use Supabase, the Supabase SQL Editor/Dashboard will appear in your screenshots — that's fine. But mention in your report: "PostgreSQL hosted on Supabase cloud platform with PostGIS extension".

---

### 7.4 — Create Tables (Common to All Methods)

> [!NOTE]
> Regardless of which of the 3 methods above you used, from this point forward the steps are the **same for all**.

**Using pgAdmin / Supabase SQL Editor / Docker exec:**

```sql
-- Buildings table
CREATE TABLE buildings (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    type VARCHAR(50),
    size NUMERIC(15,3),
    geom GEOMETRY(Polygon, 5234)
);

-- Radar locations table
CREATE TABLE radar_locations (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    type VARCHAR(50),
    size NUMERIC(15,3),
    geom GEOMETRY(Point, 5234)
);

-- Airport places table
CREATE TABLE airport_places (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    type VARCHAR(50),
    size NUMERIC(15,3),
    geom GEOMETRY(Point, 5234)
);

-- Suitability zones table
CREATE TABLE suitability_zones (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    type VARCHAR(50),
    size NUMERIC(15,3),
    geom GEOMETRY(Polygon, 5234)
);
```

### 7.5 — Import QGIS Layers into PostgreSQL

**Method A: QGIS DB Manager (Recommended):**

1. QGIS: `Database` → `DB Manager...`
2. PostGIS → Select your connection (`SL_BIA_Aerial_Info`)
3. Click Connect
4. Click the **`Import Layer/File`** button (top toolbar)
5. Settings:
   - Input: Select your shapefile layer (from dropdown)
   - Table: table name (Ex: `buildings`)
   - ✅ **Primary key**: `id`
   - ✅ **Geometry column**: `geom`
   - **Source SRID**: `5234`
   - **Target SRID**: `5234`
6. Click `OK` → Import!
7. ✅ Import your shapefile layers one by one

**Method B: QGIS Processing Toolbox:**

1. `Processing` → `Toolbox` → search "Export to PostgreSQL"
2. Input: Your layer
3. Fill in Database, schema settings
4. Click `Run`

### 7.6 — Run Spatial Queries on the Database

In pgAdmin / Supabase SQL Editor:

```sql
-- Total buildings count
SELECT COUNT(*) AS total_buildings FROM buildings;

-- Total building area
SELECT SUM(ST_Area(geom)) AS total_building_area FROM buildings;

-- Total suitability zone area
SELECT SUM(ST_Area(geom)) AS total_zone_area FROM suitability_zones;

-- Available area for radar deployment
SELECT 
    (SELECT SUM(ST_Area(geom)) FROM suitability_zones) -
    (SELECT SUM(ST_Area(geom)) FROM buildings) 
    AS available_area;
```

> [!TIP]
> **Take screenshots!** — Database creation, PostGIS extension, table creation, data import, query results — all needed for the appendix.

---

## STEP 8: Verify PostGIS Layers in QGIS

### 8.1 — Add PostGIS Layers

1. `Layer` → `Add Layer` → `Add PostGIS Layers...`
2. Select Connection: `SL_BIA_Aerial_Info` → Click `Connect`
3. Tables will be displayed → select all (or select the ones you need)
4. Click `Add`
5. ✅ Database layers will be displayed on the QGIS map

### 8.2 — Verify Data

1. Right-click the added PostGIS layer → `Open Attribute Table`
2. Check if data was imported correctly
3. Check if geometries are displaying at the correct locations on the map

---

## STEP 9: Final Map Design — Print Layout

### 9.1 — Map Styling

1. Right-click each layer → `Properties` → `Symbology`
2. Assign suitable colors/styles:

| Layer | Suggested Style |
|-------|----------------|
| Aerial Image | Background |
| Buildings | Red fill, black outline |
| Runway | Dark grey fill |
| Suitability Zone (PSR/SSR) | Semi-transparent blue |
| SMR Zone | Semi-transparent green |
| Air Force Base | Semi-transparent yellow |
| Radar Points | Large red/orange markers |
| Buffer rings | Dashed outlines |

### 9.2 — Create Print Layout

1. `Project` → `New Print Layout...`
2. Layout name: "BIA Radar Deployment Map"
3. Click `OK`

### 9.3 — Add Map Elements (MANDATORY for marks)

> [!CAUTION]
> The marking criteria clearly mentions: **North Arrow, Map Scale-Graphic, Map Scale-Numeric, Map Title, Map Legends** — all of these must be present on any map!

1. **Add Map**: `Add Item` → `Add Map` → Draw on the canvas
2. **Title**: `Add Item` → `Add Label` → text: "Geo Spatial Analysis for PSR, SSR & SMR Radar Deployment at BIA, Katunayake"
3. **Legend**: `Add Item` → `Add Legend` → Select map element
4. **Scale Bar (Graphic)**: `Add Item` → `Add Scale Bar`
5. **Scale Bar (Numeric)**: `Add Item` → `Add Label` → Add scale text (Ex: "1:25000")
6. **North Arrow**: `Add Item` → `Add North Arrow`
7. **Caption**: Add map caption (your name, date, CRS info)

### 9.4 — Export Map

1. `Layout` → `Export as PDF...` (to embed in the report)
2. `Layout` → `Export as Image...` (PNG — for the appendix)
3. ✅ Select high resolution (300 DPI)

> [!TIP]
> **Take screenshots!** — Final map, print layout process, capture everything.

---

## STEP 10: Add Base Map (Extra Marks)

The marking criteria "Excellent" band mentions "A suitable base map has been included".

### QuickMapServices Plugin:

1. `Plugins` → `Manage and Install Plugins...`
2. Search "QuickMapServices" → Install
3. `Web` → `QuickMapServices` → `OSM` → `OSM Standard`
4. ✅ An OpenStreetMap base map will be added
5. Drag the base map layer to the bottom in the Layers panel

---

## STEP 11: Report Writing — Critical Discussion

Cover these points in your report:

### Discussion Structure:

1. **Introduction to Radar Systems**
   - PSR (Primary Surveillance Radar) — what it does, why it's important
   - SSR (Secondary Surveillance Radar) — transponder-based, aircraft identification
   - SMR (Surface Movement Radar) — ground traffic monitoring

2. **Importance for BIA**
   - Increasing air traffic demands
   - Safety requirements (ICAO standards)
   - Modernization under the Millennium Renovation Project

3. **Site Selection Analysis**
   - SMR: 300m from Control Tower, 200m from RCP rationale
   - PSR/SSR: 2-3km from RCP rationale
   - Air Force base location advantage (security, access)

4. **Geo-spatial Findings**
   - Total buildings count in suitability area
   - Total building area
   - Available land area
   - Challenges (obstructions, existing structures)

5. **ICAO Compliance**
   - Clear line-of-sight
   - Electromagnetic interference minimization
   - Obstacle limitation standards

6. **Recommendations**
   - Specific location recommendations with GPS coordinates
   - Building relocation/demolition needs
   - Infrastructure requirements (power, access roads)

---

## 📋 FINAL CHECKLIST — Before Submission

| # | Item | Status |
|---|------|--------|
| 1 | Aerial image georeferenced (EPSG:5234) | ⬜ |
| 2 | All layers digitized with id, name, type, size columns | ⬜ |
| 3 | CRS = EPSG:5234 throughout | ⬜ |
| 4 | Buffer zones created (SMR 300m, PSR/SSR 2-3km) | ⬜ |
| 5 | Intersection with Air Force base done | ⬜ |
| 6 | Clip operation for buildings done | ⬜ |
| 7 | KML/KMZ files created from Google Earth | ⬜ |
| 8 | PostgreSQL database "SL_BIA_Aerial_Info" created | ⬜ |
| 9 | PostGIS extension enabled | ⬜ |
| 10 | Data imported to PostgreSQL | ⬜ |
| 11 | Total buildings count calculated | ⬜ |
| 12 | Total building area calculated | ⬜ |
| 13 | Total available land area calculated | ⬜ |
| 14 | Map has: North Arrow ✅ | ⬜ |
| 15 | Map has: Scale Bar (Graphic) ✅ | ⬜ |
| 16 | Map has: Scale Bar (Numeric) ✅ | ⬜ |
| 17 | Map has: Title ✅ | ⬜ |
| 18 | Map has: Legend ✅ | ⬜ |
| 19 | Map has: Base Map ✅ | ⬜ |
| 20 | Map properly captioned ✅ | ⬜ |
| 21 | Critical discussion written | ⬜ |
| 22 | Harvard referencing used | ⬜ |
| 23 | All screenshots in Appendix C | ⬜ |
| 24 | All data/script files ready for submission | ⬜ |

---

## ⚠️ Common Errors and Solutions

| Error | Cause | Solution |
|-------|-------|----------|
| Layer doesn't display correctly | Wrong CRS | Re-project to EPSG:5234 |
| Georeferencer high RMS error | Poor GCP placement | Re-do GCPs, use clearly identifiable points |
| Buffer tool doesn't work | CRS in degrees not meters | Convert to EPSG:5234 (meters) first |
| PostGIS extension error | PostGIS not installed | Install via Stack Builder |
| "No geometry column" in PostGIS | Import didn't include geometry | Re-import using DB Manager with geometry |
| Attribute table empty | Forgot to enter attributes during digitizing | Enter edit mode, click feature, enter values |
| Area calculation shows 0 | CRS issue | Use EPSG:5234 (projected, meters) |
| Map elements missing in PDF | Not added in Print Layout | Print Layout → Add Item → add all elements |

---

> [!TIP]
> **To achieve an Excellent grade (70-100)**, according to the marking criteria you need:
> 1. ✅ Excellent map with ALL required digitized information
> 2. ✅ ALL standard map elements (North Arrow, Scale-Graphic, Scale-Numeric, Title, Legends)
> 3. ✅ Aerial image georeferenced then digitized
> 4. ✅ Geo-processing tools used (buffering, clipping, intersection)
> 5. ✅ KML/KMZ files from Google Earth
> 6. ✅ PostgreSQL + PostGIS database "SL_BIA_Aerial_Info"
> 7. ✅ Suitable base map included
> 8. ✅ Map properly captioned
> 9. ✅ Screenshots in appendix
> 10. ✅ Excellent **critical** discussion
> 11. ✅ Proper Harvard citations and references
