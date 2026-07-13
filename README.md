# Trackrad202512456

027608
## Editorial Integrity Alert — for Handling Editor

Three issues independent verification surfaced, none raised by the three reviewers:

**Undisclosed prior preprint.** The manuscript is publicly available on bioRxiv (doi: 10.64898/2026.01.04.697552, posted 4 Jan 2026), under the identical title and author list. Nothing in the submission or the response letter discloses this. The preprint is the pre-revision version — it lacks the MFAHGN/GraphormerDTI baselines, the Orphanet rare-disease benchmark, and the significance testing added in response to review — so the two versions are not identical, but this needs disclosure and reconciliation, not silent omission.

**Uncorrected internal data error.** The Results and the bioRxiv preprint both state PrimeKG comprises "129,375 nodes... connected by over four million edges." The Methods section of *this same revised manuscript* states PrimeKG contains "over 129 million nodes... more than 8 million edges." This 1000x discrepancy was present in the original preprint and survived an entire revision cycle uncorrected.

**Reference regression.** The response letter's own reference list cites TxGNN (Huang et al.) as an unpublished medRxiv preprint ("ahead of print, August 7"). TxGNN has been peer-reviewed and published in *Nature Medicine* 30, 3601–3613 (2024) since September 2024 — well before this resubmission. The original bioRxiv version of this manuscript cited it correctly; the revision reverted to the wrong citation.

None of these is individually disqualifying, but together they indicate the authors' revision pass was not carefully proofread against its own numbers, which bears on how much confidence to place in the numerical claims addressed below.

## Did the revision address the reviewers?

**Reviewer #1** — Partially. Baselines (TxGNN, MFAHGN, GraphormerDTI), leakage-aware splits, Ray Tune hyperparameter search, and additional metrics were genuinely added — that's real work, not deflection. The novelty rebuttal, however, only contrasts NetMedGPT against message-passing GNNs; it never engages the more proximal precedent — random-walk-to-embedding methods (node2vec, DREAMwalk) that already use KG random walks for drug repurposing, differing from NetMedGPT mainly in swapping skip-gram for a transformer MLM objective. That comparison is the one a sophisticated reviewer would actually want, and it's absent. The specific trivial-subnetwork failure case reviewer #1 flagged (osteogenesis imperfecta–bosentan) was never re-run and shown fixed — only disclaimed and the interface expanded.

**Reviewer #2** — Mostly yes, with one loose thread. The softmax-dilution response (background/top-100/ground-truth analysis, Cohen's d) is rigorous. But the new rare-disease benchmark (Orphanet, n=811) reports AUPRC of 0.98–0.99 for indication/contraindication/off-label — *higher* than the general zero-shot split (0.95/0.84) it was meant to stress-test further. Rare, sparsely-annotated diseases outperforming well-annotated ones on a harder zero-shot task is not a validated finding, it's an unflagged anomaly, and it directly undercuts the paper's headline translational claim.

**Reviewer #3** — Yes on the mechanical asks (terminology purge, statistical tests, MLP-head clarification). The pathway-flow-bias and degree-centrality concerns got argued rather than tested — acceptable as a design-philosophy defense, but reviewers should not accept "we didn't test it because we didn't want to" without at least a partial ablation.

---

## Editorial Report

**1. Overall Assessment**

NetMedGPT reframes biomedical knowledge-graph reasoning as masked-sequence modeling: random walks over PrimeKG become "pseudo-sentences," and a BERT-style encoder learns to recover masked nodes/edges, yielding one model serving five drug-discovery tasks without task-specific retraining. The revision substantially strengthened the empirical case — TxGNN, MFAHGN, and GraphormerDTI as baselines, zero-shot/disease-area/rare-disease/external (Every Cure, ClinicalTrials.gov) validation, and paired significance testing. The unresolved problem is that the rare-disease benchmark — the paper's central translational pitch — outperforms the general zero-shot setting, an unexplained and biologically implausible result the authors did not flag. Combined with an uncorrected 1000x node-count error and a reference-list regression, confidence in the revision's diligence is limited.

**2. Strengths**

The generalist framing is genuine: one encoder, trained once, serves indication, contraindication, off-label, ADR, and DTI prediction via prompt reformatting, evaluated against task-specific GNN and transformer baselines (RGCN, HAN, HGT, TxGNN, MFAHGN, GraphormerDTI) rather than strawmen.

External validation against Every Cure's expert-curated indications and ClinicalTrials.gov drug-disease pairs is a meaningfully higher bar than internal PrimeKG holdouts, and the model separates KG-supported from clinical-trial-only from random associations as intended.

The KG-noise curation (removing drug-drug edges, filtering promiscuous glucocorticoid-like drugs, PubMedBERT-based ADR/indication disambiguation) reflects real domain engineering, not just modeling.

**3. Weaknesses**

The rare-disease AUPRC (0.98–0.99) exceeding the general zero-shot AUPRC (0.95/0.84) is unaddressed and suspicious — sparser data should degrade, not improve, zero-shot performance; this needs an explicit leakage audit of the Orphanet split before the result can be trusted.

Novelty is argued only against GNN message-passing, never against the closer random-walk/sequence-embedding lineage (DREAMwalk, node2vec-based repurposing models), leaving the field-positioning claim incomplete.

Interpretability remains weak in practice: reviewer #1's specific trivial two-node subnetwork example was never re-demonstrated as fixed, only reframed as "hypothesis generation" and covered by a broader disclaimer.

Statistical tests are one-sided paired t-tests chosen post hoc for a directional hypothesis the authors already believed — not disqualifying, but a more conservative two-sided test with the same effect sizes should be reported.

**4. Editorial Decision**

**Send for Review**, conditional on reviewers explicitly adjudicating: (a) whether the Orphanet rare-disease result reflects a genuine capability or a leakage artifact in test construction; (b) whether the novelty claim survives direct comparison to DREAMwalk/node2vec-style random-walk embedding methods, not just GNNs; (c) authors must correct the 129-million-node error and the TxGNN citation before external review proceeds. This is not a structural rejection — the evaluation breadth is real — but the unexplained anomaly is a live correctness question, not a style preference.

**5. Suggested Reviewer Expertise**

Transformer-based masked sequence modeling applied to graph-structured/relational data; random-walk and skip-gram knowledge-graph embedding methods for drug repurposing (node2vec/DREAMwalk lineage); zero-shot and leakage-aware evaluation design for biomedical link prediction; heterogeneous GNN baselines (RGCN/HAN/HGT) for fair-comparison auditing; clinical pharmacology with rare-disease and off-label repurposing experience to assess the Orphanet benchmark's clinical plausibility.

**6. State-of-the-Art Literature Review (Past 3 Years)**

TxGNN (Huang et al., *Nat. Med.* 2024) established the zero-shot drug-repurposing benchmark this paper directly extends, using metric learning rather than sequence modeling. DREAMwalk (Bang et al., *Nat. Commun.* 2023) is the closest structural precedent — semantic-guided random walks over drug/disease ontologies feeding a skip-gram embedding — and is conspicuously not engaged as a novelty comparator despite being more analogous to NetMedGPT's pipeline than any GNN baseline. MFAHGN (Fang et al., *Neurocomputing* 2026) and GraphormerDTI (Gao et al., *Comput. Biol. Med.* 2024) are current task-specific state-of-the-art for ADR and DTI prediction respectively, both correctly cited and fairly retrained here. The field's open problem — generalizing zero-shot repurposing to genuinely undertreated rare diseases without inflating performance via test-set artifacts — is exactly where this manuscript's most interesting claim currently fails scrutiny.

**7. Suggested Reviewers' Names**

Sequence/transformer-KG modeling: Kexin Huang (TxGNN); Payal Chandak (PrimeKG). Random-walk embedding methods: Dabin Bang (DREAMwalk). Graph-transformer DTI baselines: Daokun Zhang (GraphormerDTI). Clinical/translational rare-disease repurposing: an Every-Cure-independent clinical pharmacologist or rare-disease genomics specialist should be sourced by the handling editor, since no unaffiliated junior clinical name surfaced independently of this manuscript's own collaborators.

052292
# Editorial Report
**Manuscript:** Predicting the timing of first sustained cognitive worsening in Alzheimer's disease using real-world clinical data and machine learning
**Authors:** Venkatesh, Zhang, et al. (Xia and Hou, co-senior)

---

## 1. Overall Assessment

The manuscript applies LATTE, a semi-supervised deep neural phenotyping algorithm previously published for heart failure, diabetes, and multiple sclerosis (Wen et al., *Patterns*, 2024), to a new outcome: time-to-first sustained cognitive worsening in 27,614 AD patients from UPMC EHR data, using MCID-based CDR/MMSE/MoCA thresholds. Small gold-standard cohorts (n=632–752) train each model; predictions scale to imputation cohorts exceeding 26,000 patients. The scalability claim rests on extrapolating from a healthier, younger training subpopulation to a sicker deployment cohort, corrected only by prevalence recalibration, with no external validation.

## 2. Strengths

The outcome definition is clinically disciplined: MCID-based, severity-stratified thresholds sustained over two consecutive visits within three years, modeled on CLARITY AD and TRAILBLAZER-ALZ 2 endpoints, reduce misclassification of test-retest noise as true decline.

Evaluation is thorough: four longitudinal metrics, cross-validated thresholds, and sensitivity analyses by severity and data source, honestly disclosing that EHR-derived scores show higher AUC but worse calibration than ADRC-derived scores.

