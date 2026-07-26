# Trackrad202512456

060197
## Editorial Integrity Alert (to Handling Editor)

Two issues require author clarification before this manuscript can proceed to review.

First, an undisclosed, closely overlapping prior publication exists for Task 3. Wang, Lang, Zhang, and Anumba published "Electrical Impedance Spectroscopy Based Preterm Birth Prediction with Machine Learning" (AIiH 2024, Springer LNCS 14975, DOI 10.1007/978-3-031-67278-1_7), using the same Sheffield cervical-EIS PTB cohort, the same clinical prior (PTB history), and three of the same four classifiers (RF, MLP, SVM). Two authors (Z.-Q. Lang, D.O.C. Anumba) are shared with the present submission, yet this paper is neither cited nor discussed. The reported cohort size differs (365 records/43 PTB vs. 438 subjects/62 PTB here), suggesting either an expanded cohort or a distinct subset — either way, the relationship between the two datasets and the two sets of ML baseline results needs to be disclosed and reconciled.

Second, reference 51 duplicates reference 45 (Lin et al., Sci Rep 2025, DOI 10.1038/s41598-025-05116-8) under a garbled, near-identical title and an incomplete author list (missing M. Matella). This is either a reference-list error or an undisclosed second source; the editor should ask the authors to clarify what reference 51 is actually citing.

---

## 1. Overall Assessment

PIML fuses an ML classifier's own optimized sensitivity/specificity with a clinical prior via Bayes' theorem — a real, narrow advance over static-prior tools like Chatzimichail and Hatjimihail (2024). It does not clear the bar as submitted: Task 2 (9 diseased subjects) cannot support the "three representative domains" novelty claim, and the PTB cohort overlaps an uncited prior publication by two co-authors.

## 2. Strengths

The Cervical-G1/G2 design is genuinely strong: 1,677 training subjects plus an independent 112-subject external cohort (Royal Free), with PIML lifting AUC from 0.637–0.640 to 0.833–0.846 and generalizing externally (AUC 0.787–0.804). The four-way ablation (prior-only, ML, ML+prior, PIML) with Wilcoxon signed-rank testing across 100 repetitions is methodologically sound. The PIML(APP) arm, substituting QUiPP for the internal prior, meaningfully shows the framework tolerates external, real-world priors.

## 3. Weaknesses

Task 2's 9-case disease cohort makes its reported CIs an artifact of instability, not real performance — a non-revisable flaw. Table 1's asterisks are mislabeled: PIML sensitivity is significantly *lower* than baseline ML for DT, RF, and MLP, yet marked as "significant improvement." All three cohorts are retrospective reuses of the authors' own prior data, directly contradicting the Introduction's critique of others' lack of prospective validation. No subgroup analysis (age, ethnicity, SES) is reported despite plausible EIS confounds.

## 4. Editorial Decision

**Reject.** Task 2's sample size is unfixable and the PTB overlap must be resolved before novelty can be assessed. Counterargument: Cervical-G1/G2 alone (1,789 subjects, cross-institutional) is publishable, and a sympathetic editor might restrict review to that cohort. Not persuasive here — the paper's central claim is validation across three domains, so dropping two changes the claim itself, requiring resubmission, not revision. Recommend transfer to **npj Digital Medicine**, conditional on resolving the Wang et al. 2024 overlap.

## 5. Suggested Reviewer Expertise

Bayesian calibration and probabilistic fusion of classifier outputs with domain priors; bioimpedance/Cole-model signal processing and EIS instrumentation; small-sample and class-imbalance statistical validation in clinical ML (threshold selection, bootstrap/permutation testing); colposcopy-based cervical dysplasia screening and adjunctive diagnostic technologies; maternal-fetal medicine with expertise in preterm birth risk stratification tools (e.g., QUiPP-class instruments).

## 6. State-of-the-Art Literature Review (Past 3 Years)

Informed/knowledge-integrated ML has matured into a distinct subfield since von Rueden et al.'s 2021 taxonomy, with Sirocchi et al. (BMC Med Inform Decis Mak, 2024) mapping knowledge-integration strategies (including Bayesian-network imputation) across the full ML pipeline, and Chatzimichail and Hatjimihail (BMC Med Inform Decis Mak, 2024; Diagnostics, 2023–2024) building software tools for uncertainty-quantified Bayesian posterior estimation in diagnostics — the manuscript correctly distinguishes itself from this line by optimizing sensitivity/specificity end-to-end rather than treating them as fixed inputs. A more direct and currently uncited competitor is the 2026 line of work on using ML outputs as elicited Bayesian priors ("Supercharging Bayesian Inference with Reliable AI-Informed Priors," arXiv 2605.09834), which the authors should engage with directly. On EIS specifically, Bergqvist et al. (BMJ Open, 2023) and Tsampazis et al. (Diagnostics, 2024) provide recent prospective, multi-center EIS-colposcopy validation in exactly the clinical niche this manuscript targets but without any Bayesian fusion — the manuscript should cite and differentiate against this literature rather than relying solely on its own group's earlier cervical dataset papers.

---

