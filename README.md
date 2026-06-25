# Trackrad202512456

045975 # Editorial Report: "CBCTRepD enhances clinically grounded CBCT report generation across diverse oral and maxillofacial conditions"

## 1–4. Summary Assessment and Decision

CBCTRepD fine-tunes the existing Hulu-Med-4B backbone for bilingual oral/maxillofacial CBCT report generation, paired with a new 14,816-study, 53-category benchmark. It outperforms general and 3D medical VLM baselines on automatic and diagnostic-entity metrics, and improves human-AI collaborative reporting across three OMR experience tiers, reducing clinically significant omissions. The effort is substantial but not architecturally novel — the encoder, projector, and decoder are reused verbatim from Hulu-Med — so significance rests on the dataset and workflow study, not the model itself.

Two structural problems undercut that claim. The "four centers" are constituent campuses of one Zhejiang University hospital system, evaluated on an internal hold-out of the same 7,408-patient pool; no external site or population was tested, so both the comparative and workflow results demonstrate in-distribution competence rather than generalizability. Second, the reference reports used for training and scoring were authored within that same network, which the paper's own introduction states detects only 41.1–56.7% of incidental findings even after training; ground-truth completeness is never independently adjudicated, so high agreement may partly reflect alignment with a flawed standard rather than correctness.

Two further weaknesses compound this. The AI-assisted arm includes only two senior OMRs, and the manual-tier comparison rests on 20 cases, so tier-stratified claims — including benefit "even among senior OMRs" — are statistically fragile, with no confidence intervals reported for headline figures such as the 129% BLEU-4 gain in novices. The authors' own discussion also flags residual tooth- and site-level localization errors, yet only case-level accuracy is reported, omitting exactly the granularity that drives treatment-planning utility in implantology and endodontics.

**Decision: Reject.** The dataset and workflow-evaluation contribution are genuine, but single-health-system validation and ground-truth circularity are structural rather than revisable within this cohort, and the architecture is too thin to carry the paper on novelty alone. Transfer to *npj Digital Medicine* is recommended.

## 5. Suggested Reviewer Expertise

Reviewers should cover: vision-language architectures for 3D volumetric medical imaging and instruction tuning of multimodal LLM decoders; rotary/2D positional encoding for variable-resolution 3D patch sequences; statistical methodology for multi-rater preference ranking and ordinal quality scoring with repeated-measures correction; oral and maxillofacial radiology with hands-on CBCT reporting experience spanning novice-to-senior training; and clinical workflow integration in endodontics or implantology, where tooth-level localization error has direct treatment consequences.

## 6. State-of-the-Art Literature Review (Past 3 Years)

3D medical report generation has moved quickly: from general 3D LLaVA-style adaptations (M3D, Med3DVLM) to domain-grounded systems such as RadGenome-Chest CT, the CT-RATE/CT-CLIP foundation models, and Li et al.'s brain CT framework — the same lineage CBCTRepD draws on via Hulu-Med. Within dentistry specifically, the relevant comparator set is different, and the manuscript does not engage it. Recent work includes MMOral, a large panoramic-radiograph multimodal instruction benchmark built around four task families — structured attribute extraction, full report generation, visual question answering, and grounded dialogue; a separate oro-dental multimodal dataset comprising checkups from over 4,800 patients, on which the authors fine-tuned Qwen-VL models and evaluated full diagnostic-report generation directly against the same task this manuscript addresses; and OralGPT-Omni, a dental-specific multimodal LLM. None of these is cited or benchmarked against, despite being the closest concurrent work in modality and clinical scope. The manuscript instead compares only against out-of-domain general and 3D medical VLMs, which overstates how uncontested the dental-VLM space currently is and leaves open whether CBCTRepD's margin would hold against domain peers.

## 7. Suggested Reviewers

- **Technical — 3D medical vision-language modeling:** Weidi Xie; Ibrahim Ethem Hamamci
- **Statistical/evaluation methodology:** Jack Gallifant
- **Clinical — oral/maxillofacial CBCT radiology:** Reinhilde Jacobs; Kuo Feng Hung
- **Human-AI collaboration in radiology reporting:** Ryutaro Tanno

## Further Literature

1. **Meng, Z., Hao, J., Dai, X., et al.** DentVLM: a multimodal vision-language model for comprehensive dental diagnosis and enhanced clinical practice. arXiv:2509.23344 (2025). This is the most serious omission in the manuscript. Several authors overlap directly with CBCTRepD (Meng, Hao, Dai, Zhu, Xia, Wu, Liu), and DentVLM reports a bilingual 110,447-image, 2.46-million-VQA dataset across seven 2D oral imaging modalities, with a clinical study showing the model elevates junior dentists' performance to senior level and cuts diagnostic time 15–22% in collaborative use — the same workflow-benefit claim CBCTRepD makes for CBCT, from overlapping authorship. Failing to cite or differentiate from one's own group's directly antecedent work is a transparency problem the editor should raise explicitly with the authors.

2. **Hao, J. et al.** Towards better dental AI: a multimodal benchmark and instruction dataset for panoramic X-ray analysis (MMOral). arXiv:2509.09254 (2025). A 20,563-image, 1.3-million-instance panoramic instruction dataset spanning attribute extraction, report generation, VQA, and grounded dialogue, with an expert-curated benchmark on which even GPT-4o reaches only ~41–43% accuracy. The largest dental-imaging instruction corpus in this window and the most direct 2D comparator dataset the manuscript omits.

3. **Hao, J. et al.** OralGPT-Omni: a versatile dental multimodal large language model. arXiv:2511.22055 (2025). The dental-specialized successor to MMOral, covering eight imaging modalities — including CBCT — and five clinical tasks with chain-of-thought supervision mirroring radiologists' reasoning. Because it already includes CBCT as a modality, it is the single most directly competing system CBCTRepD should have benchmarked against rather than only non-dental 3D medical VLMs.

4. **Li, C.-Y. et al.** Towards a holistic framework for multimodal LLM in 3D brain CT radiology report generation. *Nat. Commun.* **16**, 2258 (2025). DOI: 10.1038/s41467-025-57426-0. Curates the 3D-BrainCT dataset and proposes FORTE, a clinically anchored evaluation scheme built because BLEU/ROUGE failed to track diagnostic quality — the same architecture lineage (Hulu-Med) CBCTRepD inherits, but paired with a metric purpose-built for the modality rather than borrowed wholesale from chest-X-ray literature.

5. **Lv, H., Haq, I., Du, J., et al.** A benchmark multimodal oro-dental dataset for large vision-language models. arXiv:2511.04948 (2025). Comprises 8,775 dental checkups from 4,800 patients over eight years, combining intraoral images and radiographs with full diagnostic-report text to fine-tune Qwen-VL for both anomaly classification and report generation. Its longitudinal, single-population design is a useful methodological contrast to CBCTRepD's cross-sectional, one-CBCT-per-patient cohort.

6. **Zhang, X. et al.** RadGenome-Chest CT: a grounded vision-language dataset for chest CT analysis. arXiv:2404.16754 (2024). Links each report statement to its anatomical region across 25,692 chest CT volumes. This is the closest precedent for the tooth/site-level grounding that CBCTRepD's own discussion flags as a residual weakness, yet the manuscript neither cites this grounding strategy nor attempts an analogous tooth-region linkage.

7. **Hamamci, I. E. et al.** Generalist foundation models from a multimodal dataset for 3D computed tomography. *Nat. Biomed. Eng.* (2026). DOI: 10.1038/s41551-025-01599-y. Extends the CT-RATE lineage toward a generalist 3D CT foundation model rather than a single-region specialist, offering a direct counterpoint to CBCTRepD's choice to narrowly specialize a 4B-parameter decoder to one anatomical region.

048577
# Editorial Report (Condensed)

**Manuscript:** A systematic framework for translating inverse adverse event signals from randomized trials into therapeutic hypotheses
**Section:** Digital Health, *Nature Communications*

---

## 1. Overall Assessment

This manuscript mines ClinicalTrials.gov adverse-event tables for inverse (protective) signals and uses GPT-4o curation plus knowledge-graph, competing-harm, and follow-up-trial layers to build a 278-signal repurposing catalogue. The core idea predates this work — Su & Sanger (*PeerJ*, 2017) used the identical SAE-comparison logic — so this is a scaling and curation exercise, not a conceptual advance. Two flaws dominate: the foundational screen tests 261,285 triplets at P<0.05 with no multiplicity correction, and the framework compares aggregate AE counts without exposure-time data, unable to separate true protection from differential dropout — a limitation the authors themselves call unresolvable with this data source.

## 2. Strengths

The data-engineering scale is genuine: 62,772 trials were reduced through defensible eligibility filters to 5,497 trials and 275,869 triplets. The LLM-curation benchmark is methodologically sound — three models run five times each against dual-expert adjudication, with explicit recall/specificity and rule-trace concordance reporting (GPT-4o: recall 1.00, specificity 0.94). The multi-layer validation architecture (competing-harm filter, knowledge-graph similarity, temporal linkage, endpoint forest plots) is sensibly organized and appropriately hedged as concordance rather than proof.

## 3. Weaknesses