The clinical-utility checks add value: APOE-ε4 carriers and k-means EHR clusters both show differential predicted time-to-worsening in the expected direction, anchoring outputs beyond internal accuracy metrics.

## 3. Weaknesses

No algorithmic novelty: LATTE's architecture is unchanged from Wen et al. 2024, whose authors overlap with this manuscript's senior authors; the contribution is a new outcome definition, not a new method.

Gold-standard and imputation cohorts differ systematically in age and mortality; only prevalence recalibration is applied, with no correction for covariate shift, despite this being central to the scalability claim.

External validation is absent; all data are single-site, and LATTE's cited portability was shown for other diseases, not this one.

The k-means validation is partly circular, built from the same features seeding the model's inputs; the authors also concede CDR Global's apparent superiority may reflect scale coarseness, not model advantage.

## 4. Editorial Decision

**Reject**, transfer to *npj Digital Medicine*. Absent external validation and unaddressed covariate shift are structural, non-revisable limitations of this single-site design, and the contribution applies a published algorithm rather than advancing one.

## 5. Suggested Reviewer Expertise

Reviewers should include expertise in semi-supervised and weakly supervised deep learning for longitudinal EHR event-timing phenotyping, including attention-based recurrent architectures and knowledge-graph-derived concept embeddings; survival and competing-risk modeling for chronic neurodegenerative disease trajectories; assessment of calibration and domain/covariate shift across heterogeneous EHR cohorts; and, clinically, behavioral neurology or dementia specialists with expertise in CDR/MMSE/MoCA-based endpoint definitions, MCID methodology, and APOE-stratified AD registry data (e.g., NACC/ADRC).

## 6. State-of-the-Art Literature Review (Past 3 Years)

The closest methodological precedent is LATTE itself (Wen et al., *Patterns*, 2024), which this manuscript directly reuses. Competing approaches to EHR-based AD/ADRD prediction over the past three years favor transformer/foundation-model architectures: an EHR-BERT-based transformer pretrained on NYU Langone records predicts incident MCI/ADRD 12–36 months ahead (Zhu et al., 2025), and TA-RNN, an attention-based time-aware recurrent network, predicts AD progression from ADNI longitudinal data (Al Olaimat & Bozdag, *Bioinformatics*, 2024). Both target incident diagnosis or short-horizon conversion rather than sustained post-diagnosis cognitive worsening, so this manuscript's outcome framing is comparatively novel even though its architecture is not; the authors do not benchmark against or discuss this competing transformer-based paradigm. On the endpoint side, Ito and Hutmacher (*J Alzheimers Dis*, 2014) modeled time-to-clinically-worsening from longitudinal CDR-SB in a trial-quality MCI cohort, anticipating this manuscript's core framing by a decade in cleaner data; the manuscript does not cite this precedent. The MCID thresholds underlying the outcome definition come from an active and contested literature, including a 2024 rapid review (Muir et al., *Alzheimer's & Dementia*) and a published methodological critique disputing anchor-based MCID estimates used in that review; the manuscript treats its thresholds as settled rather than engaging this controversy.

---

## Suggested Reviewers

1. **Narges Razavian, PhD** — Assistant Professor, Population Health and Radiology, NYU Grossman School of Medicine. Directly comparable work: transformer-based EHR foundation model predicting MCI/ADRD onset (Zhu et al., 2025).
2. **Serdar Bozdag, PhD** — Associate Professor, Computer Science and Engineering, University of North Texas. Directly comparable work: TA-RNN, attention-based time-aware recurrent network for longitudinal AD progression prediction (Al Olaimat & Bozdag, *Bioinformatics*, 2024).
3. **Suzanne E. Schindler, MD, PhD** — Associate Professor of Neurology, Washington University in St. Louis. Clinical expertise in CDR-SB-based outcome measures, ADRC registry data, and AD biomarker-cognition correlation.

052939
# Editorial Report
**Manuscript:** Associations of 3D abdominal MRI-derived composite and organ-specific aging with disease, mortality and lifestyle
**Authors:** Wang, Deng, Wang, Attia, et al.; corresponding: Yang, Li (Cedars-Sinai)
**Journal:** Nature Communications (Digital Health)

---

## EDITORIAL INTEGRITY ALERT — TO HANDLING EDITOR

Independent prior-art search identifies a medRxiv preprint by the same corresponding authors (Yufeng Wang, Debiao Li, Ju Dong Yang; Biomedical Imaging Research Institute, Cedars-Sinai), posted 12 May 2026 under the title "MRI reveals the hierarchical organization of abdominal biological aging from shared burden to disease-specific organ engagement" (doi: 10.64898/2026.05.08.26352767). It reports the identical UK Biobank Application (132578), the same eight-compartment MedNeXt pipeline, the same Overall Aging Gap (OAG) construct, and the same leave-one-out axis-conditional Cox design. This preprint is not disclosed anywhere in the submitted manuscript.

More serious than the non-disclosure itself is that the two documents report materially different numbers from what should be the same underlying extraction: healthy training cohort N = 7,469 (submitted) vs N = 7,715 (preprint); analytical cohort N = 58,110 vs N = 56,525; prospective cohort N = 16,892 vs N = 20,266; mean inter-compartment correlation r = 0.408 vs r = 0.423; FDR-significant prevalent diseases 190/430 vs 271/430. The preprint also contains a PDFF-based training-cohort exclusion criterion, a second mortality cohort (N = 40,985), cross-modal biomarker phenotyping, and anatomical negative controls that do not appear in the submission. These are not rounding-level discrepancies; they indicate the two circulating outputs came from different cohort-derivation or exclusion pipelines applied to the same data, with no reconciliation offered anywhere. The handling editor should request from the authors, before any review assignment: (1) confirmation of which pipeline is the frozen, pre-registered analysis; (2) an explanation for the divergent cohort sizes and effect estimates; and (3) a corrected disclosure statement covering the preprint. This is a data-provenance question that external reviewers cannot be expected to adjudicate without that clarification.

---

## 1. Overall Assessment

Eight MedNeXt models on 67,130 UK Biobank abdominal MRIs produce compartment-specific age gaps (liver, pancreas, kidneys, spleen, visceral/subcutaneous fat, muscle) that are intercorrelated (mean r=0.408) and average into an Overall Aging Gap (OAG) predicting multimorbidity, 14 incident diseases, and mortality (HR 1.15–1.49/s.d.). Leave-one-out Cox models then isolate sparse, anatomically coherent compartment residuals (kidney–CKD, liver–liver disease, fat/muscle–T2D). Execution is competent, but the claimed conceptual advance — shared axis plus conditional compartment refinement rather than parallel clocks — is not new: Kivimäki et al. (2025) and Huang et al. (2026), both cited by the authors, already perform this exact decomposition in other modalities. The real contribution is narrower: porting established logic to one new modality.

## 2. Strengths

The pipeline is rigorous at scale: MAE 2.69y, R²=0.816, calibration and repeat-scan stability (ICC=0.74) confirmed. The leave-one-out joint Cox design correctly avoids part-whole circularity by jointly estimating compartment and residual-OAG coefficients rather than conditioning a PAG on an OAG containing it. Robustness checks (partial correlations controlling age/sex/BMI; kidney sensitivity excluding renal codes) are thorough for a single-cohort design.

## 3. Weaknesses

Beyond the provenance issue above, there is zero external validation in a healthy-volunteer, largely European cohort. Incremental discrimination over age+BMI+smoking+alcohol is marginal (ΔC 0.003–0.049) with no comparison against a standard clinical risk score, undercutting the "broadly informative" framing. OAG×HLS interaction survives FDR correction for only 2/15 endpoints, yet Figure 5 and the discussion present the stratified pattern across nearly all endpoints as if confirmatory. Three of eight compartments are body-composition rather than organ measures, and no analysis tests whether OAG's signal collapses against an adiposity-only score.

## 4. Editorial Decision

**Reject and return for clarification.** The undisclosed, numerically divergent preprint must be resolved before external review can proceed. Independent of that, the core novelty claim is pre-empted by cited concurrent work, and the absence of external validation or a clinical-baseline comparison are non-revisable gaps for a paper whose contribution is decomposition logic rather than a new modality.

## 5. Suggested Reviewer Expertise

Reviewers should have direct, article-level familiarity with axis-decomposition or mutual-adjustment approaches to multi-organ biological age (proteomic, methylation, or imaging-based), with 3D deep-learning age-regression architectures (MedNeXt/nnU-Net family) applied to large-scale MRI cohorts, and with UK Biobank-scale survival-analysis and FDR-correction methodology for PheWAS-style designs. On the clinical side, reviewers should bring nephrology expertise for evaluation of the kidney-CKD engagement claims and hepatology/metabolic-disease expertise for the liver- and adiposity-linked findings, given the manuscript's disease-specific claims concentrate in these two systems.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved rapidly past organ-age-gaps-as-parallel-clocks. Tian et al. (Nat. Med. 2023) and Oh et al. (Nature 2023) established multi-organ aging from blood biomarkers and plasma proteomics, respectively, at population scale. Argentieri et al. (Nat. Med. 2024) extended proteomic clocks to diverse populations. On imaging specifically, Le Goallec et al. (Nat. Commun. 2022) first showed correlated liver–pancreas MRI age gaps (r = 0.53, closely matching this manuscript's r = 0.56 for the same organ pair), and this year the MULTI Consortium (Wen et al., Nat. Med. 2026, N = 313,645) published seven MRI-based organ clocks spanning brain, heart, liver, adipose, spleen, kidney, and pancreas integrated with proteomics, metabolomics, and genome-wide association — a substantially larger and more mechanistically integrated MRI aging-clock study than the present submission, though it does not perform an axis-conditional decomposition. Most directly relevant, Kivimäki et al. (Lancet Digit. Health 2025) applied mutual organ-age adjustment in the Whitehall II proteomic cohort, and Huang et al. (Sci. China Life Sci., published 8 May 2026) formalized a common-versus-organ-specific structural decomposition across multi-omics layers in over 500,000 UK Biobank participants — the same conceptual move this manuscript makes, in a different modality, published essentially concurrently. The manuscript cites all four but should engage more critically with the fact that its central organizing claim is now a replication of established logic in a new but narrower modality, not a novel interpretive framework.