## Suggested Reviewer Names

**Bayesian fusion/probabilistic ML for diagnostics:** Aristides T. Hatjimihail (Hellenic Complex Systems Laboratory — BMC Med Inform Decis Mak 2024, Bayesian posterior probability software for disease diagnosis); Christel Sirocchi (Univ. of Urbino — BMC Med Inform Decis Mak 2024, medical-informed ML pipeline integration, noting she is a PhD researcher rather than postdoc, offered as the closest topical match found).

**EIS instrumentation/signal processing:** a reviewer from the Bergqvist et al. (BMJ Open, 2023) or Tsampazis et al. (Diagnostics, 2024) EIS-colposcopy groups, given direct ZedScan-platform experience.

**Small-sample clinical ML validation:** authors of the Sirocchi et al. 2024 review above, given its explicit treatment of small clinical datasets.

**Clinical — colposcopy/cervical screening:** a co-author from Bergqvist et al. 2023 (e.g., I. Kalliala group, BMJ Open) given prospective EIS-colposcopy trial experience.

**Clinical — preterm birth risk assessment:** a QUiPP-app-affiliated investigator (Carter et al. 2020; Watson et al. 2020, Ultrasound Obstet Gynecol), given direct familiarity with the external prior tool used in Task 3.

059814-T
## Editorial Integrity Alert (for handling editor only)

Independent search confirms this manuscript is already public as arXiv:2605.31437, posted May/June 2026, identical title and 22-author list. The arXiv v2 abstract reports FORTE gains of 65.7% (BIMCV) and 32.2% (Merlin) versus 65.0% and 27.2% in the submitted PDF — this numeric drift needs reconciling with the authors before review proceeds. Separately, ref. [22] ("Gemini-3") cites arXiv:2312.11805, the 2023 Gemini technical report, not any Gemini 3 documentation.

---

### 1–4. Overall Assessment, Strengths, Weaknesses, Editorial Decision

Astra is a 3D CT report-generation foundation model trained on a harmonized 90,678-pair multi-center dataset (CTRgDB), combining region-wise report harmonization with GRPO reinforcement learning against a revised FORTE-style reward, and claims broad generalizability across six out-of-distribution cohorts plus a prospective human-AI trial.

CTRgDB's harmonization measurably separates positive/negative semantic clusters (Fig. 2a,b) rather than merely asserting improvement. External validation spans six OOD cohorts, including resilience testing on 2D-reconstructed pseudo-3D data. The crossover-design human-AI trial, with blinded senior-radiologist scoring, is genuinely differentiated: efficiency gains in chest CT, completeness gains in abdominal CT. Downstream extensibility experiments (ensemble classification, synthetic-report VLM pretraining) show the generated reports carry real diagnostic signal.

Set against this: FORTE/Rate-Score serve as both the GRPO reward and the headline evaluation metric, with no fully independent metric confirming the RL gains aren't partly self-referential. No demographic subgroup analysis (age, sex, scanner vendor) appears despite four newly collected cohorts. Three of four in-house cohorts and both human-AI trial arms are Chinese hospitals, undercutting the generalizability framing. The human evaluation used a single scorer per modality with no inter-rater reliability reported, undermining the statistical claims built on that one rater's scores.

**Decision: Send for Review**, contingent on the authors reconciling the arXiv/manuscript numerical discrepancy and confirming preprint disclosure. Reviewers must adjudicate whether a reward-independent metric confirms the RL diagnostic gains, whether the single-rater evaluation can be supplemented, and whether generalizability claims require qualification given the geographic concentration of real-world validation.

---

### 5. Suggested Reviewer Expertise

Reviewers should cover: reinforcement learning post-training (GRPO/RLVR) for clinical text generation and reward-design pitfalls including reward hacking; 3D vision-language model architecture for volumetric medical imaging (visual token compression, Perceiver-style resamplers); NLG/clinical-efficacy metric design for radiology report generation (entity-matching and attribute-level scoring); biostatistics for human-AI collaboration trial design, including inter-rater reliability and crossover analysis; and a practicing radiologist with combined chest and abdominal CT reporting experience across junior-to-senior expertise levels, matching the trial's reader population.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

3D CT report generation has moved rapidly from single-region proof-of-concept toward foundation-model framing. Merlin (Blankemeier et al., *Nature*, 2026) established a 3D CT-EHR-report VLM pretrained without task-specific annotation; CT-Rate/CT-CLIP (Hamamci et al., *Nat. Biomed. Eng.*, 2026) remains the dominant open chest-CT resource and is one of Astra's own harmonization sources. Region-conditioned generation (Reg2RG, cited as [12]; MedRegion-CT) and fine-grained spatial-grounding work (e.g., "Enhancing Fine-Grained Spatial Grounding in 3D CT Report Generation via Discriminative Guidance," 2026) address the same anatomical-localization problem Astra tackles via harmonized templates rather than explicit grounding — a design choice the authors should defend more directly against grounding-based alternatives.

