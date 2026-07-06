# Trackrad202512456

# Editorial Report
**Manuscript:** "Bridging Clinical and Artificial Intelligence Uncertainty in Diagnosis: An Example of OCT-Based Retinal Disease Classification"
**Corresponding author:** Haoyu Chen (JSIEC / CUHK)

---

## 1. Overall Assessment

This manuscript asks whether uncertainty scores from four uncertainty-quantification (UQ) methods — evidential deep learning (FMUE), test-time augmentation (TTA), MC-dropout Bayesian neural networks (BNN), and deep ensembles, all built on a frozen RETFound encoder with LoRA adaptation — track clinical diagnostic uncertainty in 32 ophthalmologists reading 160 OCT images spanning 16 retinal conditions. The central finding is a dichotomy: sampling-based methods (TTA/BNN/Ensemble) correlate with human uncertainty (confidence, Shannon entropy, interpretation time), while EDL-based FMUE instead self-calibrates against its own errors (OR 16.111), positioning the two paradigms as complementary rather than redundant.

This is a genuine, reasonably well-supported observational finding. But the manuscript sits very close to the authors' own prior work (ref. 14, Peng et al., *Cell Reports Medicine*, 2025), which introduced FMUE, trained it on the identical 82,813-image corpus, and already reported a human-model comparison using a near-identical three-tier ophthalmologist panel and a 160-image (16×10) test set built to test the same underlying question. Two concerns will dominate review: how much here is genuinely incremental beyond ref. 14, and the fact that the headline self-calibration statistic rests on a six-event contingency table.

## 2. Strengths

The four-method benchmark is methodologically disciplined. EDL, TTA, MC-dropout, and ensembling are implemented on an identical frozen backbone, isolating the UQ strategy as the sole variable across models — a cleaner design than most single-method uncertainty papers in ophthalmic imaging, and one that directly supports the manuscript's mechanistic claim about semantic versus perturbation-based uncertainty.

The dual-level correlation analysis is a real contribution. Image-level pooling (Fig. 2) shows strong accuracy–confidence–entropy–time correlations, but the individual-physician analysis shows this breaks down for a meaningful minority of readers (confidence uncorrelated with misclassification in 25% of physicians). Reporting this heterogeneity, rather than only the pooled correlation, is honest and undercuts the common assumption that group-level uncertainty metrics generalize to every reader.

The AI-assistance crossover design, with a one-month washout and GEE modeling for repeated per-image assessments, is sound clinical-epidemiology practice that limits the memory-bias confound common to this literature.

The expertise-stratified AI benefit — juniors gain confidence and speed, experts gain accuracy without behavioral change — is a specific, actionable finding for deployment design rather than a generic "AI helps" claim.

## 3. Weaknesses

The relationship to ref. 14 is the most consequential issue. Ref. 14 already established FMUE on the same 82,813-image training set (explicitly cited here) and already reported FMUE-uncertainty-versus-misclassification in a human-model comparison using a near-identical panel composition (10/11/9 experts/seniors/juniors there vs. 9/12/11 here) and a 160-image, 16-condition test set built the same way; the "OCT reading group" consortium author list is also nearly identical across both papers. The manuscript must state explicitly whether the test set and physician panel here are the same, overlapping, or independently constructed relative to ref. 14, and must isolate what is new beyond adding three baseline UQ methods.

The self-calibration claim central to the abstract and conclusion — FMUE uncertainty predicts its own error (OR 16.111, 95% CI 2.839–91.440, Table 1) — rests on only 6 misclassified images out of 160. An OR this large from six events is inherently unstable, as the CI width itself signals; this should be re-estimated with an exact or Firth-penalized method, or the claim softened.

Multiplicity correction is inconsistent. Benjamini-Hochberg correction is stated only for Figure 3; the many other correlations (Fig. 2; Supplementary Tables 2–8) and per-physician correlation counts are uncorrected despite dozens of tests across 32 physicians and multiple metrics.

