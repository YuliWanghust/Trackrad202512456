# Trackrad202512456

## Reviewer positions

**Reviewer 1 (Lingyao Li)** — the LLM component is not shown to be doing the work. The gain over the random-forest baseline is demonstrated only on a single 400-case balanced cohort, while every headline claim on the n=9,111 independent cohorts is benchmarked against CETIS-2020-CI alone. The ablations show the naive CETIS+LLM merge at 0.290 and the full cascade at 0.968, which points to the integration logic rather than the LLM as the source of performance. The refined rules are one- or two-condition thresholds that conventional rule optimization could plausibly recover. He also asks for latency and cost of the LLM stage, notes that the added citations are drawn from Nature-family journals rather than the ML/NLP venues where the closest competing methods appear, and reports that the repository still does not run: script 01 imports an `aitriage.development` module absent from the release and the prompt template is missing, so the final rules can be applied but not regenerated. A response-letter inconsistency is flagged regarding the vanilla-LLM ablation cells.

**Reviewer 2 (Wu Seong Kang)** — substantively satisfied. Residual request is statistical reporting: near-horizontal DCA curves for both models across a broad threshold range require confirmation that continuous predicted probabilities were used, plus clarification of DCA methodology and the clinically relevant threshold range, together with calibration plots, calibration intercept and slope, and Brier scores for both models.

**Reviewer 3 (Feng Xie)** — five substantive issues. The reference standard is nurse-assigned triage, so agreement establishes reproduction of local practice, not clinical correctness or outcome benefit, and the framing should change accordingly. The ablation pattern raises the same LLM-necessity question R1 raises, and he asks explicitly whether a non-LLM rule optimizer inside the same cascade matches performance. The Level-1 rescue analysis reports 47 of 56 captured but omits the false-alarm burden; he wants level-specific sensitivity, specificity, PPV, NPV, false-positive rate, and the count of true Level 2/3/4 patients pulled into Level 1. External validity is weakened because county-hospital labels were reviewed and calibrated by expert nurse panels from the development institution, making this partly an agreement test with the development standard. Finally, specificities of 1.000 or near-1.000 in the final cascade are implausible given the poor specificity of the LLM-refined rules alone, and require recalculation, explicit denominators, level-specific confusion matrices, and over-/under-triage rates.

**Reviewer 4 (Yanwei Jin, ECR co-reviewer)** — the released inference code implements a materially more elaborate cascade than the Methods describe, including four rule roles and stability guards that suppress escalation rather than assign a level. His conclusion is the decisive one: the reported results cannot be derived from the manuscript as written.

## Decision: Major revision

Not reject. No reviewer recommends rejection, R2 is close to satisfied, and R3 frames his concerns as clarifications required before acceptance. The defects are documentation, ablation design, and metric reporting — all correctable without new data collection.

But this must be a conditional revision with a stated failure mode. R1 and R4 independently inspected the code and independently concluded the implemented pipeline differs from the described one. That is not a presentation complaint; combined with R3's implausible specificities, it means the reported numbers currently have no verifiable provenance. The revision request should therefore require: a Methods section that describes the actual four-role cascade including the escalation-suppressing stability guards; a runnable repository with the missing module and prompt template, plus a reproduction script regenerating the headline table end-to-end; a non-LLM rule-optimization arm inside the identical cascade; level-specific confusion matrices with denominators stated; a sensitivity analysis on uncalibrated county-hospital labels; and the calibration and DCA package R2 asked for. If the code-to-Methods reconciliation fails or the headline metrics do not reproduce, reject at the next round rather than requesting a third revision.

One item to resolve before transmitting: R1's phrasing "modest (0.877 vs 0.968)" is internally inconsistent — a 9-point AUC gap is not modest, and it is unclear whether 0.877 is the RF or the proposed model. Ask him to clarify, or the authors will rebut the wrong claim.

## Counterargument for reject

A defensible reject exists. After a full revision round with four reviewers, the paper's central novelty claim — that LLM-based rule refinement is what enables the performance — remains unsupported by the authors' own ablations, and the 0.290-to-0.968 pattern suggests the claim is misattributed at the level of the science, not the writing. A manuscript whose results cannot be derived from its own Methods has already failed the reproducibility bar that Nature Communications applies, and asking for a second round rewards the authors for a repository that was flagged as unrunnable in the previous round and is still unrunnable. If the authors' next response again fails to reconcile code and Methods, the editorial record will show two avoidable rounds.

## What you are not asking

First, ceiling. Even if every point is addressed, the contribution is a locally-calibrated triage rule system validated against nurse labels at institutions sharing a calibration standard, with no outcome-linked endpoint. That is a Communications Medicine or npj Digital Medicine paper more than a Nature Communications one. Decide now whether you are running a revision toward acceptance or toward transfer, and say so in the letter rather than discovering it at round three.

Second, integrity handling. A discrepancy between released code and described Methods, plus specificity values of exactly 1.000, is the pattern that warrants requesting raw per-patient prediction files and the label files for an independent recomputation, not just a rebuttal. That request belongs in this letter, not the next one.

Third, reviewer load. You have four reports and clear convergence. Do not recruit a fifth reviewer or a statistical reviewer for round two; ask R1, R3, and R4 to re-examine only the code-reproducibility and ablation items, and release R2.

## What the reviewers actually said