On the RL side, Astra is not the first to apply GRPO with a clinically-derived reward to radiology report generation: concurrent 2025-2026 work on chest X-ray reporting — SDR (set-distance rewards, Stanford), RadVLM+RL (RadCliQ reward), OraPO (FactScore-based reward), and "Rethinking the Efficiency and Effectiveness of RL for RRG" (DiTPO) — establishes the same GRPO-with-clinical-reward paradigm months to a year earlier, albeit in 2D. None of these are cited. Astra's genuine novelty is applying this now-familiar recipe at 3D multi-region CT scale with a redesigned, region-partitioned FORTE reward; the manuscript should acknowledge this precedent rather than implying the RL strategy itself is unprecedented. A concurrent benchmark, CT-FineBench (DAMO Academy/Hupan Lab, 2026), proposes a QA-based fine-grained fidelity metric for CT reports built on the same CT-Rate/Merlin sources — a natural comparison point for Astra's own FORTE-derived evaluation that the authors likely could not have cited given timing, but reviewers should ask whether it changes the evaluation story.

---

### Suggested Reviewers' Names

**RL/reward design for radiology report generation:** H. Ibrahim Gulluk (Stanford, SDR); authors of the RadVLM+RL GRPO study; authors of OraPO (FactScore-reward GRPO).

**3D CT vision-language modeling:** Ibrahim Ethem Hamamci (MD-PhD candidate, University of Zurich; CT-Rate, CT-CLIP, CT2Rep — note possible conflict of interest given his co-founded venture building competing generalist CT foundation models); Louis Blankemeier or Ashwin Kumar (Stanford, co-first authors, Merlin, *Nature* 2026).

**Fine-grained clinical evaluation metrics:** Cheng-Yi Li or Kao-Jung Chang (FORTE/BrainGPT, *Nat. Commun.* 2025).

**Clinical/abdominal CT AI:** Junya Sato or Kento Sugimoto (Osaka University, Dept. of AI in Diagnostic Radiology — multi-center annotation-free abdominal CT abnormality detection, *EBioMedicine* 2024).

---

### 7. Further Literature (Past 3 Years, Similar Scope)

