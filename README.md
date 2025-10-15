# 🍎 Open Food Facts Nutrition Extraction — EDA & Qwen2.5-VLM Finetuning

* This repository focuses on exploratory data analysis (EDA) and fine-tuning a Vision-Language Model (VLM) to extract structured nutrition facts from Open Food Facts product images.
* The goal is to automatically extract and normalize nutrient values (per 100g) in JSON format from front or nutrition-label images.

## Overview

This project explores document understanding for food packaging using Vision-Language Models (VLMs).
It builds an end-to-end workflow that includes:

1. Dataset curation and analysis from the Open Food Facts dataset
2. Model training — finetuning Qwen2.5-VL using unsloth
3. Quantitative evaluation — defining and computing KPIs that measure extraction accuracy
4. Exploratory Data Analysis (EDA)

### The EDA notebook provides:

* Insights into product coverage, languages, and label completeness
* Filtering of samples with available nutritional images
* Visualization of image distributions by category and nutrient presence
* Sampling strategy to create a representative dataset for OCR/VLM tasks

### Qwen2.5-VLM Finetuning

The finetuning notebook trains the model to answer questions like:

`“Extract Nutrition Facts data from the given image. Normalize the nutrient values to 100g. Return the extraction output in JSON.”`

* Training setup:

  * Frameworks: unsloth, transformers
  * Trainer: SFTTrainer with UnslothVisionDataCollator
* Input Format:
  Chat-style examples combining text instructions + product nutrition images
* Output:
  JSON-formatted nutrient dictionary per product

Example Training Sample

```json
{
"user": [
{"type": "text", "text": "Extract Nutrition Facts data from the image and normalize to 100g."},
{"type": "image", "image": "./products_images/0016000157651.png"}
],
"assistant": [
{"type": "text", "text": "{\"energy-kcal_100g\": 315.0, \"fat_100g\": 2.78, ... }"}
]
}
```

### KPI Definitions — Model Evaluation

The evaluation framework compares predicted JSON outputs vs ground truth nutrient values.


| KPI                                       | Description                                                  | Formula                    |
| ----------------------------------------- | ------------------------------------------------------------ | -------------------------- |
| **Key Precision / Recall / F1**           | Measures how well the model predicts correct nutrient fields | F1 Score (Matched Keys)    |
| **MAPE (Mean Absolute Percentage Error)** | Measures numerical accuracy for matched keys                 | MAE and MAPE              |
| **Composite Score**                       | Combined structural + value accuracy                         | Overall = F1 * (1 - MAE) |

## Future Work:

* Expand dataset with multilingual nutrition images.
* Train model for longer duration.
* Evaluate on noisy and low-resolution packaging images.
* Support Full Model Evaluation.

## 📚 References

* [Open Food Facts Dataset](https://world.openfoodfacts.org/)
* [Qwen2.5-VL Model Card](https://huggingface.co/Qwen/Qwen2.5-VL-72B-Instruct)
* [Unsloth Fine-Tuning Framework](https://github.com/unslothai/unsloth)

## Author

**Sagar Rathod**
Machine Learning & Computer Vision Researchers
Focus: Vision-Language Models, OCR, and Geospatial AI
