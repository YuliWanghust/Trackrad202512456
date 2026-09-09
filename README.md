# Trackrad202512456

073912
# Editorial Report — Manuscript 073912

**Title:** SPAD: Structure-Level Prototype Adaptation for Unsupervised Cross-Domain Ultrasound Segmentation
**Corresponding author:** Xinye Ni (Nanjing Medical University / Changzhou No. 2 People's Hospital)

---

## Editorial Integrity Alert (confidential — handling editor only)

Reference [2] (Sun et al., *Computer Methods and Programs in Biomedicine*, 2022, TNSNet) is authored by Jiawei Sun and Xinye Ni, both authors of this submission. The citation is used to establish the thyroid segmentation problem and is not flagged as self-citation. This is not misconduct, but reviewers with Changzhou University, Southeast University or Nanjing Medical University affiliations should be excluded.

The manuscript cites SHAN (Zhang et al., MICCAI 2024, reference [12]) — a directly competing cross-domain thyroid ultrasound segmentation method using shape priors — in Related Work, yet omits it from the comparison. References [6] and [7], both 2024 medical UDA methods, are likewise cited but not benchmarked. Selective comparator omission in favour of DCLPS [18], a polyp-segmentation method repurposed as the "strongest baseline", warrants scrutiny.

MIC [17] returns an average Dice of 37.84%, far below the Source Only floor of 54.14%, and 24.15% on BUSI→BUSI-WHU. A published CVPR 2023 method collapsing this far below no-adaptation indicates misconfiguration rather than method failure. Reporting a broken baseline inflates the apparent competitive field.

Code is promised "upon acceptance". No preprint of this work was located on arXiv or medRxiv; no undisclosed prior posting was identified.

---

## 1. Overall Assessment

SPAD decomposes source masks into structure core, transition boundary and background context, pools a prototype per region, aligns unlabelled target features via soft confidence/uncertainty/gradient weights, and injects prototype responses into a residual logit head, across six bidirectional ultrasound transfers (thyroid, breast, cardiac). Reported averages (mIoU 74.72%, Dice 67.57%, Recall 78.03%) recompute correctly from Tables 2/4/6. But Table 6 shows SPAD without FDA pretraining averages 72.03% mIoU/63.38% Dice — below DCLPS (73.30%/65.75%). The headline gains rest on a pretraining stage baselines never received; the structure-level contribution is not isolated.

## 2. Strengths

Evaluation breadth (six transfers, three organs) and a layered ablation (Tables 3–6, five-seed mean±SD, nested 10–100% data sweeps) exceed typical ultrasound UDA papers. Negative results are disclosed rather than hidden (losses to AdvEnt/MaNi in CAMUS→HMC-QU, non-significant Recall gain over DCLPS). Soft structure assignment is a principled response to hard-pseudo-label error at speckle-blurred margins.

## 3. Weaknesses

The core comparison is confounded by unequal FDA pretraining; the required control (DCLPS/MaNi/MIC under identical pretraining) is absent. No boundary distance metric (HD95, ASSD) is reported despite the thesis being boundary reliability. The 80/20 split is stated at image level with no patient-disjointness guarantee across multi-frame datasets (TN3K, CAMUS, HMC-QU), risking leakage. Reproducibility is blocked by unreported hyperparameters (τ_core, τ_bg, γ_bnd, T, k, ρ, μ, α_dec, all λ's) and code withheld until acceptance. No clinical endpoint, subgroup analysis, or IRB statement is provided.

## 4. Editorial Decision

**Reject**; suggest transfer to *Communications Engineering* or resubmission to IEEE TMI/*Medical Image Analysis*. The manuscript's own ablation contradicts its central claim once the pretraining confound is removed, and boundary/leakage gaps remain unresolved. Counterargument: Table 6's disclosure is unusually honest and the confound may be a fixable missing control rather than a refutation — insufficient given the stakes, since a matched-pretraining rerun could erase the margin. If sent for review: does SPAD hold under matched pretraining; do HD95/ASSD confirm boundary gains; is the split patient-disjoint?

## 5. Suggested Reviewer Expertise

Reviewers should cover prototype-based and contrastive unsupervised domain adaptation for semantic segmentation, with specific familiarity with class-prototype alignment and pseudo-label self-training in the ProDA and DCLPS lineage. A second reviewer should have direct expertise in cross-domain and cross-device ultrasound segmentation, including thyroid nodule and breast lesion datasets and the shape- and boundary-prior methods developed for them. A third should specialise in boundary-aware and shape-constrained segmentation objectives and in surface-distance evaluation methodology, to adjudicate the missing boundary metrics. A fourth should cover echocardiographic image analysis, specifically left-ventricular and myocardial-wall annotation conventions across CAMUS and HMC-QU, and evaluation-validity issues such as patient-level partitioning and shortcut learning in ultrasound. Clinically, one reviewer should be a radiologist or sonographer routinely performing thyroid and breast ultrasound, able to judge whether the reported overlap gains would alter TI-RADS or BI-RADS measurement in practice.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Cross-domain ultrasound segmentation has moved decisively toward structural and shape priors rather than appearance alignment. SHAN (Zhang et al., MICCAI 2024) constructs affine relationships between nodule shape distributions and latent features for cross-domain thyroid segmentation, and is the single most direct competitor to this submission; its omission from the comparison table is the most consequential gap in the manuscript. DCLPS (Lu et al., IEEE TMI 2025), used here as the strongest baseline, was developed for polyp rather than ultrasound segmentation, so its status as the ultrasound state of the art is asserted rather than demonstrated. Style-consistency UDA (Chen et al., IEEE TIP 2024) and dual-domain distribution disruption with semantics preservation (Zheng et al., Medical Image Analysis 2024) are both cited and both unbenchmarked. On the benchmark side, TN3K and the TRFE framework (Gong et al., Computers in Biology and Medicine 2023), BUSI-WHU (Huang et al., IEEE JBHI 2025), CAMUS (Leclerc et al., IEEE TMI 2019) and HMC-QU (Degerli et al., IEEE Access 2021) are the appropriate datasets and are correctly used.

Two currents the manuscript does not engage would materially change its framing. First, foundation-model segmentation — MedSAM, SAM-Med2D and ultrasound-specific SAM adaptations — has shifted the cross-device generalisation question away from adversarial and prototype UDA entirely, and a 2026 submission claiming cross-centre transfer without a promptable-foundation-model reference point is arguing against a superseded baseline set. A DeepLabv2-ResNet101 backbone from 2018 compounds this; no comparison to nnU-Net, TransUNet or a target-supervised oracle is offered, so the absolute quality of 74.72% mIoU cannot be judged. Second, evaluation-validity work in ultrasound, notably shortcut learning in medical image segmentation (Lin et al., MICCAI 2024), has raised exactly the partition and confounding questions this manuscript leaves open. Where SPAD genuinely advances the field is in decomposing the adaptation unit below the class level into reliability-differentiated regions; where it replicates existing work is in its use of morphological boundary bands, which is the established construction behind boundary loss (Kervadec et al., Medical Image Analysis 2021) and BAS-Net, now applied to prototypes rather than to a loss term.

## 7. Suggested Reviewer Names

For prototype-based and contrastive UDA: Ziru Lu (Southeast University), first author of DCLPS, "Domain-Interactive Contrastive Learning and Prototype-Guided Self-Training for Cross-Domain Polyp Segmentation", IEEE TMI 2025 — the exact comparator at issue; and Yizhe Zhang (Associate Professor, Nanjing University of Science and Technology), co-author of the same paper.

For cross-domain ultrasound segmentation: Ruixuan Zhang (Tianjin University), first author of "SHAN: Shape Guided Network for Thyroid Nodule Ultrasound Cross-Domain Segmentation", MICCAI 2024; and Haifan Gong (Chinese University of Hong Kong, Shenzhen), first author of "Thyroid Region Prior Guided Attention for Ultrasound Segmentation of Thyroid Nodules", Computers in Biology and Medicine 2023, which produced the TN3K benchmark used here.

For boundary-aware objectives and surface-distance evaluation: Hoel Kervadec (Assistant Professor, Erasmus MC), first author of "Boundary Loss for Highly Unbalanced Segmentation", Medical Image Analysis 2021; and Manxi Lin (Technical University of Denmark), first author of "Shortcut Learning in Medical Image Segmentation", MICCAI 2024, whose work bears directly on the partition and confounding concerns raised above.

For echocardiographic analysis: Aysen Degerli (Tampere University), first author of "Early Detection of Myocardial Infarction in Low-Quality Echocardiography", IEEE Access 2021, which established the HMC-QU dataset and its left-ventricular wall annotation convention.

Excluded by conflict: any reviewer affiliated with Changzhou University, Southeast University, Nanjing Medical University, Changzhou Institute of Technology, or the Centre de Recherche en Information Biomédicale Sino-Français.

074039
# Editorial Report — Manuscript 074039

**Title:** Development and external validation of *ECG-ArrestNet*: a multimodal artificial intelligence model for prediction of in-hospital cardiac arrest within 24 hours
**Corresponding authors:** Qiming Liu, Chan Liu (Second Xiangya Hospital, Central South University)

---

## Editorial Integrity Alert (confidential — handling editor only)

Four items require attention before any further processing.

First, the submitted PDF terminates at the author declarations and contains no reference list. Citations 1–25 cannot be verified, including the claim at lines 109–111 that evidence for ECG-based IHCA prediction "remains limited." I cannot confirm whether Kwon et al., *Scand J Trauma Resusc Emerg Med* 2020 — which performs the identical task with superior reported discrimination — is cited or omitted. Request the complete reference list.

Second, the comparator designated "Emergency Risk Score (ERS)" is not an identifiable, published IHCA early-warning instrument. Searches return MEWS, NEWS/NEWS2, EDICAS, REMS and DeepCARS, none abbreviated ERS. If ERS is an in-house construct, presenting it as the clinical benchmark is misleading and must be corrected.

Third, all internal arithmetic verifies exactly (cohort splits, event counts, all four incidence figures, all three risk strata and their event shares). The consistency is clean. What does not verify is the external plausibility: see Weakness 1.

Fourth, the live prototype at ecg-arrestnet-platform.pages.dev and the Zenodo deposit both identify the authors. No preprint of this manuscript was located.

---

## 1. Overall Assessment

The authors combine a raw 12-lead ECG with 52 hand-crafted features to predict IHCA within 24 hours, validated temporally (n = 10780) and at two external sites (n = 7840; n = 12507), weights and calibration locked beforehand (AUROC 0.912/0.876/0.849). Execution is careful, but the claim does not survive prior art: Kwon et al. (2020) solved this identical task at higher AUROC (0.913/0.948). The 2.47% 24-hour event rate is also 2.5-fold above the whole-admission rate the authors cite, and no vitals-based comparator is included.

## 2. Strengths

Weights, calibration and threshold were locked on a held-out set before validation, and transported calibration is reported at all three sites without refitting — harder and more informative than AUROC alone. Discrimination is stratified by rhythm and lead-time with a bootstrap heterogeneity test, and the authors correctly decline to over-interpret a non-significant gradient. The ablation series is complete, and the discussion correctly frames the model for enrichment rather than rule-out.

## 3. Weaknesses

The event rate is implausible against the authors' own AHA citation and against EDICAS (0.16%) and DeepCARS (0.09%), most plausibly reflecting unremoved terminal resuscitations. The index ECG is essentially the admission ECG, making this an admission-acuity model despite a surveillance narrative. Every comparator shares the ECG input; "ERS" is unidentifiable and NEWS2/MEWS/DeepCARS are absent, so whether the waveform adds anything beyond heart rate is untested. Sensitivity (0.847) is reported without paired specificity or PPV; the manuscript's own strata imply ~40% of inpatients flagged at ~5% PPV. Code is "available upon request," and the public deposit is simulated data excluded from all analyses.

## 4. Editorial Decision

**Reject.** The task and horizon were established by Kwon et al. at higher discrimination; the incidence conflicts 2.5-fold with the cited epidemiology; and no vitals-based comparator answers whether the ECG adds anything to standard ward monitoring.

*Steelman:* the locked-pipeline design is above median for this literature, and a cohort flow diagram plus retrospective NEWS2 comparison could support major revision. I decline because the incidence anomaly suggests the outcome may not be IHCA as defined elsewhere, and prior art already exceeds this performance. Reconsider for *Communications Medicine* once the cohort definition is resolved and a standard-of-care comparator is added.

## 5. Suggested Reviewer Expertise

Five areas are needed, weighted toward methods. First, deep learning on raw 12-lead ECG waveforms for prognostic rather than diagnostic endpoints, specifically CNN-BiLSTM and lead-attention architectures. Second, clinical prediction model methodology under severe class imbalance — TRIPOD+AI adherence, calibration slope and intercept interpretation, decision curve analysis, and net reclassification against an incumbent score. Third, resuscitation epidemiology and IHCA outcome ascertainment, including Utstein-style event definitions, DNR and treatment-limitation censoring, and adjudication of procedure-related arrests. Fourth, ward-based early warning and rapid response systems, covering NEWS2/MEWS operating characteristics, alert burden and alarm fatigue. Fifth, hospital cardiology and critical care in a Chinese tertiary setting, to assess ECG ordering practice, ICU versus ward case mix and the realism of the proposed surveillance workflow.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The immediate prior art is not recent but is dispositive. Kwon et al., *Artificial intelligence algorithm for predicting cardiac arrest using electrocardiography* (Scand J Trauma Resusc Emerg Med, 2020; 47505 ECGs, 25672 patients) predicts cardiac arrest within 24 hours from 12-lead ECG with internal AUROC 0.913 and external AUROC 0.948, includes a Grad-CAM saliency analysis localising to the QRS complex, and adds a 14-day follow-up of initially non-event patients showing 5.74% versus 0.33% delayed arrest in the high-risk group. Every headline claim in the present manuscript has a counterpart there, at equal or better performance and with the delayed-event analysis the authors omit.

The subsequent three years have moved the field toward multimodal integration and toward benchmarking against deployed systems, and the manuscript engages with neither. Lee et al. (*J Med Internet Res*, 2024) stacked EHR baseline features with LSTM-encoded vital sign trajectories on MIMIC-IV, validating on eICU-CRD and NTUH (AUROC 0.91, 0.81, 0.945) and benchmarking against the CART score. Kim et al. (*npj Digital Medicine*, 2023) built an ICU IHCA model from 5-minute HRV epochs (AUROC 0.881, AUPRC 0.104), demonstrating that continuous single-lead signal is more deployable than intermittent 12-lead acquisition. Liu et al. (*BioData Mining*, 2024) reported Deep EDICAS integrating tabular and time-series ED data (AUROC 0.9046, AUPRC 0.2798). The EIANet study (*J Med Internet Res*, 2025) applied deep learning to triage ECG *images* for ED cardiac arrest with external validation, and its authors explicitly frame ECG-only modelling as a component to be embedded in a future multimodal system — the opposite of the direction taken here. On the clinical-benchmark side, the DeepCARS prospective multicenter validation (*Crit Care*, 2023; 55083 patients) established that a deterioration model must be compared against MEWS and NEWS on alarms per 1000 bed-days, not on AUROC alone; the EDICAS development and external validation studies (Tsai et al., *West J Emerg Med* 2022; *Sci Rep* 2022) provide the reference incidence of 0.16% against which this manuscript's 2.47% should be reconciled.

The manuscript's genuine increments over this landscape are narrow but real: chronological temporal validation plus two geographically distinct external cohorts with a fully locked pipeline, and transported calibration reported without refitting. Those are worth publishing. They are not worth publishing as a novelty claim in a domain the authors describe as having limited evidence.

## 7. Suggested Reviewer Names

For ECG deep learning applied to cardiac arrest prediction: **Joon-myoung Kwon** (Medical AI Co. / Sejong Medical Research Institute), author of the directly competing 2020 ECG cardiac arrest algorithm — the single most qualified assessor of the novelty claim, though his direct competitive stake should be weighed; **Ki-Hyun Jeon** (Mediplex Sejong Hospital), co-author of the same work and of the AI-ECG left ventricular hypertrophy series; **Emilly M. Lima** (Universidade Federal de Minas Gerais), first author of the CODE-study AI-ECG mortality prediction paper in *Nature Communications*, 2021.

For multimodal and time-series IHCA modelling: **Po-Chih Kuo** (Assistant Professor, National Tsing Hua University), computational lead on the MIMIC-IV/eICU multimodal IHCA model (*J Med Internet Res*, 2024); **Chu-Lin Tsai** (Associate Professor, National Taiwan University Hospital), developer and external validator of EDICAS and the best-placed reviewer on the incidence discrepancy.

For prediction-model methodology and calibration: **Ben Van Calster** (Associate Professor, KU Leuven), author of the calibration hierarchy framework and of the TRIPOD+AI-adjacent guidance on calibration slope and intercept reporting.

For resuscitation epidemiology and outcome ascertainment: **Ari Moskowitz** (Assistant Professor, Montefiore Medical Center), IHCA epidemiology and treatment-limitation effects on event counting; **Lars W. Andersen** (Associate Professor, Aarhus University), IHCA incidence and Utstein outcome definitions.

074097
# Editorial Report — Manuscript 074097

**Title:** AI Foundry: an integrated on-premises platform for traceable clinical AI development and requalification
**Section:** Digital Health
**Handling editor assessment**

---

## Editorial Integrity Alert (confidential — handling editor only)

Five matters require attention before any further processing.

First, name collision and unengaged prior art. "AI Foundry" is the trading name of a commercial medical-imaging AI development platform launched by HOPPR in November 2025, offering fine-tuning, version control, traceability and QMS-aligned lifecycle management — the same functional claim set as this manuscript. The authors neither cite nor distinguish it. This is a trademark exposure for the journal and, more seriously, an omission of the closest competing system.

Second, an unreported and statistically significant internal inconsistency. The identical locked baseline model scores 60.0% sensitivity in test set 1 (120/200) and 73.0% in test set 2 (146/200) across two cohorts the authors state were built with identical eligibility, quality, de-identification and reference-standard procedures (Fisher exact p=0.008; specificity 82.8% vs 88.0%, p=0.045). The manuscript never reports this contrast and offers no explanation. Either the cohorts are not exchangeable, or an undisclosed procedural difference exists.

Third, a directionally implausible result. Fine-tuning used only 80 polyp-positive false-negative images, with no negative images and no reuse of the 1,000-image development set. Specificity nonetheless rose 6.8 percentage points and false positives fell from 48 to 21. Training exclusively on positives should shift the detector toward more predictions, not fewer. Raw per-image prediction files for both locked checkpoints on test set 2 should be requested before this result is accepted.

Fourth, possible reference-standard circularity. Experts "reannotated" all 80 false-negative images after seeing model errors. Whether the revised boxes differ from the original adjudicated reference is not stated, nor whether test set 1 metrics were recomputed. If they differ, the reported 60.0% baseline sensitivity is measured against a reference standard the authors themselves subsequently revised.

Fifth, citation misuse. Reference 11 (Fernandes et al., Endoscopy 2025) reports a pooled adenoma detection rate of 26.5% per procedure. The authors invoke it to justify a 33% positive prevalence per image. Procedure-level adenoma yield and frame-level polyp prevalence are different quantities; the prespecified 1:2 ratio is unsupported by the cited source.

All arithmetic was independently verified. Every proportion, F1 score, false-positive image rate and Clopper–Pearson interval in Table 2 reproduces exactly. The problems here are design and disclosure, not computation.

---

## 1. Overall Assessment

The claim is operational, not algorithmic: an on-premises platform executes and documents a closed loop from public-data development through locked qualification, expert review, versioned feedback, updating, and independent requalification, using colonoscopy polyp detection as a demonstration. The authors correctly disclaim clinical effectiveness or causal effect of feedback. The work does not clear the bar. No code, schema, or deployment artifact is offered for a software-infrastructure claim, and the same locked baseline model shows a 13-point sensitivity swing between two "identically constructed" cohorts, unreported and unexplained.

## 2. Strengths

Evaluation discipline exceeds the norm: the baseline was locked before institutional testing, and both model versions were assessed on one identical cohort under fixed inference settings — the correct design for isolating version effects. Sensitivity is localisation-aware (IoU≥0.50 against the adjudicated box), avoiding the inflation of image-level accuracy. In-sample metrics on the 80 feedback images are explicitly quarantined as optimisation diagnostics rather than performance. The positive-image reference standard is histopathology-anchored with independent dual annotation and senior adjudication.

## 3. Weaknesses

No repository, license, or container is provided for a paper whose entire contribution is infrastructure; the claimed advance cannot be verified. All 1,000 development images are polyp-positive, so the detector never learned to reject negatives, making the 17.3% first-qualification false-positive rate an artefact of training design rather than a domain-shift finding. Negative-image ground truth rests on endoscopy reports alone, a reference with a known miss rate, so specificity is unverifiable and not comparable across cohorts. Baseline and updated models were compared on paired data (same 600 images) without a McNemar test, while the abstract still headlines the point-difference as if it were inferential.

## 4. Editorial Decision

**Reject**, with transfer suggested to *npj Digital Medicine* or *Communications Medicine* conditional on code release. The disqualifying issues are structural: no shareable artifact for a software claim, an all-positive development corpus that invalidates the false-positive findings driving the feedback loop, and a circular negative reference standard. If reviewed, reviewers should adjudicate: whether fine-tuning on 80 positive-only images can plausibly raise specificity 6.8 points; why the same locked model differs 13 points in sensitivity across "identical" cohorts; and whether the post-hoc reannotation of the 80 false negatives altered the reference standard underlying the 60.0% baseline figure.

**Counterargument for sending out.** The paper is unusually candid — no causal language, quarantined in-sample metrics, prospectively locked checkpoints — and the same-cohort version comparison is a design most submissions get wrong. This is insufficient because code release would not fix the all-positive corpus or the report-based negative standard, and the cross-cohort instability undercuts the paper's own thesis.

**Blind spot.** On-premises requalification after a model update is exactly what the FDA's Predetermined Change Control Plan guidance and EU AI Act Article 43 govern; neither is cited, and the authors should be asked whether an updating institution becomes a legal manufacturer of a modified device.

## 5. Suggested Reviewer Expertise

Five areas are needed, weighted technical. First, MLOps and reproducible infrastructure for medical imaging, specifically dataset versioning, model lineage, and audit-record design for on-premises hospital deployment. Second, object detection for endoscopic video and still frames, covering YOLO-family architectures, IoU-based localisation metrics, mAP versus lesion-level recall, and the Kvasir and Kvasir-SEG corpora. Third, continual learning and post-deployment model monitoring, including catastrophic forgetting, drift detection, recurring local validation, and update-triggered revalidation. Fourth, regulatory science for adaptive AI as a medical device, particularly predetermined change control plans and EU AI Act substantial-modification rules. Fifth, clinical gastrointestinal endoscopy with direct experience of computer-aided detection trials, colonoscopy quality indicators, adenoma detection rate, and the adenoma miss rate that governs negative-image ground truth.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Two literatures bear on this manuscript, and it engages neither adequately. On the clinical side, CADe for colonoscopy is now assessed at procedure level in randomised trials. Hassan and colleagues' meta-analysis of 21 randomised trials (Annals of Internal Medicine 2023) found adenoma detection rose from 35.9% to 44.0% but advanced adenoma detection did not, with more removal of non-neoplastic lesions. Patel, Mori and Hassan (Clinical Gastroenterology and Hepatology 2024) reported that non-randomised real-world studies show no comparable benefit. The CADeNCE cluster-randomised study at Veterans Health Administration sites (Dominitz et al., Gastroenterology 2026) found availability of CADe raised adenoma detection while leaving cancer outcomes and deskilling unresolved, and Budzyń et al. (Lancet Gastroenterology & Hepatology 2025) reported deskilling after AI exposure. Hsu et al. (JAMA Network Open 2026) found CADe merely non-inferior in a high-performing screening setting. Against this, a 94.0% still-image sensitivity at fixed 33% prevalence carries no clinical interpretation, and the manuscript cites only an editorial (Chung, Kahi and Singh) from this entire body of work.

On the infrastructure side the comparators are closer and are partially cited but not confronted. MAIA (Bendazzoli et al., npj Artificial Intelligence 2025), uRP (Wu et al., Frontiers in Radiology 2023), the cloud-based reproducible radiology pipelines of Bontempi et al. (Nature Communications 2024), and S-RACE (Traverso et al., npj Digital Medicine 2026) already deliver annotation, training, versioning and deployment in governed environments. The claimed differentiator is that error review, feedback registration, updating and requalification are linked in one traceable loop, yet this is asserted in prose and a qualitative supplementary table rather than demonstrated against any of these systems. The commercial HOPPR AI Foundry, which shares both the name and the lifecycle-traceability claim, is absent. Feng et al. (npj Digital Medicine 2022) on continual monitoring and updating of clinical AI, and Youssef et al. (Nature Medicine 2023) on recurring local validation, are the conceptual precedents for the requalification argument; the latter is cited but its central claim is not tested. What this manuscript adds beyond these is a single completed cycle at one site, undocumented in code.

## 7. Suggested Reviewer Names

For MLOps and reproducible medical-imaging infrastructure: Dennis Bontempi (postdoctoral fellow, Harvard/Maastricht), first author of "End-to-end reproducible AI pipelines in radiology using the cloud" (Nature Communications 2024) — the closest published system to the traceability claim here; Simone Bendazzoli (KTH Royal Institute of Technology), first author of "MAIA: a collaborative medical AI platform for integrated healthcare innovation" (npj Artificial Intelligence 2025); Alberto Traverso (Maastro/Erasmus), first author of the S-RACE platform paper (npj Digital Medicine 2026).

For endoscopic object detection and polyp datasets: Debesh Jha (Assistant Professor, Northwestern University), lead author of "Kvasir-SEG: A Segmented Polyp Dataset" and of real-time polyp detection benchmarking work — directly qualified on the exact development corpus used; Vajira Thambawita (SimulaMet), co-author of the Kvasir and HyperKvasir resource papers; Ilias Kafetzis, first author of "Gastrointestinal endoscopic image style transfer using EndoStyle" (npj Digital Medicine 2026), the domain-shift paper the manuscript leans on as reference 8.

For continual learning, drift and post-deployment revalidation: Jean Feng (Assistant Professor, UCSF), first author of "Clinical artificial intelligence quality improvement: towards continual monitoring and updating of AI algorithms in healthcare" (npj Digital Medicine 2022); Andrew Youssef, first author of "External validation of AI models in health should be replaced with recurring local validation" (Nature Medicine 2023), cited here as reference 10; Vimig Socrates or, preferably, Vijaytha Muralidharan (Stanford), first author of the npj Digital Medicine 2024 scoping review of reporting gaps in FDA-authorised AI devices.

For clinical CADe and colonoscopy quality: Harsh K. Patel, first author of "Lack of effectiveness of computer aided detection for colorectal neoplasia" (Clinical Gastroenterology and Hepatology 2024) — the strongest published sceptic of the effect this manuscript implies; Marco Spadaccini (Humanitas), first author of the CADe network meta-analysis in Lancet Gastroenterology & Hepatology; Roupen Djinbachian (Université de Montréal), first author on CADe randomised trial and polyp characterisation work; Krzysztof Budzyń, first author of the endoscopist deskilling analysis (Lancet Gastroenterology & Hepatology 2025).

For regulatory science: Urs J. Muehlematter (University of Zurich), first author of "Approval of artificial intelligence and machine learning-based medical devices in the USA and Europe" (Lancet Digital Health 2021) and subsequent work on device change control.

---

*Sections 1–4 condensed to target length; Sections 5–7 unchanged.*

074113
# Editorial Report — Manuscript 074113

**Title:** Federated knowledge transfer from advanced ophthalmic examinations to fundus-only glaucoma diagnosis
**Handling editor:** Nature Communications, Digital Health

---

## Editorial Integrity Alert (confidential — handling editor only)

Three items require attention before any decision letter is sent.

First, a numerical impossibility. Section 2.3 states the held-out ZHONGSHAN cohort contains 14 early-stage cases. Sections 2.4 and 4.3 state the reader study drew 15 cases from each of four severity groups, including early. Fifteen cases cannot be sampled from fourteen. Either the reader-study cases are not all held-out, or the severity counts are wrong. Every reader-study result and the abstract's 9.68% headline depend on this.

Second, Supplementary Table C2 is internally inconsistent. The reported ORIGA DeLong intervals imply SE 0.0036 (FedBKD) and 0.0079 (FedAvg), so the paired difference SE cannot exceed 0.0087; the reported ΔAUROC interval implies 0.0158. The same contradiction holds, less severely, for BEH. Separately, an SE of 0.0036 on 420 images is roughly an order of magnitude too small for any AUROC estimate at that sample size. These intervals were not produced by the stated procedure.

Third, prior art on the method and its name. "FedBKD" already denotes two published bidirectional-distillation federated frameworks (Qi et al., IEEE JSTSP 2022; and a 2025 data-free variant). OCT-to-fundus knowledge distillation for glaucoma is also established (MultiEYE/OCT-CoDA; Fundus-Enhanced Disease-Aware Distillation, MICCAI 2023). None is cited, and Supplementary A positions FedBKD as uniquely exploiting unaligned modalities. The AIROGS description (112,732 images, 60,071 subjects) matches neither the released training set (101,442 from 54,274) nor the full dataset (113,893 from 60,357), despite citing the Zenodo record for the former.

---

## 1. Overall Assessment

FedBKD federates glaucoma diagnosis across sites with heterogeneous exam availability: a fundus-only aligned model is the federation interface, forward distillation injects OCT/VF knowledge from multimodal hospitals, backward distillation returns it. The problem is real, but execution fails: two headline results rest on contradictory numbers, and the evaluation is too small and artificial to attribute gains to patients rather than random seeds.

## 2. Strengths

The modality-heterogeneity formulation matches real ophthalmic care structure and is portable beyond glaucoma. Local_Full vs. Local_Aligned (22.0–24.6% AUROC gain at ZHONGSHAN, 20.3–23.5% at GONGLI) is a convincing negative result for FedAvg under this heterogeneity. The forward/backward ablation is the right test for a bidirectionality claim, reported across all four cohorts. ZHONGSHAN's reference standard (tiered expert review, HPA severity grading with discordance resolution) exceeds typical retrospective rigor.

## 3. Weaknesses

Confidence intervals and t-tests use n=5 training seeds (df=4), not patients, so every asterisk in Figs. 2, 4, 7 is uninterpretable diagnostically; the one patient-level test (DeLong, Table C2) has internally inconsistent, implausibly narrow intervals. The fundus-only "screening" evaluation uses 2,000 of 112,732 AIROGS images at artificial 50% prevalence against ~3% source prevalence, with no calibration or decision-curve analysis, and silently mixes AIROGS's grader-assigned labels with ZHONGSHAN/GONGLI's OCT/VF-informed diagnoses. The reader study reports per-severity Kappa/F1 undefined without negatives, implying undisclosed pooling of controls, and presents relative changes (e.g., 137.63% kappa gain) on denominators of 15 cases. External validation (BEH/ORIGA) tests only the aligned model, never the personalized local full models the paper calls its strongest output.

## 4. Editorial Decision

**Reject**; transfer to *npj Digital Medicine* or *Communications Medicine*. The reader-study sampling contradiction and inconsistent DeLong intervals undermine the two pillars of the clinical argument and are not revisable by clarification; combined with seed-based uncertainty and unrealistic-prevalence screening, the evidence does not meet this journal's bar.

Counterargument: the modality-heterogeneity formulation and FedAvg negative result are independently valuable, and both numerical problems could be typographical, favoring review with targeted questions on patient-level inference. I don't adopt this: intervals simultaneously too narrow for their sample size and mutually inconsistent aren't a typographical signature, and the balanced-subsample design is structural, not a reporting error.

## 5. Suggested Reviewer Expertise

Reviewers should combine four technical competencies with one clinical. Required technical expertise: federated learning with modality-heterogeneous or partially missing clients, including personalised aggregation schemes such as FedAPM and partial-model personalisation; cross-modal knowledge distillation between retinal imaging modalities, specifically OCT-to-fundus teacher-student transfer and its evaluation; statistical methodology for diagnostic accuracy studies, covering DeLong and bootstrap inference, calibration, decision-curve analysis and multi-reader multi-case designs; and privacy analysis of federated medical imaging, including gradient inversion, membership inference and secure aggregation. Clinical expertise should come from a glaucoma specialist with direct experience of OCT RNFL and visual-field interpretation and of population-level fundus screening programmes in low-resource settings, able to judge whether referable-glaucoma and clinical-diagnosis labels can be federated as though equivalent.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant landscape has three strands, and the manuscript engages seriously with none. On fundus-based glaucoma screening, Hemelings et al. (npj Digital Medicine 2023) established with G-RISK across thirteen sources, including AIROGS, ORIGA and GAMMA, that cross-dataset generalisation is the binding constraint and that prevalence and ground-truth definition drive the performance drop; the de Vente et al. AIROGS challenge report (IEEE TMI 2024) established human-expert reference performance on this exact data and emphasised ungradable-image robustness, which this manuscript excludes by construction. Both are cited but neither is used as a comparator, so it is impossible to place FedBKD's external AUROCs of 0.820 and 0.808 against a field where fundus-only referral models are benchmarked on full cohorts at native prevalence.

On cross-modal distillation, transferring OCT knowledge into a fundus-only student is the paper's actual mechanism and it is not new: Fundus-Enhanced Disease-Aware Distillation (MICCAI 2023) and the MultiEYE benchmark with OCT-CoDA (IEEE TMI 2025) both distil across precisely these two modalities for retinal disease including glaucoma, and MultiEYE provides an unpaired-modality benchmark against which the non-federated core of FedBKD should have been evaluated. On the federated side, the name FedBKD is already occupied by Qi et al. (IEEE JSTSP 2022) for bidirectional client-server distillation and by a 2025 data-free bidirectional variant, and Lu et al. (Nature Communications 2022) established federated glaucoma detection from volumetric OCT across international sites at AUC 0.92 against 0.94 centralised — the closest existing federated glaucoma result and absent from the reference list. The genuine novelty is narrower than claimed: coupling an established cross-modal distillation step to an established personalised aggregation scheme, in a setting where only a subset of clients holds the teacher modality. That is a legitimate increment, but it must be demonstrated against these specific systems rather than against FedAvg alone.

## 7. Suggested Reviewer Names

For federated learning under modality heterogeneity: Coen de Vente (Radboud UMC, AIROGS challenge lead author, IEEE TMI 2024); Chun-Mei Feng (IHPC A*STAR, federated multimodal medical imaging with missing modalities); Cosmin Bercea (TU Munich / Helmholtz, first author of the cited FedDis disentangled federated representation work).

For cross-modal OCT-to-fundus distillation: Lehan Wang (HKUST, first author of MultiEYE and OCT-CoDA, IEEE TMI 2025); Lie Ju (Monash / Airdoc, retinal cross-modal and long-tailed learning); Ruben Hemelings (KU Leuven, first author of the G-RISK generalisability study, npj Digital Medicine 2023).

For diagnostic accuracy methodology and reader-study design: Ben Glocker (Imperial College London, evaluation and bias in medical imaging AI); Xiaoxuan Liu (University of Birmingham, CONSORT-AI and DECIDE-AI, reader-study and reporting standards).

For glaucoma clinical assessment and screening: An Ran Ran (CUHK, first author of the cited Lancet Digital Health 2019 OCT deep-learning study, now leading multimodal glaucoma AI); Fei Li (Zhongshan Ophthalmic Center, GAMMA challenge co-author and glaucoma multimodal grading).

Junior and mid-career researchers have been prioritised; no full professors are proposed. De Vente, Wang, Ju, Hemelings, Ran and Li are all first or corresponding authors on directly comparable published work and are independent of the Beihang, Hefei, Fudan and Peking University author group. Note that Fei Li is affiliated with the Sun Yat-sen Ophthalmic Center, which released the GAMMA dataset used here, and should be excluded if that is judged a conflict.

074168
# Editorial Report — Manuscript 074168

**Title:** Non-invasive Urologic Disease Screening and Diagnosis via Interpretable Multimodal Deep Learning
**Corresponding authors:** M. Li, J. Wang, C. Jin, J. Ye, B. Xu
**Section:** Digital Health

---

## Editorial Integrity Alert (Confidential — Handling Editor Only)

Four items require attention before any decision letter is sent.

First, the manuscript describes "two independent clinical centers" (line 143) and a "multicenter cohort" (line 97). The Methods state that centres A and B are the south and north campuses of the same institution, Shanghai Ninth People's Hospital (lines 552–554). These are not independent centres. No inter-campus held-out validation is reported anywhere, so the multicentre claim is unsupported by both design and analysis.

Second, undisclosed and uncited closely related prior work by the same senior author. Lu, Wang, Bi, Qian, Pan and Ye, *Nanoscale* 2025, 17, 7303–7312, reports urine SERSome profiling with machine learning for low-grade bladder cancer diagnosis at 89.47% accuracy. This is the same technique, the same specimen and a disease inside disease group 5 of the present cohort. It is absent from the 80-item reference list. The authors should be asked to cite it, to state explicitly whether any participants overlap, and to explain what the present work adds beyond it. Bi et al., *Cell Reports Medicine* 2024 (ref. 33) is cited but never positioned as a performance comparator, despite reporting both internal and external validation for prostate cancer.

Third, competing interests. J.Y. is a corresponding author and declares founding a startup commercialising this technology. The manuscript makes unbenchmarked commercial claims about the portable system, including a manufacturing cost of approximately $20,000 (line 450) and batch capacity figures. Independent verification is not possible from the text.

Fourth, data availability. "Additional data can be obtained from the corresponding author upon request" (line 854) does not satisfy the Nature Communications policy for a 1,029-participant clinical cohort. Code is deposited, but no processed SERSome, MS or coefficient matrices are.

---

## 1. Overall Assessment

A two-tier framework diagnoses urologic disease from urine SERSome profiles, LDI-MS and LLM-encoded clinical text, via a GCN-MLP and feature-perturbation interpretation, on 1,029 samples and 205,800 SERS spectra.

Engineering is real; evidence is not. Accuracy 89.6%, sensitivity 90.4%, specificity 85.0% imply ~85% diseased prevalence, so AP 0.97 sits barely above chance; AUROC 0.88 is more honest. Tier two is very likely leaked through clinical text.

## 2. Strengths

Cross-platform SERSome validation is rigorous: portable-confocal Raman agreement reaches r = 0.81±0.07 by band and r = 0.99 canonically, with LDI-MS cross-validation at r = 0.90.

MORE-SERSome decomposition, fitting spectra against a 34-metabolite panel confirmed by SERS/MS dual fingerprints, is a genuine advance; assignments are candidly flagged as putative.

Dataset scale (2M tokens, 205,800 spectra, 2,878 MS spectra) and modality-masking training for missing-data robustness are notable, and code is public.

## 3. Weaknesses

Tier one is confounded by health status, not disease: SHAP ranks cardiopathy and hypertension above every metabolite, with no matched control comparison.

Tier two is structurally leaked. Only disease-relevant examinations were collected, so document presence (an MRI, a PSA) is a near-deterministic label; the 61%→29–39% ablation collapse fits this.

No splits, seeds, confidence intervals, calibration or external validation are reported, and no baseline is tested against 61% eight-class accuracy.

Internal inconsistencies persist: "distinct participants" versus 37 repeat samplers; exclusion reason contradicted between sections; undefined disease labels in Figure 1B.

## 4. Editorial Decision

**Reject.** Both claims fail intrinsically: tier one is confounded by unmatched comorbidity, tier two leaked via examination availability. Neither is fixable by revision. Platform validation is solid; transfer to *Communications Medicine* or *npj Digital Medicine* is reasonable once the multicentre claim is corrected and *Nanoscale* 2025 is cited. Counterargument considered: scale and public code merit review rather than desk rejection; rejected because both confounds derive from the manuscript's own Methods.

## 5. Suggested Reviewer Expertise

Five areas are needed, weighted toward methodology. First, surface-enhanced Raman spectroscopy of biofluids with plasmonic nanoparticle substrates, specifically spectral-set representations and non-negative least squares unmixing against metabolite panels. Second, untargeted urine metabolomics by LDI-MS or LC-MS, including adduct-based annotation confidence and normalisation. Third, machine learning evaluation methodology for clinical prediction, with specific competence in data leakage, class-imbalance-aware metric selection, calibration and TRIPOD+AI reporting. Fourth, multimodal deep learning that fuses text encoders with structured and spectral inputs for differential diagnosis. Fifth, clinical urology covering the benign and malignant spectrum represented here, with expertise in non-invasive urine biomarker evaluation and screening study design.

## 6. State-of-the-Art Literature Review (Past Three Years)

Three lines of work define this space. In SERS metabolic phenotyping, Bi et al. (*Cell Reports Medicine* 2024) introduced SERSomes for prostate cancer with 80.8% internal and 73% external accuracy; Bi et al. (*Chem* 2025) extended this to molecule-resolvable decomposition; and Lu et al. (*Nanoscale* 2025) applied urine SERSomes to low-grade bladder cancer. All three come from the submitting group, which makes the absence of head-to-head comparison and the omission of the last of them a significant gap. Independent SERS urine work includes Moisoiu et al. (*Molecular Medicine* 2022), combining miRNA and SERS liquid biopsy for bladder cancer stratification, and the 2025 review by Ainiwaer et al. in *Photodiagnosis and Photodynamic Therapy* on Raman spectroscopy of urine in urological disease; neither is cited.

In non-invasive urologic diagnostics, Keum et al. (*Nature Biomedical Engineering* 2025) set the current bar with a double-blind, point-of-care hyaluronidase assay reaching AUC 0.93 with 88.3% sensitivity and 88.9% specificity. It is cited here as reference 14 but never used as a comparator. In multimodal differential diagnosis, Xue et al. (*Nature Medicine* 2024) is the appropriate template: it reports external cohorts, class-wise confidence intervals and clinician comparison for dementia aetiology, all of which are missing here. The present manuscript advances instrumentation and interpretability, but on diagnostic evidence it sits behind both its own precedents and the independent literature.

## 7. Suggested Reviewer Names

For SERS biofluid profiling: Tudor Moisoiu (Iuliu Hațieganu University, Cluj-Napoca), first author of "Combined miRNA and SERS urine liquid biopsy for the point-of-care diagnosis and molecular stratification of bladder cancer"; Stefania D. Iancu (Babeș-Bolyai University), co-author on the same and on SERS serum metabolite normalisation work; Andrei Ștefancu (Helmholtz Munich), postdoctoral researcher on SERS detection of metabolites in biofluids.

For urine biomarkers and non-invasive urologic diagnostics: Changjoon Keum (Korea Institute of Science and Technology), first author of "Diagnosis of early-stage bladder cancer via unprocessed urine samples at the point of care"; Michiel Maas (Radboud University Medical Center), first author of "Urine biomarkers in bladder cancer — current status and future perspectives"; Barbara Pardini (Italian Institute for Genomic Medicine), senior author on urinary molecular stratification of bladder cancer.

For machine learning evaluation and leakage: Sayash Kapoor (Princeton University), first author of "Leakage and the reproducibility crisis in machine-learning-based science"; Chonghua Xue (Boston University), first author of "AI-based differential diagnosis of dementia etiologies on multimodal data".

---

*Word count — Sections 1–4: 308; Sections 5–7: 504 (unchanged from prior draft). The 500-word target is exceeded because the manuscript contains four separable internal numerical inconsistencies and two independent validity threats that each require specific remediation language. To reach 500 words I would compress Sections 2 and 3 to one paragraph each and cut Sections 6 and 7 to bare citations, which would remove the leakage argument's evidentiary detail. Advise if that trade is acceptable.*

074274
# Editorial Report — Manuscript 074274

**Title:** SpineAgent: An Autonomous Large Language Model Multi-Agent System for Interpretable Spinal MRI Diagnosis
**Section:** Digital Health — *Nature Communications*

---

## Editorial Integrity Alert (Confidential — Handling Editor Only)

Three items require attention before any decision letter is sent.

First, a name and scope collision. arXiv:2606.08897 (Xiao, Yang, Sun, … Cross, Wang; submitted 8 June 2026) presents an unrelated system also called **SpineAgent**, likewise a multi-agent spine MRI framework, trained on 32,047 patients and 453,683 series, with cross-manufacturer and cross-cohort evaluation and expert review by five radiologists. The groups appear independent (University of Washington versus Zhejiang University). The present manuscript neither cites nor distinguishes itself from it. This is directly competing prior art that supersedes several of the present claims on scale and generalizability, and the shared name is itself a publication problem.

Second, verifiable factual errors in the Baselines section that bear on author diligence: GPT-5.4-mini and Qwen3.5-plus are both attributed to Google (lines 618–620). Reference 41 cites the original Gemini technical report (arXiv:2312.11805, 2023) as the source for Gemini-3-Flash, a December 2025 model — citation misattribution.

Third, evaluator independence. The two spine specialists who scored treatment plans (lines 168–169) match the described roles of co-authors DDY (over five years' experience) and BC (twenty years). The protocol is called double-blind, yet co-authors scoring their own system is a competing-interest issue not disclosed under Section 8, and no inter-rater agreement statistic is reported.

Additionally, the consent statement (line 732, "Every human participant should provide their consent") is an unexecuted template, and IRB approval IIT20250450B names only "the First Affiliated Hospital" without specifying the institution or covering the FAHWMU external cohort. Both must be resolved regardless of decision.

---

## 1. Overall Assessment

SpineAgent claims a three-module agentic pipeline enables interpretable spinal MRI diagnosis, outperforming six zero-shot LLM baselines on 10,374 internal and 181 external cases. The comparison is confounded: SpineAgent's core is Qwen3-VL-8B fine-tuned via SFT and GRPO on the target distribution, while every comparator is zero-shot; no fine-tuned single-model control isolates the agentic architecture's contribution. Ground truth is LLM-extracted from radiology reports, not histopathology, so the headline malignant-tumour result measures report-text agreement, not cancer detection.

## 2. Strengths

The dataset is substantial: 451,206 DICOM slices from 10,520 patients, including 1,688 malignant tumours, with stratified 8:2 splitting preserving long-tail prevalence. Raw DICOM ingestion is a genuine workflow advance over curated-export pipelines. Uncertainty reporting exceeds subfield norms, with 1,000-resample bootstrap CIs and bootstrap-derived significance. The KEA ablation is well-controlled: Gemini's hemangiomata Recall@1 rises from 0.1914 to 0.5038 with keyframe extraction, isolating slice selection as the driver.

## 3. Weaknesses

The ablation swaps only the diagnostic agent for untuned baselines; it cannot separate fine-tuning from architecture, so the central multi-agent claim is unsupported. Reported figures are internally inconsistent: cohort counts don't reconcile (10,511 − 146 ≠ 10,374), the QC claim of "85–95%" excludes its own 96.5% point estimate, and the treatment SD (0.6237) is arithmetically impossible given 68/100 cases scoring 5 with mean 4.57 (minimum feasible SD ≈0.68). External validation is thin: malignant tumours are absent from the 181-patient external cohort entirely, fractures degrade externally, and no subgroup or calibration analysis is given. Data and code are unavailable at submission.

## 4. Editorial Decision

**Reject.** The fine-tuning/architecture confound, report-derived ground truth, absent external validation for the flagship claim, and impossible treatment statistics are not fixable by revision. Countervailing case: the DICOM-native pipeline and tumour cohort are real contributions, but this requires a new study, not revision, and competing prior art (arXiv:2606.08897) already reports broader validation. Recommend transfer to *npj Artificial Intelligence* or *Communications Medicine*, conditional on correcting the arithmetic, consent statement, and evaluator disclosure.

## 5. Suggested Reviewer Expertise

Reviewers should cover parameter-efficient adaptation of vision-language models for radiology, specifically SFT plus GRPO or DPO on Qwen-VL or InternVL backbones and the design of fine-tuned controls; retrieval-augmented generation with hybrid BM25 and dense retrieval, reciprocal rank fusion and hallucination auditing in clinical text; evaluation methodology for imbalanced multi-label medical imaging, including bootstrap inference, calibration and Recall@k localization metrics; multi-agent LLM system design and ablation practice in healthcare; and, on the clinical side, musculoskeletal radiology with subspecialty expertise in spinal MRI of neoplastic and degenerative disease, plus a spine surgeon able to judge whether RAG-generated regimens are safe under Chinese and international guideline practice.

## 6. State-of-the-Art Literature Review (Past Three Years)

The relevant landscape has three strands. Automated spine MRI grading is mature and externally validated: SpineNet and SpineNetv2 have been tested on the Northern Finland Birth Cohort 1966 (McSweeney et al., *Spine* 2023, balanced accuracy 78% for disc degeneration, 86% for Modic change), against Schulthess Klinik data (Grob et al., *Eur Spine J* 2022), and most recently in a multi-pathology agreement study (Wu et al., *Eur Spine J* 2026). The RSNA 2024 Lumbar Spine Degenerative Classification challenge has since become the reference public benchmark, with DINOv2-based multi-grade stenosis pipelines validated across centres. The manuscript engages with none of this and reports no comparison to a task-specific vision model, only to general-purpose LLMs — a baseline choice that flatters the system.

The second strand is multi-agent clinical LLM design, where MDAgents (Kim et al., NeurIPS 2024) and MedAgents (Tang et al., ACL Findings 2024) are the standard references, alongside recent audits showing that multi-agent structures can manufacture false consensus. The manuscript's Review Diagnostic Agent is a consensus mechanism of exactly this kind and is never audited for that failure mode. The third strand is the direct competitor identified above, arXiv:2606.08897, which reports a DINOv3-based multi-sequence spine foundation model with cross-manufacturer evaluation and radiologist review at roughly three times the patient scale. Against this landscape the manuscript's distinctive contributions reduce to DICOM-native ingestion and the malignant-tumour cohort; the diagnostic and localization results replicate capabilities already demonstrated with stronger validation.

## 7. Suggested Reviewer Names

For vision-language adaptation and spine imaging models: **Amir Jamaludin** (University of Oxford), senior researcher and SpineNet author, on "External validation of the deep learning system SpineNet" (*Eur Spine J* 2022); **Rhydian Windsor** (University of Oxford), co-author of the same SpineNet validation work and of vertebra detection methods.

For multi-sequence spine foundation models and agentic imaging systems: **Zhiping Xiao** (University of Washington), first author of "A multi-agent system for spine MRI report generation from multi-sequence imaging" (arXiv:2606.08897, unreviewed preprint — flag accordingly); **Sheng Wang** (Assistant Professor, University of Washington), senior author of the same work. Note the direct competition and screen for conflict.

For external validation methodology in spine MRI deep learning: **Aleksei Tiulpin** (Associate Professor, University of Oulu) and **Terence P. McSweeney** (University of Oulu), authors of the SpineNet NFBC1966 external validation (*Spine* 2023, doi:10.1097/BRS.0000000000004572).

For multi-agent LLM evaluation in medicine: **Yubin Kim** (MIT Media Lab), first author of MDAgents (NeurIPS 2024); **Xiangru Tang** (Yale University), first author of MedAgents (ACL Findings 2024).

For the clinical assessment: **Jiaxiang Zhou** or **Zhiyu Zhou** (Sun Yat-sen University), authors of the SpineNetv2 multi-pathology external validation (*Eur Spine J* 2026, doi:10.1007/s00586-025-09543-z). Both are geographically and institutionally independent of Zhejiang University and Wenzhou Medical University.

# Editorial Report — "Auditable machine learning for high-stakes decisions"

*Nature Communications, Digital Health section. Handling editor's assessment.*

---

## Editorial Integrity Alert (confidential — handling editor only)

**Pre-registration claim.** The word "pre-registered" appears throughout, including in the abstract, but the only evidence offered is an internal file (`domain_labels_preregistered.csv`) inside the authors' own archive. There is no registry identifier, third-party timestamp, or DOI. A self-held CSV is not pre-registration. This claim must be substantiated or struck before any further consideration; several headline framings ("the model declares where it works, predicts where it fails") depend on it.

**Reference 39.** The cited source for the "historically reported 7–11 point rule-model discrimination deficit" (Kusner et al., *Learning optimal decision lists*, ICML 2534–2543, 2016) could not be located in the ICML 2016 proceedings (PMLR v48) or in Kusner's publication record. This citation is load-bearing: it is the baseline against which BLN's 1.5-point deficit is presented as progress. Reference 7 also renders the venue as "ACM SIGKILL" (SIGKDD). A full reference audit is warranted.

**Uncited directly competing prior art.** The priority claim ("first model to emit both sufficient and necessary conditions from a single calibrated, cross-validated architecture") is contradicted by literature the manuscript does not cite. Benamira, Guérand and Peyrin's TT-rules explicitly extracts necessary and sufficient rules from a trained network in a healthcare decision setting (arXiv:2309.11101). IRCnet (*Neurocomputing*, 2024) pairs a Neural AND Layer and a Neural OR Layer to emit CNF and DNF rule sets from one architecture. Qiao, Wang and Lin's DR-Net (AAAI 2021) and the Rule Network with Selective Logical Operators (arXiv:2408.11918) occupy the same space. The manuscript's neural-symbolic citations stop at DeepProbLog and δILP; the 2021–2025 differentiable rule-learning literature is absent. Whether this is oversight or selective citation, the novelty claim as written cannot stand.

**Competing interests / authorship.** No author list, affiliations or contributions were supplied ("to be completed upon acceptance"), so independence from the baseline authors (RRL, NCA) could not be checked.

---

## 1. Overall Assessment

BLN learns a DNF sufficient path and a CNF necessary path over binarized features, fused by a gate and thresholded into crisp rules, claiming to answer the auditor's two questions under GDPR Article 22.

Two concerns dominate. This is a general interpretable-machine-learning paper, not digital health: the flagship cases are COMPAS, German Credit and HR Attrition, and the clinical content is UCI Hepatitis (n = 155), Pima (1988) and Heart. And the abstract's certification claim is refuted by the manuscript's own verification section, where fired sufficient rules were followed by the positive prediction in only 71.5%, 50.5% and 41.7% of cases.

## 2. Strengths

The protocol is disciplined and the arithmetic holds: identical folds and seeds across eleven methods, and reconstructed out-of-scope AUCs reproduce the stated values (BLN 0.9319 versus 0.931).

The dual-path ablation is the strongest result: across 30 datasets the gated model beats both single-path variants without exception, by a median of 9.9 and 10.2 AUC points (Wilcoxon p < 10⁻⁸).

The envelope is falsifiable, and disconfirming evidence is published — real-data rule wrongness, necessary-rule Jaccard 0.677, an ICAM-2 negative control returning zero hits.

## 3. Weaknesses

A 0.0–0.4% false-veto rate is trivially achieved by near-tautologous necessary clauses. No specificity measure, no no-veto null and no excluded-input fraction is reported; P3 decidability measures coverage, not selectivity. This is the decisive missing analysis.

COMPAS is modelled and "policy legality" auditing claimed with no race-stratified or equalized-odds analysis; the only bias experiment is synthetic.

All p-values are uncorrected across 55 pairwise comparisons per scope, yet p = 0.036 confirms a pre-registered prediction; ranking claims rest on 0.001–0.012 AUC gaps against ±0.025–0.031 standard errors.

Figure 5 states 12 of 20 edges recovered in canonical direction, the text 10 of 12; and 40 of 60 stable rules connect protein pairs with no consensus edge, undiscussed.

## 4. Editorial Decision

Reject, with transfer to *npj Artificial Intelligence*. The work is not digital health, the priority claim is contradicted by uncited prior art extracting necessary and sufficient rules from one architecture, and the certification claim is refuted by the authors' own verification. Counterargument: the ablation is clean and pre-specified and disconfirming results are disclosed, so reviewers could reasonably be left to judge whether form-only auditability counts. If overridden, they must adjudicate whether the necessary conditions are non-trivially restrictive, and whether priority survives TT-rules, IRCnet, DR-Net and RNS.

## 5. Suggested Reviewer Expertise

Reviewers should cover, on the technical side, differentiable Boolean rule learning and neural-symbolic architectures that extract CNF/DNF formulae from trained networks; formal verification and bounded model checking of learned classifiers, including SAT-based rigorous explanation and the semantics of sufficient and necessary "prime implicant" explanations; benchmark methodology and multiple-comparison correction for cross-dataset model comparison on tabular data, with probability calibration (Brier, ECE) expertise; and necessary-condition methodology in the social sciences, specifically NCA and QCA, to assess whether the F1 = 0.92 versus 0.88 comparison against NCA is a fair one. On the clinical and governance side, reviewers should cover algorithmic fairness and subgroup auditing in criminal-justice and clinical risk prediction, and the regulatory interpretation of contestability and recourse under GDPR Article 22 and the EU AI Act.

## 6. State-of-the-Art Literature Review (Past Three Years)

The relevant frontier is differentiable rule learning, and the manuscript engages almost none of it. Wang et al.'s RRL (*IEEE TPAMI* 46, 1121–1133, 2024) is cited as a baseline but not as a conceptual competitor. Qiao, Wang and Lin's DR-Net (AAAI 2021) learns decision rule sets directly from a two-layer binarised network. Benamira, Guérand and Peyrin's TT-rules, built on Truth Table nets, extracts necessary and sufficient rule sets from a trained network and does so explicitly for healthcare decision making — this is the closest published antecedent and its absence from the reference list is the manuscript's most consequential omission. IRCnet (*Neurocomputing*, 2024) instantiates a Neural AND Layer and a Neural OR Layer to emit CNF and DNF rule sets from one hierarchical model. The Rule Network with Selective Logical Operators (2024) learns per-neuron AND/OR selection to form CNF/DNF rules simultaneously, which is a strictly more general version of BLN's fixed dual-path design. The formal-explanation literature (Marques-Silva, Ignatiev and colleagues on abductive and contrastive explanations, and SAT-based rigorous explanations for decision lists) has spent five years formalising exactly the sufficiency and necessity semantics BLN claims to introduce, with soundness guarantees BLN's thresholded approximations do not provide.

Two older traditions also go unacknowledged and undercut the framing of bracketing as novel. Mitchell's version-space S and G boundaries bound a target concept from below and above, which is structurally what S(x) ≤ f(x) ≤ N(x) restates in probabilistic form; Pawlak's rough-set lower and upper approximations do the same. On the interpretability side, the manuscript's positioning against Rudin (*Nat. Mach. Intell.* 1, 206–215, 2019) and Vinuesa, Brunton and Mengaldo (*Nat. Commun.* 17, 7933, 2026) is accurate — the latter's framing of an explanation as a lead requiring external verification is the paper's best-used citation. Where BLN genuinely advances the field is narrow but real: the 30-dataset demonstration that a necessary-condition path adds ~10 AUC points over a sufficient-only model is, to my knowledge, unreported elsewhere, and the mapping of sufficient and necessary rules onto activating and inhibitory edges in the Sachs network is a creative validation design. That contribution is worth a paper. It is not worth this paper's claims.

## 7. Suggested Reviewers

**Differentiable rule learning and neural-symbolic extraction:** Adrien Benamira (Nanyang Technological University; TT-rules, "A New Interpretable Neural Network-Based Rule Model for Healthcare Decision Making") — the single most directly qualified reviewer, and the one who can settle the priority question. Litao Qiao (UC San Diego; "Learning Accurate and Interpretable Decision Rule Sets from Neural Networks," AAAI 2021). Zhuo Wang (RRL; "Learning Interpretable Rules for Scalable Data Representation and Classification," *IEEE TPAMI* 2024) — note a mild competing interest as a baseline author.

**Formal verification and prime-implicant explanations:** Alexey Ignatiev (Monash University, senior lecturer; "SAT-Based Rigorous Explanations for Decision Lists"). Jiachang Liu (Duke; "FasterRisk: Fast and Accurate Interpretable Risk Scores," NeurIPS 2022).

**Benchmark methodology, calibration and interpretable tabular models:** Chudi Zhong ("Generalized and Scalable Optimal Sparse Decision Trees," ICML 2020; "The Rashomon Importance Distribution," NeurIPS 2023). Muhang Tian / Chloe Qinyu Zhu (interpretable sepsis risk modelling, KDD 2024) for the clinical-tabular perspective.

**Fairness auditing and contestability:** Berk Ustun (UC San Diego, assistant professor; "Actionable Recourse in Linear Classification") — directly on the recourse framing the manuscript invokes. Chris Russell (Oxford Internet Institute; co-author of "Counterfactual Explanations Without Opening the Black Box," which the manuscript cites as reference 48 but never engages).

**Necessary-condition methodology:** Jan Dul (Erasmus University; originator of NCA, reference 34) — full professor, suggested only because the manuscript's NCA comparison is a direct empirical challenge to his method and no junior researcher with comparable standing in that literature could be identified.
