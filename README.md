# Trackrad202512456
049658
Condensing sections 1–4 to 300 words, keeping 5–7 verbatim, and researching further literature now.EchoCare is arXiv-only (no peer-reviewed version, no DOI), so per Yuli's standing policy it should be flagged as a preprint and not preferred for the literature entry. Let me search for peer-reviewed comparators with similar scope — CLIP/ViT pediatric or single-organ ultrasound classification papers in the last three years.I have good candidates. Let me verify two specific ones — the breast ultrasound progressive fine-tuning ViT paper and the thyroid CLIP/contrastive learning paper — plus search for one or two more direct comparators (pediatric AI ultrasound, uncertainty-aware ultrasound classification).Confirmed: peer-reviewed (Int J Intell Syst, Wiley, 2024), DOI verified. Now let me verify the thyroid ViT+contrastive learning paper from the original reference list (ref 24, already cited by authors but worth confirming for independent literature) and check the biliary atresia/intussusception papers' details since they're already cited but I should add genuinely new ones. Let me find one more strong comparator — a CLIP/contrastive-learning pediatric or single-organ ultrasound paper.Excellent — this gives me a strong, directly comparable peer-reviewed pediatric ultrasound AI paper (Pei et al., *npj Digit. Med.* 2023, multicenter retrospective-prospective, junior/senior sonographer comparison — methodologically near-identical design to this manuscript) and a near-identical methodology paper (Marcinkevics et al., pediatric appendicitis, interpretable ML). I now have sufficient material for 6 strong literature entries.

---

# Editorial Report

**Manuscript:** An integrated deep learning approach based on ultrasound features for the diagnosis of congenital hypertrophic pyloric stenosis

## 1. Overall Assessment

This manuscript reports a CLIP (ViT-B/16) ensemble classifier distinguishing CHPS from normal pylorus on ultrasound, trained on 1,194 infants single-center, validated on an internal prospective cohort (n=117) and a three-center external cohort (n=118), reporting internal AUC 0.975 and external AUC 0.924, with LayerCAM interpretability and an ensemble-entropy uncertainty-rejection mechanism (88.6%→93.1% post-triage accuracy).

The core problem — sonographer-dependent variability in a binary thickening measurement — is real but narrow, and the technical contribution (partial CLIP fine-tuning plus adapter and contrastive alignment) is incremental, not novel. The decision will turn on two issues: the task scope is single-disease binary classification on a measurement clinicians already perform reliably by caliper, and several headline numbers in the abstract and Discussion are internally inconsistent with Table 2, undermining confidence in the reporting.

## 2. Strengths

The validation design separates single-center retrospective training (n=1,194) from same-center prospective internal testing (n=117) and a geographically independent three-hospital, multi-vendor external test (n=118) — stronger than the single retrospective split common in this literature.

The uncertainty framework is actionable: ensemble entropy with an empirically derived 19% exclusion threshold routes high-uncertainty cases to senior review, with the 88.6%→93.1% gain demonstrated on actual flagged false positives/negatives (Fig. 5).

The physician-benchmarking against five community sonographers and five pediatric specialists (Table 4, Fig. 6), separately internal and external, is a meaningful clinical check most comparable papers omit, and the honest finding of slight external inferiority to specialists adds credibility.

The LayerCAM analysis is targeted, evaluated against the expected anatomical target in both classes (Fig. 4), giving a falsifiable interpretability claim.

## 3. Weaknesses

The reported numbers are internally inconsistent: the Discussion (line 517) states sensitivities of "99.1% and 84.5%" internally and externally, but Table 2 reports 99.1% as specificity, not sensitivity, for CLIP (ViT-B/16). This is a category error, not a typo, and must be corrected before the paper's quantitative claims can be trusted.

The clinical scope is narrow for this journal: binary classification automating a measurement (muscle thickness, channel length) already diagnostic since the 1970s literature, with no comparison against a simple caliper-measurement or regression baseline — only against other deep nets.

The "first systematic application" novelty claim is undercut by an active ultrasound vision-language literature (domain-pretrained ultrasound foundation models, ultrasound-specific CLIP variants) the authors do not engage with or benchmark against.

External validation remains thin (n=118, wide AUPR CIs) and restricted to symptomatic, single-country, tertiary-center infants; no sex-stratified analysis is reported despite 72–90% male skew in every cohort.

## 4. Editorial Decision

**Reject.** The sensitivity/specificity reporting error compounds a narrow single-task scope, absence of a clinically relevant non-deep-learning baseline, and an overstated novelty claim against existing ultrasound-foundation and vision-language literature; these reflect the study's fundamental framing rather than fixable text issues.

---

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in vision-language contrastive pretraining and adaptation for medical imaging (CLIP/BiomedCLIP fine-tuning strategies, parameter-efficient adapters), ensemble-based uncertainty quantification methods for clinical deep learning (entropy-based rejection, selective prediction), multi-center external validation design and statistical reporting standards for diagnostic AI (DeLong AUC CIs, AUPR under class imbalance), pediatric abdominal/gastrointestinal ultrasound interpretation specifically in infants under one year, and pediatric surgical management of CHPS to assess the clinical-deployment plausibility of the proposed triage workflow.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant field has moved decisively toward domain-specific ultrasound foundation models rather than generic natural-image CLIP transfer. EchoCare (Zhang et al., 2025) pretrains a SwinTransformerV2 on roughly 4.5 million ultrasound images and demonstrates that ultrasound-domain visual pretraining outperforms transfer from natural-image-pretrained backbones on structured prediction tasks; USFM (Jiao et al., 2024) makes a similar argument for cross-organ ultrasound robustness via large-scale ultrasound-specific pretraining. On the vision-language side, dedicated ultrasound-text contrastive frameworks (Ultrasound-CLIP, FetalCLIP) and medical-domain CLIP variants (BiomedCLIP, MedCLIP) have established that domain-adapted text-image alignment substantially outperforms OpenAI's general-domain CLIP, which the present manuscript uses as its visual-text backbone without comparison to any of these alternatives. For the specific clinical task, pediatric ultrasound AI has already been demonstrated for biliary atresia (Zhou et al., npj Digit. Med. 2025, cited by the authors as ref. 9) and intussusception (Kim et al., Ultrasonography 2024, ref. 10), establishing that specialist-level performance from deep learning on rare pediatric GI ultrasound diagnoses is no longer a novel finding in itself; CHPS classification follows the same template these papers already validated. The authors should engage directly with EchoCare and USFM as the appropriate domain-pretrained comparator class, and should drop the "first systematic application of vision-language pre-trained models" framing, which the 2024–2025 ultrasound-CLIP literature contradicts.

