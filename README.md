# Trackrad202512456
034848 Reviewer Consensus: Major Convergent Criticisms
All three reviewers independently converged on the same core objection: F2Med is an engineering integration of known components (federated averaging, knowledge distillation, CoT supervision, parameter-efficient fine-tuning) rather than a methodologically novel paradigm. Reviewer #2 and #3 both explicitly state the framework does not introduce a fundamentally new learning principle. This is a fatal novelty concern that cannot be addressed through revision at this stage.
The baseline comparison is structurally unfair, flagged by Reviewers #2 and #3 and pre-identified in the pre-review assessment. Centralized baselines (RETFound, CONCH, MUSK, BiomedGPT) are fine-tuned on public test sets, while F2Med pre-trains on proprietary curated institutional data (OphFMD, GasFMD, PulFMD) unavailable to any comparator. This conflates data advantage with architectural advantage and is not resolvable by revision without rebuilding the evaluation entirely.
The "foundation model" claim is overstated. The system trains three disease-specific models (ocular, gastric, lung), not a single unified transferable model. 96.56% of OphFMD derives from synthetic retinal images. The CoT reasoning corpus covers only 20 patient cases. Reviewer #2's characterisation — "large integrated training pipeline" rather than a foundation model — is precise and damaging.
Federated realism is undemonstrated. Knowledge distillation relies on a dedicated hub and shared distillation data, which approximates centralized training. No asynchronous communication analysis, privacy leakage quantification, or communication cost benchmarking is presented. Reviewer #3 explicitly notes the code repository contains only a README.

Editorial Decision: Reject
The three reviewers — including one who reviewed the code — unanimously identify non-revisable structural flaws: the comparative evaluation design cannot be corrected without replacing the experimental backbone; the novelty claim is undermined by the architecture itself; and the federated deployment scenario is closer to a simulation than a real-world implementation. Reviewer #2 explicitly recommends rejection. Reviewer #3 concludes the gap between claims and evidence requires "significant strengthening rather than minor polish."
The Chief Editor's pre-circulation note anticipated that baseline comparison would be a major reviewer concern — it was, across all three reports. Elena Bellafante's internal note acknowledges this as a likely "major flaw" while remaining open to OTR, but the reviewer reports returned are more damaging than anticipated, and the absent code substantially worsens the reproducibility picture.
The correct decision is outright rejection. This is not a borderline case upon review. The appropriate transfer venue is npj Digital Medicine or Medical Image Analysis, with a recommendation to reframe the contribution as a federated distillation pipeline for multi-domain medical imaging rather than a foundation model, rebuild the baselines under matched data conditions, and conduct a genuine federated deployment evaluation on geographically distributed infrastructure.

039557 Multi-Reader Study

---

## 1. Overall Assessment

This manuscript reports PE-AI, a CTPA-based deep learning system generating patient-level PE classification and conditional slice-level evidence for radiologist review. The system is developed on RSPECT (n = 6,461) and evaluated across three external settings: RadFusion (US public, n = 1,742), a Chinese multicenter clinical cohort (CN-Clinical, n = 9,977), and a Chinese emergency cohort (CN-ED, n = 95) used for a four-reader retrospective reader study. The work is technically rigorous and unusually transparent regarding performance boundaries — particularly the central versus non-central PE stratification and the honest framing of the reader study as retrospective. These qualities distinguish it from most CTPA-AI papers. Two concerns dominate, however. The reader study (n = 27 PE-positive cases, n = 4 readers, single institution) is structurally underpowered and cannot isolate the incremental value of slice-level evidence from the patient-level prediction. Separately, probability calibration is unreported, and slice-level evaluation is restricted to patient-level true positives with available annotations — leaving false-negative and true-negative slice behaviour entirely uncharacterised.

---

## 2. Strengths

External validation across 11,814 examinations spanning a US public cohort, a seven-year Chinese multicenter clinical series, and a consecutive emergency cohort provides scanner, protocol, and geographic heterogeneity rarely achieved in CTPA-AI work. Maintaining patient-level AUCs of 0.925–0.937 on a threshold fixed at RSPECT validation is a credible signal of generalisation. The architecture — ConvNeXt-tiny backbone for 2.5D feature extraction, ViT-based slice aggregation, Transformer-based sequence classifier, and auxiliary slice-level classifier trained end-to-end — is coherently designed and reproducibly documented. The comparator evaluation is notably rigorous: six prior published methods were retrained under identical RSPECT conditions, with the two strongest (Islam et al. 2024; Hu et al. 2025) carried forward to external cohorts. The non-central PE stratification is the most clinically informative finding: PE-AI's external AUC of 0.886–0.903 in non-central PE exceeds both comparators by 0.03–0.08 units, with lower false-positive burden at matched 85% sensitivity.

---

## 3. Weaknesses

The reader study is critically underpowered. Ninety-five consecutive cases over one week yield 27 PE-positive examinations, from which no robust subgroup inference can be drawn; the post-hoc hard-case analysis involves three positive cases. Each experience level is represented by one reader. The retrospective within-reader design (unaided then PE-AI-assisted, 1-month washout) cannot eliminate recall bias and includes no patient-level-prediction-only control arm, so the incremental contribution of the slice-level output cannot be isolated. These limitations are structural and cannot be addressed by manuscript revision.

Probability calibration is absent. PE-AI's continuous output drives both the operating threshold and the slice-level evidence, yet no calibration curves, Brier scores, or expected calibration error are reported. Miscalibrated probabilities would directly distort the clinical utility of the slice-level output and the PPV advantages claimed. Slice-level performance (AUC 0.959–0.972; coverage 97.3–98.9%) is evaluated only on patient-level true-positive examinations with available reference annotations. Behaviour on true-negative and false-negative examinations — where erroneous slice highlights direct radiologist attention to uninvolved vessels — is uncharacterised.

Subgroup and demographic reporting is inadequate. Performance by age, sex, or body habitus is not provided. CN-Clinical spans 2018–2025; performance by scanner generation or acquisition year is absent, precluding assessment of temporal drift.

---

## 4. Editorial Decision

**Reject.** The reader study is a central and prominently positioned element of the paper but is structurally insufficient to support the reader-assistance claims: n = 27 positives, no control arm for slice-level evidence, single site. This is not correctable by revision. The absence of calibration reporting and incomplete slice-level characterisation compound the concern. The model development and multicohort validation components are of sufficient quality for a specialist journal once calibration and full slice-level analysis are addressed. Transfer to *npj Digital Medicine* or *Radiology: Artificial Intelligence* is recommended.

---

## 5. Suggested Reviewer Expertise

Reviewers should include specialists in: (1) 3D medical image analysis with experience in volumetric CT classification pipelines, multi-task learning, and 2.5D/ViT-based feature extraction; (2) statistical methodology for diagnostic accuracy studies, including sample size estimation for reader studies, McNemar's test, calibration assessment, and DeLong's method for AUC comparison; (3) thoracic radiology and CTPA interpretation in emergency settings, with direct experience in PE diagnosis across embolus locations including subsegmental disease; (4) clinical implementation of AI-assisted diagnostic tools, including familiarity with FDA SaMD guidance, the 510(k) triage-tool landscape (Aidoc, CINA-PE), and workflow integration challenges.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The CTPA-based PE detection literature has matured considerably since the RSPECT challenge (Kaggle 2020), with recent work shifting from single-institution AUC benchmarking toward external validation, reader interaction studies, and clinical deployment evaluation. Islam et al. (*Medical Image Analysis*, 2024) introduced a two-stage approach — slice-level detection followed by patient-level aggregation — that achieved strong RSPECT validation performance and is used by the authors as a primary comparator. Hu et al. (2025) reported an end-to-end examination-level design with differentiated performance by embolus location, directly contextualising PE-AI's non-central PE results. In the clinical deployment space, Rothenberg et al. (*Radiology*, 2023) conducted the first prospective evaluation of AI triage for PE on CTPA, finding that a commercially available system (Aidoc) reduced wait times for positive studies but did not improve overall radiologist accuracy or turnaround times — a result that directly challenges the translational optimism implicit in the PE-AI reader study framing. A meta-analysis of FDA-approved AI algorithms (DePry et al., *Cureus*, 2025) pooled six retrospective studies (n = 9,102) of Aidoc and CINA-PE, reporting sensitivity of 92.5% and specificity of 98.2%, providing a benchmark against which PE-AI's sensitivity of 85–89% should be contextualised. Li et al. (*Frontiers in Medicine*, 2025) reviewed current limitations of AI in CTPA, emphasising heterogeneity of external validation and the persistently challenging nature of subsegmental and non-central emboli — precisely the boundary PE-AI characterises, but without resolving it. A multicenter validation of the uAIDiscover PE system (Frontiers in Molecular Biosciences, 2026) evaluated 600 patients across three Xinjiang hospitals and provides a direct comparator in the Chinese clinical context. Against this landscape, PE-AI's non-central PE stratification and the explicit slice-level evidence framework are substantive contributions. However, the paper does not sufficiently engage with the emerging evidence that AI triage for PE, even when accurate, does not automatically translate into improved reader performance or patient-level outcomes — a gap that the underpowered reader study fails to credibly address.

---

## 7. Suggested Reviewer Names

**Technical – deep learning and medical imaging:**
- Thomas Weikert (University Hospital Basel; CTPA AI, Aidoc validation)
- Bram Stieltjes (University Hospital Basel; CT-based deep learning)
- Gregor Sommer (University Hospital Basel; CTPA-AI deployment)
- Hayit Greenspan (Tel Aviv University; medical imaging deep learning)

**Statistical methodology – diagnostic accuracy and reader studies:**
- Lotfi Senhadji (Univ. Rennes; medical image statistical validation)
- Andriy Fedorov (Harvard/BWH; imaging biomarker reproducibility)

**Thoracic radiology / clinical PE:**
- Sebastian Ley (Diakovere Hospital Hannover; thoracic radiology, PE imaging)
- David Murphy (Stanford; thoracic CT, AI-assisted radiology)

**Clinical deployment / regulatory:**
- Keith Dreyer (Mass General Brigham; AI in radiology deployment)
- Curtis Langlotz (Stanford; radiology AI evaluation and FDA context)

---

## 8. Further Literature

The following six papers share direct scope with this manuscript — multicohort or external validation of CTPA-AI for PE, reader-assistance evaluation, or slice/lesion-level evidence generation — and should be considered both as contextual benchmarks and as required citations.

**Islam NU, Zhou Z, Gehlot S, Gotway MB, Liang J.** Seeking an optimal approach for computer-aided diagnosis of pulmonary embolism. *Medical Image Analysis* 2024; 91:102988. DOI: 10.1016/j.media.2023.102988. — The primary two-stage comparator used in this manuscript. Slice-level detection followed by patient-level aggregation on RSPECT achieves strong internal performance; the paper's external validation is limited, which PE-AI explicitly improves upon. Direct head-to-head comparison in the authors' external cohorts is a key differentiator of the present submission.

**Kahraman AT, Fröding T, Toumpanakis D, et al.** Enhanced classification performance using deep learning based segmentation for pulmonary embolism detection in CT angiography. *Heliyon* 2024; 10:e38118. DOI: 10.1016/j.heliyon.2024.e38118. — nnU-Net segmentation-to-classification pipeline trained on 700 single-institution CTPAs and validated externally on RSPECT and FUMPE. Achieves sensitivity 96.1% and specificity 94.6% internally. Segmentation-based localisation is a competing approach to PE-AI's auxiliary slice-level classifier and provides relevant methodological contrast.

**Langius-Wiffen E, de Jong PA, Hoesein FAM, et al.** Retrospective batch analysis to evaluate the diagnostic accuracy of a clinically deployed AI algorithm for the detection of acute pulmonary embolism on CTPA. *Insights into Imaging* 2023; 14:102. DOI: 10.1186/s13244-023-01454-1. — Large-scale retrospective evaluation of a clinically deployed, FDA-approved AI algorithm (Aidoc) across 3,316 CTPAs at two Dutch institutions. The AI detected 23 false-negative PE versus 60 missed by radiologists. Provides a real-world commercial deployment benchmark and directly contextualises the reader-assistance claims of the present manuscript.

**Rothenberg SA, Savage CH, Abou Elkassem A, et al.** Prospective evaluation of AI triage of pulmonary emboli on CT pulmonary angiograms. *Radiology* 2023; 309(1):e230702. DOI: 10.1148/radiol.230702. — The first prospective reader-interaction study for AI-based PE triage. Commercially available AI (Aidoc) reduced wait times for positive studies but did not improve radiologist accuracy or overall report turnaround. This null result on reader performance directly contradicts the optimistic framing of the PE-AI reader study and is the most important contextual reference the manuscript underweights.