## 7. Suggested Reviewers

**Multi-organ aging / axis-decomposition methodology:** He Huang (Sci. China Life Sci. 2026 structural-decomposition paper); Zhiyuan Song and Huizi Cao (co-first authors, MULTI Consortium, Nat. Med. 2026 MRI organ clocks); Ye Ella Tian (Nat. Med. 2023 heterogeneous multi-organ aging).

**Deep-learning MRI age regression:** Thomas Küstner (Tübingen; npj Aging 2026 multi-organ MRI biological-age framework, ResNet/deep-regression architectures on UK Biobank).

**Nephrology / kidney aging:** Xianhui Qin (Nanfang Hospital, Southern Medical University; biomarker-based biological aging and CKD outcomes).

**Hepatology / metabolic imaging:** to be identified via targeted search matched to liver-PDFF and NAFLD-aging literature if the editor wishes to proceed to review after the integrity issue is resolved.

## Further Literature

1. **Tian, Y.E. et al. Heterogeneous aging across multiple organ systems and prediction of chronic disease and mortality.** *Nat. Med.* 29, 1221–1231 (2023). PMID: 37024597. Independent, foundational blood-biomarker precedent for treating multi-organ age gaps as a joint system rather than isolated clocks; cited by the manuscript but not engaged as a direct methodological ancestor of the axis/residual framing.

2. **Oh, H.S.-H. et al. Organ aging signatures in the plasma proteome track health and disease.** *Nature* 624, 164–172 (2023). PMID: 38057571. Independent. Reports substantially weaker inter-organ coupling (mean r≈0.21) than this manuscript's imaging-based r=0.408, a contrast the authors use to argue imaging captures a more integrated signal — a claim that itself needs a modality-matched confound check (shared acquisition/preprocessing vs. shared biology) that is not performed.

3. **Argentieri, M.A. et al. Proteomic aging clock predicts mortality and risk of common age-related diseases in diverse populations.** *Nat. Med.* 30, 2450–2460 (2024). PMID: 39117878. Independent. Demonstrates cross-ancestry generalizability that this UK Biobank-only, predominantly European submission does not attempt.

4. **Le Goallec, A. et al. Using deep learning to predict abdominal age from liver and pancreas magnetic resonance images.** *Nat. Commun.* 13, 1979 (2022). PMID: 35418184. Directly prior art in the same modality and two of the same organs; the reported liver–pancreas correlation (0.53) closely matches this manuscript's 0.56, supporting the finding but also confirming the coupling phenomenon itself is already established, not newly discovered.

5. **Wen, J. et al. (MULTI Consortium) MRI-based multi-organ clocks for healthy aging and disease assessment.** *Nat. Med.* 32, 82–92 (2026). PMID: 41102562. Independent, larger (N=313,645), and more mechanistically integrated (genomics, proteomics, metabolomics) competing MRI multi-organ aging study published shortly before this submission; does not perform axis-conditional decomposition, which is this manuscript's main point of differentiation, but the size and multi-omics linkage gap should be addressed directly rather than left as an uncontextualized citation.

6. **Kivimäki, M. et al. Proteomic organ-specific ageing signatures and 20-year risk of age-related diseases: the Whitehall II study.** *Lancet Digit. Health* 7, e195–e204 (2025). Independent. Applies the identical mutual-adjustment/leave-one-out logic to proteomic organ clocks; the manuscript correctly cites this as methodological precedent but this weakens rather than supports the novelty claim in Section 1.

7. **Huang, H., Li, Y., Song, Q. et al. Structural decomposition enables multi-omics dissection of common and organ-specific aging.** *Sci. China Life Sci.* (2026). doi:10.1007/s11427-025-3242-5. Published 8 May 2026, four days before the related medRxiv preprint (see entry 10). Independent, same-conceptual-class prior art: a formal common-vs-organ-specific structural decomposition across multi-omics layers in >500,000 UK Biobank participants. This is the single most damaging citation to the manuscript's originality claim and deserves a direct comparative paragraph rather than a passing discussion mention.

8. **Ecker, V., Yang, B., Gatidis, S. & Küstner, T. Imaging-derived biological age across multiple organs links to mortality and aging-related health outcomes.** *npj Aging* (2026). doi:10.1038/s41514-026-00377-7. Independent competing imaging-based multi-organ (brain, cardiac, abdomen, OCT fundus) aging-clock study using ResNet-based regression on ~143,000 UK Biobank samples; broader anatomical scope than the present abdomen-only submission and not cited.

9. **Ren, P. et al. Imaging-based organ-specific aging clock predicts human diseases and mortality.** *npj Digit. Med.* 9, 278 (2026). doi:10.1038/s41746-026-02488-7. Independent. Reports a pancreas MRI clock with higher raw performance (MAE=2.94) but explicitly trades this against organ-specificity — directly relevant to this manuscript's own MAE/R² tradeoff discussion and should be cited alongside it.

10. **Wang, Y. et al. MRI reveals the hierarchical organization of abdominal biological aging from shared burden to disease-specific organ engagement.** medRxiv 2026.05.08.26352767 (posted 12 May 2026; unreviewed preprint — not peer-reviewed evidence). Same-author-group, same-cohort concurrent version of the present submission under a different title, with materially different cohort sizes and effect estimates (see Integrity Alert). Flagged here per policy as an undisclosed, unreviewed prior version rather than independent literature; must be reconciled before further evaluation.

053962
**1. Overall Assessment**

The manuscript claims YOLO11n, repackaged as "LiteChestGreenXY11n," outperforms YOLOv5s/v8s/v11s on chest X-ray abnormality localization while using less compute and energy, formalized via a proposed Energy-Aware Clinical Deployment Suitability Index (EA-CDSI). This claim does not hold. Reported mAP@0.5 differences (0.344–0.355) are within a 3% band on a 504-image test set, with no confidence intervals or repeated runs. The EA-CDSI is mathematically degenerate: min-max normalization sets the lowest-resource model's cost to exactly zero, so LiteChestGreenXY11n's raw EA-CDSI (320,344.75) is an artifact of dividing by the epsilon term, not a meaningful signal — fatal to the paper's stated primary contribution.

**2. Strengths**

The benchmarking protocol holds resolution, batch size, epochs, and hardware constant across four YOLO variants, sounder practice than most comparable lightweight-CXR studies cited. Energy accounting in Joules per inference is a genuinely underused axis in this literature. Applying Grad-CAM identically across all four models for direct comparison is a reasonable design choice.

**3. Weaknesses**

LiteChestGreenXY11n has no described architectural modification relative to stock YOLO11n-nano; as written, this is a relabeling exercise, not a new framework. The EA-CDSI formula is structurally broken and easily gamed by dataset or hardware choice. Table 3's Grad-CAM Quality Score, Heatmap Sharpness, and Clinical Interpretability ratings have no disclosed scoring protocol, radiologist panel, or inter-rater reliability statistic. The dataset is an undisclosed VinDr-CXR derivative (classes match VinDr-CXR's local-label set exactly), sourced via Roboflow rather than the original PhysioNet release, with no citation of Nguyen et al. (2022), no discussion of the original IRB approval, and no check on leakage from the re-partitioned split.

**4. Editorial Decision**

**Reject.** The core quantitative contribution is mathematically invalid, the model lacks disclosed architectural novelty, and the explainability metrics are unvalidated — structural, non-revisable flaws. Given its computational-benchmarking framing, this work is better suited to **Communications Engineering** after fundamental revision (redesigned composite metric, disclosed dataset provenance); npj Digital Medicine would be premature absent clinical validation.

---

**5. Suggested Reviewer Expertise**

Reviewers should have expertise in: efficient/lightweight object detection architecture design (YOLO family internals, not just application); Grad-CAM and saliency-based XAI validation methodology, including inter-rater reliability protocols; Green AI / energy-efficiency benchmarking of deep learning systems; composite index construction and normalization pitfalls in multi-criteria decision metrics; and thoracic radiology, specifically radiologist-annotated CXR datasets (VinDr-CXR class taxonomy) for clinical relevance assessment of localization outputs.

**6. State-of-the-Art Literature Review (Past 3 Years)**

