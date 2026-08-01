# Trackrad202512456
062418
# Editorial Report — "From cardiopulmonary signals to sleep phenotypes: a personalized low-burden framework for longitudinal sleep-health monitoring"

---

## Editorial Integrity Alert (Handling Editor Only)

Three points require resolution before this manuscript can be assessed on its stated merits alone.

**Cohort and author overlap with the authors' own prior Nature Communications paper.** The Methods subsection "Relationship to prior work" discloses that SHHS, MESA, MrOS, ClinHuaiAn and ClinSuZhou are the same cohorts used in ResSleepNet (Zhuang, Z. et al., *Nat. Commun.* 16, 9334, 2025 — verified: published 22 Oct 2025, same first author and two of the same corresponding authors, Xue and Hong). The two papers report near-identical top-line numbers: ResSleepNet's abstract states 82.13%/79.62% internal/external staging accuracy and AHI ICC 0.90/0.94, against 80.4–85.6% and 0.92–0.94 here. The present manuscript is transparent about this in Methods, which mitigates but does not resolve the concern — the disclosure is not surfaced in the abstract or introduction, where the framework is presented as if built from first principles. The manuscript also states test partitions were "generated independently" but simultaneously concedes "participant-disjointness therefore cannot be assumed for cohorts containing repeat visits or multiple nights" — this needs a direct answer, not a hedge, before the editor can evaluate whether the reported public-cohort numbers are a genuinely independent replication or a re-run on overlapping patients.

**Undisclosed commercial relationship.** The HDP-RSM-001 sensing device — which lends its name to the paper's core clinical-transfer cohort (HDP-RSM) — is a Class II registered medical device manufactured by Nanjing Hongding Perception Technology Co., Ltd. No author lists an affiliation with this company, and competing interests are declared as none. Given that the device is central to the paper's flagship low-burden claim, the editor should confirm independently whether any author, funder, or institution has an undisclosed relationship with the manufacturer.

**Abstract overstates a null result.** The abstract states that perioperative monitoring "revealed postoperative shifts toward shorter, more fragmented sleep that aligned with recorded recovery status." The Results and Discussion state plainly that none of the eight prespecified phenotypes survived Benjamini–Hochberg correction, and the Discussion explicitly cautions that the application "does not establish clinical utility, causality or a diagnostic substitute." This is a materially more favorable framing in the abstract than the paper's own statistics support and should be corrected regardless of the editorial outcome below.

---

## 1. Overall Assessment

The manuscript pipelines PSG-anchored multimodal pretraining (respiration, ECG, SpO2), personalized federated adaptation across clinical sites, and teacher–student distillation into a contactless radar-ring student, evaluated across 15,496 nights. Metrics reconcile exactly across abstract, tables and figures. But the deployable radar-ring student — the title's central claim — is validated at one site only, and the pretraining layer substantially reuses cohorts and results from the authors' own *Nat. Commun.* paper published nine months earlier. The genuinely new contribution is narrower than the four-layer framing implies.

## 2. Strengths

The FedPer-style federated personalization is genuinely novel and honestly benchmarked against non-federated references, with mixed results reported rather than smoothed over. The teacher–student distillation (Eq. 7) is well specified and ablated component-by-component (Table 4). Module/modality ablations (Fig. 3) physiologically justify combining respiration, ECG and oximetry. The authors' unprompted self-critique — weak Deep-sleep recall, severe-AHI underestimation, single-site validation — exceeds the norm for this literature.

## 3. Weaknesses

The deployable sensor has no external validation beyond one site and one device configuration — ordinarily a rejection-level gap at this venue. AHI estimation systematically underestimates severe OSA (bias −4.18 events/h, 75% under-predicted at AHI≥30), the highest-stakes clinical group. No demographic subgroup or fairness analysis is reported despite marked cohort skew (MrOS 100% male, all ≥65y). The perioperative findings are statistically null after FDR correction yet the abstract frames them as clinically aligned — an overstatement relative to the paper's own reported statistics.

## 4. Editorial Decision

**Reject; transfer to *npj Digital Medicine*.** Two compounding, non-revision-fixable gaps — single-site deployment validation and substantial pretraining-layer overlap with the authors' prior paper — undermine both headline claims. Counterargument: the federated-personalization and distillation machinery is architecturally distinct from ResSleepNet and could stand alone if reviewers specifically adjudicate cohort-overlap and single-site-validation acceptability.

---

## 5. Suggested Reviewer Expertise

Reviewers should include expertise in multimodal Transformer/cross-modal attention fusion of physiological time-series data; federated learning with personalization layers (FedPer/FedAvg-style partial parameter sharing) applied to decentralized clinical datasets; knowledge distillation for cross-sensor-domain transfer, specifically PSG-to-contactless-radar and PSG-to-PPG transfer; and, on the clinical side, sleep medicine with direct experience in AASM-standard PSG scoring and OSA severity grading, plus perioperative or postoperative sleep physiology given the exploratory surgical cohort.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has bifurcated over the past two years into two trajectories that this manuscript sits between without fully engaging either. One trajectory is large-scale foundation modeling: <cite index="14-1">Thapa et al.'s SleepFM, trained on over 585,000 hours of PSG recordings from roughly 65,000 participants, produces latent sleep representations that generalize to predicting future disease risk across many conditions from a single night of sleep</cite>, published in *Nature Medicine* in January 2026. This represents an order-of-magnitude larger and philosophically different approach — self-supervised generalist representations rather than supervised, task-specific heads — and the present manuscript's Discussion acknowledges this direction only briefly, without benchmarking its supervised multi-task design against what a foundation-model transfer approach would offer for the same low-burden deployment problem.

The second trajectory is exactly the paper's own lane: transferring PSG-anchored mappings to genuinely low-burden contactless or minimal-contact sensors. Here <cite index="21-1">BCGNet pre-trains on 580,865 hours of PSG and fine-tunes on 15,081 hours of ballistocardiogram data, achieving four-class staging F1 of 0.710–0.817 and AHI Pearson correlation above 0.95 with strong generalizability across diverse external validation cohorts</cite> — a direct competitor that, unlike the present submission, explicitly validates across multiple independent external datasets, which is precisely the gap identified above. The manuscript's own Table 5 already positions itself credibly against this and other comparators (OxiNet, SleepPPG-Net, Sridhar et al.), which is appropriate namedropping discipline; what is missing is any external-cohort test of comparable rigor to BCGNet's own validation design. The authors should engage directly with why their radar-ring student was not tested on a second site the way BCGNet, He et al.'s radar work, and the ResSleepNet predecessor's own external-validation split were.

---

## 7. Suggested Reviewer Names

