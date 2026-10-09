# RF-MSPF data code and results 数据代码与结果

Mapping Surface-Cover Components in Desert Steppe from UAV RGB Imagery Using Interpretable Features and Multiscale Superpixel Probability Fusion

Haiyang Wang, Yuge Bi, Sen Wang, Wenye Xie, Yingshuo Du, and Zhanzhao Liu  
College of Mechanical and Electrical Engineering, Inner Mongolia Agricultural University  
Correspondence 联系邮箱: biyuge163@imau.edu.cn

## Download 下载

We provide the complete research package as **Agronomy_RF_MSPF_Data_Code_Results.zip** in [GitHub Releases](https://github.com/IDOCEANWANG/agronomy-rf-mspf/releases). This README is the shared entry point for the data, code, supplementary materials, and results.

我们通过 GitHub Releases 提供完整研究资料包 **Agronomy_RF_MSPF_Data_Code_Results.zip**。本说明统一介绍数据、代码、补充材料与结果。

## Contents 文件内容

- `dataset/`: 12 original JPEGs, 19 RGB patches, sparse annotation overlays, signed numeric labels, source and crop metadata. 12张原始JPEG影像、19个RGB切片、稀疏标注、数值标签及来源和裁剪元数据。
- `research/`: analysis code, pinned dependencies, trained RF/scaler model, full-precision results, 155 prediction archives. 分析代码、依赖配置、RF与标准化模型、全精度结果及155份预测档案。
- `supplementary/`: bilingual supplementary documents and CSV tables for manuscript Tables 3–5 and supplementary Tables S1–S4. 中英文补充材料及正文表3—5、补充表S1—S4对应的CSV。
- `publication_figures/`: manuscript Figures 1–4 and captions. 正文图1—4及图注。
- `verify_release.py`, `MANIFEST.sha256`: reproducibility checks and file integrity records. 复核程序与文件完整性记录。
- `CITATION.cff`, `LICENSE_DATA.md`, `LICENSE_CODE.txt`: citation metadata and licenses. 引用信息与许可文本。

## Data and evaluation 数据与评估

We analyzed 19 patches of 512 × 512 pixels from nine source images acquired on 4–5 July 2025. The 335,675 valid reference pixels comprise HV 113,855; WV 138,365; LT 29,023; and BS 54,432. We use HV for living herbaceous vegetation, WV for woody or semi-woody canopies, LT for visible dead plant material including identifiable standing dead herbs, and BS for bare substrate. We exclude Ignore (−1) from training and scoring.

我们分析了2025年7月4—5日采集的9张源影像所形成的19个512 × 512像素切片。有效参考像素共335,675个：HV 113,855，WV 138,365，LT 29,023，BS 54,432。HV表示活体草本植被，WV表示木本或半木本冠层，LT表示可见枯死植物材料（包括可辨识的站立枯死草本），BS表示裸露基质。我们在训练和评分中排除Ignore（−1）。

We use a fixed development split of 15 training and four validation patches, containing 247,903 and 87,772 valid pixels. Four geometric variants yield 991,612 training samples. Three source-image groups contribute patches to both subsets. We also evaluate source-image-grouped five-fold validation, keeping each source image's patches together. The evaluation concerns source-image groups within the study site and acquisition period. Fold summaries are arithmetic means and sample SD (ddof = 1). The valid pixels are spatially dependent.

我们使用15个训练切片与4个验证切片进行固定开发比较，两部分分别含247,903和87,772个有效像素。四种几何变换形成991,612个训练样本。三个源影像组同时向训练和验证子集提供切片。我们同时开展源影像分组五折验证，将同一源影像的切片归入同一折；评估范围为研究地点与采集时段内的源影像组。各折汇总采用算术均值与样本标准差（ddof = 1）。有效像素之间存在空间依赖性。

## Fixed classifier comparison 固定划分分类器比较

| Method 方法 | OA | AA | Kappa | Macro-F1 | mIoU |
| --- | --- | --- | --- | --- | --- |
| RF | 0.8411680262498291 | 0.815923011300132 | 0.7487802756776523 | 0.8044924780124953 | 0.6878749897400579 |
| KNN | 0.8306977168117395 | 0.781707098258346 | 0.7287035858693287 | 0.7881385107583367 | 0.668919168410687 |
| XGBoost | 0.7884405049446293 | 0.7550166344427385 | 0.6649888404848984 | 0.747530470036151 | 0.6072000182810126 |
| RF-MSPF | 0.8806339151437816 | 0.8778517201189293 | 0.810314304263112 | 0.8742043289304265 | 0.7839715832232097 |

We report the specified classifiers under common input features, augmented training data, and training-fitted scaling. RF-MSPF adds spatial processing to RF probabilities. We interpret these values as performance of the evaluated configurations.

我们在共同的输入特征、增强训练数据和训练集拟合的标准化条件下报告各分类器结果。RF-MSPF对RF概率进一步进行空间处理。我们据此比较所评估配置的表现。

## Fixed spatial ablation 固定划分空间消融

| Method 方法 | OA | AA | Kappa | Macro-F1 | mIoU |
| --- | --- | --- | --- | --- | --- |
| RF | 0.8411680262498291 | 0.815923011300132 | 0.7487802756776523 | 0.8044924780124953 | 0.6878749897400579 |
| S150 | 0.8743676798979173 | 0.8784525211747611 | 0.8015429190305373 | 0.8629901570927192 | 0.7639025523829414 |
| S300 | 0.8523105318324751 | 0.8246037448620652 | 0.7662945251957263 | 0.8141001908619363 | 0.7009784386245309 |
| S500 | 0.8589413480380987 | 0.8279611859478949 | 0.7762593013934642 | 0.8222771695567686 | 0.7130135326776962 |
| MS_equal | 0.8803946588889395 | 0.8777504505727081 | 0.8100416597567327 | 0.8732176613746324 | 0.7827003836979196 |
| RF-MSPF | 0.8806339151437816 | 0.8778517201189293 | 0.810314304263112 | 0.8742043289304265 | 0.7839715832232097 |

We observed an OA gain of 3.32 percentage points from S150 regional aggregation over RF, a further 0.60 percentage points from equal multiscale fusion, and 0.024 percentage points from consistency weighting on the fixed split. Differences use unrounded values.

我们观察到，在固定划分上，S150区域聚合相较RF提高OA 3.32个百分点，等权多尺度融合进一步提高0.60个百分点，一致性加权再提高0.024个百分点。差值由未舍入结果计算。

## Grouped validation 分组验证

| Method 方法 | OA mean 均值 | OA sample SD 样本标准差 | Macro-F1 mean 均值 | Macro-F1 sample SD 样本标准差 |
| --- | --- | --- | --- | --- |
| RF | 0.8019884316047936 | 0.057274376457083984 | 0.7670676359002212 | 0.05350215407323871 |
| S150 | 0.8686245933742264 | 0.027846482559643827 | 0.8164675866067658 | 0.052214145815467905 |
| S300 | 0.8495100184276756 | 0.0443328150418657 | 0.8046510666260371 | 0.040576171862002096 |
| S500 | 0.8480444267883689 | 0.0467317936036849 | 0.8078664213251356 | 0.036426268844802934 |
| MS_equal | 0.8703726415374232 | 0.03669599384119489 | 0.8306999500694342 | 0.03702485631989057 |
| RF-MSPF | 0.8691448963442101 | 0.036725753002620515 | 0.8301776079334143 | 0.03660983261979043 |

We observed higher RF-MSPF OA than RF in all five folds, with a mean paired gain of 6.72 percentage points. Equal fusion has mean OA 0.870373, compared with 0.869145 for RF-MSPF. Consistency weighting lowers OA in three folds and increases it in two; its mean paired difference is −0.122775 percentage points. We identify regional aggregation as the principal supported gain. Table S4 supplies all six spatial methods, five metrics, and paired differences.

我们观察到RF-MSPF在五折中均取得高于RF的OA，平均配对增益为6.72个百分点。等权融合的OA均值为0.870373，RF-MSPF为0.869145。一致性加权在三折降低OA、两折提高OA，平均配对差值为−0.122775个百分点。因此，我们将区域聚合视为有结果支持的主要收益。表S4列出全部六种空间方法、五项指标与配对差值。

## Feature and class results 特征与类别结果

We evaluated all 31 nonempty feature combinations on the fixed development split. The full five-feature combination achieved OA 0.880634; H + SP300_Grad + Gabor ranked second at 0.861926. We interpret this ordering as an exploratory development comparison. RF-MSPF class F1 scores were HV 0.897368, WV 0.860173, LT 0.768247, and BS 0.971030.

我们在固定开发划分上评估全部31种非空特征组合。完整五特征组合的OA为0.880634；H + SP300_Grad + Gabor以0.861926位列第二。该排序属于探索性开发比较。RF-MSPF各类别F1分别为HV 0.897368、WV 0.860173、LT 0.768247及BS 0.971030。

## Acquisition and computation 采集与计算

We report local acquisition times in Beijing time (UTC+8). Original source images have 4000 × 3000 pixels, DJI camera model FC300S, and focal length 3.61 mm. Camera coordinates identify recorded camera positions. Device-relative altitude values span 6.7–7.2 m among analyzed images; we use them as device records. The archived Apple M4 benchmark with 16 GiB memory averaged 0.794583 ± 0.045674 s over 12 runs for a 512 × 512 patch, covering features, scaling, RF probabilities, three fresh SLIC segmentations, fusion, and argmax. The RF/scaler file occupies 27,157,561 bytes.

我们按北京时间（UTC+8）报告采集时间。原始影像为4000 × 3000像素，DJI相机型号FC300S，焦距3.61 mm。坐标表示相机记录位置。分析影像中的设备相对高度为6.7—7.2 m，我们将其作为设备记录。归档的Apple M4、16 GiB内存环境基准测试中，512 × 512切片在12次运行中的平均耗时为0.794583 ± 0.045674 s，包含特征计算、标准化、RF概率预测、三个重新计算的SLIC分割、融合与argmax。RF与标准化模型文件大小为27,157,561字节。

## Reproduction 复现

We provide the numerical environment in `research/requirements.txt` and the protocol in `research/config.json`. Use Python 3.9 and install the dependencies. From the package root, run:

我们在 `research/requirements.txt` 中提供依赖环境，在 `research/config.json` 中提供实验配置。使用Python 3.9安装依赖后，在资料包根目录运行：

```sh
python -m pip install -r research/requirements.txt
python -B verify_release.py --model-inference
```

For full retraining, work in a copy of the extracted package and run the following from `research/`:

完整重新训练会生成实验输出，请在解压资料包的工作副本中进入 `research/` 运行：

```sh
python -B reproduce_all.py
```

We supply separate fixed, grouped, feature-combination, figure, and benchmark commands in `research/run_experiments.py` and companion scripts. The feature order is NGRDI, H, SP300_Grad, GR-NLT, Gabor. The `Proposed` code identifies RF-MSPF. Signed reference arrays use −1 for Ignore. The fixed spatial archives cover six methods; grouped and feature-combination archives provide RF and RF-MSPF arrays, with additional spatial metrics recorded as confusion counts. KNN and XGBoost arrays cover evaluated labeled positions. We verify source crops, labels, saved predictions, confusion-derived metrics, table alignment, and file hashes.

我们通过 `research/run_experiments.py` 及配套脚本提供固定划分、分组验证、特征组合、绘图和计时命令。特征顺序为NGRDI、H、SP300_Grad、GR-NLT、Gabor。内部代码 `Proposed` 对应RF-MSPF。有符号参考数组用−1表示Ignore。固定空间档案覆盖六种方法；分组与特征组合档案提供RF、RF-MSPF数组，其他空间指标以混淆计数记录。KNN与XGBoost数组覆盖有效标注位置。我们核对源影像裁剪、标签、保存的预测、由混淆计数计算的指标、表格对应关系及文件哈希。

## License and citation 许可与引用

We license original data, numerical results, and original publication figures under **CC BY 4.0**, and original Python code and software documentation under **MIT**. Third-party components follow their applicable licenses. Use `CITATION.cff` for citation metadata.

我们将原创数据、数值结果及原创论文图件以 **CC BY 4.0** 许可发布，将原创Python代码与软件说明以 **MIT** 许可发布。第三方组件遵循各自适用许可。引用信息见 `CITATION.cff`。