1. **Blankemeier, L. et al.** "Merlin: a computed tomography vision–language foundation model and dataset." *Nature* 652, 1318–1328 (2026). DOI: 10.1038/s41586-026-10181-8. Peer-reviewed. **Cited** by Astra (ref. 31; also Astra's abdominal region template source). Author-independent (Stanford). Directly comparable scope: multi-task 3D CT-report-EHR foundation model with external-site validation, the closest existing analogue to Astra's generalizability claim, though single-anatomy (abdomen) versus Astra's multi-region design.

2. **Hamamci, I.E. et al.** "Generalist foundation models from a multimodal dataset for 3D computed tomography." *Nat. Biomed. Eng.* (2026). DOI: 10.1038/s41551-025-01599-y. Peer-reviewed. **Cited** (CT-Rate/CT-CLIP source). Author-independent (UZH). Source of CT-Rate, one of Astra's five harmonized training cohorts and its principal chest-CT benchmark; also introduces CT-CHAT, a competing 3D chat-style report/QA model Astra does not directly benchmark against.

3. **Li, C.-Y. et al.** "Towards a holistic framework for multimodal LLM in 3D brain CT radiology report generation." *Nat. Commun.* 16, 2258 (2025). DOI: 10.1038/s41467-025-57426-0. Peer-reviewed. **Cited** (ref. 11; origin of FORTE). Author-independent (Taiwan). Astra's entire reward function is a re-engineered extension of this paper's FORTE metric; direct methodological lineage, different anatomy (brain vs. thoracoabdominal).

4. **Chen, Z., Bie, Y., Jin, H., Chen, H.** "Large language model with region-guided referring and grounding for CT report generation." *IEEE Trans. Med. Imaging* (2025). **Cited** (ref. 12; chest CT template source). Author-independent. Region-guided generation approach Astra's chest-CT harmonization template is explicitly modeled on; Astra harmonizes reports into fixed regions rather than learning explicit grounding, a design contrast reviewers should probe.

5. **Zhang, X. et al.** "Development of a large-scale grounded vision language dataset for chest CT analysis" (RadGenome-Chest CT). *Sci. Data* 12, 1636 (2025). DOI: 10.1038/s41597-025-05922-9. Peer-reviewed. **Cited** (ref. 64). Author-independent (Shanghai Jiao Tong University/SJTU-affiliated group, distinct from Astra's SJTU-affiliated authors — no name overlap). Supplied the region-level annotations for CT-Rate that Astra reused rather than re-deriving.

6. **Yuan, R. et al.** "CT-FineBench: A Diagnostic Fidelity Benchmark for Fine-Grained Evaluation of CT Report Generation." arXiv:2604.24001 (2026). **Not peer-reviewed** — flag as unreviewed. **Not cited** by Astra. Institutional overlap: DAMO Academy/Hupan Lab, the same institutional affiliation as three Astra co-authors (Yu, Wang, Luo), though no overlapping named authors. QA-based fine-grained factual-consistency benchmark built on the same CT-Rate/Merlin sources Astra uses — a directly competing evaluation paradigm to FORTE/Rate-Score that reviewers should ask the authors to engage with.

7. **Gulluk, H.I., Van Puyvelde, M., Van Criekinge, W., Gevaert, O.** "SDR: Set-Distance Rewards for Radiology Report Generation." arXiv:2606.00440 (2026). **Not peer-reviewed** — flag as unreviewed. **Not cited**. Author-independent (Stanford/Ghent). GRPO with a continuous, clinically-grounded, permutation-invariant reward for report generation — same reward-design philosophy Astra presents as novel, applied to chest X-ray with a different reward formulation.

8. **[Authors].** "Enhancing Radiology Report Generation and Visual Grounding using Reinforcement Learning" (RadVLM+RL). arXiv:2512.10691 (2025). **Not peer-reviewed** — flag as unreviewed. **Not cited**. Author-independent. GRPO with a clinically-grounded reward (RadCliQ) for report generation, predating Astra by roughly six months; establishes that GRPO-with-clinical-reward for radiology reporting is not a novel paradigm, only novel at 3D CT scale.

9. **[Authors].** "OraPO: Oracle-educated Reinforcement Learning for Data-efficient and Factual Radiology Report Generation." arXiv:2509.18600 (2025). **Not peer-reviewed** — flag as unreviewed. **Not cited**. Author-independent. Introduces a dense, per-label FactScore-based reward for GRPO radiology reporting — directly relevant precedent for Astra's own claim that "dense rewards were more effective than sparse diagnostic rewards."

10. **[Authors].** "A Multi-Center Benchmark for Abdominal Disease Diagnosis and Report Generation from Non-Contrast CT." arXiv:2606.16991 (2026). **Not peer-reviewed** — flag as unreviewed. **Not cited**. Author independence unconfirmed — recommend the editor verify no overlap with Astra's abdominal-CT external sites. Directly competing scope claim: a multi-center abdominal CT report-generation benchmark, the same underexplored niche Astra's introduction identifies as its motivating gap.

059239
# Editorial Integrity Alert (to Handling Editor)

Two items warrant verification before this manuscript proceeds. First, the Introduction attributes a ResNet-50 patellar-MRI sex-estimation result (accuracy 0.889) to "Oner et al." (citing ref. 22), but independent search identifies ref. 22 as Cavlak, Çınarer, Erkoç & Kılıç, *Forensic Sci Med Pathol* 2025 — no "Oner" appears among its authors, and the reported figure (88.88% with ResNet-50) matches this paper exactly. This is a citation misattribution that should be corrected regardless of outcome. Second, the stated code repository (github.com/LiuTao331/Patella-MTF) could not be located via independent search; the editor should confirm with the authors that it is public and populated before relying on it for reproducibility claims.

---

## 1. Overall Assessment

The manuscript proposes a Transformer-based fusion model that combines automated morphometric parameters, radiomic features, and 2D/3D CNN embeddings to estimate sex from patellar CT, tested on 697 internal and 139 external cases from two Qinghai centres. The central claim is that principled cross-modal fusion via self-attention outperforms single-modality models and simpler fusion baselines, and generalises better across acquisition protocols.

The engineering is careful and the statistical apparatus (DeLong test, bootstrap CIs, decision curve analysis) is more rigorous than most of the cited literature. However, the paper's own external-validation results undercut its headline claim: on the harder, distribution-shifted external cohort — the very test meant to demonstrate the value of the architecture — Transformer Fusion did not significantly outperform the six-parameter logistic-regression Conventional model (ΔAUC = −0.007, p = 0.628). The elaborate multimodal pipeline earns its keep only against CNN and ensemble baselines, not against the simplest one.

## 2. Strengths

The feature-engineering pipeline is unusually transparent: 107 PyRadiomics features reduced via variance filtering, Spearman pruning, and LASSO to 13 stable features, with cross-validation curves and correlation heatmaps reported rather than asserted.

External validation from an independent centre (Qinghai Ren Ji Hospital, different scanner, 2.0 mm vs 1.5 mm slices) is a genuine domain-shift test, rare in this specific literature where most comparators (Cavlak et al., Oner-attributed work notwithstanding) are single-site.

The human-machine time-motion comparison, quantifying an order-of-magnitude speed advantage and documenting ~8 mm inter-operator variability in manual patellar length, is a concrete and useful contribution.

## 3. Weaknesses

The entire cohort derives from one province and is implicitly one regional population; the literature this paper itself cites (Peckmann, Maio, Akhlaghi) repeatedly demonstrates population-specific dimorphism, so forensic deployment claims exceed what a single-population sample supports.

The model is trained and tested exclusively on in vivo clinical CT of living patients, yet the Discussion and Introduction motivate the work through disaster victim identification and degraded/burnt remains — a deployment context never tested.

The human-machine comparison used a Sichuan Han discriminant formula because no Qinghai-specific formula exists, meaning the "expert" comparator was handicapped by population mismatch identical to what the authors criticise; this invalidates the comparison as a ceiling estimate of human performance.

The pipeline still depends on manual ROI segmentation (three experts, Dice > 0.9), so claims of full automation and objectivity are only partially true, and no sensitivity analysis quantifies how segmentation variability propagates to classification.

## 4. Editorial Decision

**Reject, with transfer to npj Digital Medicine or Communications Medicine.** The engineering is sound but the core justification for the Transformer architecture does not survive its own external test, the population base is narrow for the sweeping forensic claims made, and the human comparator was structurally disadvantaged. These are addressable through reframing and additional analyses, not disqualifying, but they fall short of the cross-population, deployment-relevant advance this venue requires.

## 5. Suggested Reviewer Expertise

Multimodal transformer fusion architectures for medical imaging; radiomics feature selection and LASSO-based pipelines; forensic skeletal sex estimation methodology; population-specific discriminant function validation; forensic anthropology and disaster victim identification workflows.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Multimodal transformer fusion is now well established in oncologic imaging — e.g., PBTC-TransNet for bone tumor classification across X-ray/CT/MRI, and transformer fusion for hepatic cystic echinococcosis lesion bioactivity (Wang et al., 2025, cited as ref. 23, notably sharing a likely author with this submission). Forensic sex estimation, by contrast, remains dominated by single-modality CNN benchmarking: Cavlak et al. (2025) benchmarked five CNN backbones on patellar MRI; a 2025 Diagnostics study benchmarked six CNNs on whole-foot radiographs. This manuscript's contribution is best characterised as transplanting an already-validated fusion architecture into a new anatomical/forensic context rather than a novel modeling advance, and it should engage directly with why cross-modal attention fusion, proven in oncology, adds less over simple baselines here than in those settings.

## Suggested Reviewer Names

Multimodal fusion / transformer methods: Zhenwei Shi; Jakob Nikolas Kather. Radiomics pipelines: Martin Vallières; Ahmad Chaddad. Forensic sex estimation: Elena Kranioti; Kate Robson Brown. Disaster victim identification: Hans H. de Boer; Soren Blau.

058926
**Editorial Report — Condensed (Sections 1–4) + Further Literature**

**1. Overall Assessment**

The manuscript applies a Decision Transformer to recommend RRT-initiation timing in AKI, trained on 89,185 CRDS patients and validated across five external cohorts (N=42,121), reporting a weighted HR of 0.54 for 30-day mortality and 3.21 for renal recovery under DT-clinician concordance. The contribution is scale and evaluation rigor, not architectural novelty: the "first" sequence-modeling claim for RRT timing does not hold against existing peer-reviewed RL-based RRT literature, and the causal framework is adapted closely from a very recent published precedent.

**2. Strengths**

Six-cohort validation spanning US ICU databases and three general Chinese hospital systems is larger and more heterogeneous than prior RRT-RL validation, which has topped out near 1,000–1,400 patients. The WIS-plus-IPTW causal design mirrors JAMA's OVISS framework, appropriately cited. Four pre-specified sensitivity analyses, including a shuffled-policy negative control, credibly test whether the effect is patient-specific rather than a population-level shift.

**3. Weaknesses**

The novelty claim is overreached: Grolleau et al. (JAMIA, 2024) and, more pressingly, HRRT (npj Digital Medicine, June 2026) — a hierarchical-RL RRT CDSS published one month prior — are not engaged. The concordance definition is dominated by the ~95% "mutual non-initiation" majority, and the discordant comparator group necessarily skews toward faster-deteriorating patients, a confounding-by-indication only partly resolved by excluding 3-day deaths. Ref. 4, the "KDIGO 2026 Clinical Practice Guideline," remains a public-review draft rather than a finalized publication, yet is cited as settled consensus. WIS effective sample size and weight-distribution diagnostics, defined in Methods, are not reported despite RRT's rarity (4.3–4.6%) making heavy-tailed weights likely.

**4. Editorial Decision**

Send for Review, with major revisions required first. The validation scale and causal framework represent a real, narrower-than-claimed advance; none of the weaknesses is structurally unfixable. Reviewers should adjudicate whether the revised novelty claim survives engagement with HRRT and the Grolleau line of work, whether a severity-restricted sensitivity analysis can address the concordance confound, and whether reported ESS supports the WIS reliability claimed.

---

**5. Suggested Reviewer Expertise**

Reviewers should cover: offline reinforcement learning and Decision Transformer / sequence-modeling architectures for longitudinal EHR data; off-policy and offline policy evaluation methods (weighted importance sampling, doubly robust estimators) in clinical decision support; marginal structural models and time-varying confounding in observational EHR causal inference; and, on the clinical side, critical-care nephrology with direct experience in RRT-timing trial design and KDIGO AKI staging.

**6. State-of-the-Art Literature Review (Past 3 Years)**

The field has moved rapidly past static risk prediction toward dynamic, validated RRT decision support: Grolleau et al. (JAMIA, 2024) externally validated a doubly robust dynamic RRT strategy against two RCTs; Morzywołek et al. (Crit Care, 2022) applied dynamic treatment regimes to the same question; and HRRT (npj Digital Medicine, 2026) delivered a hierarchical-RL CDSS spanning timing, modality, and weaning across US, Dutch, and Chinese cohorts. Separately, the OVISS vasopressin study (JAMA, 2025) established the WIS-plus-IPTW causal evaluation template this manuscript adopts. Against this landscape, the manuscript's distinguishing feature is validation breadth, not methodological originality, and the Discussion should be rewritten to position the DT contribution accordingly rather than as a first-in-kind.

**7. Suggested Reviewer Names**

For offline RL / sequence modeling: François Grolleau (JAMIA, 2024 — RL-based dynamic RRT initiation externally validated on AKIKI/AKIKI2). For offline policy evaluation methodology: Anand Kalimouttou (JAMA, 2025 — OVISS, WIS plus IPTW framework for treatment-initiation timing). For clinical AI CDSS in RRT: Mengling Feng or Zhongheng Zhang (npj Digital Medicine, 2026 — HRRT hierarchical RL for RRT decision support). For critical-care nephrology: Kay Choong See (npj Digital Medicine, 2026 — corresponding author, HRRT, critical-care nephrology and CDSS deployment).

---

**Further Literature (Past 3 Years, Similar Scope)**

1. Grolleau F, Petit F, Gaudry S, et al. Personalizing renal replacement therapy initiation in the intensive care unit: a reinforcement learning-based strategy with external validation on the AKIKI randomized controlled trials. *J Am Med Inform Assoc*. 2024;31(5):1074–1083. DOI: 10.1093/jamia/ocae004. Peer-reviewed. Not cited by the manuscript. No author overlap (AP-HP/INSERM, Paris). Directly on RRT-timing optimization via RL, externally validated against AKIKI/AKIKI2 RCT data using an importance-sampling evaluation logic closely paralleling this manuscript's WIS approach — the single most direct piece of missing prior art.

2. Xu Q, Wu F, Thong ZYC, et al. HRRT: hierarchical reinforcement learning for renal replacement therapy decision support. *npj Digit Med*. 2026;9. DOI: 10.1038/s41746-026-02900-2. Peer-reviewed. Not cited. No author overlap (National University of Singapore / Sir Run Run Shaw Hospital). Published one month before this submission; a holistic hierarchical-RL CDSS covering RRT timing, modality, ultrafiltration, and weaning, externally validated across US, Dutch, and Chinese cohorts — the most direct contemporaneous competitor and the strongest challenge to the "first" claim.

3. Kalimouttou A, Kennedy JN, Feng J, et al. Optimal Vasopressin Initiation in Septic Shock: The OVISS Reinforcement Learning Study. *JAMA*. 2025;333(19):1688–1698. DOI: 10.1001/jama.2025.3046. Peer-reviewed. Already cited (ref. 41) — correctly engaged. No author overlap. Establishes the WIS-plus-IPTW-weighted pooled logistic regression causal template this manuscript adopts wholesale, applied to a different organ system (vasopressin timing in septic shock).

4. Zhang B, Mi Y. World Model Enhanced Offline Reinforcement Learning for Sequential Intervention Optimization in Acute Kidney Injury. *AI Med*. 2026;3(1):2. DOI: 10.53941/aim.2026.100002. Peer-reviewed (newer venue; maturity should be independently confirmed by the editor). Not cited. No apparent author overlap. Uses MIMIC-IV (46,337 patients) with an FNO-Transformer world model plus stage-aware Implicit Q-Learning for AKI sequential interventions including RRT — overlapping clinical scope and transformer-based architecture, though value-based rather than return-conditioned sequence modeling.

5. Kim H, Kim JH, Lee SW, et al. Safety-aware explainable deep reinforcement learning for nephrotoxic medication management in critical care. *Biomed Signal Process Control*. 2026;112:108577. DOI: 10.1016/j.bspc.2025.108577. Peer-reviewed. Not cited. No author overlap (Korea University). Offline RL framework modeling AKI and dialysis as terminal outcomes alongside mortality — adjacent scope, comparable safety-aware evaluation design.

6. Choi Y, et al. Deep reinforcement learning extracts the optimal sepsis treatment policy from treatment records. *Commun Med*. 2024;4:245. DOI: 10.1038/s43856-024-00665-x. Peer-reviewed (Nature Portfolio). Not cited. No author overlap (Gwangju Institute of Science and Technology / Asan Medical Center). Broader critical-care RL policy extraction from historical treatment records with offline evaluation — comparable design philosophy, different clinical target.

7. Wang Y, Liu A, Yang J, et al. Clinical knowledge-guided deep reinforcement learning for sepsis antibiotic dosing recommendations. *Artif Intell Med*. 2024;150:102811. DOI: 10.1016/j.artmed.2024.102811. Peer-reviewed. Not cited. No author overlap. Adjacent critical-care RL dosing-recommendation scope with knowledge-guided constraints.

8. Tu R, Luo Z, Pan C, et al. Offline safe reinforcement learning for sepsis treatment: tackling variable-length episodes with sparse rewards. *Hum-Centric Intell Syst*. 2025;5(1):63–76. DOI: 10.1007/s44230-025-00093-7. Peer-reviewed. Not cited. No author overlap (Southwest Jiaotong University). Addresses the same core technical problem this manuscript's return-to-go formulation targets — sparse terminal rewards and variable-length trajectories in offline RL for critical care.

9. Abdul Rahman A, Agarwal P, Noumeir R, Jouvet P, Michalski V, Ebrahimi Kahou S. Empowering Clinicians with Medical Decision Transformers: A Framework for Sepsis Treatment. arXiv:2407.19380 (OpenReview submission), 2024. **Not peer-reviewed — unreviewed preprint.** No author overlap (Mila / Université de Montréal / CHU Sainte-Justine). The closest architectural precedent found: applies the Decision Transformer itself (not RL generally) to a critical-care treatment-timing problem with goal-conditioned, sparse rewards, evaluated via WIS/WDR/FQE — nearly the identical toolkit as this manuscript, applied to sepsis rather than AKI/RRT. Should be cited and distinguished, not ignored.

10. Zhu S, Yan J, Gong S, Feng X, Ning G, Xu L. Machine Learning-Aided Decision-Making Model for the Discontinuation of Continuous Renal Replacement Therapy. *Blood Purif*. 2024;53(9):704–715. DOI: 10.1159/000539787. Peer-reviewed. Not cited. No author overlap (Zhejiang University / Zhejiang Hospital). Dynamic ML decision-support model for RRT discontinuation timing — the mirror-image clinical question (stopping vs. starting RRT) from a Chinese ICU dataset, methodologically comparable and geographically adjacent to this manuscript's Chinese external cohorts.

053828—T
**Reviewer 1 – Zaifu Zhan (most critical, effectively a reject).** Argues the entire premise is a manufactured problem: investigation ordering in real medicine is constrained by cost, compliance, and protocol, not just information-theoretic optimality, and the paper never benchmarks against deployed CDSS (UpToDate, Isabel, DXplain) — only against other LLMs. Calls out that DiagBench's "diagnoses" are reproduced from EHRs where the answer is already known, so this is diagnosis-reproduction, not blind diagnosis. Flags a circular evaluation loop: DiagGym is validated by similarity metrics, DiagAgent is trained inside DiagGym, and the headline "behavioral" results (Figs 5–6) are then tested on DiagGym's own generated trajectories. Adds RL-specific gaps (unspecified algorithm, no hyperparameter sensitivity, no ablation removing DiagGym) and clinical-safety gaps (no interpretability, no adversarial testing, no patient-safety discussion, no prospective or even retrospective real-world validation). Also argues the RL+LLM+simulator combination is not novel relative to DoctorAgent-RL, MedAgentSim, and AgentClinic.

**Reviewer 2 – Samuel Schmidgall (constructive, major revision).** Sees genuine promise but independently lands on the same circularity problem: the two strongest claims (proactive evidence-gathering, better trajectory alignment) rest entirely on in-distribution evaluation inside DiagGym, while the only simulator-independent test (Fig. 3) is single-step, not the multi-step decision-making the RL formulation is built for. Second concern: DiagGym conditions on the ground-truth final diagnosis when generating counterfactual test results, which he argues manufactures artificially clean feedback — no evidence is given that it generates reliable results for novel (never-ordered) tests. Third: no safety/ethics statement, no error-type or demographic breakdown despite a ~13% diagnostic error rate. He proposes concrete fixes (held-out real trajectories, a second independent simulator, physician review of DiagGym's counterfactual plausibility) rather than declaring the work dead.

**Reviewer 3 – Jian Li (most favorable, minor-to-moderate revision).** Calls the work "high-quality, original, well-engineered." Main technical critique: the turn-penalty reward doesn't weight test cost, invasiveness, or radiation — so the policy could in principle win by over-ordering expensive/invasive tests as long as turn count stays low; wants a cost-aware reward term plus an ablation. Independently raises the same DiagGym-realism issue as Schmidgall (conditioning on true diagnosis, no modeling of delay, noise, or contradictory results). Wants case-level comparisons against a general LLM on identical cases, formal error analysis, rare-disease (Orphanet) testing, and token-efficiency analysis. Minor items: reconcile inconsistent case counts, flag that DiagAgent is task-trained while baselines are zero-shot.

**Editor's own circulation notes (Eric Wang).** Independently converges on the same load-bearing issue as Reviewers 1 and 2 — the same LLM judge (Qwen2.5-72B) computes the reward *and* the primary evaluation metric, and the self-generated behavioral rollouts (Figs 5–6) are treated as primary evidence rather than the static reference-matching evaluation (Table 4). Also flags single-center MIMIC-IV training with no demographic subgroup analysis, and no deployment-safety/regulatory framing.

**Convergence.** Three independent reviewers and the handling editor, writing without access to each other's comments, all identified the same core defect: DiagGym's self-referential validation loop, and the unverified claim that it generates trustworthy counterfactual results for tests never actually ordered. That's not noise — that's the paper's central vulnerability.

**Decision: Major Revision, not outright reject.** None of the four sources allege fabrication, undisclosed preprints, or cohort overlap — this is a methodological gap, not an integrity issue. Two of three reviewers (Schmidgall, Li) explicitly frame the flaws as fixable with defined experiments (simulator-independent trajectory evaluation, cost-aware reward ablation, safety/ethics statement, subgroup and rare-disease analysis, broader base-model coverage), and the underlying contribution — joint investigation+diagnosis RL with a purpose-built benchmark — is independently valued by 2/3 reviewers and by the editor's own strengths list. Revision should be made conditional on: (1) simulator-independent, multi-step validation of DiagAgent's trajectory-level claims (held-out real data or a second simulator, as Schmidgall specifies); (2) physician validation of DiagGym's counterfactual generation for tests not in the original record; (3) a cost/risk-weighted reward term with ablation; (4) a patient-safety, ethics, and data-governance section; (5) demographic/rare-disease stratified performance.

**Counterargument for outright rejection.** Reviewer 1's position is not unreasonable: every piece of evidence for the paper's multi-step claims currently comes from the same environment used to train the policy. If the requested simulator-independent evaluation is run and the gains evaporate, the entire contribution reduces to "an RL policy overfit to a hand-built reward inside its own training simulator" — a non-revisable flaw that would only surface after this revision round, costing another full review cycle. Recommend telling the authors explicitly that if the resubmission's independent validation doesn't hold up, this should be rejected without further revision — no second grace cycle.

**One thing worth flagging that wasn't asked:** the tracking system currently shows an *unsubmitted* "Overall Rating: Reject" with letter template "1 Reject – no review (DC)" — a desk-reject template — dated before any of the three substantive reviews came in. That looks like stale form state from before the paper was sent out. Worth clearing/overwriting before you submit the actual decision, or the system may fire off a desk-reject-no-review letter that contradicts the fact that three reviews exist.

043605
**Reviewer 1 (Wu Yuan — medical imaging/agentic AI):** Recommends outright reject. Core objections: (1) evaluation confined to small, well-worn public tabular sets (Pima, Wisconsin Breast Cancer, CKD) with no prospective or multimodal task, so findings shouldn't be presented as generalizable to real clinical practice; (2) validation methodology (splits, seeds, stratification, whether preprocessing/tuning happened inside or outside the resampling loop) is unspecified, raising a concrete Varma-and-Simon-style leakage risk; (3) performance is reported as bare point estimates — deltas as small as 0.003–0.005 are called "better" with zero uncertainty quantification, seeds, or significance testing; (4) the claimed human-in-the-loop oversight is undocumented — no audit trail of what humans changed, when, or how much autonomy the agents actually had; (5) manuscript-quality scoring relies on undisclosed LLM judges (reportedly Gemini) with no blinded human expert check, inviting self-preference bias; (6) no ablations isolate what's driving the result — single- vs multi-agent, with/without refinement, vs. a standardized AutoML baseline are all absent.

**Reviewer 2 (chen qian — general LLMs/agentic AI):** No explicit recommendation given in the excerpt, but the balance is negative. Strengths credited: addresses a genuine question (workflow-level vs. single-step agent participation), performance is competitive on directly comparable tasks, and the five-category refinement taxonomy (problem framing, feature representation, validation design, model exploration, clinical interpretation) is a useful analytic lens. Weaknesses largely mirror Reviewer 1: limited methodological novelty (standard AI-PI orchestration pattern), case selection and inclusion/exclusion criteria under-specified with several cases not directly comparable (reframed targets, mixed metrics — AUC/accuracy/F1 — with no unified statistical synthesis), no baseline/ablation comparisons, data diversity limited to structured tabular only (no imaging, waveform, pathology, genomic, or longitudinal EHR data), LLM-only article-quality evaluation without human validation, and no statistical robustness testing on the (small) reported gains. Also flags sloppy presentation — apparently AI-generated figures and inconsistent naming (ELVES vs. "V-Labs").

**Convergence:** Both reviewers land on the same four structural problems: (a) narrow, easy, non-clinical benchmark; (b) absent baselines/ablations, so the causal driver of any reported gain is unknown; (c) no uncertainty quantification, so the reported "wins" cannot be distinguished from noise; (d) LLM-as-judge quality scoring with no independent human validation, which is close to circular given the system itself uses an LLM to write and grade.

**Decision: Reject**, not revise-and-resubmit. The uncertainty-quantification and baseline gaps are individually fixable, but the combination — small/easy benchmark, no ablations to attribute the effect to multi-agent coordination versus base model capability, and self-graded output quality — means the manuscript's central claim ("agentic systems can substitute for human-led research workflows") is currently unfalsifiable as evaluated. That is a design-level flaw, not a reporting gap; fixing it means rerunning the study with a different evaluation architecture, not patching the current one. Combined with genuinely limited novelty in an already-crowded agentic-LLM-for-science literature, this doesn't clear the bar for sending to a second round — reject and redirect toward a venue with a lower novelty threshold (e.g., npj Digital Medicine or Communications Medicine) once redesigned with prospective/multimodal data, nested cross-validation, ablations against a standard AutoML baseline, and blinded human evaluation of output quality.
