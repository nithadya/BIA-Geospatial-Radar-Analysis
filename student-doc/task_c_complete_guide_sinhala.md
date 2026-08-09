# 🗺️ Task C - Complete Step-by-Step Guide
## Geo Spatial Analysis for PSR, SSR & SMR Radar System Deployment (30 Marks)

---

> [!IMPORTANT]
> මේක assessment එකේ **ලොකුම task එක** — 30 marks. QGIS, PostgreSQL, සහ Google Earth use කරන්න ඕන. පහල step by step ඔක්කොම explain කරලා තියෙනවා, error නැතුව කරන්න.

---

## 📋 Task C කරන්න ඕන දේවල් Summary

Assessment එකට අනුව, ඔයාට මේ දේවල් කරන්න ඕන:

1. **Aerial image එක Geo-reference** කරන්න (MANDATORY - මේක පලවෙනිම කරන්න ඕන)
2. **Digitize** කරන්න — vector layers හදලා (id, name, type, size columns ඕන)
3. **CRS: EPSG:5234** use කරන්න (Kandawala / Sri Lanka Grid)
4. **PSR/SSR සහ SMR radar** deploy කරන්න suitable locations identify කරන්න
5. **GPS data extract** කරන්න Google Earth වලින් KML/KMZ files use කරලා
6. **PostgreSQL Geo Spatial Database** — "`SL_BIA_Aerial_Info`" නමින් database එකක් හදන්න
7. **Geo-processing tools** use කරන්න (Buffer, Clip, Intersection)
8. **Calculate** කරන්න:
   - Suitability area එකේ total buildings ගණන
   - Buildings වලින් occupy වෙන total land area
   - Radar deployment වලට available total land area
9. **Map elements** add කරන්න (North Arrow, Scale Bar, Title, Legend)
10. **Critical discussion** ලියන්න

---

## 🔧 ඔයාට ඕන Software

| Software | Purpose |
|----------|---------|
| **QGIS** (3.x recommended) | Main GIS software — georeferencing, digitizing, geo-processing, map making |
| **PostgreSQL + PostGIS** | Geo Spatial Database හදන්න |
| **Google Earth Pro** | KML/KMZ files හදන්න, GPS coordinates extract කරන්න |

---

## 📁 ඔයාට දීලා තියෙන Data Files

