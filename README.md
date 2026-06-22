# Trackrad202512456

049033 Organs and Radiological Tasks

## 1. Overall Assessment

This manuscript reports UUSIC25, a MICCAI-affiliated challenge benchmarking 15 finalist algorithms on a single-model, multi-organ ultrasound task spanning five segmentation targets (breast, thyroid, kidney, fetal head, cardiac) and four classification tasks (breast malignancy, fatty-liver, appendicitis, four-class breast molecular subtyping), evaluated on a 2,479-image private test set that includes a fully unseen external center (NKI, n=512). The central claim is that a single consolidated architecture can match organ-specific Dice performance (macro-DSC 0.854 for the winning team, SMART) while exposing a severe generalization failure in pathology-linked classification, with the best internal AUC for molecular subtyping (0.612, Lanzhou) collapsing to near-chance (0.474) on the external cohort.

The work is a well-instrumented benchmarking exercise, not a methodological or clinical advance. It does not propose a new architecture, algorithm, or theoretical contribution; it aggregates third-party Docker submissions and reports comparative metrics. Two issues will dominate the decision. First, an essentially identical manuscript describing the same challenge, same dataset, same leaderboard, and overlapping authorship (Lin, Tan, Xu, and the same consortium) is already circulating as an arXiv preprint (arXiv:2512.17279, "Diagnostic Performance of Universal-Learning Ultrasound AI Across Multiple Organs and Tasks: the UUSIC25 Challenge"), with materially different headline numbers for the same comparisons (e.g., breast malignancy AUC reported as 0.837 there versus 0.876 attributed to fatty-liver here; molecular subtyping AUCs differ team-by-team). Second, the paper's own data expose a foundational pathology-classification failure that the manuscript frames as a finding rather than a disqualifying limitation of the entire challenge design for half its task portfolio.

## 2. Strengths

The external validation design is genuinely rigorous for a challenge paper. Reserving the entire NKI cohort (n=512, different scanners, different country) exclusively for testing, with zero exposure during training or validation, is the correct way to interrogate generalization, and the resulting AUC collapse (0.612→0.474 for Lanzhou; Table 4) is a clinically important negative result rather than a buried footnote.

The evaluation framework's joint weighting of diagnostic performance (70%) and computational efficiency (30%), reported transparently in the ranking formula (Methods, Eq. 1), is a meaningful design choice that surfaces real deployment trade-offs: SMART's 0.59 GB peak memory versus flamingo's 12.41 GB for comparable accuracy is a finding with direct relevance to point-of-care and edge deployment, which most segmentation challenges ignore entirely.

Annotation quality control is well documented. The two-round correction pipeline, with junior annotators (1–3 years' experience) followed by senior physician review (>10 years' experience) and a reported inter-annotator ASSD below 0.5 pixels at the 75th percentile, gives the reference standard credibility that many multi-site retrospective ultrasound datasets lack.

The DeLong-based pairwise statistical comparisons (Figure 8Q–T) and the explicit acknowledgment that no single model statistically dominates across all four classification endpoints is honest reporting that most leaderboard papers omit in favor of declaring a single winner.

## 3. Weaknesses

The molecular subtyping task is not merely "harder under domain shift"—it is not learnable from B-mode ultrasound alone with this design, and the manuscript does not draw that conclusion. An AUC of 0.474–0.567 on NKI across all five top teams is statistically indistinguishable from or only marginally above chance (Table 4). Reporting this as evidence of a "generalization gap" rather than as evidence that the underlying biological signal (HER2/luminal subtype) is not recoverable from this imaging modality and label source overstates what the data show. The manuscript should explicitly state that this endpoint failed and should not be retained as a co-equal task in a future iteration without a fundamentally different feature source (e.g., paired clinical/genomic data).

The classification reference standard is heterogeneous and partially circular by design. Molecular subtype labels derive from "surgical pathology logs" while malignancy labels derive from "pathological biopsy reports" (Methods) — these are different chains of clinical evidence with different latency and noise properties, pooled into one task family without separate sensitivity analysis of label quality.