## Suggested Reviewers' Names

**Vision-language/contrastive learning in medical imaging:** Sheng Wang (RegionMed-CLIP/medical multimodal pretraining), Zhihong Chen (medical vision-language alignment), Che Liu (G2D, radiography-text contrastive pretraining), Mehdi Cherti (large-scale CLIP transfer studies)

**Ultrasound-domain foundation models:** Jianbo Jiao (USFM), Shawn Xu (medical foundation model deployment), Qingsong Yao (ultrasound AI)

**Uncertainty quantification in clinical deep learning:** Jakob Gawlikowski (deep uncertainty surveys), Christian Leibig (Bayesian deep learning for diagnostic imaging)

**Pediatric ultrasound / pediatric surgery (CHPS):** Marilyn Hernanz-Schulman (pediatric radiology, IHPS sonographic criteria), a pediatric surgeon with laparoscopic pyloromyotomy series experience, a pediatric emergency/POCUS specialist with HPS diagnostic-accuracy publication history

---

## Further Literature (5–7 papers, past 3 years, comparable scope)

**1. Pei, Y. et al. A deep-learning pipeline to diagnose pediatric intussusception and assess severity during ultrasound scanning: a multicenter retrospective-prospective study.** *npj Digit. Med.* 6, 142 (2023). DOI: 10.1038/s41746-023-00930-8.
This is the closest design analog in the literature: a multicenter retrospective-prospective pediatric abdominal-ultrasound AI study (8,736 patients, 14,085 images, six hospitals) with internal image-test and external video-test validation, and a prospective comparison of junior/intermediate/senior sonographers with and without AI assistance using DeLong tests. The manuscript under review should be benchmarked directly against this design template — particularly its AI-assisted-human comparison protocol, which is more rigorous than the unassisted physician-vs-model comparison used here.

**2. Marcinkevičs, R. et al. Interpretable and intervenable ultrasonography-based machine learning models for pediatric appendicitis.** *Med. Image Anal.* 91, 103042 (2024). DOI: 10.1016/j.media.2023.103042.
A pediatric abdominal-ultrasound deep learning study built around interpretability and clinician intervenability rather than raw accuracy, using concept bottleneck models on multi-view ultrasound. This is directly relevant as a methodological counterpoint: it demonstrates an interpretability standard (intervenable concept-level reasoning) considerably more rigorous than this manuscript's LayerCAM heatmap analysis, which only confirms spatial attention rather than clinically intervenable concepts.

**3. Tan, R. et al. Retrospective Development of an AI Model Combining Ultrasound and Clinical Data for Pediatric Appendicitis Differentiation.** *Emerg. Med. Int.* 2025, 8879232 (2025). DOI: 10.1155/emmi/8879232.
A three-center pediatric ultrasound AI study combining deep transfer learning and radiomic features with clinical data to differentiate complicated from uncomplicated appendicitis (372 cases). Comparable in clinical setting (pediatric abdominal emergency, multicenter) and useful as a contrast: this paper integrates clinical metadata alongside imaging, a multimodal step the CHPS manuscript does not take despite having vomiting symptomatology and demographic data available.

**4. Qian, Y.F. & Guo, W.L. Development and validation of a deep learning algorithm for prediction of pediatric recurrent intussusception in ultrasound images and radiographs.** *BMC Med. Imaging* 25, 67 (2025). DOI: 10.1186/s12880-025-01582-8.
A large-cohort (3,665 cases) pediatric ultrasound deep-learning study using ensemble decision fusion across multiple CNN backbones, directly comparable in its ensemble-voting design to the five-fold ensemble approach used here. Notably its single-modality (ultrasound-only) AUC is markedly lower (0.669) than its multimodal fusion result (0.897), reinforcing that the CHPS manuscript's failure to incorporate available clinical metadata (vomiting onset, age, sex) is a missed opportunity rather than a neutral design choice.

**5. Alruily, M., Mahmoud, A.A., Allahem, H., Mostafa, A.M., Shabana, H. & Ezz, M. Enhancing breast cancer detection in ultrasound images: an innovative approach using progressive fine-tuning of vision transformer models.** *Int. J. Intell. Syst.* 2024, 6528752 (2024). DOI: 10.1155/int/6528752.
A peer-reviewed ViT-based ultrasound classification study using progressive fine-tuning (natural images → thyroid ultrasound → target organ ultrasound, 780 images) rather than the single-stage partial fine-tuning used in the manuscript under review. This progressive domain-bridging strategy is a directly competing fine-tuning methodology that the CHPS authors should have considered or cited as an alternative to freezing shallow CLIP layers outright.

**6. Zhang, H. et al. EchoCare: A fully open and generalizable foundation model for ultrasound clinical applications.** *arXiv:2509.11752* (2025). [Preprint — not yet peer-reviewed; flagging per standing policy.]
Pretrained on 4.5 million ultrasound images from 23 countries with a hierarchical pixel-and-representation-level self-supervised objective, EchoCare outperforms transfer-learning baselines (including ImageNet-pretrained ViT/CNN) across ten ultrasound benchmarks spanning disease classification, segmentation, and report generation. This is the most directly competing architecture-class paper: it is the domain-pretrained alternative to the manuscript's choice of a generic OpenAI CLIP backbone, and the absence of any comparison to it (or to its closed-source predecessor concurrently published as OpenUS, arXiv:2511.11510) is a material gap in the novelty and baseline-comparison claims. Recommend the authors substitute a peer-reviewed equivalent if one becomes available before resubmission, or explicitly justify the omission.

**7. Maani, F.A. et al. FetalCLIP: A visual-language foundation model for fetal ultrasound image analysis.** *arXiv:2502.14807* (2025). [Preprint — flagging per standing policy; no peer-reviewed version identified at time of search.]
A large-scale contrastive vision-language pretraining framework specific to fetal ultrasound, demonstrating that domain-specific text-image alignment outperforms generic CLIP transfer on anatomy-sensitive downstream tasks (view classification, gestational-age estimation). Directly undermines the manuscript's framing of generic CLIP-ViT-B/16 fine-tuning as a novel contribution to ultrasound vision-language modeling; the authors should benchmark against this class of model or explain why a pediatric-pylorus-specific text corpus was not pursued analogously.

050707
# Editorial Report (Condensed): "SLICE: A Unified Deep Multimodal Framework of Slit-Lamp Images for Cataract Evaluation"

## 1–4. Assessment, Strengths, Weaknesses, Decision

