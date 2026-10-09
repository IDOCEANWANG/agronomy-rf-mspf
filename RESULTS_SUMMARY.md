# Results summary for the Agronomy submission

Documentation checked 2026-10-09. Haiyang Wang, Yuge Bi, Sen Wang, Wenye Xie, Yingshuo Du, and Zhanzhao Liu; Inner Mongolia Agricultural University; correspondence: biyuge163@imau.edu.cn. Public deposit; repository https://github.com/IDOCEANWANG/agronomy-rf-mspf; complete archive at https://github.com/IDOCEANWANG/agronomy-rf-mspf/releases; no DOI assigned. Data and original results: CC BY 4.0; original code: MIT. Scientific scores are unchanged from the reconciled frozen experiments. “Proposed” in historical outputs means RF-MSPF, the consistency-weighted multiscale method.

## Dataset and validation

Nineteen 512 × 512 patches derive from nine source photographs, with 335,675 annotated pixels (HV 113,855; WV 138,365; LT 29,023; BS 54,432). Twelve original JPEGs are included, of which three do not contribute analysis patches. Annotations are sparse. The fixed development split contains 15 training patches and four validation patches: 247,903 and 87,772 valid pixels. Four geometric variants yield 991,612 training samples. Three source groups are shared across that fixed split. Patch_012 and patch_014 overlap by 27,642 source-image pixels; both are training patches and grouped fold 2.

Source-image grouped five-fold validation keeps all patches from a source photograph together. Its unit is the source-image group within the same site/acquisition period; it is not external-site validation. Pixel counts describe annotation volume, not independent experimental replication. No pixelwise significance claim is made. Tables S1 and S3 give acquisition and provenance evidence.

## Fixed development-validation classifier comparison

Values are fractions (OA × 100 gives percent); AA is mean class recall, Macro_F1 is unweighted class-mean F1, and mIoU is mean class IoU. All methods share the same features, augmented training pixels, training-only scaling and evaluation pixels.

| method | OA | AA | Kappa | Macro_F1 | mIoU |
| --- | --- | --- | --- | --- | --- |
| RF | 0.841168 | 0.815923 | 0.748780 | 0.804492 | 0.687875 |
| KNN | 0.830698 | 0.781707 | 0.728704 | 0.788139 | 0.668919 |
| XGBoost | 0.788441 | 0.755017 | 0.664989 | 0.747530 | 0.607200 |
| RF-MSPF | 0.880634 | 0.877852 | 0.810314 | 0.874204 | 0.783972 |

RF-MSPF improves OA over pixelwise RF by **3.9466 percentage points**. This is a comparison on a previously used development subset. SVM is excluded because the supplied capped fit was not converged and the later unlimited attempt did not yield a verified completed model.

## Fixed spatial ablation

| method | OA | AA | Kappa | Macro_F1 | mIoU |
| --- | --- | --- | --- | --- | --- |
| RF | 0.841168 | 0.815923 | 0.748780 | 0.804492 | 0.687875 |
| RF + SLIC-150 | 0.874368 | 0.878453 | 0.801543 | 0.862990 | 0.763903 |
| RF + SLIC-300 | 0.852311 | 0.824604 | 0.766295 | 0.814100 | 0.700978 |
| RF + SLIC-500 | 0.858941 | 0.827961 | 0.776259 | 0.822277 | 0.713014 |
| RF + equal multiscale fusion | 0.880395 | 0.877750 | 0.810042 | 0.873218 | 0.782700 |
| RF-MSPF | 0.880634 | 0.877852 | 0.810314 | 0.874204 | 0.783972 |

The fixed RF-MSPF versus equal-fusion OA difference is only **+0.0239 percentage points**. SLIC-150 has slightly higher fixed AA than RF-MSPF. These comparisons do not support describing the weighted model as uniformly superior on every metric.

## Source-grouped five-fold spatial results

The following statistics are arithmetic means and sample standard deviations across five folds (ddof=1); they are not pooled-pixel estimates or confidence intervals. All methods in a fold use the same fitted RF and the same held-out patches.

| method | OA_mean | OA_sample_sd | Macro_F1_mean | Macro_F1_sample_sd |
| --- | --- | --- | --- | --- |
| RF | 0.801988 | 0.057274 | 0.767068 | 0.053502 |
| RF + SLIC-150 | 0.868625 | 0.027846 | 0.816468 | 0.052214 |
| RF + SLIC-300 | 0.849510 | 0.044333 | 0.804651 | 0.040576 |
| RF + SLIC-500 | 0.848044 | 0.046732 | 0.807866 | 0.036426 |
| RF + equal multiscale fusion | 0.870373 | 0.036696 | 0.830700 | 0.037025 |
| RF-MSPF | 0.869145 | 0.036726 | 0.830178 | 0.036610 |