**DePry JL, Wexler R, Rosman IS, et al.** Performance of FDA-approved AI algorithms in detecting acute pulmonary embolism on CTPA: a meta-analysis of real-world retrospective studies. *Cureus* 2025; 17(10):e94391. DOI: 10.7759/cureus.94391. — Pooled analysis of six retrospective studies (n = 9,102) of Aidoc and CINA-PE; sensitivity 92.5%, specificity 98.2%. These pooled commercial benchmarks exceed PE-AI's reported sensitivity of 85–89% and should be explicitly acknowledged, particularly given that PE-AI was not evaluated in a prospective or post-market surveillance setting.

**Langius-Wiffen E, Nijholt IM, van Dijk RA, et al.** An artificial intelligence algorithm for pulmonary embolism detection on polychromatic computed tomography: performance on virtual monochromatic images. *European Radiology* 2024; 34(1):384–390. DOI: 10.1007/s00330-023-10048-w. — Evaluation of an established PE-AI algorithm on spectral CT virtual monochromatic images (VMI) versus conventional polychromatic images in 114 consecutive patients. Demonstrates that models trained on conventional CT may degrade on different reconstruction modalities — directly relevant to PE-AI's evaluation across heterogeneous Chinese CT scanner types and acquisition protocols in CN-Clinical.

046521 Person-Centered Dementia Care

## 1. Overall Assessment

This manuscript presents a sociotechnical framework for translating AI-enabled assistive robotics into home-based dementia care, synthesising primary deployment data from the NIH-funded MARSS project with qualitative expert interviews across five informants. The central claim is that a five-pillar architecture — covering hardware resilience, redefined HITL control, a tiered intervention ladder, privacy-preserving computation, and uncertainty-aware decision-making — provides a translational roadmap for bridging the sim-to-real gap. The work is interdisciplinary and the deployment context is clinically meaningful. However, fundamental methodological and transparency failures preclude publication at this stage.

---

## 2. Strengths

The manuscript's grounding in genuine in-home deployment data is its most defensible contribution. The MARSS platform's documented failure modes — sunlight-induced docking failures corrected by infrared sensor integration, LiDAR motor burnout under continuous domestic use addressed via software sleep cycles, and carpet-induced localisation drift resolved by fusing wheel odometry with LiDAR scan-matching — constitute concrete failure-mode documentation that the SAR literature, dominated by short supervised demonstrations, largely lacks. The five-tier escalation ladder (passive monitoring → automated prompt → social nudge → caregiver alert → emergency dispatch) is a clinically coherent formalisation of the assist-as-needed principle, with appropriate linkage to learned helplessness literature and disease-stage prescriptive deployment. The treatment of the privacy-utility paradox is empirically grounded in MARSS focus group findings, with the observation that caregivers consistently prioritise functional safety over absolute data confidentiality carrying direct implications for consent frameworks and privacy-by-design engineering. Finally, the interdisciplinary author composition — spanning mechanical engineering, nursing science, biomedical informatics, robotics, care ethics, and computer science — is genuinely unusual and permits triangulation across failure logs, clinical assessments, and bioethics analysis within a single study.

---

## 3. Weaknesses

