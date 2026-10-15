# Deep Learning-Based Skin Lesion Classification on HAM10000

A comparison of a custom Convolutional Neural Network (CNN) and an ImageNet-pretrained EfficientNetB0 for **seven-class classification of dermoscopic skin-lesion images**.

The project focuses on lesion-level data splitting, class imbalance handling, quantitative model evaluation, and visual interpretation using Grad-CAM.

**Research and educational demonstration only. Not intended for clinical diagnosis or use as a medical device.**

## 1. Dataset and Splitting

The [HAM10000 dataset](https://doi.org/10.1038/sdata.2018.161) contains **10,015 dermoscopic images** representing seven skin lesion categories: `akiec`, `bcc`, `bkl`, `df`, `mel`, `nv`, and `vasc`.

Since multiple images can correspond to the same lesion, the dataset was divided using `StratifiedGroupKFold`, with `lesion_id` as the grouping variable. This prevents images of the same lesion from appearing in different subsets and reduces the risk of data leakage.

| Split | Images | Unique Lesions |
|---|---:|---:|
| Training | 6,981 | 5,229 |
| Validation | 1,020 | 746 |
| Test | 2,014 | 1,495 |

The splitting strategy is lesion-level rather than patient-level because patient identifiers are unavailable.

## 2. Methodology

**CNN Baseline:** A custom convolutional neural network incorporating convolutional blocks, batch normalization, ReLU activations, global average pooling, and dense classification layers.

**EfficientNetB0:** An ImageNet-pretrained model adapted for skin lesion classification through transfer learning and partial fine-tuning.

**Image Preprocessing:** Images were resized to 224 × 224 pixels, with flipping, rotation, and zoom augmentation applied during training.

**Class Imbalance Handling:** Balanced class weights were calculated exclusively from the training data.

**Model Evaluation:** Performance was assessed using accuracy, macro-F1, balanced accuracy, ROC-AUC, confusion matrices, and per-class precision, recall, and F1-score.

**Statistical Analysis:** Lesion-level bootstrap resampling was used to estimate 95% confidence intervals.

**Model Interpretation:** Grad-CAM was applied to visualize image regions contributing to model predictions and explore selected classification errors.

## 3. Experimental Results

The models were evaluated on a test set containing **2,014 dermoscopic images**.

| Metric | CNN Baseline | EfficientNetB0 |
|---|---:|---:|
| Accuracy | 0.607 | **0.664** |
| Macro-F1 | 0.422 | **0.480** |
| Balanced Accuracy | 0.526 | **0.540** |
| Melanoma Recall | 0.613 | 0.613 |
| Macro ROC-AUC | 0.879 | **0.902** |

EfficientNetB0 achieved higher accuracy, macro-F1, balanced accuracy, and macro ROC-AUC than the CNN baseline in this experiment.

Both models achieved the same melanoma recall of 0.613, emphasizing the importance of evaluating individual lesion categories alongside overall performance.

### EfficientNetB0: Per-Class Performance

| Class | Samples | Precision | Recall | F1 |
|---|---:|---:|---:|---:|
| akiec | 68 | 0.526 | 0.441 | 0.480 |
| bcc | 100 | 0.523 | 0.450 | 0.484 |
| bkl | 205 | 0.395 | 0.580 | 0.470 |
| df | 22 | 0.133 | 0.182 | 0.154 |
| mel | 222 | 0.303 | 0.613 | 0.405 |
| nv | 1,363 | 0.951 | 0.717 | 0.818 |
| vasc | 34 | 0.422 | 0.794 | 0.551 |

### Statistical Confidence Intervals

The following 95% confidence intervals were estimated through 1,000 lesion-level bootstrap resamples.

| Metric | CNN (95% CI) | EfficientNetB0 (95% CI) |
|---|---|---|
| Macro-F1 | 0.385–0.458 | 0.438–0.515 |
| Balanced Accuracy | 0.484–0.574 | 0.494–0.586 |
| Melanoma Recall | 0.524–0.692 | 0.537–0.693 |

## 4. Grad-CAM Visualization

Grad-CAM was used to generate heatmaps highlighting image regions associated with model predictions.

Visualizations were generated for selected validation images across all seven classes, including misclassified melanoma examples.

These visualizations provide qualitative insight into model behavior rather than clinically validated lesion localization.

## 5. Repository Structure

```text
skin-lesion-classification-cnn/
│
├── Codes/
│   ├── 01_train_and_evaluate.ipynb
│   └── 02_figures_and_analysis.ipynb
│
├── Results/
│   └── figures/
│
└── README.md
```

**01_train_and_evaluate.ipynb**

Contains data preprocessing, lesion-level splitting, CNN and EfficientNetB0 training, model evaluation, confidence interval estimation, and Grad-CAM.

**02_figures_and_analysis.ipynb**

Contains exploratory data analysis, data distribution visualizations, training curves, model comparison plots, confusion matrices, and ROC/precision-recall analysis.

The `results/figures/` directory can be used to store generated plots and visualizations.




