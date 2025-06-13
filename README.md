
AX08 Project – XBT Temperature Profile Cleaning

This repository contains robust quality control (QC), cleaning routines, and visualizations for Expendable Bathythermograph (XBT) data collected along the AX08 transect.

---

## 🧪 What This Project Does

- Cleans 500+ raw AX08 XBT profiles using custom filtering routines  
- Removes artifacts like bottom-strike, sensor noise, and surface inversions  
- Detects and excludes profiles with unrealistic gradients, spikes, or flat segments  
- Computes **thermocline depths** and **mixed layer depths (MLD)** per profile  
- Produces cleaned outputs and plots saved to local directories

---

## 📂 Project Structure 


AX08_Project/
├── cleaned_profiles/         # CSVs of cleaned XBT profiles & metadata
├── figures/                  # Saved PNG plots (MLD, gradients, etc.)
├── AX08_profiles.ipynb       # Main analysis and cleaning notebook
├── Logs, summary and report/ # Supporting materials
├── EP2022-1825.pdf           # Expedition documentation
├── README.md
└── .gitignore

---

## 🔧 Cleaning & QC Methods

Cleaning logic aligns with accepted oceanographic QC practices and includes:

- ✅ **Monotonicity check** – profiles with non-increasing depth removed  
- ✅ **Valid range filtering** – temperature and depth constrained to realistic bounds  
- ✅ **Missing data & low-resolution check** – removes sparse or NaN-heavy profiles  
- ✅ **Spike removal** – local & zonal spikes removed using a rolling median and deviation threshold  
- ✅ **Surface inversion filter** – filters profiles where near-surface water is warmer than subsurface (>0.5°C)  
- ✅ **Flat segment removal** – segments with <0.05°C variation flagged and dropped  
- ✅ **Excessive gradient removal** – filters steep unrealistic gradients (>1.2°C per meter), relaxed below 800 m  
- ✅ **Median filtering** – 7-point kernel median filter applied to smoothed noise  
- ✅ **Bottom-strike clipping** – temps below 800 m clipped at 20°C, profiles >22°C below that are dropped  
- ✅ **Minimum valid depth check** – profiles must extend below 200 m

All filters are implemented in the `clean_profile()` function in the notebook.

---

## 🔍 Data Source

Raw profiles were obtained from NOAA's publicly available XBT archives:  
🌐 https://www.aoml.noaa.gov/phod/xbt.html

---

## 🧼 Cleaned Profiles

Only profiles that pass all QC criteria are retained. This includes:

- Monotonic increasing depth  
- Realistic temperature structure (no inversions or noise)  
- Valid vertical resolution and depth coverage  
- Removal of sensor artifacts (e.g., below 800 m)

📁 Output files are saved to [`cleaned_profiles/`](cleaned_profiles/).  
🖼️ PNG plots of MLD, thermoclines, and gradients are saved to [`figures/`](figures/).

---

## 📊 Example Plots

- **Mixed Layer Depth vs Latitude**  
- **Thermocline Depth vs Latitude**  
- **Temperature Gradient Profiles by Depth**  
- **Temperature-Depth Profiles Colored by Latitude**

These are saved automatically during the notebook run.

---

## 🚧 Known Limitations

Some edge cases — like extreme coastal gradients, partial drops, or unusual thermal structures — may be excluded. Profiles deeper than 800 m are handled more leniently due to common noise at depth.

---

## 🚀 Getting Started

To run the full pipeline:

```bash
cd ~/AX08_Project
jupyter lab AX08_profiles.ipynb

👤 Author

Alistair Blair
🌍 github.com/oceandata4fun
💬 Feedback and contributions are welcome!