**Multimodal fusion / cross-modal attention for physiological time-series:** Hyatt Moore IV (Stanford/BioSerenity — sleep signal processing and PSG-derived model pipelines); Andreas Brink-Kjaer (Technical University of Denmark — co-author on SleepFM's multimodal contrastive architecture); Magnus Ruud Kjaer (Technical University of Denmark — SleepFM co-lead author, direct expertise in multimodal sleep representation learning).

**Federated learning in clinical/decentralized settings:** Manisha Padala or a comparably positioned postdoctoral/assistant-professor-level federated-learning-in-healthcare researcher with published work applying FedPer- or FedAvg-style personalization to multi-site clinical time-series (to be confirmed for independence from the submitting group before invitation).

**Cross-sensor knowledge distillation / low-burden sleep sensing:** Kevin Kotzen (SleepPPG-Net, IEEE JBHI 2023 — PPG-to-PSG transfer); Joachim Behar or Jeremy Levy (OxiNet, *Nat. Commun.* 2023 — single-channel oximetry transfer to AHI estimation); Xiangdong Tang or Yue Leng (BCGNet corresponding authors, West China Hospital Sichuan University / UCSF — PSG-to-BCG two-stage transfer learning, directly comparable low-burden design). Note: BCGNet's first author (Shigeng Chen) and one corresponding author (Chunfeng Liu) share an institution — the Second Affiliated Hospital of Soochow University — with this manuscript's ClinSuZhou site; Tang and Leng do not share that overlap and are the safer independent choice.

**Clinical sleep medicine / perioperative recovery physiology:** a sleep-medicine physician with OSA severity-grading and AASM scoring experience, and a perioperative/anesthesiology-adjacent clinician with postoperative recovery and sleep-continuity monitoring experience, both confirmed independent of Xiangya Hospital, Central South University and Soochow University, the submitting authors' clinical sites.

---

## Further Literature (Past 3 Years, Closely Overlapping Scope)

**1. Lin, S.; Tang, R.; Wang, Y.; Wang, Z. "Multimodal Fusion Multi-Task Learning Network Based on Federated Averaging for SDB Severity Diagnosis." *Applied Sciences* 2025, 15(14), 8077.** DOI: 10.3390/app15148077. Peer-reviewed (MDPI, open access). Not cited by manuscript. Authors affiliated with Jilin University and TU Eindhoven — independent of the submitting group. This is the single closest published analogue in the literature: a federated multi-task learning (FMTL) framework performing joint sleep staging and SDB severity classification from multimodal physiological signals, using a shared-feature-extractor/task-specific-head architecture and FedAvg across three public datasets (APPLES, SHHS, HMC) treated as independent clients — methodologically parallel to the submitted manuscript's shared-private decomposition and PEL design. The manuscript's failure to cite or differentiate from this paper is a material SOTA-engagement gap.

**2. Xie, J.; Fonseca, P.; van Dijk, J.; Overeem, S.; Long, X. "A multi-task learning model using RR intervals and respiratory effort to assess sleep disordered breathing." *BioMedical Engineering OnLine* 2024, 23, 45.** DOI: 10.1186/s12938-024-01240-0. Peer-reviewed. Not cited. Independent (Eindhoven/Kempenhaeghe group, Netherlands). A shared-encoder multi-task model combining cardiac (ECG-derived RR) and respiratory-effort signals to jointly perform sleep-wake classification and AHI estimation — essentially a minimal two-endpoint version of the submitted paper's three-endpoint design, without four-class staging or SDB severity stratification.

**3. Xie, J.; Fonseca, P.; van Dijk, J.P.; Overeem, S.; Long, X. "Multi-modal multi-task deep neural networks for sleep disordered breathing assessment using cardiac and audio signals." *International Journal of Medical Informatics* 2025, 201, 105932.** DOI: 10.1016/j.ijmedinf.2025.105932. Peer-reviewed. Not cited. Same independent group as #2, extending the architecture with an audio modality — direct precedent for the modality-ablation logic underlying the submitted paper's Fig. 3.

**4. Choi, J.; Koo, D.; Kim, D.; Nam, H.; Lee, J.; Hong, S.; Kim, B. "A novel deep learning model for obstructive sleep apnea diagnosis: hybrid CNN-Transformer approach for radar-based detection of apnea-hypopnea events." *Sleep* 2024, 47(12), zsae184.** DOI: 10.1093/sleep/zsae184. Peer-reviewed. Not cited (distinct from He et al., ref. 28, zsae187, same journal/year). Independent (South Korea). Radar-only AHI/OSA estimation via hybrid CNN-Transformer (MAE 7.54 events/h, ICC 0.889) — a direct radar-based AHI benchmark the submitted paper's radar-ring result (MAE 4.32, ICC 0.960) should be positioned against but is not.

**5. Lin, S.-Y.; Tsai, C.-Y.; Majumdar, A.; et al. "Combining a wireless radar sleep monitoring device with deep machine learning techniques to assess obstructive sleep apnea severity." *Journal of Clinical Sleep Medicine* 2024, 20(8), 1267–1277.** DOI: 10.5664/jcsm.11136. Peer-reviewed (official AASM journal). Not cited. Independent (Taiwan). Commercial wireless-radar device plus deep-learning OSA-severity classification — directly parallel to the HDP-RSM device-validation arm, but evaluated as a home-setting screening tool across a broader population than the submitted paper's single sleep-center cohort.

**6. Gross-Isselmann, J.A.; Eggert, T.; Wildenauer, A.; Dietz-Terjung, S.; Grosse Sundrup, M.; Schoebel, C. "Validation of the Sleepiz One+ as a radar-based sensor for contactless diagnosis of sleep apnea." *Sleep and Breathing* 2024, 28(4), 1691–1699.** DOI: 10.1007/s11325-024-03057-6. Peer-reviewed. Not cited. Independent (Germany). A single-site (n=141), radar-plus-SpO2 commercial-device validation against PSG — essentially the same sensor combination and single-center design as the manuscript's HDP-RSM arm; notably, this paper also reports that agreement with PSG-AHI worsens with increasing SDB severity, the same failure pattern flagged as a weakness above, and is worth citing as convergent evidence rather than an isolated finding.

**7. Wang, J.; Xue, J.; Zou, Y.; Ma, Y.; Xu, J.; Li, Y.; Deng, F.; Wang, Y.; Xing, K.; Li, Z.; Zou, T. "A Dual-Modal Wearable Pulse Detection System Integrated with Deep Learning for High-Accuracy and Low-Power Sleep Apnea Monitoring." *Advanced Science* 2025, 12(24), 2501750.** DOI: 10.1002/advs.202501750. Peer-reviewed, open access. Not cited. Independent (Beijing Hospital/CAMS/BINN/BIT/USTC group). A low-power PPG-plus-piezoelectric wearable for apnea-event detection (99.6%/95.0% accuracy in high-accuracy/low-power modes) — relevant to the ring-PPG component of the deployable student, though it targets binary event detection rather than AHI/staging.

**8. "Fusion of Millimeter-wave Radar and Pulse Oximeter Data for Low-burden Diagnosis of Obstructive Sleep Apnea-Hypopnea Syndrome." arXiv:2501.15264 (posted January 2025).** **Not peer-reviewed — preprint only; flagged per protocol.** Not cited by manuscript. Independence not fully confirmed (author list not verified in available sources). Nearly identical sensor combination to two-thirds of the submitted paper's low-burden student (mmWave radar + pulse oximeter, i.e., radar + SpO2 without the ring-PPG channel) applied to the same clinical problem. Given the concurrent timing (Jan 2025) and near-identical sensor pairing, the editor may wish to confirm the authors are aware of this work, though its unreviewed status means it carries less weight than items 1–7.

**9. "A Multi-Task Deep Learning Approach for Simultaneous Sleep Staging and Apnea Detection for Elderly People" (RGMNet). *Interdisciplinary Sciences: Computational Life Sciences*, published online 5 June 2025.** DOI: 10.1007/s12539-025-00721-7. Peer-reviewed. Not cited. Independence appears likely (uses the unrelated "Human Sleep Project" dataset) but author/institutional affiliation was not independently verified in available sources and should be confirmed before reviewer assignment. Directly relevant to the age-subgroup fairness gap flagged in Weaknesses: this model is purpose-built for an elderly-only population (ages 60–90) and explicitly models age-related staging/apnea interaction, which the submitted manuscript — despite MrOS being 100% ≥65-year-old — does not attempt.

**10. Gadangi, P.V.; Lambert, B.S.; Goble, H.; Harris, J.D.; McCulloch, P.C. "Validated Wearable Device Shows Acute Postoperative Changes in Sleep Patterns Consistent With Patient-Reported Outcomes and Progressive Decreases in Device Compliance After Shoulder Surgery." *Arthroscopy, Sports Medicine, and Rehabilitation* 2023, 5(5), 100783.** DOI: 10.1016/j.asmr.2023.100783. Peer-reviewed, open access. Not cited. Independent (Houston Methodist, USA). The closest existing precedent for low-burden, wearable-derived perioperative sleep-pattern monitoring linked to clinical/patient-reported recovery status — and, notably, this paper reports statistically supported correlations between sleep-metric changes and validated patient-reported outcome measures, which is precisely the kind of evidentiary support the submitted manuscript's perioperative section lacks (its eight phenotypes did not survive multiplicity correction). Directly relevant counter-example the authors should engage with when reframing their perioperative claims.

062702
Sections 1–4 condensed to ~300 words below; Sections 5–7 unchanged from the prior report. Further Literature appendix follows.

---

### 1–4. Overall Assessment, Strengths, Weaknesses, Editorial Decision (condensed)

This manuscript combines two frozen self-supervised UK Biobank accelerometry encoders to predict incidence across 388 phecode outcomes plus mortality (mean concordance 0.688), then decomposes cross-disease risk into a single Shared Actigraphic Risk Component (SHARC, 76% of variance) plus disease-specific residual signal. The core contribution is conceptual: unlike most phenome-wide wearable studies, the authors show apparent multi-disease prediction is mostly one frailty-like axis, with genuine disease-specific signal surviving mainly for neurodegenerative and select cardiometabolic outcomes, most notably prodromal Parkinson's disease (five-year AUROC 0.90, 428 cases), a verified improvement over the Schalkamp et al. (2023) benchmark under a matched definition.

Strengths: the SHARC decomposition is methodologically novel and unusually self-critical for this literature; the comparator design (demographic, 100-field activity-summary, and polygenic-score baselines, all leakage-safe cross-fitted) is rigorous; the Parkinson's finding is stress-tested with lead-time washout and a higher-powered secondary cohort analysis; and the ablation program preempts obvious objections.

Weaknesses: no external cohort validation anywhere, a significant gap given UK Biobank's known selection bias; no subgroup analysis by ancestry, ethnicity, or socioeconomic status; substantial, unquantified under-ascertainment for the flagship neurodegenerative outcomes; and calibration/decision-curve claims resting on a reconstructed rather than original baseline hazard.

**Editorial Decision: Send for Review.** The SHARC framework and rigorous baseline comparisons constitute a genuine, non-incremental contribution, and the principal risk (near-term detection bias) is adequately addressed via washout analysis. Reviewers should adjudicate the SHARC's novelty relative to the authors' own SleepFM architecture, the acceptability of omitting external validation and subgroup analysis, and cohort independence from the authors' concurrent Parkinson's preprint.

---

### 5. Suggested Reviewer Expertise

Reviewers should include expertise in self-supervised representation learning for time-series and wearable sensor data, specifically masked-autoencoder and transformer pretraining objectives applied to accelerometry, to assess whether the frozen-encoder-plus-linear-head design is adequately justified against fine-tuning alternatives. A second technical reviewer should have expertise in large-scale multilabel Cox survival modeling and leakage-safe cross-fitting methodology for phenome-wide disease panels, to scrutinize the event-stratified cross-fitting procedure and the principal-component-based SHARC construction. A third technical area is UK Biobank-scale epidemiological cohort methodology, including phecode-based outcome definition and polygenic risk score integration, to assess case-ascertainment validity and the genetics-fusion analysis. On the clinical side, reviewers should include movement-disorder neurology expertise in prodromal Parkinson's disease biomarkers, and sleep medicine or respiratory physiology expertise relevant to the AcceleRest encoder's cardiorespiratory-amplification design and its clinical plausibility for conditions such as sleep apnoea and COPD.

### 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved rapidly from single-outcome accelerometry models toward two convergent directions this manuscript sits between: phenome-wide association-style studies using engineered activity features (Khurshid et al., *npj Digital Medicine* 2022), and self-supervised foundation models for wearable time series (Yuan et al., *npj Digital Medicine* 2024, 700,000 person-days pretraining, which this manuscript's HA encoder is built on; the Pretrained Actigraphy Transformer applied to NHANES mental-health outcomes, Ruan et al. 2026). The single most important comparator, Schalkamp et al. (*Nature Medicine* 2023), established UK Biobank accelerometry as a strong prodromal Parkinson's predictor (AUPRC 0.07 prodromal, 0.14 diagnosed) against genetic, lifestyle, and biochemistry baselines; this manuscript's improvement to AUPRC 0.18/0.64 under a matched definition is a legitimate and verifiable advance over that specific benchmark.

The more consequential concurrent context is the authors' own research program. SleepFM (Thapa et al., *Nature Medicine*, January 2026) established the phenome-wide-prediction-from-a-frozen-physiological-foundation-model template this manuscript follows, achieving C-index ≥0.75 for 130 conditions from a single night of polysomnography with the identical senior-author team. Separately, Ricciardiello Mejia et al. (medRxiv, July 2026), also co-authored by Brink-Kjaer, applies UK Biobank accelerometry specifically to Parkinson's disease via an RBD-classifier route. The present manuscript's distinguishing claim — that a general-purpose, disease-agnostic embedding outperforms a bespoke single-disease pipeline — is scientifically interesting and is the paper's strongest argument for standalone significance, but reviewers should require the authors to state explicitly how the three papers' Parkinson's disease claims relate to one another and whether population overlap exists. Also directly relevant and not cited is Steinfeldt et al. (*Nature Communications* 2025), whose externally validated (All of Us) phenome-wide neural-network framework represents the standard against which this manuscript's lack of external validation should be judged.

### 7. Suggested Reviewers' Names

For self-supervised wearable representation learning: **Hang Yuan** (first author, self-supervised HAR foundation model on 700,000 UK Biobank person-days, *npj Digital Medicine* 2024) or **Shing Chan** (co-first author, same work), both at Oxford and independent of the submitting group.

For phenome-wide survival modeling and external validation methodology: **Jakob Steinfeldt** (Charité Berlin / University College London; lead author, phenome-wide neural-network disease-onset prediction with All of Us external validation, *Nature Communications* 2025), independent of the submitting group and directly positioned to assess the external-validation gap.

For prodromal Parkinson's disease and digital biomarkers: **Ann-Kathrin Schalkamp** (University of California, San Francisco; first author of the principal comparator study, *Nature Medicine* 2023), independent of the submitting group and uniquely positioned to adjudicate the novelty claim against her own benchmark.

---

## Further Literature (Past 3 Years)

1. **Schalkamp, A.-K., Peall, K. J., Harrison, N. A. & Sandor, C.** Wearable movement-tracking data identify Parkinson's disease years before clinical diagnosis. *Nature Medicine* 29, 2048–2056 (2023). DOI: 10.1038/s41591-023-02440-2. Peer-reviewed. Cited by manuscript (ref. 8). Author group independent of submitting authors. Relevance: the direct predecessor benchmark for the manuscript's flagship Parkinson's claim (AUPRC 0.07 prodromal / 0.14 diagnosed); the manuscript's improvement to 0.18/0.64 under a matched definition should be independently checked against this paper's exact case definitions and follow-up window.

2. **Yuan, H., Chan, S., Creagh, A. P., Tong, C., Acquah, A., Clifton, D. A. & Doherty, A.** Self-supervised learning for human activity recognition using 700,000 person-days of wearable data. *npj Digital Medicine* 7, 91 (2024). DOI: 10.1038/s41746-024-01062-3. Peer-reviewed. Cited by manuscript (ref. 14). Independent group (Oxford). Relevance: this is the pretraining paradigm and, per the manuscript's Methods, effectively the lineage of the Human Activity (HA) encoder underlying the daytime-movement channel; reviewers should confirm the manuscript's HA model is a genuine architectural advance (frequency-aware masked autoencoding) over this baseline rather than a re-implementation.

3. **Steinfeldt, J., Wild, B., Buergel, T. et al.** Medical history predicts phenome-wide disease onset and enables the rapid response to emerging health threats. *Nature Communications* 16, 585 (2025). DOI: 10.1038/s41467-025-55879-x. Peer-reviewed. **Not cited by manuscript.** Independent group (Charité Berlin / UCL). Relevance: the closest methodological analogue outside accelerometry — a single neural network predicting onset across 1,741 diseases from passive data (medical history), externally validated in All of Us. This is the paper reviewers should invoke when assessing whether the present manuscript's absence of external validation is acceptable at this journal's standard.

4. **Thapa, R., Kjaer, M. R., He, B., Covert, I., Moore IV, H., Hanif, U., Ganjoo, G., Westover, M. B., Jennum, P., Brink-Kjaer, A., Mignot, E. & Zou, J.** A multimodal sleep foundation model for disease prediction. *Nature Medicine* 32, 752–762 (2026). DOI: 10.1038/s41591-025-04133-4. Peer-reviewed. Cited by manuscript (ref. 18). **Not independent** — shares all four senior/corresponding authors (Jennum, Brink-Kjaer, Mignot, Zou) with the submitted manuscript. Relevance: establishes the phenome-wide, frozen-foundation-model-plus-Cox-head template this manuscript applies to a new modality; the SHARC concept's novelty relative to any analogous shared-variance structure in SleepFM must be adjudicated by reviewers.

5. **Ricciardiello Mejia, G., Brink-Kjaer, A., Liu, L., Zhou, L., Gunter, K., Ryu, K. H., Wickramaratne, S., Parekh, A., Gan-Or, Z. & During, E.** Accelerometry-derived REM sleep behavior disorder predicts future Parkinson's disease in the UK Biobank. *medRxiv* (2026), preprint. **Not peer-reviewed** — flag explicitly as unreviewed. Cited by manuscript (ref. 10). **Not independent** — shares co-senior author Andreas Brink-Kjaer. Relevance: near-concurrent, same-cohort, same-outcome (incident Parkinson's disease from UK Biobank accelerometry) work; central to the Editorial Integrity Alert regarding cohort overlap and priority.