Recent work has moved past demonstrating that YOLO variants can detect CXR abnormalities toward rigorously validating explainability and efficiency claims. Ahsan et al. (MDPI, Nov. 2025) paired YOLOv11 with Grad-CAM for pneumonia detection specifically, evaluated across two independent datasets with disclosed metric protocols — directly overlapping with this manuscript's core method but with stronger external validation. Rajaraman and Liang's ensembled YOLO work (PMC, 2025) addresses multi-organ CXR detection with attention to generalization across imaging sources, a step this manuscript does not attempt. On the dataset side, the Mamba-YOLOvX study (ScienceDirect, 2025) benchmarks directly on VinDr-CXR and explicitly documents class-imbalance effects (e.g., poor atelectasis/pleural-thickening detection), a confound this manuscript's nine-class subset likely inherits but never discusses. This manuscript does not engage with any of this concurrent work, despite citing tangential lightweight-model papers (SlimNet/EdgeNet, NeuroVision-Lite) that are less directly comparable than the YOLOv11+Grad-CAM CXR literature it omits.

**Suggested Reviewer Names**

*Lightweight detection/YOLO architecture:* Sovit Ranjan Rath; Mohammad Hossein Rezvan; Rejin Varghese (YOLOv8/v9 architecture analysis authors).
*XAI/Grad-CAM validation:* Sivaramakrishnan Rajaraman; Andrea De Simone; Pooya Khosravi.
*Green AI/energy efficiency:* Kostas Ordoumpozanis; Roberto Verdecchia; Sasha Luccioni.
*Thoracic radiology/VinDr-CXR:* Ha Q. Nguyen; Hieu H. Pham; Khanh Lam.

---

**Further Literature**

1. Nguyen, H.Q. et al. "VinDr-CXR: An open dataset of chest X-rays with radiologist's annotations." *Scientific Data* 9, 429 (2022). DOI: 10.1038/s41597-022-01498-w. Peer-reviewed. This is the original source dataset the manuscript's nine-class subset is drawn from (via an uncited Roboflow mirror); the manuscript should cite this directly and address the original patient-level splitting and IRB approval rather than treating the Roboflow copy as an independent resource.

2. Ahsan et al. "An Explainable YOLO-Based Deep Learning Framework for Pneumonia Detection from Chest X-Ray Images." *Algorithms* 18(11):703 (2025). Peer-reviewed. Nearly identical method (YOLOv11 + Grad-CAM) applied to CXR, with cross-dataset evaluation the present manuscript lacks; a direct, uncited competitor.

3. Rajaraman, S. & Liang, Z. "Ensembled YOLO for multiorgan detection in chest x-rays." *Proc SPIE* 13407 (2025). Peer-reviewed. Demonstrates YOLO ensembling for robustness across diverse CXR sources, a generalization strategy absent from this manuscript's single-source evaluation.

4. Mamba-YOLOvX localization/classification study on VinDr-CXR. *ScienceDirect* (2025). Peer-reviewed. Benchmarks directly on VinDr-CXR and documents severe class-imbalance effects on detection accuracy — a confound this manuscript's class subset inherits but does not analyze.

5. Sobek, J. et al. "MedYOLO: a medical image object detection framework." *J Imaging Inform Med* 37(6):3208-3216 (2024). Peer-reviewed; already cited by the manuscript [7]. Prior lightweight-YOLO-for-medical-imaging work the authors reference but do not benchmark against directly, despite it being a closer competitor than the generic YOLOv5s/v8s/v11s baselines chosen.

6. Ordoumpozanis, K. & Papakostas, G.A. "Green AI: Assessing the carbon footprint of fine-tuning pre-trained deep learning models in medical imaging." *3ICT* (2024). Peer-reviewed; already cited [18]. Establishes carbon/energy accounting methodology in medical imaging that this manuscript's EA-CDSI should have been benchmarked against for measurement rigor (e.g., repeated-trial variance), which it lacks.

7. Khan, S. et al. "Green AI techniques for reducing energy consumption in AI systems." *Array* (2025): 100652. Peer-reviewed; already cited [28]. Survey of Green AI methods; the manuscript invokes this framing but does not adopt any of its recommended measurement-reliability practices (e.g., multiple power-draw samples, hardware-isolation controls).

8. De Simone, A. et al. "Optimizing Uncertainty-Aware Deep Learning for On-the-Edge Murmur Detection in Low-Resource Settings." arXiv:2511.00966 (2025). **Unreviewed preprint.** Relevant for its uncertainty-quantification approach to edge deployment suitability, an axis (confidence/calibration) entirely missing from this manuscript's EA-CDSI.

9. Karagoz, G. et al. "XIMED: A Dual-Loop Evaluation Framework Integrating Predictive Model and Human-Centered Approaches for Explainable AI in Medical Imaging." *Machine Learning and Knowledge Extraction* 7(4):168 (2025). Peer-reviewed; already cited [17]. Provides a human-centered XAI evaluation protocol with disclosed rater methodology — precisely the validation structure missing from this manuscript's Table 3 Grad-CAM scores.

054248
**Reject.** On reflection, "send for review, contingent on resolution" was too hedgy — that's not a real editorial state. A paper with an unresolved undisclosed-overlap question shouldn't go to reviewers at all; sending it out treats the integrity question as separable from the science when it isn't. The correct move is to reject now, without prejudice, and invite resubmission only once the authors disclose the March 2026 preprint, cite it, and demonstrate the submission's incremental contribution stands independently of it.

Three things support this beyond the disclosure problem itself:

The concept-meaning task was quietly weakened from twenty candidate definitions (preprint) to four (this submission). That's not a neutral methodological choice — it removes the one part of the shared benchmark where the preprint found real signal (72.6% baseline accuracy, sharp poisoned-context degradation) and replaces it with a task that ceilings out above 90% for most models. Absent justification, this reads as re-engineering the instrument to produce a different headline rather than a principled redesign, which is a bigger problem than ordinary revisability covers.

The paper's actual novel content — model-version transitions and the downstream disease-inference experiment — is real, but it doesn't need the disputed benchmark infrastructure to stand on its own. That's a sign the two papers should not coexist as currently drawn: either this is a distinct paper built around version-transition and downstream propagation (with the shared concept-benchmark material properly cited and minimized), or it's the same study double-published. The authors control which, but they haven't told us.

The TeaBERT three-distractor disease-inference design is a structural choice baked into the dataset, not something reviewers can fix with a revision request — if it's inflating the 13.1% flip rate, that requires new data construction, which is a rejection-grade limitation on its own per the non-revisable/structural-dataset criterion.

**Editorial Decision (revised):** Reject. The manuscript shares its core benchmark and roughly half its results with an undisclosed, same-author March 2026 medRxiv preprint, and the one task modified between the two versions was weakened in a way that removes rather than adds discriminative power — together these prevent sending the paper to review as submitted. Recommend transfer to **npj Digital Medicine**, with resubmission conditioned on explicit disclosure of and differentiation from the preprint, restoration or justification of the definition-recognition task design, and a stated rationale for the three-distractor disease-inference construction.

054291
# Editorial Report — "The VIRTUheart Framework: Robust 3D Coronary Reconstruction from Monoplane Angiography for Virtual Fractional Flow Reserve"

## 1. Overall Assessment

The manuscript discloses the full mathematics behind VIRTUheart's 3D coronary reconstruction from two non-simultaneous monoplane angiographic projections: Hermite cubic spline centreline interpolation, bidirectional forward/backward tracking to resolve epipolar-line/centreline near-parallelism, and single-point rigid-body registration for residual motion. This transparency is valuable against a field dominated by proprietary commercial tools (QFR, CAAS vFFR, FFRangio).

However, the contribution is largely an explicit write-up and modest refinement of an already-published, already-clinically-validated tool (in use since 2013), not a new empirical result. The novel components — spline formulation, the 32° bidirectional threshold, single-point registration — are validated on one digital phantom vessel under four synthetic movements, with no patient data, no comparator method, and no uncertainty quantification.

## 2. Strengths

The full derivation (Section 2, Appendix A) is genuinely reproducible detail rarely published for a clinically deployed vFFR tool. Bidirectional tracking sensibly addresses a well-characterised failure mode, with Table 2 showing the forward/backward angle asymmetry motivating it. Single-point registration is computationally cheap and consistent with the 10-minute procedural constraint; Table 1 shows a credible mechanism by which omitting it inflates radial error at maximal stenosis from 1.41% to 42.30% under a 5,5,0 mm shift.

## 3. Weaknesses

Phantom validation uses a single vessel (60% LCX stenosis) under four discrete translations — insufficient to characterise behaviour across tortuosity, stenosis severity, or the rotational motion the authors acknowledge as unmodelled. The 32° threshold is "determined empirically" with no calibration dataset or sensitivity analysis reported. Cited clinical validation (VIRTU-1, VIRTU-Fast, COMPLETE, ORBITA) predates or is independent of this specific algorithm; none demonstrates that this newly formalised pipeline reproduces those results. No head-to-head benchmarking exists against QFR, CAAS, FFRangio, NeCA, or DeepCA, despite the SOTA section itself arguing this comparison is overdue.

## 4. Editorial Decision

**Reject**, with transfer recommendation. This is a well-written methods disclosure, but its novel components are validated on a single synthetic vessel with no comparator, and its clinical evidence is inherited from earlier, non-equivalent pipeline versions. I recommend **Communications Engineering** as primary transfer target, given the contribution is algorithmic/mathematical transparency rather than new patient outcomes; **npj Digital Medicine** is a secondary option if authors expand patient-level validation of this specific pipeline version.

## 5. Suggested Reviewer Expertise