Generalizability is limited to one institution and one recurring reading cohort; ground truth incorporated fundus photography that OCT-only readers lacked, which the authors acknowledge but which still inflates the apparent AI-over-physician margin by design.

---

### EDITORIAL INTEGRITY ALERT (for handling editor)

Independent verification confirms substantial overlap between this submission and the authors' own Peng et al., *Cell Reports Medicine* (2025) (ref. 14): identical FMUE model and training corpus (82,813 images), a near-identical three-tier ophthalmologist panel drawn from the same OCT reading group consortium (author lists overlap almost completely), and an equivalent 160-image/16-condition test-set construction protocol addressing the same core question (model uncertainty vs. clinical uncertainty). Overlap is disclosed for the training-data reuse but not for the study-design overlap. This is not necessarily misconduct — incremental follow-up work is legitimate — but the editor should require authors to explicitly state the relationship between the two studies' cohorts/test sets and to quantify the incremental contribution before this proceeds further.

---

## 4. Editorial Decision

**Send for Review**, conditioned on the authors adding an explicit statement disentangling this study's test set and physician cohort from ref. 14's, and revisiting the sparse-event odds ratio in Table 1. Neither issue is a non-revisable structural flaw; both are addressable through disclosure and reanalysis rather than new data collection. Reviewers should be asked to adjudicate whether the four-method comparison and AI-assistance behavioral analysis constitute sufficient incremental advance over ref. 14, and whether OR 16.111 survives an exact logistic method.

## 5. Suggested Reviewer Expertise

Reviewers should cover: evidential deep learning and Dirichlet-based uncertainty quantification for classification; Bayesian deep learning and MC-dropout epistemic uncertainty in medical imaging; retinal foundation models and OCT-based diagnostic deep learning; human-AI clinical decision-making and diagnostic behavior change under AI assistance; and a practicing vitreoretinal specialist experienced across AMD, PCV, DME, and less common categories such as VKH and RAO/RVO.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field is anchored by RETFound (Zhou et al., *Nature*, 2023), the self-supervised retinal foundation model this manuscript's backbone depends on, and by the same authors' own UIOS (Wang, Lin et al., *Nature Communications*, 2023) and FMUE (Peng et al., *Cell Reports Medicine*, 2025), both built on evidential/Dirichlet uncertainty for retinal disease and open-set detection. Beede et al. (CHI, 2020) remains the most-cited empirical study of AI-assistance behavior change in retinal screening (diabetic retinopathy, Thailand), documenting expertise- and workflow-dependent reliance patterns broadly consistent with this manuscript's expertise-stratified finding — yet the manuscript does not engage with it directly, which reviewers should press on. Methodologically, the four UQ approaches trace to Sensoy et al. (evidential deep learning, NeurIPS 2018) and Gal & Ghahramani (MC-dropout, ICML 2016); benchmarking these against clinician behavior rather than only against each other is where this manuscript could add value, contingent on the ref. 14 overlap being resolved.

## Suggested Reviewers' Names

- Pearse A. Keane or Yukun Zhou — RETFound and foundation-model validation in ophthalmology
- Yarin Gal — MC-dropout Bayesian deep learning
- Murat Sensoy — evidential deep learning methodology
- Emma Beede — human-AI interaction and diagnostic behavior in retinal screening
- Daniel S.W. Ting — clinical translation and validation of ophthalmic AI systems

---

## Further Literature — Extended Set (Past 3 Years)

All entries below are peer-reviewed and independently verified by web search; none are arXiv-only. Entries 1–2 are same-author-group prior work and are the basis of the integrity alert above — included for completeness, not as independent corroborating literature.

1. **Peng Y, Lin A, Wang M, et al.** "Enhancing AI reliability: A foundation model with uncertainty estimation for optical coherence tomography-based retinal disease diagnosis." *Cell Reports Medicine*. 2025;6(1):101876. doi:10.1016/j.xcrm.2024.101876. This is the manuscript's own ref. 14: introduces FMUE, trains it on the same 82,813-image corpus, and already reports an FMUE-uncertainty-vs-misclassification association using a near-identical three-tier ophthalmologist panel and a 160-image, 16-condition test set. Same corresponding authors (Fu, Chen). Directly bears on the overlap concern flagged above, not a distinct comparator.

