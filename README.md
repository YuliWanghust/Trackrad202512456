# Trackrad202512456
# Editorial Report — Manuscript 048657

## 1. Overall Assessment

ScoliPFT-AI is a dual-view deep learning system predicting FEV1 and FVC ratios from AP and lateral whole-spine radiographs in AIS, validated across three Chinese centers (n=2,027). An AP-anchored fusion model (ConvNeXt-Tiny embeddings, single-view predictions, basic clinical variables) achieves external AUCs of 0.870, 0.853, 0.854 for impairment classification at the FEV1/FVC <0.8 threshold.

This is competent engineering on a clinically real problem, but not a substantial advance. Continuous prediction is mediocre externally (MAE 0.071–0.079; validation R² 0.5–0.6; Pearson r ~0.78–0.79), and the manuscript treats the AUC/MAE divergence as an explainable nuance rather than a limitation that undercuts the stated triage use case. Single-country external validation and the absence of any comparison against manually measured radiographic predictors are the two issues most affecting the decision.

## 2. Strengths

The cohort (2,027 patients, temporally separated internal test, fully independent external test, patient-level split) is large and well-structured for this niche. The AP-anchored gated-residual fusion design is a deliberate, validated choice (learned AP gate weight 0.748) rather than naive concatenation. Evaluation is comprehensive: regression and classification metrics, decision curve analysis, twelve-axis subgroup stratification, permutation importance, and Grad-CAM, with the radiograph-dominance finding (MAE increase 0.084 vs. 0.005 for clinical variables) being a genuine interpretability result.

## 3. Weaknesses

External validation spans only three tertiary Chinese hospitals, 85% female, with no reference-equation or equipment harmonization analysis despite the discussion flagging this as a likely calibration confound. Continuous prediction accuracy (R² 0.5–0.6, MAE up to 0.096 in low-function subgroups) is too weak to support individualized decisions near the 0.8 threshold — precisely where the claimed triage use case operates. No head-to-head comparison exists against Cobb angle/kyphosis/vertebral-rotation regression baselines, despite the manuscript explicitly claiming superiority over such "measurement-based" approaches. Backbone selection (four architectures, one validation split, no cross-validation) is thin for a tool with an active public deployment URL.

## 4. Editorial Decision

**Reject.** The calibration gap, missing baseline comparator, and single-country validation are addressable but collectively insufficient for this venue; resubmission should add the manually measured radiographic baseline and multi-country external data.

---

## 5. Suggested Reviewer Expertise

Reviewers should include expertise in multi-view convolutional fusion architectures and residual/gated fusion design for medical imaging; calibration and external validation methodology for clinical prediction models (TRIPOD-AI/PROBAST-AI familiarity); spirometry reference equation standardization and cross-population pulmonary function measurement; pediatric/adolescent spinal deformity radiographic measurement (Cobb angle, vertebral rotation, thoracic kyphosis quantification); and pediatric orthopedic or pulmonology clinical practice in scoliosis management, specifically perioperative respiratory risk stratification.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

Ueda et al. (Lancet Digital Health, 2024) developed the first deep learning model to estimate spirometric FEV1 and FVC directly from posterior-anterior chest radiographs, training on 134,307 image-spirometry pairs across multiple Japanese institutions and achieving correlation coefficients of 0.90–0.91 for FVC and FEV1 in external test sets — substantially higher than the 0.78–0.79 correlations reported here, though on a much larger adult cohort with chest (not whole-spine) radiographs and different disease pathophysiology (predominantly restrictive/obstructive lung disease versus thoracospinal deformity). A newer probabilistic deep learning framework (Killing et al., Communications Medicine) estimates FEV1 and FVC from chest X-rays combined with anthropometric-normalized peak expiratory flow rate, using anatomical normalization and uncertainty modeling specifically to improve reliability near diagnostic thresholds — directly addressing the calibration-near-threshold weakness this manuscript leaves unresolved, and a design choice the present authors should engage with rather than treat threshold-proximal miscalibration as a footnote. In the scoliosis-specific imaging space, a 2025 meta-analysis pooling fifteen studies found deep learning measurement of spinopelvic radiographic parameters achieves mean absolute errors of 4.3° for Cobb angle and 3.9° for thoracic kyphosis against human raters, confirming that automated parameter extraction is now mature and could have been deployed as a baseline comparator in this study rather than omitted. A 2024 systematic review of machine learning models for curve-progression prediction in AIS concluded that most models achieve only moderate accuracy with very low certainty of evidence and generally lack external validation, situating this manuscript's three-center external test favorably relative to the broader AIS-ML literature, but that comparison is a low bar set by a field still maturing, not parity with the chest-radiograph-to-PFT benchmark this paper should be measured against. The manuscript's framing as the first AP+lateral whole-spine system for opportunistic AIS pulmonary screening is plausible, but its quantitative performance trails the directly analogous chest-X-ray literature it does not cite or benchmark against, and that comparison — not just the AIS-specific niche literature — is the appropriate yardstick reviewers should apply.

---

## Suggested Reviewer Names