Reviewers should have direct expertise in: epipolar geometry and multi-view 3D reconstruction from X-ray projection data; parametric spline-based curve fitting for vascular centreline modelling; interventional cardiology with hands-on angiography-derived physiology (vFFR/QFR) experience; digital phantom and in-silico validation methodology for medical imaging pipelines; and CFD-based coronary flow modelling.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has bifurcated over the past three years into explicit geometric methods and learned/implicit representations. On the deep-learning side, Wang et al.'s NeCA uses self-supervised neural implicit representation with a multiresolution hash encoder and differentiable cone-beam forward projection to reconstruct 3D coronary trees from two projections without requiring 3D ground truth or large training sets, and the related DeepCA line pursues GAN-based reconstruction from sparse views — both cited by the authors but not benchmarked against. On the clinical-computational side, large multicentre comparisons such as the QFR-versus-FFR non-inferiority trial (Andersen et al., 2024, cited by the manuscript) and continued CAAS vFFR / FFRangio clinical deployments have shifted the field's emphasis toward head-to-head diagnostic accuracy and outcome prediction rather than reconstruction transparency alone. The manuscript's contribution — disclosing the mathematics of an already fifteen-year-old tool — engages meaningfully with the epipolar-geometry literature (Çimen et al.) but does not engage empirically with the learned-representation methods it cites, leaving the central question the field is now asking — how explicit geometric methods compare quantitatively to implicit/learned ones on real, non-simultaneous monoplane data — unanswered.

## 7. Suggested Reviewers' Names

**Epipolar/3D reconstruction geometry:** Serkan Çimen; Alejandro F. Frangi; Maysam Orouskhani.
**Spline-based vascular modelling:** Alistair Young; Pau Medrano-Gracia.
**Interventional cardiology / angiography-derived physiology:** William Fearon; Nils Johnson; Bon-Kwon Koo.
**Deep-learning coronary reconstruction:** Abhirup Banerjee; Vicente Grau; Yiying Wang.

## Further Literature

1. **Wang et al., "NeCA," Bioengineering 11(12):1227, 2024 (DOI 10.3390/bioengineering11121227).** Peer-reviewed, independent (Oxford) group. Cited by the manuscript. Self-supervised neural-implicit alternative to explicit epipolar reconstruction from two projections; directly competing paradigm, not benchmarked head-to-head against VIRTUheart.

2. **Wang et al., "DeepCA," WACV 2025 (IEEE Xplore; preprint arXiv:2407.14616).** Peer-reviewed conference paper, independent (Oxford) group. Cited by the manuscript. Explicitly targets non-rigid cardiac/respiratory motion between non-simultaneous projections via a Wasserstein GAN — a direct methodological contrast to this manuscript's rigid single-point registration assumption, which the authors themselves flag as a limitation.

3. **Andersen et al., "Quantitative flow ratio versus fractional flow reserve," Lancet 404(10465):1835–1846, 2024.** Peer-reviewed multicentre non-inferiority RCT, independent group. Cited by the manuscript. Establishes the clinical-trial evidentiary bar (patient-level non-inferiority) that competing angiography-derived physiology tools have met; the current manuscript's specific reconstruction algorithm has no equivalent trial-level validation.

4. **Lashgari, Choudhury, Banerjee, "Patient-specific in silico 3D coronary model," Front. Cardiovasc. Med. 11:1398290, 2024.** Peer-reviewed review, independent (Oxford) group. Cited by the manuscript. Recent comprehensive review of the segmentation-to-CFD pipeline space; situates VIRTUheart as one of several competing frameworks rather than a uniquely transparent one.

5. **Çimen, Gooya, Grass, Frangi, "Reconstruction of coronary arteries from X-ray angiography: A review," Med. Image Anal. 32:46–68, 2016.** Peer-reviewed, independent group. Cited by the manuscript. Foundational review of epipolar-geometry reconstruction methods; the current manuscript's core mathematical apparatus is a direct descendant of this line rather than a conceptual departure from it.

6. **Kaba et al., deep-learning coronary segmentation/classification review, 2023.** Peer-reviewed, independent group. Cited by the manuscript. Relevant to the manuscript's Step 1 (2D centreline segmentation), which is treated as an automated pre-processing step but not itself validated in this paper.

7. **Taylor et al., ORBITA hMVR microvascular resistance analysis, 2025–2026.** Peer-reviewed, **same author group** (Sheffield). Cited by the manuscript. Demonstrates downstream clinical utility of VIRTUheart-derived geometry for microvascular resistance, but does not validate the specific Hermite-spline/bidirectional-tracking reconstruction introduced in this paper — an important same-group distinction the manuscript blurs.

8. **Fearon et al., FFRangio (CathWorks) full-coronary-tree reconstruction, 2026.** Cited by the manuscript as an emerging competitor. Independent group. Represents the commercial full-tree benchmark against which the manuscript's single-vessel, two-view approach is explicitly *not* compared, despite the manuscript itself calling for this comparison in its Discussion.

9. **Ghobrial et al., VIRTUheart real-world catheterisation laboratory feasibility, 2024.** Peer-reviewed, **same author group**. Cited by the manuscript. Demonstrates procedural-time feasibility of the broader vFFR workflow but not geometric accuracy of this specific reconstruction algorithm.

10. **Anonymous Scientific Reports phantom-validation study (Sheffield VIRTUheart group), 2021, "The importance of three-dimensional coronary artery reconstruction accuracy when computing vFFR," PMC8490364.** Peer-reviewed, **same author group**, **not cited in the current manuscript**. Validated an earlier epipolar-line-based reconstruction against 66 phantom datasets spanning seven stenoses and fifteen 3D-printed patient-based geometries — a substantially larger and more systematic phantom validation than the single-vessel, four-condition test presented here. Its omission is notable given its direct relevance to, and methodological precedence over, the present validation approach.

054466
## Editorial Report — TRIM: Unlearning Transformer for Multimodal Trial Emulation (Condensed)

### 1. Overall Assessment

TRIM repurposes negative control outcomes (NCOs) from a passive bias-detection diagnostic into an active pruning signal: NCO-derived per-subject disagreement scores identify and prune components of a multimodal transformer propensity network, which is then refit to produce debiased propensity scores for target trial emulation (TTE) of dopaminergic therapies in PPMI. This is a genuine conceptual extension of empirical calibration (Schuemie et al.) into a structured-pruning intervention, and the ablation depth — a 54-setting hyperparameter sweep (972 runs), transformer-vs-MLP frozen-encoder comparison, held-out NCO splits — is unusually thorough for applied clinical ML. But the entire demonstration lives inside one densely-phenotyped research cohort, and the paper never checks its emulated estimates against the RCT ground truth that exists for exactly its own comparisons (levodopa vs. MAO-B inhibitors). That gap undermines the paper's central claim that pruning improves accuracy rather than merely smoothness.

### 2. Strengths

TRIM's reframing of NCOs as an active debiasing lever, not just a post hoc correction, is methodologically novel. The robustness battery — consistent EASE reduction across 8/9 pairs and the full hyperparameter sweep — supports that the effect is not a tuning artifact. The multimodal architecture (InfoNCE alignment, masked-autoencoder imputation) is tested against an appropriately matched MLP baseline, and the frozen-transformer's cleaner few-shot transfer is a useful finding. The attention-interpretability section is unusually disciplined, tying claims to verifiable metrics rather than attention weights alone.

### 3. Weaknesses

No benchmarking against PD MED (Lancet, 2014), the RCT establishing levodopa's motor superiority over MAO-B inhibitors for exactly this comparison class. Validation occurs entirely in PPMI, a protocol-driven research cohort shown to diverge systematically from real-world PD populations (Beaulieu-Jones et al., 2024) — undercutting the paper's real-world screening claims. Directly comparable prior work is missing: van den Heuvel et al. (2021) already ran causal treatment-effect estimation in PPMI itself, and deep-learning-unlearning-for-causal-inference precedents (Ramachandra & Sethi, 2023) are not engaged with. Several fixed NCOs are rare binary flags with unreported event counts, raising instability concerns in the bias index. The high-bias subset disproportionately captures genetically enriched (LRRK2/GBA) participants, risking systematic down-weighting of a subgroup of increasing precision-medicine interest, unaddressed via subgroup ATEs.

### 4. Editorial Decision

