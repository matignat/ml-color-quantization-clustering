# Color Palette Reduction via Clustering

---

## Project Overview

This project solves the problem of **lossy image compression via color-palette reduction**.
The core idea is to represent every pixel in an image not by its exact RGB triplet
but by one of *k* cluster centroids — effectively reducing the palette from up to ~10 000 unique
colors to exactly *k* colors.

We work with a dataset of **132 PNG images** (55 cats, 77 flowers), each 100 × 100 pixels.

| Task | Description |
|------|-------------|
| 1 | Build `df_pixels` and `color_cats` DataFrames |
| 2 | Exploratory Data Analysis |
| 3 | KMeans vs KMedoids clustering, choose best k |
| 4 | Save compressed images, measure gain, regression |
| 5 | kNN classification — original vs compressed |

---

## Project Structure & Data

### 1. `df_pixels`
Contains one row per pixel. Stores image identifier, pixel position, and the full color description in both RGB and HSL space. Each image is 100 × 100 px, resulting in 1,320,000 rows across 132 images.

### 2. `color_stats`
Contains one row for each unique RGB color observed in the dataset. Stores occurrences in cat/flower images and binary indicators derived from RGB/HSL definitions. It has 848,248 rows.

---

## Clustering Analysis

The project compares **KMeans** and **KMedoids** algorithms for clustering image pixels to reduce the color palette. 

*   Algorithms were tested for `k` values in `[5, 10, 15]`.
*   Evaluation metrics used: **Silhouette Score** and **Calinski-Harabasz Index (CHI)**.
*   **Result:** `k=5` maximizes the Silhouette score for both algorithms. **KMeans** was chosen as the final algorithm because it is significantly faster than KMedoids while maintaining comparable clustering quality.