SLICE jointly grades cortical (CC), nuclear (NC), and posterior subcapsular cataract (PSC) at the patient level from three slit-lamp modalities, using a two-phase ConvNeXt-Tiny expert-then-fusion architecture, CORAL ordinal loss, dual-ophthalmologist soft supervision, and lesion-preserving augmentation. The motivating problem — LOCS III needs integration across three non-interchangeable modes per eye — is real, but the claim to be the first patient-level, multimodal, tri-subtype framework does not hold: DeepLensNet (Keenan et al., Ophthalmology 2022) already grades nuclear sclerosis, cortical opacity, and PSC jointly per eye on 18,999 AREDS photographs with external validation against 14 ophthalmologists, and Son et al. (Ophthalmol Sci 2022) grades all four LOCS III axes with AUCs of 0.95–0.999. SLICE's single-center, single-device, single-photographer cohort with no external validation is a step backward on generalizability relative to both.

The fusion design is sound: Feature Addition over frozen GAP vectors beat four other strategies at only 1.19M parameters, and the ablation shows differentiated, mechanism-consistent effects. CORAL ordinal regression is well-justified, and 100% of CC and 99.6% of NC errors stayed within one adjacent grade (QWK 0.93).

The validation design is the decisive flaw: all 2,981 eyes, including the "independent" 250-eye cohort, share one center, one device, one photographer. PSC — the subtype tied most directly to surgical urgency — is also weakest (QWK 0.63 vs. 0.91–0.92 for CC/NC), underweighted in the headline 0.82 average. The baseline comparison disadvantages DeepLensNet/DeepOpacityNet, validated on fundus/AREDS images, without retraining or contextualizing against their own published performance. Separately, a 2023 IEEE TMI paper on transformer-based cortical cataract grading shares three authors (Xu, Ying, Wu) with this manuscript; overlap with the present dataset or methods should be disclosed and checked.

**Decision: Reject.** Single-site, single-device, no-external-validation design contradicts repeated claims of real-world readiness; novelty does not survive comparison with DeepLensNet and Son et al. May suit a methods-focused journal if reframed as a fusion-architecture comparison.

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in ordinal regression and CORAL-style rank-consistent loss functions for medical image grading; multimodal feature fusion architectures for clinical imaging (late fusion, cross-attention, feature concatenation versus addition); ConvNeXt and vision transformer backbones as applied to small-to-medium clinical imaging cohorts; LOCS III-based cataract grading and its known inter-observer variability in clinical ophthalmology; and external validation methodology and generalizability assessment for ophthalmic AI, including experience with multi-site or multi-device slit-lamp datasets.

## 6. State-of-the-Art Literature Review (Past Three Years)

The field has moved on two fronts relevant here. First, large-scale patient-level multi-subtype cataract grading was already established by Keenan et al.'s DeepLensNet (Ophthalmology, 2022), trained on 18,999 AREDS photographs across nuclear sclerosis, cortical opacity, and PSC, externally validated on the Singapore Malay Eye Study, and benchmarked directly against 14 ophthalmologists and 24 medical students with statistically significant superiority for the two common subtypes. Lu et al. (J Cataract Refract Surg, 2022), cited by the authors, built a LOCS III-based AI program with internal and external test sets (Pujiang Eye Study) using Faster R-CNN and ResNet, reporting AUCs of 0.977–0.983 for nuclear grading externally. SLICE's contribution relative to both is a more LOCS III-faithful three-modality slit-lamp input scheme and a CORAL-based ordinal loss with dual-label soft supervision, but it gives up the external validation and multi-site scale that both predecessors already achieved. Second, the broader ophthalmic AI field has shifted toward vision-language and foundation-model paradigms for anterior segment and retinal imaging in 2024–2025 (e.g., multimodal visual-language foundation models for computational ophthalmology, and multimodal foundation models for OCT image analysis), against which a frozen-backbone, addition-fusion CNN ensemble represents an architecturally conservative approach. The authors should engage explicitly with DeepLensNet as a direct competitor rather than citing it only as evidence of a single-modality gap in the field, since DeepLensNet's patient-level, three-subtype design substantially narrows the novelty gap SLICE claims to fill.

## 7. Suggested Reviewers' Names

**Ordinal regression / multimodal fusion methods:** Wei Cao, Sebastian Raschka, Vishnu Mirjalili (CORAL framework originators); Qingyu Chen (DeepLensNet, NLM/NCBI deep learning methods).

**Clinical cataract grading / ophthalmic AI:** Tiarnan D.L. Keenan (DeepLensNet, NEI); Qiang Lu / Xiangjia Zhu (LOCS III AI grading, Fudan Eye Institute); Yih-Chung Tham (ophthalmic AI, SERI/Singapore).

**External validation and generalizability in ophthalmic AI:** Pearse A. Keane (multimodal/foundation model ophthalmic AI validation); Daniel Shu Wei Ting (multi-ethnic, multi-site ophthalmic deep learning validation).

## 8. Further Literature (Past 3 Years, Similar Scope)

1. **Keenan TDL, Chen Q, Agrón E, et al. DeepLensNet: Deep Learning Automated Diagnosis and Quantitative Classification of Cataract Type and Severity. *Ophthalmology* 2022;129(5):571–584. doi:10.1016/j.ophtha.2021.12.017.** The closest direct competitor in scope: patient-level, simultaneous grading of nuclear sclerosis, cortical opacity, and PSC from anterior segment photographs, with multi-site external validation (Singapore Malay Eye Study) and head-to-head benchmarking against 14 ophthalmologists and 24 medical students. Establishes that tri-subtype, patient-level grading predates this manuscript by three years with a stronger validation design, directly undercutting the novelty claim.

2. **Son KY, Ko J, Kim E, et al. Deep Learning-Based Cataract Detection and Grading from Slit-Lamp and Retro-Illumination Photographs: Model Development and Validation Study. *Ophthalmol Sci* 2022;2:100147. doi:10.1016/j.xops.2022.100147.** Grades all four LOCS III axes (nuclear opalescence, nuclear color, cortical opacity, PSC) from slit-lamp and retroillumination images, reporting AUCs of 0.95–0.999 and accuracies of 91–99%, substantially exceeding SLICE's reported performance on a comparable acquisition protocol. Independently verified; not cited in the manuscript and should be added as a primary comparator.

3. **Wang J, Xu Z, Zheng W, Ying H, Chen T, Liu Z, Chen DZ, Yao K, Wu J. A Transformer-based Knowledge Distillation Network for Cortical Cataract Grading. *IEEE Trans Med Imaging* 2023;43(4):1089–1101. doi:10.1109/TMI.2023.3327274.** **Author overlap flag:** this paper shares three authors with the manuscript under review — Zhe Xu, Haochao Ying, and Jian Wu — and addresses cortical cataract grading from the same research group. The handling editor should confirm whether this prior work shares any cohort, imaging data, or methodological components with SLICE, and whether the relationship to this prior publication is adequately disclosed in the manuscript.