6. **Zhao, A., Cui, E., Leroux, A., Zhou, X., Muschelli, J., Lindquist, M. A. & Crainiceanu, C. M.** Objectively measured physical activity using wrist-worn accelerometers as a predictor of incident Alzheimer's disease in the UK Biobank. *The Journals of Gerontology, Series A* 80(2), glae287 (2025). Peer-reviewed. Cited by manuscript (ref. 11). Independent group (Johns Hopkins). Relevance: the direct comparator the manuscript uses for its Alzheimer's disease claim (C 0.85 vs. 0.68); reviewers should verify the case-definition and follow-up-window comparability underlying this stated advantage.

7. **Smits Serena, R., Hirschmann, M. T., Matziolis, G., von Eisenhart-Rothe, R., Rueckert, D., Hinterwimmer, F. & Valle, C.** Deep learning of wrist accelerometry from UK Biobank data identifies early movement signatures of knee osteoarthritis up to 5 years before diagnosis. *Knee Surgery, Sports Traumatology, Arthroscopy* 34(4), 1524–1533 (2026). Peer-reviewed. Cited by manuscript (ref. 12). Independent group. Relevance: another single-disease, bespoke-signature UK Biobank accelerometry study; useful for reviewers benchmarking whether the manuscript's general-purpose embedding genuinely subsumes disease-specific engineering of this kind for musculoskeletal outcomes, a category where the manuscript's own results are comparatively weak (mean AUROC 0.672, Supplementary Table 2).

8. **Brooks, T. G., Lahens, N. F., Grant, G. R., Sheline, Y. I., FitzGerald, G. A. & Skarke, C.** Diurnal rhythms of wrist temperature are associated with future disease risk in the UK Biobank. *Nature Communications* 14, 5172 (2023). Peer-reviewed. Cited by manuscript (ref. 6). Independent group (University of Pennsylvania). Relevance: establishes that a single derived wrist signal (temperature rhythmicity) carries broad future-disease information, a precedent directly supporting the manuscript's premise that accelerometry-derived signal is not confined to a handful of prespecified summaries.

9. **Wang, Y., Wen, Q., Luo, S., Tang, L., Zhan, S., Cao, J., Wang, S. & Chen, Q.** Phenome-wide analysis of diseases in relation to objectively measured sleep traits and comparison with subjective sleep traits in 88,461 adults. *Health Data Science* 5, 0161 (2025). Peer-reviewed. Cited by manuscript (ref. 7). Independent group. Relevance: a phenome-wide framing applied specifically to sleep traits rather than full accelerometry embeddings; useful comparator for evaluating whether the manuscript's AcceleRest-derived night-time channel adds information beyond conventional sleep phenotyping.

10. **Ruan, F. Y., Zhang, A., Oh, J. Y., Jin, S. & Jacobson, N. C.** A foundation model for wearable movement data in mental health research. *IEEE Journal of Biomedical and Health Informatics* (2026); preprint arXiv:2411.15240. Peer-review status mixed — arXiv preprint with journal publication as cited by the manuscript; independent confirmation of final journal acceptance recommended. Cited by manuscript (ref. 17). Independent group (Dartmouth). Relevance: the Pretrained Actigraphy Transformer (PAT) is the nearest architectural competitor to this manuscript's frozen-encoder approach, trained on NHANES rather than UK Biobank; a head-to-head comparison of PAT versus the manuscript's dual-encoder embedding on a shared outcome would materially strengthen the novelty case and is a fair question for reviewers to raise.

061903
# Editorial Report

**Manuscript:** "A self-auditing AI framework for structured data extraction in evidence synthesis from observational studies"
**Authors:** Sumsuzzman, Shi, Bawden, Galvani, Sharma, Moghadas

---

## 1. Overall Assessment

A three-module GPT-4o pipeline (inventory, schema-constrained extraction, coverage-triggered repair) reports 87.1% accuracy and F1 92.9% on 13,952 elements from 100 observational studies. The engineering is careful, but the manuscript's central claim — a "self-auditing" framework producing "trustworthy" machine-readable evidence — rests on a completeness check that is not independent of the model it checks: the same GPT-4o instance builds the inventory and audits extraction against it. That is not a caveat-able limitation; it invalidates the paper's defining claim as written.

## 2. Strengths

The ablation is well executed and the prospective, protocol-registered design (CRD420251032836) is sound methodology. The finding that hallucination accounts for only 12.0% of discrepancies against ~50% for omission is a genuine, useful observation. Neither substitutes for an independent verification mechanism, which the framework does not have.

## 3. Weaknesses

Circular self-audit is fatal as designed: nothing distinguishes "the model verified completeness" from "the model agreed with itself," and the ablation's collapse without Module 3 only confirms how much of the headline result rests on this unverified mechanism. Under the framework's own audit, participant age still lands at 27.0% accuracy — the audit does not rescue the variable it exists to protect. "Foundational architecture" claims rest on one model, one cross-sectional topic, and tabular-only reporting, with no evidence of generalization past this narrow slice. Time-to-completion methodology folds prompt-development time into the reported 7.3-minute median against a 62.0-minute human baseline, inflating the comparison further.

## 4. Editorial Decision

**Reject.** The self-audit's lack of independence is a fundamental design flaw, not a revision item: fixing it requires a different verification architecture, and the paper's central claim does not survive without it. Suggested transfer: npj Digital Medicine, better suited to methods-stage AI pipeline work than this journal's bar for demonstrated clinical significance. Counterargument: same-model self-verification is common practice in this literature, so a reviewer could treat the circularity as a field-wide limitation rather than grounds for rejection — but that leniency elsewhere doesn't establish that this framework's own defining claim survives its own test.

## 5. Suggested Reviewer Expertise

Schema-constrained and provenance-linked structured extraction from unstructured biomedical text; self-verification and retrieval-audit architectures for generative AI pipelines (as distinct from human-in-the-loop verification models); systematic review and meta-analysis methodology, specifically data-extraction quality assessment in Cochrane-aligned frameworks; cluster-based statistical inference for correlated diagnostic-accuracy data; and COVID-19 vaccine hesitancy or health-behavior epidemiology in observational/cross-sectional designs.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has split into two competing paradigms for AI-assisted extraction: human-in-the-loop verification, where a reviewer checks each field (shown by 2025 work to lift accuracy from roughly 62% to over 70%), and autonomous self-verification, the category this manuscript occupies. Gartlehner and colleagues' "From promise to practice" (BMJ Evid Based Med, 2025) remains the field's most-cited methodological critique of LLM extraction evaluation and is appropriately engaged by the authors. Chen et al. (Nat Med, 2026) used an LLM to audit the clinical-LLM evidence base itself — a useful methodological cousin illustrating that LLM-auditing-LLM designs are an active, unresolved concern across the field, not one specific to this manuscript. Most directly competing is Mortezaagha et al., "From chaos to clarity" (BMC Med Res Methodol, 2026), a schema-constrained, sentence-provenance extraction pipeline for full-text biomedical PDFs (DOAC-measurement literature) that explicitly declines to build an automated completeness-audit loop, deferring blinded comparative benchmarking to future work. This manuscript's ablation-validated repair loop is a real advance over that concurrent design, but the manuscript neither cites this line of work nor tests whether the field's other dominant paradigm — cheaper human-verified single-pass extraction — would match its 92.9% F1. That comparison, not another single-model ablation, is the most damaging missing benchmark.