ඔයාගේ [Question-(c)](file:///c:/Users/mihisara/Desktop/BI-Project/data/Question-(c)) folder එකේ මේ files තියෙනවා:

| File | Type | Description |
|------|------|-------------|
| `Bandaranayake Airport Areal Latest3_1_modified.tif` | Raster (Aerial Image) | BIA aerial photo — මේක georef කරන්න ඕන |
| `Airport Places.shp` + `.kml` | Shapefile + KML | Airport places — point data |
| `Airport Places New.shp` | Shapefile | Updated airport places |
| `Admin Regions.shp` | Shapefile | Administrative regions |
| `Air Force Base Katunayake.shp` | Shapefile | Air Force base boundary |
| `Air Force Base Region.shp` | Shapefile | Air Force base region |

---

# 🚀 STEP-BY-STEP GUIDE

---

## STEP 1: QGIS Project Setup (පළවෙනිම කරන්න)

### 1.1 — QGIS Open කරලා New Project එකක් හදන්න

1. QGIS Desktop open කරන්න
2. `Project` → `New` click කරන්න
3. `Project` → `Save As...` → ඔයාගේ project folder එකේ save කරන්න (Ex: `GIS-Task-C.qgz`)

### 1.2 — CRS Set කරන්න (EPSG:5234)

> [!CAUTION]
> CRS එක **EPSG:5234 (Kandawala / Sri Lanka Grid)** ලෙස set කරන්න ඕන. Assessment එකේ specifically mention කරලා තියෙනවා. වෙන CRS එකක් use කළොත් marks ලැබෙන්නේ නෑ.

1. QGIS bottom right corner එකේ CRS button එක click කරන්න (default "EPSG:4326" වගේ show වෙනවා)
2. Search bar එකේ `5234` type කරන්න
3. **"Kandawala / Sri Lanka Grid - EPSG:5234"** select කරන්න
4. `Apply` → `OK` click කරන්න
5. ✅ Bottom right එකේ `EPSG:5234` display වෙනවා confirm කරන්න

> [!TIP]
> **Screenshot ගන්න!** — CRS set කරපු එක appendix එකට ඕන.

---

## STEP 2: Aerial Image Geo-Referencing (MANDATORY FIRST STEP)

> [!WARNING]
> Assessment brief එකේ clearly කියනවා: *"It is mandatory to do the image geo-referencing before initiation of the digitization."* මේක skip කළොත් marks cut වෙනවා!

### 2.1 — Georeferencer Tool Open කරන්න

1. QGIS menu: `Layer` → `Georeferencer` (QGIS 3.26+ — older versions: `Raster` → `Georeferencer`)
2. Georeferencer window open වෙනවා

### 2.2 — Aerial Image Load කරන්න

1. Georeferencer window එකේ: `File` → `Open Raster...`
2. `Bandaranayake Airport Areal Latest3_1_modified.tif` file එක browse කරලා select කරන්න
3. Image එක Georeferencer window එකේ display වෙනවා

### 2.3 — Transformation Settings Set කරන්න

1. Georeferencer menu: `Settings` → `Transformation Settings...`
2. මේ values set කරන්න:

| Setting | Value |
|---------|-------|
| Transformation type | **Polynomial 1** |
| Resampling method | **Nearest Neighbour** |
| Target SRS | **EPSG:5234** |
| Output Raster | ඔයාගේ folder එකේ save — Ex: `BIA_georeferenced.tif` |
| Compression | **LZW** |
| ✅ Load in project when done | Check කරන්න |

3. `OK` click කරන්න

### 2.4 — Ground Control Points (GCPs) Add කරන්න

> [!IMPORTANT]
> GCP points minimum **4ක්** (ideally 6-8ක්) add කරන්න ඕන. මේ points එක්ක Google Earth/Google Maps use කරලා real GPS coordinates ගන්න.

---

#### 🔍 Part A: Aerial Image එකේ Point එකක් Select කරන්න

1. QGIS Georeferencer window එකේ ඔයාගේ aerial image load වෙලා තියෙනවා
2. Image එක **zoom in** කරන්න (mouse scroll wheel)
3. **Clearly identifiable** point එකක් හොයන්න — මේ වගේ දේවල්:

| හොයන්න ඕන දේ | Example |
|---------------|---------|
| 🏢 Building corner | Terminal building එකේ corner එකක් |
| ✈️ Runway edge/corner | Runway එකේ threshold marking |
| 🛣️ Road intersection | Road දෙකක් හමුවෙන තැන |
| 🔲 Roof corner | Building එකක roof corner |

> ඔයාගේ aerial image එකේ runway, buildings, roads clearly පේනවා — ඒ features use කරන්න!

4. Georeferencer toolbar එකේ **"Add GCP Point"** button click කරන්න — මේ icon එක:
   - 🟡 **Yellow dot with a plus (+) sign**
   - Toolbar එකේ left side එකේ තියෙනවා

5. දැන් aerial image එකේ ඔයා select කරපු **point එක exactly click** කරන්න (Ex: building corner එකක් click කරන්න)

6. Click කරාම **dialog box** එකක් open වෙනවා — "Enter Map Coordinates" කියලා

---

#### 🌍 Part B: Google Earth එකෙන් Same Point එකේ Coordinates ගන්න

**මේක important part එක — parallel වැඩ දෙකක් කරනවා:**

7. **Google Earth Pro** open කරන්න (QGIS minimize කරලා)
8. Search bar එකේ type: `Bandaranaike International Airport` → Enter
9. ඔයා QGIS aerial image එකේ click කරපු **exact same point** එක Google Earth එකේ හොයන්න

   **Example:** ඔයා QGIS එකේ Terminal building එකේ top-left corner click කළා නම්, Google Earth එකේත් **ඒම Terminal building එකේ top-left corner** එක හොයන්න

10. Google Earth එකේ ඒ point එක උඩට mouse pointer එක ගෙනියන්න (**click කරන්න එපා, hover කරන්න**)
11. **Screen bottom bar** එකේ coordinates display වෙනවා:
    ```
    7°10'15.23"N  79°53'02.45"E  elev 8m
    ```
    හෝ decimal format එකේ:
    ```
    7.170897°  79.884015°
    ```

> [!TIP]
> **Decimal format ගන්න:** Google Earth bottom bar එකේ coordinates format change කරන්න: `Tools` → `Options` → `Show Lat/Long` → **Decimal Degrees** select කරන්න. ඒකෙන් decimal format එකේ coordinate ලැබෙනවා — QGIS enter කරන්න ලේසියි.

12. ඒ **Latitude** සහ **Longitude** values note කරන්න / remember කරන්න

---

#### 📝 Part C: Coordinates Enter කරන්න QGIS Georeferencer වලට

13. ආපහු **QGIS Georeferencer** window එකට එන්න
14. Open වෙලා තියෙන dialog box එකේ:

| Field | Enter කරන්න |
|-------|-------------|
| **X / East** | **Longitude** value (Ex: `79.884015`) |
| **Y / North** | **Latitude** value (Ex: `7.170897`) |
| **CRS** | `EPSG:4326 - WGS 84` (Google Earth coordinates WGS84 වලින් — QGIS auto-convert කරනවා EPSG:5234 වලට) |

> [!WARNING]
> **X = Longitude (79.xxx), Y = Latitude (7.xxx)** — මේක mix up කරන්න එපා! Longitude (79) X field එකට, Latitude (7) Y field එකට.

15. **OK** click කරන්න
16. ✅ GCP point 1 add වුනා! Georeferencer window එකේ **red dot** එකක් display වෙනවා

---

#### 🔁 Part D: Repeat — Minimum 4 Points Add කරන්න

**තව points 3-5ක් add කරන්න same process එකෙන්:**

17. ආයෙමත් **"Add GCP Point"** click → aerial image එකේ **වෙන point** එකක් click → Google Earth එකෙන් same point එකේ coordinates ගන්න → enter කරන්න

**Point Placement Strategy — Image එකේ spread out කරන්න:**

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
> Points ඔක්කොම **එක තැනකට එකතු කරන්න එපා!** Image එකේ **spread out** වෙන්න ඕන — corners සහ middle cover කරන්න. ඒකෙන් accuracy වැඩි වෙනවා.

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
> ඉහත coordinates approximate values. ඔයාම Google Earth එකෙන් accurate values ගන්න ඕන. Image එකේ clearly identify වෙන points use කරන්න.

---

#### ✅ Part E: RMS Error Check කරන්න

18. Minimum 4 points add කරාට පස්සේ, Georeferencer window එකේ **GCP table** (bottom panel) බලන්න:

| GCP | Source X | Source Y | Dest X | Dest Y | **Residual** |
|-----|----------|----------|--------|--------|-------------|
| 1 | 234 | 567 | 79.884 | 7.170 | **1.23** |
| 2 | 890 | 123 | 79.891 | 7.181 | **0.89** |
| ... | ... | ... | ... | ... | ... |

- **Residual** column එකේ values බලන්න — **low values = good** (< 5 pixels ideal)
- Bottom එකේ **Mean error** / **Total RMS error** display වෙනවා
- Error ගොඩක් නම් (> 10), ඒ point එක **delete** කරලා re-do කරන්න (right-click → Delete Point)

---

#### 🎯 GCP Process Quick Summary

```
QGIS Aerial Image එකේ click  →  Google Earth එකේම point එක hover
         ↓                              ↓
   dialog open වෙනවා             coordinates බලන්න (bottom bar)
         ↓                              ↓
   X = Longitude (79.xxx),  Y = Latitude (7.xxx) enter කරන්න
         ↓
   OK → GCP added! ✅
   
   Repeat 4-8 times → Check RMS Error → Start Georeferencing ▶
```

### 2.5 — Georeferencing Run කරන්න

1. Georeferencer toolbar: **"Start Georeferencing"** button click කරන්න (green play icon)
2. Process complete වෙනවා
3. QGIS main window එකේ georeferenced image automatically load වෙනවා
4. ✅ Image එක correct location එකේ display වෙනවද check කරන්න

> [!TIP]
> **Screenshot ගන්න!** — GCP table එක, Transformation settings, georeferenced result — ඔක්කොම screenshot ගන්න appendix එකට.

---

## STEP 3: Google Earth — KML/KMZ Files Create කරන්න

### 3.1 — Google Earth Pro Open කරලා Placemarks Create කරන්න

Assessment brief එකට අනුව KML/KMZ files use කරන්න ඕන. මේවා GPS data extract කරන්නයි key locations mark කරන්නයි use කරනවා.

1. **Google Earth Pro** open කරන්න
2. BIA (Bandaranaike International Airport) search කරන්න
3. **Key Locations Mark කරන්න** (Placemark tool use කරලා — yellow pin icon):

| Location | Type | Why? |
|----------|------|------|
| CMB Control Tower | Point | Reference point |
| Runway Center Point (RCP) | Point | PSR/SSR distance measure කරන්න |
| Proposed SMR location | Point | ~300m from Control Tower, ~200m from RCP |
| Proposed PSR/SSR location | Point | ~2km from RCP, within Air Force base |
| Airport Terminal | Point | Digitize කරන්න reference |
| Air Force Base | Polygon | Area boundary mark |

### 3.2 — Placemark Details Enter කරන්න

Each placemark add කරද්දී:
1. **Name** field එකට descriptive name දෙන්න (Ex: "CMB Control Tower", "Proposed PSR SSR Location")
2. **Latitude/Longitude** note කරන්න
3. `OK` click කරන්න

### 3.3 — KML/KMZ Export කරන්න

1. Left panel එකේ "My Places" / ඔයා create කරපු folder එක right-click කරන්න
2. `Save Place As...` click කරන්න
3. File type: **KML** හෝ **KMZ** select කරන්න
4. ඔයාගේ project folder එකේ save කරන්න (Ex: `BIA_Radar_Locations.kml`)

### 3.4 — KML QGIS වලට Import කරන්න

1. QGIS: `Layer` → `Add Layer` → `Add Vector Layer...`
2. Source එක browse කරලා ඔයාගේ `.kml` file select කරන්න
3. `Add` click කරන්න
4. ✅ Points QGIS map එකේ correct locations වල display වෙනවා confirm කරන්න

> [!IMPORTANT]
> **Import / CRS Troubleshooting Note:** KML file එක Import කළ පසු QGIS map එකේ points නොපෙනී යන්නේ නම් හෝ වෙනත් තැනක පෙනෙන්නේ නම්, ඊට හේතුව Google Earth හි default CRS එක WGS 84 (EPSG:4326) වීමයි. එම KML Layer එක උඩ Right-click කර **`Export` → `Save Features As...`** ගොස්, **CRS එක `EPSG:5234 (Kandawala / Sri Lanka Grid)`** ලෙස තෝරා Save (Re-export) කරගන්න. එවිට points සියල්ල Aerial Image එක උඩ නිවැරදි ස්ථානවල පැහැදිලිව Display වේ!

> [!TIP]
> **Screenshot ගන්න!** — Google Earth placemark creation, KML save, QGIS import — ඔක්කොම.

---

## STEP 4: Provided Shapefiles Load කරන්න

### 4.1 — Shapefiles Add කරන්න

1. QGIS: `Layer` → `Add Layer` → `Add Vector Layer...`
2. One by one මේ shapefiles add කරන්න:
   - `Airport Places New.shp`
   - `Airport Places.shp`
   - `Admin Regions.shp`
   - `Air Force Base Katunayake.shp`
   - `Air Force Base Region.shp`
3. Each layer add කරද්දී CRS prompt ආවොත් **EPSG:5234** select කරන්න

### 4.2 — Layers CRS Re-project කරන්න (if needed)

ඔයාගේ shapefiles EPSG:4326 (WGS84) වලින් තියෙන්න පුළුවන්. ඒවා EPSG:5234 වලට convert කරන්න:

1. Layer එක right-click → `Export` → `Save Features As...`
2. Format: **ESRI Shapefile**
3. CRS: **EPSG:5234** select කරන්න
4. Filename: Ex: `Airport_Places_5234.shp`
5. `OK` click කරන්න
6. ✅ Re-projected layer add වෙනවා

---

## STEP 5: Digitization — Vector Layers Create කරන්න

> [!IMPORTANT]
> Assessment brief එකේ කියනවා: *"Every vector layer attribute table should contain suitable data in columns id, name, type, and size"*. මේ 4 columns ඔබේ every layer එකේ attribute table එකේ තියෙන්නම ඕන!

### 5.1 — New Vector Layer එකක් Create කරන එක (Example: Buildings Layer)

1. QGIS: `Layer` → `Create Layer` → `New Shapefile Layer...`
2. Settings:

| Setting | Value |
|---------|-------|
| File name | Ex: `BIA_Buildings.shp` |
| Geometry type | **Polygon** |
| CRS | **EPSG:5234** |

3. **Fields add කරන්න** (New Field section එකේ):

| Field Name | Type | Length |
|------------|------|--------|
| id | Integer | 10 |
| name | String | 100 |
| type | String | 50 |
| size | Real (Decimal) | 15, 3 |

   - Each field add කරද්දී: Name type කරලා, Type select කරලා, **"Add to Fields List"** button click කරන්න
4. `OK` click කරන්න
5. ✅ Empty layer එක Layers panel එකේ add වෙනවා

### 5.2 — Create කරන්න ඕන Layers List

මේ layers ඔක්කොම create කරලා digitize කරන්න:

| Layer Name | Geometry | Purpose |
|------------|----------|---------|
| `BIA_Buildings` | Polygon | Airport area එකේ buildings |
| `BIA_Runway` | Polygon / Line | Runway digitize |
| `BIA_Taxiways` | Line / Polygon | Taxiways |
| `BIA_Terminal` | Polygon | Terminal building |
| `BIA_Roads` | Line | Airport roads |
| `BIA_Radar_PSR_SSR` | Point | Proposed PSR/SSR location |
| `BIA_Radar_SMR` | Point | Proposed SMR location |
| `BIA_Control_Tower` | Point | Control Tower location |
| `BIA_RCP` | Point | Runway Center Point |

### 5.3 — Digitizing කරන්න (Drawing Features)

1. Digitize කරන layer එක select කරන්න (Layers panel එකේ click)
2. **Toggle Editing** button click කරන්න (pencil icon 🖊️)
3. **"Add Polygon Feature"** (හෝ Point/Line) button click කරන්න
4. Georeferenced aerial image එක reference කරමින් feature එක draw කරන්න:
   - Polygon: Click click click කරලා boundary draw → right-click to finish
   - Point: Click once
   - Line: Click click → right-click to finish
5. Dialog box එකක් open වෙනවා — attribute values enter කරන්න:
   - **id**: 1, 2, 3... (sequential)
   - **name**: "Terminal Building 1", "Hangar A", etc.
   - **type**: "Terminal", "Hangar", "Office", "Residential", etc.
   - **size**: `0` ලෙස දමන්න (පසුව QGIS එකෙන් Auto-Calculate කරනු ලැබේ)
6. `OK` click කරන්න
7. Feature drawn!
8. Continue drawing more features...
9. Done ද? **Save Layer Edits** button click කරන්න (floppy disk icon)
10. **Toggle Editing** off කරන්න

> [!TIP]
> **`size` ($m^2$) Auto-Calculate කරන ආකාරය:**
> ඩ්‍රෝ කරද්දී `size` සඳහා අතින් අගයන් ගැසීමට අවශ්‍ය නැත (නිකන්ම `0` Enter කරන්න). සියලුම Features ඩ්‍රෝ කර අවසන් වූ පසු:
> 1. Layer එක Right-click → **`Open Attribute Table`** යන්න.
> 2. **Field Calculator** icon එක (🧮 abacus icon) Click කරන්න (Ctrl + I).
> 3. **`Update existing field`** Check කර `size` field එක තෝරන්න.
> 4. Expression එකට **`$area`** ලෙස Type කර **OK** Click කරන්න.
> QGIS මඟින් සියලුම Polygons වල exact square meters ($m^2$) අගය Attribute table එකට Auto-calculate කර පුරවනු ඇත!

> [!WARNING]
> Digitize කරද්දී regularly save කරන්න! QGIS crash වුනොත් data lose වෙනවා.

### 5.4 — Buildings Digitize කරන්න (ලොකුම part එක)

> [!IMPORTANT]
> **ප්‍රමාණාත්මක සටහන සහ ක්‍රමවේද සාධාරණීකරණය (Building Scope & Academic Justification):**
> 
> 1. **Building Digitization Scope:** මුළු සිතියමේම ඇති සියලුම ගොඩනැගිලි (thousands of buildings) digitize කිරීමට අවශ්‍ය නැත! BIA Airport Premises සහ Katunayake Air Force Base ප්‍රදේශය වටා ඇති ප්‍රධාන ගොඩනැගිලි 20 - 40ක් පමණ (representative buildings) Trace/Digitize කිරීම ප්‍රමාණවත් වේ.
> 
> 2. **Digitizing & Buffer Workflow (ක්‍රමවේද 2ක තේරීම):**
>    - **ක්‍රමය A (Clip Tool Automation - Recommended):** පළමුව Airport/Air Force base අවට ඇති ගොඩනැගිලි digitize කරන්න. Buffer සීමාවන් ගැන වදවීමට අවශ්‍ය නැත. Step 6 හිදී `Clip` Tool එක run කළ පසු, QGIS මඟින් Auto-select කර exact radar suitability zone එක ඇතුළත ඇති ගොඩනැගිලි පමණක් කපා වෙන්කර දෙනු ඇත.
>    - **ක්‍රමය B (Visual Guide Approach):** නැතහොත්, පළමුව Step 6.1 හි `Buffer` run කර සිතියම මත suitability zone වටරවුම පෙනෙන්න තබාගෙන, එම වටරවුම ඇතුළත ඇති ගොඩනැගිලි පමණක් digitize කරන්න.
> 
> 3. **Marking Criteria & Academic Justification (ඇගයීම් නිර්ණායක සාධාරණීකරණය):**
>    - Task C හි ලකුණු 30 ප්‍රදානය කෙරෙන්නේ Spatial Analysis & Geo-processing ශක්‍යතාවය වෙනුවෙනි. 
>    - `Clip` සහ `Buffer` වැනි GIS Geoprocessing tools භාවිතයෙන් Suitability boundary එකක් ගණනය කර, ඊට අදාළ ගොඩනැගිලි වෙන්කර ගැනීම (spatial overlay analysis) මඟින් ඔබ අතින් (manually) උපකල්පනය කරනවාට වඩා විද්‍යාත්මක සහ නිවැරදි geospatial analytical process එකක් අනුගමනය කර ඇති බව මහාචාර්ය/ඇගයුම්කරුට (Assessor) තහවුරු වේ.

> [!CAUTION]
> **සාමාන්‍යයෙන් වෙන වැරැද්දක් නොකිරීමට වගබලාගන්න (Individual Polygons vs. One Giant Box):**
> ❌ **කරන්න එපා:** මුළු Airport Area එක හෝ Apron එකම වහෙන සේ එක විශාල රතු/දුඹුරු පෙට්ටියක් (One Giant Bounding Box Polygon) එකපාර ඇඳින්න එපා! එසේ කළහොත් QGIS හි Count වන්නේ 1 Building එකක් පමණි.
> ✅ **නිවැරදි ක්‍රමය:** Aerial Image එක ගොඩනැගිලි පැහැදිලිව පෙනෙන සේ **Zoom In** කරන්න. ඉන්පසු එක එක ගොඩනැගිල්ල (Terminal, Hangars, Offices, nearby structures) වටේට වෙන වෙනම (Individual Polygon Feature) Click කර ඇඳලා Finish කරන්න. එවිට Attribute Table එකේ Rows 20–40ක් (Building 1, Building 2...) ලෙස එක්රැස් වේ.
> 💡 **Pro Tip (Opacity 50%):** ගොඩනැගිලි ඩ්‍රෝ කරද්දී යට තියෙන Photo එක පෙනීමට, `BIA_Buildings` Layer එක උඩ Right-click කර `Properties` → `Symbology` → `Opacity` slider එක **50%** ට අඩු කරන්න.

Aerial image එක zoom in කරලා:
1. Suitability area එක (PSR/SSR 2-3km zone, SMR zone) ඇතුලේ **සෑම building** එකම trace/draw කරන්න
2. Each building එකට unique id, name, type, size attribute values fill කරන්න
3. ✅ Attribute table open කරලා check කරන්න — `Right-click layer` → `Open Attribute Table`

---

## STEP 6: Geo-Processing — Buffer, Clip, Intersection

මේක **ඉතාම important** — marks ගොඩක් ලැබෙනවා geo-processing tools use කළොත්.

### 6.1 — Buffer Analysis (Radar Coverage Zones)

**SMR Buffer (Control Tower එකෙන් ~300m):**
1. Control Tower point layer select කරන්න
2. `Vector` → `Geoprocessing Tools` → `Buffer...`
3. Settings:
   - Input layer: `BIA_Control_Tower`
   - Distance: **300** (meters — CRS EPSG:5234 meters units)
   - Segments: 36
   - Output: `SMR_Buffer_300m.shp`
4. `Run` click කරන්න

**PSR/SSR Buffer (RCP එකෙන් 2km-3km zone):**

පලවෙනි buffer: 
1. RCP point layer select කරන්න
2. `Vector` → `Geoprocessing Tools` → `Buffer...`
   - Input: `BIA_RCP`
   - Distance: **3000** (3km = 3000m)
   - Output: `PSR_SSR_Buffer_3km.shp`
3. `Run`

දෙවෙනි buffer:
4. Again Buffer:
   - Input: `BIA_RCP`
   - Distance: **2000** (2km = 2000m)
   - Output: `PSR_SSR_Buffer_2km.shp`
5. `Run`

**Ring Zone create කරන්න (2km-3km area):**
6. `Vector` → `Geoprocessing Tools` → `Difference...`
   - Input: `PSR_SSR_Buffer_3km`
   - Overlay: `PSR_SSR_Buffer_2km`
   - Output: `PSR_SSR_Suitability_Zone.shp`
7. `Run`
8. ✅ මේකෙන් 2km සිට 3km දක්වා donut-shaped zone එකක් ලැබෙනවා — PSR/SSR deploy කරන්න suitable zone!

### 6.2 — Intersection (Air Force Base + Suitability Zone)

Assessment brief කියනවා PSR/SSR ideally Air Force base premises ඇතුලේ install කරන්න ඕන:

1. `Vector` → `Geoprocessing Tools` → `Intersection...`
   - Input: `PSR_SSR_Suitability_Zone`
   - Overlay: `Air Force Base Katunayake` (or Air Force Base Region)
   - Output: `PSR_SSR_Ideal_Zone.shp`
2. `Run`
3. ✅ මේකෙන් Air Force base ඇතුලේ + 2-3km zone ඇතුලේ overlap වෙන area එක ලැබෙනවා

### 6.3 — Clip (Buildings within Suitability Area)

Suitability area ඇතුලේ buildings identify කරන්න:

1. `Vector` → `Geoprocessing Tools` → `Clip...`
   - Input: `BIA_Buildings` (ඔයා digitize කරපු buildings layer)
   - Overlay: `PSR_SSR_Ideal_Zone`
   - Output: `Buildings_in_Radar_Zone.shp`
2. `Run`
3. ✅ Suitability area ඇතුලේ buildings විතරක් show වෙනවා

### 6.4 — Calculate Required Statistics

**Total number of buildings:**
1. `Buildings_in_Radar_Zone` layer right-click → `Open Attribute Table`
2. Bottom bar එකේ **feature count** show වෙනවා — ඒක total buildings ගණන

**Total land area (buildings):**
1. Attribute table open → `Field Calculator` (abacus icon) click
2. ✅ Create new field: `area_sqm`
3. Expression: `$area`
4. `OK` click
5. `Processing` → `Toolbox` → search "Basic Statistics" → run on `area_sqm` field
6. **Sum** value = Total building area

**Total available land area for radar:**
1. `PSR_SSR_Ideal_Zone` layer attribute table open → Field Calculator
2. Expression: `$area`
3. ✅ ඒක total zone area
4. Available area = Zone area − Total building area

> [!TIP]
> **Screenshot ගන්න!** — Buffer zones, Intersection results, Attribute tables, Area calculations — ඔක්කොම.

---

## STEP 7: PostgreSQL + PostGIS — Geospatial Database Create කරන්න

> [!IMPORTANT]
> Database name exactly **"`SL_BIA_Aerial_Info`"** ලෙස දෙන්න ඕන — assessment brief එකේ specify කරලා තියෙනවා.

> [!NOTE]
> PostgreSQL + PostGIS setup කරන්න methods **3ක්** තියෙනවා. ඔයාට convenient method එක select කරන්න. ඔක්කොම methods වලින් QGIS connect කරන්න පුළුවන්.

| Method | Difficulty | Best For |
|--------|-----------|----------|
| 🖥️ **Method 1: Local Install** | Medium | PostgreSQL already install කරලා තියෙන අය / traditional approach |
| 🐳 **Method 2: Docker** | Easy | Docker install කරලා තියෙන අය / clean setup ඕන අය |
| ☁️ **Method 3: Supabase** | Easiest | Install කරන්න බැරි / cloud solution ඕන අය |

---

### 🖥️ METHOD 1: Local PostgreSQL Install

#### 7.1a — PostgreSQL + PostGIS Install කරන්න

**PostgreSQL install කරලා නැත්නම්:**
1. [postgresql.org/download/windows](https://www.postgresql.org/download/windows/) → Download
2. Installer run කරන්න
3. Install කරද්දී:
   - Port: **5432** (default)
   - Password: ඔයාට මතක තියෙන password එකක් දෙන්න (Ex: `postgres123`)
   - ✅ Install complete වෙද්දී **Stack Builder** launch checkbox check කරන්න

**PostGIS Install (Stack Builder):**
4. Stack Builder open වෙනවා
5. DropDown එකෙන් ඔයාගේ PostgreSQL version select කරන්න (Ex: `PostgreSQL 16 on port 5432`)
6. `Next` click
7. **Spatial Extensions** expand → ✅ **PostGIS 3.x Bundle** check කරන්න
8. `Next` → `Next` → Install
9. ✅ PostGIS installed!

**PostgreSQL already install කරලා තියෙනවා, PostGIS නැත්නම්:**
1. Windows Start Menu → **Stack Builder** search කරලා open
2. ඉහත steps 5-9 follow කරන්න

#### 7.1b — pgAdmin Configure කරන්න

1. Windows Start Menu → **pgAdmin 4** open
2. First time open කරද්දී master password set කරන්න
3. Left panel: `Servers` → `PostgreSQL XX` expand
4. Password prompt ආවොත් install time එකේ set කරපු password enter

#### 7.1c — Database Create කරන්න (pgAdmin)

1. `Servers` → `PostgreSQL XX` → **Databases** right-click → `Create` → `Database...`
2. **Database** tab:
   - Database name: **`SL_BIA_Aerial_Info`**
   - Owner: `postgres`
3. `Save` click
4. ✅ Left panel එකේ `SL_BIA_Aerial_Info` database display වෙනවා

#### 7.1d — PostGIS Extension Enable කරන්න

1. Left panel: `SL_BIA_Aerial_Info` database click
2. Top menu: `Tools` → `Query Tool` (හෝ database right-click → Query Tool)
3. Query editor එකේ type:
```sql
CREATE EXTENSION postgis;
```
4. **▶ Execute** button click (හෝ F5)
5. ✅ Message: "Query returned successfully" — PostGIS enabled!

**Verify PostGIS:**
```sql
SELECT PostGIS_Version();
```
Result එකේ version number display වෙනවා (Ex: `3.4 USE_GEOS=1 USE_PROJ=1`)

#### 7.1e — QGIS Connect කරන්න (Local)

1. QGIS open → Left side **Browser Panel** එකේ `PostGIS` right-click → **`New Connection...`**
2. Dialog box එකේ fill කරන්න:

| Field | Value |
|-------|-------|
| **Name** | `SL_BIA_Aerial_Info` |
| **Host** | `localhost` |
| **Port** | `5432` |
| **Database** | `SL_BIA_Aerial_Info` |

3. **Authentication** section:
   - ✅ **"Store"** checkbox check
   - **User name**: `postgres`
   - **Password**: install time password

4. **`Test Connection`** button click
5. ✅ "Connection to SL_BIA_Aerial_Info was successful" message ආවොත් හරි!
6. `OK` click

> [!WARNING]
> **"Connection failed" error ආවොත්:**
> - PostgreSQL service run වෙනවද check: Windows Services → `postgresql-x64-XX` → **Running** ද බලන්න. නැත්නම් right-click → Start
> - Port 5432 correct ද check
> - Password correct ද check
> - Firewall block කරනවද check

---

### 🐳 METHOD 2: Docker Use කරලා

> [!TIP]
> Docker use කළොත් PostgreSQL install කරන්න ඕන නෑ! Container එකක් run කරනවා විතරයි. Clean, fast, easy to remove.

#### 7.2a — Docker Install (if not installed)

1. [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/) → Download Docker Desktop for Windows
2. Install කරන්න → Restart computer
3. Docker Desktop open කරන්න → ✅ "Docker Desktop is running" confirm

#### 7.2b — Docker Compose File Create කරන්න

ඔයාගේ project folder එකේ `docker-compose.yml` file එකක් create කරන්න:

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
> `postgis/postgis:16-3.4` image එකේ PostgreSQL 16 + PostGIS 3.4 **දෙකම** include වෙලා තියෙනවා. වෙනම install කරන්න ඕන නෑ!

#### 7.2c — Docker Container Run කරන්න

PowerShell / Terminal open කරලා (project folder එකේ):

```powershell
docker-compose up -d
```

Output:
```
✔ Container sl_bia_postgis  Started
```

**Container run වෙනවද check:**
```powershell
docker ps
```
`sl_bia_postgis` container **Up** status එකේ display වෙන්න ඕන.

#### 7.2d — PostGIS Extension Enable (Docker)

Docker container එකේ PostGIS auto-enable වෙනවා `postgis/postgis` image එක use කරනකොට. But confirm කරන්න:

```powershell
docker exec -it sl_bia_postgis psql -U postgres -d SL_BIA_Aerial_Info -c "CREATE EXTENSION IF NOT EXISTS postgis;"
```

✅ Output: `CREATE EXTENSION`

#### 7.2e — QGIS Connect කරන්න (Docker)

1. QGIS → Browser Panel → `PostGIS` right-click → **`New Connection...`**
2. Fill:

| Field | Value |
|-------|-------|
| **Name** | `SL_BIA_Aerial_Info` |
| **Host** | `localhost` |
| **Port** | `5432` |
| **Database** | `SL_BIA_Aerial_Info` |
| **User name** | `postgres` |
| **Password** | `postgres123` |

3. `Test Connection` → ✅ Success!
4. `OK`

> [!TIP]
> **Docker stop/start:**
> - Stop: `docker-compose down` (data save වෙනවා volume එකේ)
> - Start: `docker-compose up -d`
> - Computer restart කරාට පස්සේ Docker Desktop open කරලා container start කරන්න

---

### ☁️ METHOD 3: Supabase (Cloud PostgreSQL)

> [!NOTE]
> Supabase free tier එකේ PostgreSQL database එකක් ලැබෙනවා PostGIS extension එක්ක. Install කරන්න ඕන නෑ — browser එකෙන් setup, QGIS එකෙන් connect.

#### 7.3a — Supabase Account Create කරන්න

1. [supabase.com](https://supabase.com/) → **Start your project** click
2. GitHub account එකෙන් sign in (හෝ email use)
3. ✅ Dashboard open වෙනවා

#### 7.3b — New Project Create කරන්න

1. **New Project** click
2. Fill:
   - **Organization**: ඔයාගේ default org select
   - **Name**: `SL_BIA_Aerial_Info`
   - **Database Password**: strong password එකක් set (Ex: `MyBIA_2024!secure`) — **මේක save කරන්න!**
   - **Region**: closest region select (Ex: `Southeast Asia (Singapore)`)
3. **Create new project** click
4. ⏳ 1-2 minutes wait — project setup වෙනවා

#### 7.3c — PostGIS Extension Enable කරන්න

1. Left menu → **SQL Editor** click
2. New Query:
```sql
CREATE EXTENSION IF NOT EXISTS postgis;
```
3. **Run** click
4. ✅ "Success. No rows returned" — PostGIS enabled!

#### 7.3d — Connection Details ගන්න

1. Left menu → **Project Settings** (gear icon) click
2. **Database** section click
3. **Connection string** section එකේ `URI` tab click
4. මේ details note කරන්න:

| Detail | Where to find | Example |
|--------|--------------|---------|
| **Host** | Connection string එකේ | `db.xxxxxxxxxxxx.supabase.co` |
| **Port** | Default | `5432` |
| **Database** | Default | `postgres` |
| **User** | Default | `postgres` |
| **Password** | ඔයා set කරපු password | `MyBIA_2024!secure` |

> [!WARNING]
> **Direct Connection use කරන්න** (Pooler connection **එපා**). 
> - ✅ Use: `Host: db.xxxxxxxxxxxx.supabase.co` Port: `5432`
> - ❌ Don't use: Pooler connection (port 6543)

#### 7.3e — QGIS Connect කරන්න (Supabase)

1. QGIS → Browser Panel → `PostGIS` right-click → **`New Connection...`**
2. Fill:

| Field | Value |
|-------|-------|
| **Name** | `SL_BIA_Aerial_Info` |
| **Host** | `db.xxxxxxxxxxxx.supabase.co` (ඔයාගේ project host) |
| **Port** | `5432` |
| **Database** | `postgres` |
| **SSL mode** | **require** (important!) |
| **User name** | `postgres` |
| **Password** | ඔයා set කරපු password |

3. `Test Connection` → ✅ Success!
4. `OK`

> [!CAUTION]
> **Supabase limitations:**
> - Free tier: **500MB** database storage (Task C වලට ප්‍රමාණවත්)
> - Internet connection ඕන (offline work බෑ)
> - Data upload **slow** විය හැක (cloud connection)
> - 7 days inactive → project pause වෙනවා (dashboard එකෙන් resume කරන්න)

> [!TIP]
> **Assessment submission වලට:** Supabase use කළොත් screenshots වල Supabase SQL Editor/Dashboard show වෙනවා — ඒක fine. But report එකේ mention කරන්න "PostgreSQL hosted on Supabase cloud platform with PostGIS extension" කියලා.

---

### 7.4 — Tables Create කරන්න (ඔක්කොම methods වලටම common)

> [!NOTE]
> ඔයා ඉහත methods 3න් ඕනම එකක් use කළාම, මෙතනින් ඉදිරියට ඔක්කොමටම **same steps**.

**pgAdmin / Supabase SQL Editor / Docker exec** use කරලා:

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

### 7.5 — QGIS Layers PostgreSQL වලට Import කරන්න

**Method A: QGIS DB Manager (Recommended):**

1. QGIS: `Database` → `DB Manager...`
2. PostGIS → ඔයාගේ connection select (`SL_BIA_Aerial_Info`)
3. Connect click
4. **`Import Layer/File`** button click (top toolbar)
5. Settings:
   - Input: ඔයාගේ shapefile layer select (dropdown එකෙන්)
   - Table: table name (Ex: `buildings`)
   - ✅ **Primary key**: `id`
   - ✅ **Geometry column**: `geom`
   - **Source SRID**: `5234`
   - **Target SRID**: `5234`
6. `OK` → Import!
7. ✅ ඔයාගේ shapefile layers one-by-one import කරන්න

**Method B: QGIS Processing Toolbox:**

1. `Processing` → `Toolbox` → search "Export to PostgreSQL"
2. Input: ඔයාගේ layer
3. Database, schema settings fill
4. `Run`

### 7.6 — Database එකේ Spatial Queries Run කරන්න

pgAdmin / Supabase SQL Editor එකේ:

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
> **Screenshot ගන්න!** — Database creation, PostGIS extension, table creation, data import, query results — ඔක්කොම appendix එකට ඕන.

---

## STEP 8: Verify PostGIS Layers in QGIS

### 8.1 — PostGIS Layers Add කරන්න

1. `Layer` → `Add Layer` → `Add PostGIS Layers...`
2. Connection: `SL_BIA_Aerial_Info` select → `Connect`
3. Tables display වෙනවා → select all (හෝ ඕන tables select)
4. `Add` click
5. ✅ Database layers QGIS map එකේ display වෙනවා

### 8.2 — Verify Data

1. Added PostGIS layer right-click → `Open Attribute Table`
2. Data correctly import වෙලා තියෙනවද check
3. Map එකේ geometries correct locations වල display වෙනවද check

---

## STEP 9: Final Map Design — Print Layout

### 9.1 — Map Styling

1. Each layer right-click → `Properties` → `Symbology`
2. Suitable colors/styles assign කරන්න:

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

### 9.2 — Print Layout Create කරන්න

1. `Project` → `New Print Layout...`
2. Layout name: "BIA Radar Deployment Map"
3. `OK`

### 9.3 — Map Elements Add කරන්න (MANDATORY for marks)

> [!CAUTION]
> Marking criteria එකේ clearly mention කරනවා: **North Arrow, Map Scale-Graphic, Map Scale-Numeric, Map Title, Map Legends** — මේවා ඔක්කොම ඕනෑම map එකක තියෙන්නම ඕන!

1. **Map Add කරන්න**: `Add Item` → `Add Map` → canvas එකේ draw
2. **Title**: `Add Item` → `Add Label` → text: "Geo Spatial Analysis for PSR, SSR & SMR Radar Deployment at BIA, Katunayake"
3. **Legend**: `Add Item` → `Add Legend` → map element select
4. **Scale Bar (Graphic)**: `Add Item` → `Add Scale Bar`
5. **Scale Bar (Numeric)**: `Add Item` → `Add Label` → scale text add (Ex: "1:25000")
6. **North Arrow**: `Add Item` → `Add North Arrow`
7. **Caption**: Map caption add (ඔයාගේ name, date, CRS info)

### 9.4 — Map Export

1. `Layout` → `Export as PDF...` (report එකට embed කරන්න)
2. `Layout` → `Export as Image...` (PNG — appendix එකට)
3. ✅ High resolution select (300 DPI)

> [!TIP]
> **Screenshot ගන්න!** — Final map, print layout process, ඔක්කොම.

---

## STEP 10: Base Map Add කරන්න (Extra Marks)

Marking criteria "Excellent" band එකේ "A suitable base map has been included" කියලා mention කරනවා.

### QuickMapServices Plugin:

1. `Plugins` → `Manage and Install Plugins...`
2. Search "QuickMapServices" → Install
3. `Web` → `QuickMapServices` → `OSM` → `OSM Standard`
4. ✅ OpenStreetMap base map add වෙනවා
5. Layers panel එකේ base map layer drag කරලා bottom එකට දාන්න

---

## STEP 11: Report Writing — Critical Discussion

Report එකේ මේ points cover කරන්න:

### Discussion Structure:

1. **Introduction to Radar Systems**
   - PSR (Primary Surveillance Radar) — what it does, why important
   - SSR (Secondary Surveillance Radar) — transponder-based, aircraft identification
   - SMR (Surface Movement Radar) — ground traffic monitoring

2. **Importance for BIA**
   - Increasing air traffic demands
   - Safety requirements (ICAO standards)
   - Modernization under Millennium Renovation Project

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

## 📋 FINAL CHECKLIST — Submit කරන්න කලින්

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

## ⚠️ Common Errors සහ Solutions

| Error | Cause | Solution |
|-------|-------|----------|
| Layer doesn't display correctly | Wrong CRS | Re-project to EPSG:5234 |
| Georeferencer high RMS error | Poor GCP placement | Re-do GCPs, use clear identifiable points |
| Buffer tool doesn't work | CRS in degrees not meters | Convert to EPSG:5234 (meters) first |
| PostGIS extension error | PostGIS not installed | Stack Builder වලින් install කරන්න |
| "No geometry column" in PostGIS | Import didn't include geometry | DB Manager use කරලා re-import with geometry |
| Attribute table empty | Forgot to enter attributes during digitizing | Edit mode, click feature, enter values |
| Area calculation shows 0 | CRS issue | EPSG:5234 (projected, meters) use කරන්න |
| Map elements missing in PDF | Print Layout එකේ add කරලා නෑ | Print Layout → Add Item → add all elements |

---

> [!TIP]
> **Excellent grade (70-100) ගන්න** marking criteria අනුව ඔයාට ඕන:
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