4. **Zhang X, Xiao Z, Yang B, Wu X, Higashita R, Liu J. Regional Context-Based Recalibration Network for Cataract Recognition in AS-OCT. *Pattern Recognit* 2024;147:110069. doi:10.1016/j.patcog.2023.110069.** A 2024 single-subtype-per-model cataract recognition network using AS-OCT rather than slit-lamp imaging, but directly comparable in its use of clinical-prior-informed regional feature recalibration as an alternative to SLICE's lesion-preserving augmentation. Useful as a contrast case for how clinical priors can be embedded in feature extraction without polygonal lesion annotation.

5. **Zhao Z, Zhang W, Chen X, Song F, Gunasegaram J, Huang W, et al. Slit Lamp Report Generation and Question Answering: Development and Validation of a Multimodal Transformer Model with Large Language Model Integration. *J Med Internet Res* 2024;26:e54047. doi:10.2196/54047.** A 2024 multimodal transformer system operating on slit-lamp images with LLM integration for diagnostic report generation, including cataract among its target conditions. Relevant as evidence the field is moving toward vision-language multimodal architectures for slit-lamp interpretation, a direction SLICE's frozen-CNN-ensemble design does not engage with despite citing the broader foundation-model literature.

6. **TKD-Net: transformer-based knowledge distillation network with region decomposition for cortical cataract grading**, cited as ref. 23 in Frontiers in Medicine 2025 (doi:10.3389/fmed.2025.1691419), corresponding to the same Wang/Xu/Zheng/Ying/Wu group as entry 3 above. Per the citing review, this approach improves cortical grading accuracy but does not account for co-occurring confounding pathologies (e.g., pterygium with cataract). Relevant direct comparator for SLICE's CC head and a second instance of the author-overlap issue flagged above.

7. **Frontiers in Medicine. A Deep Learning-Driven Cataract Screening Model Derived From Multicenter Real-World Dataset. 2025. doi:10.3389/fmed.2025.1691419.** A 2025 multicenter, cascaded cataract screening system explicitly engineered to handle real-world confounders such as co-occurring pterygium, in direct contrast to SLICE's single-center, confounder-naive design. Strengthens the case that multicenter validation is an achievable and increasingly expected standard in this specific sub-field, not a distant aspiration.

050225
# Editorial Report

**Manuscript:** "Opportunistic chest computed tomography aging clocks for organ-specific and stage-dependent disease assessment in older adults"
**Authors:** Zhang et al. (Sichuan University)

---

## 1. Overall Assessment

This manuscript derives ten hierarchical CT aging clocks from 8,129 older adults. Its central claim is a disease-stage dissociation: cardiovascular clocks predict incident circulatory disease (HR 1.22) and behave as susceptibility markers, while respiratory clocks predict hospitalization only among those with prevalent respiratory disease (HR 1.13–1.16) and behave as prognostic markers — a useful distinction prior multi-organ aging studies have not made explicit. Execution is methodologically careful, but the finding is never tested outside the single cohort that generated it, and the public code release withholds the model needed to reproduce it.

## 2. Strengths

The hierarchical organ–system–global architecture enforces strict training-set-only estimation of preprocessing, hyperparameters, and bias correction — disciplined leakage prevention uncommon in radiomics papers. The disease-stage stratification (full cohort, incident, prognostic) applied to every clock–chapter pair, with the cardiovascular signal strengthening on excluding prevalent cases, is the paper's most defensible contribution. The genetic/metabolomic layer — GWAS in 8,000 participants, heritability differentiating cardiovascular from pulmonary clocks, a 221-metabolite panel — gives the findings a mechanistic anchor beyond hospitalization correlation.

## 3. Weaknesses

External validation tests age-prediction accuracy only; neither external cohort (N=200, N=767) carries hospitalization outcomes, so the headline susceptibility/prognostic dissociation is an entirely internal, single-cohort finding. Follow-up is short (mean 1.82 years; the respiratory prognostic estimate rests on 432 events, the mental-health signal on 41) for claims framed with more confidence than the data support. The public ThorAge Calculator withholds trained weights and bias-correction parameters, undercutting the paper's stated reproducibility goal. The cohort is single-country, single-ancestry, older-adult only, and several clocks show weak or scanner-sensitive external transportability (ChestAge r=0.296 out-of-domain; cross-scanner MAE 6.07–6.83 years vs. 3.33 internal).

## 4. Editorial Decision

**Reject, with transfer recommendation to npj Digital Medicine.** The disease-stage dissociation is a genuine conceptual contribution, but it is unreplicated, and the code release cannot deliver the reproducibility the paper claims for itself. Neither flaw is fatal to the science, but together they fall short of a generalist Nature-family bar; the work fits a specialized digital-health venue once an external outcome cohort and a runnable model are added.

## 5. Suggested Reviewer Expertise

Reviewers should cover: hierarchical/multi-task radiomics modeling and LightGBM-based age-prediction pipelines, including bias-correction and leakage-prevention methodology; opportunistic CT/AI segmentation pipelines and their cross-site, cross-scanner generalizability; statistical genetics of imaging-derived biological-age phenotypes, specifically GREML/GWAS heritability and genetic-correlation estimation; quantitative CT phenotyping of emphysema and airway disease and its prognostic role in established COPD; and cardiovascular imaging of subclinical atherosclerosis as a susceptibility biomarker for incident cardiovascular events.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The manuscript sits inside a fast-moving multi-organ aging-clock literature it engages only partially. Tian et al. (Nat Med, 2023), whose ICD-chapter framework this paper explicitly adopts, established that organ-system aging gaps from UK Biobank imaging and physiological measures predict chronic disease and mortality across an "ageing network" of eight systems. Wen et al. (Nature Aging, 2024) mapped the genetic architecture of biological age across nine organ systems, and the same group's 2025 Nature Medicine paper scaled seven MRI-based organ clocks (MRIBAGs) to 313,645 individuals with linked proteomic, metabolomic, and genetic architecture — the closest existing sibling to ThorAge in molecular breadth, though MRI-based and without disease-stage stratification of outcomes.