The empirical backbone is critically underpowered. Five expert informants and five PLWD–caregiver dyads cannot support a generalisable translational framework. The manuscript reports no saturation criteria, no inter-rater reliability metric (e.g., Cohen's κ), and no structured codebook for the conventional content analysis; the thematic categories in Table 1 are therefore not independently reproducible. A manuscript advancing architectural pillars for real-world deployment requires demonstrably rigorous qualitative methods, which are absent here. Second, an unremoved internal author note at lines 247–248 — "however this is still in progress the system we tested with didn't work as we wanted so not sure if you want to add it" — reveals that the activity recognition module central to Pillar 1 was non-functional at submission, and that the authors were uncertain whether to disclose this. This is a material transparency failure that independently disqualifies the work. Third, the manuscript does not cite the authors' own substantially overlapping prior abstract (Wang, Arthanat, Begum et al., *Innovation in Aging*, 2025, DOI: 10.1093/geroni/igaf122.1543), which reports the same MARSS deployment, the same five-dyad cohort, and the same HITL design modifications. This undisclosed prior disclosure must be resolved editorially before any review process begins. Finally, the UQ pillar conflates calibration failure with hallucination in a technically imprecise formulation, and no UQ framework — conformal prediction, Monte Carlo dropout, or ensemble methods — is implemented or evaluated in the MARSS system; the pillar is a design aspiration, not a demonstrated capability.

---

## 4. Editorial Decision

**Reject.** Three non-revisable problems govern this decision: the qualitative evidence base is insufficient and methodologically under-specified; an internal note reveals that a core system component was non-functional at submission, constituting a transparency failure; and an undisclosed prior publication by the same team on the same dataset raises prior disclosure concerns that must be resolved before any review can proceed. Authors are encouraged to consider resubmission to *npj Digital Medicine* or *JAMIA* after substantially expanding the cohort, declaring prior publications, and resolving internal inconsistencies. Should the authors address these issues and resubmit, reviewers should be asked to adjudicate: (1) whether the qualitative sample achieves saturation; (2) whether the prior abstract disclosure represents redundant publication; and (3) whether the UQ pillar rests on any implemented methodology.

---

## 5. Suggested Reviewer Expertise

Reviewers should include expertise in the following areas: (1) sim-to-real transfer and hardware-software co-design for autonomous mobile robots operating in unstructured domestic environments; (2) socially assistive robotics for populations with cognitive impairment, with specific experience in longitudinal in-home deployment and outcome measurement; (3) qualitative research methodology in health informatics, including conventional content analysis, thematic saturation assessment, and inter-rater reliability in multi-coder qualitative studies; (4) privacy-preserving machine learning and federated learning for edge-deployed healthcare systems; and (5) person-centred dementia care, with clinical experience in ADRD management, caregiver burden assessment, and assistive technology adoption.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field of in-home socially assistive robotics for dementia has developed rapidly since 2022. Ponce Torres et al. (*Applied Sciences*, 2024) surveyed ambient assisted living deployments across European care settings, confirming that sensor reliability and flooring-dependent navigation remain the dominant failure modes — a finding this manuscript corroborates but does not substantially advance. Díaz-Boladeras et al. (*ACM THRI*, 2024, DOI: 10.1145/3700889) proposed a three-cycle human-centred framework (Engagement → Automation → Efficacy) for SAR design with PLWD that provides a comparable and arguably more operationally grounded translational scaffold, including a four-year case study on cognitive stimulation therapy delivery. The present manuscript neither cites nor differentiates itself from this directly competing framework. On the LLM-in-robotics front, a parallel RL-plus-LLM framework for dementia ADL support (arXiv:2501.17206) addresses the social intelligence deficit this manuscript identifies in its behavioural data constraint section, and offers more technically specified solutions. The JMIR Human Factors evaluation of an LLM-integrated SAR in geriatric outpatient care (2025, DOI: 10.2196/76496) provides a contemporaneous and higher-powered comparator (three-wave mixed-methods, clinical setting) that sets a methodological benchmark the present paper does not meet. On privacy, the Radiology:AI review of federated learning and UQ in medical imaging (2024, DOI: 10.1148/ryai.240637) demonstrates that the field has moved well beyond conceptual advocacy for federated approaches toward validated architectural implementations — a gap the present manuscript's UQ pillar does not close. The manuscript's most distinctive claim — that collaborative autonomy rather than total autonomy is the correct design target for dementia robotics — is well-supported by the literature but is not new: the specific application to dementia care has been articulated by the EmPRISE Lab at Cornell (cited in the manuscript itself). The translational five-pillar synthesis is the paper's genuine contribution, but requires a substantially larger and more rigorously analysed evidence base to be credible at this level.

---

## 7. Suggested Reviewer Names

**Socially Assistive Robotics / In-Home Deployment:**
- Maja Matarić (USC, EmPRISE Lab, SARs for cognitive impairment)
- Selma Šabanović (Indiana University, social robotics and dementia care)
- Wendy Rogers (University of Illinois, aging and assistive technology)

**Qualitative Research Methods / Dementia Care Implementation:**
- Wendy Moyle (Griffith University, SAR trials in dementia)
- Sarah Szanton (Johns Hopkins, home-based dementia care implementation)

**Privacy-Preserving ML / Federated Learning in Healthcare:**
- Farhad Maleki (McGill, federated learning and clinical AI)
- Mohammad Ghassemi (Michigan State, privacy-preserving health AI)

**Uncertainty Quantification in Clinical AI:**
- Ghulam Rasool (Moffitt Cancer Center, UQ in mission-critical AI systems)

---

## 8. Further Literature — Thematically Similar Work (Past 3 Years)

The following papers share substantial scope with the manuscript under review, spanning in-home SAR deployment, collaborative autonomy in dementia care, and the sociotechnical ethics of assistive robotics. Authors should engage with each of these in any revised submission.

1. **Cruz-Sandoval D, Tentori M & Favela J** (2024). A Framework to Design Engaging Interactions in Socially Assistive Robots to Mitigate Dementia-Related Symptoms. *ACM Transactions on Human-Robot Interaction*, DOI: 10.1145/3700889. Proposes a three-cycle design framework (Engagement → Automation → Efficacy) grounded in a four-year development programme with PLWD, including autonomous delivery of Cognitive Stimulation Therapy. This is the most directly competing translational framework in the literature and is not cited in the submitted manuscript.

2. **Voinea C & Wangmo T** (2025). Socially Assistive Robots and Meaningful Work: The Case of Aged Care. *Humanities and Social Sciences Communications*, 12:1070, DOI: 10.1057/s41599-025-05498-0. Examines how SAR design choices — particularly around task allocation and degree of autonomy — affect the meaningfulness of caregiver work and, by extension, care recipient well-being. Provides an ethical framework for the collaborative autonomy paradigm that the submitted manuscript advocates but does not ground theoretically.

3. **Skowronski A et al.** (2024). Exploring the Viability of Socially Assistive Robots for At-Home Cognitive Monitoring: Potential and Limitations. *International Journal of Social Robotics*, DOI: 10.1007/s12369-024-01158-6. Reports a longitudinal in-home deployment of a SAR for cognitive monitoring across ten households (≥10 weeks each), yielding granular data on acceptance, navigation failure modes, and user withdrawal. Directly benchmarks against the present manuscript's MARSS five-dyad cohort in study design and scope.

4. **Hung L, Zhao Y, Alfares H & Shafiekhani P** (2025). Ethical Considerations in the Use of Social Robots for Supporting Mental Health and Wellbeing in Older Adults in Long-Term Care. *Frontiers in Robotics and AI*, DOI: 10.3389/frobt.2025.1560214. Draws on two multi-year Canadian studies (Paro and LOVOT) to examine equity-focused ethical frameworks for SAR deployment, including consent, emotional dependency, and the limits of institutional ethics board oversight. Directly relevant to the manuscript's privacy and autonomy pillars.

5. **Ciuffreda G et al.** (2025). A Field Study to Explore User Experiences with Socially Assistive Robots for Older Adults: Emphasizing the Need for More Interactivity and Personalisation. *Frontiers in Robotics and AI*, DOI: 10.3389/frobt.2025.1537272. Reports an iterative, real-life deployment study of a SAR co-designed with older adults, formal and informal caregivers, identifying interactivity and speech naturalness as the principal acceptance barriers — findings that complement and contextualise the present manuscript's social intelligence deficit analysis.

6. **Qu X & Wang J** (2025, arXiv:2501.17206). Integrating Reinforcement Learning and AI Agents for Adaptive Robotic Interaction and Assistance in Dementia Care. Introduces an RL-plus-GPT-4o framework for autonomous dementia ADL support, including an open-source PLWD behavioural simulator to address the behavioural training data scarcity that the submitted manuscript identifies as a bottleneck. Provides a more technically specified solution to the social intelligence and UQ gaps described in this paper's Pillars 3 and 5.

 Predicting Grade C Periodontitis  048129

---

## 1. Overall Assessment

This manuscript presents a soft-voting ensemble — XGBoost with recursive feature elimination, CatBoost without prior selection, and LightGBM with recursive feature elimination — trained on NHANES 2009–2014 to predict Grade C periodontitis from noninvasive demographic, haematological, and behavioural variables, with external validation on 219 prospectively enrolled patients from a single Chinese tertiary centre. The clinical rationale is sound: grading under the 2018 EFP/AAP framework formally requires radiographic bone loss-to-age ratios, making it inaccessible in primary care. Two concerns dominate. The grade label in the NHANES development cohort is an algebraic proxy from clinical attachment loss (RBL = 100 × CAL / root length), whereas the validation cohort uses true radiographic RBL/age grading — a construct-validity misalignment that is not quantified. External discriminative performance is modest: ROC-AUC 0.648, PR-AUC 0.360, with 30 of 39 Grade C cases (76.9%) misclassified at the default threshold.

---

## 2. Strengths

Ten algorithms evaluated across 13 feature-selection strategies within a nested 5×5 stratified cross-validation, generating 130 candidate configurations pre-specified on Grade C PR-AUC with Brier Skill Score > 0 as selection criteria, materially limits post-hoc optimism. The prospective external validation cohort (ChiCTR2500104002), graded by two blinded raters (ICC = 0.95) in a single pre-specified evaluation, exceeds the split-sample standard prevalent in this field. Permutation importance and SHAP jointly converge on a biologically coherent predictor core — age, dental visit frequency, gender, education, tooth count — and the post-prediction integration of HbA1c and smoking as application-level modifiers preserves methodological orthogonality with the EFP/AAP grade framework.

---

## 3. Weaknesses

The development outcome is a surrogate, not clinical grade. CAL-derived RBL conflates cumulative tissue destruction with disease progression rate — the actual construct the 2018 grade dimension indexes. No estimate of the resulting misclassification magnitude or its directional effect on performance is provided. At the default threshold, 76.9% of Grade C cases are missed; no threshold-sensitivity analysis explores a recall-optimised operating point appropriate for a triage tool. The validation cohort is a Chinese tertiary dental centre — the inverse of the primary-care context the tool targets — and predictor distributions in that cohort are unreported. Subgroup performance across sex, age, and ethnicity is absent despite Grade C disproportionately affecting younger males and TRIPOD+AI compliance being claimed.

---

## 4. Editorial Decision

**Reject.** The structural misalignment between CAL-derived development labels and radiographic validation labels cannot be resolved through revision without NHANES radiographic data. Compounded by discriminative performance that leaves three-quarters of Grade C cases undetected and by absent subgroup analyses incompatible with the population-screening claim, the manuscript does not meet the bar for *Nature Communications*. Transfer to *Journal of Clinical Periodontology*, *Journal of Periodontology*, or *PLOS Digital Health* is recommended.

---

## 5. Suggested Reviewer Expertise

The handling editor should seek four to five reviewers spanning the following areas: (1) clinical prediction modelling in dentistry or oral epidemiology, specifically with experience in the 2018 EFP/AAP staging and grading framework and its epidemiological operationalisation; (2) gradient boosting ensemble methods and model calibration in imbalanced binary classification, with familiarity with the Brier Skill Score and decision curve analysis; (3) survey-weighted statistical analysis and complex sampling design as applied in NHANES-based studies; (4) periodontal clinical practice, specifically specialist-level experience with Grade C periodontitis diagnosis and the radiographic evidence requirements for grading; and (5) health equity and algorithmic fairness in clinical screening tools, particularly across race, sex, and socioeconomic strata in oral health contexts.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field of ML-assisted periodontitis classification has expanded substantially since 2023, but has proceeded along largely parallel and often non-intersecting tracks. Image-based approaches have attracted the most technical investment: a November 2025 *npj Digital Medicine* study from a multicentre consortium demonstrated that AI radiographic analysis surpasses specialist performance for Stage II–IV detection, and YOLO/U-Net architectures applied to periapical radiographs have achieved stage and grade prediction with competitive accuracy in independent test sets (Ameli et al., *Frontiers in Dental Medicine*, 2024). These approaches directly and accurately operationalise the radiographic bone loss component of the 2018 framework, which the present manuscript explicitly avoids. On the non-invasive side, Vu et al. (*Health Informatics Journal*, 2025) applied eleven ML classifiers to NHANES 2009–2014 data with an overlapping feature set and the same three survey cycles, predicting periodontal disease broadly (not grade-specific) using nineteen expert-selected variables. The degree of overlap between that work and the present manuscript — same dataset, same cycles, similar algorithms — is not acknowledged and should be. Ameli et al. (*PLOS Digital Health*, 2024) used BERT applied to clinical notes to predict stage and grade simultaneously, achieving 75% grade-level accuracy in a university clinic population. For treatment outcome modelling, Feher et al. (*Journal of Periodontology*, 2025) at Harvard Dental demonstrated Random Forest-based prediction of one-year post-treatment outcomes using microbiological and clinical variables, while Furquim et al. (*Journal of Clinical Periodontology*, 2025) incorporated salivary multi-omics in a longitudinal cohort to model progression. The present manuscript occupies a distinct niche — noninvasive, general-health-data-only, grade-specific prediction — but its differentiation from Vu et al. (2025) on the same NHANES cycles is underdeveloped, and its performance relative to the radiographic-grade-prediction literature is materially weaker, a gap the discussion does not adequately confront.

---

## 7. Suggested Reviewer Names

**Periodontal Clinical Expert / 2018 EFP/AAP Classification:**
- Maurizio Tonetti (University of Hong Kong)
- Mariano Sanz (Universidad Complutense de Madrid)
- Iain Chapple (University of Birmingham)

**ML in Oral Health / Clinical Prediction Modelling:**
- Hollis Lai (University of Alberta; BERT-based grade classification, *PLOS Digital Health* 2024)
- Jay S. Patel (Temple University; XGBoost-based periodontal prediction from EDR data, *Frontiers in AI* 2022)

**Survey-Weighted Epidemiology / NHANES Methods:**
- Kimon Divaris (University of North Carolina; longitudinal periodontal ML cohort studies)
- Astha Singhal (University of Florida; NHANES-based periodontal ML, *Health Informatics Journal* 2025)

**Health Equity / Algorithmic Fairness:**
- Flavia Teles (University of Pennsylvania; multi-omics periodontitis progression modelling, *Journal of Clinical Periodontology* 2025)

---

## 8. Further Literature

The following six papers published in the past three years share the closest scope with this manuscript — noninvasive or minimally invasive ML prediction of periodontitis severity or grade from clinical, demographic, or general health data — and should be engaged by authors and reviewers alike.

**1. Enevold C et al. (2024). Suitability of machine learning models for prediction of clinically defined Stage III/IV periodontitis from questionnaires and demographic data in Danish cohorts.** *Journal of Clinical Periodontology*, 51(12):1561–1573. doi:10.1111/jcpe.13874.  
The most directly comparable paper in the field. Enevold et al. applied Random Forest, XGBoost, and partial least squares to self-reported questionnaire data and demographic variables in two Danish population cohorts (CAMB, DANHES), targeting clinically established Stage III/IV periodontitis — the staging analogue of the present study's grading target. External cross-cohort AUROC reached 0.64–0.70 with sensitivities of 0.44–0.63, closely mirroring the discriminative ceiling observed here (ROC-AUC 0.648). The parallel performance ceiling across both studies implies a fundamental information limit for noninvasive predictors of severe periodontitis from self-report and demographic data — a conclusion the present discussion does not engage.

**2. Swinckels L et al. (2025). A personalized periodontitis risk based on nonimage electronic dental records by machine learning.** *Journal of Dentistry*, 153:105469. doi:10.1016/j.jdent.2024.105469.  
Swinckels et al. developed a Random Forest model from the BigMouth electronic dental record repository using nonimage dental record features to predict periodontitis risk, and evaluated how far in advance of clinical diagnosis the model could flag high-risk patients — a translational framing directly relevant to the triage application claimed by Zhuang et al. The contrasting input source (dental records vs. general health check variables) and the temporal lead-time analysis offer an important comparator for the present study's novelty claim.

**3. Vu GT et al. (2025). Application of machine learning to predict periodontal disease in US adults: A cross-sectional analysis of NHANES 2009–2014.** *Health Informatics Journal*, 31(4):14604582251394617. doi:10.1177/14604582251394617.  
Vu et al. applied eleven ML classifiers — including logistic regression, Random Forest, XGBoost, and CatBoost — to the same NHANES 2009–2014 cycles used by Zhuang et al., predicting general periodontal disease from nineteen expert-selected features. The overlap in dataset, survey cycles, and algorithm families is substantial. This reference is absent from the manuscript, an omission that is editorially significant.

**4. Ameli N et al. (2024). Classification of periodontitis stage and grade using natural language processing techniques.** *PLOS Digital Health*, 3(12):e0000692. doi:10.1371/journal.pdig.0000692.  
Ameli et al. applied fine-tuned BERT to anonymised periodontal clinical notes and charts to predict 2018 EFP/AAP stage and grade simultaneously, achieving 75% grade-level accuracy in a university clinic setting. Unlike the present study, this approach uses specialist-documented clinical features, making it higher-fidelity but less deployable in general health contexts. The contrast directly frames the accuracy-vs-access trade-off motivating Zhuang et al. and should be cited.

**5. Feher B et al. (2025). Machine learning-assisted prediction of clinical responses to periodontal treatment.** *Journal of Periodontology*, 96(11):1199–1212. doi:10.1002/JPER.24-0737.  
Feher et al. developed a Random Forest model predicting one-year post-treatment outcomes using baseline demographic, clinical, and microbiological parameters. While the outcome differs (treatment response vs. grade), the study contextualises the incremental predictive gain available from microbiological versus purely demographic and haematological inputs — relevant to evaluating whether the present study's feature set is sufficient.

**6. Furquim CP et al. (2025). Developing predictive models for periodontitis progression using artificial intelligence: a longitudinal cohort study.** *Journal of Clinical Periodontology*, 52(10):1478–1490. doi:10.1111/jcpe.14194.  
Furquim et al. applied ML to longitudinal clinical and salivary biomarker data (including IL-1β) from a prospective cohort to model periodontitis progression — directly the biological process that the 2018 grade dimension indexes. The finding that integrating salivary biomarkers with clinical data materially improves predictive accuracy over clinical data alone constitutes a counterargument to the present study's claim that general health check variables are sufficient for grade stratification.

047546 Diagnosis and Prognosis
Reject

---

## 1. Overall Assessment

This manuscript introduces OrthoFoundation, a ViT-based vision foundation model pretrained via a DINO-style student-teacher self-supervised framework on 1,251,655 knee radiographs and MRI slices from OAI, fastMRI, and a private Peking University Third Hospital cohort. The central claim is that a knee-specific foundation model generalises to hip, shoulder, and ankle pathologies, outperforming DINOv2-L, DINOv3-L, and IN-ViT across 17 diagnostic and prognostic tasks. A reader study with three junior doctors is offered as clinical utility evidence.

The engineering is competent, but the manuscript does not meet *Nature Communications* bar. Cross-joint validation is conducted on single-site private cohorts drawn from the same institution that dominates pretraining, and the reader study involves three readers across 120 radiographs and 270 MRI cases — both structural weaknesses that cannot be addressed through revision.

---

## 2. Strengths

The pretraining corpus is large and multi-source, integrating OAI, fastMRI, and a 135,617-patient proprietary multi-centre clinical cohort across three hospital sites, covering heterogeneous MRI acquisition protocols (PDWFS in sagittal, coronal, and axial planes). Patient-level 80/20 partitioning is applied consistently across all 17 downstream tasks, with explicit leakage prevention logic.

The backbone selection is principled and unusual in this literature. Computing five complementary transferability estimators (LogME, PARC, SFDA, PED, ITM) across 30 dataset-estimator combinations and six candidate architectures before committing to DINOv3-L is a methodological contribution that merits independent attention.

Label-efficiency results are credible: AUROC of 94.4% for ACL injury at 12.5% of labelled data versus 92.6% for DINOv2-L under identical constraints, evaluated on fixed hold-out test sets with patient-level random seeding. The hybrid ground-truth protocol — arthroscopic records as the primary gold standard, supplemented by three-reader consensus (Cohen's κ = 0.85) for non-surgical cases — is more rigorous than reader-label-only designs that predominate in this area.

---

## 3. Weaknesses

The cross-joint generalisation claim — the paper's stated main contribution — rests entirely on private validation cohorts from Peking University Third Hospital, the same institution that supplies the bulk of pretraining data. Hip, shoulder, and ankle transfer tasks lack disclosed patient demographics, scanner diversity, and sample sizes in the submitted document. Covariate proximity between pretraining and transfer cohorts cannot be excluded, and this is not addressable without geographically external, prospective validation.

The reader study is disqualifying for the clinical utility conclusions drawn. Three junior readers, 120 radiographs, and 270 MRI cases are insufficient to estimate diagnostic performance with narrow confidence intervals. There is no senior radiologist reference arm, making it impossible to determine whether AI-assisted performance approaches subspecialty expert level. The McNemar's test significance (p < 0.001) reflects large accuracy deltas in small paired samples, not robust clinical benefit. MRMC design is the minimum standard at this journal level.

The model processes MRI as 2D slice sequences, discarding inter-slice volumetric context that is clinically essential for ACL continuity assessment, meniscal morphology, and cartilage grading. The 2D slice-averaging aggregation imposes a known performance ceiling relative to 3D architectures; the authors acknowledge this but provide no quantification. Longitudinal prognosis results (63.4% accuracy at 4-year KL progression, 58.5% at 8-year) lack calibration analysis, net reclassification improvement statistics, and subgroup stratification by age, sex, BMI, and baseline KL grade — primary confounders of KOA trajectory — rendering these results insufficient for a prognostic claim.

---

## 4. Editorial Decision

**Reject.** The two central claims — cross-joint generalisation and clinical utility augmentation — are supported by single-institution validation data and an underpowered three-reader study respectively, neither of which can be remedied through revision without reconceiving the study. Transfer to *npj Digital Medicine* or *Medical Image Analysis* is recommended, where the benchmarking contribution and label-efficiency analysis are competitive; *Radiology: Artificial Intelligence* is an alternative if the imaging validation framing is primary.

---

## 5. Suggested Reviewer Expertise

The manuscript requires reviewers with expertise in: (1) self-supervised and contrastive representation learning for medical vision transformers, specifically DINO-family continued pretraining strategies and transferability estimation; (2) musculoskeletal radiology with subspecialty focus on knee MRI interpretation, OA imaging biomarkers, and OAI dataset provenance and KL grading reliability; (3) foundation model evaluation methodology including cross-domain generalisation testing and detection of covariate proximity confounding; (4) clinical trial design and statistical methodology for AI-assisted reader studies, specifically MRMC analysis, McNemar's test applicability, and confidence interval construction; (5) orthopedic surgery or sports medicine with direct experience in MRI-based ACL, meniscal, and ligamentous injury assessment in AI-assisted diagnostic contexts.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The medical vision foundation model landscape has advanced substantially since 2023. The generalist paradigm surveyed by Moor et al. (*Nature* 2023, 616:259–265) has since been instantiated in increasingly domain-specific forms. Pérez-García et al. published RAD-DINO (*Nature Machine Intelligence* 2025, doi:10.1038/s42256-024-00965-w), a DINOv2-based ViT-B/14 self-supervised encoder pretrained on ~840k chest radiographs and validated across classification, segmentation, and report generation tasks, establishing a clear methodological antecedent for the image-only DINO continued-pretraining approach that OrthoFoundation adopts. Directly competing in the musculoskeletal space, Kim et al. introduced SKELEX (arXiv 2602.03076, 2025), a two-stage MAE-then-SSL model pretrained on 1,296,540 radiographs from Seoul National University Hospital (SNUH-1M) and validated across seven public MSK radiograph benchmarks — the closest structural comparator to OrthoFoundation, which is not cited or benchmarked against. Hoyer et al. (*npj Digital Medicine* March 2026, doi:10.1038/s41746-026-02520-w) fine-tuned SAM, SAM2, and MedSAM on multi-anatomy musculoskeletal MRI from OAI and demonstrated 48-month knee replacement forecasting with explicit calibration and net benefit analysis, directly competing with OrthoFoundation's prognostic claims with a more rigorous decision-curve framework. Zhang et al. (*NEJM AI* 2025, 2:AIoa2400640) trained a multimodal biomedical foundation model on 15 million image-text pairs spanning dozens of modalities, providing the scale context against which OrthoFoundation's single-anatomy pretraining strategy should be evaluated. The multi-anatomy X-ray foundation model preprint (arXiv 2509.12146, 2025) demonstrates that anatomical diversity during pretraining — rather than single-joint scale — is critical for generalizable radiograph representations, which directly challenges OrthoFoundation's core design assumption. OrthoFoundation's arXiv preprint (2601.18250, January 2026) confirms simultaneous priority and indicates the submitted manuscript and the earlier preprint represent partially overlapping work; the submitted version extends the preprint primarily through the reader study and the expanded 17-task evaluation.

---

## 7. Suggested Reviewer Names

**Self-supervised and contrastive learning for medical vision transformers:**
- Mathilde Caron (Meta AI Research / DINOv2 group)
- Julien Mairal (Inria Grenoble — DINO-family SSL methods)
- Shruthi Bannur (Microsoft Research — BioViL-T, medical vision-language pretraining)

**Musculoskeletal radiology and OA imaging:**
- Ali Guermazi (Boston University — OAI, knee MRI biomarkers)
- Frank W. Roemer (University of Erlangen — MRI semi-quantitative scoring of OA)
- Daichi Hayashi (Tufts Medical Center — imaging biomarkers in OA)

**Foundation model evaluation and transferability methodology:**
- Judy Gichoya (Emory University — AI evaluation, bias, and generalisability in radiology)
- Pranav Rajpurkar (Harvard Medical School — medical AI benchmarking and foundation models)

**Clinical trial design and reader study statistics:**
- Luís Filipe Nakayama (Hospital das Clínicas, Brazil / Harvard — MRMC design and AI-assisted reading trials)
- Konstantinos Kamnitsas (University of Oxford — medical image analysis and AI evaluation design)

---

## 8. Further Literature

The following papers share closely related scope with OrthoFoundation — domain-specific vision foundation models pretrained via self-supervised learning on large-scale medical imaging data, evaluated on musculoskeletal or orthopaedic downstream tasks, or directly concerned with cross-anatomy generalisation from unimodal pretraining corpora.

1. **Pérez-García F, Sharma H, Bond-Taylor S, et al. Exploring scalable medical image encoders beyond text supervision. *Nature Machine Intelligence* 2025; doi:10.1038/s42256-024-00965-w.**
RAD-DINO is the closest architectural antecedent: a DINOv2 ViT-B/14 model pretrained on ~840k chest radiographs using image-only self-supervised learning, without language supervision. It outperforms vision-language models on classification, segmentation, and report generation at inference time and demonstrates downstream performance scaling with training data volume and diversity. OrthoFoundation adopts the same core DINO continued-pretraining paradigm for an orthopedic imaging domain; the authors should have benchmarked against RAD-DINO or engaged with its image-only scaling findings.

2. **Kim S, Lee S, Shin K, et al. A generalizable large-scale foundation model for musculoskeletal radiographs. arXiv:2602.03076, 2025.**
SKELEX is the most direct structural comparator to OrthoFoundation in the musculoskeletal radiograph domain. It uses a two-stage pretraining strategy (MAE on ImageNet-1K, then SSL on 1,296,540 unlabeled MSK radiographs from SNUH-1M) and demonstrates generalisation across seven public MSK radiograph benchmarks spanning multiple anatomical regions and disease states. Unlike OrthoFoundation, SKELEX pretrains on a multi-anatomy corpus from the outset, directly testing the assumption that anatomical diversity during pretraining — rather than single-joint scale — drives cross-joint transfer.

3. **Hoyer C, et al. Clinical utility of foundation models in musculoskeletal MRI for biomarker fidelity and predictive outcomes. *npj Digital Medicine* 2026; doi:10.1038/s41746-026-02520-w.**
This paper fine-tunes SAM, SAM2, and MedSAM on multi-anatomy musculoskeletal MRI from the OAI longitudinal cohort to generate quantitative cartilage and bone biomarkers, then applies these to 48-month knee replacement and osteoarthritis progression forecasting with explicit decision-curve and calibration analysis. It directly competes with OrthoFoundation's TKR prediction claim (AUROC 82.2% on 354 pairs) using a more rigorous prognostic evaluation framework and a larger, fully public dataset.

4. **Zhang K, Zhou R, Adhikarla E, et al. A generalist vision-language foundation model for diverse biomedical tasks. *Nature Medicine* 2024; 30:3129–3141.**
This paper trains a multimodal biomedical foundation model on 15 million image-text pairs spanning radiology, pathology, ophthalmology, and dermatology, achieving cross-modality generalisation at a scale that contextualises OrthoFoundation's single-anatomy strategy. It is relevant because OrthoFoundation's cross-joint transfer claim is essentially a claim about generalisation from a restricted pretraining distribution — the same problem this work addresses at broader scope.

5. **Multi Anatomy X-Ray Foundation Model. arXiv:2509.12146, 2025.**
This preprint demonstrates that anatomical diversity during SSL pretraining is critical for building general-purpose radiograph encoders, challenging the premise that large-scale single-anatomy corpora are sufficient for cross-joint transfer. The finding that supervised anatomical labels during pretraining materially improve downstream generalisation to unseen anatomical regions is directly relevant to OrthoFoundation's design choice to pretrain exclusively on knee imaging.

6. **Hoyer C, et al. Foundations of a knee joint digital twin from qMRI biomarkers for osteoarthritis and knee replacement. *npj Digital Medicine* 2025; doi:10.1038/s41746-025-01507-3.**
This work develops a digital twin framework using automated cartilage and bone segmentation from OAI 3D-DESS MRI on 4,796 patients, extracting quantitative biomarkers for OA progression and knee replacement prediction. It is relevant to OrthoFoundation's 2D slice-based MRI processing limitation: this paper demonstrates that volumetric quantitative biomarker extraction from 3D MRI provides distinct predictive signal not available from 2D slice-averaging, highlighting the performance ceiling that OrthoFoundation's architecture imposes.

047893 EEG Cohorts

---

### 1. Overall Assessment

This manuscript proposes FedSWR, a federated sampling-with-replacement strategy for seizure prediction from single-channel EEG across four heterogeneous public cohorts (CHB-MIT, Helsinki, Siena, NCH), spanning adult, paediatric, and neonatal populations. The core claim is that equalising per-round sample contributions — by training each client on a fixed-size randomly drawn local subset — substantially improves macro-averaged and worst-site performance versus FedAvg, FedProx, FedNova, and SCAFFOLD. A privacy-preserving global normalisation protocol via zero-sum masking is offered as a complementary contribution.

The problem is clinically consequential and the federated formulation is appropriate. However, the proposed method is a thin adaptation: fixed-size per-client data subsampling is conceptually equivalent to centralised oversampling recast as a local data-loading policy, and does not constitute a principled algorithmic advance relative to existing FL fairness literature. More critically, the manuscript is publicly available on arXiv (arXiv:2508.08159, posted 11 August 2025) under a near-identical title, raising a simultaneous submission concern requiring immediate clarification. On scientific grounds, the absence of patient-level clinical metrics — sensitivity and false-alarm rate — renders the clinical claims unsubstantiable. These concerns together constitute non-revisable barriers at *Nature Communications*.

---

### 2. Strengths

The multi-cohort federation spanning CHB-MIT (22 patients, 182 seizures, 2.75M windows), Helsinki neonatal NICU (79 patients), Siena adult, and NCH paediatric sleep-study cohorts is meaningfully broader than the single-dataset patient-level FL setups dominating the prior literature, and the fixed train-validation-test splits maintained across all centralised and federated conditions support credible cross-method comparison.

The pairwise KL-divergence analysis of cross-hospital feature distributions (Fig. 2) is a useful diagnostic absent from most federated clinical AI papers. Demonstrating that KL structure aligns with cross-site accuracy degradation provides empirical grounding for the failure of FedAvg that goes beyond the standard non-IID narrative.

The privacy-preserving global normalisation protocol, based on zero-sum masking via Diffie-Hellman key agreement and a pseudo-random generator, is technically sound and addresses a practical preprocessing barrier — channel-wise z-score normalisation without sharing site-level statistics — that prior multi-site EEG FL work has largely ignored.

The convergence and efficiency characterisation (Fig. 6, Table 6) is rigorous: total wall-clock time for FedSWR (~8.14 hours) is substantially lower than FedAvg (~37 hours) despite requiring 15× more communication rounds, and per-site validation loss variance reduction is quantified explicitly.

---

### 3. Weaknesses

FedSWR's methodological novelty is insufficient. The mechanism — constraining each client's per-round training to a fixed-size random subset — is a transparent federated re-implementation of centralised minority-class oversampling, and the authors acknowledge its conceptual relationship to prior sample-level balancing strategies (their ref. [35]). The paper does not engage with personalised FL alternatives (FedL2T, FedMWAD, Ditto) that address minority-site underperformance through model-level rather than data-loading interventions, and does not establish whether FedSWR is complementary or superior to these approaches.

The evaluation is misaligned with clinical requirements. Accuracy, F1, and AUROC on artificially balanced preictal/interictal segments are standard ML metrics, not clinical ones. The primary outputs for a deployable seizure prediction system are per-patient sensitivity at a specified false-alarm rate (FAR, in events per hour) and detection latency before seizure onset. The manuscript reports none of these. The Helsinki dataset alone contains 79 patients with 460 seizures; whether FedSWR's AUROC improvement translates to seizure-level benefit at clinically acceptable FAR is entirely unaddressed.

The NCH cohort consists of 14 patients selected from a sleep-study databank in which seizures were incidentally captured, not prospectively recorded. No justification is provided for the patient selection threshold, and no comparison is made to the remainder of the NCH database. Given NCH's role as the primary worst-site anchor in the fairness argument, uncharacterised selection bias in this subset materially weakens the paper's central claim.

---

### 4. Editorial Decision

**Reject.** The arXiv preprint (arXiv:2508.08159) is a near-identical version of this submission, which requires disclosure clarification under *Nature Communications* policy. On scientific grounds, FedSWR's contribution — per-round fixed-size client subsampling — does not represent a sufficient algorithmic advance for this journal, and the absence of clinically grounded evaluation renders the stated population medicine claims unsubstantiable. Transfer to *npj Digital Medicine* or *Computers in Biology and Medicine* is recommended, where technically solid federated EEG benchmarking work with clear clinical motivation but moderate algorithmic novelty is regularly published.

---

### 5. Suggested Reviewer Expertise

Reviewers should include specialists in: (1) federated optimisation under non-IID and client-imbalanced conditions, specifically sampling-based and variance-reduction methods in synchronous cross-silo settings; (2) deep learning for single-channel EEG time-series, with direct experience in preictal/interictal segment labelling pipelines and architecture design for biosignal classification; (3) privacy-preserving distributed computation, specifically secure aggregation threat models in clinical cross-institutional settings; (4) quantitative clinical epileptology, with expertise in automated seizure prediction evaluation methodology — event-level sensitivity, FAR, and warning latency — across paediatric and neonatal populations; (5) federated learning fairness and client-equity metrics in multi-institutional medical AI deployments.

---

### 6. State-of-the-Art Literature Review

Federated learning for EEG-based seizure prediction has evolved substantially since 2022, with the frontier moving from patient-level federation within single datasets toward the cross-repository, cross-site problem this manuscript addresses. Jemal et al. (*Front. Neuroinform.*, 2024) demonstrated that domain adaptation methods (DANN, CDAN, CDAN+E) achieve only modest cross-subject AUROC gains on CHB-MIT and Siena, confirming that distributional shift between hospitals exceeds what preprocessing can resolve. Shafiezadeh et al. (*J. Neural Eng.*, 2024) systematically reviewed 50+ cross-patient seizure prediction approaches, identifying multi-site distribution shift as the primary unsolved bottleneck and calling for demographic-stratified benchmarks — a framework this paper partially instantiates but does not complete. On the federated side, Baghersalimi et al. (*IEEE Trans. Mobile Comput.*, 2023) extended personalised FL to decentralised wearable epilepsy monitoring using multi-to-single knowledge distillation, demonstrating that per-client model adaptation substantially outperforms global aggregation under patient-level heterogeneity. FedMWAD (Ding et al., *Inf. Process. Manag.*, 2025) combined module-wise weighted aggregation with Ditto-style local fine-tuning for patient-independent seizure prediction across heterogeneous EEG sources, representing a direct model-level competitor to FedSWR that the authors do not cite. FedL2T (arXiv:2510.08984, 2024) proposed two-teacher knowledge distillation — a global model and a dynamically assigned peer model — for personalised federated seizure prediction, outperforming FedAvg, FedProx, and SCAFFOLD under heterogeneous inter-patient distributions; again unaddressed by the authors. A federated few-shot learning framework (arXiv:2512.13717, 2024) demonstrated patient-level adaptation within a four-hospital federated loop on TUEV II with non-uniform seizure-type distributions, showing that event-level sensitivity metrics are achievable within a privacy-preserving setup — directly relevant to the evaluation gap in this manuscript.

The present paper occupies an increasingly populated niche. Its distinguishing feature is cross-demographic (neonatal, paediatric, adult) multi-repository evaluation, which is genuine value. However, the absence of engagement with the personalised FL line of work and the non-clinical evaluation framework limit its contribution to a well-executed ablation study rather than a field advance.

---

### 7. Suggested Reviewer Names

**Federated optimisation / non-IID FL:**
Tian Li (Carnegie Mellon), Virginia Smith (Carnegie Mellon), Sashank Reddi (Google DeepMind)

**EEG deep learning and seizure detection:**
Jonathan Attia (Hunter Medical Research Institute), Nhan Tran (Mayo Clinic), Mark Cook (University of Melbourne)

**Privacy-preserving distributed computation:**
Mete Akgün (University of Tübingen — *recuse due to co-authorship*), Vitaly Shmatikov (Cornell Tech), Florian Tramèr (ETH Zürich)

**Clinical epileptology / neonatal EEG:**
Sampsa Vanhatalo (University of Helsinki), Hannah C. Glass (UCSF), Renée A. Shellhaas (University of Michigan)

---

### 8. Further Literature — Thematically Similar Papers (Past 3 Years)

**1. Jemal I, Abou-Abbas L, Henni K, Mitiche A, Mezghani N. "Domain adaptation for EEG-based, cross-subject epileptic seizure prediction." *Frontiers in Neuroinformatics* 18:1303380, 2024. https://doi.org/10.3389/fninf.2024.1303380**
Uses DANN, CDAN, and CDAN+E domain adaptation across CHB-MIT and Siena in a leave-one-patient-out cross-subject paradigm. Directly comparable in scope: same public datasets, same cross-site generalisation objective. Demonstrates that model-level distribution alignment achieves modest but consistent gains, contextualising the magnitude of FedSWR's improvements and offering an alternative methodological strategy the manuscript does not consider.

**2. Shafiezadeh S et al. "A systematic review of cross-patient approaches for EEG epileptic seizure prediction." *Journal of Neural Engineering* 21(6):061004, 2024. https://doi.org/10.1088/1741-2552/ad9682**
Comprehensive review of 50+ cross-patient seizure prediction methods, with taxonomy of distribution shift sources, evaluation protocols, and demographic coverage. Establishes the benchmark framework against which this manuscript's multi-cohort evaluation should be positioned, and explicitly calls for stratified reporting across age groups and recording contexts — a standard this paper does not fully meet.

**3. Baghersalimi S, Teijeiro T, Atienza D, Aminifar A. "Decentralized federated learning for epileptic seizures detection in low-power wearable systems." *IEEE Transactions on Mobile Computing* 23(5):6392–6407, 2023. https://doi.org/10.1109/TMC.2023.3320862**
Extends personalised FL to fully decentralised (serverless) architecture for seizure detection on wearable edge devices, combining multi-to-single knowledge distillation with local adaptation. Represents a direct architectural competitor operating on overlapping patient populations with substantially richer personalisation than FedSWR. The per-patient sensitivity metrics reported here (sensitivity 90.24%, specificity 91.58%) are the clinical evaluation standard this manuscript fails to adopt.

**4. Ding Y, Zhao W, Huang K. "FedMWAD: Module-wise weighted aggregation federated learning combined with Ditto for patient-independent seizure prediction." *Information Processing & Management* 62(6):104253, 2025. https://doi.org/10.1016/j.ipm.2025.104253**
Combines module-wise weighted aggregation with Ditto-style local fine-tuning on a TS-SEFFNet backbone for patient-independent seizure prediction across heterogeneous EEG sources. Scope is essentially identical to this manuscript — cross-patient heterogeneity, federated training, fairness across clients — but addresses it at the model-aggregation level rather than the data-sampling level. A critical omission from the manuscript's baseline comparisons.

**5. [Anonymous authors]. "FedL2T: Personalized Federated Learning with Two-Teacher Distillation for Seizure Prediction." arXiv:2510.08984, 2024.**
Proposes a two-teacher knowledge distillation framework (global model + dynamically assigned peer model) for personalised federated seizure prediction under inter-patient variability. Benchmarked against FedAvg, FedProx, and SCAFFOLD — the exact baseline set used here — and reports consistent improvements under low-label heterogeneous conditions. The most directly competing unpublished work, unacknowledged by the authors.

**6. [Anonymous authors]. "Federated Few-Shot Learning for Epileptic Seizure Detection Under Privacy Constraints." arXiv:2512.13717, 2024.**
Applies federated few-shot learning across a four-hospital simulated federation on TUEV II, with non-uniform seizure-type distributions across clients, and includes a federated personalisation phase using patient-specific few-shot adaptation. Demonstrates that event-level performance metrics are reportable within a privacy-preserving federated framework — directly relevant to the evaluation gap identified in this manuscript. Also provides morphology-stratified analysis of when federated aggregation succeeds or fails, setting a methodological standard the present work does not match.

048669 clinical evidence — from a real-world Neurology study"

---

### 1. Overall Assessment

This manuscript introduces NeuroBeliefBench, a matched-case benchmark derived from 46,075 real-world Chinese outpatient neurology records, to evaluate how patient- and clinician-derived belief cues influence diagnostic performance across five frontier LLMs. The central claim is that narrative framing — subjective interpretive statements appended to otherwise identical factual clinical evidence — systematically biases accuracy and confidence in source-dependent, non-additive ways. The most clinically salient result is the dissociation between perceived output quality and diagnostic correctness under senior-physician framing: ChatGPT Top-1 accuracy fell from 85.0% to 20.0% while expert quality ratings simultaneously increased.

The matched-case design is the paper's genuine methodological contribution, and the confidence–accuracy dissociation finding is publishable. However, two concerns are controlling. First, all source data derive from a single centre in Chengdu, China; whether the framing effects — especially the magnitude of senior-doctor accuracy suppression — generalise across languages, specialties, and health systems is entirely untested and unaddressed beyond a perfunctory limitations note. Second, the expert clinical evaluation that anchors the quality-correctness dissociation claim carries an ICC(3,1) of 0.33 — poor-to-fair reliability by standard thresholds — yet the dissociation is presented in the abstract without this caveat. These limitations are structural and not resolvable through revision without new data.

**Decision: Reject.** Transfer to *npj Digital Medicine* or *JAMIA* is recommended, where single-centre benchmark construction studies in this sub-domain are within scope.

---

### 2. Strengths

The matched-case design cleanly isolates narrative framing from changes in underlying clinical information. By holding factual evidence constant and varying only the injected belief cue, the authors avoid the confound that has weakened prior framing-sensitivity studies. The 5,000-case balanced subset yielding 45,000 matched prompt variants is substantially larger than comparable benchmarks, and McNemar tests for paired comparisons are statistically appropriate.

The confidence–accuracy dissociation under senior-doctor framing is the paper's most clinically significant finding. Accuracy among high-confidence outputs declined 12–38% across models under senior-doctor framing while over 80% of outputs retained high-confidence labels — precisely characterising the failure mode most dangerous in clinical deployment, and grounding it in authentic outpatient records rather than abstract QA settings.

Multi-model evaluation across five frontier LLMs (zero-shot, standardised prompts, temperature fixed at 0.3, inference-time thinking disabled) reduces major confounds present in most multi-model clinical comparisons in the recent literature. The Claude Sonnet 4.6 robustness check on a 100-case stratified subset provides partial evidence that observed effects are not artefacts of the primary belief-generation model.

---

### 3. Weaknesses

The single-centre, single-language, single-specialty design is the study's most limiting structural constraint. All records come from one hospital in Chengdu, and belief cues were generated in Chinese clinical register. Whether the authority-framing effect replicates in English-language, European, or multi-specialty settings is entirely unknown. The authors frame the findings as evidence about LLM diagnostic behaviour in clinical settings broadly — a claim the data do not support.

The inter-rater agreement for the expert quality evaluation is ICC(3,1) = 0.33 — poor-to-fair reliability, implying approximately 11% shared variance between the two neurologists. The quality-correctness dissociation is one of the paper's headline results, yet this ICC is not disclosed in the abstract or the results subsection where the claim is made; it appears only in the methods. This requires prominent qualification wherever the quality rating data are used to support conclusions.

The belief-generation pipeline is partially circular. LLM-assisted synthesis produced the injected cues; the same model class was then evaluated on them. The 100-case Claude Sonnet robustness check is directionally reassuring but underpowered for disease-category-level analysis. An independent linguistic audit confirming that generated belief texts are clinically indistinguishable from authentic clinician and patient statements is absent.

---

### 4. Editorial Decision

**Reject.** The matched-case design and the confidence–accuracy dissociation finding are genuinely meritorious, but the single-centre, single-language scope cannot support claims about LLM diagnostic behaviour in clinical settings generally. The ICC of 0.33 for the expert rating component — which anchors the paper's most clinically prominent claim — is inadequately disclosed and falls below the threshold for reliable inference. These issues are non-revisable without new multi-centre or cross-linguistic data collection. The authors are encouraged to reframe the paper explicitly as a single-centre benchmark construction study, obtain independent cross-linguistic validation, and resubmit to *npj Digital Medicine* or *JAMIA*.

---

### 5. Suggested Reviewer Expertise

Reviewers should include specialists in: (1) prompt sensitivity and robustness evaluation of LLMs in closed-domain reasoning tasks, with familiarity with matched-case and counterfactual experimental designs; (2) clinical NLP applied to free-text medical records, particularly diagnostic narrative structure in non-English-language clinical documentation; (3) cognitive bias and sycophancy characterisation in large language models, including confidence calibration and overconfidence in generative models; (4) outpatient neurology and clinical decision-making in the context of specialist-to-specialist and patient-to-clinician communication, with experience in diagnostic uncertainty; and (5) psychometric methodology and inter-rater reliability assessment for clinical evaluation studies, including ICC interpretation and Likert-scale study design.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

The manuscript sits at the intersection of clinical LLM robustness evaluation and cognitive/authority bias in generative AI. The closest concurrent work is Yan et al. (2025, COLING), which proposed an LLM sensitivity evaluation framework for clinical diagnosis assessing model responses to key factual feature perturbations; however, that work targets sensitivity to clinical feature changes rather than narrative framing, and NeuroBeliefBench extends the question to interpretive cues. Yun et al. (2026, arXiv:2604.05051) directly evaluates LLM sensitivity to patient question framing in RAG-based medical QA, demonstrating systematic response inconsistency from phrasing variation alone even when grounded in the same evidence — a parallel the manuscript should engage with and cite. On cognitive bias more broadly, Schmidgall et al. (npj Digital Medicine, 2024) developed BiasMedQA, modifying 1,273 USMLE questions to replicate clinically relevant cognitive biases across six LLMs, finding model-specific vulnerability profiles consistent with NeuroBeliefBench's inter-model heterogeneity; this is the most direct methodological predecessor. Wang et al. (2025, arXiv:2601.13433) characterised authority bias in LLMs by systematically varying endorsement source expertise, finding monotonic susceptibility with authority level — directly relevant to the junior-versus-senior-doctor effects here, yet unengaged in the manuscript. On interactive evaluation, Schmidgall et al. (npj Digital Medicine, 2026) showed via AgentClinic that diagnostic accuracy can fall to one-tenth of static benchmark performance in multi-turn simulated clinical environments across nine specialties and seven languages — contextualising NeuroBeliefBench's single-turn, single-specialty findings as likely conservative estimates. MedDialBench (Luo et al., arXiv:2604.06846, 2026) extends this further by benchmarking five frontier LLMs across 7,225 dialogues under graded adversarial patient behaviour, finding worst-case accuracy drops of 38.8–54.1 percentage points under information pollution, substantially larger than those in NeuroBeliefBench and raising the question of whether the single-turn design materially underestimates real-world framing susceptibility.

---

### 7. Suggested Reviewer Names

**LLM robustness and prompt sensitivity:** Rongwu Xu (Tsinghua University); Chujie Zheng (Tsinghua/UCLA); Hye Sun Yun (Northeastern University); Junyi Jessy Li (UT Austin).

**Clinical NLP and medical LLM evaluation:** Danielle S. Bitterman (Harvard/Dana-Farber); Xien Liu (Tsinghua University); Zhongyu Wei (Fudan University); Junying Chen (Chinese University of Hong Kong).

**Cognitive bias and sycophancy in AI:** Samuel Schmidgall (Johns Hopkins); Mrinank Sharma (Anthropic/prior sycophancy work); Arvind Subramaniam (Stanford AI Lab).

**Outpatient neurology and clinical decision-making:** Lawrence Moura (Mayo Clinic Neurology); David Jones (Mayo Clinic); Lichy Han (Stanford Neurology).

**Psychometrics and inter-rater reliability:** Terry Koo (Hong Kong Polytechnic University, ICC methodology); Rory Wolfson (clinical reliability methodology).

---

### 8. Further Literature

**1. Schmidgall S, Harris C, Essien I, et al. Evaluation and mitigation of cognitive biases in medical language models. *npj Digital Medicine* 7, 295 (2024). https://doi.org/10.1038/s41746-024-01283-6**
The most direct methodological predecessor. Constructed BiasMedQA by modifying 1,273 USMLE questions to embed clinically relevant cognitive biases (anchoring, availability, framing) and evaluated six LLMs. Found GPT-4 resilient while open-source models showed large performance drops; three mitigation strategies improved but did not restore accuracy. NeuroBeliefBench extends this logic from exam-style questions to free-text real-world clinical narratives and adds source attribution (patient vs. clinician) as a structuring variable absent from BiasMedQA.

**2. Yun HS, Kapoor G, Mackert M, et al. This Treatment Works, Right? Evaluating LLM Sensitivity to Patient Question Framing in Medical QA. arXiv:2604.05051 (2026). https://arxiv.org/abs/2604.05051**
Evaluates LLM response consistency under positive versus negative patient question framing in a RAG-based medical QA setting, with the same underlying evidence held constant across paired queries. Demonstrates systematic directional inconsistency from phrasing variation alone. Shares the core matched-evidence design principle with NeuroBeliefBench but focuses on patient-side query language rather than clinician- and patient-side narrative injection in diagnostic scenarios.

**3. Schmidgall S, Ziaei R, Harris C, et al. AgentClinic: a multimodal benchmark for tool-using clinical AI agents. *npj Digital Medicine* (2026). https://doi.org/10.1038/s41746-026-02674-7**
Benchmarked LLMs as clinical agents across nine medical specialties and seven languages in simulated multi-turn patient interaction environments. Diagnostic accuracy dropped to below one-tenth of static benchmark performance under interactive conditions. Contextualises NeuroBeliefBench's single-turn, single-specialty, single-language design as likely producing conservative estimates of framing susceptibility; the performance gap between static and interactive evaluation directly motivates extending NeuroBeliefBench to multi-turn settings.

**4. Luo X, Jiang X, Wu J. MedDialBench: Benchmarking LLM Diagnostic Robustness under Parametric Adversarial Patient Behaviors. arXiv:2604.06846 (2026). https://arxiv.org/abs/2604.06846**
Characterises LLM diagnostic degradation under five graded adversarial patient behaviour dimensions (information withholding, fabrication, denial, etc.) across 85 cases and five frontier LLMs. Information pollution (symptom fabrication) produced 1.7–3.4× larger accuracy drops than information deficit, with worst-case drops of 38.8–54.1 percentage points — substantially exceeding NeuroBeliefBench's senior-doctor accuracy reduction of up to 26.6 points. The comparison raises whether single-turn belief injection underestimates susceptibility in realistic clinical dialogue, and the fabrication-versus-withholding asymmetry parallels NeuroBeliefBench's patient-versus-clinician asymmetry in direction and mechanism.

**5. Yan C, Fu X, Xiong Y, et al. LLM Sensitivity Evaluation Framework for Clinical Diagnosis. In: *Proceedings of COLING 2025*, pp. 3083–3094. https://aclanthology.org/2025.coling-main.207**
Proposed a framework for evaluating LLM sensitivity to perturbations of key clinical features (symptom presence/absence, test result polarity) in diagnostic QA. Unlike NeuroBeliefBench, perturbations target factual clinical content rather than interpretive framing, and data are drawn from structured inputs rather than free-text outpatient records. The two papers are complementary: factual sensitivity and belief sensitivity are distinct failure modes, and combined evaluation would constitute a more complete robustness profile for clinical LLMs.

**6. Wang B, Chang J, Qian Y, et al. Trust Me, I'm an Expert: Decoding and Steering Authority Bias in Large Language Models. arXiv:2601.13433 (2025). https://arxiv.org/abs/2601.13433**
Systematically varied the expertise level of endorsement sources attached to LLM-evaluated claims, finding monotonically increasing compliance with authority level. Identified authority bias as distinct from sycophancy proper, driven specifically by perceived source credibility rather than user preference alignment. Directly relevant to NeuroBeliefBench's senior-versus-junior-doctor asymmetry: the steeper accuracy drop under senior framing (up to −26.6 pp) versus junior framing (up to −9.2 pp) is consistent with the authority-gradient mechanism characterised here, yet the paper is not cited and the mechanistic link is not discussed.

048160 gynecologic care"

---

### 1. Overall Assessment

This manuscript presents a dual-agent framework for full-cycle gynecologic clinical decision support, evaluated on 304 real-world longitudinal inpatient records from three Chinese centers. A doctor agent progresses sequentially through outpatient, inpatient, postoperative, and rehabilitation stages; an environment agent enforces process gating by replaying true temporal information. Five frontier LLMs generate 1,520 decision trajectories evaluated via blinded clinician scoring and LLM-as-Judge metrics across eleven dimensions.

The conceptual shift from single-node LLM evaluation to closed-loop multi-stage clinical process evaluation is timely. However, the manuscript's novelty argument is fragile given the simultaneous emergence of ClinEnv, PhysicianBench, AgentEHR, and TRACE — none of which are engaged. More critically, the LLM-as-Judge adjudicator is Gemini 2.5 Pro, which is also one of the five evaluated doctor-agent LLMs. This circularity is the dominant editorial concern.

---

### 2. Strengths

The cohort construction is a genuine asset. Three geographically distinct Chinese centers, full diagnostic transition data across PALM-COEIN categories from D1 to D3, and stage-specific examination and management records create longitudinal fidelity that MIMIC-IV snapshots cannot replicate. The evaluation framework is the most developed contribution: three independent axes with quantitatively distinct sub-metrics, and a clinician–LLM-as-Judge concordance of 71–85% providing reasonable cross-validation. The ablation removing active examination feedback — reducing D1 and D2 diagnostic proximity by 0.315 and 0.270 but D3 by only 0.006 — is mechanistically interpretable and not predictable from prior work. The deliberate D1 dangerous-shortcut audit is methodologically commendable and rarely attempted in clinical AI papers.

---

### 3. Weaknesses

Gemini 2.5 Pro simultaneously serves as a doctor agent and as the sole LLM-as-Judge for all 1,520 trajectories. This creates unquantifiable evaluation bias and is a structural flaw requiring full remediation before peer review. The dataset is proprietary and not publicly released, making the study non-reproducible in practice — a critical deficiency for a methodology paper. The cohort is restricted to Chinese tertiary inpatient gynecology with no external validation, yet the authors claim the work "delineates capability boundaries of LLMs in longitudinal sequential clinical tasks," an overreach. No non-agentic control arm exists; it is therefore impossible to attribute observed performance to the workflow architecture rather than frontier LLM capability alone.

---

### 4. Editorial Decision

**Reject.** The circular LLM-as-Judge design is a fundamental evaluation flaw that cannot be corrected without regenerating all scored trajectories. Combined with the non-reproducible proprietary pipeline, these concerns are structural. Transfer to *npj Digital Medicine* or *Lancet Digital Health* is appropriate once evaluation circularity is resolved and reproducible components are released.

---

### 5. Suggested Reviewer Expertise

Reviewers should collectively cover: multi-agent LLM system design for sequential clinical decision-making with familiarity with process-gating and context-management architectures; LLM evaluation methodology including LLM-as-Judge validity, calibration analysis, and ablation design for generative clinical AI; longitudinal EHR modelling and temporal reasoning in clinical AI, particularly cross-stage consistency and memory management under long-horizon inference; gynecologic oncology or general gynecology with clinical experience in the outpatient-to-postoperative care pathway for abnormal vaginal bleeding; and clinical AI safety and reproducibility standards including familiarity with TRIPOD-AI and emerging agentic AI deployment frameworks.

---

### 6. State-of-the-Art Literature Review

The agentic clinical AI landscape has developed rapidly since 2024. AgentClinic (Schmidgall et al., 2024) established a multimodal agent benchmark for sequential clinical decision-making across nine specialties using simulated patient interactions, demonstrating that LLMs capable of high static accuracy can drop to below a tenth of that accuracy in sequential decision formats — a finding that directly motivates this manuscript's design rationale. MedAgentBench (Jiang et al., 2025, *NEJM AI*) advanced evaluation fidelity by testing agents in FHIR-compliant virtual EHR environments with clinician-authored tasks. PhysicianBench (Jiang et al., 2026) further extended this with long-horizon verifiable action execution across 21 specialties. AgentEHR (Liao et al., 2026) and ClinEnv (2026) both specifically target multi-stage longitudinal reasoning over raw EHR databases, with ClinEnv's design most directly overlapping with the presented workflow in structure. TRACE (Qu & Färber, 2026) addresses temporal reasoning over streaming EHR data via a dual-memory architecture using MIMIC-IV as a reproducible benchmark, demonstrating measurable improvements over long-context and RAG baselines. The manuscript is silent on all of these contemporaneous works. The authors' claim of priority is sustainable only for the gynecology-specific, full-cycle, gated-progression formulation; the general agentic clinical workflow and evaluation paradigm is now a crowded field. Engagement with ClinEnv, AgentEHR, and TRACE is required. Furthermore, the LLM-as-Judge paradigm invoked here was systematically critiqued for metacognitive limitations in clinical reasoning contexts (Griot et al., *Nat Commun* 2025;16:642), a concern the authors do not address.

---

### 7. Suggested Reviewer Names

For multi-agent LLM system design and evaluation methodology: Samuel Schmidgall (AgentClinic, Stanford/Johns Hopkins), Yuan Jiang (MedAgentBench, Stanford), Michael Moor (ETH Zürich/Stanford, clinical agent benchmarking).

For longitudinal EHR modelling and clinical AI safety: Zhan Qu (TRACE, Karlsruhe Institute of Technology), Matthew McDermott (MIT/Harvard, longitudinal clinical NLP and reproducibility).

For gynecology and clinical decision support: a senior gynecologic oncologist from an institution independent of the three study centers, identified through IGCS or ESGO faculty listings; a practicing gynecologist with EHR-integrated CDS experience in a non-Chinese health system to assess cross-setting generalisability.

---

### 8. Further Literature

The following five papers share direct scope with this manuscript — agentic or sequential LLM workflows evaluated on longitudinal clinical records — and represent the competitive landscape the authors must engage.

**1. Schmidgall S et al. "AgentClinic: a multimodal agent benchmark to evaluate AI in simulated clinical environments." arXiv:2405.07960 (2024).**
The closest structural antecedent. AgentClinic pairs a doctor agent with an LLM-simulated patient agent across nine specialties, requiring sequential examination requests and diagnosis under incomplete information. The finding that LLM accuracy drops to below a tenth of static performance in sequential formats directly motivates — and partially pre-empts — the present manuscript's core design rationale. The present work should differentiate on real longitudinal records versus simulated patient agents, and on four-stage full-cycle scope versus single-encounter diagnosis.

**2. Jiang Y et al. "MedAgentBench: A Virtual EHR Environment to Benchmark Medical LLM Agents." *NEJM AI* (2025). DOI: 10.1056/AIdbp2500144.**
Evaluates 12 LLM agents on 300 clinician-authored tasks in a FHIR-compliant EHR environment. Directly competes on the claim of real EHR grounding and multi-step agent evaluation. Key differentiator from the present work: MedAgentBench uses standardised interoperable infrastructure (FHIR/SMART-on-FHIR), enabling reproducibility the present manuscript lacks. The fact that agents reached only 30.3% task completion in MedAgentBench — far below the 86.8% workflow pass rate reported here — raises questions about task difficulty calibration and comparability.

**3. Liao Z et al. "AgentEHR: Advancing Autonomous Clinical Decision-Making via Retrospective Summarization." arXiv:2601.13918 (2026).**
Challenges agents to perform diagnosis and treatment planning through long-range interactive reasoning over raw EHR databases, covering a multi-turn evidence acquisition paradigm structurally similar to the present workflow's D1–D2 loop. Directly overlaps with the present work's outpatient-inpatient transition mechanism and sequential evidence acquisition design. The absence of any discussion of AgentEHR is a material gap the authors must address.

**4. Qu Z and Färber M. "TRACE: Temporal Reasoning via Agentic Context Evolution for Streaming Electronic Health Records." arXiv:2602.12833 (2026).**
Introduces a dual-memory architecture (static Global Protocol + dynamic Individual Protocol) for longitudinal clinical reasoning on MIMIC-IV streaming events. TRACE's explicit treatment of cross-stage consistency degradation and memory compression maps directly onto the memory composite index and consistency composite index findings in the present manuscript. Moreover, TRACE uses a public benchmark, enabling the kind of independent reproducibility this manuscript cannot currently support.

**5. Griot M et al. "Large language models lack essential metacognition for reliable medical reasoning." *Nature Communications* 2025;16:642.**
Provides systematic evidence that LLMs exhibit unreliable metacognitive calibration in clinical reasoning contexts, directly challenging the validity of LLM-as-Judge paradigms for medical output scoring. The present manuscript's entire evaluation superstructure depends on Gemini 2.5 Pro as adjudicator, yet this paper — published in the same journal — is not cited. Given the identified overconfidence at D2 (calibration gap 0.167) and the absence of inter-judge reliability testing across multiple LLM adjudicators, this omission is not defensible.

**6. ClinEnv: "An Interactive Multi-Stage Long Horizon EHR Environment for Agents." arXiv:2606.02568 (2026).**
The most directly competing contemporaneous work. ClinEnv explicitly frames multi-stage, long-horizon EHR interaction as the core evaluation design, with task decomposition across clinical reasoning stages. The structural overlap with the four-stage D1–D4 workflow presented here is substantial. The manuscript under review must distinguish its contribution — domain specificity, real longitudinal gynecologic records, PALM-COEIN diagnostic taxonomy, and stage-gated progression — against ClinEnv's more general multi-specialty framing with verifiable execution.

048966 # Editorial Report — Manuscript 048966
**Title:** Vision-language models for chest radiography do not always need the image  
**Journal:** Nature Communications — Digital Health  
**Decision:** Send for Review

---

## 1. Overall Assessment

This manuscript asks whether medical vision-language models (VLMs) actually use the image when answering chest radiograph questions. The authors introduce a causal interventional audit applied to nine systems across 2,575 yes-or-no decisions drawn from MS-CXR, MIMIC-CXR, and ReXErr, exposing each case to four image conditions: original, same-label patient swap, radiologist-marked target-region occlusion, and irrelevant-region occlusion. Three behavioural metrics follow: the causal grounding rate (CGR), the unrelated-image answer rate (UAR), and the irrelevant-mask stability (IS). The finding that a text-only model (MedGemma-27B-text) reaches within 5.7 accuracy points of the strongest multimodal system while registering zero grounding, and that a 119-billion-parameter multimodal model is statistically indistinguishable from a 7-billion text-only baseline, is clinically consequential and well-evidenced.

Two concerns dominate. The CGR ground truth is a single MS-CXR radiologist-marked phrase-grounding box, which the authors confirm fully contains the queried evidence in only 48.3% of cases, producing CGR values that are systematically depressed for diffuse bilateral findings. This bias is acknowledged in Discussion but not quantified in Results, where it affects interpretation of the core metric. The human reference comparison (n=80, inter-rater Cohen's κ=0.224) is too small and too single-observer dependent to support the "radiologist-comparable grounding" framing: one of the two readers registers zero CGR and 58.8 accuracy, making this a null result under power rather than an equivalence finding.

---

## 2. Strengths

The causal triad (CGR, UAR, IS) is methodologically well-motivated. Unlike adversarial benchmark degradation or post hoc saliency maps, the three metrics are jointly informative: none is interpretable in isolation, but together they deterministically classify every model into a behavioural category that is stable across IS thresholds from 50 to 90 and reproducible without model internals or gradient access. This is a meaningful contribution to VLM evaluability.

The model panel is unusually broad. Nine systems spanning 1.5B to 119B parameters — including specialist medical models (MedGemma-1.5-4B, LLaVA-Med-7B), general-purpose multimodal models (Gemma-4-26B, Qwen3-VL-32B), the closed-source GPT-5, text-only and vision-only baselines — are all evaluated under an identical fixed-prompt, deterministic-decoding pipeline, making cross-model comparisons internally consistent.

Robustness probes substantially strengthen the claims. UAR rankings replicate on CheXpert (Spearman ρ=0.931, p<0.001), category assignments are stable at 224 and 512 pixels, and prompt reformulations collapse parse rates without altering behavioural category, confirming that findings reflect model properties rather than probe artefacts.

Confidence calibration analysis is directly deployment-relevant. Image-using models report markedly higher confidence on grounded-correct than ungrounded-correct answers (Gemma-4-26B: 97.5 vs 45.6), while ECE remains elevated across all systems (31.4–47.0), and confidence-gating fails for precisely the models that most need a safeguard.

---

## 3. Weaknesses

The CGR ground-truth reference is critically noisy for diffuse findings. A single MS-CXR phrase-grounding box fully contains the queried evidence in only 48.3% of cases by the authors' own validation; for bilateral or spatially distributed findings (atelectasis, lung opacity), this produces near-zero CGR that is structurally indistinguishable from genuine image-ignoring. Four of five image-using models register zero on atelectasis and lung opacity (Fig. 5), yet this is not adequately separated from possible artefact in Results. The supplementary sensitivity analysis (CGR rising from 33.2 to 43.9 on fully-valid boxes) belongs in the main text, not a table footnote.

The human reference comparison is underpowered and single-observer dependent. The claim that MedGemma-27B-text is statistically indistinguishable from a radiologist (+2.5±6.6, p=0.746, n=80) cannot distinguish a clinically meaningful accuracy difference from null on this sub-sample size. Inter-reader disagreement (κ=0.224, one reader at zero CGR) means the comparison effectively reduces to one reference reader. The "radiologist-comparable" framing should be replaced with explicit acknowledgment of this limitation throughout.

The probe is structurally restricted to binary finding-presence questions under a single zero-shot protocol, yet the deployment-gating claim ("grounding audits, not accuracy, should gate clinical deployment") implicitly applies to free-text report generation and error detection — the actual primary clinical uses. Extending the interventional framework to open-ended generation is framed as future work but is in fact a prerequisite for the normative claim to be actionable.

The UAR metric contains an insufficiently addressed confound: for visually stereotyped findings (cardiomegaly, large pleural effusion), a model genuinely reading the image should preserve its answer under same-label swap, yielding high UAR even with genuine image dependence. The proportion of finding-specific UAR values explainable by label-appearance homogeneity rather than text-prior exploitation is not quantified. An opposite-label swap control would resolve this ambiguity.

---

## 4. Editorial Decision

**Send for Review.** The causal triad is a genuine methodological contribution; the model panel breadth is exceptional; and the core finding — that benchmark accuracy and image grounding are orthogonal on chest radiograph VQA — is clinically important without a single fatal structural flaw. Reviewers should be asked to adjudicate three specific questions: (1) whether the CGR lower-bound bias from single-box ground truth is quantitatively tolerable given the finding-level conclusions; (2) whether the human comparison is appropriately framed given sub-sample size and inter-reader disagreement; and (3) whether the deployment-gating normative claim is premature given restriction to binary yes/no QA.

---

## 5. Suggested Reviewer Expertise

Reviewers should span the following domains. One reviewer with deep expertise in causal inference and interventional methods applied to neural networks, including familiarity with do-calculus and counterfactual experimental design in vision-language systems. One reviewer specialising in chest radiograph AI benchmark construction and calibration methodology, with direct experience using MS-CXR and MIMIC-CXR phrase-grounding corpora. One reviewer expert in multimodal LLM alignment and visual grounding failure mechanisms, ideally with knowledge of training objectives that target visual dependence. One reviewer who is a practising radiologist with experience in AI-assisted interpretation pipelines and familiarity with clinical deployment standards for FDA SaMD or CE-marked radiology AI.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The concern that medical VLMs exploit linguistic priors rather than visual evidence has attracted sustained attention since 2023. Yan et al. (ACL Findings, 2025) demonstrated that state-of-the-art multimodal models perform worse than random on negated and hallucinated-attribute diagnostic probes via the ProbMed dataset, drawing from ChestX-ray14 and MedICaT across three imaging modalities. Sepehri et al. (ICLR 2025) constructed MediConfusion — a benchmark of model-confusable but visually distinct image pairs — showing that most proprietary and medical-specialist VLMs fall to chance when language priors are structurally neutralised. Both works establish the field context but operate through adversarial benchmark construction rather than direct image intervention, a distinction the present work correctly identifies and addresses. Felizzi et al. (2025) demonstrated that GPT-4o and Claude 3.5 produce medically valid conclusions in the absence of visual input; their stress-testing protocol using shuffled and blank images is closely related to the UAR intervention here, though without the localized target-region masking that anchors CGR. The manuscript's use of MS-CXR radiologist-marked bounding boxes to define causally sufficient regions is a structural advance over blank-image controls, separating global from local image dependence.

Within the radiology AI grounding literature, MAIRA-2 (Bannur et al., arXiv 2406.04449, 2024) introduced grounded report generation on MIMIC-CXR using autoregressive bounding-box decoding, evaluated on MS-CXR phrase grounding, achieving competitive mIoU on the held-out phrase set. That work and M4CXR (2024) evaluate grounding by agreement with reference boxes rather than by behavioural change under intervention — the methodological gap the present study fills. The closest prior work is the interventional VQA literature (Niu et al., 2021), but no published study has applied a causal intervention framework to medical VLMs at this model diversity and scale. The manuscript is well-positioned at the intersection of causal evaluation methodology and medical AI trustworthiness, and reviewers in the Nature portfolio have consistently flagged this gap as unaddressed.

---

## 7. Suggested Reviewer Names

**Causal inference and interventional ML methods:** Bernhard Schölkopf (Max Planck Institute for Intelligent Systems); Jonas Peters (University of Copenhagen); Judy Hoffman (Georgia Tech).

**Chest radiograph AI evaluation and benchmark construction:** Curtis Langlotz (Stanford University); Sheng Wang (University of Washington); Olatunji Ruwase (Microsoft Research, medical imaging).

**Multimodal LLM alignment and visual grounding:** Yann LeCun (Meta AI); Douwe Kiela (Contextual AI); Anna Rohrbach (UC Berkeley).

**Clinical radiology and AI deployment:** Keith Dreyer (Mass General Brigham); Paras Lakhani (Thomas Jefferson University); Sham Sokhi (NHS AI Lab, UK).

---

## 8. Further Literature

The following six papers from the past three years share significant scope with this manuscript, each approaching the question of whether medical VLMs use visual input or exploit statistical shortcuts.

**Yan Q et al. "Worse than Random? An Embarrassingly Simple Probing Evaluation of Large Multimodal Models in Medical VQA." ACL Findings, 2025.** Introduces ProbMed, pairing original diagnostic questions with negated and hallucinated-attribute variants across ChestX-ray14, MedICaT, X-ray, MRI, and CT modalities. Shows GPT-4o, GPT-4V, and Gemini Pro fall below random on fine-grained diagnostic questions. Directly relevant as a parallel shortcut-detection framework that uses adversarial question construction rather than image intervention.

**Sepehri MS et al. "MediConfusion: Can you trust your AI radiologist? Probing the reliability of multimodal medical foundation models." ICLR, 2025.** Constructs a paired-image VQA benchmark where language priors are structurally constrained to chance, showing most frontier and specialist medical VLMs achieve near-random accuracy on confusable image pairs. Shares the core thesis of the manuscript under review but cannot isolate localized from global visual dependence, which the CGR/UAR/IS triad addresses.

**Bannur S et al. "MAIRA-2: Grounded Radiology Report Generation." arXiv:2406.04449, 2024.** Presents a radiology-specific multimodal model combining RAD-DINO with Vicuna-7B, generating bounding-box-grounded chest X-ray reports evaluated on MS-CXR phrase grounding (mIoU) and MIMIC-CXR factuality (RadFact). Complementary in focus — MAIRA-2 measures output grounding on a model trained for it; the manuscript under review audits whether grounding occurs at all in systems not trained for it.

**Felizzi A et al. "Beyond Accuracy: Evaluating Visual Grounding and Faithfulness in Multimodal Medical Reasoning." arXiv:2603.03437, 2025.** Demonstrates that GPT-4o and Claude 3.5 produce medically valid conclusions without visual input, using shuffled and blank-image stress tests. The methodology is closely related to the UAR condition in the manuscript under review, though absent the MS-CXR localized masking that distinguishes target-region from irrelevant-region sensitivity.

**Auditing Frontier Vision-Language Models for Trustworthy Medical VQA: Grounding Failures, Format Collapse, and Domain Adaptation. arXiv:2604.27720, 2025.** Audits multiple frontier VLMs across grounding failure modes using domain adaptation and format collapse probes, finding systematic grounding deficits and output brittleness orthogonal to accuracy. Overlapping conclusions on the accuracy–grounding decoupling, though evaluated on different datasets and without the causal interventional design.

**Howell L et al. "Understanding the robustness of vision-language models to medical image artefacts." npj Digital Medicine, 2025.** Evaluates VLM performance degradation under weak and strong image artefacts, showing accuracy decline and poor artefact detection across multiple modalities. Relevant as a complementary perturbation-based evaluation that demonstrates image content sensitivity is task- and artefact-specific, reinforcing the manuscript's finding that image use is finding- and view-dependent rather than a global model property.

049028 **Editorial Report — Nature Communications (Digital Health)**
*Revised: Sections 1–4 condensed; Sections 5–7 preserved verbatim; Section 8 appended.*

---

### 1. Overall Assessment

This manuscript applies a Procrustes-based landmark-matching pipeline to 41,078 lateral knee radiographs from two independent cohorts — a European tertiary-care institutional dataset (n=13,525) and the publicly available Emory MRKR dataset (n=27,553) — to test whether the ISR, mISR, and CDI align with their canonical reference ranges. The central finding is that ISR distributions are systematically shifted above the conventional upper limit of 1.2, with 38–43% of reference-cohort measurements exceeding this threshold, while mISR and CDI remain closer to their normative ranges.

The study is methodologically disciplined and clinically motivated. The core unresolved problem is the absence of ground-truth clinical validation: the paper characterises a distributional mismatch but cannot establish whether the conventional threshold or the observed distribution is clinically correct. Clinical implications drawn — particularly regarding overdiagnosis via the Patellar Instability Severity Score — are plausible but unsubstantiated by outcome data.

---

### 2. Strengths

Scale and dual-source design substantially exceed prior normative work, with both cohorts independently reproducing the ISR shift. The pipeline is publicly available, the MRKR dataset is openly accessible, and leave-one-out cross-validation against two radiologists with distinct experience levels constitutes a credible evaluation design. The LLM-based report label-extraction pipeline (AUC=0.95, accuracy=95%) enables principled cohort stratification from unstructured radiology text at scale.

---

### 3. Weaknesses

Neither cohort represents a truly asymptomatic normative population. The institutional reference cohort is defined by radiology-report negativity, which is operationally circular: normality is asserted rather than anatomically verified. The pipeline performs unequally across indices (ISR ICC=0.89 vs. CDI ICC=0.43), and the finding that mISR and CDI align with historical ranges may partly reflect measurement imprecision rather than true distributional fidelity. No clinical outcome linkage is attempted despite the MRKR dataset containing ICD-coded OA status and pain scores — a missed opportunity that limits the impact of the clinical claims. Race-stratified ISR differences (δ up to 0.35) are relegated to supplementary material despite being clinically non-trivial given the MRKR's 40% African American representation.

---

### 4. Editorial Decision

**Send for External Review**, with reservations. The consistent ISR shift across two independent datasets clears the bar for peer adjudication. Reviewers should be asked to evaluate: (1) whether reference-cohort construction is sufficient to support a normative claim or constitutes circular reasoning; (2) whether differential pipeline accuracy across indices accounts for the index-specific distributional patterns; and (3) whether MRKR clinical metadata should have been leveraged to link findings to patient outcomes.

---

### 5. Suggested Reviewer Expertise

Reviewers should be drawn from the following domains: (1) AI-based anatomical landmark detection and registration for musculoskeletal radiographs, including template-matching and keypoint detection architectures; (2) normative reference range methodology, including distributional approaches to clinical threshold derivation and population-stratified normative modelling; (3) large-scale retrospective cohort construction from radiological databases, including quality-control pipelines and label-extraction from unstructured clinical text; (4) patellofemoral biomechanics and clinical management of patellar instability, including familiarity with ISR, CDI, and the Patellar Instability Severity Score in surgical decision-making; (5) musculoskeletal health disparities research, specifically with experience in race- and sex-stratified imaging analyses.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

The automated measurement of patellar height indices has advanced considerably since 2020, when Ye et al. (*European Radiology*, 2020) reported deep learning ICCs of 0.91–0.95 for ISI on 1,018 knee radiographs. More recent work by Kwolek et al. (*World Journal of Orthopaedics*, 2023) extended automated patellar height assessment to high-resolution radiographs, and Liu et al. (*Journal of Orthopaedic Surgery and Research*, 2024) reported a multicenter deep learning system across 2,341 radiographs achieving strong measurement accuracy for ISR and CDI. Fully automated ISR measurement using keypoint AI was specifically described in the *Journal of Imaging Informatics in Medicine* (2024) on 2,647 radiographs with a mean ISR of 1.11±0.21, with 30.3% exceeding the patella alta threshold — a directly comparable finding that the present manuscript cites as reference [16] and extends substantially in scale. Concurrently, normative threshold critique has emerged from CT-based analyses: a 2024 *Scientific Reports* study using a SOMA CT modelling system on 434 knees demonstrated that the Insall-Salvati 1.2 threshold does not correspond to the 98th percentile of the study population, supporting the present manuscript's central argument. Against this landscape, the present study's primary contribution is scale and dual-site replication; it does not introduce a new measurement method. The authors should more explicitly situate themselves against the 2024 *Scientific Reports* CT-based normative critique and directly address whether their radiograph-derived distributional estimates converge with or diverge from CT-derived normative data, since the ISR is known to be sensitive to projection angle — a confounder that CT eliminates.

---

### 7. Suggested Reviewer Names

For AI-based anatomical landmark detection and musculoskeletal radiograph analysis: Zahi A. Fayad (Mount Sinai), Mingqian Huang (Mount Sinai), Shaeke Saarakkala (University of Oulu).

For normative reference range methodology and population-stratified threshold derivation: Tim B. Briggs (University of Bristol), Judith F. Baumhauer (University of Rochester).

For patellofemoral biomechanics and patellar instability surgery: Betina Hinckel (William Beaumont Hospital), David Dejour (Lyon Ortho Clinic), Kristian Thorborg (Copenhagen University Hospital).

For musculoskeletal health disparities and race-stratified imaging research: Judy Wawira Gichoya (Emory University), Cody C. Wyles (Mayo Clinic).

---

### 8. Further Literature (Past 3 Years — Thematically Similar Scope)

**Kwolek K et al. "Automated patellar height assessment on high-resolution radiographs with a novel deep learning-based approach." *World Journal of Orthopaedics* 14(6):387–398, 2023.** Develops a CNN-based pipeline for automated ISR and CDI measurement on clinical radiographs and validates it against manual radiologist measurements. Directly comparable in methodological scope; the present manuscript supersedes this work in scale (41,078 vs. a smaller single-centre series) and adds explicit normative threshold testing, which Kwolek et al. do not attempt.

**Liu Z et al. "Deep learning-based automatic measurement system for patellar height: a multicenter retrospective study." *Journal of Orthopaedic Surgery and Research* 19(1), 2024.** Reports a keypoint detection system across 2,341 radiographs from multiple Chinese centres, achieving ICC >0.90 for ISR. Provides the most methodologically comparable recent benchmark; however, it does not interrogate whether automated measurements challenge conventional reference ranges, which is the key conceptual step the present manuscript takes.

**[Authors not visible in search]. "Fully Automated Measurement of the Insall-Salvati Ratio with Artificial Intelligence." *Journal of Imaging Informatics in Medicine* 37(2), 2024.** Cited in the present manuscript as reference [16]. Applies a keypoint AI model to 2,647 radiographs and reports a mean ISR of 1.11±0.21 with 30.3% exceeding the 1.2 patella alta threshold — the single most directly analogous finding. The present manuscript's contribution is to replicate and extend this observation across two independent, large-scale, demographically diverse cohorts.

**[Authors not visible in search]. "Patella height ratios diagnose the same healthy knees differently." *Scientific Reports*, 2024.** Uses a CT-based SOMA modelling system on 434 asymptomatic knees to show that the ISR 1.2 threshold does not align with the 98th percentile of the study population, while the CDI is better calibrated. Provides independent, modality-orthogonal corroboration of the present manuscript's ISR-specific distributional mismatch finding. The present manuscript does not engage with it directly; authors should address convergence or divergence between radiograph- and CT-derived normative estimates.

**Liu Z, Zhou A, Fauveau V et al. "Deep Learning for Automated Measurement of Patellofemoral Anatomic Landmarks." *Bioengineering* 10(7):815, 2023.** Applies a modified ResNet50 to 483 CT-based knee datasets across six centres, predicting seven patellofemoral landmarks with a mean absolute error of 0.20–0.26 cm. Demonstrates that multi-template, multi-centre landmark aggregation generalises well across healthy and arthroplasty cohorts. Relevant to the methodological design choices made in the present manuscript's Procrustes-based pipeline; represents a competing architectural approach not discussed in the present work.

**Tuya E et al. "Automatic measurement of the patellofemoral joint parameters in the Laurin view: a deep learning-based approach." *European Radiology* 33:566–577, 2023.** Extends automated patellofemoral morphometry beyond the lateral view to the axial Laurin projection, enabling tilt and sulcus angle quantification at scale. Contextually relevant because patellar instability workup typically requires both lateral and axial measurements; the present manuscript's exclusive focus on lateral-view sagittal indices represents a scope boundary that readers in the patellar instability field will notice.