**Fusion architecture / model methodology:** Daiju Ueda (Osaka Metropolitan University); Po-Hsuan Cameron Chen (Verily/Google Health, multi-view medical imaging fusion); Pranav Rajpurkar (Harvard, CXR deep learning benchmarking).

**Calibration / external validation methodology:** Gary Collins (University of Oxford, TRIPOD-AI); Karel Ramspek (Leiden University Medical Center, external validation methodology); Ben Glocker (Imperial College London, distribution shift in medical imaging AI).

**Pediatric spinal deformity / radiographic measurement:** Stefan Parent (CHU Sainte-Justine, AIS radiographic and surgical outcomes); Suken Shah (Nemours Children's Health, AIS deformity correction and pulmonary outcomes).

**Pulmonology / scoliosis respiratory function:** Theodoros B. Grivas (University of Athens, pulmonary function in idiopathic scoliosis); Brian Snyder (Boston Children's Hospital, early-onset scoliosis respiratory mechanics).

---

## Further Literature

1. **Orbach MR, Cahill PJ, Larson AN, El-Hawary R, Mayer OH, Balasubramanian S.** Predicting pulmonary function using thoracic deformity parameters in early onset scoliosis patients. *PLoS One* 2025;20(7):e0329199. DOI: 10.1371/journal.pone.0329199. *Relevance:* The closest direct comparator in spirit — multiple linear regression on 19 literature-derived deformity parameters predicting %FVC in 47 early-onset scoliosis patients. This manuscript's deep learning approach should be benchmarked against exactly this kind of parameter-based regression baseline, which it currently omits; the small cohort (n=47) here also underscores how much larger and more externally valid the present submission's cohort is by comparison.

2. **Ueda D, Matsumoto T, Yamamoto A, et al.** A deep learning-based model to estimate pulmonary function from chest x-rays: multi-institutional model development and validation study in Japan. *Lancet Digit Health* 2024;6(8):e580–e588. DOI: 10.1016/S2589-7500(24)00113-4. *Relevance:* The field-defining benchmark for radiograph-to-spirometry deep learning, achieving r=0.90–0.91 across two external Japanese cohorts (n=7,427) versus this manuscript's r=0.78–0.79. Establishes the performance ceiling this submission should be measured against and is conspicuously absent from its introduction and discussion.

3. **Killing C, et al.** Deep learning approach for probabilistic pulmonary function estimation from chest X-ray and peak expiratory flow rate. *Commun Med* 2026;6:art. 1702. DOI: 10.1038/s43856-026-01702-7. *Relevance:* Directly tackles the calibration-near-threshold problem this manuscript's discussion flags but does not solve, using anatomical normalization and uncertainty quantification to improve reliability at diagnostic cutoffs — a methodological gap the present authors should address in revision.

4. **[Meta-analysis] Deep learning for automated spinopelvic parameter measurement from radiographs: a meta-analysis.** *Artif Intell Surg* 2025;5(1) (OAE Publishing). DOI: per oaepublish.com/articles/ais.2024.36. *Relevance:* Pools fifteen studies (>10,000 radiographs) showing automated Cobb angle and thoracic kyphosis measurement now achieves MAE of 4.3° and 3.9° respectively against human raters. Demonstrates that an automated-parameter-extraction-plus-regression pipeline is a feasible, low-complexity baseline this manuscript should have run head-to-head against its deep learning fusion model.

5. **[Systematic review] A Systematic Review of Machine Learning Models for Predicting Curve Progression in Teenagers With Idiopathic Scoliosis.** *JOSPT Open* 2024;2(3):202–224. DOI: 10.2519/josptopen.2024.0718. *Relevance:* Surveys the broader AIS-ML landscape and concludes most models lack external validation and show only moderate accuracy with very low certainty of evidence. Useful context confirming this manuscript's external test design is a genuine relative strength within the AIS-specific subfield, even though it trails the adjacent chest-radiograph-PFT literature.

6. **Zhang L, Pei B, Zhang S, Lu D, Xu Y, Huang X, Wu X.** A new method for scoliosis screening incorporating deep learning with back images. *Glob Spine J* 2025;15(1) (SAGE). DOI: 10.1177/21925682241282581. *Relevance:* Represents the parallel deep-learning-for-AIS-screening literature using surface/back imaging rather than radiographs for Cobb angle estimation. Relevant as a comparator on methodological maturity and external validation rigor, though it targets deformity quantification rather than pulmonary function and so does not directly compete on outcome.

7. **Orbach MR, et al. (companion correlation analysis)** — Wang Y, Yang F, Wang D, et al. Correlation analysis between the pulmonary function test and the radiological parameters of the main right thoracic curve in adolescent idiopathic scoliosis. *J Orthop Surg Res* 2019;14(1):443 (cited by manuscript as ref. 13, included here for currency check). *Relevance:* Already cited by the authors as their primary measurement-based comparator; flagged here because despite being the manuscript's own benchmark reference, its Cobb-angle/rib-hump/apical-vertebral-translation regression model is never run as a quantitative baseline against ScoliPFT-AI, which is the single most important missing analysis for substantiating the manuscript's central comparative claim.