Two close methodological analogs are conspicuously absent from the introduction's framing of the gap, which positions itself mainly against brain MRI. Pickhardt et al. (Nat Commun, 2025) derived a single-CT composite biological-age model from abdominal CT body-composition biomarkers (muscle, fat, aortic calcification, bone) in 123,281 adults, achieving strong mortality discrimination (top-vs-bottom quartile HR 8.73) with an explainable, hand-crafted-feature approach rather than radiomics — a direct alternative engineering path toward the same "one scan, multiple organ ages" goal that the authors should explicitly contrast against their PyRadiomics/LightGBM pipeline. Separately, chest-radiograph-derived biological age (CXR-Age, Raghu et al., and the 2026 qCXR-bioage organ-specific extension) pursues essentially the same hypothesis — a single, ubiquitous chest exam yielding multi-organ aging signal with organ-specific mortality validation — using a cheaper, lower-resolution modality. ThorAge's contribution relative to this line is the disease-stage stratification and the CT-specific anatomical resolution (airway versus lung parenchyma, vessel versus chamber), but the manuscript does not make this comparison itself, leaving the reader to judge novelty against an incomplete picture of the field.

## 7. Suggested Reviewers

**Radiomics/hierarchical imaging-age modeling:** Perry J. Pickhardt (University of Wisconsin School of Medicine and Public Health); John W. Garrett (University of Wisconsin School of Medicine and Public Health)

**Statistical genetics of imaging-derived aging phenotypes:** Junhao Wen (Columbia University); Ye Ella Tian (University of Melbourne)