## 7. Suggested Reviewer Names

**Technical:** Pouria Mortezaagha (University of Ottawa; lead author of the concurrent schema-constrained, provenance-linked extraction pipeline above — best positioned to assess the novelty gap directly). Qiao Jin (National Library of Medicine, NIH; co-author of TrialMind, npj Digital Medicine 2025, on LLM-assisted evidence synthesis and screening). Lena Schmidt (University of Bristol / EPPI-Centre; GPT-4 feasibility study for SR data extraction, arXiv 2405.14445, and active in Cochrane's AI-in-evidence-synthesis methods work).

**Clinical/epidemiological:** Michael J. Deml (University of Geneva; determinants of COVID-19 vaccine hesitancy, scoping-review methodology, independent of the submitting group).

## Further Literature

1. Mortezaagha P, Shaw J, Sun B, Rahgozar A. From chaos to clarity: schema-constrained AI for auditable biomedical evidence extraction from full-text PDFs. *BMC Med Res Methodol*. 2026;26:119. DOI: 10.1186/s12874-026-02847-8. Peer-reviewed. Not cited by the manuscript. Author group independent of submitting authors. Directly overlapping scope: a schema-constrained, evidence-provenance extraction pipeline for full-text biomedical PDFs; explicitly declines to build an automated completeness-audit/repair loop and defers blinded comparative benchmarking to future work — the sharpest concurrent novelty gap for this manuscript.

2. Khan MA, Ayub U, Ahmed Naqvi SA, et al. Collaborative large language models for automated data extraction in living systematic reviews. *J Am Med Inform Assoc*. 2025;32(4):638–647. DOI: 10.1093/jamia/ocae325. Peer-reviewed. Not cited by the manuscript. Author group (Mayo Clinic/ASU) independent of submitting authors. Uses dual-LLM cross-critique as a self-verification mechanism, an alternative architecture to this manuscript's same-model inventory-and-audit design; directly relevant to the independence critique in Section 3.

3. Wang Z, Cao L, Danek B, Jin Q, Lu Z, Sun J. Accelerating clinical evidence synthesis with large language models. *npj Digit Med*. 2025;8:509. DOI: 10.1038/s41746-025-01840-7. Peer-reviewed. Not cited by the manuscript. Author group (UIUC/NLM) independent of submitting authors. TrialMind pipeline benchmarks LLM-only extraction against human-AI collaborative extraction on 100 systematic reviews; provides the missing comparator (human-verified vs. autonomous) this manuscript's discussion lacks.

4. Gartlehner G, Kahwati L, Nussbaumer-Streit B, Crotty K, Hilscher R, Kugley S, Viswanathan M, Thomas I, Konet A, Booth G, Chew R. From promise to practice: challenges and pitfalls in the evaluation of large language models for data extraction in evidence synthesis. *BMJ Evid Based Med*. 2025;30(6):385–389. DOI: 10.1136/bmjebm-2024-113199. Peer-reviewed. **Cited by the manuscript (ref. 20).** Independent authorship. Field's leading methodological critique of LLM-extraction evaluation design, including reference-standard construction and metric choice — directly bears on this manuscript's own evaluation framework.

5. Chen SF, Alyakin A, Seas A, et al. LLM-assisted systematic review of large language models in clinical medicine. *Nat Med*. 2026;32:1152–1159. DOI: 10.1038/s41591-026-04229-5. Peer-reviewed. **Cited by the manuscript (ref. 6).** Independent authorship. Uses an LLM to audit the clinical-LLM evidence base itself, a methodological cousin illustrating that LLM-auditing-LLM designs are an unresolved, field-wide concern rather than one specific to this manuscript.

6. Gartlehner G, Kahwati L, Hilscher R, et al. Data extraction for evidence synthesis using a large language model: a proof-of-concept study. *Res Synth Methods*. 2024;15(4):576–589. DOI: 10.1002/jrsm.1710. Peer-reviewed. **Cited by the manuscript (ref. 11).** Independent authorship. Earlier single-pass extraction proof-of-concept against which this manuscript's self-auditing architecture should be positioned as an explicit successor design, which the current text does not do explicitly.

7. Peng Z, Wu X, Qin Z, Doi SA, Furuya-Kanamori L, Hong Y, Lin L, Chu H, Xu C, Liu M. Accuracy of large language models in data extraction from randomized controlled trials in sleep medicine: a proof-of-concept study. *Sleep Med Rev*. 2025;84:102192. DOI: 10.1016/j.smrv.2025.102192. Peer-reviewed. Not cited by the manuscript. Independent authorship. Multi-model comparison (GPT-4o vs. Claude 3.5) absent from this manuscript, which evaluates only one frontier model despite claiming model-agnostic generalizability.

8. Hasan B, Saadi S, Rajjoub NS, et al. Integrating large language models in systematic reviews: a framework and case study using ROBINS-I for risk of bias assessment. *BMJ Evid Based Med*. 2024;29:394–398. DOI: 10.1136/bmjebm-2023-112597. Peer-reviewed. Not cited by the manuscript. Independent authorship. ROBINS-I is the standard risk-of-bias tool for non-randomized/observational studies specifically; directly relevant to this manuscript's observational-study focus and absent from its discussion of downstream synthesis use.

9. Sercombe J, Bryant Z, Wilson J. Evaluating a customized version of ChatGPT for systematic review data extraction in health research: development and usability study. *JMIR Form Res*. 2025;9:e68666. DOI: 10.2196/68666. Peer-reviewed. Not cited by the manuscript. Independent authorship. Usability-focused evaluation of a customized (non-agentic) GPT extraction tool; relevant comparator for the practical deployment claims in this manuscript's discussion.

10. Schmidt L, Hair K, Graziosi S, et al. Exploring the use of a Large Language Model for data extraction in systematic reviews: a rapid feasibility study. arXiv:2405.14445 (2024; revised 2025). **Unreviewed preprint — flagged accordingly.** Not cited by the manuscript. Independent authorship (University of Bristol/EPPI-Centre). Early GPT-4 feasibility study across human, animal, and social-science domains proposing an evaluation template subsequently used across the field; useful for benchmarking this manuscript's evaluation design against an established template, but not peer-reviewed and should be weighted accordingly.

061892
# Editorial Report
**Manuscript:** Diagnostic Accuracy of LLMs and 2,114 Clinicians on a Multilingual ICD-11 Psychiatric Benchmark
**Corresponding Authors:** Malgaroli, Schultebraucks

---

## 1. Overall Assessment

The manuscript benchmarks ten LLMs against 2,114 clinicians from three WHO ICD-11 field studies (anxiety, mood, stress-related disorders; six languages). Claude-Opus-4.6 and Gemini-2.5-Pro significantly exceed clinician accuracy (88.37%, 86.05% vs. 65.11%); seven models are non-inferior. The stated contribution is the first multilingual, clinician-validated ICD-11 diagnostic benchmark for LLMs — but this repackages an established LLM-vs-clinician paradigm, and the multilingual claims rest on vignette counts too small to bear their weight.

## 2. Strengths

The reference standard is unusually strong: 2,114 clinicians across 155 countries (WHO Global Clinical Practice Network) on vignettes validated through peer-reviewed ICD-11 field trials (Keeley 2016, Kogan 2021, Rebello 2020) — far larger than comparable efforts (e.g., Raballo et al. 2025, two vignettes). Statistical rigor exceeds field norms: non-inferiority testing (δ=0.1) with Holm correction, a contamination check, and a paraphrasing ablation, rarely reported together. Seven open-weights models (7B–70B+) alongside three proprietary models, HIPAA-compliantly deployed, enable a genuine scale-vs-training dissociation.

## 3. Weaknesses

The manuscript fails to cite or differentiate itself from directly competing, clinician-benchmarked diagnostic-accuracy studies predating submission (Li et al. 2024; Raballo et al. 2025; Wang et al. 2026, *Nat Mach Intell*); the "first" claim must be earned against this cluster. The multilingual claims are statistically fragile — anxiety vignettes cover six languages with only 11 items, so language-specific accuracies (e.g., 72.73% Chinese) are single-digit numerators, yet the Discussion reads signal into noise. A sampling asymmetry is unaddressed: clinicians rated two vignettes each, LLMs ran all 43 deterministically, with no discussion of the effect on non-inferiority. Reproducibility is incomplete: benchmark and clinician labels remain unreleased.

## 4. Editorial Decision

**Send for Review.** These issues are addressable through revision, not fabrication or a fatal design flaw. Reviewers should adjudicate whether per-language vignette counts support the multilingual claims as written, and whether the clinician-sampling asymmetry affects the reported non-inferiority margins.

## 5. Suggested Reviewer Expertise

Multilingual LLM evaluation methodology, particularly bias from small or imbalanced per-language test sets; non-inferiority and paired statistical testing for diagnostic-accuracy comparisons; prompt-sensitivity and contamination ablation design; and, clinically, WHO ICD-11 field-trial methodology and transcultural psychiatric assessment across mood, anxiety, and stress-related disorders.

## 6. State-of-the-Art Literature Review (Past 3 Years)

LLM-vs-clinician diagnostic benchmarking has moved from small multiple-choice comparisons (Li et al. 2024) to structured vignette studies without predefined options (Raballo et al. 2025) and to domain-adapted, clinically deployed models with clinician-benchmarked evaluation (PsychFound/PsychBench, 2026, *Nat Mach Intell*). Multilingual coverage remains the frontier but is addressed unevenly: LingxiDiagBench (Xu et al. 2026) is Chinese-only, built on synthetic dialogues rather than clinician-scored vignettes; PsychiatryBench (Fouda et al. 2026, *npj Digit Med*) is textbook-grounded but English-only. This manuscript sits at the genuine intersection of scale, multilinguality, and clinician grounding, but must be positioned against this cluster, not presented as occupying an empty field.

## 7. Suggested Reviewer Names

**Andrea Raballo** (Università della Svizzera Italiana / Cantonal Sociopsychiatric Organisation, Ticino) — co-author, LLMs-vs-leading-psychiatrists schizophrenia benchmark; clinical/comparator-design expertise. **Federico Ravenda** (Informatics, USI) — technical lead on the same study. **Mohammed E. Fouda** (Compumacy AI Solutions) — corresponding author, PsychiatryBench; benchmark-construction expertise. All independent of the submitting group.

---

## Further Literature (Past 3 Years)

1. **Li DJ, Kao YC, Tsai SJ, et al.** Comparing the performance of ChatGPT GPT-4, Bard, and Llama-2 in the Taiwan psychiatric licensing examination and in differential diagnosis with multi-center psychiatrists. *Psychiatry Clin Neurosci.* 2024;78(6):347–352. DOI: 10.1111/pcn.13656. Peer-reviewed. **Not cited** by manuscript. Independent of submitting group. Relevance: the founding LLM-vs-multicenter-psychiatrist diagnostic-accuracy design this manuscript's paradigm extends but never engages.

2. **Urkin B, Parnas J, Raballo A, Koren D.** Schizophrenia spectrum disorders: an empirical benchmark study of real-world diagnostic accuracy and reliability among leading international psychiatrists. *Schizophr Bull Open.* 2024;5:sgae012. DOI: 10.1093/schizbullopen/sgae012. Peer-reviewed. **Not cited.** Independent. Relevance: establishes the clinician-only vignette-benchmark methodology (no predefined diagnostic options) later extended to LLMs by entry 3.

3. **Raballo A, Ravenda F, Mira A.** Diagnosing schizophrenia spectrum disorders: large language models (LLMs) vs. leading international psychiatrists (LIPs). *Psychiatry Clin Neurosci.* 2025;79(9):599–600. DOI: 10.1111/pcn.13864. Peer-reviewed (correspondence). **Not cited.** Independent. Relevance: directly overlapping open- and closed-source LLM-vs-psychiatrist comparison on unstructured (non-multiple-choice) vignettes.

4. **Wang R, Liu S, Zhang L, et al.** A domain-adapted large language model to support clinicians in psychiatric clinical practice. *Nat Mach Intell.* 2026;8:690–707. DOI: 10.1038/s42256-026-01224-w. Peer-reviewed. **Not cited.** Independent. Relevance: PsychFound/PsychBench — psychiatry-specialized LLM benchmarked against clinicians across five clinical tasks including diagnosis, in a directly comparable top-tier venue.

5. **Dennstädt F, Hastings J, Putora PM, et al.** Benchmarking large language models against practicing clinicians on psychopathological assessment. *npj Digit Med.* 2026. DOI: 10.1038/s41746-026-02852-7. Peer-reviewed. **Not cited** (likely postdates submission). Independent. Relevance: closest contemporaneous design — 10 LLMs vs. 108 clinicians against an expert-consensus reference standard, including GPT-5.1/Gemini-3-Pro-Preview.

6. **Fouda AE, Hassan AA, Hanafy RJ, Fouda ME.** PsychiatryBench: a multi-task benchmark for LLMs in psychiatry. *npj Digit Med.* 2026;9:320. DOI: 10.1038/s41746-026-02582-w. Peer-reviewed. **Cited** by manuscript (ref. 23). Independent. Relevance: closest-scope existing benchmark; manuscript distinguishes it as English-only but does not otherwise engage its task design.

7. **Shan G, Chen X, Wang C, Liu L, Gu Y, Jiang H, Shi T.** Comparing diagnostic accuracy of clinical professionals and large language models: systematic review and meta-analysis. *JMIR Med Inform.* 2025;13:e64963. DOI: 10.2196/64963. Peer-reviewed. **Not cited.** Independent. Relevance: cross-specialty meta-analysis of 30 LLM-vs-clinician diagnostic-accuracy studies (2023–2025); a reference-class baseline for the effect sizes and risk-of-bias norms this manuscript's design should be judged against.

8. **Levkovich I.** Evaluating diagnostic accuracy and treatment efficacy in mental health: a comparative analysis of large language model tools and mental health professionals. *Eur J Investig Health Psychol Educ.* 2025;15(1):9. DOI: 10.3390/ejihpe15010009. Peer-reviewed. **Not cited** (this specific paper; related co-authored work by the same author is cited at refs. 19–21). Independent of submitting group. Relevance: LLM-vs-mental-health-professional diagnostic accuracy across depression, schizophrenia, PTSD, social phobia vignettes.

9. **Sun M, Yu J, Long Z, Yang Y, Xiao T, Liang J, Feng J, Deng H, Huang G.** Large language models for psychiatric diagnosis based on multicenter real-world clinical records: comparative study. *JMIR Med Inform.* 2026;14:e77699. DOI: 10.2196/77699. Peer-reviewed. **Not cited.** Independent. Relevance: LLM diagnostic accuracy against physician-confirmed discharge diagnoses across 9,923 real-world EHRs from six centers — complements this manuscript's vignette-based design with a real-clinical-record comparator.

10. **Xu S, Zhou T, Ma J, et al.** LingxiDiagBench: a multi-agent framework for benchmarking LLMs in Chinese psychiatric consultation and diagnosis. *arXiv:2602.09379* (2026). **Preprint — not peer-reviewed; flagged accordingly.** Independent (Shanda Group / Evermind Lingxi team). Relevance: the only other identified multilingual (non-English), clinician-verified-label psychiatric diagnostic benchmark, bearing directly on this manuscript's multilingual novelty claim, though limited to a single non-English language and not yet peer-reviewed.

061886
# Editorial Report
**Manuscript:** "Reimagining Clinical Trials in the Era of Generative AI: Toward Lifecycle-Integrated, Agentic Systems"
**Authors:** Lian, Xin, Mishra-Kalyani, Yuan, Meric-Bernstam, Parikh, Sallée, Vonderheide, Long
**Article type as submitted:** Comment / Perspective (no primary data, no implementation)

**Editorial Integrity Alert (handling editor only):** None identified. No evidence of fabrication, undisclosed prior publication, or citation misattribution. The manuscript's self-citation of ref. 20 (Parikh et al., co-author) is accurately represented against the source finding.

---

## 1. Overall Assessment

The authors argue AI tools for clinical trials are siloed and imitation-trained on historical protocols, proposing a multi-agent "copilot" — an orchestrator coordinating evidence, design, statistical, regulatory, conduct, and analysis agents — as remedy. This is conceptual only: no prototype, implementation, or evaluation metric anywhere. Its novelty is undercut by EmulatRx (Li et al., *Nat Commun* 2026, ref. 23), an orchestrator-coordinated five-agent system already built and validated on real EHR data, cited only in one subordinate clause.

## 2. Strengths

Table 1's gap-to-cause mapping names concrete deficits (BEACON design tooling, EHR interoperability), not generic "AI limitations." The operational detail — basket-trial cohort churn, dynamic arm replacement, competitive enrollment — reflects real domain expertise rarely captured in benchmark-driven AI papers. The critique is empirically anchored: the authors' own RCT (ref. 20) showing no efficiency gain from AI-assisted prescreening is reported honestly, not assumed away. Regulatory grounding in named, current FDA guidance (refs. 14–15) is specific and verified accurate.

## 3. Weaknesses

No implementation exists; Figure 2 is a labeled diagram with no accuracy, efficiency, or safety metric. Decisively, the claimed gap is largely already closed by cited work: EmulatRx, AERO (ref. 24), and ClinicalReTrial (ref. 25) already implement orchestrated, adaptive agentic systems, engaged only as passing examples, not competing precedent for the manuscript's own Figure 2. No failure-mode or override mechanism is specified for an agent influencing statistical design. Table 1 attributes all gaps to "AI development philosophy," ignoring regulatory/liability caution as a competing, persistent explanation.

## 4. Editorial Decision

**Reject** from *Nature Communications*; transfer to **npj Digital Medicine**. Absence of implementation fails the reproducibility bar, and the architecture is insufficiently differentiated from EmulatRx, AERO, and ClinicalReTrial, already in the authors' own reference list. Counterargument: *Nature Communications* does run non-data Comments (the authors' own ref. 1), so this could read as agenda-setting synthesis, making the EmulatRx overlap corroborating, not disqualifying. That doesn't survive the manuscript presenting the architecture as original rather than a response to that prior art.