**Reviewer #2 (Maloca, associate professor, Switzerland)** submitted one substantive paragraph and roughly eighty line-level edits. The substantive paragraph is the important one: monocular 3D reconstruction from a single 2D fundus photograph is a mathematically underdetermined inverse problem, so infinitely many 3D surfaces project to the same image. The output is therefore only meaningful to the extent that it is identifiable and stable out of distribution. He asks for proof of identifiability, external validation against real 3D references, error distribution across the surface rather than a single aggregate, explicit handling of out-of-distribution inputs, and uncertainty quantification that signals when the model is guessing. He also disputes three specific claims: that "full-field" is achievable from a fundus image covering only a 20 × 20 mm posterior patch, that OCT-based PES reconstruction is "too burdensome" when the TowardPi BMizar SS-OCT platform already does it in seconds, and that a 0.070 mm RMSE is impressive without stating what ground truth it is measured against. He notes device details and basic clinical characteristics (age, stage, sex, surgical status) are missing. The rest is copyediting.

**Reviewer #3 (Moradi, postdoc, US)** is the technically decisive report. Nine major points: (1) "micrometer-scale" is overclaimed — 0.070 mm is 70 µm against a ground truth whose own verification RMSE is 0.037 ± 0.008 mm, and the surface reconstructed is Bruch's membrane, not sclera; (2) the ground-truth pipeline (BM segmentation, NURBS fitting, LightGlue SLO-to-CFP registration) has no reported QC metrics, exclusion rates, or error-propagation analysis; (3) the split level is unstated — patient, eye, or image; (4) external evaluation uses 45° CFPs against 6 × 6 mm OCT while internal uses 20 × 20 mm, so full-field performance is not externally demonstrated; (5) the PM AUC rests on a two-component GMM whose training and evaluation sets may be identical, which would make 0.95 circular; (6) glaucoma and AMD AUCs (0.92, 0.89) are unadjusted for age, axial length, refraction, device, and center; (7) the 10-year incident PM comparison (0.90 vs 0.78) benchmarks PES only against refractive error, with no multivariable model, no calibration, no decision-curve analysis, and no accounting for inter-eye correlation; (8) clinical utility claims outrun retrospective evidence; (9) missing ablations for the super-resolution branch, dual-branch ViT, refinement head, and uncertainty head. Minor points include a figure-caption contradiction and absent confidence intervals.

## Decision