Reject, with recommendation to transfer to *npj Digital Medicine* (alternative: *npj Parkinson's Disease*). The pruning mechanism is a real contribution, but validating clinical-plausibility claims requires either RCT benchmarking or a second, more representative RWD source — not patchable in a short revision. Missing engagement with van den Heuvel et al. and the deep-causal-unlearning literature also needs resolution before novelty can be properly assessed.

---

### 5. Suggested Reviewer Expertise

Reviewers should cover: (1) deep-learning-based causal inference and treatment-effect estimation on multimodal or EHR-derived data, specifically prior work combining representation learning with propensity modeling; (2) negative-control methodology and empirical calibration for residual confounding, including its assumptions and failure modes; (3) neural network pruning / machine unlearning as applied to tabular or structured clinical models, distinct from LLM-unlearning contexts; (4) movement-disorder clinical epidemiology, specifically real-world and observational treatment-effect studies in Parkinson's disease and familiarity with PPMI's eligibility structure and MDS-UPDRS/MoCA measurement properties; and (5) target trial emulation methodology and its validation standards (benchmarking emulated estimates against RCTs).

### 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved in two directions relevant here. First, deep-learning causal inference on structured/multimodal clinical data has matured beyond single-modality EHR models: Targeted-BEHRT (Rao et al., 2022) tested deep causal EHR models against an RCT-established null association; DoubleMLdeep (Klaassen et al., 2024) and related work from the Feuerriegel group (Frauen, Melnychuk) extend doubly-robust/representation-based causal estimation explicitly to multimodal settings, directly overlapping TRIM's stated contribution of "unified multimodal RWD analysis." Second, target trial emulation itself has been formalizing its validation standards: the TARGET reporting guideline (JAMA, September 2025) and large-scale RCT-replication efforts (Wang et al., JAMA 2023, emulating 32 trials) have pushed the field toward mandatory benchmarking of emulated estimates against randomized ground truth wherever it exists — a standard TRIM's own comparisons (levodopa vs. MAO-B inhibitors) could meet via PD MED but do not attempt. Within PD specifically, van den Heuvel et al. (2021) already applied classical causal machine learning (MSM/g-formula) to PPMI treatment-timing questions, and Beaulieu-Jones et al. (2024) established that PPMI-like research cohorts diverge systematically from real-world PD populations in treatment initiation timing and disease trajectory — a finding that directly bears on TRIM's generalizability claims and is not engaged with. TRIM advances the field methodologically (pruning-as-debiasing is new) but is positioned against a narrower slice of prior art (empirical calibration, attention-interpretability critique) than the literature actually contains, and it inherits rather than addresses the RWD-representativeness problem the field has just begun explicitly flagging.

### 7. Suggested Reviewer Names

**Technical / causal-ML (70%):**
Jesse H. Krijthe (Delft University of Technology — co-author of the directly comparable PPMI causal-treatment-effect study using IPTW/g-formula); Dennis Frauen (LMU Munich — deep learning for treatment-effect estimation under confounding); Shishir Rao (University of Oxford — Targeted-BEHRT, deep causal inference on longitudinal EHR with negative-control validation); Sven Klaassen (Universität Hamburg — DoubleMLdeep, multimodal causal effect estimation).

**Clinical / movement disorders (30%):**
Lieneke van den Heuvel (Radboud University Medical Center — PPMI-based observational causal analysis of PD treatment timing); Brett K. Beaulieu-Jones (Harvard Medical School / Beth Israel Deaconess — real-world vs. research-cohort divergence in PD progression).

---

### Further Literature

1. **PD MED Collaborative Group et al., "Long-term effectiveness of dopamine agonists and monoamine oxidase B inhibitors compared with levodopa as initial treatment for Parkinson's disease (PD MED)."** *Lancet* 384, 1196–1205 (2014). DOI: 10.1016/S0140-6736(14)60683-8. Not cited. The RCT ground truth for exactly the C/L-DOPA vs. rasagiline/selegiline comparisons TRIM emulates; levodopa showed somewhat better motor control than MAO-B inhibitors. TRIM's ATEs should be checked for directional concordance against this trial rather than judged only by internal calibration metrics.

2. **Van den Heuvel, L. et al., "Estimating the Effect of Early Treatment Initiation in Parkinson's Disease Using Observational Data."** *Movement Disorders* 36, 407–414 (2021). DOI: 10.1002/mds.28339. Not cited. The most directly comparable prior art: causal treatment-effect estimation (MSM, IPTW, g-formula) performed in PPMI itself. Independent literature; establishes a methodological and empirical baseline TRIM should be benchmarked against, not merely a citation gap.

3. **Beaulieu-Jones, B. K. et al., "Disease progression strikingly differs in research and real-world Parkinson's populations."** *npj Parkinson's Disease* 10, 58 (2024). DOI: 10.1038/s41531-024-00667-5. Not cited. Independent literature. Directly undermines TRIM's implicit generalizability claim by showing PPMI-like research cohorts diverge systematically from real-world PD populations in treatment timing and progression — the single-cohort validation weakness identified in this review.

4. **Rao, S. et al., "Targeted-BEHRT: Deep learning for observational causal inference on longitudinal electronic health records."** *IEEE Transactions on Neural Networks and Learning Systems* (2022). arXiv:2202.03487. Preprint/arXiv version flagged as such where journal version unconfirmed; treat with appropriate caution. Not cited. Independent literature. Closely overlapping goal (deep causal inference validated via a known-null RCT association) using a different mechanism (representation learning, not NCO-guided pruning) — a natural comparator for TRIM's novelty claims.

5. **Klaassen, S., Teichert-Kluge, J., Bach, P., Chernozhukov, V., Spindler, M. & Vijaykumar, S., "DoubleMLdeep: Estimation of causal effects with multimodal data."** arXiv:2402.01785 (2024). **Preprint — unreviewed, flagged accordingly.** Not cited. Independent literature. Directly overlaps TRIM's "unified multimodal RWD" framing via a doubly-robust deep-learning estimator rather than pruning; should be discussed to sharpen what pruning-based unlearning adds over doubly-robust multimodal estimation.

6. **Ramachandra, V. & Sethi, M., "Machine Unlearning for Causal Inference."** arXiv:2308.13559 (2023). **Preprint — unreviewed, flagged accordingly.** Not cited. Independent literature. Introduces machine unlearning applied to propensity-score models for causal inference — the same combination of concepts (unlearning + propensity modeling) that TRIM builds on; earliest identified prior use of this pairing and should anchor TRIM's novelty framing.

7. **Wang, S. V., Schneeweiss, S., Franklin, J. M. et al., "Emulation of randomized clinical trials with nonrandomized database analyses: results of 32 clinical trials."** *JAMA* 329, 1376–1385 (2023). DOI: 10.1001/jama.2023.4221. Not cited. Independent literature. Establishes the field-standard practice of systematically benchmarking TTE emulations against RCT results; directly supports the recommendation that TRIM validate its ATEs against PD MED rather than relying solely on internal EASE/ECE diagnostics.

8. **Schuemie, M. J., Hripcsak, G., Ryan, P. B., Madigan, D. & Suchard, M. A., "Empirical confidence interval calibration for population-level effect estimation studies in observational healthcare data."** *PNAS* 115, 2571–2577 (2018). DOI: 10.1073/pnas.1708282114. **Cited (ref. 6)** by the manuscript. Same conceptual lineage, independent group. This is the empirical-calibration/EASE foundation TRIM builds on; correctly cited, included here to note that TRIM's contribution is best read as an extension of this passive-diagnostic framework into an active pruning mechanism, a distinction the manuscript could state more explicitly.

9. **Frauen, D. et al., "LLM-driven treatment effect estimation under inference-time text confounding."** *NeurIPS* (2025). Not cited. Independent literature. Represents the same research group's (Feuerriegel lab) broader program on deep learning for confounded treatment-effect estimation across modalities; useful for situating TRIM against the most active current group working on this exact intersection of deep learning and causal inference.

10. **Tong, J., Hu, J., Hripcsak, G., Ning, Y. & Chen, Y., "Federated target trial emulation using distributed observational data for treatment effect estimation."** *npj Digital Medicine* (2025). Not cited. **Same-author-group prior work** (senior author Yong Chen). Demonstrates the group's active TTE research program in a different direction (federated/distributed data rather than multimodal debiasing); useful for reviewers assessing incremental contribution relative to the group's own recent output, though not a competing or duplicative submission.

054793
# Editorial Report: "MetaHarmonizer: robust biomedical metadata harmonization and a contamination control for inflated LLM performance on public benchmarks"

## EDITORIAL INTEGRITY ALERT

Independent search confirms this manuscript is textually identical, section for section, figure for figure, and reference for reference, to a bioRxiv preprint by the same author group (DOI 10.64898/2026.06.13.732088), publicly posted June 17, 2026, under a CC-BY license. The submitted manuscript does not disclose this preprint anywhere in its Data Availability, Code Availability, or cover materials as provided. Prior preprinting is permitted at this journal, but non-disclosure of an existing, identical, publicly indexed preprint at submission is a transparency lapse that must be resolved with the corresponding author before the manuscript proceeds to review. This is flagged as a process item, not a data-fabrication concern; the preprint and submission appear fully consistent with each other.

## 1. Overall Assessment

The manuscript's central claim is two-fold: LLM-only performance on public GDC/EFO benchmarks largely reflects pretraining memorization rather than transferable matching capability, and MetaHarmonizer offers a deterministic, competitive alternative. The contamination finding is the real contribution: the E3 target-rename collapse (LLM-only Top-1 losses of 12–24 pp) is clean and mechanistically interpretable, replicated across two model families. The tool itself, built from RapidFuzz, SapBERT, and FAISS in a cascade, is competent but recombinant rather than methodologically novel. Primary concerns are the undisclosed preprint noted above and whether an infrastructure paper without clinical evaluation clears this journal's bar.

## 2. Strengths

The contamination battery is the strongest element. Combining source paraphrase (E2), target renaming (E3), and memorization probes (P1–P3) isolates memorization more rigorously than existing n-gram-overlap methods; 80–100% verbatim GDC-identifier recovery in three of five models, replicated across Anthropic and Google families, has implications beyond this tool.

Statistical discipline is unusually careful: aggregation choices are justified rather than asserted, Holm-corrected tests span 28 comparisons, and calibrated-confidence AUCs of 0.73–0.94 support the triage claim rather than sitting as an isolated metric.

## 3. Weaknesses

SchemaMapper's retrieval is brittle under exactly the condition it targets: under synonym-swap paraphrase, alias-augmented SchemaMapper lost 22–30 pp Top-1, roughly three times LLM-only's loss, undercutting the practical case more than the Discussion acknowledges.

The benchmark is single-domain (CPTAC oncology, n = 165, 10 studies) despite the "domain-agnostic" framing, and the alias prompt was itself oncology-tuned. Two of nine LLMs failed to produce a usable alias dictionary and a third needed hallucination filtering, undermining the "training-free" pitch. LLM-only baselines used simple zero-shot prompting without retrieval augmentation, likely understating achievable performance.

## 4. Editorial Decision

**Send for Review, contingent on resolving the preprint-disclosure item.** The contamination methodology is a genuine contribution not undermined by the flaws above. Reviewers should adjudicate benchmark generalizability, paraphrase-fragility severity, and whether the tool stands independently of the contamination finding.

## 5. Suggested Reviewer Expertise

Reviewers should include expertise in embedding-based and ensemble schema matching for structured biomedical data (evaluation design, bipartite/graph reranking, benchmark construction such as Valentine-style protocols); biomedical ontology grounding and terminology services (EFO, NCIt, UMLS-trained encoders such as SapBERT, synonym/alias expansion pipelines); LLM benchmark contamination and memorization detection methodology (perturbation-based decontamination, membership-inference-adjacent probing, statistical treatment of pretraining leakage); and cancer genomics data curation and controlled-vocabulary governance (GDC/CPTAC/TCGA data dictionaries, FAIR metadata infrastructure for multi-omics repositories). A reviewer with applied statistics background in paired nonparametric testing and multiple-comparison correction for benchmark evaluation would strengthen adjudication of the paper's extensive statistical apparatus.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant landscape has moved quickly in 2025–2026. Magneto (Liu et al., arXiv 2412.08194), the manuscript's primary comparator, combines small-model retrieval with LLM reranking on the same CPTAC/GDC benchmark and remains competitive on MRR with SchemaMapper's best alias configuration. A directly relevant omission is BDIViz (Wu et al., IEEE VIS 2025 / arXiv 2507.16117) and its recent extension BDIViz-in-Action (arXiv 2604.10763), from the same VIDA-NYU group behind Magneto: an interactive visual-analytics system for the identical GDC/PDC schema-matching task that already implements ensemble matching with LLM-based validation and heatmap-driven human-in-the-loop triage, the same use case MetaHarmonizer's confidence-calibration section claims as a contribution. This should be engaged with directly, not merely benchmarked against Magneto's automated variants. A second concurrent, undisclosed-by-citation work is MetaMuse (bioRxiv, April 2026), a multi-agent LLM framework that, like OntologyMapper, uses SapBERT for terminology normalization, applied to GEO rather than GDC metadata; its existence suggests SapBERT-anchored normalization is converging as a field default rather than a distinguishing design choice. On the contamination side, the manuscript's E2/E3/E4 battery parallels, without citing, established perturbation-based contamination-detection techniques such as slot-masking probes (the "TS-Guessing" paradigm) and membership-inference-style benchmark auditing; situating the contribution against this literature, rather than only against Magar & Schwartz (2022) and the DCR framework (Xu et al., 2025), would better establish what the schema-matching-specific application adds. On balance, MetaHarmonizer's tool architecture replicates rather than surpasses the current frontier (Magneto, BDIViz, text2term), while its contamination-control protocol is the paper's one clearly novel contribution to the field.

## Suggested Reviewers

For schema-matching and entity-resolution methodology: Juliana Freire (NYU, VIDA Center; senior author on Magneto and BDIViz), Renée J. Miller (Northeastern University, schema-matching and data-integration foundations), Erhard Rahm (Leipzig University, COMA schema-matching framework).

For biomedical ontology grounding and terminology services: Mark A. Musen (Stanford, BioPortal/ontology infrastructure), Rafael S. Gonçalves (Stanford, text2term), Olivier Bodenreider (National Library of Medicine, UMLS and biomedical terminology mapping).

For LLM contamination and benchmark evaluation methodology: Roy Schwartz (Hebrew University of Jerusalem, data-contamination detection), Yanai Elazar (Allen Institute for AI, training-data leakage and memorization analysis).

For cancer genomics data curation and controlled-vocabulary governance: Robert L. Grossman (University of Chicago, Genomic Data Commons architecture), a GDC/CPTAC data-curation lead identifiable through the NCI Center for Cancer Genomics.

## Further Literature

1. **Golchin, S. & Surdeanu, M.** "Time Travel in LLMs: Tracing Data Contamination in Large Language Models." *Proceedings of the Twelfth International Conference on Learning Representations (ICLR)*, 2024. arXiv:2308.08493, doi:10.48550/arXiv.2308.08493. Peer-reviewed (ICLR 2024). **Uncited** by the manuscript. No author overlap (University of Arizona). This is the direct general-domain precedent the authors should have engaged with: its "guided instruction" completion-probing method, where a model is prompted to complete a partially masked reference instance and scored on exact/near-exact match, is methodologically identical in structure to the manuscript's P2/P3 memorization probes, just applied to GDC schema fields instead of NLP benchmark partitions. The manuscript presents its probe battery as a novel task-agnostic contribution without acknowledging this lineage.

2. **Wu, E., Koutras, C., Silva, C. T. & Freire, J.** "BDIViz: An Interactive Visualization System for Biomedical Schema Matching with LLM-Powered Validation." *IEEE Transactions on Visualization and Computer Graphics* (IEEE VIS 2025). arXiv:2507.16117. Peer-reviewed. **Uncited.** No author overlap with the MetaHarmonizer team, though it shares a co-author (Freire) with the manuscript's primary comparator, Magneto. Directly overlapping scope: an ensemble schema matcher with LLM-based validation and heatmap-driven human-in-the-loop triage, evaluated on the same GDC/PDC/CPTAC harmonization task. This is the closest existing system to the "calibrated confidence enables human-in-the-loop triage" claim made for SchemaMapper and should be a required comparator, not an omission.

3. **Wu, E., Koutras, C., Silva, C. T. & Freire, J.** "BDIViz in Action: Interactive Curation and Benchmarking for Schema Matching Methods." arXiv:2604.10763, 2026. Preprint, not yet peer-reviewed. **Uncited.** No author overlap. Extends BDIViz into a benchmarking harness that uses human-validated curation as evolving ground truth for schema-matcher comparison, a methodological alternative to the manuscript's static ground-truth benchmarking convention that bears directly on its Recall@GT and per-query metric discussion.

4. **"MetaMuse: A Multi-Agent AI System for Biomedical Metadata Curation and Harmonization."** bioRxiv, posted April 2026 (2026.04.12.718044v2), doi:10.1101/2026.04.12.718044. Preprint, not yet peer-reviewed; full author list not resolvable from available metadata, so overlap with the manuscript's author group cannot be confirmed and should be checked directly. **Uncited.** A concurrent, closely parallel design: a multi-agent LLM curation pipeline that, like OntologyMapper, uses SapBERT for terminology normalization, applied to GEO rather than GDC/EFO metadata. Its independent convergence on a SapBERT-anchored normalizer weakens the manuscript's implicit framing of this component choice as distinctive.

5. **Liu, Y., Pena, E., Santos, A., Wu, E. & Freire, J.** "Magneto: Combining Small and Large Language Models for Schema Matching." arXiv:2412.08194, 2025. Preprint (not yet peer-reviewed in a venue confirmable from available metadata). **Cited** (ref. 9) and used as the primary SchemaMapper comparator. No author overlap. Included here because its fine-tuned LLM-reranker variant remains statistically indistinguishable from SchemaMapper+Opus-4.5-alias on MRR (Table 1), meaning the manuscript's central accuracy claim rests on beating only Magneto's weaker bipartite variants, not its strongest configuration.

6. **Verbitsky, A., Boutet, P. & Eslami, M.** "Metadata Harmonization from Biological Datasets with Language Models." *Bioinformatics Advances* 5(1), vbaf241, 2025. doi:10.1093/bioadv/vbaf241. Peer-reviewed. **Cited** (ref. 20). No author overlap. Reports the same in-dictionary versus out-of-dictionary accuracy cliff (90–96% vs. 12–17%) that OntologyMapper's Stage 2.5 synonym-boost mechanism is implicitly designed to mitigate; the manuscript cites this once in the Introduction but never returns to it when discussing OntologyMapper's own out-of-corpus failure modes, a missed opportunity for direct methodological comparison.

7. **Gonçalves, R. S. et al.** "The text2term Tool to Map Free-Text Descriptions of Biomedical Terms to Ontologies." arXiv:2407.02626, 2024. Preprint. **Cited** (ref. 13) and used as the primary OntologyMapper comparator. No author overlap (Stanford BMIR). Its TF-IDF/edit-distance approach is the field's most widely adopted lightweight baseline; the manuscript's own benchmark shows the gap between OntologyMapper and text2term narrows to 2.2 pp on OLS-EFO (disease) but widens to 16.4 pp on Biomappings-EFO, a benchmark-dependent pattern the Discussion attributes to synonym-set density but does not test directly (e.g., via a synonym-count-stratified analysis).

055300
# Editorial Integrity Alert — For Handling Editor Only

**Undisclosed overlapping prior publication.** The submitted manuscript's pure-text dataset (TCM-5CMEval's five dimensions — TCM-Exam, TCM-LitQA, TCM-MRCD, TCM-CMM, TCM-ClinNPT) is not novel to this submission. An arXiv preprint, *TCM-5CEval: Extended Deep Evaluation Benchmark for LLM's Comprehensive Clinical Research Competence in Traditional Chinese Medicine* (arXiv:2511.13169, posted 17 Nov 2025), by an overlapping and largely identical author team (Tianai Huang, Jiayuan Chen, Lu Lu, Pengcheng Chen, Tianbin Li, Bing Han, Wenchao Tang, Jie Xu, Ming Li — same institutions: Shanghai University of TCM, Shanghai AI Laboratory, University of Washington), reports the identical five-dimension architecture, identical item counts per dimension and question type (e.g., TCM-Exam single-choice N=122, multiple-choice N=78, open-ended N=70 — exact matches), and identical funding acknowledgments (grants 82174506, 2024PT001, 2025BZ002). The submitted manuscript does not cite or disclose this preprint anywhere, despite it predating submission and being authored by the same group. This is textbook salami-slicing / undisclosed prior work, not a citation oversight — the core textual instrument being presented here as new is the same instrument already public under a near-identical name two months prior. This must be resolved with the authors before any further editorial action; it is not a matter for reviewers to adjudicate.