No comparison against any published single-organ state-of-the-art model is performed empirically within this paper; the "competitive with specialists" claim that anchors the companion arXiv version is absent here entirely, and this manuscript's own text never benchmarks SMART's 0.854 breast DSC or 0.942 fetal-head DSC against the actual single-task literature (e.g., Huang et al.'s boundary-rendering network, or Lancet Digital Health-grade thyroid AI). Without that comparison, "universality without performance cost" is asserted, not demonstrated.

The manuscript and its arXiv twin report different numbers for nominally identical comparisons (breast malignancy AUC 0.876 here for fatty-liver vs. 0.837 there for malignancy; internal subtyping AUCs differ by team), which is either a labeling inconsistency between concurrent submissions or a sign that "final" results were not yet final when one or both papers were drafted. This must be resolved and disclosed before any further consideration; concurrent near-duplicate submission with discrepant primary results is a reproducibility problem independent of overlap policy.

## 4. Editorial Decision

**Reject.** The benchmarking exercise is competently executed, but the manuscript (a) draws an overly optimistic top-line conclusion ("UUSIC25 establishes... robust cross-center generalization") that its own Table 4 contradicts for the pathology-linked half of the task portfolio, and (b) has a parallel, numerically inconsistent preprint covering the identical challenge and cohort already in public circulation, which the editor cannot adjudicate without author clarification on which results are authoritative. Neither flaw is fixable through revision alone without first resolving data consistency across the two manuscripts. Recommend transfer to *npj Digital Medicine* or *Scientific Data* contingent on reconciling the two reported result sets and reframing the subtyping task as a negative result rather than a generalization caveat.

## 5. Suggested Reviewer Expertise

Multi-task and multi-domain deep learning architectures for medical image segmentation (Transformer/Swin-based backbones, FiLM/prompt conditioning); benchmark and challenge design methodology (CodaLab/Docker-based evaluation, statistical ranking schemes); domain shift and generalization in medical imaging classifiers; breast radiology with expertise in molecular subtyping correlation to B-mode ultrasound; and a clinical ultrasonographer or point-of-care ultrasound specialist familiar with multi-organ scanning workflows and device heterogeneity across LMIC and tertiary settings.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved decisively toward self-supervised, organ-agnostic ultrasound foundation models rather than supervised multi-task challenge leaderboards. URFM, pretrained on over one million images from 15 anatomical organs using representation-based masked image modeling, was designed to enable label-efficient adaptation to diverse diagnostic tasks, directly addressing the "organ barrier" problem this manuscript benchmarks empirically but does not solve architecturally. EchoCare, a fully open and generalizable foundation model released in September 2025, outperformed state-of-the-art comparison models across ten representative ultrasound benchmarks spanning disease diagnosis, segmentation, organ detection, and report generation, with code and pretrained weights publicly released. Chen et al.'s MOFO model, from one of this challenge's own winning teams, used task prompts and anatomical priors to extract organ-invariant representations across a ten-organ, 7,039-image segmentation database, outperforming single-organ baselines with statistically sufficient margins — this is the direct architectural predecessor the present manuscript should engage with explicitly but does not benchmark against quantitatively.

Against this landscape, UUSIC25's contribution is a community benchmark, not a model — closer in kind to AMOS or BraTS than to USFM or EchoCare. That is a legitimate contribution category, but the manuscript should be explicit that it is positioning itself as infrastructure for the field (a shared evaluation protocol) rather than as evidence that any single submitted architecture has solved multi-organ ultrasound AI. The companion arXiv preprint already makes a stronger, more triumphalist claim along these lines ("debunking the myth that versatility must come at the cost of precision"); this Nature Communications version should not import that framing, particularly given that the classification side of the benchmark — the half of the task portfolio that actually tests pathology inference rather than boundary delineation — failed outright under external validation.

## 7. Suggested Reviewers

**Multi-task/foundation model architecture:** Qingbo Kang, Qicheng Lao, Kang Li (URFM, West China/BUPT), Jing Jiao or Tao Tan (USFM/orchestration learning authors — note Tan is a co-author here, so an independent name from that group is needed), Hongyuan Zhang (EchoCare).

**Domain generalization / distribution shift in medical imaging:** Cheng Ouyang, Christian Baumgartner, or another author from the domain-randomization/causality-inspired segmentation generalization literature.

**Breast radiology / molecular subtyping:** Nehmat Houssami, or a breast-imaging pathologist with expertise correlating sonographic phenotype to IHC/molecular subtype.

**Clinical point-of-care ultrasound / multi-organ scanning workflow:** Cristiana Baloescu or another JAMA-published POCUS generalist with multi-organ device experience.

Note: this report's section structure is six numbered sections, not seven — sections 1–4 here map to Overall Assessment, Strengths, Weaknesses, and Editorial Decision. I'm condensing those four to ~300 words and preserving Suggested Reviewer Expertise and the original literature review verbatim, then appending a new Further Literature section with 5–6 papers from the past three years sharing similar scope (MCDM/benchmarking methodology, not clinical imaging).# Editorial Report: HERA (Revised)

---

044685

HERA is a MATLAB toolbox for paired multi-criteria benchmarking, combining Wilcoxon signed-rank testing with Holm–Bonferroni correction and a dual effect-size gate (Cliff's Delta, Relative Mean Difference) against bootstrap-derived, data-driven thresholds. It addresses a genuine gap: existing MCDM tools (TOPSIS, PROMETHEE, ELECTRE) require subjective weighting, and post-hoc tests (Nemenyi, Friedman) ignore effect magnitude. This is a statistical methods/software contribution, not a clinical study; the "neuroimaging use case" is entirely synthetic Monte Carlo data calibrated to undisclosed moments of an unpublished, institutionally restricted dataset.

The validation suite is genuinely rigorous: 19 ground-truth tests, 2,400 Monte Carlo convergence datasets across eight distributional scenarios, and adversarial stress tests (60% MCAR, outlier-driven false positives) demonstrate disciplined self-interrogation. The dual-criterion conjunction logic is a defensible solution to the significance-versus-magnitude conflation problem, and the intransitivity handling (N² abort criterion, demonstrated threshold-based cycle suppression) anticipates a known pairwise-ranking failure mode rather than discovering it post hoc.

However, no real dataset appears anywhere in the manuscript. Methods A–F/G lack the specificity needed to assess whether the conflicting OC/CNR/SNR pattern reflects real contrast-algorithm behavior or a simulation artifact. The metric hierarchy is asserted from one prior paper, never validated against expert or clinical ground truth. Most critically, the journal-fit problem is structural: HERA is a domain-agnostic ranking algorithm with no clinical architecture, endpoint, or patient population — explicitly generalized by the authors to "resource optimization" and HTA, undermining any digital-health framing.

**Decision: Reject.** The absence of real data and clinical content are non-revisable for this venue regardless of methodological quality; a methods-focused outlet (Journal of Statistical Software, PLOS Computational Biology) is more appropriate.

---

### 5. Suggested Reviewer Expertise

Reviewers should have expertise in: nonparametric statistical inference and multiple-testing correction (Wilcoxon signed-rank theory, Holm–Bonferroni/FDR procedures); bootstrap resampling methodology, including BCa interval theory and cluster bootstrap for correlated data; multi-criteria decision analysis (TOPSIS/PROMETHEE/ELECTRE/Bayesian ROPE methods) and benchmarking methodology in machine learning; and, on the clinical side, quantitative MR image-quality assessment (contrast-to-noise ratio, signal-to-noise ratio, and their correlation with radiologist-rated diagnostic quality) to evaluate whether the use case has any clinical grounding at all.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant comparator lineage for HERA is the Bayesian hierarchical and ROPE-based classifier-comparison literature (Benavoli, Corani, Demšar, and colleagues), which the authors cite as ref. 16 but which has continued to develop generalized stochastic-dominance fronts and joint multi-dataset hierarchical models as alternatives to exactly the post-hoc NHST pitfalls HERA targets; a quantitative comparison against this Bayesian baseline, rather than only a textual contrast in the Discussion, would substantially strengthen any future submission. On the clinical-imaging side relevant to the use case, recent work has directly addressed the gap HERA leaves open: a 2024–2025 study trained neural image-quality metrics (IQ-Net) on nearly 20,000 radiologist pairwise rankings from the NYU fastMRI database to align quantitative IQMs with expert diagnostic judgment, and a 2025 study in MAGMA showed that paired image-quality metrics (versus unpaired) better detect clinically meaningful degradation in AI-reconstructed MR images across field strengths, with explicit comparison to radiologist ratings. These metrics responded to changes such as adjustments to denoising strength and the addition of image filters, providing evidence that these IQMs are suitable for detecting changes in image quality, while unpaired metrics displayed lower sensitivity. HERA does not engage with this literature at all: its OC/CNR/SNR hierarchy is asserted from one prior optimization paper (Nöth et al.) rather than validated against any expert-rated ground truth, which is precisely the standard the current radiology image-quality field has converged on as necessary for any new ranking or metric-aggregation framework to be clinically credible.

---

### 7. Further Literature (Methodological Scope — Past 3 Years)

These six papers share HERA's core scope — subjective-weight-free or statistically grounded multi-criteria ranking/benchmarking software — rather than its incidental clinical-imaging use case.

1. **Taherdoost, H. & Madanchian, M.** Multi-Criteria Decision Making (MCDM) Methods and Concepts. *Encyclopedia* 3, 77–87 (2023). doi:10.3390/encyclopedia3010006. Already cited by the authors as ref. 1; included here because it remains the most current general MCDM survey and underscores that HERA's "no subjective weighting" claim should be benchmarked against the full taxonomy this survey catalogs, not only TOPSIS/PROMETHEE/ELECTRE.

2. **Pereira, V., Basilio, M. P. & Santos, C. H. T.** Enhancing decision analysis with a large language model: pyDecision, a comprehensive library of MCDA methods in Python. *Journal of Modelling in Management* (2024). doi:10.1108/JM2-04-2024-0118. Directly competing open-source software (70 MCDA methods) cited by the authors as ref. 8; a head-to-head runtime/ranking-agreement comparison against pyDecision on a shared dataset is conspicuously absent from HERA's validation.

3. **Najafi, A. & Mirzaei, S.** RMCDA: The comprehensive R library for applying multi-criteria decision analysis methods. *Software Impacts* 24, 100762 (2025). doi:10.1016/j.simpa.2025.100762. Introduces Stratified MCDM and Stratified Best-Worst Method as newer hierarchical-weighting alternatives in R; relevant because it explicitly surveys the same competing-toolbox landscape (pyDecision, pymcdm, JMcDM) HERA positions itself against, and could serve as an external ranking-agreement baseline.

4. **Kizielewicz, B., Shekhovtsov, A. & Sałabun, W.** pymcdm — the universal library for solving multi-criteria decision-making problems. *SoftwareX* 22, 101368 (2023). doi:10.1016/j.softx.2023.101368. Already cited as ref. 9; the most actively maintained Python MCDM library and the most natural empirical benchmark target HERA omits, since pymcdm implements COMET and PROMETHEE II variants that could be run on HERA's own synthetic datasets for a direct ranking-concordance test.

5. **Matejová, M. et al.** A Multi-Criteria Decision-Making Approach for the Selection of Explainable AI Methods. *Algorithms* 7(4), 158 (2025). A 2025 application of MCDM to benchmark 113 XAI methods using aggregated benchmark and user-study data; relevant as a contemporary example of MCDM applied to a high-candidate-count, multi-metric selection problem analogous to HERA's stated target use case, illustrating how competing frameworks handle candidate pools exceeding HERA's N≈15 ceiling.

6. **Labreuche, C.** Application of multi-criteria decision aiding to quantum benchmarking: some results on scale invariance. In *Quantum Engineering Sciences and Technologies for Industry and Services* (Springer, 2026). A 2025/2026 application of MCDA to benchmarking systems with multiple conflicting KPIs (quantum computing), directly paralleling HERA's neuroimaging use case in structure; useful as a comparator for how scale-invariance and synthesis-of-conflicting-KPI problems are handled outside biomedical contexts, reinforcing that HERA's domain-agnostic design is better positioned against this literature than against digital-health benchmarks.
