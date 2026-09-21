# 💻 GAEZ v5 Data Access Notebooks — User Guide

This directory contains **Jupyter Notebooks for access to and download of GAEZ v5 datasets through the API**.

The notebooks provide interactive workflows for querying the **GAEZ v5 data catalog**, filtering datasets according to user-defined parameters, and downloading the corresponding **GeoTIFF raster files** from the FAO public data repository for use in external analyses and workflows.

Both notebooks follow the same general workflow: run all cells, make your selections using the interactive panel displayed at the bottom of the notebook, compile the matching files, and download them.


|Notebook|Dataset|
|-|-|
|`gaez\_res02\_downloader\_selection\_notebook.ipynb`|RES02 — Agro-climatic Potential Yield|
|`gaez\_res05\_downloader\_selection\_notebook.ipynb`|RES05 — Suitability and attainable yield|

Each notebook reads the official FAO README catalog for its dataset, lets you filter and select what you need through dropdown menus, and downloads the matching files into organized local folders. The RES05 notebook is fully self-contained (no external `utilities.py` dependency).

## Requirements

* Python 3.9+ with Jupyter Notebook or JupyterLab
* Packages: `pandas`, `openpyxl`, `requests`, `ipywidgets`

Install them if needed:

```bash
pip install pandas openpyxl requests ipywidgets
```

(The RES05 notebook has a commented-out install line in its first cell you can uncomment instead.)

## How to run either notebook

1. Open the notebook you need in Jupyter.
2. Run **all cells** (Kernel → Restart \& Run All, or "Run All" in the toolbar).
3. Wait for the catalog to load — this pulls the latest README file from FAO, so it needs an internet connection. A preview/summary will print near the top before the notebook finishes.
4. Once the notebook finishes running, an interactive selector panel appears at the bottom. Use it to make your selections:

   * **Mode** — *Download selected combination(s)* (pick 1–3 specific crops) or *Download all datasets for one variable* (every crop for that variable).
   * **Variable**, **Period**, **Climate**, **SSP**, **Input** — dropdowns to narrow the dataset. Most default to "All" and can be left as-is.
   * **Crop(s)** — only shown in "selected combination" mode; select 1 to 3 crops.
5. Click **Compile selection**. A table of matching files appears, and a "Compiled files" list is populated below it.
6. Click **Download compiled files** to download everything compiled, or switch **Download** to "Download only selected rows from the file list" and pick specific files from the "Compiled files" list first.

## Where files go

* RES02 → `downloads/_res02/<VARIABLE>/<PERIOD>/_<CLIMATE>/_<SSP>/_<INPUT>/<file/_name>.tif`
* RES05 → `downloads/_res05/<VARIABLE>/<PERIOD>/_<CLIMATE>/_<SSP>/_<INPUT>/<file/_name>.tif`

Both are organized in the same way: by variable, period, climate source, SSP, and input level.

## Settings

* **Check cloud file existence during compile** — verifies each file actually exists before downloading (slower; automatically skipped for large selections, e.g. over 200 files).
* **Overwrite existing downloaded files** — re-downloads files that are already present locally.

## Troubleshooting

* A 404 error on download means the file is listed in the FAO README catalog but isn't currently available at the expected cloud location.
* If the notebook can't reach the README URL, check your internet connection — the catalog is fetched live from FAO's servers each time you run the notebook.