---

### 1. Overall Assessment

The manuscript introduces TCM-5CMEval, a five-dimension, multimodal (text, image, video) benchmark for evaluating LLMs on Traditional Chinese Medicine, paired with a psychometric validation layer (criterion validity against human cohorts, construct validity, item-stability reliability, subjective-scoring reliability) largely absent from prior TCM benchmarks such as TCMBench, TCMD, TCMEval-SDT, and MTCMB. The stated contribution — genuine multimodality plus human-anchored measurement validation — is a real gap in the literature. However, the pure-text component of this benchmark is not new: it is the previously arXiv-published TCM-5CEval (see Integrity Alert). The manuscript's actual incremental contribution is therefore narrower than presented — multimodal extension plus reliability/validity analysis layered onto an already-public textual instrument, not a de novo five-dimension benchmark.

### 2. Strengths

The psychometric validation is the manuscript's genuine advance. Criterion validity (Spearman's ρ between LLM and discipline-matched human performance, pooled mean ρ=0.774), construct validity via inter-dimensional correlation matrices, item-stability reliability (Cronbach's α up to 0.895), and subjective-scoring reliability (ICC(2,k), Krippendorff's α, CSS–expert correlation) collectively address a real measurement gap that TCMBench, TCMD, and MTCMB never attempted.