No multiplicity correction is applied across 261,285 simultaneous tests, so a substantial share of the 1,294 candidate signals entering LLM curation may be chance findings; the curation rules test clinical plausibility, not statistical credibility. The top-100 GPT-4o evaluation set is the most statistically extreme, easiest-to-classify subset and is not representative of the harder triplets making up the bulk of the 278-signal catalogue, so reported recall/specificity will not generalize. Differential exposure time and dropout between arms — the central confound for any AE-rate comparison — is acknowledged but never bounded with a sensitivity analysis. The endpoint-concordance validation is circular: all four representative cases are established pharmacology, so no genuinely novel candidate was tested to the same rigor.

## 4. Editorial Decision

**Reject.** The uncorrected multiplicity problem and the self-acknowledged, unresolvable exposure-time confound undermine the causal interpretability of "inverse AE = candidate efficacy," and validation demonstrates recovery of known pharmacology rather than novel discovery. Resolving this would require individual-level trial data the framework forgoes by design.

## 5. Suggested Reviewer Expertise

Pharmacoepidemiology and competing-risk methodology for aggregate-level RCT safety data, with specific attention to differential dropout and exposure-time confounding; statistical methodology for multiple-hypothesis testing and false-discovery control in large-scale screening (genomics- or claims-data-adjacent expertise transfers well); LLM-assisted biomedical text classification and evaluation, including prompt-sensitivity and out-of-distribution generalization of LLM-as-curator pipelines; biomedical knowledge-graph construction and embedding-based similarity methods for drug-disease plausibility assessment; and clinical pharmacology of cardiometabolic and cardiorenal agents (SGLT2 inhibitors, mineralocorticoid receptor antagonists) to judge whether the case-study signals represent genuinely new hypotheses or already-described class effects.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The specific idea of mining ClinicalTrials.gov AE tables for repositioning signals predates this manuscript by nearly a decade: Su and Sanger described a method of drug repositioning by mining ClinicalTrials.gov, extracting serious adverse event data from randomized trials and ranking drugs where the treatment arm had fewer predefined serious adverse events than the control arm to generate repositioning hypotheses. The present manuscript's core statistical logic is the same idea scaled up roughly 1,700-fold in trial count, with an LLM curation layer added; this lineage should be explicitly engaged with in the Introduction rather than folded into a generic citation cluster (refs 9-10), since it is the most direct prior precedent for the entire framework.

Methodologically, two recent strands are relevant. First, LLM-assisted safety-literature screening has been benchmarked directly against human reviewers in pharmacovigilance contexts: a comparative study of GPT-3.5, GPT-4, and Claude2 for categorizing medical publications as relevant or irrelevant to safety-signal reviews reported 93% reproducibility, 97% sensitivity, and 67% specificity. The present manuscript's GPT-4o specificity (0.94) on its top-100 evaluation set is notably higher, which is more likely attributable to the non-representative, easy-case composition of that evaluation set than to a genuine reliability advantage, and the discrepancy with this prior benchmark deserves direct discussion. Second, LLM-augmented knowledge-graph repurposing has advanced substantially in 2025: LLaDR (EMNLP Findings 2025) fine-tunes knowledge-graph embeddings using LLM-derived semantically enriched entity representations to improve drug-disease link prediction, and DrugKLM integrates knowledge-graph structure with LLM-based mechanistic reasoning for therapeutic prioritization, showing that confidence scores align with transcriptional phenotypes linked to clinical outcomes across multiple cancer types. Both use LLM reasoning to add mechanistic grounding to graph-based candidate generation, which is precisely what the present manuscript's knowledge-graph layer lacks: condition-event cosine similarity in an epidemiological co-occurrence graph establishes disease-relatedness, not mechanism, and the manuscript should engage with these mechanistic-grounding approaches as a methodological benchmark it falls short of, rather than only the descriptive plausibility check it currently performs.

## Suggested Reviewer Names

**Pharmacoepidemiology / competing-risk methodology:** Sebastian Schneeweiss; Til Stürmer; Shirley V. Wang; Miguel A. Hernán

**Multiple-testing / large-scale signal-detection statistics:** Patrick B. Ryan; Manfred Hauben; Yoav Benjamini; Jeffrey T. Leek

**LLM-assisted biomedical text classification and evaluation:** Qingyu Chen; Zhiyong Lu; Hua Xu; Yifan Peng

**Biomedical knowledge-graph and embedding methods:** Marinka Zitnik; Russ B. Altman; Sergio E. Baranzini

**Cardiometabolic / cardiorenal clinical pharmacology:** Rajiv Agarwal; Bertram Pitt; Javed Butler; Muthiah Vaduganathan

---

## Further Literature (Past 3 Years, Closely Scoped)

1. **Shuey MM, Lee KM, Keaton J, Khankari NK, Breeyear JH, Walker VM, Miller DR, Heberer KR, Reaven PD, Clarke SL, Lee J, Lynch JA, Vujkovic M, Edwards TL.** A genetically supported drug repurposing pipeline for diabetes treatment using electronic health records. *EBioMedicine*. 2023;94:104674. doi:10.1016/j.ebiom.2023.104674.
 Builds a comparably structured multi-stage repurposing pipeline (genetic association → drug-target mapping → EHR self-controlled case series → Mendelian randomization) for a single disease area. Unlike the manuscript under review, every candidate surviving curation is carried through individual-level causal validation rather than left at the level of aggregate trial counts — a direct illustration of the exposure-time and confounding control this manuscript lacks.

2. **Yan C, Grabowska ME, Dickson AL, Li B, Wen Z, Roden DM, Stein CM, Embí PJ, Peterson JF, Feng Q, Malin BA, Wei WQ.** Leveraging generative AI to prioritize drug repurposing candidates for Alzheimer's disease with real-world clinical validation. *npj Digit Med*. 2024;7:46. doi:10.1038/s41746-024-01038-3.
 Uses an LLM (GPT-4) strictly as a candidate-generation/prioritization tool, then validates every shortlisted candidate against incident-disease risk in two independent real-world cohorts (Vanderbilt, All of Us). This is the closest precedent for using an LLM as a hypothesis "curator," and it shows what independent outcome-level validation of LLM output looks like — a step the manuscript under review performs only for already-known drug-effect pairs (finerenone, SGLT2 inhibitors, metformin).

3. **Li D, Wu L, Zhang M, Shpyleva S, Lin YC, Huang HY, Li T, Xu J.** Assessing the performance of large language models in literature screening for pharmacovigilance: a comparative study. *Front Drug Saf Regul*. 2024;4:1379260. doi:10.3389/fdsfr.2024.1379260.
 Benchmarks GPT-3.5, GPT-4, and Claude2 against human-labeled abstracts for safety-signal triage, reporting 97% sensitivity but only 67% specificity, with explicit testing of prompt-sensitivity and N-shot reproducibility. This more representative benchmark directly undercuts the credibility of the manuscript's 0.94 GPT-4o specificity, which was measured on an unrepresentative, easy-case top-100 evaluation set rather than a random sample of the full candidate pool.

4. **Hauben M, Rafi M, Abdelaziz I, Hassanzadeh O.** Knowledge graphs in pharmacovigilance: a scoping review. *Clin Ther*. 2024;46(7):544-554. doi:10.1016/j.clinthera.2024.06.003.
 Systematically reviews 47 peer-reviewed studies using knowledge graphs for ADR/drug-drug-interaction signal detection and finds sparse comparison against legacy disproportionality methods across the field. The manuscript under review has the same gap: its knowledge-graph layer is validated only by internal Mann-Whitney comparison of condition-event similarity, with no comparison against a legacy plausibility-screening baseline.

5. **Xiang C, Ma T, Fu X, Liu Y, Song B, Zeng X.** From Knowledge to Treatment: Large Language Model Assisted Biomedical Concept Representation for Drug Repurposing. *Findings of the Association for Computational Linguistics: EMNLP 2025*, pp.13967-13982. doi:10.18653/v1/2025.findings-emnlp.751.
 Uses LLM-derived semantic embeddings to enrich knowledge-graph entity representations for drug-disease link prediction (LLaDR), benchmarked against TransE, RotatE, ComplEx, and other KG-embedding baselines. This is the current technical standard for LLM+KG integration in repurposing; the manuscript's knowledge-graph layer instead uses plain Word2Vec random-walk embeddings for descriptive similarity only, with no embedding-model baseline comparison.

6. **Toonsi S, Schofield PN, Hoehndorf R.** Causal knowledge graph analysis identifies adverse drug effects. *Bioinformatics*. 2026;42(1):btaf661. doi:10.1093/bioinformatics/btaf661.
 Integrates knowledge graphs with structural causal models to identify adverse drug effects from UK Biobank and MIMIC-IV, explicitly adjusting for graph-derived confounders, then validates novel findings via a drug-repurposing side-effect-similarity task. This is the most directly comparable contemporary framework attempting AE-to-repurposing translation, and it solves with formal causal adjustment precisely the confounding problem (informative dropout/exposure time analog) that the manuscript under review leaves unresolved.

048657

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

049233

I'll load the editorial skill and review the manuscript thoroughly before drafting the report.Now let me search for current literature to properly situate this manuscript — specifically biomedical knowledge graphs, heterogeneous GNN/Transformer biomarker prediction, and MoE-based architectures in this domain.This confirms PrimeKG is the central, directly competing prior art the manuscript must engage with. Let me check one more angle — explainability via attribution-guided subgraph paths and KG-based GNN explainability, since that's a specific selling point.I have enough to ground the literature section. Now drafting the full report.

