# Nighttimelights
GEE script to download night time ligths data
# Guyana Night‑Time Lights (2015 – 2025)

**Yearly VIIRS composites with cloud filtering, ready for PCNL harmonisation**

---

## What this script does

1. **Loads** monthly VIIRS‑DNB (VCMSLCFG) night‑time light images for 2015 – 2025.
2. **Masks** cloudy pixels using the `cf_cvg` QA band (`> 3` observations criterion).
3. **Builds** a **mean composite** for each calendar year.
4. **Clips** each composite to an ROI covering mainland Guyana.
5. **Displays** the layers in the Google Earth Engine (GEE) Code Editor with a perceptually uniform colour ramp.
6. **Exports** every yearly raster (GeoTIFF, 500 m) to a "Nightlights" folder in your Google Drive.

> **Why?**  Chapter 4 needs a clean, inter‑annual NTL signal to compare against Pixel‑Scale Corrected NTL (PCNL) and socio‑economic data, probing whether Guyana’s oil boom brightens some regions more than others.

---

## Folder structure

```
.
├── gee_script_viirs.js   # GEE code (this script)
├── data/                 # Empty; GeoTIFFs live in Google Drive to keep the repo slim
├── docs/
│   └── roi.kml           # (Optional) ROI polygon for quick GIS preview
└── LICENSE
```

---

## Prerequisites

* A **Google Earth Engine** account
  Apply at [https://earthengine.google.com/](https://earthengine.google.com/).
* **Google Drive** with \~3 GB free space for 11 GeoTIFFs.
* Browser: Chrome or Firefox recommended.

---

## Quick‑start

1. **Clone** the repo and open the script in the GEE Code Editor.

   ```bash
   git clone https://github.com/<your‑user>/guyana‑ntl.git
   cd guyana‑ntl
   ```
2. **Paste** `gee_script_viirs.js` into a new GEE script; save.
3. **Run** – execution time ≈ 4 min (cloud‑filtering is lightweight).
4. **Monitor exports** in the **Tasks** tab; once finished, files appear in `Drive/Nightlights/`.

---

## Workflow at a glance

| Step | Function(s)                   | Key inputs                           | Output                            |
| ---- | ----------------------------- | ------------------------------------ | --------------------------------- |
| 1    | Load VIIRS collection         | `NOAA/VIIRS/DNB/MONTHLY_V1/VCMSLCFG` | Monthly NTL images, 2012‑present  |
| 2    | `createYearlyComposite(year)` | `cf_cvg > 3` mask                    | Mean yearly composite (`avg_rad`) |
| 3    | Clip                          | ROI rectangle                        | Yearly image clipped to Guyana    |
| 4    | Visualise                     | `Map.addLayer`                       | Layer in Code Editor              |
| 5    | Export                        | `Export.image.toDrive`               | GeoTIFF, 500 m, EPSG:4326         |

---

## Customising the script

| Parameter              | Default                            | Why change it?                                                |
| ---------------------- | ---------------------------------- | ------------------------------------------------------------- |
| `roi`                  | Rectangle (‑61.5, 1.0, ‑56.0, 8.5) | Use a finer shapefile if you want coastal buffering.          |
| `startYear`, `endYear` | 2015, 2025                         | Extend backwards to 2012 or forward as new data drop.         |
| `cf_cvg` threshold     | > 3                                | Lower it (e.g., 2) for cloudier months, at the risk of noise. |
| `scale`                | 500 m                              | Down to 15 m for urban focus; heed `maxPixels`.               |

---

## Expected outputs

| File           | Example name                 | Size\*   | Description                                     |
| -------------- | ---------------------------- | -------- | ----------------------------------------------- |
| Yearly GeoTIFF | `VIIRS_Nightlights_2018.tif` | 25–30 MB | Cloud‑filtered mean radiance (nW · cm⁻² · sr⁻¹) |

\*Size varies by Drive compression.

---

## Next steps: PCNL harmonisation

1. **Download** yearly GeoTIFFs.
2. **Run** Use ArcGISPro to correct saturation and blooming.
---


## License

Apache License 2.0
using apache lic