2. **Wang M, Lin T, Wang L, et al.** "Uncertainty-inspired open set learning for retinal anomaly identification." *Nature Communications*. 2023;14:6757. doi:10.1038/s41467-023-42444-7. Same author group's earlier evidential/Dirichlet uncertainty model (UIOS), applied to fundus photography rather than OCT. Establishes the uncertainty-thresholding methodology that FMUE and the present manuscript both inherit; relevant for assessing what, methodologically, is actually new here.

3. **Zhou Y, Chia MA, Wagner SK, et al.** "A foundation model for generalizable disease detection from retinal images." *Nature*. 2023;622:156–163. doi:10.1038/s41586-023-06555-x. Source of the RETFound encoder backboning all four uncertainty methods in this manuscript. The present manuscript does not test whether its uncertainty-behavior findings are backbone-specific or would hold with a non-RETFound encoder.

4. **Kuo D, et al.** "How Foundational Is the Retina Foundation Model? Estimating RETFound's Label Efficiency on Binary Classification of Normal versus Abnormal OCT Images." *Ophthalmology Science*. 2025;5:100707. PMID:40161460. Independently (non-author-group) stress-tests RETFound's label efficiency on OCT. Relevant because it questions how much of RETFound's advantage survives outside the developing group's own pipelines — a generalizability question this manuscript does not address for its own RETFound-LoRA models.

5. **Du K, et al.** "Detection of Disease Features on Retinal OCT Scans Using RETFound." *Bioengineering (Basel)*. 2024;11:1186. PMID:39768004. Independent group applying RETFound to OCT disease-feature detection against a ResNet-50 baseline, finding comparable rather than superior performance — a useful counterpoint to this manuscript's framing of foundation-model uncertainty as straightforwardly superior to conventional baselines.

6. **Xia T, Dang T, Han J, Qendro L, Mascolo C.** "Uncertainty-Aware Health Diagnostics via Class-Balanced Evidential Deep Learning." *IEEE Journal of Biomedical and Health Informatics*. 2024;28(11):6417–6428. doi:10.1109/JBHI.2024.3360002. Shows that standard evidential deep learning (the FMUE approach) is biased under class imbalance and proposes a corrective pooling loss. Directly relevant: this manuscript's 16-condition dataset (10 images/condition) likely does not reflect real-world prevalence, and this potential confound in the FMUE self-calibration result is not addressed.