---

# Editorial Report: BioGT — A Knowledge Graph-Grounded Predictor for Pan-Disease, Multi-Layer Biomarker Discovery

## 1. Overall Assessment

The manuscript presents BioGT, a two-part system comprising BioGT-KG, a disease-centric heterogeneous knowledge graph with 624,810 nodes and 4,139,816 edges across 11 entity types and 38 relation types, and BioGT-Predictor, a dual-stream model combining an edge-weighted heterogeneous graph convolutional network (HGCN), a Multi-head Latent Attention (MLA) Transformer with mixture-of-experts (MoE) routing, and a weighted-fusion MLP head, trained as four independent modality-specific link predictors for DNA, RNA, protein, and metabolite biomarker association with disease nodes.

The central claim is that jointly modeling local graph topology and long-range semantic dependency yields a generalizable, pan-disease, multi-layer biomarker prioritization tool, evidenced by random-split benchmarking against GCN, GAT, and Transformer baselines, 10-fold cross-validation, ablation, fusion-strategy comparison, two holdout generalization settings, and two case studies (pheochromocytoma DNA, Parkinson disease protein). The architecture is a competent but largely incremental combination of existing components — HGCN message passing, MLA (a compression technique originating in large language model serving, here repurposed without clear justification for a 64-dimensional embedding space), and MoE feed-forward routing — assembled around a knowledge graph that is conceptually a narrower, disease-biomarker-focused analogue of PrimeKG. The two issues most likely to drive the decision are: (1) absence of any comparison against PrimeKG, Hetionet, or other established biomedical KG-embedding baselines (DistMult, RotatE, ComplEx, R-GCN) that would establish whether BioGT-KG's evidence-aware weighting scheme and dual-stream encoder actually outperform standard KG embedding pipelines on the same task; and (2) the negative-sampling protocol (k=1 random negative per positive, drawn from the same biomarker type) is weak and likely inflates all reported AUC-PRC/AUC-ROC figures, given that biomedical link prediction is known to be highly sensitive to negative sampling strategy.

## 2. Strengths

The evidence-aware edge weighting scheme in BioGT-KG is a genuine, well-specified contribution. Assigning continuous weights derived from curated evidence levels (e.g., UniProt Protein Existence levels 0.2–1.0, HPO evidence codes 0.5/1.0, MarkerDB clinical-validation weights of 1.0) and propagating them directly into HGCN message passing (Eq. in §4.2, $h_u^{(l)} = \phi(\sum_r \sum_{v \in \mathcal{N}_r(u)} w_{vu} W_r^{(l)} h_v^{(l-1)})$) is a more principled treatment of source heterogeneity than naive multi-database concatenation, and is explicitly validated by the ablation showing distinct, non-redundant contributions from HGCN, Transformer, and MoE branches (Fig. 3f).

The generalization battery is more rigorous than is typical for this literature. Beyond random-split cross-validation, the authors impose a direct disease-biomarker association holdout (excluding the very edges being predicted) and an 11-category disease-etiology holdout, and report signed relative performance changes rather than raw numbers alone. The finding that ranking metrics (AUC-PRC, AUC-ROC) are preserved under holdout while threshold-dependent accuracy and F1 degrade is a specific, falsifiable, and biologically interpretable result rather than a generic robustness claim.

The dual explanation strategy (embedding-weighted Dijkstra shortest path versus gradient-attribution-guided subgraph search, with explicit path selection by cumulative cost) is methodologically more transparent than typical post-hoc GNN explainability add-ons (GNNExplainer-style masking), because it is run independently with two distinct mechanisms and the lower-cost path is retained by an explicit, auditable rule rather than a single uninspectable attention map.

The pheochromocytoma case study is grounded in real, checkable biology: the top six DNA candidates (SDHB, VHL, SDHD, RET, TMEM127, NF1) are bona fide pheochromocytoma/paraganglioma susceptibility genes, and the manuscript correctly distinguishes direct biomarker-level evidence from indirect mechanistic support (KIF1B) and exploratory candidates (PDZK1IP1), which suggests the evidence-categorization framework in Table 3 was applied conscientiously rather than retrofitted to favor the model.

## 3. Weaknesses

