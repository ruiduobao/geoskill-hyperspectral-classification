---
name: geoskill-hyperspectral-classification
description: 'PCA降维+RF/SVM逐像元高光谱监督分类'
---

# 高光谱分类 | Hyperspectral Classification

Performs per-pixel supervised classification on hyperspectral image cubes (bands × H × W, typically 30+ bands). PCA first projects the high-dimensional spectra into principal-component space to reduce noise and redundancy; a classifier is then trained with random forest (RF) or support vector machine (SVM) to predict the land-cover class of each pixel.

Synthetic mode automatically generates N land-cover classes with characteristic spectral signatures (e.g., minerals/vegetation/soil/water), distributed as spatial patches with added noise; training samples are produced by stratified sampling from the ground-truth labels (70% training / 30% validation by default). The outputs include a classification map, accuracy assessment (overall accuracy, Kappa), and a confusion matrix. Suitable for hyperspectral mapping, mineral/vegetation mapping, and method-comparison teaching.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy scikit-learn
```

## Usage / 使用方法

### Basic Usage (Synthetic Data, Offline)

```bash
python geoskill-hyperspectral-classification.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 1: Random Forest, 4-Class Classification (30 Bands)

```bash
python geoskill-hyperspectral-classification.py \
    --bbox 116.0 39.0 117.0 40.0 \
    --synthetic --n-bands 30 --n-classes 4 --method rf \
    --output-dir ./rf_4class
```

### Example 2: SVM Method Comparison

```bash
python geoskill-hyperspectral-classification.py \
    --bbox 121.0 31.0 122.0 32.0 \
    --synthetic --n-bands 30 --n-classes 4 --method svm \
    --output-dir ./svm_4class
```

### Example 3: More Classes and Bands

```bash
python geoskill-hyperspectral-classification.py \
    --bbox 116.0 39.0 117.0 40.0 \
    --synthetic --n-bands 60 --n-classes 6 --method rf \
    --output-dir ./rf_6class
```

### Example 4: Real Hyperspectral GeoTIFF Input

```bash
python geoskill-hyperspectral-classification.py \
    --input cuprite_subset.tif --method rf \
    --output-dir ./real_rf
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `classification.tif` | GeoTIFF (int class ID) | Per-pixel classification result, EPSG:4326 |
| `accuracy.json` | JSON | Overall accuracy, Kappa, confusion matrix, per-class accuracy |
| `output-manifest.json` | JSON | Run manifest (input/output/QA/software versions) |

## Data Source / 数据源 / Source

- **Real mode**: local hyperspectral GeoTIFF (multi-band rasters exported from ENVI/PRISMA/AVIRIS, etc.)
- **Synthetic mode**: locally generates characteristic spectral curves + spatial patches, with no external data source

## Privacy / 隐私声明 / Privacy

- Runs fully offline by default and makes no network requests
- `--synthetic` mode reads no external data
- All computation is done locally; user data is never uploaded

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
