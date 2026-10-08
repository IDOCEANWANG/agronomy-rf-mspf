# Mapping Surface-Cover Components in Desert Steppe from UAV RGB Imagery Using Interpretable Features and Multiscale Superpixel Probability Fusion

This repository browser copy accompanies the unpublished Agronomy submission manuscript by Haiyang Wang, Yuge Bi, Sen Wang, Wenye Xie, Yingshuo Du, and Zhanzhao Liu. Prepared and checked on 8 October 2026. Correspondence: biyuge163@imau.edu.cn.

## Download the complete dataset and runnable code

Download **Agronomy_RF_MSPF_Data_Code_Results_20261007_v2.zip** from this repository's **Releases** page. The fixed release is **[v1.0.0](https://github.com/IDOCEANWANG/agronomy-rf-mspf/releases/tag/v1.0.0)**. The complete ZIP contains source JPEGs, analysis patches, annotations, numeric labels, models, predictions, publication figures, full-precision tables and verification scripts. The main branch currently contains documentation and summaries; the complete research code and data are in the release attachment; cloning it alone is insufficient to reproduce the study. GitHub's automatically generated source-code ZIP also omits the complete dataset payload.

The full ZIP was audited on 8 October 2026. Its historical filename is preserved to match the companion manuscript; use the SHA-256 in the same release to identify the exact archive. Do not mix it with the earlier 7 October preparation copy.

## Reproduction

Extract the full ZIP, install research/requirements.txt with Python 3.9, and run `python -B verify_release.py --model-inference` from its root. See research/README.md for complete retraining in a working copy. Existing archived outputs are overwritten by full reproduction; preserve the release snapshot separately. See RESULTS_SUMMARY.md and MANUSCRIPT_ALIGNMENT.json for numerical evidence and correspondence.

## Data and evaluation scope

There are 12 original JPEGs, nine analyzed source groups, 19 patches of 512 × 512 pixels and 335,675 sparse valid reference labels. The fixed 15/4 development split shares three source groups. Grouped five-fold evaluation holds out source photographs within the same site and acquisition period; it is not external-site validation.

Fixed-split OA is 0.841168 for RF and 0.880634 for RF-MSPF. Grouped mean OA is 0.801988 for RF, 0.869145 for RF-MSPF and 0.870373 for equal multiscale fusion. The evidence supports regional aggregation, without a consistent gain from consistency weighting. Reference labels exclude Ignore (-1). The retained LT code denotes visible dead plant material including standing dead herbs.

## Licenses and citation

Original data, numerical results and original publication figures use **CC BY 4.0** (LICENSE_DATA.md); original Python code and software documentation use **MIT** (LICENSE_CODE.txt). Third-party material retains its existing terms. See LICENSE_STATUS.md for scope and CITATION.cff for author/title metadata. The journal template is outside this grant. No journal publication or DOI is claimed. Repository: https://github.com/IDOCEANWANG/agronomy-rf-mspf.