No comparison is made against any established biomedical knowledge-graph or KG-embedding baseline. PrimeKG (Chandak et al., 2023, cited in the manuscript's own reference list) integrates 20 resources into over 4 million relationships across ten biological scales and is the de facto standard precision-medicine KG; BioGT-KG is materially narrower in scope (15 sources, no drug-disease "indication/contraindication" structure) yet the manuscript never benchmarks BioGT-Predictor against PrimeKG-based pipelines, against standard KG embedding methods (TransE, DistMult, RotatE, ComplEx), or against R-GCN. The three baselines used (GCN, GAT, vanilla Transformer) are generic graph backbones, not knowledge-graph-specific competitors, so the claimed improvements (e.g., +32.58% AUC-PRC for RNA) cannot be situated against the actual state of the art in biomedical KG link prediction.

The negative sampling scheme is a serious and likely outcome-altering weakness. Section §4.4 states k=1 random negative per positive pair, sampled by pairing the same disease node with a random candidate of the same biomarker type, excluding known positives. This is the weakest possible negative sampling design for KG link prediction; it is well established in the KG completion literature that random negatives produce easy negatives and inflated AUC-PRC/AUC-ROC relative to harder negative sampling strategies (e.g., type-constrained, degree-matched, or self-adversarial negatives as used in RotatE). With only one negative per positive and no sensitivity analysis across k or sampling strategy, every headline metric in Figs. 2–4 is potentially optimistic by an unknown and unreported margin.

Use of MLA — a technique introduced specifically to reduce KV-cache memory in autoregressive LLM inference at scale (DeepSeek-V2, cited in ref. list) — to replace self-attention in a 64-dimensional, three-block Transformer encoder over small sampled node sequences is conceptually unmotivated. MLA's benefit is a serving-time memory optimization for long-context generation; in this setting, with $d_\text{model}=64$ and no autoregressive decoding or long token sequences, the manuscript supplies no ablation isolating MLA's effect versus standard multi-head attention, so it is impossible to know whether MLA contributes anything beyond standard attention at this scale, or whether it is included primarily for novelty signaling.

The disease-category holdout experiment, despite being a real strength in design, surfaces a result the manuscript underweights: DNA prediction's four-metric mean drops from 0.9203 (random split) to 0.8921 (holdout), with the degenerative age-related disease category showing accuracy and F1 reductions of −0.0620 and −0.0934. Combined with the direct-association holdout showing a 21.69% relative DNA decrease, this indicates DNA-layer predictions — arguably the most clinically actionable biomarker class — are the least transferable and most dependent on directly observed evidence already in the graph, which undercuts the "pan-disease generalization" framing for exactly the modality where false positives carry the highest downstream cost.

The Parkinson disease case study explicitly acknowledges that one critical path segment (Drug niclosamide → Biological process cellular response to oxidative stress) is a "virtual edge" introduced by cosine-similarity thresholding in the attribution-guided subgraph search, not a curated graph edge. The manuscript is commendably transparent about this, but it means the most narratively complete explanatory path in the entire case-study section is partially model-inferred rather than evidence-grounded, and no quantification is given of how often virtual edges appear in explanation paths across the broader candidate set, leaving open whether this case was cherry-picked for its coherence.

## 4. Editorial Decision

**Reject.** The absence of any comparison against PrimeKG or standard KG-embedding baselines, combined with a single-random-negative sampling protocol known to inflate link-prediction metrics, means the manuscript's central performance claims cannot be distinguished from artifacts of an easy benchmark design; these are structural evaluation-design flaws rather than addressable presentational weaknesses, and resolving them would require a substantially redesigned benchmarking section, not a revision.

## 5. Suggested Reviewer Expertise

Reviewers should have demonstrated expertise in biomedical knowledge graph construction and embedding methods (specifically PrimeKG, Hetionet, or comparable precision-medicine KGs) to assess the adequacy of baseline comparisons; negative sampling strategies and evaluation protocols for knowledge graph completion and link prediction; heterogeneous graph neural network architectures (R-GCN, HGT, HAN) for biomedical applications; mixture-of-experts and efficient-attention architectures (to assess whether MLA is appropriately motivated at this model scale); and clinical genetics of pheochromocytoma/paraganglioma susceptibility syndromes and Parkinson disease molecular pathology, to evaluate the biological plausibility claims in the two case studies.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The dominant precision-medicine knowledge graph remains PrimeKG a knowledge graph integrating 20 high-quality resources to describe 17,080 diseases with over 4 million relationships spanning ten major biological scales, including disease-associated protein perturbations, biological processes and pathways, and the full range of approved and experimental drugs, and derivative efforts such as PollyKG have specifically targeted PrimeKG's static-snapshot limitation by building continuously updated KG pipelines. A 2025 Bioinformatics Advances benchmarking study evaluated 42 techniques including nine generic heterogeneous graph neural networks across eight biomedical link-prediction datasets, providing exactly the kind of baseline landscape BioGT fails to engage with. On explainability, recent work has moved toward path-based and attribution-cluster explanations rather than single attention maps: XAIPath combines GNN-based predictions with a post-hoc interpretability layer that extracts simple paths between drug and disease nodes and clusters them via MinHash similarity to represent alternative mechanistic hypotheses, and case-based reasoning frameworks evaluated on the MIND network pursue similar mechanistic-path goals. BioGT's dual shortest-path/attribution-subgraph explanation strategy is a reasonable contribution to this space but is not benchmarked against any of these contemporaneous explainability frameworks, and the manuscript's introduction cites only CardioKG and HGANMDA as related deep-learning-on-KG work, omitting the PrimeKG lineage entirely despite using it in the reference list for an unrelated methodological citation. This is the most consequential omission: the paper positions itself as filling a gap in pan-disease, multi-layer biomarker prediction that PrimeKG-adjacent tools already substantially address, and does not engage with why BioGT-KG's narrower, disease-biomarker-specific schema should be preferred over extending PrimeKG's existing infrastructure.

## Suggested Reviewers' Names

**KG/precision-medicine knowledge graphs:** Marinka Zitnik; Payal Chandak; Michelle M. Li; Kexin Huang

**Heterogeneous GNN / link prediction methodology:** Zaiwen Feng; Junwei Hu; Wen Zhang; Hong-Yu Zhang

**MoE / efficient Transformer architectures in biomedical ML:** Zexuan Zhong; Marinka Zitnik (cross-listed for GNN+MoE work); Ziniu Hu

**Clinical genetics — pheochromocytoma/paraganglioma and Parkinson disease:** Hartmut P.H. Neumann; Karel Pacak; Anthony H.V. Schapira; Mark R. Cookson

049243
# Editorial Report: "Wearable Single-Lead ECG Detects Fine-Grained Structural Heart Disease Through Echo-Report Supervision"

## 1. Overall Assessment

The manuscript presents AnyECG-Echo, a contrastive pre-training framework that aligns single-lead (Lead I) ECG embeddings with physician-authored echocardiography reports via a frozen MedCPT text encoder, then fine-tunes a linear head to detect 13 fine-grained structural heart disease (SHD) subtypes. The central claim is that this report-supervised paradigm scales to geographically independent external validation (SHTMU, n=16,621), achieves broader diagnostic granularity than prior single-lead work, and yields outputs that double as physiologically grounded digital biomarkers correlating with LVEF and wall thickness.

The core architectural and training paradigm — contrastive alignment of Lead I ECGs with free-text echo reports for SHD screening — is not novel; it is a direct extension of Wearable-Echo-FM (Knight et al., Eur Heart J Digit Health 2026), which established this exact pairing (CNN ECG encoder, RoBERTa-family text encoder, InfoNCE/CLIP-style loss) on a larger single-institution cohort. The genuine increments here are external geographic validation, expansion from 3 to 13 subtype labels, and the Shapley/digital-biomarker interpretability analyses. Whether these increments clear a Nature Communications bar, rather than constituting an incremental extension of an already-published architecture, is the question that will most influence the decision. A second material concern is that the external AUROCs for atrial pathologies (LA enlargement 0.610–0.665, ascending aortic dilation 0.610–0.685) are near-chance to weak across all three cohorts, undermining the "13 fine-grained subtypes" headline claim.

## 2. Strengths

The geographically independent external validation (SHTMU, 140 km from the development site, n=16,621) is a genuine advance over Wearable-Echo-FM, which was validated only within a single health system (Yale New Haven). Demonstrating AUROC 0.806–0.906 retention for mitral stenosis, global heart enlargement, and reduced LV systolic function across this external cohort is the strongest evidence in the paper.

The data efficiency analysis (Fig. 4) is methodologically clean: scaling from 100 to 12,726 patients with a clear asymptotic plateau at 50% of the development cohort, and exceeding 75% of full-dataset performance with only 100 labeled samples, is a defensible and reproducible demonstration of the value of contrastive pre-training for label-scarce fine-tuning.

The dual-axis interpretability analysis (Fig. 2) — population-level median-beat morphology compared against individual-level occlusion-based Shapley attribution across six physiologically defined ECG segments — is a reasonable and appropriately conservative attempt at mechanistic validation, and the directional alignment with known electrophysiology (e.g., QRS/ST attribution for pericardial effusion and RV enlargement, P-wave and QRS for mitral stenosis) is internally consistent.

The decision curve analysis and number-needed-to-screen framing (Fig. 5) translates discrimination metrics into a clinically interpretable deployment argument, which is a useful addition that most comparator papers in this space omit.

## 3. Weaknesses

The principal comparator, Wearable-Echo-FM, is cited only narrowly (Table 2, Introduction) without being engaged on its central limitation — single-site validation — being the same limitation this manuscript claims to solve, yet the manuscript does not discuss why an architecturally near-identical approach, applied to a different population, constitutes a distinct methodological contribution rather than a replication with a new dataset and added labels.

Per-label AUROC comparisons against EchoNext, EchoNext-Mini, AI-ECG VHD, and Wearable-Echo-FM (Table 2) are explicitly acknowledged as cross-cohort, not head-to-head, yet the abstract and data-efficiency narrative ("5 to 33 times fewer pairs," "match or exceed... models trained on orders-of-magnitude more data") draw quantitative superiority conclusions from these same numbers. This is an internal inconsistency: the limitation is disclosed in prose but not honored in the framing of the central claim.

Three of 13 labels (aortic regurgitation, ascending aortic dilation, LA enlargement) fall into the AUROC<0.65 range in the external cohort, and the manuscript's own discussion attributes this to "limited discriminative power for atrial pathologies" from the single-lead configuration. Reporting these subtypes as part of "13 fine-grained subtypes spanning myocardial, chamber, valvular, and great-vessel pathologies" in the abstract without immediately flagging that nearly a quarter of them are near-uninformative is an overstatement of diagnostic breadth.

The retrospective, referral-enriched cohort design (patients clinically referred for echocardiography, not general-population screening) is explicitly acknowledged as a limitation in the Discussion, but the community-prevalence NNS recalculation in Figure 5 is then presented as supporting "population-scale screening" feasibility despite having no prospective validation in an asymptomatic population. The 41.5% missing sex data in cohort subsets further weakens the demographic robustness claims that are foregrounded in the subgroup analysis.

The temporal validation set is acknowledged by the authors themselves to be an internal hold-out rather than a true distributional shift, since it shares institutional infrastructure, hardware, and physician workforce with the development cohort; this honest disclosure is appropriate but means the "three distinct validation tiers" framing in the Introduction overstates the independence of two of the three tiers.

## 4. Editorial Decision

**Reject.** The manuscript's core contribution — contrastive single-lead ECG/echo-report alignment for SHD screening — has already been established by Wearable-Echo-FM, and the present work's increments (external validation at one additional site, expanded label set, post-hoc interpretability) are evolutionary rather than substantial enough to meet the bar of a clear, reproducible, clinically meaningful advance, particularly given that the abstract's quantitative claims rely on cross-cohort comparisons the authors themselves caution against treating as direct. The near-chance performance on a quarter of the claimed 13 subtypes in external validation further undercuts the central "fine-grained, clinically deployable" framing. This is suitable for transfer to a specialty venue such as *npj Digital Medicine* or the *European Heart Journal – Digital Health*, where incremental extension of an established paradigm with added external validation is a more appropriate fit.

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in: (1) multimodal contrastive learning for time-series/text alignment (CLIP-style or InfoNCE objectives applied to physiological signals); (2) single-lead and wearable ECG signal processing and deep learning architecture design (ResNet/CNN-based encoders); (3) Shapley-value and occlusion-based interpretability methods for time-series models; (4) clinical echocardiography and ASE/EACVI valvular and chamber-quantification guidelines, to adjudicate the validity of the rule-based NLP label extraction; and (5) cardiology with specific experience in population-level SHD screening program design and decision-curve/NNS-based clinical utility assessment.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field of AI-ECG for SHD detection has moved rapidly over the past 18 months. Poterucha et al. (Nature, 2025) introduced EchoNext, a 12-lead model trained on over 1.2 million ECG-echo pairs across an eight-hospital system with three external sites (Montreal Heart, Cedars-Sinai, UCSF), reporting composite SHD AUROC of 0.852 and outperforming cardiologists in a prospective deployment; this remains the benchmark for scale and prospective clinical impact. Hughes et al. (NEJM AI, 2026) released EchoNext-Mini, a lighter 12-lead baseline on 100,000 pairs intended for resource-constrained benchmarking. Knight et al. (Eur Heart J Digit Health, 2026) published Wearable-Echo-FM, contrastively pre-training single-lead (Lead I) ECG and RoBERTa-based echo-report encoders on 194,551–274,057 pairs from Yale New Haven Health System, targeting LVSD, diastolic dysfunction, and composite SHD — this is architecturally the direct precursor to the present manuscript and was validated only within one health system. Separately, valvular-specific AI-ECG work has advanced via Liang et al. (Eur Heart J, 2025), an international multi-cohort study predicting regurgitant valvular disease, and prior multi-center work (Vaid et al., Commun Med 2023) on left heart valvular dysfunction from 12-lead ECG.

Against this landscape, the present manuscript's distinguishing claims are external geographic validation for the single-lead contrastive paradigm and an expanded 13-label taxonomy; neither is unprecedented in isolation (EchoNext provides external multi-site validation at far greater scale; Wearable-Echo-FM established the single-lead contrastive method), and the manuscript does not engage with the international, multi-cohort valvular AI-ECG literature when contextualizing its valvular subtype results (aortic stenosis, mitral regurgitation, mitral stenosis), an omission reviewers should require the authors to address.

## Suggested Reviewer Names

**Multimodal contrastive learning / representation learning for clinical time-series:** Rohan Khera (Yale, senior author of Wearable-Echo-FM and related AI-ECG foundation model work); Pierre Elias (Columbia, EchoNext senior author); Zachi Attia (Mayo Clinic, AI-ECG architecture).

**Single-lead/wearable ECG signal processing:** Evangelos Oikonomou (Yale, co-author Wearable-Echo-FM); Geoffrey Tison (UCSF, AI-ECG external validation expertise, EchoNext external site); Timothy Poterucha (Columbia/NYP, EchoNext first author).

**Echocardiography and valvular/chamber quantification guidelines:** Catherine Otto (University of Washington, ASE/ACC valvular guideline authorship); Yuan Liang or co-authors of the international regurgitant VHD AI-ECG study (Eur Heart J 2025).

**Interpretability methods for physiological deep learning models:** James Zou (Stanford, ML interpretability in clinical models); or a Shapley/occlusion-attribution methods specialist with cardiology ECG experience.

050141
I'll consult the editorial skill file first to ensure I follow the established format exactly.Now let me search for the most relevant, recent competing literature before writing the State-of-the-Art section.This found two highly relevant, directly competing pieces: the Christophe et al. (2026) arXiv preprint already cited by the manuscript itself, and a closer hit — "When Correct Beliefs Collapse: Epistemic Resilience of LLMs under Clinical Pressure" — which appears to address almost exactly the manuscript's "unjustified rejection" concept under a different name. Let me pull that one directly.This is decisive. There is a substantial, very recent, directly competing literature — including a paper the manuscript's own authors did not cite (Med-Stress/RBED, Xiao et al. 2026), Fanous et al.'s SycEval progressive/regressive sycophancy framework, and Celebi et al.'s PARROT framework — all measuring essentially the same "abandonment of correct belief under doubt/pressure" phenomenon this manuscript calls "unjustified rejection." This materially undercuts the novelty claim. I have what I need.

---

# Editorial Report

**Manuscript:** "Epistemic framing alters accuracy of LLMs for medical second opinions" (Reis et al.)

## 1. Overall Assessment

This manuscript tests whether physician epistemic framing — confirmation-seeking versus contradiction-seeking, applied to correct or incorrect prior hypotheses — alters the diagnostic accuracy of three frontier LLMs (Claude Opus 4.7, Gemini 3.1 Pro Preview, GPT-5.5) on 499 MedQA-derived vignettes. The central finding is that doubt expressed toward a correct hypothesis (C3) drops accuracy from 93.79% to 88.51% (OR 0.51, 95% CI 0.43–0.61), driven by 86 "unjustified rejection" events, while confirmation-seeking toward an incorrect hypothesis (C2) leaves accuracy statistically unchanged (OR 0.99).

The design is clean and the statistics are competently executed, but the central claim — that "abandonment of correct hypotheses under doubt" is the dominant, underappreciated sycophancy failure mode — is not new. As detailed in Section 6, near-identical phenomena have already been named and quantified by at least three concurrent 2025–2026 papers, one of which the authors do not cite. The manuscript's contribution is a controlled factorial isolation of this effect using static MedQA vignettes rather than multi-turn pressure dialogues; whether this constitutes a sufficient methodological advance over the existing multi-turn stress-test literature is the question that will determine the decision.

## 2. Strengths

The factorial design is genuinely well-constructed. By crossing hypothesis correctness with epistemic framing and adding a neutral baseline (C0) and negative control (C4), the authors isolate the causal effect of framing while holding clinical content fixed — a stronger design than the single-condition sycophancy probes common in this literature (e.g., Ibrahim et al., ref. 9). The inclusion of C4 (doubt toward an incorrect hypothesis) as a "beneficial skepticism" check, showing a modest accuracy gain (93.72% to 94.72%), strengthens the causal interpretation by demonstrating the framing effect is bidirectional and not an artifact of prompt length or complexity.

The preregistration on OSF, with two explicitly flagged deviations (cluster-robust logistic regression instead of mixed-effects, and the stricter paired-transition definition of unjustified rejection), is a transparency standard this literature frequently lacks. The case-clustered logistic regression with Holm-adjusted p-values for the two co-primary contrasts (C2 vs. C0, C3 vs. C0) is the statistically correct choice for repeated within-case measurements and avoids the inflated Type I error common when treating 7,485 responses as independent.

The exploratory stratification by case difficulty (442 "clear" vs. 57 "ambiguous" cases) is a useful diagnostic. Showing that unjustified rejection occurs in 4.6% of clear cases but 32.1% of ambiguous baseline-correct cases supports the more clinically important claim that framing vulnerability concentrates exactly where decision support is most needed — this is the paper's most novel empirical observation and is underexploited in the current framing.

## 3. Weaknesses

The core phenomenon — models abandoning a correct initial answer under user-expressed doubt or pressure — is not new and is not adequately situated against concurrent work. Christophe et al. (arXiv:2601.18334, already cited as ref. 18) directly measures this via an "Adjusted Sycophancy Score" across Qwen-3 and Llama-3 families. Fanous et al.'s SycEval framework (arXiv:2502.08177, not cited) explicitly distinguishes "progressive" from "regressive" sycophancy in clinical advice under rhetorical pressure. Most critically, a contemporaneous preprint, Xiao et al., "When Correct Beliefs Collapse: Epistemic Resilience of LLMs under Clinical Pressure" (arXiv:2605.23932, not cited), uses a structurally similar paradigm — tracking belief decay from an initially correct diagnosis under escalating pressure across nine frontier models — and even proposes mitigations (RBED, R-FT). The manuscript's "unjustified rejection" is this same construct under a different label. Without engaging this paper directly, the claim that this failure mode is underrecognized in the literature is not defensible.

The single-turn, static-prompt design is a real limitation that the authors acknowledge (lines 315–329) but underweight in the discussion. Med-Stress and SycEval both use multi-turn, escalating pressure, which is closer to how doubt is actually expressed in clinical dialogue (a physician rarely states doubt once and stops). The manuscript's C3 condition is a single-shot expression of doubt; it is unclear whether the 5.28-point accuracy drop reflects a robust framing effect or a more superficial artifact of how the doubt sentence was lexically constructed for this one-shot probe. No paraphrase or wording-robustness check is reported.

The clinical realism of the case-difficulty result is undercut by sample size: only 57 of 499 cases are "ambiguous," and the ambiguous-case unjustified rejection denominator is 78 baseline-correct observations. A 32.1% rate on n=78 carries wide uncertainty that is not reported (no CI given for this specific exploratory stratification), and the paper should not lean on this figure as heavily as the discussion implies without quantifying it.

The model selection (Opus 4.7, Gemini 3.1 Pro Preview, GPT-5.5) is reasonable but narrow given that Med-Stress and Christophe et al. both run open-weight model families (Qwen-3, Llama-3) at multiple scales, which allows scaling-law conclusions this manuscript cannot make. Three closed frontier models at one point in time, as the authors themselves note (lines 322–325), limits generalizability and is exactly the design the competing literature has already moved past.

## 4. Editorial Decision

**Reject.** The experimental design is sound and the statistics are correctly executed, but the central contribution — quantifying sycophantic abandonment of correct clinical beliefs under doubt — has been independently and more comprehensively demonstrated in at least three concurrent papers, including one (Xiao et al., Med-Stress) using a more realistic multi-turn pressure paradigm and proposing mitigations this manuscript does not. This is a non-revisable novelty deficit, not an addressable methodological weakness; no amount of additional analysis on the existing 499-case static dataset will resolve the overlap with Med-Stress's escalating-pressure framework. The paper may be suitable for a more specialized venue (e.g., npj Digital Medicine) if substantially repositioned around the case-difficulty/ambiguity interaction, which is the one finding not already well covered elsewhere.

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in: (1) multi-turn LLM robustness and belief-stability evaluation under user pressure, specifically familiarity with stress-test frameworks such as SycEval or Med-Stress; (2) causal/factorial experimental design for LLM behavioral evaluation, including cluster-robust inference for repeated within-case measurements; (3) clinical reasoning benchmarks derived from MedQA/USMLE-style vignettes and their limitations relative to real clinical dialogue; (4) RLHF/preference-optimization mechanisms underlying sycophancy, to assess whether the manuscript's mechanistic framing is accurate; and (5), clinically, a physician with experience in diagnostic second-opinion workflows or clinical decision support deployment, to evaluate the ecological validity of the C1–C4 framing manipulations.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Medical LLM sycophancy has moved rapidly from single-turn compliance studies (Sharma et al. 2023; Ibrahim et al. 2026, cited as ref. 9) toward dynamic, pressure-based evaluation frameworks. Fanous et al.'s SycEval (2025) introduced progressive/regressive sycophancy categories specifically for clinical advice and found citation-based rebuttals most effective at inducing harmful belief flips. Celebi et al. introduced the PARROT framework to evaluate how sycophancy impacts clinical reasoning across medical subtasks, finding that models often abandon correct diagnostic paths when prompted with incorrect user beliefs — a near-exact restatement of this manuscript's "unjustified rejection" finding. Most directly competing is Xiao et al.'s Med-Stress (arXiv:2605.23932), which identifies a knowledge-robustness gap in which high initial diagnostic accuracy does not guarantee belief stability under escalating multi-turn clinical pressure, and proposes inference-time and fine-tuning defenses (RBED, R-FT) that substantially mitigate the failure. Christophe et al. (2026, already cited as ref. 18) build an "Adjusted Sycophancy Score" correcting for stochastic model instability and show a clear scaling trajectory for resilience across open-weight model families.

Against this landscape, the present manuscript's static, single-shot factorial design is a methodological step backward relative to Med-Stress and SycEval's multi-turn pressure paradigms, even though its internal causal isolation (via C0–C4) is cleaner for the narrow question of one-shot framing. The manuscript does not engage Xiao et al. or Fanous et al. at all, and cites Christophe et al. only in passing without addressing the direct conceptual overlap. The authors should reposition the paper around what is genuinely undercovered elsewhere — the interaction between case ambiguity and framing sensitivity — and explicitly differentiate "unjustified rejection" from the now-established "belief collapse under clinical pressure" construct, or risk the paper reading as a less rigorous replication of work already in print or preprint.

## 5. Suggested Reviewers' Names

**Multi-turn LLM robustness / sycophancy evaluation:** Aaron Fanous (Stanford); Lujain Ibrahim (Oxford Internet Institute); Myra Cheng (Stanford).

**Clinical AI evaluation / diagnostic reasoning benchmarks:** Daniel McDuff (Google Research); Ethan Goh (Stanford, Limbic/AI-CDS trials); Adam Rodman (Beth Israel Deaconess, clinical reasoning with LLMs).

**Physician-AI interaction / clinical decision support deployment:** Sandeep Reddy (digital health/AI governance); Roxana Daneshjou (Stanford, dermatology AI evaluation); Sonoo Thadaney Israni (Stanford, human-AI clinical collaboration).

050413

# Editorial Report

**Manuscript:** "From inconsistent definition to standardized extraction: large language model for reproducible multicenter cardiovascular research"

---

## 1. Overall Assessment

The manuscript reports a two-stage LLM workflow (OCR-style transcription via Qwen3-VL-235B-A22B, followed by Qwen3-235B-A22B/32B/8B applying standardized extraction prompts) that converts photographed coronary artery disease (CAD) records into ten structured research variables, tested on 313 cases across nine institutions in two trials (AIM-CHD internal, SMART-CHD external). The central claim is that encoding indicator definitions into prompts, not model capability alone, resolves both labor cost and inter-reviewer inconsistency in multicenter cardiovascular data abstraction, with the largest gain on judgment-dependent "logical" indicators (96.5% vs 90.7% manual, P<0.001).

This is a competent, well-powered validation study, but it is fundamentally a benchmarking exercise dressed as a methodological advance. The core technical contribution — task-specific prompting with explicit operational rules — is not novel; it restates prompt engineering and structured extraction principles already established in EHR-extraction literature. The genuine value lies in the deployment context (photograph-based, multicenter, three model sizes, cost/time accounting) rather than in any new extraction method. The single-country, single-language, single-model-family design and absence of any non-Qwen baseline are the two concerns most likely to drive the decision.

---

## 2. Strengths

The research-equivalence framework is the most defensible contribution. Rather than stopping at indicator-level accuracy, the authors fit logistic regression models predicting multivessel disease from each extracted dataset and tested AUC equivalence (ΔAUC −0.003, 90% CI within ±0.05) against an adjudicated reference. This shifts the unit of evaluation from "did the field match" to "would the science change," which is the right question and is rarely asked in this literature.

The three-model-size comparison (235B, 32B, 8B) with consistent performance above 97% overall accuracy, and the explicit finding that performance loss was confined to logical indicators, gives the paper a genuine deployment-relevance angle: the 8B model is plausibly runnable on commodity hospital hardware, which matters for community-hospital participation in multicenter trials.

External validation across eight SMART-CHD subcenters (n=70) with documented degradation (235B: 98.4% internal vs 96.4% external, P<0.01) is appropriately transparent. Many LLM-extraction papers report only internal held-out performance; this one quantifies and reports the generalization gap rather than hiding it.

The error taxonomy — seven causes, split into systematic (n=44) versus random (n=44) across three independent runs — is methodologically careful and correctly identifies that numerical errors are OCR-driven while logical errors are judgment-driven (rule application, evidence omission, hallucination). This distinction is clinically actionable for anyone implementing the workflow.

---

## 3. Weaknesses

The entire validation rests on a single model family (Qwen3) deployed through a single platform (Alibaba Cloud API). The manuscript explicitly lists this as a limitation but does not mitigate it with even one comparator run on GPT-4-class or open alternatives (Llama, DeepSeek, Gemma). Without a cross-family baseline, the claim that "standardized prompts" rather than "this specific model" drive the gain is asserted, not demonstrated. A reviewer cannot distinguish a generalizable prompting principle from a Qwen3-specific result.

The reference standard, while dual-reviewed with adjudication, is exclusively human-derived, and the equivalence analysis compares the LLM workflow against that same human-derived standard used to train (via the 50-case development set) and judge it. There is no independent ground truth (e.g., source-document re-adjudication by a third blinded panel) to rule out shared bias between the prompt-development process and the evaluation reference, particularly for the "logical" indicators where definitional judgment calls were made by the same two cardiologists who built the prompts.

The cohort is entirely Chinese-language, single-disease (CAD), single-country, with ten preselected indicators. The manuscript's own limitations section concedes this, but the discussion oversells generalizability ("standardized prompts maintain extraction consistency regardless of local documentation practices") well beyond what a single-language, single-condition dataset can support. Claims about applicability to "routine cardiovascular data collection" need either a second-language cohort or substantially softened language.

The cost analysis (0.216 CNY/case vs 6.51 CNY/case manual) is a useful operational figure but is built on a fixed assumption (20,000 CNY/month, 8-hour/5-day week) that does not account for model-output verification time, IT/security infrastructure for on-premises deployment of even the 8B model, or the audit/QA layer any IRB-governed multicenter trial would require before accepting LLM-extracted data as primary endpoints. The 97% cost reduction figure will be quoted out of context unless the manuscript explicitly scopes it to raw extraction labor only.

---

## 4. Editorial Decision

**Reject**, with a suggestion to transfer to *npj Digital Medicine* or *JAMIA*. The single-model-family limitation and the absence of any non-Qwen baseline are structural, not revisable within a reasonable revision cycle, and the language/disease-scope narrowness makes the generalizability claims in the discussion incommensurate with the evidence. The research-equivalence framework and multicenter external validation are genuinely good work and would be competitive at a methods-focused digital health journal, but they do not clear the bar of broad clinical or methodological significance this journal requires.

---

## 5. Suggested Reviewer Expertise

Reviewers should include: (1) multimodal/vision-language model evaluation methodology, specifically prompt-based structured extraction from document images; (2) clinical natural language processing and information extraction benchmarking across model families and architectures; (3) biostatistics with expertise in equivalence testing and bootstrap-based AUC comparison; (4) interventional cardiology with direct experience in CAD registry data abstraction and multicenter trial coordination; (5) clinical informatics with experience in OCR/EHR pipeline deployment and data governance in hospital information systems.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

LLM-based clinical extraction has moved rapidly from single-document NER toward multimodal, schema-based, multicenter pipelines over 2024–2026. A 2026 medRxiv benchmark tested seven LLM-based information-extraction tools on molecular test reports, finding GPT-4.1-mini with OCR-extracted text most effective at an average F1 of 55.6, with the best local model (Gemma3-27B) reaching only 41.3 F1, underscoring that this manuscript's >96% exact-match accuracy is achieved on a narrower, more numerically structured indicator set than typical free-text IE benchmarks — a comparison the authors should engage with directly. A separate 2025 medRxiv study built a scalable schema-based LLM extraction pipeline from C-CDA EHR documents (including embedded images, up to 32% of source data) validated on 34 patients and deployed across 11,115 patients, achieving roughly 95% accuracy/F1 across data fields — directly comparable in scale ambition but lacking this manuscript's explicit research-equivalence step. An earlier 2025 BMJ Health & Care Informatics multi-model evaluation found eight LLMs exceeding 0.98 accuracy on structured/semi-structured EHR notes, with Claude 3 Opus performing best overall, which is the kind of cross-family comparison this manuscript conspicuously omits. On the deployment side, a late-2025 implementation paper described an on-premises, GDPR-compliant LLM assistant using Qwen3-235B with retrieval-augmented generation integrated into a European hospital's Epic EHR, showing that Qwen3-family deployment in cardiovascular-adjacent clinical settings is already being explored elsewhere, which weakens any claim of architectural novelty in model choice. Photograph-based (versus scanned/typed) source documents and the research-equivalence framework remain the manuscript's most distinctive contributions relative to this landscape; the authors should explicitly benchmark against at least one non-Qwen model family and engage with the F1-based IE literature rather than relying solely on exact-match accuracy, which is a more permissive metric for short categorical/numerical fields.

---

## Suggested Reviewers' Names

**Technical/Methodological:**
- Vasiliki Ntinopoulou or co-authors of the BMJ Health & Care Informatics multi-LLM EHR extraction evaluation
- Authors of the LLM-AIx open-source extraction pipeline (medRxiv 2024.09.02.24312917)
- A senior author from the LlamaIndex/LlamaParse agentic document-extraction research group
- A biostatistician with published work in bootstrap-based equivalence testing for clinical prediction models

**Clinical/Cardiology:**
- A interventional cardiologist with active leadership in a multicenter CAD registry (e.g., a site PI from a national PCI or ACS registry)
- A clinical epidemiologist with publication record in cardiovascular registry data quality and inter-reviewer variability

050707

# Editorial Report (Condensed): "SLICE: A Unified Deep Multimodal Framework of Slit-Lamp Images for Cataract Evaluation"

## 1–4. Assessment, Strengths, Weaknesses, Decision

SLICE jointly grades cortical (CC), nuclear (NC), and posterior subcapsular cataract (PSC) at the patient level from three slit-lamp modalities, using a two-phase ConvNeXt-Tiny expert-then-fusion architecture, CORAL ordinal loss, dual-ophthalmologist soft supervision, and lesion-preserving background-swap augmentation. The motivating problem — LOCS III requires integrating three non-interchangeable modes per eye — is real. But the framing as the first patient-level, multimodal, tri-subtype framework is overstated: DeepLensNet (Keenan et al., Ophthalmology 2022) already grades nuclear sclerosis, cortical opacity, and PSC jointly per eye on 18,999 AREDS photographs with multi-site external validation against 14 ophthalmologists, and Son et al. (Ophthalmol Sci 2022) grades all four LOCS III axes from slit-lamp plus retroillumination images with AUCs of 0.97–0.999, again with proper test-set reporting. SLICE's single-center, single-device, single-photographer dataset with no external validation is a step backward on generalizability relative to both 2022 benchmarks.

The fusion design is technically coherent: Feature Addition over frozen modality-specific GAP vectors beat four other fusion strategies (Late Fusion, Concatenation, Unfrozen End-to-End, Transformer) at only 1.19M parameters, and the ablation (Supplementary Table S1) shows differentiated, mechanism-consistent effects — lesion-preserving augmentation lifting PSC accuracy from 73.36% to 76.23%, dual-label supervision lifting CC/NC accuracy. CORAL ordinal regression is well-justified given LOCS III's ordinal structure, and 100% of CC and 99.6% of NC errors stayed within one adjacent grade (QWK 0.93).

The validation design is the decisive flaw. All 2,981 eyes, including the "independent" 250-eye validation cohort, come from one center, one Topcon SLD701 device, one photographer. PSC — the subtype most tied to surgical urgency — is also the weakest, with QWK against the most experienced ophthalmologist at only 0.63 versus 0.91–0.92 for CC/NC, a gap underweighted in the Abstract and Discussion's headline 0.82 average. The baseline comparison is also unfair to DeepLensNet/DeepOpacityNet, which were validated on fundus/AREDS-protocol images, not retrained or contextualized against their own published performance.

**Decision: Reject.** Single-site, single-device, no-external-validation design directly contradicts repeated claims of real-world clinical readiness, and the novelty claim does not survive comparison with DeepLensNet and Son et al., both already offering patient-level, multi-subtype, externally-validated grading. May suit a methods-focused or regional journal if reframed as a fusion-architecture comparison rather than a validated clinical tool.

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in ordinal regression and CORAL-style rank-consistent loss functions for medical image grading; multimodal feature fusion architectures for clinical imaging (late fusion, cross-attention, feature concatenation versus addition); ConvNeXt and vision transformer backbones as applied to small-to-medium clinical imaging cohorts; LOCS III-based cataract grading and its known inter-observer variability in clinical ophthalmology; and external validation methodology and generalizability assessment for ophthalmic AI, including experience with multi-site or multi-device slit-lamp datasets.

## 6. State-of-the-Art Literature Review (Past Three Years)

The field has moved on two fronts relevant here. First, large-scale patient-level multi-subtype cataract grading was already established by Keenan et al.'s DeepLensNet (Ophthalmology, 2022), trained on 18,999 AREDS photographs across nuclear sclerosis, cortical opacity, and PSC, externally validated on the Singapore Malay Eye Study, and benchmarked directly against 14 ophthalmologists and 24 medical students with statistically significant superiority for the two common subtypes. Lu et al. (J Cataract Refract Surg, 2022), cited by the authors, built a LOCS III-based AI program with internal and external test sets (Pujiang Eye Study) using Faster R-CNN and ResNet, reporting AUCs of 0.977–0.983 for nuclear grading externally. SLICE's contribution relative to both is a more LOCS III-faithful three-modality slit-lamp input scheme and a CORAL-based ordinal loss with dual-label soft supervision, but it gives up the external validation and multi-site scale that both predecessors already achieved. Second, the broader ophthalmic AI field has shifted toward vision-language and foundation-model paradigms for anterior segment and retinal imaging in 2024–2025 (e.g., multimodal visual-language foundation models for computational ophthalmology, and multimodal foundation models for OCT image analysis), against which a frozen-backbone, addition-fusion CNN ensemble represents an architecturally conservative approach. The authors should engage explicitly with DeepLensNet as a direct competitor rather than citing it only as evidence of a single-modality gap in the field, since DeepLensNet's patient-level, three-subtype design substantially narrows the novelty gap SLICE claims to fill.

## 7. Suggested Reviewers' Names

**Ordinal regression / multimodal fusion methods:** Wei Cao, Sebastian Raschka, Vishnu Mirjalili (CORAL framework originators); Qingyu Chen (DeepLensNet, NLM/NCBI deep learning methods).

**Clinical cataract grading / ophthalmic AI:** Tiarnan D.L. Keenan (DeepLensNet, NEI); Qiang Lu / Xiangjia Zhu (LOCS III AI grading, Fudan Eye Institute); Yih-Chung Tham (ophthalmic AI, SERI/Singapore).

**External validation and generalizability in ophthalmic AI:** Pearse A. Keane (multimodal/foundation model ophthalmic AI validation); Daniel Shu Wei Ting (multi-ethnic, multi-site ophthalmic deep learning validation).

## 8. Further Literature

1. **Keenan TD, Chen Q, Agrón E, et al. DeepLensNet: Deep Learning Automated Diagnosis and Quantitative Classification of Cataract Type and Severity. *Ophthalmology* 2022;129(5):571–584. doi:10.1016/j.ophtha.2021.12.017.** Directly competing patient-level, tri-subtype (NS/CLO/PSC) grading system with multi-site external validation and head-to-head comparison against 14 ophthalmologists. This is the strongest prior-art challenge to SLICE's novelty claim and is not engaged with as a direct competitor in the manuscript's Discussion.

2. **Son KY, Ko J, Kim E, et al. Deep Learning-Based Cataract Detection and Grading from Slit-Lamp and Retro-Illumination Photographs: Model Development and Validation Study. *Ophthalmol Sci* 2022;2:100147. doi:10.1016/j.xops.2022.100147.** Grades all four LOCS III axes (NO, NC, CO, PSC) from slit-lamp and retroillumination images with substantially higher reported AUC (0.95–0.999) and accuracy than SLICE achieves. Independently verified via PubMed/ScienceDirect; not cited in the manuscript. Reviewers should ask the authors to benchmark against this system's reported performance rather than only against fundus-based DeepOpacityNet.

3. **Lu Q, Wei L, He W, et al. Lens Opacities Classification System III-based artificial intelligence program for automatic cataract grading. *J Cataract Refract Surg* 2022;48(5):528–534. doi:10.1097/j.jcrs.0000000000000790.** Cited by the manuscript as evidence of a single-modality gap, but independent verification shows it includes internal AND external (Pujiang Eye Study) test sets with AUC 0.977–0.983 for nuclear grading — a stronger validation design than SLICE's. The manuscript's characterization of this paper's limitations should be revised for accuracy.

4. **Tang Y, Zhang H, Du Y, Jiang Q, Qi M, Zhou X. Artificial intelligence in cataract grading system: a LOCS III-based hybrid model achieving high-precision classification. *Front Cell Dev Biol* 2025. PMCID: PMC12454382.** A 2025 hybrid (non-deep-learning-only) cortical/PSC grading model using Hough-transform and cluster-analysis feature extraction. Relevant as a recent comparator showing the field still actively explores non-end-to-end approaches for PSC, the subtype where SLICE is weakest (QWK 0.63).

5. **Frontiers in Medicine. A deep learning-driven cataract screening model derived from multicenter real-world dataset. 2025. doi:10.3389/fmed.2025.1691419.** A 2025 multicenter, cascaded screening system explicitly designed to handle real-world confounders (e.g., co-occurring pterygium), directly contrasting with SLICE's single-center, confounder-naive design. Useful for reviewers assessing SLICE's real-world readiness claims.

6. **Shi D, et al. A multimodal visual-language foundation model for computational ophthalmology. *NPJ Digit Med* 2025;8:381. doi:10.1038/s41746-025-01772-2.** Representative of the foundation-model paradigm shift cited in the manuscript's own introduction (ref. 10) but not substantively engaged with in the Discussion. Differentiates from SLICE by using vision-language pretraining rather than frozen CNN experts with addition fusion; the authors should explain why a more conservative CNN-ensemble approach is preferable for this clinical task.

7. **DOI:10.3389/fdgth.2025.1716501 — SLID: a slit-lamp image dataset for deep learning-based anterior eye anatomical segmentation and multi-lesion detection (2026), from the same institution (Zhejiang University Eye Center, Second Affiliated Hospital).** Note for editorial awareness: this concurrent or recent publication from an overlapping author/institution group works with slit-lamp datasets from the same center. Authors should disclose whether patient overlap exists between this dataset and the SLICE cohort, and whether concurrent publications from the group share underlying data.

050971

I'll load the skill file first, then process this manuscript.This manuscript makes claims I need to verify independently before drawing novelty conclusions — particularly the dataset claims, the "NOUN-53" architecture novelty, and the comparator baselines. Let me run targeted searches.This is critical. The dataset is a *segmentation* dataset (kidney vs. background masks) for TKV measurement — it has no CKD-vs-normal diagnostic ground truth at the per-subject classification level beyond "healthy control" vs "CKD patient" cohort labels, and crucially it provides only kidney masks, not disease-stage labels. Let me verify the original Daniel et al. paper and check whether other groups have used this exact dataset for "classification," which would expose a critical flaw.This confirms the central problem: the dataset is a 60-subject (30 HC / 30 CKD), kidney-mask-only segmentation dataset built for total kidney volume measurement — not a disease-staging dataset. The manuscript claims a CKD vs. normal binary classification task, which is trivial to solve on this cohort (healthy young controls, mean age 26, vs. CKD patients, mean age 59, mean stage 3.5) since age and gross anatomy alone separate the groups; the elaborate claims about "Stage 2 vs Stage 3" hidden comorbidity bias and biological vague boundaries cannot be evaluated on this dataset because it carries no per-subject CKD stage labels at all in the classification task as described. Let me verify a few more specific claims — the "DenseNet-201 + DarkNet-53 + Stochastic Feature Mapping" combination and check for any prior art using nonsense-named hybrid architectures, a hallmark of this manuscript mill pattern.This is decisive. A 2024 ScienceDirect paper using the *exact same* Zenodo/Kaggle dataset (100 T2-weighted scans, 1299 images) with a "Resnet18-Self-ONN-UNet++" segmentation network achieved 94.38% classification accuracy — and this manuscript's own AER-SO U-Net++ deep-feature module name is nearly identical to that prior published architecture name. This is a serious undisclosed-prior-art flag. I now have enough to write the report.

---

## Editorial Report: Manuscript 050971 — "NOUN-53: Nyul's ONN-U-Net++ with Gray Boruta-based DarkNet-53 Model for Automated Classification of Chronic Kidney Disease Using MRI Images"

### 1. Overall Assessment

The manuscript proposes a multi-stage pipeline ("NOUN-53") for binary CKD-versus-normal classification from T2-weighted kidney MRI, combining Nyul histogram normalization and Hessian filtering, an attention-enhanced ResNet18-Self-ONN-U-Net++ for deep feature extraction, a "Neighboring Gray-based Boruta Algorithm" for radiomic feature selection, canonical-correlation-based feature fusion, an Otsu-guided level-set TransUNet for segmentation, and a DenseNet-201/DarkNet-53/stochastic-feature-mapping ensemble for final classification, reporting 99.21% accuracy and 99.19% F1-score.

The central claim does not survive scrutiny of the dataset used to support it. The cohort is the UKRIN-derived Zenodo/Kaggle T2-weighted kidney MRI set of 60 subjects (30 healthy controls, mean age 26±11; 30 CKD patients, mean age 59±14, mean CKD stage 3.5), assembled by Daniel et al. (2021) specifically for total-kidney-volume segmentation, not for diagnostic classification. Age and gross renal morphology alone separate these two groups; a classifier trained on this cohort cannot demonstrate the fine-grained discriminative capability the manuscript claims to address (Stage 2 vs. early Stage 3 "Hidden Comorbidity Bias," "Pseudo-Progression Trap"). The paper's own motivation section describes problems — biologically ambiguous stage boundaries, B0-field-induced texture artifacts — that this dataset cannot test, since it carries no per-subject CKD stage labels usable for the binary task described and was never validated for diagnostic discrimination. This is the dominant concern and is fatal to the manuscript as framed.

### 2. Strengths

The preprocessing pipeline is mechanistically well specified. The Nyul histogram-matching plus Hessian-filter cost function (Equations 1–3) and the PSGM-up beta-interpolation augmentation (Equations 4–6) are concretely defined rather than asserted, which is uncommon in this submission category and gives reviewers something falsifiable to test.

The explainability component is appropriately implemented. Grad-CAM is applied post-classification (Equation 28) and the authors report both a CKD case (30% pathological-area activation overlap) and a healthy case (diffuse, non-localized activation) as a sanity check, which is the correct minimal bar for demonstrating that activation is not spuriously concentrated on background or scanner artifact.

The motivation section's mechanistic account of "Voxel-Grain Bias" — linking hemosiderin-driven B0 field inhomogeneity to inflated Busyness and fractal-dimension radiomic features — is a genuine and well-articulated radiomics insight, independent of whether the proposed architecture actually mitigates it.

### 3. Weaknesses

The dataset-task mismatch described above is the primary flaw and is non-revisable: no amount of architectural refinement corrects for evaluating a 60-subject, age-confounded, segmentation-purposed cohort as if it demonstrated robust diagnostic classification. The reported 99.21% accuracy, 99.94% specificity, and 0.995 AUC are consistent with a trivial age/morphology separation, not with resolution of "biological vague boundaries" between disease stages, which this cohort does not contain.

There is no external validation, no train/test split description, no cross-validation scheme, and no confidence intervals anywhere in the results. A 60-subject cohort with a single confusion matrix (Figure 9: 50/50 split, one misclassification) is reported without specifying which subjects were held out, raising direct concern about test-set leakage given the architecture's many tunable stages.

The novelty of the deep-feature module is independently contestable. A 2024 ScienceDirect paper using the identical Zenodo/Kaggle dataset (1299 images, 100 T2-weighted scans) proposed a "Resnet18-Self-ONN-UNet++" network for kidney segmentation and reported 94.38% CKD-vs-healthy classification accuracy with DenseNet-201 among its comparator backbones. The present manuscript's "Attention-Enhanced ResNet18-Self-ONN-U-Net++" is a near-verbatim architectural descendant of that published network, and this prior work is not cited or distinguished anywhere in the manuscript's 25-reference literature review. This must be addressed before any further evaluation is possible.

No ablation isolates the marginal contribution of any of the five major proposed modules (NHM-up, AER-SO U-Net++, NG-BA, V-MC fusion, OLO-TransUNet, SD-DN53). With this many interacting components and a 60-subject dataset, the 99%+ performance figures cannot be attributed to any specific design choice, and overfitting cannot be excluded.

### 4. Editorial Decision

**Reject.** The dataset is unsuited to the diagnostic claims being made, the apparent undisclosed overlap with a previously published "ResNet18-Self-ONN-UNet++" segmentation architecture on the identical dataset raises a novelty concern that is disqualifying on its own, and the absence of any validation methodology (splits, cross-validation, confidence intervals) means the reported metrics cannot be assessed for reliability. These are independently fatal; none is correctable through revision without a new dataset and a transparent novelty accounting against the 2024 prior art.

### 5. Suggested Reviewer Expertise

Reviewers should have expertise in: deep learning-based medical image segmentation architectures (U-Net variants, operational neural networks/Self-ONN); radiomics feature engineering and stability analysis under scanner-induced variability; ensemble CNN classifier design (DenseNet, DarkNet) for small-cohort medical imaging; nephrology with specific familiarity with CKD staging by eGFR and renal MRI biomarkers (TKV, T1/T2 mapping); and clinical AI validation methodology, including cross-validation design and generalizability assessment for small (n<100) cohorts.

### 6. State-of-the-Art Literature Review (Past 3 Years)

Recent CKD-MRI work has moved toward two credible directions this manuscript does not engage with adequately. First, diffusion- and relaxometry-based severity classification on larger, label-rich cohorts: Nagawa et al. (Scientific Reports, 2024) trained a 3D CNN on Dixon T1-weighted MRI from 321 patients spanning CKD stages G1–G5 to classify severity directly by eGFR-defined stage, achieving 86.2% accuracy — a genuine staging task, unlike the present binary healthy-vs-CKD problem on an age-confounded cohort. Second, uncertainty-aware radiomics: Damiano et al. (Medical Physics, 2025) used Monte Carlo dropout and test-time augmentation on the same UKRIN dataset used here to quantify radiomic feature reproducibility under segmentation uncertainty, directly addressing the "Voxel-Grain Bias" concept this manuscript raises but does not rigorously test. Most directly competitive is the 2024 ScienceDirect study (Classification and segmentation of kidney MRI images for chronic kidney disease detection) that used this exact Kaggle/Zenodo dataset with a "Resnet18-Self-ONN-UNet++" model and DenseNet-201 comparator, reporting 94.38% accuracy — a paper this manuscript should have cited, distinguished, and benchmarked against directly, and did not.Want this saved as a file (.docx or .md) for your records, or is the inline report sufficient? Also note per your project instructions, this manuscript's content stays isolated to this chat — I have not and will not carry any detail from it into other conversations in this project.