The human-model reversal finding — LLMs surpass humans on pure-text open-ended items but fall below discipline-matched human experts on multimodal items in LitQA, MRCD, and ClinNPT — is a substantive and diagnostically useful result, directly contradicting text-only evaluations that would credit these models with expert-surpassing competence.

The Composite Subjective Score (0.8×MacroRecall + 0.2×BERTScore) is a sensible, reproducible answer to the open-ended-scoring reliability problem that plagues the field.

### 3. Weaknesses

The undisclosed dataset overlap (above) is disqualifying pending resolution and cannot be waved through to review.

No external validation cohort beyond the 50 discipline-matched postgraduate students; generalizability of the human anchor to practicing clinicians is unestablished.

The error-item analysis identifies "clinical syndrome differentiation" and "classical text exegesis" as dominant failure modes but offers no controlled ablation isolating architecture, training corpus, or reasoning-chain length as causal factors — a limitation the authors themselves concede.

### 4. Editorial Decision

**Reject.** The undisclosed overlap with the authors' own prior arXiv publication is a disqualifying integrity flaw independent of the work's technical merits; it cannot be resolved through revision within a review cycle and misrepresents the novelty of the submission's core dataset.

### 5. Suggested Reviewer Expertise

Multimodal LLM evaluation methodology; psychometric test theory (reliability/validity indices) applied to AI benchmarks; TCM clinical pattern differentiation and classical-text pedagogy; computer vision for medical/pharmacognostic image-video content; research integrity in dataset reuse.

### 6. State-of-the-Art Literature Review

TCM LLM benchmarking has moved rapidly: TCMBench and TCMD (2024) established exam-style objective assessment; TCMEval-SDT (Scientific Data, 2025) added expert-annotated syndrome-differentiation cases; MTCMB (arXiv:2506.01252) integrated 12 sub-datasets across knowledge, reasoning, and safety; TCM-Ladder (arXiv:2505.24063) was first to introduce image/video multimodality; a second TCM-Eval (arXiv:2511.07148) targets dynamic, extensible expert-level assessment. This submission's differentiator — pairing multimodality with formal reliability/validity analysis — is not yet claimed elsewhere and would be a genuine advance, contingent on resolving its relationship to the authors' own TCM-5CEval preprint.

---

## Suggested Reviewers

**Multimodal LLM evaluation:** Wenjing Yue, Jiacheng Xie, Shufeng Kong

**Psychometrics/measurement validity:** Zhe Wang, Yan Zhu, Ariel Levy

**TCM clinical/classical literacy:** Ping Yu, Kaitao Song, Junying Chen

056083
## 1. Overall Assessment

This manuscript uses the Haodf dataset (48,861 matched consultations, six disease groups) to show Chinese online consultations concentrate heavily in a few doctor-side cities (Beijing 34.1%, Gini 0.929), with disease-specific variation driven by physician visibility rather than patient geography. The central claim — telemedicine reinforces rather than flattens offline medical hierarchies — is not new: Xiang, Hong, Guo et al., *Nature Cities* (2026), already establish hub-dominated, core–periphery reinforcement in Chinese telemedicine at national network scale with a more sophisticated framework. This manuscript cites that paper but does not differentiate its contribution from it. Independent verification also found that IEEE DataPort's documentation for this exact dataset defines the sixth category as **Lung Cancer**, not "lung disease" as used throughout — a mislabeling that removes the most parsimonious explanation (oncology referral) for that category's concentration.

## 2. Strengths

The city-linkage pipeline is transparent (90.0%/94.4% match rates) and correctly separates the full 161-city output from the 86 positive-volume cities used in concentration analysis. The Gini/HHI/effective-number-of-cities toolkit, applied per disease group, is well-triangulated. The paired logistic-regression and XGBoost–SHAP design, with grouped feature domains, gives a disciplined audit structure, appropriately labeled non-causal. Sensitivity checks — stricter Beijing/Shanghai core definition, and dropping the structurally dependent proxy indicator to show expected discrimination collapse — show genuine methodological self-awareness.

## 3. Weaknesses

The disease mislabeling is the most serious flaw. Novelty is undercut by the 2026 *Nature Cities* paper covering the same phenomenon at greater scale. The core-city matching model conditions on physician reputation/title as both covariate and dominant SHAP predictor (42.6%), risking mediator adjustment rather than confounding. The self-admittedly unvalidated cross-city proxy is reported with two-decimal odds ratios despite 59.6% of its own model discrimination being mechanically driven by the proxy variable.

## 4. Editorial Decision

**Reject.** The uncorrected clinical mislabeling and substantial anticipation by a more rigorous published study leave no viable path to review as submitted. A revision correcting the taxonomy and repositioning against Xiang et al. 2026 could be considered for transfer to *npj Digital Medicine* or *Communications Medicine*.

---

## 5. Suggested Reviewer Expertise

Reviewers should cover: spatial accessibility and concentration modeling in health systems (Gini/HHI-based, two-step floating catchment methods); network-analytic approaches to intercity service-flow data; explainable machine learning (XGBoost/SHAP) applied to health-services tabular data, including circularity and proxy-variable pitfalls; oncology or pulmonology referral-pathway epidemiology, to adjudicate the lung cancer/"lung disease" issue; and China's hierarchical medical system (fenji zhenliao) policy context.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The defining recent contribution is Xiang, Hong, Guo et al., *Nature Cities* (2026), which maps China's intercity telemedicine system as a network and shows dominant hubs capturing disproportionate consultation share while simultaneously extending reach to smaller cities — the same core tension this manuscript documents, but derived from full network topology rather than city-rank shares. Wang, Chen, Liu & Tao, *ISPRS International Journal of Geo-Information* (2025), quantify spatial inequality in healthcare accessibility across the Beijing–Tianjin–Hebei region incorporating intercity patient mobility, directly relevant to this manuscript's unresolved patient-residence gap. Fu, Wang & Dong, *Scientific Reports* (2025), examine how China's hierarchical medical system shapes resource allocation, providing the offline baseline this manuscript's "re-encoding" argument depends on but does not directly test against. Niu & Silva, *Sustainable Development* (2026), apply an XGBoost–SHAP framework to urban health determinants at fine spatial resolution, a close methodological parallel worth engaging on interpretability limits. This manuscript sits adjacent to, rather than clearly ahead of, this literature; its narrower disease-specific and SHAP-based lens is a plausible angle of extension but is not yet argued as one.

## 7. Suggested Reviewer Names

**Network/spatial telemedicine analysis:** B. Xiang, M. Hong, F. Guo (*Nature Cities*, 2026, intercity telemedicine system).

**Health geography / accessibility modeling:** Y. Wang, L. Chen, B. Liu, Z. Tao (*ISPRS Int. J. Geo-Information*, 2025, spatial inequality in Beijing–Tianjin–Hebei healthcare accessibility).

**Chinese hierarchical medical system / health policy:** L. Fu, R. Wang, Y. Dong (*Scientific Reports*, 2025, hierarchical medical system and resource allocation).

**Explainable ML in health/urban systems:** H. Niu (Renmin University of China; *Sustainable Development*, 2026, XGBoost–SHAP urban health determinants).