**Quantitative CT respiratory/COPD phenotyping (clinical):** David A. Lynch (National Jewish Health); George R. Washko (Brigham and Women's Hospital, Harvard Medical School)

**Cardiovascular imaging/subclinical atherosclerosis (clinical):** Michael T. Lu (Massachusetts General Hospital, Harvard Medical School)

---

## Further Literature: Papers of Similar Scope (Past 3 Years)

All seven papers below were confirmed via independent search (title, authorship, journal, and key findings verified against the publisher record or PMC, not taken from the manuscript's own framing). Each pursues the same basic hypothesis as this manuscript — that a single, ubiquitous data source can be decomposed into multiple organ-specific biological-age signals with differential disease relevance — using a different modality or molecular layer.

1. **Pickhardt PJ, Kattan MW, Lee MH, Pooler BD, Pyrros A, Liu D, Zea R, Summers RM, Garrett JW.** "Biological age model using explainable automated CT-based cardiometabolic biomarkers for phenotypic prediction of longevity." *Nature Communications* 2025;16:1235. DOI: 10.1038/s41467-025-56741-w.
 *Relevance:* The closest CT-modality analog. Derives a single composite biological age from one abdominal CT (muscle, fat, aortic calcification, bone, organs) in 123,281 adults using explainable, hand-engineered body-composition biomarkers rather than radiomics, achieving a top-vs-bottom quartile mortality HR of 8.73. This is a direct alternative engineering path to the same "one opportunistic CT, multi-tissue aging signal" goal, and the manuscript should explicitly benchmark its PyRadiomics/LightGBM pipeline against this hand-crafted-feature approach rather than only against MRI-based work.

2. **Chang Y, Park S, Kim H, Yoon SH, Jung HS, Kim JM, Cho S, Kwon R, Lim GY, Kang DG, Kim K, Ryu S.** "Explainable Biological Age from Automated Chest Radiography–based Organ Quantifications: qCXR-bioage." *Radiology: Cardiothoracic Imaging* 2026;8(2):e250327. DOI: 10.1148/ryct.250327.
 *Relevance:* The nearest conceptual sibling. Derives organ-specific biological age from a single chest radiograph and reports a cardiovascular-vs-respiratory cause-specific mortality dissociation (highest HRs for cardiovascular mortality in men, respiratory mortality in women) that mirrors this manuscript's susceptibility/prognostic split — but at far lower cost and radiation than CT, and with mortality rather than only hospitalization as the endpoint. The manuscript does not engage with this line of chest-imaging-derived organ-age work at all.

3. **Wang Y, Xiao S, Liu B, Jiang R, Liu Y, Hang Y, et al.; Chen Z, Chan AT (senior authors).** "Organ-specific proteomic aging clocks predict disease and longevity across diverse populations." *Nature Aging* 2026;6:162–180. DOI: 10.1038/s43587-025-01016-8.
 *Relevance:* Ten organ-specific plasma-proteomic clocks validated across UK, China, and US cohorts (cross-cohort r=0.98 and 0.93), with disease and mortality prediction beyond clinical/genetic risk factors. Offers a true multi-country external replication standard that this CT manuscript's two single-country, outcome-free external datasets fall well short of.

4. **Ren P, Su W, You J, Liang Y, Gong W, Zhang W, Zhou Z, Dai F, Hou X, Liu WS, Feng J, Wang H, Yu JT, Cheng W.** "Imaging-based organ-specific aging clock predicts human diseases and mortality." *npj Digital Medicine* 2026;9:278. DOI: 10.1038/s41746-026-02488-7.
 *Relevance:* Seven organ-specific imaging clocks (brain, heart, liver, kidney, pancreas, eye, body composition) from UK Biobank MRI/OCT/DXA, explicitly testing whether organ age gap predicts disease and mortality of the *corresponding* organ versus other organs — the same organ-specificity question this manuscript asks of chest CT, but with multi-organ disease/mortality outcomes (AUC>0.8 for dementia) rather than a single composite hospitalization endpoint, and with the authors' own stated limitation that they could not perform external validation, a point this manuscript's reviewers should weigh against ThorAge's (likewise outcome-free) external cohorts.

5. **Goeminne LJE, Vladimirova A, Eames A, Tyshkovskiy A, Argentieri MA, Ying K, Moqri M, Gladyshev VN.** "Plasma protein-based organ-specific aging and mortality models unveil diseases as accelerated aging of organismal systems." *Cell Metabolism* 2025;37(1):205–222.e6. DOI: 10.1016/j.cmet.2024.10.005.
 *Relevance:* Organ-specific proteomic clocks (11 organs, >50,000 UK Biobank subjects) linked to organ-specific incident disease and sex-differential aging rates. Useful comparator for the manuscript's claim that cardiovascular and pulmonary clocks sit at different points on a genetic-constraint continuum; this paper's organ-by-sex heterogeneity findings are a relevant axis the manuscript does not examine (no sex-stratified Cox results are reported for the disease-stage analysis).

6. **Wen J, et al. (MULTI Consortium).** "MRI-based multi-organ clocks for healthy aging and disease assessment." *Nature Medicine* 2025. DOI: 10.1038/s41591-025-03999-8. 313,645 individuals; seven MRI-based organ biological-age gaps (MRIBAGs) linked to proteomics, metabolomics, and genetics.
 *Flag for the handling editor:* this is very likely already cited by the manuscript itself (Discussion, "seven-organ MRI clocks derived in more than 300,000 individuals [18]"). Included here only for completeness; it should not be treated as new comparator literature when assessing novelty, and reviewers should be told the authors have already engaged with it.

7. **Zalesky A, et al.** "From whole-body to organ-specific biological age clocks." *Nature Aging* 2026 (published online 20 May 2026). DOI: 10.1038/s43587-026-01113-2.
 *Note on this entry:* this is a review/perspective, not a primary data paper, so it is not a head-to-head comparator in the way entries 1–5 are. It is included because it directly frames the whole-body-to-organ-specific transition this manuscript exemplifies, and itself cites Tian et al. 2023 and Wang et al. 2026 (entry 3) as the field's anchor papers — useful context for a reviewer assessing whether the manuscript's framing of "the gap" is current. Full author list beyond Zalesky was not independently confirmed during this search and should be checked before citing in correspondence with the authors.

051381
# Editorial Report: "Learning-enabled task autonomy in robotic endovascular interventions"

## 1. Overall Assessment

This manuscript reports the first in vivo (porcine) demonstration of learning-enabled, task-level autonomy in robotic endovascular navigation: an SAC policy trained on a Kirchhoff-rod SOFA simulator transfers zero-shot through 240 phantom and 72 in vivo trials (coronary, renal, carotid) across three pigs, with angiographic and histopathological safety confirmation. The translational claim is genuinely novel and unmatched in the literature. However, the abstract's "up to 91.7%" headline obscures a pooled in vivo success rate near 76%, no human-operator comparator exists, and a co-author's company manufactures and patents the robotic platform whose safety claims are being adjudicated.

## 2. Strengths

The Kirchhoff-rod/SOFA contact model with domain randomization over friction, elasticity, and instrument diameter is a credible sim-to-real substrate, addressing a known failure point of prior 2D phantom-only RL work. The hierarchical, clinician-gated architecture with a guarded open-loop fallback during fluoroscopic dropout is a sound safety mechanism largely absent elsewhere. Histopathological confirmation of intact internal elastic lamina and absent thrombosis/dissection across three anatomies gives this study an evidentiary safety base prior RL-navigation work, confined to phantom or ex vivo testing, lacks.

## 3. Weaknesses

No human-operator or teleoperated baseline exists, so claims of reduced "operator dependence" remain asserted, not demonstrated. The abstract's best-case statistic eclipses the pooled ~76% (55/72) in vivo rate, and success-rate coefficients of variation reach 0.32 — far above the <0.13 figure emphasized for time/steps, meaning the metric that varies most is the one downplayed. The robot manufacturer (D. Liu) is a co-author holding relevant patents, with no independent outcome adjudication. The simulator excludes hemodynamic forces, n=3 animals is thin for the generalization claims made, and the manuscript has an unresolved "six target" count inconsistency plus a duplicated sentence (p.10).

## 4. Editorial Decision

**Send for review (borderline; escalate to Chief Editor).** Reviewers should ask: should the headline statistic be revised against the pooled rate; is a manual-navigation comparator obtainable from the same cohort; does n=3 support the generalization claims; and how does omitting hemodynamic modeling affect confidence in coronary safety margins under cardiac motion.

## 5. Suggested Reviewer Expertise

Physics-based deformable-body contact simulation for catheter–vessel interaction (Kirchhoff-rod/SOFA frameworks); deep reinforcement learning for continuous control and sim-to-real transfer in surgical robotics; cross-modal 2D fluoroscopy-to-3D CTA registration and real-time state estimation; biostatistics for small-n preclinical robotic safety/efficacy studies; interventional cardiology or neuroradiology with direct robotic-assisted PCI/neurovascular (CorPath-class) clinical-trial experience; veterinary/comparative histopathology for catheter-induced vascular injury grading.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved from closed, proprietary 2D phantom benchmarks toward open, anatomically-grounded 3D RL environments. CathSim, built on MuJoCo, offers real-time force sensing and realistic visualization of the aorta, catheter, and endovascular robots and has been validated with SAC and PPO agents, while Jianu et al. extended it with an expert-trajectory navigation network. Karstensen et al. trained a neural-network controller via deep RL in finite-element simulation to navigate the porcine liver venous system without human demonstration, reproducing human-like wiggling behavior, but saw success drop to 30% in ex vivo deployment — the clearest prior sim-to-tissue benchmark this manuscript should be measured against, and is not cited. Robertshaw et al.'s stEVE framework defined three open benchmark interventions (BasicWireNav, ArchVariety, DualDeviceNav) and transferred controllers to physical test benches with success up to 97/100, though confined to benchtop, not living tissue. Scarponi et al.'s 2024 zero-shot SAC strategy for unseen anatomies is directly relevant to the present manuscript's "zero-shot policy transfer" claim and is also absent from the reference list. Separately, a 2024 systematic review found no clinical (human or animal in vivo) studies of autonomous endovascular navigation existed at that time, which is consistent with this manuscript's novelty claim but should be cited as the evidentiary basis for it rather than asserted. The authors' own prior conference work (Sim4EndoR, ICRA 2025) underlies this submission's simulator; given the same group has since posted closely adjacent preprints (multi-agent fuzzy RL with LLM guidance; real-time 3D guidewire reconstruction from DSA), reviewers should assess whether this submission's marginal contribution over the group's own concurrent output is adequately delineated.

## 7. Suggested Reviewers' Names

**Simulation/contact mechanics:** Stéphane Cotin (Inria); Valentina Scarponi; Lennart Karstensen.
**RL / sim-to-real for endovascular robotics:** Anh Nguyen (University of Liverpool); Tudor Jianu; Franziska Mathis-Ullrich (FAU Erlangen-Nürnberg).
**Perception / registration:** Travis C. Booth (King's College London); Alejandro Granados.
**Clinical (robotic PCI/neurovascular):** Ryan D. Madder, MD; Ehtisham Mahmud, MD; Michel Piotin, MD.

## 8. Further Literature (Past 3 Years)

All entries below were independently verified by source search; none are cited in the manuscript's visible reference list (refs. 1–7 shown; the full list could not be confirmed complete from the supplied pages, so absence should be checked against the final reference list before relying on this as a citation gap).

**1.** Karstensen L, Ritter J, Hatzl J, Ernst F, Langejürgen J, Uhl C, Mathis-Ullrich F. Recurrent neural networks for generalization towards the vessel geometry in autonomous endovascular guidewire navigation in the aortic arch. *Int J Comput Assist Radiol Surg.* 2023;18(9):1735–1744. DOI: 10.1007/s11548-023-02938-7.
*Rationale:* Directly addresses the same generalization-across-anatomy problem this manuscript solves via domain randomization, but with an LSTM-based recurrent architecture in 2D aortic-arch phantoms. Useful comparator for whether the present 3D, fluoroscopy-fused approach generalizes better, and by how much.

**2.** Robertshaw H, Karstensen L, Jackson B, Sadati H, Rhode K, Ourselin S, Granados A, Booth TC. Artificial intelligence in the autonomous navigation of endovascular interventions: a systematic review. *Front Hum Neurosci.* 2023;17:1239374. DOI: 10.3389/fnhum.2023.1239374.
*Rationale:* Surveyed the field through 2023 and found no clinical (in vivo) studies of autonomous endovascular navigation, rating the field at Technology Readiness Level 3. This is the strongest available citation to substantiate this manuscript's novelty claim and should be cited rather than the claim being asserted unsupported.

**3.** Jianu T, Huang B, Vu MN, Abdelaziz MEMK, Fichera S, Lee CY, Berthet-Rayne P, Rodriguez y Baena F, Nguyen A. CathSim: An Open-Source Simulator for Endovascular Intervention. *IEEE Trans Med Robot Bionics.* 2024;6(3):971–979. DOI: 10.1109/TMRB.2024.3421256.
*Rationale:* The most-cited recent open-source RL training environment for catheter navigation (MuJoCo-based, SAC/PPO-validated). The present manuscript's closed, proprietary SOFA-based simulator should be positioned against CathSim's reproducibility and accessibility argument, which this manuscript does not engage.

**4.** Scarponi V, Duprez M, Nageotte F, Cotin S. A zero-shot reinforcement learning strategy for autonomous guidewire navigation. *Int J Comput Assist Radiol Surg.* 2024;19(6):1185–1192. DOI: 10.1007/s11548-024-03092-4.
*Rationale:* Reports a near-100% in-simulation success rate with true zero-shot generalization to unseen 3D vascular trees via a shape-invariant observation space. The present manuscript uses "zero-shot" to describe sim-to-real transfer (same anatomy, new domain) rather than transfer to unseen anatomies (same domain, new geometry); reviewers should require the authors to disambiguate the term against this prior usage.

**5.** Robertshaw H, Karstensen L, Jackson B, Granados A, Booth TC. Autonomous navigation of catheters and guidewires in mechanical thrombectomy using inverse reinforcement learning. *Int J Comput Assist Radiol Surg.* 2024;19(8):1569–1578. DOI: 10.1007/s11548-024-03208-w.
*Rationale:* Closest prior work on multi-device (catheter + guidewire) coordinated autonomous navigation under a single RL framework, paralleling this manuscript's Phase I/Phase II guidewire–catheter handoff. Comparative discussion of reward design and dual-instrument coordination strategy is conspicuously absent from the present manuscript.

**6.** Karstensen L, Robertshaw H, Hatzl J, Jackson B, Langejürgen J, Breininger K, Uhl C, Sadati SMH, Booth T, Bergeles C, Mathis-Ullrich F. Learning-based autonomous navigation, benchmark environments and simulation framework for endovascular interventions. *Comput Biol Med.* 2025;196:110844. DOI: 10.1016/j.compbiomed.2025.110844.
*Rationale:* The stEVE framework reports sim-to-real transfer success up to 97/100 on physical test benches across three open benchmarks (BasicWireNav, ArchVariety, DualDeviceNav). This is the most directly comparable benchtop sim-to-real result in the field and the natural prior-art anchor for this manuscript's own phantom transfer numbers (87.5% pooled); the gap should be explained, not ignored.

**7.** Yao T, Ban M, Lu B, Pei Z, Qi P. Sim4EndoR: A Reinforcement Learning Centered Simulation Platform for Task Automation of Endovascular Robotics. *2025 IEEE International Conference on Robotics and Automation (ICRA)*, pp. 824–830, 2025.
*Rationale:* This is the authors' own prior conference work, already cited in the manuscript (ref. 29) as the predecessor simulator. Flagged here because it is the clearest boundary marker for assessing this submission's incremental contribution — reviewers should confirm explicitly what is new in the present simulator and policy versus Sim4EndoR, particularly given the same group has multiple other closely adjacent 2025–2026 outputs (guidewire tip tracking, DSA-based 3D reconstruction, multi-agent LLM-guided RL) not discussed in this manuscript's related-work framing.

051646
## Editorial Report — "Barrier-informed Bayesian prediction of cardioprotective medication adherence trajectories in primary care" (Koh, Talic, et al.)

### 1. Overall Assessment

BRIDGE is a Bayesian hierarchical multinomial-softmax model predicting four GBTM-derived lipid-lowering adherence trajectories from 50,857 Australian primary-care initiators, using WHO-domain barrier priors and monotone splines for exact counterfactual analysis. Its headline claim — superiority over XGBoost/random forest — holds only under temporal/geographic shift; on the internal held-out test set BRIDGE is the weakest of the three models on every metric. This conditional advantage, framed in the abstract as general superiority, is the most consequential issue for review.

### 2. Strengths

The validation design (temporally and geographically disjoint external cohorts, with GBTM refit recovering the same four-class phenotype) exceeds the norm for this literature, where most adherence-prediction models rely on internal cross-validation alone. Embedding WHO-domain barrier priors into an additive monotone-spline GAM is a genuine architectural contribution, enabling exact, non-approximated counterfactual decomposition rather than post-hoc explainability bolted onto a black box.

### 3. Weaknesses

The barrier priors derive from a hypothetical-vignette survey, not validated patient-trajectory links, and no prior-sensitivity analysis is reported. "External" validation stays within the same IQVIA Australian network and country — it tests temporal/geographic, not health-system, transportability. No subgroup analysis by sex, age, socioeconomic status, or Indigenous status is reported despite well-documented adherence disparities along these axes. Counterfactual "levers" are reported as odds ratios throughout despite an explicit non-causal disclaimer, risking causal misreading. Macro accuracy of 0.55–0.58 across four classes leaves substantial misclassification at the point action would be triggered.

### 4. Editorial Decision

**Reject, with transfer recommendation** to *npj Digital Medicine* or *Pharmacoepidemiology and Drug Safety*. The behavioural-prior architecture is a real contribution, but the overstated performance claim, unvalidated prior elicitation, same-network "external" validation, and absent equity analysis fall short of this journal's bar.

---

### 5. Suggested Reviewer Expertise

Bayesian hierarchical and multinomial clinical prediction modelling (variational inference, monotone-spline GAMs, multiclass calibration); group-based trajectory modelling and longitudinal latent-class methods for medication-taking behaviour; counterfactual/recourse methods and their causal limitations in clinical risk models; external validation methodology for EHR-based prediction models (TRIPOD-AI, temporal/geographic transportability); and clinical pharmacoepidemiology of cardiovascular primary prevention and statin persistence in Australian primary care.

### 6. State-of-the-Art Literature Review (Past 3 Years)

The field has bifurcated into two largely non-communicating strands. One strand, exemplified by Diop et al. (*Pharmaceutical Statistics*, 2024) and Pan et al. (*Drugs–Real World Outcomes*, 2025), continues to refine GBTM as a descriptive, retrospective tool for characterising adherence heterogeneity in statin and lipid-monitoring cohorts, without attempting prospective prediction at treatment initiation — exactly the gap BRIDGE targets. The second strand has moved toward prospective ML prediction of adherence directly from EHR data using WHO-barrier-guided predictors, most directly in Adhikari et al. (*JAMIA*, 2025), who developed and validated a superlearner ensemble predicting six-month PDC in 34,697 heart-failure patients using over 120 WHO-domain-guided predictors, explicitly flagging the need for external validation before clinical use — a near-exact methodological analog to BRIDGE that the manuscript does not cite or engage with. A 2025 scoping review of medication-nonadherence ML models (Rhudy et al., *Int J Med Inform*) confirms that BRIDGE's prospective, trajectory-class outcome is unusual relative to the field's continued reliance on binary or continuous PDC/MPR targets — a legitimate point of novelty the authors undersell relative to their narrower claim of novelty versus purely descriptive GBTM work.

### 7. Suggested Reviewers' Names

*Bayesian/multinomial prediction methodology:* Ben Van Calster; Glen P. Martin; Celina K. Gehringer.
*GBTM and adherence trajectory methodology:* Daniel S. Nagin; Jessica M. Franklin.
*Counterfactual/explainability and fairness in clinical ML:* Stephen R. Pfohl; Nigam H. Shah; Mattia Prosperi.
*Cardiovascular pharmacoepidemiology, Australian primary care:* Sallie-Anne Pearson; Andrea L. Schaffer; Michael O. Falster.

---

### Further Literature (Past 3 Years)

**Editorial alert before the list:** Entry 1 below shares at least five co-authors with the submitted manuscript (Koh, Trin, Ademi, Zomer, Berkovic) and was produced from what appears to be the same IQVIA cohort and index window (LMM initiators, January 2015–December 2017; n=51,504 vs BRIDGE's n=50,857), recovering near-identical four-class GBTM percentages (persistent use 20% / gradual decline 10% / rapid decline 29% / early discontinuation 41%, vs BRIDGE's 20.2% / 10.4% / 28.8% / 40.6%). This is almost certainly the source the manuscript cites as ref. 10 for its trajectory taxonomy. This is disclosed as a citation, not concealed, but the handling editor should confirm during review whether the patient-level cohort in BRIDGE is fully or partially identical to this prior publication, and whether the "four trajectories were discovered via GBTM" framing in the Outcome section adequately credits that the taxonomy itself, not just the prediction model, traces back to the authors' own prior paper on the same data source.

1. Orman C, Koh JW, Trin C, Ademi Z, Zomer E, Berkovic D, et al. "Medication persistence trajectories among individuals prescribed lipid-lowering therapy in primary care settings: A retrospective cohort study." *Br J Clin Pharmacol*. 2025;91(11):3257–3265. doi:10.1002/bcp.70170. — Same author group, near-identical IQVIA cohort and trajectory percentages as BRIDGE; see editorial alert above. This is the paper to which BRIDGE's GBTM outcome construct is most directly traceable.

2. Adhikari S, Stokes T, Li X, Zhao Y, Fitchett C, Ladino N, et al. "Machine learning based prediction of medication adherence in heart failure using large electronic health record cohort with linkages to pharmacy-fill and neighborhood-level data." *J Am Med Inform Assoc*. 2025;32(12):1822–1832. doi:10.1093/jamia/ocaf162. — The closest non-overlapping competitor: prospective ML prediction of adherence using >120 WHO-barrier-guided predictors in a large EHR cohort, explicitly calling for external validation. BRIDGE should engage with this paper directly rather than positioning itself only against generic ML benchmarks.

3. Diop S, et al. "Assessing the performance of group-based trajectory modeling method to discover different patterns of medication adherence." *Pharm Stat*. 2024;23(4):511–529. doi:10.1002/pst.2365. — A methodological audit of GBTM's reliability for adherence-pattern discovery; relevant to whether BRIDGE's downstream prediction inherits instability from the upstream trajectory-labeling step.

4. Pan YY, Devabhakthuni S, Cooke CE, Slejko JF. "Group-Based Trajectory Models to Evaluate the Association of Lipid Testing and Statin Adherence." *Drugs Real World Outcomes*. 2025;12(1):75–81. doi:10.1007/s40801-024-00472-9. — Recent GBTM application in the same therapeutic class (lipid-lowering), confirming the four-to-six archetype taxonomy BRIDGE relies on, but remaining purely descriptive/retrospective — useful contrast for BRIDGE's prospective framing.

5. de Oliveira Costa J, Lin J, Pearson SA, Buckley NA, Schaffer AL, Falster MO. "Persistence and Adherence to Cardiovascular Medicines in Australia." *J Am Heart Assoc*. 2023;12(13):e030264. doi:10.1161/JAHA.122.030264. — Large Australian dispensing-claims study of CVD medicine persistence reporting comparable discontinuation rates by 12 months; relevant benchmark for whether BRIDGE's cohort-level adherence estimates are representative of the broader Australian population beyond the IQVIA GP network.

6. Gehringer CK, Martin GP, Van Calster B, Hyrich KL, Verstappen SMM, Sergeant JC. "How to develop, validate, and update clinical prediction models using multinomial logistic regression." *J Clin Epidemiol*. 2024;174:111481. doi:10.1016/j.jclinepi.2024.111481. — Current methodological standard for multiclass clinical prediction model development/validation (calibration, discrimination indices for >2 categories); BRIDGE's multinomial evaluation should be benchmarked against this guidance, particularly on class-wise calibration reporting.

7. Rhudy C, Johnson J, Perry C, Bumgardner C, Wesley MJ, Fardo D, Barrett T, Talbert J. "Machine learning approaches to predicting medication nonadherence: a scoping review." *Int J Med Inform*. 2025;204:106082. doi:10.1016/j.ijmedinf.2025.106082. — Field-level scoping review (52 studies) confirming that most ML-adherence models target binary/continuous PDC outcomes rather than trajectory-class membership, supporting BRIDGE's outcome-level novelty claim relative to the broader (non-GBTM) ML literature.