## 5. Suggested Reviewer Expertise

Reviewers should cover: multi-agent LLM orchestration for structured biomedical workflows, including shared-state and tool-augmented agent architectures; Bayesian and adaptive (BEACON) clinical trial design methodology, including operating-characteristic calibration and platform/master protocol design; clinical trial eligibility formalization and patient-trial matching NLP, including EHR-to-protocol interoperability; and regulatory science for AI/ML-based clinical trial decision-support tools, including FDA guidance interpretation. One clinical reviewer should have direct experience in academic oncology trial operations, particularly basket or multi-arm platform trial conduct, to assess the manuscript's operational claims.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved decisively from single-task AI tools toward orchestrated multi-agent systems in the past eighteen months. EmulatRx (Li et al., *Nat Commun* 2026) is the most directly relevant advance: a five-agent, orchestrator-coordinated framework producing target trial protocols and causal-effect estimates from EHR data (MIMIC-IV, INSIGHT Network), with an open implementation. AERO (medRxiv, 2026) and ClinicalReTrial (arXiv, 2026) extend this toward self-evolving, adaptive eligibility and protocol optimization. On the matching side, TrialGPT-lineage work (Jin et al., *Nat Commun* 2024, ref. 5) and Panacea (Lin et al., arXiv 2024, ref. 3) established foundation-model approaches to trial search, summarization, and recruitment, while Gupta et al.'s PRISM (*npj Digital Medicine* 2024, ref. 4) proposed tiered eligibility frameworks distinguishing strict from flexible criteria — directly relevant to the manuscript's own claim that eligibility coverage requirements remain unclear.

Against this landscape, the manuscript's contribution is organizational rather than technical: its distinct value is the explicit mapping of gaps to causes (Table 1) and the naming of operational failure modes (basket-trial cohort churn, competitive enrollment) that empirical papers tend not to surface. But its central architectural claim — an orchestrator coordinating specialized agents over shared structured trial state — is not new relative to EmulatRx, published in the same journal weeks earlier. The manuscript would be substantially stronger, and more honest about the state of the field, if it engaged EmulatRx, AERO, and ClinicalReTrial as the directly competing implementations they are rather than as passing citations.

## 7. Suggested Reviewer Names

**Multi-agent orchestration / agentic clinical trial systems:** Haoyang Li (Weill Cornell Medicine, postdoctoral researcher, co-first author of EmulatRx — directly competing orchestrator-agent architecture, independent of submitting institutions); Weishen Pan (Weill Cornell Medicine, postdoctoral researcher, co-first author of EmulatRx, same relevance).

