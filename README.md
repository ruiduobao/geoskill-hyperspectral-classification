# Hyperspectral Classification (geoskill-hyperspectral-classification)

> PCA dimensionality reduction + RF/SVM per-pixel hyperspectral supervised classification

---

## 1. Overview

Performs per-pixel supervised classification on hyperspectral image cubes (bands × H × W, typically 30+ bands). PCA first projects the high-dimensional spectra into principal component space to reduce noise and redundancy; a random forest (RF) or support vector machine (SVM) classifier is then trained to predict the land cover class of each pixel. Synthetic mode automatically generates N classes with characteristic spectral curves (e.g. minerals/vegetation/soil/water), distributed as spatial patches with added noise; training samples are drawn by stratified sampling from ground-truth labels (default 70% training / 30% validation). Outputs the classification map, accuracy assessment (overall accuracy, Kappa), and confusion matrix. Suitable for hyperspectral mapping, mineral/vegetation mapping, and method-comparison teaching scenarios.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-hyperspectral-classification.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `classification.tif` | GeoTIFF (int class IDs) | Per-pixel classification result, EPSG:4326 |
| `accuracy.json` | JSON | Overall accuracy, Kappa, confusion matrix, per-class accuracy |
| `output-manifest.json` | JSON | Run manifest (input/output/QA/software versions) |


## 6. Technical Principle

(see SKILL.md for details)

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