**Major revision, not reject.** Neither reviewer identifies an unfixable flaw, and both wrote revision-shaped reports. The distinctive asset — a 726-eye prospective cohort with 155 incident PM cases over ten years — cannot be replicated by competitors and survives every criticism raised. Most objections are reframing (Bruch's membrane, sub-0.1 mm rather than micrometer-scale, "posterior region" rather than "full-field") or reanalysis on data already held (adjusted models, calibration, CIs, ablations, stratified external error).

Two items must be conditions, not suggestions. First, the split level: the development set is 288 eyes yielding exactly 6 CFPs and 96 OCT B-scans per eye. If that split was at image level rather than participant level, internal performance is meaningless and the paper becomes a reject. Ask for this before the revision is written. Second, the GMM: if clustering and AUC came from the same eyes, the headline PM result is circular and must be recomputed on held-out data.

## The counterargument I would expect

A case for rejection exists. Strip the overclaims and what remains is a model predicting an OCT-derived Bruch's membrane contour, trained on 288 eyes, validated in an ethnically homogeneous population, where the decisive clinical claim may be circular. If the GMM and split questions both resolve badly, there is no paper left, and inviting revision costs the authors six months to reach the same endpoint. I still favour revision because the prospective cohort is genuinely rare, but the invitation should be explicitly conditional.

## What you have not asked but should

The reviewers did not raise ethnic homogeneity or cross-vendor geometric calibration, both of which appeared in your own pre-review assessment and will not reach the authors unless you add them to the decision letter. Nobody asked the clinically decisive question either: whether PES adds incremental value over axial length and refraction in a *combined* model, rather than beating them head-to-head — a marker that only wins when used alone is not a marker anyone will adopt. Novelty also needs restating: if Maloca is right that the BMizar platform already reconstructs PES on-device, and the authors used that platform for ground truth, the contribution is PES *without* OCT, and the framing must change accordingly. Finally, both reviewers declined to examine the code, and only two of three reports returned; given the circularity and DeLong issues, consider adding a statistician before the revision comes back.

# Editorial Report — Manuscript 070143

**Title:** Integrating Single-Molecule Variant Phenotyping with Clinical Features Predicts Outcomes in KIF1A-Associated Neurological Disorder
**Handling section:** Nature Communications — Digital Health

---

## 1. Overall Assessment

The manuscript claims single-molecule phenotyping of 91 KIF1A variants, added to clinical/computational data, yields individualized KAND prognosis via a two-stage Random Forest (AUC 0.834; r² = 0.484, age ≥10). The smTIRF dataset is unmatched for a motor protein disease, but the prognostic claim is unestablished: labels are partly definitional (thresholded VABS ABC; death before 10 forces Group 2), and value over clinical variables alone is never benchmarked against the authors' own prior model (34% variance from EEG/seizure and ESM; Sudnawa et al. 2024).

---

## 2. Strengths

Ninety-one variants across 66 residues assayed by smTIRF with MTBR pre-clearing is an unmatched panel. The switch-I loop series (A206V, M210T, S215R, R216C) shows structural proximity does not predict function. Growth Scale Values across 11 VABS-3 subdomains suit this floor-prone population. Leave-one-variant-out cross-validation correctly prevents recurrent variants (R254W n=31) from leaking across folds. Withdrawing the play-and-leisure correlation once found driven by one observation is honest handling of a fragile result.

---

## 3. Weaknesses

The classification target is circular: VABS ABC below 50 defines Group 2, and death before 10 forces the label, after which a 5.8-fold mortality difference is reported as a finding. "r² = 0.484" is a squared Pearson r, not R², for a post hoc subgroup (whole-cohort r²=0.419). No clinical-only model is reported, so the assay's marginal value is unreadable. Hyperparameters were tuned on the full dataset before cross-validation, and Stage 1 predictions leak across co-carriers into Stage 2 training. No external validation, no subgroup analysis, and inconsistent cohort counts (343 vs. 313; 35% reported for 101/291, not 101/313).

---

## 4. Editorial Decision

**Reject**, transfer to **Communications Medicine** or **npj Genomic Medicine**. The claim rests on a circular label, a mislabeled metric, and a missing baseline comparison — re-analysis, not discussion, is required. The molecular resource is publishable elsewhere on its own terms.

**Steelman.** Circularity is near-unavoidable without a biomarker, and ablation shows AUC falling 0.804→0.753 without molecular features — independent signal exists. The panel is not quickly reproducible, favoring major revision over rejection. I do not adopt it: the 34%-variance benchmark is not shown to be beaten.

---

## 5. Suggested Reviewer Expertise

Five areas are needed. (i) Single-molecule TIRF characterisation of kinesin-3 motors, specifically velocity, run length, dwell time and rigor-binding phenotypes in KIF1A disease variants, including expertise in homodimer versus heterodimer constructs. (ii) Calibration and clinical interpretation of functional and multiplexed assays of variant effect, including ClinGen functional-evidence frameworks and the comparative performance of REVEL, gMVP, ESM-1b, AlphaMissense and MisFit. (iii) Machine learning for prognosis in small-n cohorts, covering nested cross-validation, leakage from hyperparameter tuning, calibration assessment and bootstrap confidence intervals on performance differences. (iv) Psychometrics of the Vineland Adaptive Behavior Scales and Growth Scale Values in neurodevelopmental populations, including floor effects, caregiver-report bias and longitudinal trajectory modelling. (v) Clinical neurogenetics of developmental and epileptic encephalopathies and hereditary spastic paraplegia, with direct experience of KAND natural history, EEG phenotyping and optic nerve involvement.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

Three lines of work define the current landscape. On the molecular side, Benoit et al. (Nat Commun 2024) resolved cryo-EM structures of KIF1A on microtubules and the mechanism by which P305L degrades processivity, and Budaitis et al. (J Cell Biol 2021) established that KAND variants impair force generation allosterically; and Borland and colleagues (bioRxiv 2026.01.14.699478, posted 14 January 2026; preprint, not peer reviewed) compared loss-of-function (C92*, P305L) against hyperactive (R350G) alleles in isogenic gene-edited human iNeurons and found opposite directions of effect on synaptic maturation — directly competing work the authors do not cite. On the computational side, AlphaMissense (Cheng et al., Science 2023), ESM-1b (Brandes et al., Nat Genet 2023) and MisFit (Zhao et al., Nat Commun 2025) have made proteome-wide variant scoring routine, while the MAVE community has moved toward assay calibration against clinical evidence rather than raw correlation with outcome; the manuscript reports correlations but never calibrates its assay to an interpretable evidence strength. On the clinical side, Sudnawa et al. (Genet Med 2024) and Kaat et al. (J Child Adolesc Psychopharmacol 2025) established the VABS and Growth Scale endpoints for trial readiness in KAND and SCN2A respectively.

Against this landscape, the manuscript advances scale — 91 variants assayed uniformly is a real contribution and exceeds any published KIF1A functional series. It replicates rather than extends the genotype–phenotype correlation itself, which Boyle et al. (2021) and the authors' own Rao et al. (2025) already reported. The bifurcated trajectory finding parallels descriptions in SCN1A-positive Dravet syndrome (Feng et al., Brain Commun 2024) and is not distinctive on its own. The authors should engage explicitly with the gain-of-function KIF1A literature, with the ClinGen functional-evidence calibration framework, and with their own published 34% variance benchmark, which is the correct comparator for any claim of prognostic improvement.

---

## 7. Suggested Reviewers

*Single-molecule kinesin biophysics:* Kyoko Chiba (Tohoku University; KIF1A autoinhibition and hyperactivating variants, PNAS 2019, J Cell Sci 2023); Breane Budaitis (KIF1A force generation and allosteric disruption, J Cell Biol 2021); Nida Siddiqui (kinesin force generation impaired by pathogenic mutations, Curr Biol 2022). Shinsuke Niwa (Tohoku) holds the most directly comparable expertise but is a full professor and a direct competitor on the gain-of-function question; use only if the above decline.
*Variant-effect prediction and assay calibration:* Nadav Brandes (University of California, San Francisco); Alan Rubin (Walter and Eliza Hall Institute); Jochen Weile (University of Toronto); Shawn Fayer (University of Washington).
*Machine learning for small-cohort prognosis:* Ahmed Alaa (UC Berkeley / UCSF); Bo Wang (University of Toronto); Stephen Pfohl (Google Research).
*Adaptive behaviour psychometrics:* Aaron Kaat (Northwestern University); Vanessa Bal (Rutgers University).
*Clinical neurogenetics of KAND and DEE:* Ingo Helbig (Children's Hospital of Philadelphia); Julie Xian (Children's Hospital of Philadelphia); Filippo Nicita (Bambino Gesù Children's Hospital).

Exclusions: Columbia University Irving Medical Center, Albert Einstein College of Medicine, Boston Children's Hospital, Harvard Medical School, and any current or former co-author of Chung, Gennerich or Shen.

---

## Confidential Editorial Integrity Alert (handling editor only)

Three items warrant clarification from the authors before any further consideration.

First, cohort and data overlap. The clinical cohort appears to extend the cohort reported in Sudnawa et al., Genet Med 2024 (177 individuals, same recruitment pathway, same EEG/seizure and ESM analyses, same senior author), and at least part of the smTIRF dataset overlaps Rao et al., Biomolecules 2025 (R216, R254, R307 series, same first author and same construct). Neither overlap is declared. A statement specifying which patients and which variant measurements are previously published is required.

Second, cohort size inconsistency. 343 versus 313 individuals across Abstract, Introduction, Results 2.1 and Discussion, with a denominator error in the recurrent-variant percentage (101/291 = 34.7% reported as 35% of a stated 313-person cohort, where the correct figure is 32.3%). This must be reconciled.

Third, reference 7 (Shatarupa et al., Nat Commun 2026) is cited without volume or pages; it is now published as Nat Commun 2026;17(1):5175 and shares two authors with this submission (Rao, Gennerich). Self-citation density across refs 3, 4, 5, 6, 7, 13, 19 and 32 should be noted when selecting reviewers.

Fourth, metric labelling. The Abstract presents "R² = 0.484" for a quantity the Methods identify as a Pearson correlation squared. In a prognostic paper this is a material misstatement of model performance and should be corrected regardless of venue.

# Editorial Report — Manuscript 074770

**Title:** GeoSentinel-DCM: LGE-conditioned multimodal digital twin framework for prognostication in non-ischemic dilated cardiomyopathy
**Recommendation: Reject**

---

## 1. Overall Assessment

The authors propose GeoSentinel-DCM, a four-pillar prognostic framework for non-ischemic DCM combining Elastic-Net Cox regression on 27 clinical and CMR variables (B1), a two-layer GraphSAGE network on a 388-vertex time-resolved biventricular control mesh (B2), a Random Survival Forest, gradient-boosting and DeepSurv ensemble on 5,810-vertex subdivided-surface morphometrics (B3), and a ridge Cox kinematic model (B4). Pillar scores are rank-normalized, weighted according to binary LGE status through subgroup-adaptive routing, then passed to a Random Survival Forest meta-learner. Development used 399 patients across four Chinese centres and external validation used 149 patients from a fifth. Reported C-indices are 0.881 internally and 0.778 externally for the composite of cardiac death, sudden death, or heart transplantation.

The reconstruction pipeline and the ablation design are genuine assets. The central claim is not supported by the reported numbers. The decision curve analysis is arithmetically impossible, the headline subgroup result rests on approximately three events, and the internal C-index of the conditioned-fusion configuration behaves in a way no other configuration in Table 2 does. These are not presentational problems.

## 2. Strengths

The imaging infrastructure is careful and reusable. A subject-independent 388-vertex biventricular template with fixed topology is diffeomorphically fitted to slice-corrected contours, then refined by two Catmull-Clark subdivisions to 5,810 vertices. Mean point-to-surface reconstruction error is below 2 mm and vertex correspondence is preserved across subjects. Because both mesh levels share that correspondence, the same anatomy supports graph-based learning and explicit regional morphometry without separate registration. This is a defensible basis for geometric deep learning on cine CMR.

The ablation in Table 2 is unusually complete and, to the authors' credit, is what makes the paper falsifiable. Thirteen configurations spanning single pillars, pairwise fusion, three-pillar fusion, uniform four-pillar fusion and conditioned fusion are reported with paired internal and external C-indices. Most submissions in this area report only the final model.

The kinematic pillar is the most credible finding in the paper. B4 alone reaches an external C-index of 0.754 against 0.673 for the clinical baseline, the highest external value of any single pillar, and it transfers across cohorts better than the learned mesh representation. The authors also correctly decline to call SSHI a strain measurement, noting that it derives from cine-based geometric deformation rather than tagging or DENSE. The domain-adversarial gradient-reversal head and sub-1.2-second inference time are appropriate engineering choices.

Endpoint handling is sound. Events were adjudicated by two physicians blinded to CMR findings and model output, censoring was to a common date of June 2024, and the external cohort is stated to have been excluded from feature selection, hyperparameter search and model selection.

## 3. Weaknesses

**The decision curve analysis cannot be correct.** Net benefit is bounded above by event prevalence and is non-increasing in threshold probability for any fixed model. The manuscript reports net benefit rising from 0.119 at a 20% threshold to 0.178 at 50% for GeoSentinel-DCM, and rising for NYHA class (0.080 to 0.121), LGE presence (0.066 to 0.103) and LVEF (0.049 to 0.079). All four curves move in the wrong direction, and 0.178 exceeds the maximum attainable value in either cohort (0.168 external, 0.103 internal). This is a computational error in the net-benefit formula, most plausibly an inverted odds weighting term, and it invalidates the clinical utility claim in its entirety.

**The subgroup finding that carries the paper's novelty rests on approximately three events.** Table 1 reports 103 LGE-positive patients in the external cohort, leaving 46 LGE-negative. With LGE present in 88% of the 25 primary events, roughly three primary events fall in the LGE-negative subgroup. A C-index of 0.943 with a confidence interval of 0.847–1.000 is not estimable from three events, and the reported interval is far too narrow for that sample. The third principal conclusion of the Discussion, that the framework provides prognostic information in the absence of LGE, is therefore unsupported. Table 1 and Supplementary Table 2 also disagree: 88% of 25 plus 67% of 124 implies 105 LGE-positive patients, not 103. This must be reconciled.

**The internal performance of the conditioned-fusion model is anomalous against the authors' own table.** Every fusion configuration in Table 2 has an internal C-index at or below its constituent pillars (B1+B2, 0.686; B1+B2+B3, 0.694; B1+B2+B4, 0.706; uniform four-pillar, 0.710, against pillar values of 0.758–0.768), while externally the same fusions exceed every pillar. That inversion already suggests internal and external results were not produced by one procedure. Against that backdrop, moving from uniform to LGE-conditioned weighting of identical pillars raises the internal C-index by 0.171 to 0.881 and widens its CI to 0.160 when every other row sits near 0.095. The reported fusion weights, 35/30/20/15 and 80/10/5/5, are exact round percentages, which learned continuous weights do not produce, and no per-fold weight variability is shown. A Brier score of 0.0125 against a null-model value of approximately 0.092 at a 10.3% event rate, with no evaluation horizon stated, compounds the concern. The most economical explanation is that conditioning weights were fixed a priori or selected with visibility of held-out performance. Per-fold weights, the fold-level C-index vector, the Brier time point and the net-benefit computation must be released before any of this is assessable.

**The stated contribution is not tested against the right comparator, and the effect does not survive that comparison.** Every p-value in Table 2 is referenced to B1. The claim the paper actually makes is that LGE-conditioned fusion beats uniform fusion: an external difference of 0.012 (0.778 versus 0.766) and 0.008 over B1+B3+B4, on 25 events, with near-complete CI overlap and no paired bootstrap or DeLong-type test. Three configurations sharing an identical delta of +0.083 are assigned p-values of 0.025, 0.038 and 0.109, which requires explanation. External CI widths are near-constant across rows regardless of the point estimate, indicating a fixed-SE formula rather than resampling. Separately, the manuscript's own benchmark records Zhou et al. at an external C-index of 0.793 using LGE and ECV alone, above GeoSentinel-DCM's 0.778; the paper does not address that a far simpler published model outperforms it. Comparators are single variables (NYHA class, LGE presence, LVEF) rather than established scores such as MAGGIC or the Seattle Heart Failure Model, or continuous LGE burden and ECV. LGE also serves as both conditioning variable and comparator, which is circular.

**Power, framing and generalizability.** Forty-one primary events support 27 clinical covariates in B1, four pillars, two fusion weight vectors, a Random Survival Forest meta-learner and a performance-weighted five-model ensemble. Effective events per parameter is far below any defensible threshold, and Elastic-Net penalization does not repair this at the fusion or meta-learner stage. The term "digital twin" is not earned: there is no biophysical simulation, no parameter inference and no bidirectional updating, as the authors concede, and the "biomechanical" features are curvature and wall thickness, which are geometric. All 548 patients are from Chinese centres; no sex-stratified analysis is presented despite 24–28% female representation, and no age or comorbidity subgroup analysis is offered. The domain-adversarial head was trained only on internal centres and cannot be expected to neutralize the fifth-centre shift. The code availability statement asserts public release at github.com/FluxVisionAI/GeoSentinel-DCM; that repository was not locatable at the time of assessment, and data are unavailable.

## 4. Editorial Decision

**Reject.** The decision curve analysis is mathematically impossible, the LGE-negative result that constitutes the paper's distinctive claim is computed from roughly three events, and the internal performance of the conditioned-fusion model is inconsistent with the authors' own ablation in a pattern most simply explained by weight selection on held-out data. These are not revisable within a review cycle at this journal, because the incremental external gain over uniform fusion of 0.012 on 25 events would remain uninterpretable even if every arithmetic error were corrected. I recommend rejection without external review, with an invitation to resubmit elsewhere once the DCA is recomputed, per-fold fusion weights and fold-level C-indices are released, the LGE-negative analysis is either adequately powered or withdrawn, and the model is benchmarked against MAGGIC, the Seattle Heart Failure Model and continuous LGE or ECV. The reconstruction pipeline and the B4 kinematic result would make a solid methods-and-validation paper. Suitable transfer venues are **npj Cardiovascular Health**, **Communications Medicine** or **npj Digital Medicine**.

**Counterargument (steelman).** The strongest case against rejection is that the pipeline is real, the external cohort is genuinely independent, and the B4 external C-index of 0.754 against 0.673 for clinical variables is a defensible incremental finding that does not depend on any of the flawed analyses. On this reading the DCA error is an isolated formula bug in a supplementary analysis, and the LGE-negative claim could be struck in revision without touching the primary external result of 0.778; the correct action would then be major revision demanding per-fold weights and code, and desk rejection forecloses a contribution that needs only its overclaiming removed. I do not adopt this position, because the anomalous internal C-index is not an isolated bug and bears on whether the headline number is trustworthy at all. If the authors supply per-fold fusion weights and fold-level C-indices that reconcile the 0.710-to-0.881 jump, the rejection should be revisited.

**Confidential note to the handling editor.** Three items warrant integrity attention rather than ordinary methodological critique: net-benefit values that increase monotonically with threshold and exceed event prevalence; fusion weights reported as exact round percentages while described as learned; and a +0.171 internal C-index gain attributable solely to re-weighting identical pillars. Individually each is explicable as error. Together they justify requesting analysis code and fold-level outputs before any resubmission is considered.

## 5. Suggested Reviewer Expertise

Reviewers should cover geometric deep learning on cardiac surface meshes and point clouds, specifically GNN and mesh-autoencoder survival modelling on biventricular atlases with cross-subject vertex correspondence; cardiac digital twin construction and the distinction between statistical shape models and biophysically constrained twins; prognostic model methodology with direct competence in discrimination-difference testing, calibration metrics and decision curve analysis, since the DCA and CI construction are the decisive defects; CMR-based risk stratification in non-ischemic DCM including LGE burden, ECV and feature-tracking strain; and clinical electrophysiology and heart failure practice covering ICD decision-making and transplant referral. The intended split is roughly 70% technical and 30% clinical.

**Conflict note.** Alistair Young, Peter Swoboda, Tim Leiner, Angela Koh, Ru-San Tan, Shuang Leng and Liang Zhong are co-authors. Because the biventricular atlas pipeline descends from Young's line of work, the most obviously qualified mesh-modelling reviewers are concentrated in a conflicted network; the King's College London, Auckland, Leeds, National Heart Centre Singapore and Mayo Clinic groups should be excluded. All names below require standard conflict verification before invitation.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Three lines of work define the relevant landscape. The first is mesh- and motion-based survival modelling, which begins with Bello et al. (Nature Machine Intelligence, 2019, 4Dsurvival) and Dawes et al. (Radiology, 2017) and has since moved to explicit geometric deep learning. Beetz and colleagues have published point-cloud and mesh autoencoder pipelines on UK Biobank biventricular anatomies for outcome and phenotype prediction, and Biffi's explainable shape variational autoencoder work established the interpretability template that B2 and B3 are reproducing. GeoSentinel-DCM's B2 pillar is a two-layer GraphSAGE with a 64-dimensional pooled embedding, a conservative instantiation of this literature rather than an advance on it. The manuscript benchmarks against neither 4Dsurvival nor any mesh-autoencoder alternative, which is the comparison the field would expect. The second line is cardiac digital twins proper, where the past three years have been dominated by biophysically constrained electrophysiology and mechanics twins with inverse parameter inference, including DCM-specific pipelines calibrated to ECG and CMR. Measured against that standard, the present framework is a statistical shape-and-motion model with a survival head, and the terminology should be corrected.

The third line is prognosis in non-ischemic cardiomyopathy, where the 2024–2025 literature has converged on multimodal integration with modest and honestly reported gains. Kolk et al. (2024) combined ECG features, LGE-CMR and clinical variables in 289 NICM patients and reported externally validated AUROC of 0.84 for ventricular arrhythmia. A 2025 systematic review and meta-analysis of quantified LGE in NICM found a pooled hazard ratio of 3.31 for any LGE and roughly 12% added risk per additional 1% of LGE, independent of LVEF, establishing continuous LGE burden rather than the binary status used here as the current benchmark for phenotype conditioning. Recent work in ischemic disease has shown DeepSurv and Random Survival Forests outperforming Cox regression with scar entropy as a leading predictor, at cohort sizes and event counts comparable to this study. The authors' own comparison places Zhou et al. at an external C-index of 0.793 using LGE and ECV alone. The manuscript therefore enters a field in which its external discrimination sits at or below simpler published models, its conditioning variable is a coarser version of the accepted marker, and the directly competing work it must engage with is largely absent from the Discussion.

## 7. Suggested Reviewers

**Geometric deep learning on cardiac meshes.** Marcel Beetz (University of Oxford), mesh and point-cloud deep learning on UK Biobank biventricular anatomy for cardiac outcome prediction, the closest direct methodological counterpart to B2 and B3. Wenjia Bai (Imperial College London), large-scale cardiac image and shape deep learning. Marta Varela (Imperial College London), cardiac geometry and deep learning for phenotyping. Carlo Biffi, explainable shape variational autoencoders for cardiac disease.

**Cardiac digital twins and biophysical modelling.** Caroline Roney (Queen Mary University of London), patient-specific cardiac digital twins and model personalization. Julia Camps (University of Oxford), inverse inference for cardiac digital twins from ECG and imaging. Lei Li (University of Southampton), deep computational models for cardiac digital twin inverse inference in cardiomyopathy.

**Prognostic model methodology, calibration and decision curve analysis.** Ben Van Calster (KU Leuven), calibration hierarchy and net-benefit methodology, the single most relevant reviewer for the DCA and confidence interval defects. Laure Wynants (Maastricht University), prediction model validation and reporting standards. Maarten van Smeden (University Medical Center Utrecht), sample size and events-per-variable requirements for clinical prediction models.

**Clinical CMR and DCM prognosis.** Brian Halliday (Imperial College London and Royal Brompton Hospital), LGE-based risk stratification and therapy withdrawal in DCM. Upasana Tayal (Imperial College London and Royal Brompton Hospital), CMR phenotyping and outcomes in dilated cardiomyopathy including sex differences. Fleur Tjong (Amsterdam UMC), multimodal machine learning for arrhythmic risk in non-ischemic cardiomyopathy.

# Editorial Report — Manuscript 074791

**Title:** InteRA-BM: An Explainable Multimodal Clinical–Microbiome Framework for Rheumatoid Arthritis Prediction and Biomarker Prioritization
**Corresponding author:** C. Dharmashekar, JSS Academy of Higher Education and Research, Mysuru, India
**Handling editor:** Nature Communications, Digital Health

---

## 1. Overall Assessment

InteRA-BM integrates CLR-transformed 16S ASV abundances with clinical metadata via ExtraTrees–Boruta selection and a calibrated Random Forest, reporting ROC-AUC 0.906 ± 0.014 on the APRAC cohort (Li et al., Sci Data 2025) and 0.892 ± 0.052 on a second, "externally validated" cohort. It is not a substantial advance: the pipeline is standard, and the two claims that would make it interesting are each contradicted by the paper's own tables.

---

## 2. Strengths

Feature selection and calibration are correctly nested within each outer fold, avoiding the leakage common in this literature. Reported metrics reconcile exactly against the underlying confusion matrices in both cohorts. Reprocessing the second cohort from raw FASTQ through FastQC/DADA2/SILVA, rather than importing a processed table, is genuine additional rigor.

---

## 3. Weaknesses

The "external validation" (Section 3.6) is a second in-cohort nested cross-validation — feature selection, training, and calibration were all refit there, so the development model never scored independent data. Table 3 directly contradicts the text: the Age/BMI-ablated model (ROC-AUC 0.827) underperforms clinical-only (0.832) on every metric, yet lines 399–401 claim it outperformed both baselines. Age and BMI carry SHAP importance 10× any microbial feature, and the two cohorts' biomarker panels share only Age and *Streptococcus* — non-replication presented as success. The design (treated, prevalent RA vs. controls) cannot support the paper's early/seronegative-diagnosis framing, and no leave-one-site-out analysis is run despite six source hospitals. The validation cohort is never named or accessioned; there is no data/code availability statement; Table 2 mislabels negative CLR values as "mean abundance"; Table 4 disagrees with in-text figures in the third decimal; no statistical test appears anywhere.

---

## 4. Editorial Decision

**Reject.** The two headline claims — generalisability and microbiome-driven gain — are each falsified by the manuscript's own tables, not merely under-supported. This requires new experiments, not revision, and the underlying methodology is otherwise too standard to clear the novelty bar regardless. Recommend the authors rebuild validation as a locked-model single-pass evaluation with confidence intervals, add leave-one-site-out analysis, and resubmit to *Communications Medicine*, *npj Biofilms and Microbiomes*, or (if reframed around the pipeline) *BMC Bioinformatics*.

---

## 5. Suggested Reviewer Expertise

Technical expertise should cover compositional data analysis and CLR-based preprocessing of 16S ASV tables, including the consequences of CLR for feature-level interpretation; cross-cohort transfer and batch effects in amplicon microbiome classifiers, specifically leave-one-study-out benchmarking and taxonomic feature-space harmonisation between ASV- and genus-level representations; and prediction-model methodology, covering locked-model external validation, calibration assessment and TRIPOD+AI-compliant reporting, with the ability to adjudicate confounding by age, BMI and antibiotic exposure in case–control designs. Clinical expertise should cover rheumatology with a focus on early and seronegative RA diagnosis and the limits of RF/anti-CCP testing, and gut–joint axis biology with familiarity with DMARD effects on gut microbial composition.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The RA microbiome prediction field has consolidated around three lines of work that this manuscript does not engage. Wang, Yu and colleagues (Rheumatology, 2025, keae706) published a gut-microbiota-based diagnostic model for RA on a Chinese cohort, the closest direct competitor to the present study and uncited. Qi et al. (Autoimmunity Reviews 2025;24:103912) survey the field and note that microbiota-based ML models routinely exceed AUC 0.88 with recurring discriminatory taxa such as *Ruminococcus gnavus* and *Fusicatenibacter* — neither of which appears anywhere in InteRA-BM's panels, a discrepancy the authors should explain rather than ignore. Gupta, Sung and colleagues at Mayo (npj Digital Medicine 2021, and the Genome Medicine follow-on) established the multimodal template the present paper claims as novel, combining baseline microbiome with clinical and demographic covariates in a deep model for RA outcome. On the methodological side, Rojas-Velazquez et al. (BMC Bioinformatics 2024;25:26) already set out a reproducibility-oriented biomarker discovery methodology for microbiome ML; the manuscript cites it as reference 29 without acknowledging the overlap with its own claimed contribution. For cross-cohort generalisation specifically, the metagenomic meta-analysis literature established leave-one-study-out evaluation as the field standard several years ago, and its absence here is conspicuous.

Situated against this landscape, InteRA-BM replicates rather than advances. Its discrimination (0.906) sits inside the range already reported for microbiome-only RA classifiers, and its own microbiome-only arm (0.798) underperforms them. The taxa it prioritises — Faecalibacterium, Blautia, Bilophila, Klebsiella — are the standard RA case–control findings reported since Zhang et al. (Nat Med 2015) and Chen et al. (Genome Med 2016), both cited. The serostatus literature (systematic review, 2025) reports Collinsella and Blautia enrichment and Faecalibacterium depletion in seropositive RA, which partially conflicts with Table 2's direction for Faecalibacterium (higher in RA); this contradiction is unaddressed. The genuinely novel element on offer is the demonstration that an ASV-trained biomarker panel does not replicate in an independently processed genus-level cohort. Written honestly as a negative result about cross-pipeline transfer, that would be a more defensible and more useful paper than the one submitted.

---

## 7. Suggested Reviewers

For compositional microbiome machine learning and reproducible biomarker discovery: **Aldo López-Rincón** (Utrecht University; assistant professor) — first/corresponding on "Methodology for biomarker discovery with reproducibility in microbiome data using machine learning," BMC Bioinformatics 2024;25:26, the direct methodological comparator. **Laura Judith Marcos-Zambrano** (IMDEA Food Institute; senior researcher, non-professorial) — lead author of the ML-in-microbiome feature-selection and biomarker-identification review, Front Microbiol 2021;12:634511. **Marta B. Lopes** (NOVA University Lisbon; assistant researcher) — co-author on microbiome ML preprocessing best practice, Front Microbiol 2023;14:1250909.

For cross-cohort transfer and multimodal microbiome modelling: **Jaeyun Sung** (Mayo Clinic; assistant professor, Center for Individualized Medicine) — senior author on gut-microbiome prediction of clinical improvement in RA integrating microbiome with clinical and demographic features; the closest multimodal precedent. **Edoardo Pasolli** (University of Naples Federico II; associate professor) — leave-one-dataset-out benchmarking of microbiome classifiers across cohorts.

For clinical rheumatology and the gut–joint axis: **Sheng-Xiao Zhang** (Second Hospital of Shanxi Medical University; associate professor) — senior author, Autoimmun Rev 2025;24:103912 and the Rheumatology 2025 gut-microbiota RA diagnostic model. **Jose U. Scher** (NYU Grossman; associate professor) — new-onset and treatment-naive RA microbiome, directly relevant to the early-diagnosis framing. **Kristine A. Kuhn** (University of Colorado Anschutz; associate professor) — RA microbiome mechanism and the causality/temporality gap this manuscript elides.

Exclusions: any reviewer at JSS Academy of Higher Education and Research; the Li/Jin/Xu group at Peking University People's Hospital, who generated the APRAC development cohort and have a direct interest in downstream analyses of it. Editorial office should verify co-authorship conflicts and current affiliations before invitation.

---

## Confidential note to the handling editor — not for transmission to authors

No evidence of fabrication: the reported metrics reconcile arithmetically with the stated class splits and confusion matrices in both cohorts. The concerns are misrepresentation rather than falsification, and are as follows. Lines 399–401 assert a result that Table 3 contradicts, and the assertion is load-bearing for the paper's central claim. The procedure described in Section 3.6 is internal cross-validation but is labelled external validation throughout the abstract, results, discussion and conclusion. The validation cohort is unidentified and the citation at that point (reference 21) does not describe a cohort, so the claim is currently unverifiable; I recommend the authors be asked for the accession regardless of outcome. There is no data or code availability statement despite a "reusable framework" claim. Table 2's columns are mislabelled as abundances while reporting CLR values.

One scope question for triage: this is a microbiome informatics paper with no digital health component in the usual sense — no device, no deployment, no clinical workflow, no health data infrastructure. Even had the science held, routing to Digital Health is questionable and the submission would have been better assessed by a computational biology or immunology editor.

---

## Counterargument to the editorial recommendation

The strongest case against rejection is that the reject rests on a framing error rather than a scientific one. If "external validation" were relabelled "independent-cohort reproducibility of the pipeline," the experiment performed would be an honest and non-trivial one: the same code, applied to raw reads from a different population, sequencing run and bioinformatic pipeline, recovers comparable discrimination (0.892 vs 0.906). Pipeline-level reproducibility is a real and under-reported property in microbiome ML, where most published classifiers cannot be re-executed at all, and demonstrating it on reprocessed raw FASTQ is more than most authors attempt. The ablation misstatement is one sentence contradicting a table printed on the facing page, which is exactly the sort of error peer review exists to catch. The leave-one-site-out analysis and the Age/BMI-free clinical baseline are both single additional runs on data already in hand. On this reading, the paper is a poorly framed but salvageable methods report, and a rejection at desk forecloses a revision that could produce a defensible negative result about cross-pipeline biomarker transfer.

I do not find this persuasive, for two reasons. The revision it describes would invert the paper's conclusions rather than support them, which is a new study, not a revision. And it does not touch the novelty problem: a competently assembled pipeline of CLR, Boruta, Random Forest and SHAP, applied to another group's dataset, does not meet the Nature Communications bar even when correctly described. The counterargument does, however, strengthen the case for an encouraging rejection letter with a concrete experimental roadmap rather than a bare desk reject.