**Patient-trial matching / clinical NLP:** Qiao Jin (National Library of Medicine, NIH, postdoctoral fellow, first author of the *Nat Commun* 2024 LLM patient-trial matching study cited as ref. 5).

**Bayesian / adaptive (BEACON) trial design:** Lorenzo Trippa (Dana-Farber Cancer Institute / Harvard, Associate Professor of Biostatistics, designer of Bayesian adaptive platform trials including GBM AGILE and INSIGhT). Last-resort senior alternative: Yuan Ji (University of Chicago, Professor of Biostatistics, author of a 2026 practical analysis of FDA's Bayesian methodology draft guidance).

**Regulatory science:** Sara Gerke (Penn State Dickinson Law, Associate Professor, health-AI regulatory scholarship, independent of FDA and of the submitting authors' institutions).

---

## Further Literature (Past 3 Years, Closely Overlapping Scope)

1. **Li, H., Pan, W., Rajendran, S., Zang, C. & Wang, F.** "Empowering clinical trial design with agentic intelligence and real-world data." *Nature Communications* 17, 5501 (2026). DOI: 10.1038/s41467-026-74501-2. **Peer-reviewed.** **Cited by manuscript (ref. 23), but only in passing.** Independent (Weill Cornell Medicine). Relevance: implements the exact architecture the manuscript proposes conceptually — a "Supervisor" orchestrator coordinating Trialist, Informatician, Statistician, and Clinician agents over a shared trial representation, with tool-augmented reasoning and empirical validation on MIMIC-IV and INSIGHT Network EHR data. This is the single most important omission in the manuscript's positioning.

2. **Loaiza-Bonilla, A., Kurnaz, S., Tuysuz, E., Huner, O., Giritlioglu, D. & Noel Meza, J.P.** "Transforming oncology clinical trial matching through neuro-symbolic, multi-agent AI and an oncology-specific knowledge graph: a prospective evaluation in 3804 patients." *ESMO Real World Data and Digital Oncology* 12, 100706 (2026). DOI: 10.1016/j.esmorw.2026.100706. **Peer-reviewed.** **Not cited by manuscript.** Independent (Massive Bio, industry). Relevance: knowledge-graph-grounded multi-agent reasoning validated prospectively at scale (n=3,804), directly bearing on the manuscript's open question of what eligibility coverage is "necessary for meaningful operational benefit."

3. **Kim, H., Kim, M., Kim, S. & You, S.C.** "From study design to executable code: automating target trial emulation with large language models." *JAMIA Open* 9(4), ooag131 (2026). DOI: 10.1093/jamiaopen/ooag131. **Peer-reviewed.** **Not cited by manuscript.** Independent (Ajou University, South Korea). Relevance: LLM agent converts study design directly into executable analysis code — a working instance of the manuscript's own design principle that agents should communicate through "machine-interpretable intermediate outputs" rather than free text.

4. **Wang, Y., Li, Y., Lin, T. et al.** "An operational target trial emulation framework for causal inference using electronic health record data." *npj Digital Medicine* 9, 424 (2026). DOI: 10.1038/s41746-026-02563-z. **Peer-reviewed.** **Not cited by manuscript.** Independence not fully verifiable from available metadata; no indication of overlap with submitting authors. Relevance: operationalizes exactly the evidence-synthesis-from-real-world-data function assigned to the manuscript's proposed "evidence agent."

5. **Landman, R., Emir, B., Zhang, R. et al.** "Leveraging generative AI to transform statistical analysis plan authoring in clinical trials." *Clinical Trials* (2026). DOI: 10.1177/17407745261422365. **Peer-reviewed.** **Not cited by manuscript.** Independent (industry-affiliated, non-overlapping with submitting institutions). Relevance: directly implements the "Statistical Analysis Plan Agent" the manuscript places in its Protocol Drafting stage (Fig. 2) as an unrealized capability.

6. **Shin, E., Bhat, A.G. & Ramanathan, M.** "Large Language Models for Clinical Trial Protocol Assessments." *Clinical Pharmacology & Therapeutics* (2025). DOI: 10.1002/cpt.70096. **Peer-reviewed.** **Not cited by manuscript.** Independent (University at Buffalo). Relevance: LLM-based review of SAP and PK-PD plan compliance against FDA E9 guidance — a working prototype of the manuscript's "regulatory agent" concept.

7. **Wornow, M., Lozano, A., Dash, D. et al.** "Zero-shot clinical trial patient matching with LLMs." *NEJM AI* 2(1), AIcs2400360 (2025). DOI: 10.1056/AIcs2400360. **Peer-reviewed.** **Not cited by manuscript.** Independent (Stanford). Relevance: directly undercuts the manuscript's claim (Section 3) that matching tools "require weeks to months of training, fine-tuning, and validation for each new study protocol" — a zero-shot alternative the manuscript should have engaged.

8. **Paulson, J.N. et al.; Subbiah, V., senior author.** "A unified framework for pre-screening and screening tools in oncology clinical trials." *npj Precision Oncology* 10, 1 (2026). DOI: 10.1038/s41698-026-01306-3. **Peer-reviewed.** **Not cited by manuscript.** Author independence: Subbiah left MD Anderson (co-author Ying Yuan's institution) in 2023 for Sarah Cannon Research Institute, moving to Stanford Cancer Institute in 2026; no current institutional overlap with submitting authors. Relevance: proposes a workflow-integration framework for trial screening tools, bearing directly on the manuscript's Section 3 critique of poor real-world workflow fit.

9. **Li, X., James, J., Pellikka, P. & Zong, N.** "AERO: An AI Agent for Adaptive Eligibility Refinement and Optimization of Clinical Trial Criteria in Real-World Trial Emulation." *medRxiv* 2026.04.30.26352142 (2026). **Preprint — not peer-reviewed; flagged as unreviewed.** **Cited by manuscript (ref. 24), but only in passing.** Independence not verifiable from available metadata. Relevance: self-contained agentic eligibility-refinement system, directly competing with the manuscript's proposed design agent.

10. **Xing, S. et al.** "ClinicalReTrial: A Self-Evolving AI Agent for Clinical Trial Protocol Optimization." *arXiv* 2601.00290 (2026). **Preprint — not peer-reviewed; flagged as unreviewed.** **Cited by manuscript (ref. 25), but only in passing.** Independence not verifiable from available metadata. Relevance: self-evolving protocol-optimization agent reported to improve 83.3% of tested protocols — an existing, if unreviewed, instance of the "adaptive decision rules" capability the manuscript frames as missing.

061807
# Editorial Report

**Manuscript:** "A hierarchical memory architecture overcomes context limits in long-horizon multi-agent computational modeling"
**Authors:** Shivendra G. Tewari, Holly Kimko (AstraZeneca, Systems Medicine, Clinical Pharmacology & Safety Sciences)

---

## Editorial Integrity Alert (Handling Editor Only)

The manuscript states that "no existing LLM agent framework supports such workflows autonomously" and claims, in the Discussion, to be "the first system combining autonomous scientific implementation, cross-session hierarchical memory, and domain-expert grounding." Independent verification found three closely relevant, published, uncited systems that bear directly on this claim: QSP-Copilot (Saini & Farnoud, *CPT: Pharmacometrics & Systems Pharmacology*, 2025), a multi-agent LLM platform built specifically for QSP model development and described by its own authors as "the first end-to-end AI-augmented solution" in this space; The Virtual Lab (Swanson et al., *Nature*, 2025), a PI-agent-orchestrated team of specialist sub-agents for open-ended biomedical research, architecturally close to the PI/sub-agent hierarchy presented here; and MemGPT (Packer et al., 2023), the originating work on OS-inspired hierarchical/paged memory management for LLM context, which frames the identical problem this manuscript presents as its central innovation. Notably, the Acknowledgments thank James Zou — senior author of the Virtual Lab paper — for "valuable feedback on the manuscript." The handling editor should weigh whether the omission of this specific prior art is inadvertent or reflects awareness of directly competing work. Separately, the manuscript is simultaneously posted to arXiv (2607.07666); the arXiv abstract's headline figures (301-token median, 4,050 max, 104 runs) match the submission with no detected inconsistency.

---

## 1. Overall Assessment

Ensemble QSP presents a multi-agent LLM system with a three-layer hierarchical memory for autonomous, multi-session QSP modeling under a PI agent and five specialists. The engineering is careful, but its "first"/novelty claims are contradicted by uncited, closely competing prior work (QSP-Copilot, Virtual Lab, MemGPT), and the reported ablation never isolates the memory mechanism the title foregrounds.

---

## 2. Strengths

Cost/token accounting (Table 1) is rigorous and candid, showing a low-cost writer's per-token price advantage eroded to roughly 2-fold overall by a 5.5-fold rise in self-correction tokens.

The system autonomously caught and corrected a mass-conservation error in the published Shah and Betts (2012) mAb PBPK parameter table, recovering the correct FcRn-mediated half-life.

Adversarial literature-extraction trap cases (unretrievable PMID, off-domain papers) were correctly declined rather than hallucinated, and an intentionally incorrect PMID was correctly diagnosed.

---

## 3. Weaknesses

The novelty claim is contradicted by uncited, directly competing work: QSP-Copilot occupies the same niche with the same "first" claim; the Virtual Lab already demonstrates the same PI-plus-specialist architecture; MemGPT originated hierarchical LLM memory. This undercuts the "no existing framework" language throughout.

The ablation (Fig. 3c) never removes the memory hierarchy against a flat-history baseline, so the title's causal claim is asserted, not demonstrated.

Comparisons are single-replicate on small synthetic benchmarks (n=8–20) with no confidence intervals, yet results are called "statistically indistinguishable" without a formal test.

The sole comparator, GitHub Copilot, received nine human-assisted iterations versus zero for the MAS, and its edge on the easier subset is explained away post hoc rather than controlled for.

---

## 4. Editorial Decision

**Reject**, transfer to *npj Artificial Intelligence*. No patient-level validation places this outside this venue's clinical-significance bar; independently, the novelty and mechanism claims are unsupported given the uncited competing work and incomplete ablation. Counterargument: engineering rigor is above the norm, and Major Revision could be justified if authors reframe the contribution, benchmark against QSP-Copilot, and add a flat-history ablation — but if that shows no advantage over simple truncation, the mechanism claim collapses and Reject stands.

---

## 5. Suggested Reviewer Expertise

Reviewers should include: LLM agent memory and context-management architectures, specifically hierarchical or OS-paging-style systems, to assess whether the memory design is genuinely differentiated from MemGPT-derived approaches; multi-agent orchestration for autonomous scientific workflows, to evaluate the PI/specialist-agent hierarchy against comparable systems such as the Virtual Lab; QSP/PBPK-PD mechanistic modeling and stiff-ODE parameter identifiability, to judge the technical soundness of the model-selection and parameter-recovery benchmarks; and translational pharmacometrics for GLP-1 receptor agonist or monoclonal-antibody drug-development programs, to assess the clinical plausibility and generalizability of the two case studies.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant landscape has moved quickly. MemGPT (Packer et al., 2023) established OS-inspired hierarchical memory paging for LLM agents; Generative Agents (Park et al., 2023) established memory-stream-plus-reflection architectures for long-horizon agent behavior. Building on these, 2025 saw a wave of PI-agent-orchestrated scientific systems: The Virtual Lab (Swanson et al., *Nature*, 2025) used a PI agent directing specialist sub-agents to design experimentally validated SARS-CoV-2 nanobodies; Google's AI co-scientist (Gottweis et al., 2025) applied a similar multi-agent structure to hypothesis generation; and, most directly, QSP-Copilot (Saini & Farnoud, *CPT: Pharmacometrics & Systems Pharmacology*, 2025) applied a multi-agent LLM architecture specifically to QSP model development, reporting roughly 40% workflow time reduction. A December 2025 system, GRASP (Bazgir et al.), further encodes QSP models as typed knowledge graphs validated by multi-agent mass-balance checks — directly overlapping with this manuscript's physics-checklist approach. Against this landscape, Ensemble QSP's genuine contribution is the quantitative characterization of bounded context growth across a real multi-month project (median 301 tokens across 104 runs) and transparent cost accounting absent from the above systems; its memory pattern and PI/specialist hierarchy, however, largely replicate architecture already established by MemGPT and the Virtual Lab, and its central use case is directly anticipated by QSP-Copilot, which the manuscript does not engage.

---

## 7. Suggested Reviewer Names

For memory-architecture and multi-agent-orchestration expertise, Kyle Swanson (Stanford University), lead author of the Virtual Lab paper describing a PI-agent-orchestrated specialist team for autonomous biomedical research, is well positioned to assess architectural novelty; his group is independent of AstraZeneca. For QSP-specific multi-agent systems, Anuraag Saini and Ali Farnoud (Boehringer Ingelheim), authors of QSP-Copilot, the directly competing multi-agent QSP platform, would be able to assess the manuscript's claims of priority and differentiation; both are at a pharmaceutical company independent of AstraZeneca. For translational pharmacometrics of GLP-1 receptor agonists, Rolien Bosch (Erasmus MC, with LAP&P Consultants), first author of the 2024 extension of the same Hall body-composition model to GLP-1RA effects on body weight, is directly qualified to evaluate the clinical plausibility of the manuscript's semaglutide/liraglutide/dulaglutide fits; this group is independent of the submitting authors.

---

## Further Literature (Past 3 Years, Closely Overlapping Scope)

1. Packer, C., Fang, V., Patil, S.G., Lin, K., Wooders, S., Gonzalez, J.E. "MemGPT: Towards LLMs as Operating Systems." arXiv:2310.08560 (2023). DOI: 10.48550/arXiv.2310.08560. Peer-review status: arXiv preprint only, unreviewed. Cited by manuscript: No. Author independence: Independent (UC Berkeley / Letta). Relevance: originates the OS-inspired hierarchical/paged memory management for LLM context that this manuscript presents as its core architectural contribution; the manuscript's three-layer capped-and-evicted design is a direct domain-specific instantiation of this mechanism.

2. Park, J.S., O'Brien, J.C., Cai, C.J., Morris, M.R., Liang, P., Bernstein, M.S. "Generative Agents: Interactive Simulacra of Human Behavior." *UIST 2023*, 1–22. DOI: 10.1145/3586183.3606763. Peer-review status: peer-reviewed (ACM). Cited by manuscript: No. Author independence: Independent (Stanford/Google/DeepMind). Relevance: establishes memory-stream-plus-reflection as a mechanism for long-horizon agent memory, the foundational alternative design point against which the manuscript's capped-JSON approach should be benchmarked.

3. Swanson, K., Wu, W., Bulaong, N.L., Pak, J.E., Zou, J. "The Virtual Lab of AI agents designs new SARS-CoV-2 nanobodies." *Nature* 646, 716–723 (2025). DOI: 10.1038/s41586-025-09442-9. Peer-review status: peer-reviewed. Cited by manuscript: No. Author independence: Independent (Stanford); note the senior author is thanked in the manuscript's Acknowledgments. Relevance: directly analogous PI-agent-plus-specialist-team architecture applied to autonomous, experimentally validated biomedical research; the closest architectural precedent for this manuscript's PI/five-specialist hierarchy.

4. Saini, A., Farnoud, A. "QSP-Copilot: An AI-Augmented Platform for Accelerating Quantitative Systems Pharmacology Model Development." *CPT Pharmacometrics Syst Pharmacol* 14, 1775–1786 (2025). DOI: 10.1002/psp4.70127. Peer-review status: peer-reviewed. Cited by manuscript: No. Author independence: Independent (Boehringer Ingelheim). Relevance: the most directly competing prior system — a multi-agent LLM platform built specifically for QSP model development, with its own short/long-term memory design and an explicit "first end-to-end" claim that this manuscript's priority language does not engage.

5. Bazgir, O. et al. "GRASP: Graph Reasoning Agents for Systems Pharmacology with Human-in-the-Loop." arXiv:2512.05502 (2025); presented at the NeurIPS 2025 AI4D3 workshop. Peer-review status: workshop-reviewed (lighter than journal review). Cited by manuscript: No. Author independence: Independent (Genentech). Relevance: multi-agent QSP model construction enforcing mass-balance and unit constraints via typed knowledge graphs, methodologically overlapping with the manuscript's physics-checklist domain-grounding approach, including an independently derived mass-balance audit mechanism.

6. Gottweis, J. et al. "Towards an AI co-scientist." arXiv:2502.18864 (2025). Peer-review status: arXiv preprint only, unreviewed. Cited by manuscript: No. Author independence: Independent (Google DeepMind). Relevance: multi-agent hypothesis-generation system with a supervisor-agent structure for open-ended scientific research, relevant prior art for the manuscript's PI-agent delegation and synthesis design.

7. Ghareeb, A.E. et al. "Robin: A multi-agent system for automating scientific discovery." arXiv:2505.13400 (2025). Peer-review status: arXiv preprint only, unreviewed. Cited by manuscript: No. Author independence: Independent (FutureHouse). Relevance: end-to-end multi-agent system spanning literature synthesis, hypothesis generation, and experimental design, directly comparable in scope to the manuscript's literature-pipeline and autonomous-modeling benchmarks.

8. Sun, M., Zhang, Y., Meng, G. "Constraint-Aware Corrective Memory for Language-Based Drug Discovery Agents." arXiv:2604.09308 (2026). Peer-review status: arXiv preprint only, unreviewed. Cited by manuscript: No. Author independence: Independent (Chinese Academy of Sciences). Relevance: organizes agent memory into static, dynamic, and corrective channels for a pharmaceutical R&D task, a directly comparable memory-compression design in the same application domain (drug development) that the manuscript does not benchmark against.

9. Bosch, R., Snelder, N., Sijbrands, E.J.G., et al. "Quantification of the effect of GLP-1R agonists on body weight using in vitro efficacy information: An extension of the Hall body composition model." *CPT Pharmacometrics Syst Pharmacol* 13, 1488–1502 (2024). DOI: 10.1002/psp4.13183. Peer-review status: peer-reviewed. Cited by manuscript: No. Author independence: Independent (Erasmus MC / LAP&P). Relevance: extends the identical Hall body-composition model used in the manuscript's GLP-1RA case study to incorporate drug-specific effects, offering a direct, peer-reviewed comparator for the manuscript's own semaglutide/liraglutide extension and its parameter estimates.

10. Villaescusa-Navarro, F. et al. "The Denario project: Deep knowledge AI agents for scientific discovery." arXiv:2510.26887 (2025). Peer-review status: arXiv preprint only, unreviewed. Cited by manuscript: No. Author independence: Independent (multi-institution astrophysics/biology consortium). Relevance: modular multi-agent system spanning idea generation, literature validation, execution, and manuscript drafting across scientific disciplines, comparable in end-to-end scope to the manuscript's autonomous, multi-session workflow and useful as a generalizability benchmark beyond pharmacometrics.

061079
# Editorial Report: BEGINN: BSPM-EGM Inference using Neural Networks for Non-Invasive Atrial Signal Reconstruction in Regular Rhythms

---

## Editorial Integrity Alert (Handling Editor Only)

Two items require resolution before this manuscript proceeds to external review.

First, reference 26 (Gutiérrez-Fernández et al., *Frontiers in Physiology*, 2026), cited as "the most recent and methodologically comparable deep learning approach" with CC = 0.37–0.42, shares three co-authors (Fambuena-Santos, Guillem, Climent) with the submitted manuscript and originates from the same institute (ITACA, Universitat Politècnica de València). The verified figures are accurate, but the manuscript frames this as an independent external benchmark without disclosing the authorship overlap. This is a disclosure issue, not fabrication, and is resolvable by revision.

Second, the simulation database's 42 atrial/torso geometries used to build the training statistical shape model and the clinical validation cohort's 42 patients are described using identical language and count. The manuscript does not clarify whether these are the same or a disjoint population. If the clinical cohort contributed to or overlaps with the SSM training geometries, this constitutes an undisclosed train–test relationship (indirect, via anatomy rather than raw signal) that would need explicit resolution — potentially reverting the decision toward rejection. Authors must clarify this in any revision.

---

## 1. Overall Assessment

BEGINN is a geometry-free 3D CNN–LSTM autoencoder reconstructing atrial electrograms from body surface potentials, targeting classical Tikhonov ECGI's two core weaknesses: over-smoothing and geometric sensitivity. Trained on 16,800 simulations from 42 anatomies, it is validated in silico and in a 60-recording, 42-patient, three-hospital clinical cohort.

The in silico case is strong: BEGINN is invariant to a geometric perturbation that collapses classical ECGI's correlation from 0.73 to 0.42. But the clinical validation, which should carry the paper, shows non-inferiority, not superiority — McNemar's test found no significant localization difference (cavity 88.3% vs. 93.3%, p = 0.55; neighboring 85% vs. 88.3%, p = 0.79), with classical ECGI numerically ahead on both. The superiority narrative instead rests on unvalidated secondary morphology metrics.

---

## 2. Strengths

The training design is disciplined: leakage-free 28/7/7 geometry splits and clinically grounded positional-perturbation ranges (±20 mm, ±20°/±15°). The multicenter clinical validation — 60 pacing recordings, 42 patients, three hospitals, blinded scoring, McNemar's test — is genuinely rare for this sub-field; competing geometry-free deep learning ECGI work remains simulation-only or single-center. The authors are commendably explicit that regional pacing accuracy confirms only labeled activation origin, not full propagation-pattern fidelity, given no invasive electroanatomical ground truth. Electrode-dropout training targets a real deployment failure mode — contact loss, high-impedance leads — rather than an idealized full-vest scenario.

---

## 3. Weaknesses

The primary clinical endpoint does not support the superiority claim: cavity and neighboring accuracy showed no significant difference, with classical ECGI numerically higher on both. The pivot to focality area and maximum slope as evidence is unvalidated against an independent substrate reference, and the Monte Carlo dropout uncertainty described in Methods — the tool that could substantiate this — is never reported in Results. Whether the 42 SSM training anatomies overlap with the 42 clinical validation patients is unclarified (see Integrity Alert). Engagement with the directly competing, concurrent geometry-free diffusion approach (Jara & Meyers, 2026) is superficial, and no external hospital was held out for site-level generalizability.

---

## 4. Editorial Decision

**Major Revision.** The architecture and clinical validation effort are genuine, and no fabrication is evident, but the superiority narrative is unsupported by its own primary endpoint, and the disclosure gaps above must be resolved first. If the geometry/patient overlap proves to be genuine contamination, the decision reverts to Reject.

**Counterargument:** Geometric robustness by design may itself be the clinically relevant contribution, independent of an underpowered (n = 60) localization comparison — a fair point that favors revision over rejection, provided the manuscript is honest about what the clinical data does and does not show.

---

## 5. Suggested Reviewer Expertise

Reviewers should be drawn primarily from technical backgrounds, with clinical expertise calibrated to persistent AF ablation. Needed technical expertise: deep learning architectures for the inverse problem of electrocardiography, specifically geometry-free and generative (diffusion, variational) approaches to BSPM-to-electrogram mapping; boundary element method forward modeling and Tikhonov/L-curve regularization as applied to atrial ECGI, sufficient to assess whether the classical comparator was optimally tuned; statistical shape modeling of cardiac and torso anatomy and its role in quantifying geometric uncertainty; and Bayesian or noise-robust local activation time estimation methodology. Clinical expertise should cover catheter ablation of persistent atrial fibrillation with specific experience in non-pulmonary-vein trigger and driver-guided ablation, ideally including prior use of ECGI or panoramic mapping systems to select ablation targets.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

Geometry-free deep learning ECGI has moved from a theoretical possibility to an active, competitive sub-field within the past several months. Gutiérrez-Fernández et al. (2026) proposed a dual-branch variational autoencoder for atrial electrogram estimation trained on 680 simulated BSPM–EGM pairs spanning sinus rhythm, multirotor AF, ectopic foci, and fibrotic substrates, reporting correlation coefficients of 0.37–0.42 for AF and 0.42–0.66 for sinus rhythm against zero-order Tikhonov — a smaller and more heterogeneous training set than BEGINN's, but notably including irregular rhythms and fibrotic substrate that BEGINN's regular-rhythm-only training database does not cover. Independently, Jara and Meyers (arXiv, January 2026) introduced a geometry-free conditional diffusion model for the same inverse problem, evaluated against CNN, LSTM, and transformer baselines on real ECGI data, with the explicit advantage of probabilistic multi-sample reconstruction rather than a single deterministic estimate. In the ventricular domain, Wang et al. (2025, *Artificial Intelligence in Medicine*) used a Pix2Pix architecture with a cosine-similarity loss for heart-surface potential reconstruction during ventricular pacing, and He et al. (2025) reported correlation coefficients exceeding 0.90 using an attention-based network under known geometry, while Pilia et al. (2023) demonstrated that ventricular localization error rises from under 3 mm to 32–47 mm once patient-specific geometry is removed — the same domain gap BEGINN targets in the atrial setting.

Against this landscape, BEGINN's genuine advance is the first multicenter, pacing-validated clinical demonstration that a geometry-free deep learning atrial ECGI model can match classical ECGI's regional localization accuracy while remaining structurally immune to geometric mismatch. It does not, however, address irregular or fibrotic rhythms as the VAE work does, nor does it exploit uncertainty quantification as the concurrent diffusion approach does, and the manuscript would benefit from directly engaging both as competing rather than merely adjacent directions.

---

## 7. Suggested Reviewers' Names

**Technical expertise:**
- Steffen Schuler (Karlsruhe Institute of Technology) — spatio-temporal basis methods for atrial ectopic ECGI localization; author of the noise-robustness benchmark (7.9 mm at 0 dB) directly cited in this manuscript.
- Adam Meyers (Assistant Professor, University of Miami) — geometry-free conditional diffusion modeling for the inverse ECG problem; directly competing, independent architecture.
- Jaume Coll-Font (Massachusetts General Hospital / Harvard Medical School) — geometric uncertainty and cardiac position sensitivity in ECGI forward/inverse modeling.

**Clinical expertise:**
- Shohreh Honarbakhsh (Consultant Electrophysiologist, Barts Health NHS Trust) — ECGI-guided driver ablation in persistent AF; principal investigator, TARGET-AF1 trial.
- Ghassen Cheniti (Bordeaux University Hospital, LIRYC Institute) — non-invasive mapping and electrocardiographic imaging in atrial and ventricular arrhythmia ablation.

---

## Further Literature (Past 3 Years)

1. **Li, L., Camps, J., Rodriguez, B. & Grau, V.** Solving the Inverse Problem of Electrocardiography for Cardiac Digital Twins: A Survey. *IEEE Reviews in Biomedical Engineering* 18, 316–336 (2025). DOI: 10.1109/RBME.2024.3486439. Peer-reviewed. Not cited by manuscript. Independent (Oxford). Comprehensive recent survey spanning physics-based and deep learning ECGI inverse methods, including graph-based and hybrid architectures; situates BEGINN's specific architectural choices against the full current landscape it otherwise cites only piecemeal.

2. **Jiang, X. et al.** Hybrid Neural State-Space Modeling for Supervised and Unsupervised Electrocardiographic Imaging. *IEEE Transactions on Medical Imaging* (2024). PMID: 38478452. Peer-reviewed. Not cited. Independent. Combines a physics-based forward operator with a learned neural transition function, including unsupervised validation on in-vivo data without EGM ground truth — directly relevant to BEGINN's own acknowledged inability to validate reconstructed propagation fidelity against invasive mapping.

3. **Li, L., Camps, J., Wang, Z.J., Beetz, M., Banerjee, A., Rodriguez, B. & Grau, V.** Toward Enabling Cardiac Digital Twins of Myocardial Infarction Using Deep Computational Models for Inverse Inference. *IEEE Transactions on Medical Imaging* 43, 2466–2478 (2024). DOI: 10.1109/TMI.2024.3367409. Peer-reviewed. Not cited. Independent. Ventricular/substrate-focused analog of BEGINN's atrial trigger-localization goal; offers a template for linking reconstructed fields to substrate characterization, a step BEGINN defers to future work.

4. **Wang, T., Karel, J.M.H., Bonizzi, P. & Peeters, R.L.M.** Influence of the Tikhonov Regularization Parameter on the Accuracy of the Inverse Problem in Electrocardiography. *Sensors* 23(4), 1841 (2023). Peer-reviewed. Not cited. Independent (Maastricht). Directly examines sensitivity of L-curve-selected Tikhonov regularization — the exact method used for BEGINN's classical ECGI comparator — relevant to whether that baseline was optimally tuned.

5. **Yadan, Z., Jian, L., Jian, W., Yifu, L., Haiying, L. & Hairui, L.** An Expert Review of the Inverse Problem in Electrocardiographic Imaging for the Non-Invasive Identification of Atrial Fibrillation Drivers. *Computer Methods and Programs in Biomedicine* 240, 107676 (2023). Peer-reviewed. Not cited. Independent. Recent expert review focused specifically on AF-driver ECGI; situates BEGINN's regular-rhythm-only scope against the irregular-rhythm AF driver problem it explicitly defers.

6. **Gutiérrez-Fernández, M., López-Linares, K., Fambuena-Santos, C., Guillem, M.S., Climent, A.M. & Barquero-Pérez, Ó.** Deep Learning for Atrial Electrogram Estimation: Toward Non-Invasive Arrhythmia Mapping Using Variational Autoencoders. *Frontiers in Physiology* 16, 1720244 (2026). DOI: 10.3389/fphys.2025.1720244. Peer-reviewed. **Cited by manuscript (ref 26).** **Not independent** — shares three co-authors with the submission (see Integrity Alert). Dual-branch VAE trained on 680 pairs covering sinus, multirotor AF, ectopic foci, and fibrotic substrate — broader rhythm coverage than BEGINN's regular-rhythm-only database, on a smaller dataset.

7. **Valdes Jara, R. & Meyers, A.** Geometry-Free Conditional Diffusion Modeling for Solving the Inverse Electrocardiography Problem. arXiv:2601.18615 (2026). **Preprint, not peer-reviewed.** Cited by manuscript (ref 19), but only briefly. Independent (University of Miami). The most direct architectural competitor: geometry-free, evaluated on real ECGI data against CNN/LSTM/transformer baselines, with native probabilistic uncertainty quantification that BEGINN's MC-dropout output could have been benchmarked against but was not.

8. **Wang, T. et al.** Deep Learning Based Estimation of Heart Surface Potentials. *Artificial Intelligence in Medicine* 163, 103093 (2025). Peer-reviewed. Cited by manuscript (ref 21). Independent (Maastricht). Pix2Pix-based ventricular surface-potential reconstruction (CC ≈ 0.64); useful cross-chamber benchmark for BEGINN's atrial correlation figures.

9. **He, S. et al.** AI-Powered Noninvasive Electrocardiographic Imaging Using the Priori-to-Attention Network (P2AN) for Wearable Health Monitoring. *Sensors* 25, 1810 (2025). Peer-reviewed. Cited by manuscript (ref 32). Independent. Reports CC > 0.90 under known ventricular geometry, illustrating the accuracy ceiling geometry-aware methods can reach and the trade-off BEGINN accepts by discarding geometry.

10. **Pilia, N. et al.** Non-Invasive Localization of the Ventricular Excitation Origin Without Patient-Specific Geometries Using Deep Learning. *Artificial Intelligence in Medicine* 143, 102619 (2023). Peer-reviewed. Cited by manuscript (ref 33). Independent (KIT). Documents the same geometry-dependency domain gap BEGINN targets (localization error rising from <3 mm to 32–47 mm without patient geometry), but in the ventricle; the closest direct precedent for BEGINN's core "geometry-free by design" argument.