7. **Alves N, Bosma JS, Venkadesh KV, et al.** "Prediction variability to identify reduced AI performance in cancer diagnosis at MRI and CT." *Radiology*. 2023;308(2):e230275. doi:10.1148/radiol.230275. Uses prediction variability under perturbation (conceptually equivalent to this manuscript's TTA/Ensemble arms) to flag degraded AI performance in a different imaging domain — external validation that sampling-based variance-as-uncertainty generalizes beyond ophthalmology.

8. **Zou K, Chen Y, Huang L, et al.** "Toward Reliable Medical Image Segmentation by Modeling Evidential Calibrated Uncertainty." *IEEE Transactions on Cybernetics*. 2025 (IEEE Xplore document 11176052). Same senior authors (Fu, Wang) applying Dirichlet/evidential uncertainty to segmentation rather than classification. Another instance of the group's recurring evidential-uncertainty pipeline across tasks; relevant context for judging the marginal novelty of applying the same machinery to a new classification dataset.

9. **Lambert B, Forbes F, Doyle S, Dehaene H, Dojat M.** "Trustworthy clinical AI solutions: a unified review of uncertainty quantification in deep learning models for medical image analysis." *Artificial Intelligence in Medicine*. 2024;150:102830. Independent review of UQ methods (EDL, MC-dropout, ensembles, TTA) across medical imaging — a non-author-group framing of the same four-method landscape this manuscript benchmarks, useful for judging whether method selection and terminology are standard.

10. **Chen M, Wang Y, Wang Q, Shi J, Wang H, Ye Z, Xue P, Qiao Y.** "Impact of human and artificial intelligence collaboration on workload reduction in medical image interpretation." *npj Digital Medicine*. 2024;7(1):349. doi:10.1038/s41746-024-01328-w. Meta-analysis of 36 studies: AI concurrent assistance reduces reading time by ~27% pooled. Directly comparable to this manuscript's Figure 4C interpretation-time findings; the manuscript neither cites this nor situates its own effect size against the pooled literature estimate — reviewers should request this.

053691
# Editorial Report: TheraNephroSpec-Mamba (TNS-Mamba)

**⚠ FORMAL EDITORIAL ALERT — UNDISCLOSED AUTHOR OVERLAP AND LIKELY COHORT REUSE**

Independent literature search identified two closely related prior publications by an overlapping author set that are not cited or disclosed in this manuscript. Liu, Hou, Li, and Wang published "Hyperspectral imaging to predict the effect of cyclophosphamide in primary membranous nephropathy" (2023), using the identical 400–1000 nm HSI acquisition range and a spectral CNN to classify remission versus non-remission in PMN. Sun, Zhang, Tian, Wang, Liu, Li, Lv, and Wang published "A Novel Classification Model Based on Hyperspectral Imaging for Predicting Response to Tacrolimus in Patients With Primary Membranous Nephropathy" (J Biophotonics, 2025), again using HSI-based spectral classification of remission status in PMN. Four authors of that 2025 paper — Tian, Wang (Ruiyang), Li (Yang), and Wang (Zunsong, corresponding author on both) — are also authors on the present submission. This is a direct, undisclosed overlap in personnel, disease model, treatment-response endpoint, and acquisition hardware/spectral range across at least three sequential single-drug or omnibus papers from what appears to be the same sample source. The handling editor must require the authors to disclose these prior publications, clarify whether any patients or biopsy slides are shared across the three studies, and explain how the present multicenter cohort's relationship to the earlier single-center tacrolimus and cyclophosphamide cohorts is not simple data augmentation of previously published material presented as a new architecture.

## 1. Overall Assessment

The manuscript proposes TNS-Mamba, a treatment-conditioned spectral–spatial state-space MIL model that classifies 12-month remission (CR/PR/NR) in membranous nephropathy from pretreatment renal-biopsy hyperspectral imaging, externally validated at two independent centers (macro-AUC 0.902). The central claim — that renal HSI adds prognostic value beyond clinical variables and conventional pathology when interpreted conditional on the treatment actually given — is reasonably well supported by the reported numbers. However, given the undisclosed prior work above, the paper's novelty rests almost entirely on the architectural upgrade from 1D-CNN to a selective-SSM/Mamba backbone with compartment-aware attention, not on the underlying biological or clinical premise, which this same group has published in narrower form at least twice already.

## 2. Strengths

External validation at two institutionally independent, prospectively locked cohorts (n=255, n=251) with no involvement in preprocessing, threshold selection, or model selection is methodologically sound and rare in HSI pathology work.

The treatment-conditioning mechanism (Eq. 9–10, FiLM-style modulation) and explicit clinical co-attention (Eq. 12) are a genuine architectural contribution addressing a real problem: remission is observed-regimen-specific, and pooling across five heterogeneous treatment strata without conditioning would confound the signal.

The ablation study (Supplementary Table S6) and reported ~13-point macro-AUC gap between the full model and the non-treatment-conditioned state-space comparator support that compartment-aware and treatment-conditioning components are doing real work, not just adding parameters.

Calibration reporting (slope, intercept, ECE, Brier) alongside discrimination, and adherence to TRIPOD+AI/CLAIM structure, meets a reporting bar many comparable HSI papers fail.

## 3. Weaknesses

Beyond the disclosure issue above, the anti-CD20 (n=33) and glucocorticoid-monotherapy (n=37) subgroup validations are far too small to support the treatment-stratified claims made in Table 5; wide, overlapping CIs (0.861–0.938) do not distinguish these strata from noise.

All three cohorts share the same ATH5010 platform and harmonized acquisition specification; the authors correctly flag this as cross-institution but not cross-device generalizability, which materially limits real-world deployment claims given known HSI sensitivity to scanner/staining batch effects.

Treatment assignment is confounded by indication and not addressed by anything stronger than overlap weighting and propensity adjustment (Supplementary Table S4); residual confounding cannot be ruled out, and the paper's own honest admission that the model cannot support treatment selection undercuts its primary claimed clinical utility pathway.

The comparator set, while extensive (11 models), does not include a foundation-model pathology encoder (e.g., UNI, CONCH) or MambaMIL/2DMamba applied directly as an off-the-shelf baseline, leaving open whether the gain is from bespoke architecture or simply more capacity.

## 4. Editorial Decision

**Reject, pending author clarification of undisclosed prior publications** — this is not revisable at the review stage. If the authors can demonstrate the cohorts are non-overlapping and disclose the relationship to the 2023 and 2025 papers, this could be **sent for review** with reviewers specifically charged to adjudicate: (1) whether the biopsy sample library overlaps across the three papers; (2) whether the incremental architectural contribution over MambaMIL/structured-SSM MIL baselines is sufficient for this venue; (3) adequacy of the anti-CD20/glucocorticoid subgroup claims.

## 5. Suggested Reviewer Expertise

State-space/Mamba sequence modeling for computational pathology and multiple-instance learning; hyperspectral/spectral-imaging signal processing and calibration for tissue phenotyping; multicenter clinical prediction-model validation methodology (TRIPOD+AI, calibration, decision-curve analysis); treatment-selection bias and causal inference in observational nephrology cohorts; clinical nephropathology of membranous nephropathy and immunosuppressive treatment response.

## 6. State-of-the-Art Literature Review

MIL in computational pathology has moved rapidly from attention-based pooling and TransMIL (2021) toward state-space backbones: MambaMIL (MICCAI 2024) and the structured-SSM MIL formulation of Fillioux et al. (MICCAI 2023) established selective scanning as an efficient alternative to transformer attention for long instance sequences, and 2DMamba (CVPR 2025) extended this to native 2D scanning for gigapixel WSIs. SurvMamba (2024) and several 2025 graph-Mamba hybrids applied similar architectures to multimodal survival prediction. TNS-Mamba's spectral-plus-spatial dual-branch design is a reasonable domain-specific adaptation of this line of work to the wavelength dimension, but it is not the first HSI-remission classifier in PMN: the group's own 2023 (cyclophosphamide, 1D-CNN) and 2025 (tacrolimus, RCN/RVM) papers already established the core premise that HSI spectral signatures separate remission from non-remission in this disease. The present paper's actual advance is extending that premise to five treatment regimens with explicit conditioning and two-center validation — a real but incremental step that should have been framed, and cited, as such.

053828
# Editorial Report

**Manuscript:** "Training clinical decision-support agents to investigate and diagnose through reinforcement learning" (Qiu, Wu, Liu, Zheng et al.)

---

**⚠ EDITORIAL INTEGRITY ALERT (read before decision below)**

Independent search identifies an arXiv preprint, *"Evolving Diagnostic Agents in a Virtual Clinical Environment"* (arXiv:2510.24654, posted 28 Oct 2025), authored by the **identical 14-author list** (Qiu, Wu, Liu, Zheng, Liao, H. Wang, Yue, Fan, Zhen, J. Wang, Gu, Y. Wang, Zhang, Xie), describing the same DiagGym world model, DiagAgent policy, and DiagBench benchmark, with closely related (though not identical) quantitative results. The submitted manuscript does not cite or disclose this preprint anywhere. This is either an undisclosed prior publication of substantially the same work or a concurrent dissemination that the authors are obligated to declare and differentiate. This must be resolved before any decision is finalized, independent of the scientific merits below.

---

### 1–4. Overall Assessment, Strengths, Weaknesses, Editorial Decision

The manuscript proposes DiagGym, an EHR-trained generative world model that simulates test results, and DiagAgent, an RL policy (GRPO) trained inside DiagGym to jointly optimize investigation ordering and final diagnosis. Evaluation spans DiagBench (2,257 cases, 4 sources) with automated hit-ratio/F1/accuracy metrics, physician Likert ratings (12 raters, 6,000 annotations), and 3,318 physician-authored rubrics.

Strengths are substantial. The world-model-as-environment approach is a genuine mechanism for solving an important and under-addressed problem: static instruction-tuning cannot supervise counterfactual test orderings. The dual-reward design (diagnosis + investigation alignment) is empirically justified by the ablation showing hit-ratio collapse under diagnosis-only reward. Physician validation is unusually rigorous for this literature — three independent raters per instance, majority-vote consistency reporting, and weighted rubrics rather than accuracy alone. Generalization is demonstrated across three model families/sizes and to three out-of-domain sources never used in world-model training.

Weaknesses are also substantial. First, the investigation-recommendation reward (r_exam) is F1 against a single physician-derived reference trajectory, and the same LLM-judge (Qwen2.5-72B) computing this reward also computes it as the primary automated evaluation metric — the objective and the yardstick are the same instrument, raising circularity concerns for a task where multiple test orderings are often equally valid. Second, the "behavioral analysis" rollouts (Figs. 5–6), which produce the largest headline margins, are entirely self-generated against DiagGym rather than real records; the authors flag this appropriately, but reviewers should require the main-evaluation numbers (Table 4, static reference matching) as the load-bearing claim, not the simulated-rollout numbers. Third, DiagGym is trained solely on single-center MIMIC-IV (ICU/ED); no demographic subgroup analysis (age, sex, ethnicity) is reported despite this being standard practice for diagnostic-AI submissions. Fourth, there is no discussion of deployment safety, human-in-the-loop fallback, or regulatory framing for a system that recommends clinical tests.

**Decision: Send for Review**, conditional on resolution of the integrity alert above. The core weaknesses (metric circularity, subgroup analysis, deployment framing) are reviewer-addressable through additional analyses and reframing, not structural flaws requiring new data collection. Reviewers should be explicitly asked to (i) adjudicate whether reward-metric circularity meaningfully inflates reported gains, and (ii) require subgroup and safety/deployment discussion as a condition of acceptance.

---

### 5. Suggested Reviewer Expertise

Technical: RL for sequential clinical decision-making under partial observability; LLM-based generative world models / synthetic EHR simulation; benchmark construction for multi-turn diagnostic agents. Clinical: emergency/internal medicine differential diagnosis workflows, particularly test-ordering strategy under diagnostic uncertainty; clinical AI safety and deployment standards.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

Multi-turn clinical-agent evaluation has moved rapidly from static QA (MedAgents, MDAgents) toward interactive settings. DoctorAgent-RL (arXiv:2505.19630) reformulates clinical consultation as an MDP trained with a patient-simulator agent, addressing the single-round history-taking limitation of prior supervised multi-turn systems, but that work targets pre-diagnosis history-taking dialogue rather than test-ordering after initial presentation — the manuscript's stated distinction from DoctorAgent-RL is accurate. Separately, MIMIC-CDM (Hager et al.) and its RL extension "Language Agents for Hypothesis-driven Clinical Decision Making" model sequential test-ordering directly on MIMIC-IV abdominal-pain cases, which is the closest prior comparator to DiagAgent's core task and is conspicuously absent from the manuscript's related-work discussion — this omission should be raised with authors. MedAgents (2311.10537) and MDAgents (2404.15155) established multi-agent collaborative reasoning for medical QA, which the manuscript correctly repurposes as agentic baselines and correctly finds underperforming on the investigation-ordering task, consistent with those systems' original QA-only design.

---

### 5. Suggested Reviewers' Name

- **Paul Hager** — PhD researcher, Institute for AI and Informatics, TU Munich. Directly comparable article: Hager et al., *Nature Medicine* 2024 (MIMIC-CDM, sequential clinical decision-making with LLMs).
- **Samuel Schmidgall** — PhD candidate, Johns Hopkins University / Google DeepMind. Directly comparable article: Schmidgall et al., AgentClinic (arXiv:2405.07960), multi-agent simulated clinical environments.
- **Jeffrey K. Jopling** — Assistant Professor of Surgery, Johns Hopkins Medicine. Clinical co-author on AgentClinic; can assess clinical realism of simulated test-ordering trajectories.

(No full professor added — sufficient directly comparable expertise was found at postdoc/junior-faculty level.)

---

### 7. Further Literature (8–10 papers, past 3 years)

1. **Hager, P. et al.** Evaluation and mitigation of the limitations of large language models in clinical decision-making. *Nat. Med.* 30, 2613–2622 (2024). DOI: 10.1038/s41591-024-03097-1. Peer-reviewed. Introduces MIMIC-CDM, the closest prior sequential test-ordering benchmark; the manuscript should cite and differentiate DiagBench from it.
2. **Schmidgall, S. et al.** AgentClinic: a multimodal agent benchmark to evaluate AI in simulated clinical environments. arXiv:2405.07960 (2024). **Unreviewed preprint — flagged.** Comparable multi-turn simulated-environment paradigm; differs by using an LLM-as-patient rather than an EHR-trained world model.
3. **Feng, Y. et al.** DoctorAgent-RL: A multi-agent collaborative RL system for multi-turn clinical dialogue. arXiv:2505.19630 (2025), accepted ICASSP 2026. Directly relevant RL-for-clinical-dialogue comparator; scope differs (history-taking vs. test-ordering).
4. **Chen, X. et al.** Enhancing diagnostic capability with multi-agents conversational large language models. *npj Digit. Med.* 8, 159 (2025). Peer-reviewed. Multi-agent diagnostic conversation system; useful contrast to DiagAgent's single-policy RL approach.
5. **MedAgentBoard** (arXiv:2505.12371, 2025). **Unreviewed preprint — flagged.** Systematic benchmarking of multi-agent vs. conventional methods across medical tasks; contextualizes why MedAgents/MDAgents underperform as diagnostic baselines here.
6. **Language Agents for Hypothesis-driven Clinical Decision Making with RL** (arXiv:2506.13474, 2025). **Unreviewed preprint — flagged.** RL-trained hypothesis/decision agent pair on MIMIC-CDM; closest direct methodological competitor to DiagAgent and should be discussed explicitly by the authors.
7. **Kim, Y. et al.** MDAgents: An adaptive collaboration of LLMs for medical decision-making. arXiv:2404.15155 (2024). **Unreviewed preprint — flagged.** Baseline used in the manuscript; included here for completeness of the agentic-systems comparison class.
8. **Tang, X. et al.** MedAgents: LLMs as collaborators for zero-shot medical reasoning. arXiv:2311.10537 (2023–24). **Unreviewed preprint — flagged.** Original QA-only framing of the baseline reused here; manuscript should note the task mismatch when using it as a diagnostic-agent baseline.
9. **Sellergren, A. et al.** MedGemma technical report. arXiv:2507.05201 (2025). **Unreviewed preprint — flagged.** Underlies the MedGemma-27B baseline; relevant for interpreting that baseline's medical specialization.
10. **Deep-DxSearch** (cited in radiology-agent surveys as end-to-end RL for retrieval-aware diagnosis, 2025). Latest-generation RL-for-diagnosis comparator; authors should confirm publication status and cite directly rather than through a survey reference.