RF-MSPF mean OA is **86.9145 ± 3.6726%**, versus **80.1988 ± 5.7274%** for pixelwise RF; mean paired gain is **6.7156 ± 2.9754 percentage points**. Equal fusion reaches **87.0373 ± 3.6696%**, which is **0.1228 percentage points higher** than RF-MSPF. Equal fusion also has slightly higher grouped means for AA, kappa, Macro_F1 and mIoU. RF-MSPF OA exceeds equal fusion in two of five folds and is lower in three. Thus the frozen main model is retained, but a consistent benefit from consistency weights is **not established**. Table S4a provides each fold, S4b all five metrics and S4c paired method differences.

## Class-level results and feature analysis

Table 5 supplies precision, recall, F1 and IoU for all four classes with their validation supports. RF-MSPF F1 scores are HV **0.897368**, WV **0.860173**, LT **0.768247** and BS **0.971030**. LT is an RGB-visible dead-material class including standing dead herbaceous material; attachment, tissue vitality and decomposition stage were not independently field validated.

All 31 nonempty combinations of NGRDI, H, SP300_Grad, GR-NLT and Gabor appear in Table S2. The full five-feature model has the highest fixed development OA (0.880634). The next highest is H + SP300_Grad + Gabor (0.861926). Repeated comparison on the same development subset is exploratory; these ranks are not a separate held-out feature-selection test.

## Acquisition and computational evidence

Table S1 is extracted from all 12 original JPEGs. EXIF timestamps span 4–5 July 2025, without an explicit timezone. Camera GPS positions are not surveyed plot boundaries. For the nine analyzed source images, device XMP relative altitudes span 6.7–7.2 m (all 12 retained images: 6.7–8.7 m) and are not independently verified AGL; no 30 m AGL value is established by these files. Source images are not resampled.

The retained benchmark averages **0.794583 ± 0.045674 s** over 12 inferences (three repetitions on each of four patches) on Apple M4 with 16 GiB memory. It includes features, scaling, RF probabilities, fresh SLIC at three scales, fusion and argmax; it excludes image decoding and model loading. The supplied RF/scaler file is **27,157,561 bytes**. Benchmark timing was not remeasured during this document review and is hardware/load dependent.

## Verification status and publication metadata

The release supplies 155 prediction archives: 124 for 31 feature combinations × four fixed validation patches; 19 for grouped validation; four for fixed spatial evaluation; four each for KNN and XGBoost. All carry the original reference labels. Fixed spatial archives contain all six methods; CV and feature archives contain RF and RF-MSPF. Other CV/feature spatial scores are verified against retained confusion matrices, with no claim that their absent per-pixel arrays were independently checked.

KNN and XGBoost were refitted on 6 October 2026 using the unchanged protocol to complete their evaluation arrays, and exactly matched retained confusion counts. Baseline arrays use -1 outside evaluated annotation positions. Fixed RF inference and all six spatial variants match the retained results exactly. The release verification checks archive coverage, pixel arrays, confusion matrices, metric formulas, all 31 feature combinations, fold membership, original crops, duplicated data, signed labels and file hashes. Full CV/feature retraining and new timing were not performed during this document review. See VALIDATION_STATUS.json and research/outputs/prediction_archive_completion.json.

The author confirmed CC BY 4.0 for original data/results and MIT for original code on 7 October 2026. The complete archive is publicly available in [GitHub Releases](https://github.com/IDOCEANWANG/agronomy-rf-mspf/releases); no DOI has been assigned. The six authors confirmed their common affiliation as the College of Mechanical and Electrical Engineering, Inner Mongolia Agricultural University. Final journal submission remains subject to approval of the final manuscript. 


## Acquisition and annotation metadata metadata clarification

The author-reported approximate acquisition height is 10 m without a recoverable flight log or independent measurement; the reference is unknown. Original device values are retained separately and do not establish calibrated height above ground. Acquisition times are identified by the authors as Beijing time, while EXIF contains no time-zone field. Labels used self-developed software and auxiliary near-ground photographs, not hyperspectral data; neither the software nor auxiliary photographs is included. Independent annotation review was not performed. See dataset/AUTHOR_REPORTED_METADATA.json (or AUTHOR_REPORTED_METADATA.json from within dataset). All numerical classification results are unchanged.


## Archive identity and manuscript alignment

The complete release attachment is the complete research ZIP archive (249,752,786 bytes). Its SHA-256 is `fa63d5c11c9b1b5d0068c8b739b4648881a95020624819b1565d5309de5851d7`. The public GitHub asset digest matched the local archive on 8 October 2026. The repository root contains documentation; complete data and analysis code are in the release attachment.

The bilingual manuscript review retains the published numerical results. Table S1–S4 and figures are unchanged. This document review does not add training, fieldwork, independent annotation review, or new timing measurements. The archived benchmark, KNN/XGBoost archive-completion refits, and prior verification are historical procedures, not newly performed experiments in this document review.

On 9 October 2026, 155 saved prediction archives, 224 confusion-derived metric rows, 87 supplementary records, 827 layered manifest entries, and source-image crops were checked again and matched. This check did not retrain models, rerun model inference, or repeat timing.
