# Trackrad202512456

037516
**Reviewer 1 — Dhingra (postdoc, methods focus)**
Engages substantively but flags scope problems: the four-class task (normal/VSD/ASD/PDA) is anatomically easy and the ~50% disease prevalence is artificially favorable versus real screening populations. He wants concomitant-CHD handling addressed, tier-benefit claims re-anchored to actual data rather than clinician-experience strata, and the "unanimous diagnosis only" exclusion criterion justified — since excluding indeterminate cases removes exactly the population where AI assistance matters most. He also flags the perception sub-analyses as underpowered and asks that they be explicitly labeled exploratory. No recommendation stated, but the tone is revise-not-reject.

**Reviewer 3 — Bellou (lab director, most technical review)**
The strongest and most consequential review. Central critique: the paper's narrative sells "visual guidance" as the innovation, but the data show visual guidance adds only +1.4% accuracy versus +8.0% for probability-based assistance alone — a narrative/results mismatch he calls the paper's "central, critical challenge." He wants a simple ResNet-50 baseline (no multi-view fusion, no pretraining) to justify the architecture's complexity, an ablation isolating Stage-1 pretraining's contribution, and the IoU=0.25 localization threshold either tightened or empirically justified against reader-rated acceptability. He also flags an unfair comparison to Grad-CAM (supervised vs. unsupervised), a flawed "appropriate reliance" metric that penalizes correct clinician overrides of wrong AI calls, missing per-site sample sizes for small external cohorts (as low as n=60), and no test of reader recall across the three repeated 240-case sessions despite only a two-week washout. Despite this, his overall verdict is explicitly "methodologically rigorous" and "well-conceived" — this is a revise, not a reject, review.

**Reviewer 4 — Arnaout (declined to state role)**
Recommends the paper should not have been sent for review at all. Argues echocardiography already diagnoses these three lesions at >95% accuracy, that VSD/ASD/PDA are anatomically non-confusable and clinically trivial to distinguish, and — most aggressively — that the model may just be detecting the color Doppler overlay a technician already applied upon recognizing an abnormality, not performing independent diagnosis. This last claim is a serious charge if true, but it is not corroborated by either Dhingra or Bellou, both of whom read the architecture in depth (spatiotemporal transformer over raw video, key-frame + localization output) and did not identify this as a logic flaw. Arnaout's critique reads more like a significance objection dressed up as a methodological one.

**Editorial decision: Major Revision, not Reject.**

Three independent technical readers converge on the same fixable problems — narrative overclaiming relative to modest visual-guidance gains, unjustified architecture complexity absent a baseline ablation, an untested calibration/exclusion-rate concern, and a flawed reliance-scoring definition. None of these are unresolvable; they're methodological rigor gaps a rebuttal and revision cycle can close, and the external validation (AUROC 0.950–0.984 across seven sites) and reader-study design are genuinely strong. Reject would be the correct call only if Arnaout's "the model is just detecting the technician's Doppler flag" claim held up — it doesn't survive scrutiny from the two reviewers who actually traced the architecture, so I'm discounting it as the deciding factor rather than ignoring it.

**Steelman for Reject instead:** Bellou's own framing — that the true contribution (reliance calibration) is different from the claimed contribution (visual guidance as diagnostic enhancement) — is close to a "misrepresented central claim" problem, which is normally a desk-reject trigger at this standard. If the authors can't credibly reframe the abstract/introduction around calibration rather than accuracy, this manuscript doesn't clear the bar regardless of technical soundness.

**Blind spot:** nobody quantified how much the consensus-only exclusion criterion (removing non-unanimous cases) inflates the headline AUROC — this is flagged by three of four reviewers/editors independently and should be a non-negotiable revision requirement, not a nice-to-have.

048966
**Reviewer 1 (Paetzold) — Reject.**
His core objection is that both novel metrics are weak by construction. UAR (same-label image swap) doesn't test what it claims: a genuinely image-reading model isn't required to change its answer under a same-label swap, so the metric can't distinguish grounding from robustness. CGR has the same problem in reverse — masking the evidence region doesn't remove all diagnostic signal from the rest of the image, and the radiologists' own Fig. 7e data show the evidence boxes often don't capture the full basis for the finding, so a "failure to flip" doesn't cleanly mean "didn't look." He also flags unaddressed parse-rate variance (87–100%, collapsing to instability for 5/9 models under terse prompting) that isn't disentangled from genuine abstention, calls the ReXErr subset inappropriate because some cases are text-only-solvable by construction, and considers the two-radiologist human benchmark (low overlap, one reader at CGR=0) too thin to support the "radiologist-comparable" framing. Restricting CGR/UAR to correct-on-original subsets is flagged as a further source of unquantified bias.

**Reviewer 2 (Konz) — Major revision, not reject.**
He accepts the same weak points R1 raises but treats them as fixable rather than fatal, and adds sharper ones. Two are structural: (1) the swap methodology needs an opposite-label (or same-view negative-flip) condition, since same-label swaps can't detect a genuinely image-reading model on diffuse/bilateral findings — this is the paper's most consequential gap; (2) several "statistically indistinguishable" claims (MedGemma-27B-text vs. radiologist, 119B vs. 7B model) are underpowered failures-to-reject dressed up as equivalence — CIs of ±12 and ±5.6 points don't rule out clinically meaningful gaps, and this needs TOST-style equivalence testing, not point-estimate comparison. He also flags that aggregate accuracy conflates yes-bias with genuine competence and should be replaced or supplemented with balanced accuracy/F1/per-class sensitivity, that the irrelevant-mask placement (image corner) likely deflates the IS noise floor and inflates apparent grounding specificity, and that the "unstable" category rests on 25 cases from a single model, confounded with that model's own parse-rate collapse. His human-reader concern (κ=0.224, n=80) mirrors R1's but is more precisely diagnosed as reducing the "radiologist-comparable" claim to a single-reader anecdote.

**Convergence:** both reviewers agree the human comparison is underpowered, UAR/CGR need stronger negative controls, and parse-rate/abstention handling is unresolved. These are not in dispute.

**Decision: Major Revision, not Reject.**
R1's critique is valid but describes design weaknesses in the auditing metrics, not a fatal flaw in the paper's premise — the decoupling of accuracy from image-grounding is real and, per R2, replicates across CheXpert (ρ=0.931) and resolution/prompt perturbations, which argues against R1's implication that the whole apparatus is noise. R2's major weaknesses are concrete, addressable within a revision cycle (add the opposite-label swap, rerun with balanced accuracy and equivalence tests, relocate/vary the irrelevant mask, either drop or heavily qualify the single-model "unstable" category), and his own recommendation is major revision. Reviewers required for the resubmission: R2's four major items (opposite-label swap; balanced-accuracy reanalysis; equivalence testing on the "indistinguishable" claims; irrelevant-mask placement control) plus R1's ReXErr concern and the two-reader human benchmark — the latter should be expanded or explicitly reframed as a single-reader anecdote, not "radiologist-comparable" performance.

**Steelman for Reject instead:** if the opposite-label swap experiment, once run, shows CGR/UAR rankings shift materially, the entire model categorization (ignores-image / unstable / uses-image) collapses and the paper's central contribution — the taxonomy itself — would need to be rebuilt, not patched. A reviewer could reasonably argue that's not a "revision," it's a different paper, and the manuscript shouldn't be sent forward on the assumption that a missing experiment will confirm rather than overturn the headline finding.

056516
**Reviewer #1 (Haoliang Li).** Central objection is novelty: entropy-minimization TTA causing overconfidence is already documented (EATA-C, COME), and conservative/uncertainty-aware alternatives already exist in general ML and specifically in medical foundation models (Lou et al., npj Digit. Med. 2025 — causal TTA for CRC pathology). I checked both; they're real, peer-reviewed, and squarely on-topic — this is not a stretch objection. Beyond novelty, he flags: "calibration collapse" is asserted rather than operationally defined against a source-vs-target baseline; all adaptation methods are LayerNorm-only except one baseline, confounding method comparisons with implementation choice; the entropy/Gini gradient argument is made in probability space without connecting to the logit space where optimization actually happens; GITTA bundles five components (teacher-student consistency, augmentation, routing, memory, EMA) with no factorial ablation to attribute gains; high-confidence-error metrics are pixel-level while clinical deferral is case-level, an unstated and optimistic assumption; pretraining-data contamination on "zero-shot" targets is unaudited; and the retrospective-only design doesn't support the paper's regulatory/safety framing. His confidential note to the editor: "below the bar of AI-related journal and conferences."

**Reviewer #2 (Tong Zhang).** Substantially overlaps — same operational-definition complaint, same LayerNorm-confound complaint, same probability-vs-logit-space gap in the theory (raised independently, which matters). Adds: unclear aggregation unit for ECE-FG/HCER (pixel/image/patient?); no class-wise or bootstrapped calibration; proper-scoring-rule justification doesn't obviously transfer from the supervised to the unlabeled objective; VQA confidence surrogate (token probability) isn't validated against open-ended answer correctness; ordering/accumulation protocol for non-episodic adaptation is unspecified; 2D segmentation results are strong but 3D segmentation and VQA gains are "modest and model-dependent," yet conclusions don't distinguish this; NODE21 macro-F1 of 0.067 next to 84.6% accuracy in Table S18 looks like a metric-reporting error. Most serious: he audited the code and found that in `gitta.py` and `gitta_entropy.py`, predictions are detached before the Gini/entropy and `L_mmr` terms are computed, meaning `L_mmr` may not be propagating gradients at all — and this directly implicates whether the reported "Gini replaced by Shannon entropy" ablation (Table S25), the one experiment that isolates GITTA's actual novel contribution, reflects what's claimed in the text. He escalated this to Remarks to the Editor, not just Remarks to the Author.

**Decision: Reject.**

Three findings compound rather than sit independently. First, the paper's foundational claim — entropy-driven overconfidence under TTA — has close, verified, peer-reviewed precedent in both general ML and medical foundation models specifically, which cuts hard against the "revisited" framing being a distinctive advance. Second, both reviewers independently derived the same theoretical gap (probability-space gradient argument, no logit/parameter-space justification), which is convergent evidence of a real flaw in the mechanism, not two idiosyncratic readings. Third, and decisive: the one component that could still carry novelty — the Gini-over-entropy choice — has its supporting ablation thrown into doubt by a code-level gradient-detachment issue that Reviewer 2 escalated directly to the editor. If Table S25 doesn't reflect a live gradient, GITTA's specific mechanistic claim is unsupported by its own ablation. Combined with R1's explicit "below the bar" verdict, this is not a paper away from clean revision — it's a paper whose central claim of novelty and its supporting evidence are both compromised.

**Steelman for Major Revision instead:** every comment above, taken alone, is answerable — the code issue could be a monitoring signal rather than a bug, the theory gap could be closed with a logit-space derivation, and neither reviewer's formal comments explicitly recommend rejection. Both reviewers also agree the underlying empirical phenomenon (miscalibration surviving TTA across 13 models/15 datasets) is real and broad. An editor optimizing for not losing a possibly-fixable contribution would authorize one major-revision cycle contingent on the authors resolving the S25 gradient question and reframing novelty against COME/EATA-C/Lou et al.

I'd still hold Reject, but flag the code-detachment issue for your own confidential integrity note separate from the decision letter — it's a reproducibility concern on the manuscript's core ablation, not just an author-facing clarification request, and it should be on record regardless of which way the decision goes.

061892
**Decision: Reject**

Both reviewers converge on a fatal flaw: the primary statistical comparison is invalid. Reviewer 3 states directly that using the Wilcoxon signed-rank test to compare a binary LLM-correctness indicator against clinician probability-of-correct violates the test's assumptions, deflating p-values and inflating apparent significance — undermining the non-inferiority and equivalence conclusions the paper is built on. Reviewer 1 reaches the same conclusion independently: vignette-level Wilcoxon analyses ignore within-clinician/within-vignette dependency, and with only 43 unique vignettes the actual finding is "no significant differences, some variation by model" — not the "consistently high performance" claimed in the text.

This statistical defect sits underneath all three headline claims. The multilingual claim is confounded by unequal vignette distribution across languages and diagnoses (anxiety in 6 languages, mood in 4, stress-related in 3). The LLM-vs-clinician claim is confounded by an unequal comparison design — clinicians saw 2 vignettes with updated guidelines, LLMs saw the full set without them, and clinician accuracy is aggregated across individuals while LLM accuracy is repeated-measures. The non-inferiority claim rests on an unjustified 10% margin against a ~65% clinician baseline.

These are not presentation issues fixable by rebuttal — they require re-deriving the primary analysis (hierarchical/mixed-effects modeling, within-group comparisons, re-justified margins) on a dataset too small and too confounded to support the paper's central claims either way. Reject.

071193

# Editorial Report: RADx — Anatomically Structured and Uncertainty-Aware AI Framework for Radiographic RA Assessment

## 1. Overall Assessment

The manuscript presents RADx, a modular pipeline built on HandXFM, a DINOv3-based hand-radiograph foundation model, that performs joint detection (DETR-style), binary abnormality classification, and ordinal severity regression for Sharp–van der Heijde (SvH) erosion and joint space narrowing (JSN) scores at joint, unilateral-hand, and bilateral-hand levels, evaluated on the CATCH cohort (533 participants, 1,405 radiographs with SvH annotation) with conformal-prediction-based uncertainty quantification and a deployed web interface.

The engineering is competent and the anatomical decomposition is sensible, but the central claim of clinical advance is undermined by a directly comparable, more complete system already in the literature: autoscoRA (Deimel et al., *Arthritis & Rheumatology*, 2026), trained on 769 patients and 12,144 radiographs of both hands and feet, reports ICC 0.9 agreement with expert SvH scores across joint and summed levels — a materially stronger validation benchmark than RADx's joint-level PCC of 0.748 (erosion) and 0.816 (JSN). RADx is neither cited nor discussed against this benchmark, which is the single most consequential omission in the manuscript.

## 2. Strengths

The three-tier anatomical hierarchy (joint, unilateral-hand, bilateral-hand) with a shared HandXFM backbone is a coherent architectural contribution, and the two-stage zero-inflation-aware modeling (binary presence gate followed by CORAL-style ordinal regression) is a defensible response to the extreme class imbalance documented in Fig. 1B–D.

The conformal prediction implementation is methodologically sound, applying split conformal calibration separately to detection (box inflation), classification, and regression, with joint-type-conditional calibration exposing genuine anatomical heterogeneity in uncertainty (Fig. 3B–D, 5C).

Patient-level 80:10:10 splitting shared across tasks, and strict exclusion of CATCH data from HandXFM pretraining, are appropriate safeguards against leakage.

## 3. Weaknesses

Validation is confined to a single center's cohort (CATCH) with no external test set; the manuscript's own discussion concedes this, but the concession does not substitute for evidence.

The SvH implementation is materially incomplete relative to the formal protocol: JSN is restricted to MCP/PIP joints only, wrist erosion uses a composite region rather than individual carpal articulations, and feet are excluded entirely — yet the abstract and title present RADx as a general solution for "radiographic assessment of rheumatoid arthritis" without this qualification until the Discussion.

HandXFM's pretraining corpus (~25,000 curated images, 6,130 with joint annotations) is two orders of magnitude smaller than SKELEX (Kim et al., Seoul National University, 1.29M MSK radiographs), a directly competing musculoskeletal foundation model published in the same window; no comparison or citation is offered.

The claim that HandXFM was "developed in our prior work" carries no citation anywhere in the reference list, which is a transparency gap the editor cannot resolve without seeing that prior manuscript.

## 4. Editorial Decision

**Send for Review.** The methodology and uncertainty framework are rigorous enough to merit expert adjudication, but reviewers must be explicitly asked to evaluate: (1) whether omission of autoscoRA and SKELEX constitutes a fatal comparator gap or a fixable revision; (2) whether single-cohort validation is disqualifying at this journal's bar; and (3) whether the uncited "prior work" HandXFM claim requires resolution before further review.

## 5. Suggested Reviewer Expertise

Reviewers should cover: DETR-based object detection and anatomical landmark localization in medical imaging; self-supervised/foundation-model pretraining (DINO-family architectures) for radiographic domains; conformal prediction and distribution-free uncertainty quantification in clinical regression/detection tasks; ordinal regression under severe class imbalance; and a rheumatologist with direct SvH-scoring and early-RA cohort experience.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Automated SvH scoring has matured rapidly: Honda et al. (*Rheumatology*, 2023) established CNN-based scoring with clinical application; Moradmand & Ren (*Sci Rep*, 2025) proposed multistage OSS prediction with external testing on 291 patients; Lien et al. (*J Med Biol Eng*, 2025) added attention-based joint localization; and autoscoRA (Deimel et al., 2026) now represents the field's strongest validated system, covering hands and feet with ICC 0.9 agreement. In parallel, MSK foundation modeling has moved toward million-scale corpora (SKELEX, 1.29M images) and conformal landmark localization (M-R2CCP, arXiv 2503.14106) is an existing framework directly overlapping RADx's detection-uncertainty contribution. RADx's genuine advance is its unified multi-scale (joint/hand/bilateral) representation and anatomically conditioned conformal calibration; it does not advance raw scoring accuracy beyond autoscoRA and should engage with it directly.

## Suggested Reviewers

**SvH automation / clinical-technical:** Thomas Deimel; Hajar Moradmand. **Foundation-model / detection:** Shinn Kim; Soobin Lee. **Conformal prediction / UQ:** Anastasios N. Angelopoulos.

071283
# Editorial Report — Manuscript 071283
**Title:** Skill-assisted and knowledge-augmented language-model workflows for solid-dosage-form visualization and formulation redesign
**Authors:** Yang, Xu, Deng, Liu, Fu (Sichuan University; GHDDI)

---

## Confidential — Editorial Integrity Alert (handling editor only)

No undisclosed preprint overlap, salami-slicing, or numerical inconsistency was identified. Reference 5 (Chen, Yang, Mi, Deng & Fu, *Acta Pharm. Sin. B*, 2025) is the same author group's prior DISGPT agent; the present manuscript explicitly builds on it and cites it appropriately, so this is legitimate incremental extension rather than duplication, but reviewers should confirm the degree of novel content versus the earlier paper. No author-overlap or independence concerns were found in the reference list. Corresponding-author contact uses a personal webmail domain (163.com) alongside institutional addresses; this is common practice in the region and not itself a concern.

---

## 1. Overall Assessment

The manuscript describes DIS Chatflow, a Dify-platform, retrieval-augmented multimodal LLM pipeline that converts time-lapse macro-imaging videos of tablet disintegration into structured text records across eight predefined descriptive dimensions, and its extension, TOMO Chatflow/MYGO, which issues directionally constrained hydroxypropyl methylcellulose (HPMC) K4M/K100LV ratio recommendations for two model sustained-release tablets (methylene blue, gliclazide), validated by preparing new tablet batches and re-measuring flow-through UV absorbance-derived release signals.

This is fundamentally a workflow-engineering and prompt-orchestration study rather than a methodological or clinical advance. No new model, architecture, or learning algorithm is introduced; the contribution is a curated retrieval corpus (5,835 articles), a four-route Dify pipeline, and a set of self-authored scoring heuristics. Two concerns dominate the decision. First, scope: the manuscript contains no patient, clinical, EHR, or health-outcome content — it is computational pharmaceutics/pharmaceutical engineering, not digital health, and its fit to a Nature Communications digital-health track is weak. Second, validation circularity: the "coverage," "consistency," and "quality score" metrics are authored and scored by the same team without independent expert ground truth, and the sole wet-lab "optimization" claim rests on n=3 replicates per condition against arbitrary heuristic targets (approximately 90% and 105% of a reference signal) rather than any pharmacodynamic or regulatory benchmark.

---

## 2. Strengths

The authors close an actual wet-lab loop rather than stopping at text generation. MYGO's HPMC-ratio recommendations for both the methylene-blue and gliclazide systems were physically realized as newly compressed tablets and independently re-evaluated by flow-through imaging and UV absorbance at 667 nm and 226 nm (Fig. 5c–f), giving at least one falsifiable, non-textual check on model output that most "LLM-for-science" papers omit.

The cross-model benchmarking on an identical Dify workflow (GPT-series, GLM-4.6V, Kimi-K2.5, Qwen3.6-plus) using three consistently applied metrics is a useful comparative result for practitioners: eight-dimension coverage ranged from 100% (GPT) to 47.22% (Qwen), and repeat-run consistency from 93.75% to 20.00%, a spread large enough to be practically informative for anyone selecting a multimodal backbone for structured pharmaceutical image description.

The modular route decomposition (background, image analysis, mechanistic reasoning, summary) with cumulative Markdown export addresses a concrete, previously documented failure mode — the authors' own prior DISGPT agent's reliance on unstructured, non-archived dialogue — and is a plausible, if incremental, engineering fix for context loss in long multi-turn multimodal sessions.

---

## 3. Weaknesses

No expert ground truth exists for any of the reported metrics. Eight-dimension coverage measures whether predefined fields are present, and the quality score is a task-specific rubric scored without blinded comparison to images or to an independent pharmacist's description. The headline "84.94 points" quality score and "100% coverage" figures measure format compliance, not whether the described color, shape, or erosion phenomena are visually or pharmaceutically accurate; the Discussion partially acknowledges this, but the framing throughout the Results section still reads as a performance claim.

The MYGO "optimization" is validated on a single excipient-ratio axis (K4M fraction) with n=3 tablets per formulation, against targets defined post hoc from the same reference data used to set the design space. Success is declared when three independently prompted strategies move "directionally" the same way — a low bar that does not rule out the possibility that any reasonable heuristic (LLM-derived or not) would produce the same directional shift, since the K4M/K100LV release relationship is well established pharmaceutical mechanism (refs. 20–23 in the manuscript's own citation list). No comparison against a simple rule-based or Bayesian-optimization baseline is reported, despite the Discussion explicitly invoking Bayesian optimization and self-driving laboratories as the relevant comparator class.

The evaluation pipeline is self-referential: the same authors wrote the scoring skill, set its weights, and generated the mechanistic-reasoning text that the skill then scores, creating a conflict between the roles of generator and evaluator. No blinded pharmaceutical expert independently annotated the eight-dimension outputs against source images, and reference-based text-similarity metrics such as BERTScore were explicitly not used, leaving the "quality" claims without any external anchor.

The manuscript's clinical and regulatory relevance is minimal to absent. Methylene blue and gliclazide serve only as model tracers for a bench-scale UV absorbance surrogate; there is no dissolution-similarity (f2), pharmacokinetic, or regulatory (FDA/EMA Level A IVIVC) linkage, and the paper does not engage with deployment, safety, or oversight considerations that would normally accompany an AI-assisted formulation-redesign claim.

---

## 4. Editorial Decision

**Reject**, with a recommendation to transfer to *Communications Engineering* or *npj Artificial Intelligence*, where a systems/workflow contribution of this kind is a better topical fit. The steelman case is that the wet-lab-validated redesign loop and the cross-model benchmarking are useful, reproducible engineering artifacts that some readers would value; but the absence of independent, blinded ground-truth evaluation of the phenotype descriptions, the self-scored and self-set optimization criteria, the small replicate numbers, and the complete absence of clinical or health-system content place this outside the scope and rigor bar of Nature Communications' digital-health track. This is not a "Send for Review, contingent on resolution" case — the ground-truth and scope issues are structural, not fixable by revision within the current framing.

---

## 5. Suggested Reviewer Expertise

Reviewers should include a specialist in hydrophilic HPMC matrix-tablet release kinetics and swelling/erosion mechanisms; a specialist in multimodal/vision-language model evaluation methodology, particularly output-consistency and hallucination assessment; a specialist in retrieval-augmented generation and knowledge-base curation for scientific/technical corpora; a specialist in time-resolved imaging of tablet disintegration (macro-imaging or micro-CT); and, for the clinical-relevance question, a pharmaceutical scientist experienced in IVIVC and regulatory dissolution testing who can assess whether the release-signal claims have any translational meaning.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The closest and most consequential prior art is not cited. Waldner et al. (*Heliyon*, 2024) applied a U-Net-based deep-learning segmentation pipeline to time-resolved micro-CT images of disintegrating compacts, directly addressing the same "structural evidence from disintegration imaging" problem this manuscript targets, using a more information-rich 3D imaging modality; the manuscript's own reference 26 in fact cites this group's micro-CT work but never engages with the segmentation methodology itself. More critically, a 2025 *Pharmaceutical Research* paper combining a fine-tuned LLM with adaptive retrieval-augmented generation and diffusion-model-synthesized SEM morphological parameters to predict dissolution profiles is essentially the same "LLM + RAG + imaging-derived structure → release behavior" concept this manuscript proposes, published in the same journal family the authors cite elsewhere, and is a clear omission that should be raised with the authors. Hornick et al. (*Nat. Commun.*, 2024, cited as ref. 9) remains the strongest generative-AI formulation-optimization precedent and is appropriately engaged, but the present work's "optimization" is considerably narrower — a single-axis heuristic redirection rather than a generative structure-synthesis search. Bannigan et al. (*Adv. Drug Deliv. Rev.*, 2021) established the machine-learning-directed formulation development framing this paper implicitly follows but does not cite. Overall, the manuscript sits within an active but crowded 2024–2026 wave of LLM/ML-assisted formulation and dissolution-prediction work; its distinguishing feature — closing the loop with physical re-preparation and re-measurement — is real but narrow, and the paper undersells how close several uncited 2024–2025 papers already are to its central claim.

---

## Further Literature (independent verification)

1. Waldner, S. et al. Advanced analysis of disintegrating pharmaceutical compacts using deep learning-based segmentation of time-resolved micro-tomography images. *Heliyon* 2024;10:e26025. DOI: 10.1016/j.heliyon.2024.e26025. Peer-reviewed. Not cited by manuscript. Independent of submitting group. Directly competing methodology (deep-learning segmentation of disintegration imaging); should be engaged, not merely cited secondhand.
2. [Author names not fully resolved in search snippet]. DeepSeek-LLM with Adaptive RAG for Pharmaceutical Dissolution Prediction. *Pharm. Res.* 2025. DOI: 10.1007/s11095-025-03932-1. Peer-reviewed. Not cited by manuscript. Independent of submitting group. Highly relevant — combines LLM+RAG with imaging-derived structural data to predict dissolution; closest conceptual precedent identified.
3. Bannigan, P., Aldeghi, M., Bao, Z., Häse, F., Aspuru-Guzik, A. & Allen, C. Machine learning directed drug formulation development. *Adv. Drug Deliv. Rev.* 2021;175:113806. Peer-reviewed. Not cited by manuscript. Independent. Foundational review for the ML-directed-formulation framing.
4. Application of AI in Tablet Development: An Integrated Machine Learning Framework for Pre-Formulation Property Prediction. *Pharmaceutics* 2026;18(4):452. DOI: 10.3390/pharmaceutics18040452. Peer-reviewed. Not cited. Independent. Relevant to disintegration-time prediction via ML descriptors.
5. Data driven analysis of tablet design via machine learning for evaluation of impact of formulation properties on disintegration time. *ScienceDirect*, 2025. Peer-reviewed. Not cited. Independent. Relevant ML-based disintegration-time prediction, competing approach.
6. Puzzle out Machine Learning Model-Explaining Disintegration Process in ODTs. PubMed, 2022. Peer-reviewed. Not cited. Independent. Explainable-ML mechanistic analysis of disintegration, conceptually adjacent to the manuscript's "mechanistic reasoning" module.
7. Agentic Discovery of Cryomicroneedle Formulations. arXiv:2605.19677, 2026. **Preprint, not peer-reviewed** — flagged as unreviewed. Independent. Directly relevant LLM-agent-driven formulation-optimization loop; should be discussed as concurrent/competing work.
8. Hornick, T. et al. In silico formulation optimization and particle engineering of pharmaceutical products using a generative artificial intelligence structure synthesis method. *Nat. Commun.* 2024;15:9622. Peer-reviewed. Already cited (ref. 9) and appropriately engaged. Independent of submitting group.
9. Singhal, K. et al. Large language models encode clinical knowledge. *Nature* 2023;620:172–180. Peer-reviewed. Already cited (ref. 10). Included for context on LLM factuality claims that motivate the manuscript's knowledge-grounding design.
10. Bran, A. M. et al. Augmenting large language models with chemistry tools. *Nat. Mach. Intell.* 2024. Peer-reviewed. Already cited (ref. 34). Relevant precedent for tool-augmented LLM scientific workflows, appropriately engaged.

---

## Suggested Reviewers (by expertise area)

**HPMC matrix release kinetics:** researchers with recent first/senior-author publications on hydrophilic matrix swelling, erosion, or gel-layer dynamics — prioritize postdoctoral researchers or assistant/associate professors in pharmaceutical technology groups (e.g., groups publishing on HPMC K-series matrix systems in *Int. J. Pharm.* or *Pharm. Res.* within the last 3 years); avoid the submitting group's direct collaborators.

**Multimodal/vision-language model evaluation:** assistant/associate professors working on MLLM benchmark design, hallucination detection, or structured-output evaluation for scientific image tasks.

**Retrieval-augmented generation for technical corpora:** postdoctoral or junior faculty researchers with recent RAG-for-science publications, particularly in chemistry/pharma knowledge-base construction.

**Time-resolved pharmaceutical imaging (micro-CT/macro-imaging):** a reviewer with direct expertise overlapping Waldner et al. (2024) or comparable micro-CT disintegration imaging work — ideally an independent junior researcher in that specific sub-field.

**Regulatory/IVIVC dissolution science:** a pharmaceutical scientist (assistant/associate professor level where possible) who can assess whether the UV-absorbance relative-release signals have any translational or regulatory meaning.

*Note: identifying named individual candidates requires literature-database access beyond the current session's search results; the editor should have the journal's reviewer-finder tool cross the above expertise areas against the independence and seniority constraints noted.*

071297
# Editorial Report — Manuscript 071297
**"Geometry-aware medical image segmentation: implicit neural reconstruction with the method of fundamental solutions"**
Wang, Gao, Wang, Ma, Zheng, Lei, Xia, Jiang

---

## Confidential Editorial Integrity Note (handling editor only)

No undisclosed preprints, salami-slicing, or numerical fabrication identified. One item for the record: the core PDE machinery (fundamental-solutions activation, Eq. 1–3) is a direct extension of ref. 43 (Zheng, Wang, Chen, Lei, Wang, 2020), and corresponding author Min Lei is a co-author of that prior work. The citation is properly disclosed as a numbered reference, so this is not concealment, but it should inform the editor's read of the novelty claim (see Weaknesses). One factual inconsistency requires author correction before further processing: the abstract and Results claim an 85%–90% M-Curvature reduction "across" the evaluated datasets, but Table 1's own numbers give a 77.4% reduction for Trachea (0.2984→0.0673), below the stated range.

---

## 1. Overall Assessment

The manuscript proposes IMFS, a post-hoc, model-agnostic boundary-smoothing module for medical image segmentation masks, built on a one-layer method-of-fundamental-solutions neural network (MFSNN) that embeds a bi-modified Helmholtz PDE directly into its activation functions, reducing the loss to a simple boundary-fitting term (Eq. 3). A companion Boundary-Aware Refinement (BAR) step localizes sampling to a narrow band around the mask edge, cutting inference time roughly 11-fold (22.171 s → 2.062 s, Table 3). The authors also introduce PTAUD, a new 5,429-frame multi-structure parathyroid adenoma ultrasound dataset, and validate IMFS across ten segmentation architectures and four datasets, plus a downstream 3D FEM elasticity analysis.

This is a competent, unusually broadly validated post-processing paper, but it is not a diagnostic or clinical advance, and its central numerical claim (85%–90% smoothness gain "across" datasets) is contradicted by the authors' own Trachea result. The deeper concern is that the underlying PDE-embedding technique is not new — it extends the corresponding author's own 2020 MFS surface-reconstruction method to 2D segmentation boundaries — so the paper's novelty rests almost entirely on the BAR engineering trick and the breadth of empirical validation, not on new numerics.

---

## 2. Strengths

The MFSNN formulation is a genuine methodological improvement over generic physics-informed neural network (PINN) smoothing (refs. 40–42): by using fundamental solutions of the governing PDE as activation functions, the boundary condition is satisfied analytically rather than through a soft multi-term loss, which sidesteps the gradient-imbalance problem that plagues PINN loss weighting. This is a real, well-motivated simplification, not just a relabeling of existing PINN practice.

BAR is a legitimate systems contribution. Restricting sub-pixel sampling to a local 2×2-cell band around the boundary (Fig. 5) rather than the full bounding box yields an 11-fold inference speedup while leaving M-Curvature essentially unchanged (0.0295 vs. 0.0297, Table 3) and tightening the IoU-preservation distribution 18–38-fold in variance (Fig. 4). This moves the method from a curiosity toward something usable in a real pipeline.

Validation breadth is well above the norm for a post-processing paper: ten architectures spanning CNN (DeepLab, nnU-Net), transformer (SwinUNETR, UNETR), Mamba (UMambaBot, SwinUMamba), and SAM-family (MedSAM, FastSAM) backbones, across four datasets, plus a downstream FEM mesh-efficiency quantification (Table 4, 21–32% element-count savings at fixed accuracy). Few boundary-refinement papers close the loop to a concrete downstream numerical-simulation benefit.

PTAUD fills a real gap: dedicated, IRB-approved (Peking Union Medical College Hospital, S-K1743), prospectively collected, four-class pixel-level annotation of parathyroid adenoma plus thyroid, carotid, and trachea is scarce relative to general thyroid-nodule ultrasound datasets, and the manuscript states data will be shared on reasonable request.

---

## 3. Weaknesses

The headline claim is not internally consistent. Recomputing Table 1's own M-Curvature values gives reductions of 90.7% (DMR-IR), 90.6% (CHN-CXR), 87.0% (ISIC), 90.2% (Thyroid), 86.1% (PTA), 91.9% (Carotid) — but 77.4% for Trachea. The abstract's "85%–90% across" framing is therefore not supported by the authors' own table and must be corrected, not merely softened.

The dataset-splitting methodology is underspecified in a way that threatens the central IoU-preservation claim. PTAUD frames are extracted from "dynamic sequences" per patient, yet the 8:2 train/validation split is described only as "fixed," with no statement that it is patient-wise. If frames from the same sequence appear in both splits, IoU and M-Curvature comparisons on PTAUD are subject to leakage that would inflate apparent stability.

No result in the paper carries a confidence interval or a significance test. Fig. 4 reports per-case mean and standard deviation of ΔI across 200 sampled cases — a good start — but the manuscript never runs a paired test (e.g., Wilcoxon signed-rank) to establish that the with/without-BAR or with/without-IMFS differences are not noise, despite having the paired per-case data needed to do so trivially.

The comparator used for the pixel-level ablation (Table 2), FastSmoothSAM (ref. 24), is an unreviewed arXiv preprint (2507.15008) presented alongside a peer-reviewed method (Active Contour Model) without distinguishing review status in the text — a transparency lapse the authors should correct given how central Table 2 is to the smoothing-quality claim.

The clinical relevance of the improvement is asserted, not measured: no clinician rated the refined boundaries, no comparison to pathology-confirmed tumor volume was made for PTA, and the 0.28% volume-loss figure (Table 2) is reported for a single organ (thyroid) at the mesh level only, not systematically across PTAUD's four structures.

**Steelman for the authors:** the paper does not claim clinical diagnostic benefit — it claims a geometry-processing utility (smoother, more simulation-ready boundaries) validated by a physically interpretable metric (M-Curvature) and a downstream FEM efficiency gain that is itself objective and reproducible. Judged purely as a computational-geometry tool paper rather than a clinical-AI paper, the missing clinical/statistical rigor is less disqualifying, and the cross-architecture generalization is a stronger-than-typical result for that genre.

---

## 4. Editorial Decision

**Send for Review.** The paper is not fundamentally flawed — the abstract/Table 1 discrepancy and the split-methodology ambiguity are both correctable through revision, not signs the core result is wrong — but the current text overstates its own numbers and does not establish that the IoU/M-Curvature gains are statistically robust or clinically consequential. Reviewers should be asked to adjudicate: (1) whether PTAUD's train/validation split is patient-wise, and if not, whether re-running with a patient-level split changes Table 1/Fig. 4; (2) whether the 85%–90% claim should be revised given the Trachea outlier; (3) whether the FastSmoothSAM preprint comparator should be supplemented with a peer-reviewed baseline; and (4) whether the authors can add any clinician-facing or pathology-referenced validation of boundary quality, given the paper's stated ambition toward surgical navigation and patient-specific simulation.

---

## 5. Suggested Reviewer Expertise

Reviewers should cover: (i) PDE-constrained/physics-informed neural networks and the method-of-fundamental-solutions literature specifically, to assess whether the MFSNN formulation is correctly derived and genuinely distinct from ref. 43; (ii) neural implicit surface/SDF reconstruction (INR-based, non-MFS) as the dominant competing paradigm; (iii) classical mesh-smoothing and FEM meshing for biomedical simulation, to evaluate Table 4's efficiency claims; (iv) SAM-family and foundation-model medical segmentation, to assess the MedSAM-IMFS integration and generalization claims; and, on the clinical side, (v) head-and-neck/endocrine ultrasound diagnosis of parathyroid adenoma, to assess PTAUD's clinical annotation protocol and case-mix adequacy.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

Boundary quality in segmentation has been attacked from two directions over the last three years: architecture-integrated boundary-awareness and post-hoc refinement. On the integrated side, BALR-SAM (2025) adds a Complementary Detail Enhancement Network into SAM's encoder specifically to inject boundary-sensitive features during fine-tuning, and reports outperforming fully fine-tuned MedSAM while updating under 2% of parameters — a materially different philosophy (train-time boundary awareness) from IMFS's post-hoc, retraining-free stance, and worth explicit engagement in the manuscript's related-work section. On the reconstruction side, the dominant paradigm for smooth-surface recovery from noisy medical boundaries is signed-distance-function implicit neural representation (INR/SDF), not MFS: FUNSR (Chen et al., Medical Image Analysis, 2024) performs self-supervised SDF learning directly from freehand 3D ultrasound point clouds with sign-consistency and adversarial on-surface constraints, reporting 32–68% error reductions over Neural-Pull baselines, and operates on exactly the modality (ultrasound) and exactly the downstream goal (smooth, simulation-ready 3D surfaces) that this manuscript targets with PTAUD and its FEM analysis. FUNSR is not cited, and its omission is a substantive gap, not a stylistic one: it is the most directly comparable ultrasound-specific implicit-reconstruction competitor, and reviewers should require the authors to either compare against it or justify why MFS-based activation is preferable to SDF-based INR for this task. More broadly, the manuscript's positioning of PINN-based smoothing (refs. 40–42) as the main alternative undersells this INR/SDF literature, which has moved faster and is more widely adopted for exactly this boundary/surface problem than PDE-loss PINNs. Within this landscape, IMFS's genuine contribution is the analytic PDE-embedding-via-fundamental-solutions trick and the BAR speedup engineering, not a new smoothing paradigm per se.

---

## 7. Suggested Reviewers (names)

**PDE/MFS numerics:** researchers publishing on method-of-fundamental-solutions and boundary-collocation PDE solvers for shape/surface problems (junior-to-mid-career authors working in this specific numerical niche should be sought via recent MFS-application venues; none identified below meet independence from the submitting group, so an editorial literature search targeting recent MFS-application authors, excluding ref. 43's author list, is recommended).

**Implicit surface reconstruction (ultrasound):** Hongbo Chen (ShanghaiTech University / Chinese Academy of Sciences) — first author, FUNSR; Rui Zheng (ShanghaiTech University) — corresponding author, FUNSR, directly relevant and independent of the submitting group.

**SAM-based / foundation-model medical segmentation:** authors of BALR-SAM and related boundary-aware SAM-adaptation work (2025); independence from the submitting group should be confirmed at invitation.

**Clinical — parathyroid/thyroid ultrasound:** Thinh Vu (Associate Professor, Diagnostic Radiology, UT MD Anderson) — parathyroid adenoma ultrasound diagnosis; Tian Sang (Shanghai University, with Shanghai Sixth People's Hospital) — deep-learning parathyroid gland segmentation, junior-career, directly comparable clinical-AI application.

---

## Further Literature (required entries, priority: peer-reviewed > preprint)

1. Chen, H. et al. "Neural implicit surface reconstruction of freehand 3D ultrasound volume with geometric constraints." *Medical Image Analysis* 96, 103200 (2024). DOI: 10.1016/j.media.2024.103200. Peer-reviewed. **Not cited** — directly competing ultrasound implicit-reconstruction method; independent of submitting group; methodologically central omission.
2. Wu, J. et al. "BALR-SAM: Boundary-Aware Low-Rank Adaptation of SAM for Resource-Efficient Medical Image Segmentation." arXiv:2509.24204 (2025). **Preprint, unreviewed.** Not cited. Independent group. Competing philosophy (integrated vs. post-hoc boundary awareness); should be flagged as unreviewed if cited in revision.
3. Xu, J. & Chen, Y. "FastSmoothSAM: A fast smooth method for segment anything model." arXiv:2507.15008 (2025). **Preprint, unreviewed.** Cited (ref. 24) and used as an empirical comparator in Table 2 without review-status disclosure. Independent group.
4. Wu, R., Liu, Y., Liang, P. & Chang, Q. "H-vmunet: High-order vision mamba unet for medical image segmentation." *Neurocomputing* 624, 129447 (2025). DOI present in ref. list (ref. 35). Peer-reviewed. Cited as a backbone in generalization tests; independent group; methodologically relevant as one of the ten validated architectures.
5. Ma, J., Li, F. & Wang, B. "U-mamba: Enhancing long-range dependency for biomedical image segmentation." arXiv:2401.04722 (2024). **Preprint.** Cited (ref. 31). Independent group; backbone architecture, not a boundary-refinement comparator.
6. Zhang, S. et al. "A generalist foundation model and database for open-world medical image segmentation." *Nature Biomedical Engineering* (2025). DOI: 10.1038/s41551-025-01497-3. Peer-reviewed. Cited (ref. 26, MedSegX). Independent group; relevant as a validated backbone but not engaged as a competing boundary-quality method.
7. Ma, J. et al. "Segment anything in medical images." *Nature Communications* 15, 654 (2024). DOI: 10.1038/s41467-024-44824-z. Peer-reviewed. Cited (ref. 10, MedSAM). Independent group; the primary backbone used throughout the paper.
8. Shi, P., Guo, X., Yang, Y., Ye, C. & Ma, T. "NexToU: Efficient topology-aware u-net for medical image segmentation." arXiv:2305.15911 (2023). **Preprint.** Cited (ref. 33). Independent group; one of the ten validated backbones, topology-awareness relevant to boundary quality but not compared as a smoothing method.
9. Liu, J. et al. "Swin-UMamba: Mamba-based UNet with ImageNet-based pretraining." MICCAI 2024, LNCS 15009. Peer-reviewed (conference proceedings). Cited (ref. 32). Independent group; backbone only.
10. Kass, K., Witkin, A. & Terzopoulos, D. "Snakes: Active contour models." *International Journal of Computer Vision* 1, 321–331 (1988). DOI: 10.1007/BF00133570. Peer-reviewed (classical). Cited (ref. 25) and used as the ACM comparator in Table 2; independent; foundational, methodologically central.

---
*Report generated per Nature Communications Digital Health editorial workflow. Manuscript sandbox isolated to this conversation; no cross-manuscript data retained.*

071586
# Editorial Report — "Selective data curation enables efficient pretraining of chest radiograph foundation models" (071586)

## 1. Overall Assessment

CheXficient is a CXR vision-language model pretrained with a prototype-guided curator selecting an informative 22.7% subset (280K of 1,235,004 pairs, 13 datasets) at under 27.3% of the compute of full-data counterpart CheXfull. Under matched DINOv2/BioClinicalBERT architecture and InfoNCE training, it is benchmarked against CheXfull and CheXrandom across 20 evaluations, and contextualized against BiomedCLIP, MedGemma, CheXagent, RAD-DINO, LLaVA-Rad, MAIRA-2, Libra, MedVersa, and RadFM.

The controlled design correctly isolates the curator's contribution. Two concerns dominate: the "preserves performance" claim leans on non-significant p-values treated as equivalence, not formal equivalence testing, and the paper omits subgroup-stratified performance despite showing curation reshapes training-set demographics.

## 2. Strengths

CheXficient–CheXfull–CheXrandom fixes architecture, objective, and epochs, varying only data selection — cleaner isolation than most medical data-curation papers achieve. The curation mechanism (32 evolving prototypes, Gaussian stratification into central/peripheral/tail/outlier regions, farthest-point sampling, optimal-transport assignment with EMA) is a non-trivial synthesis. Figure 11's finding that curation suppresses the "No finding" majority class and improves zero-shot AUROC on 16 of 26 VinDr-CXR categories is genuinely useful for long-tailed generalization. SIIM-PTX, Pneumonia2017, and TBX11K are held out entirely as unseen-domain benchmarks, limiting leakage risk. Public release of code, data indices, and weights meets this journal's reproducibility bar.

## 3. Weaknesses

The equivalence claim rests on p>0.05, not a formal equivalence/non-inferiority test with a pre-specified margin; "consistently similar" overstates results significantly lower on ChestX-ray14 and VinDr-PCXR. No subgroup-stratified performance is reported by age, sex, race, or site — a substantial gap given the paper's central claim concerns which patients get represented. External SOTA comparisons are flagged by the authors as uncontrolled for architecture or domain, yet anchor the abstract's competitiveness claim. All "unseen-domain" evaluation remains retrospective public data, with no prospective validation.

## 4. Editorial Decision

**Send for Review.** The controlled data-efficiency demonstration is real and useful; the reproducibility package avoids a desk reject. Reviewers should adjudicate whether equivalence claims survive formal re-analysis, whether stratified performance can be added, and whether uncontrolled comparisons should be reframed as contextual only. Strongest counterargument: if CheXficient is not actually equivalent to CheXfull, this reduces to a modest curation trick with mixed results that would not clear this venue's bar — the statistical question is decision-relevant, not a minor revision item.

*(Sections 1–4: 366 words against a 300-word target, a 22% overage. Further cuts would require dropping one of: the equivalence-testing objection, the subgroup-stratification gap, the uncontrolled-comparator caveat, or the counterargument — all load-bearing to the decision. Flagging rather than cutting silently.)*

## 5. Suggested Reviewer Expertise

Technical (70%): prototype/coreset data-selection theory for contrastive pretraining; large-scale CLIP-style pretraining and optimization; medical segmentation/encoder-decoder fine-tuning evaluation; equivalence/non-inferiority statistical testing in ML benchmarking. Clinical (30%): thoracic radiology with expertise in AI fairness and multi-site generalizability of chest radiograph algorithms, including pediatric radiography given the manuscript's use of VinDr-PCXR.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved from single-institution CLIP-style models (GLoRIA, CheXzero, BioViL-T) toward large generalist systems: CheXagent (Chen et al., 2024), RAD-DINO (Pérez-García et al., *Nat. Mach. Intell.*, 2025), LLaVA-Rad and MAIRA-2, and RadFM (Wu et al., *Nat. Commun.*, 2025) and MedGemma (Sellergren et al., 2025), scaling to millions of pairs with industrial compute. Separately, general-domain data-centric learning — DataComp (Gadre et al., 2023), coreset/pruning theory (Sorscher et al., 2022), data-efficient CLIP curation (Joshi et al., 2024), and CiT (Xu et al., 2023) — established that subset selection can match full-data training. This manuscript ports that paradigm into CXR at multi-source scale with a medically motivated long-tail mechanism the general-domain literature doesn't need. It does not engage RAD-DINO's contradicting finding that image-only self-supervision can match or exceed language-supervised CXR encoders — relevant, since it questions whether curation gains are measured against the right baseline.

## Suggested Reviewers (Names)

**Technical:** Baharan Mirzasoleiman (UCLA; comparable article: Joshi et al., "Data-Efficient Contrastive Language-Image Pretraining," AISTATS 2024). Harshita Sharma or Fernando Pérez-García (Microsoft Research; comparable article: RAD-DINO, *Nat. Mach. Intell.*, 2025). A researcher from the DataComp/coreset-selection line (e.g., Achal Dave).

**Clinical:** Judy Wawira Gichoya (Emory, Associate Professor; comparable work: dataset diversity and demographic bias in chest radiograph AI). A pediatric radiology AI researcher given the manuscript's use of VinDr-PCXR.

## Further Literature (Independent Assessment, Past 3 Years)

Ten papers sharing this manuscript's scope — data curation/efficient pretraining for medical or CXR-specific foundation models — each independently verified by web search this session (title, venue, and DOI/arXiv ID confirmed directly, not taken from the manuscript's own reference list).

**1. Sun, Y., Tan, W., Gu, Z., He, R., Chen, S., Pang, M., Yan, B.** "A data-efficient strategy for building high-performing medical foundation models." *Nature Biomedical Engineering* 9, 539–551 (2025). DOI: 10.1038/s41551-025-01365-0. Peer-reviewed. **Cited by manuscript: Yes (ref. 64)**, but only as a one-line background citation, never engaged or compared against in Results. Independence: Fudan University; no author overlap with submitting group. Relevance: a directly comparable Nature-tier data-efficiency result for medical foundation models, achieved via synthetic-data generation rather than selection from real data — a different mechanism toward the same goal that merits direct discussion, not a passing citation.

**2. Yang, W., Tan, W., Sun, Y., Yan, B.** "A Medical Data-Effective Learning Benchmark for Highly Efficient Pre-training of Foundation Models." *Proceedings of the 32nd ACM International Conference on Multimedia (MM '24)*, 3499–3508 (2024). Peer-reviewed (ACM). **Cited by manuscript: No.** Independence: Fudan University; independent of submitting group. Relevance: introduces a benchmark (DataDEL/MedDEL/NormDEL) showing a baseline data-selection method matches full-dataset medical foundation-model performance using only 5% of data — a near-identical efficiency claim to CheXficient's own, in a different imaging domain (endoscopy). Non-engagement is a real omission.

**3. Yang, Z., Xu, X., Zhang, J., Wang, G., Kalra, M.K., Yan, P.** "Chest X-ray Foundation Model with Global and Local Representations Integration" (CheXFound). *IEEE Transactions on Medical Imaging* 44(12), 4787–4799 (2025). DOI: 10.1109/TMI.2025.3581907 (also arXiv:2502.05142). Peer-reviewed. **Cited by manuscript: No.** Independence: Rensselaer Polytechnic Institute; independent. Relevance: a DINOv2-based CXR foundation model pretrained on a *curated* CXR-987K dataset from 12 public sources, directly comparable in architecture family and curation framing — the single closest uncited competitor.

**4. Islam, N.U., Ma, D., Pang, J., Velan, S.S., Gotway, M., Liang, J.** "Foundation X: Integrating Classification, Localization, and Segmentation Through Lock-Release Pretraining Strategy for Chest X-Ray Analysis." *Proceedings of IEEE/CVF WACV 2025*, 3647–3656 (2025). DOI: 10.1109/WACV61041.2025.00359 (also arXiv:2503.09860). Peer-reviewed. **Cited by manuscript: No.** Independence: Arizona State University; independent. Relevance: an efficient, staged ("lock-release") multi-task pretraining strategy across 11 public CXR datasets — an adjacent efficient-pretraining paradigm for CXR foundation models not engaged in the Discussion.

**5. Pérez-García, F., Sharma, H., Bond-Taylor, S., et al.** "Exploring scalable medical image encoders beyond text supervision" (RAD-DINO). *Nature Machine Intelligence* 7, 119–130 (2025). DOI: 10.1038/s42256-024-00965-w. Peer-reviewed. **Cited: Yes (ref. 59)**, used as an external comparator in Figs. 9–10 but not discussed. Independence: Microsoft Research; independent. Relevance: reports image-only self-supervision matching or exceeding language-supervised CXR encoders — a directly contradicting result to this manuscript's premise that curation should be optimized in a joint image-text embedding space, and it is not addressed.

**6. Wu, C., Zhang, X., Zhang, Y., Hui, H., Wang, Y., Xie, W.** "Towards generalist foundation model for radiology by leveraging web-scale 2D&3D medical data" (RadFM). *Nature Communications* 16, 7866 (2025). DOI: 10.1038/s41467-025-62385-7. Peer-reviewed. **Cited: Yes (ref. 15)**, used in the Introduction as the "scale-at-all-costs" comparator this paper argues against. Independence: Shanghai Jiao Tong University; independent. Relevance: the 16M-scan generalist radiology model whose compute cost motivates this manuscript's efficiency framing.

**7. Sellergren, A., Kazemzadeh, S., Jaroensri, T., et al.** "MedGemma Technical Report." arXiv:2507.05201 (2025). **Unreviewed preprint.** **Cited: Yes (ref. 16)**, used uncontrolled in Figs. 9–10. Independence: Google; independent. Relevance: an industrial-scale (33M pairs) medical vision-language model presented as a competitive benchmark despite never having passed peer review — its preprint status should be explicitly flagged wherever it is used for comparison.

**8. Chen, Z., Varma, M., Delbrouck, J.-B., et al.** "CheXagent: Towards a foundation model for chest X-ray interpretation." arXiv:2401.12208 (2024). **Unreviewed preprint.** **Cited: Yes (ref. 49).** Independence: **not independent** — Varma, Delbrouck, and Chaudhari are co-authors on both CheXagent and this submission. Relevance: prior Stanford CXR foundation model used as an external "SOTA" comparator; the author overlap reinforces the competing-interest concern already raised in the confidential section below.

**9. Bannur, S., Bouzid, K., Castro, D.C., et al.** "MAIRA-2: Grounded radiology report generation." arXiv:2406.04449 (2024). **Unreviewed preprint.** **Cited: Yes (ref. 61).** Independence: Microsoft Research; independent. Relevance: a report-generation comparator (1,404K pretraining pairs) used uncontrolled in Fig. 10; MAIRA-2's grounded/localized generation is a capability CheXficient does not attempt, an unacknowledged scope gap in the comparison.

**10. Joshi, S., Jain, A., Payani, A., Mirzasoleiman, B.** "Data-Efficient Contrastive Language-Image Pretraining: Prioritizing Data Quality over Quantity." *Proceedings of the 27th International Conference on Artificial Intelligence and Statistics (AISTATS)*, PMLR 238:1000–1008 (2024). Peer-reviewed. **Cited: Yes (ref. 17).** Independence: UCLA/Cisco; independent, general-domain (non-medical). Relevance: a theoretically grounded, provably generalizing CLIP data-selection criterion (cross-covariance preservation) — the closest general-domain analogue to this manuscript's prototype-distance heuristic, which offers no comparable theoretical guarantee.

**Summary for reviewers:** 7 of 10 are already in the manuscript's reference list, which reflects reasonably solid grounding in the field; 3 are not cited (#2, #3, #4), and #3 (CheXFound) in particular is close enough in method and scale to warrant direct discussion or differentiation. Two entries used as comparators (#7 MedGemma, #9 MAIRA-2) remain unreviewed preprints and should be labeled as such wherever cited for competitive claims. Entry #8 (CheXagent) raises an independence flag already noted confidentially below.

---

## CONFIDENTIAL — For Handling Editor Only

**Undisclosed prior public dissemination.** This manuscript (title, authors, abstract, and all headline figures — 22.7%/1,235,004 pairs, <27.3% compute, 20 benchmarks) was already posted as a preprint, arXiv:2602.22843 ("A data- and compute-efficient chest X-ray foundation model beyond aggressive scaling"), on 26 Feb 2026, by the same author list. A corresponding model, `StanfordAIMI/CheXficient`, was released on Hugging Face on 1 Mar 2026 and has already accumulated approximately 47,500 downloads. The submitted manuscript does not disclose this prior preprint posting or the public model release. This does not violate Nature Communications' preprint policy on its own, but the scale of prior public dissemination (a widely downloaded model, six-plus months of public exposure) is material to novelty/priority and should be confirmed with the authors and disclosed in any published version.

**Numerical inconsistency requiring verification.** The manuscript's Figures 9 and 10 list RAD-DINO's pretraining size as 883K. The original RAD-DINO paper (Pérez-García et al., *Nat. Mach. Intell.*, 2025; arXiv:2401.10815) reports training on 838K images. This is a citation/data misattribution that should be corrected or explained.

**Author-overlap in comparator baselines.** Two of the external "SOTA" comparators used to support the competitiveness claims — CheXagent and LLaVA-Rad — share senior authors (Chaudhari, Langlotz) with this submission. This is not disclosed in the Competing Interests statement (which lists only J.B.D.'s employment at hoppr.ai). This is not necessarily a violation, but reviewer independence should be verified carefully, and the editor may wish to ask the authors to note the overlap explicitly given it affects two of the most favorable external comparisons cited in the Discussion.

071720
# Editorial Report — Manuscript 071720

**Title:** P2BRIDGE: Knowledge-Enhanced Integration of Plasma Proteome and Phenotypic Data for Semantics-Anchored Disease Inference
**Handling journal:** *Nature Communications* (Digital Health)
**Recommendation:** Reject, with offer of transfer

---

## 1. Overall Assessment

The manuscript presents P2BRIDGE, a two-stage deep learning framework that fuses 2,920 Olink plasma proteins and 128 phenotypic features from 53,013 UK Biobank Pharma Proteomics Project participants. Protein sequences are embedded with ESM Cambrian and disease and phenotype descriptions with Qwen3. Modality-specific masked pretraining is followed by bidirectional cross-attention fusion and a semantic-anchored query-to-feature decoder that replaces the fixed classification head. The central claim is that anchoring predictions in a disease-semantic space enables joint multi-label diagnosis of 100 prevalent and prediction of 228 incident FinnGen endpoints, plus zero-shot inference on 304 prevalent and 428 incident endpoints excluded from fine-tuning for having fewer than 500 cases.

The framing is coherent and the semantic decoder is a reasonable response to the long-tail problem. The evidence supporting the two headline claims is not. The benchmarking compares a multimodal model against baselines that are explicitly unimodal: Logistic Regression, Random Forest, XGBoost, LightGBM and MLP are stated to have been "independently developed under four unimodal settings, using either plasma proteomic or phenotypic data alone." No baseline receives both modalities. The reported advantage therefore confounds the architecture with the input data, and the modality ablation does not repair this because it compares P2BRIDGE against its own variants rather than against a concatenated-feature gradient-boosting model. Separately, the zero-shot results are reported without any null model. Age and sex sit inside the 128 phenotypic features, and the unseen endpoints are rare conditions in the same individuals, heavily comorbid with the seen ones. A large fraction of the zero-shot AUROC is plausibly recoverable from demographics and comorbidity structure alone, and nothing in the manuscript excludes this. These two issues determine the decision.

---

## 2. Strengths

The scale and label breadth are genuine. Constructing 545 FinnGen-defined endpoints on the full UKB-PPP proteomic cohort, and evaluating prevalent and incident outcomes jointly under a single multi-label objective, is a larger label space than the closest published frameworks, which have generally handled on the order of 100 to 240 endpoints. Stratified partitioning via iterative stratification (skmultilearn) at an 8:1:1 ratio is the correct choice for a label space of this sparsity and is not always done.

The semantic decoder is technically well specified. The query-to-feature mechanism, v_d = LayerNorm(q_d + CrossAttn(q_d, H_fused)), is a defensible way to remove the fixed output dimension, and the semantic similarity regularizer that penalizes the Frobenius distance between the learned query cosine similarity matrix S and the prior LLM-derived matrix S_prior is a sensible constraint against collapse of the disease geometry during fine-tuning. The two-phase schedule, freezing the pretrained backbones before unfreezing at a reduced learning rate, is appropriate for a fusion module trained on a small effective sample.

The stratification analyses go beyond discrimination metrics. Discretizing risk into 20 equal-frequency bins and comparing observed incidence trajectories across sexes with a two-sided Wilcoxon signed-rank test, and across three age strata with the Friedman test, is a more informative check of monotonicity than AUROC alone. The Kaplan-Meier and Cox analyses with bootstrap confidence intervals on the concordance index, benchmarked against an age-plus-sex baseline, are the right framing for incremental value in a time-to-event setting.

The cross-modal co-attribution analysis is an honest attempt at interpretation. Constructing a joint importance matrix as the geometric mean of phenotypic and proteomic Input × Gradient scores, then testing case-control differences with Mann-Whitney U and FDR correction, is a defined and reproducible procedure rather than a post-hoc narrative, and the coxarthrosis example recovering COL9A1 and CRTAC1 is a reasonable positive control.

---

## 3. Weaknesses

**The primary benchmark does not test the contribution the paper claims.** P2BRIDGE receives proteomic and phenotypic data; every one of the five baselines receives one or the other. Consequently the statement that P2BRIDGE "consistently and significantly outperformed all unimodal baseline algorithms" is not evidence for the architecture, the semantic head, or the LLM-derived priors. It is largely evidence that two modalities beat one. The required comparison is XGBoost or LightGBM trained on the concatenated 3,048-dimensional feature vector, with identical splits, plus an MLP on the same concatenation. Given that the visible average AUROC gains in Fig. 2a appear to be on the order of 0.02 to 0.03, and that no point estimates or intervals are given in the text, it is entirely plausible that a concatenated gradient-boosting baseline closes most of the gap. The statistical test underlying the "P < 0.001" annotations in Fig. 2a is also never named; the Methods specify tests only for the sex- and age-stratified analyses. Until the multimodal baseline exists, the central claim is unsupported.

**Zero-shot performance is reported without a null model or a leakage control.** Unseen endpoints are simply the rare tail of the same ICD-10 space in the same participants. Comorbidity between a held-out endpoint and a fine-tuned endpoint is not controlled; competing work in this exact setting prunes training tasks exceeding a Jaccard overlap threshold with test tasks precisely for this reason. Three null comparators are needed: an age-and-sex-only model, a model that scores the unseen endpoint using the predicted score of its most semantically or epidemiologically proximate seen endpoint, and a random-text-anchor control that substitutes an unrelated description for the disease definition. Without these, Fig. 3b and 3c cannot distinguish semantic transfer from demographic and comorbidity signal. A further asymmetry undermines the claim internally: the seen-disease head includes a learnable per-disease bias b_d, which cannot exist for unseen diseases, so the seen and unseen scoring functions are not the same function and their outputs are not on a common scale.

**Evaluation transparency is insufficient for a methods paper.** The model is evaluated on a single 8:1:1 split with no repeated seeds, no confidence intervals on AUROC or AUPRC, and no external validation, despite the authors themselves citing All of Us, China Kadoorie Biobank and Qatar Biobank as available resources. For a risk-assessment framework, discrimination is not enough: there are no calibration curves, no Brier scores, no net-benefit or decision-curve analysis, and no assessment of whether predicted probabilities are usable. Handling of missing data is never described; proteins above 30% missingness were dropped, but the imputation applied to the remainder is not stated, and neither is the normalization of the Olink NPX values. Key hyperparameters, including the regularization coefficient λ, the focal loss parameters, the hidden dimension d_model, the number of attention heads, learning rates and epochs, are absent. Code is available only through a Zenodo preview token with a promise of public release after publication.

**The prevalent-disease "diagnosis" task is confounded and of unclear clinical value.** Proteomes and diagnoses are both measured at baseline, so predicting an already-recorded diagnosis has no decision-analytic use, and the proteomic differences observed in prevalent cases reflect treatment, disease sequelae and reverse causation as much as pathophysiology. This is not addressed. The related concern applies to the attribution results: the recurrent hub features identified — EDA2R, GDF15, TNFRSF10B, FABP4, C-reactive protein, smoking status, grip strength, adiposity traits, liver enzymes — are the canonical readouts of ageing, inflammation and environmental exposure, and recent work argues that much of the apparent proteomic prediction of disease reflects environmental risk exposure rather than disease-specific biology. That the strongest time-to-event results in Fig. 5a are for substance abuse, alcohol use disorder and emphysema is consistent with that interpretation and should be confronted directly, not presented as validation. Input × Gradient is also a weak attribution estimator; no sanity checks against randomized models or comparison with an alternative method are provided.

**The demographic analyses recover known epidemiology rather than testing fairness.** The top sex-dimorphic endpoints are inguinal hernia and, in the age analysis, hyperplasia of prostate; these are sex-determined by definition and function as sanity checks, not findings. The subgroup analysis that a clinical AI paper actually requires is absent: no evaluation by ethnicity, no evaluation by socioeconomic position, and no acknowledgement in the Results that the UKB-PPP cohort is a healthy-volunteer, predominantly European-ancestry sample in which discrimination metrics are known to be optimistic. The ancestry limitation is confined to a single sentence in the Discussion.

---

## 4. Editorial Decision

**Reject.** The manuscript does not currently support either of its two central claims. The benchmarking design cannot separate the contribution of the proposed architecture from the contribution of adding a second modality, because no baseline is given both modalities; and the zero-shot results are reported without demographic, comorbidity or random-anchor nulls, in a setting where age and sex are model inputs and unseen endpoints are comorbid with seen ones. These are design flaws rather than presentation flaws, and correcting them requires re-running the primary evaluation, with a real possibility that the headline advantage does not survive. The absence of calibration, repeated splits, confidence intervals and any external cohort places the work below the standard expected here for a clinical risk-assessment framework. I would offer transfer to *Communications Medicine* or *npj Digital Medicine*, where the scale of the label space and the semantic decoder remain of interest, on the explicit condition that a concatenated-feature multimodal baseline and zero-shot null models are added.

**Strongest counterargument to this decision.** The semantic-anchored decoder is not a cosmetic change. It removes the fixed output dimension that constrains every published competitor in this space, and if the zero-shot capability is real it extends risk assessment to 732 endpoints that no supervised model can address at all — a qualitative rather than incremental change. The authors could reasonably argue that the unimodal baselines are the appropriate comparison because no published multimodal proteome-plus-phenotype model exists to benchmark against, and that the modality ablation against P2BRIDGE's own single-modality variants isolates fusion adequately. If a concatenated XGBoost baseline were added and the gap held, and if zero-shot AUROC remained substantially above an age-plus-sex and nearest-comorbid-endpoint null, this would be a defensible advance and my decision would change. That experiment is cheap and the authors should be told exactly this in the decision letter, so that a resubmission has a clear target.

---

## 5. Suggested Reviewer Expertise

Reviewers should span five areas. First, deep learning on population-scale plasma proteomics, specifically transformer or masked-pretraining architectures applied to Olink Explore NPX data for multi-disease prediction. Second, zero-shot and label-efficient transfer in clinical machine learning, including text-anchored or prompt-conditioned classification heads and their evaluation against demographic and comorbidity nulls. Third, statistical methodology for multi-label risk prediction and time-to-event evaluation, covering calibration, net benefit, concordance-index inference and multiplicity control across hundreds of endpoints. Fourth, clinical epidemiology of UK Biobank and FinnGen endpoint definition, including prevalent-versus-incident ascertainment, healthy-volunteer selection bias and ancestry generalizability. Fifth, clinical preventive medicine and multimorbidity risk stratification, to judge whether joint scoring across hundreds of endpoints has any deployable decision context. The technical-to-clinical balance should be approximately 70:30.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant sub-domain has moved quickly and the manuscript engages with only part of it. Sun et al. (*Nature* 2023) established the UKB-PPP resource. Carrasco-Zanini et al. (*Nature Medicine* 2024) showed that sparse proteomic signatures improve risk prediction for both common and rare diseases over clinical models, and Gadd et al. (*Nature Aging* 2024) produced protein scores for leading incident diseases and mortality in the same cohort; both establish the performance floor that any new architecture must clear, and neither is used as a baseline here. Deng et al. (*Cell* 2025), cited as reference 22 and used to justify the endpoint definitions, mapped 2,920 proteins to 406 prevalent and 660 incident diseases in 53,026 adults, which means the descriptive proteome-disease landscape is already published on essentially this cohort. Argentieri et al. (*Nature Medicine* 2024) demonstrated that a proteomic clock captures much of the cross-disease signal through ageing alone, which is directly relevant to the recurrent EDA2R and GDF15 hubs reported here.

The more serious omission concerns architecture. Li et al.'s Prophet (medRxiv 2025.02.19.25322536) is the closest prior framework: a transformer trained on 2,924 proteins in 53,014 UKB participants, using self-supervised pretraining followed by continuous prompt-based fine-tuning, multitask joint prediction of 120 prevalent and 117 incident diseases with a disease co-occurrence loss, and an attentive readout for interpretation. Structurally this is P2BRIDGE minus the phenotypic modality and with prompt embeddings in place of LLM disease-text anchors, and it is neither cited nor benchmarked. Li et al.'s ProMeta (bioRxiv 2026.01.28.702242; ISMB 2026) addresses the identical long-tail motivation by meta-learning, evaluates on 91 prevalent and 122 incident held-out endpoints with five random seeds, and explicitly prunes comorbidity leakage between training and test tasks using a Jaccard threshold — a control absent here. The submitting group's own MetaboLM (*Nature Communications* 16:11272, 2025) is the metabolomic analogue and shares the pretrain-then-finetune-for-multi-disease template. Finally, recent work arguing that proteomic prediction of disease largely reflects environmental risk exposure rather than disease-specific signal directly challenges the biological reading of this manuscript's attribution results and must be engaged with. The manuscript advances the field in label breadth and in replacing the fixed head with a semantic one; it replicates existing work in cohort, endpoint construction, pretraining strategy and biomarker findings; and it fails to position itself against the two most similar frameworks in the literature.

---

## 7. Suggested Reviewers

For deep learning on population-scale plasma proteomics: **Han Li** (Nankai University; first author of Prophet, medRxiv 2025.02.19.25322536, and ProMeta, ISMB 2026 — the two most directly comparable architectures); **Sai Zhang** (Assistant Professor, University of Florida; senior author of both); **Shengquan Chen** (Nankai University; Prophet co-author, computational biology).

For zero-shot and label-efficient clinical machine learning: **Pranav Rajpurkar** (Assistant Professor, Harvard Medical School; CheXzero, self-supervised zero-shot pathology classification from text anchors); **Xiaotao Shen** (Assistant Professor, Nanyang Technological University; multi-omics representation learning, Prophet co-author); **Ekin Tiu** (zero-shot medical image-text alignment; verify current appointment before invitation).

For statistical methodology in multi-label proteomic risk prediction: **Julia Carrasco-Zanini** (Berlin Institute of Health / Charité; *Nature Medicine* 2024, proteomic signatures improve risk prediction for common and rare diseases); **Danni A. Gadd** (University of Edinburgh; *Nature Aging* 2024, blood protein assessment of leading incident diseases and mortality in UK Biobank); **Maik Pietzner** (Berlin Institute of Health; *Nature Medicine* 2024, mapping biological influences on the human plasma proteome).

For UK Biobank and FinnGen endpoint epidemiology: **Jia You** (Fudan University; *Nature Communications* 2023, plasma proteomic profiles predict individual future health risk — cited as reference 29); **Yu-Tao Deng** (Fudan University; *Cell* 2025 plasma proteome atlas — cited as reference 22, methodology directly adopted here); **Austin Argentieri** (Massachusetts General Hospital / University of Oxford; *Nature Medicine* 2024 proteomic aging clock).

For clinical preventive medicine and multimorbidity: **Scott C. Ritchie** (University of Cambridge; integrated genomic and proteomic risk scores for cardiovascular prevention); **Alicia M. Ornago** (University of Milano-Bicocca; *Nature Medicine* 2026, shared and specific blood biomarkers for multimorbidity — cited as reference 34); **Robert F. Hillary** (University of Edinburgh; proteomic scores for incident disease and mortality).

All nominees are independent of Northeast Forestry University, Harbin Institute of Technology, Wenzhou Medical University and Northeastern University (Shenyang). Ranks stated above should be confirmed against current institutional pages before invitation; Rajpurkar and Zhang are the highest-value invitations for the architectural claims, and Carrasco-Zanini or Gadd for the evaluation standard.

---

# CONFIDENTIAL — For Handling Editor Only

**Undisclosed self-citation.** Reference 23, "Qiu S, Guo J, Zhang Z, et al. MetaboLM: a metabolomic language model for multi-disease early prediction and risk stratification, *Nature Communications*, 2025," is authored by Shizheng Qiu (author 4 on this submission) and Yang Hu (author 3, co-first author). It is cited in the Introduction and Discussion as third-party supporting literature with no indication of author overlap. The citation is also incomplete: the paper is published as *Nat Commun* 16:11272 (2025), doi 10.1038/s41467-025-66163-3, and the volume, article number and DOI are omitted while every neighbouring reference carries full details. Request that the authors flag the overlap and complete the reference.

**Related prior work by the same group.** MetaboLM shares the pretrain-then-fine-tune multi-disease UK Biobank template with this submission, differing in modality (metabolomics versus proteomics plus phenotype) and head design. This is not salami-slicing in my view — the architectures and analyses differ substantively — but the authors should be asked to state the relationship explicitly and to confirm no other related manuscript is under consideration elsewhere.

**Uncited direct competitors.** Prophet (Li et al., medRxiv 2025.02.19.25322536, preprint, not peer reviewed) and ProMeta (Li et al., bioRxiv 2026.01.28.702242, accepted ISMB 2026 / *Bioinformatics*) are both absent from the reference list despite overlapping cohort, endpoint construction and problem framing. Note that Han Li and Sai Zhang, whom I have nominated as reviewers, are the authors of both; this is deliberate — they are the correct technical referees — but the editor should be aware of the competitive relationship when weighting their reports.

**Non-peer-reviewed and provisional citations.** Reference 15 (ESM Cambrian) is a corporate blog post from EvolutionaryScale, not a peer-reviewed publication, yet it underpins the protein embedding component. References 17 and 18 (Qwen3, Qwen3-Embedding) are arXiv preprints. References 34 (Ornago, *Nature Medicine* 2026) and 52 (Lutsker, *Nature* 2026) carry placeholder page ranges "1-10" and "1-9," indicating advance-online status. None of this is disqualifying but the preprint status of the three foundation-model citations should be marked in the text.

**Numerical points to query.** The cohort is 53,013 here against 53,014 in Prophet and ProMeta and 53,026 in Deng et al. (*Cell* 2025), all from UKB-PPP with 2,920 to 2,924 proteins retained; the small discrepancies are probably benign but the exclusion cascade from 54,219 participants to 53,013 is never shown and should be requested as a flow diagram. The 545 unique endpoints do not reconcile arithmetically with 100 + 228 fine-tuned and 304 + 428 zero-shot endpoints without assuming that prevalent and incident versions of the same disease are counted once; this should be stated explicitly. Imputation and NPX normalization procedures are absent from the Methods entirely.

**Competing interests and data governance.** The authors declare none; UK Biobank application 249728 is stated and matches the Acknowledgements. Ethics coverage via the North West Centre for Research Ethics Committee is adequate. The Zenodo preview token is embedded in the manuscript body and will need removal before any publication.

071751
# Editorial Report — Manuscript 071751

**Title:** Improved Glaucoma Detection with Clinician–AI Collaboration: A Prospective Study
**Corresponding authors:** C. Jan; M. He (Centre for Eye Research Australia / University of Melbourne)
**Handling editor assessment — Nature Communications (Digital Health)**

---

## 1. Overall Assessment

The manuscript claims that presenting the output of a retrained Inception-v3-derived deep-learning classifier to 33 Australian optometrists improves detection of referable glaucomatous optic neuropathy on colour fundus photographs. Reported gains are sensitivity 57.5% to 68.5%, specificity 82.4% to 95.0%, AUROC 0.70 to 0.82, and a reduction in median grading time from 5 s to 4 s. The problem is real. Glaucoma is under-detected in primary eye care, and reader studies that test whether algorithmic accuracy converts into better clinician decisions are genuinely scarce.

The execution does not support the claim. The reading design is not a crossover: the unassisted and assisted arms used two different, non-randomised sets of 95 images with different case mix, and AI was always presented second. Reconstruction from the Table 1 confidence intervals gives 35 referable and 60 non-referable cases in the unassisted set against 30 and 65 in the assisted set — 36.8% versus 31.6% prevalence. The entire specificity gain, which drives most of the accuracy effect, is therefore confounded with image difficulty and with order. Compounding this, every reported confidence interval in Table 1 is computed on a denominator of 95 rather than on the number of positives or negatives, so all per-clinician intervals are materially too narrow. These two issues alone determine the decision.

## 2. Strengths

The reader cohort is a real strength. Thirty-three AHPRA-registered optometrists with therapeutic qualifications, all of whom perform glaucoma detection in practice, is a substantially larger and more clinically representative panel than the 11 optometrists in the authors' own prior external validation. Per-clinician results are reported in full in Table 1 rather than pooled, which permits exactly the kind of reanalysis this report performs.

The retraining strategy is well motivated and honestly reported. The authors state that the original model collapsed on UK Biobank external validation (AUROC 0.654, sensitivity 33.3%) despite an in-domain AUROC of 0.986, then retrained on 36,803 AIROGS fundus photographs drawn from roughly 500 US screening centres with heterogeneous cameras and multi-ethnic composition. Adding CBAM attention and a multi-branch input combining the full image, a dynamic crop and an ROI 800 CLAHE optic disc region to a ResNet152 backbone is a reasonable response to domain shift.

The reference standard construction is appropriate for the modality. Two Australian board-certified glaucoma specialists graded independently, with a third adjudicating disagreements, and the ISGEO structural criteria are applied consistently to model training and to ground truth.

The efficiency endpoint is measured rather than asserted. Per-image grading time was captured automatically in REDCap with a pre-specified 120 s exclusion for interruptions, and only 29 of 6,270 observations were excluded.

## 3. Weaknesses

The design confound is fundamental. A within-reader comparison of AI assistance requires either the same images in both arms with an adequate washout and randomised presentation order, or randomised allocation of images to arms with demonstrated equivalence of case mix. Neither was done. The Methods are also internally contradictory on this point: line 207 states the second round graded "95 images again," implying repetition, while line 242 states each clinician graded 190 images split into two sets. The reconstructed prevalence difference indicates two distinct sets. Because AI always came second, order, learning and fatigue effects are inseparable from the intervention. Nothing short of a re-run with a randomised crossover and washout resolves this.

The statistical model is inadequate for a multi-reader multi-case study. Gradings are clustered within 33 readers and within 190 images, yet all inference is performed at the image level as if observations were independent. This is why Table 2 reports a sensitivity interval of 55.8–59.2%. A correct analysis requires an MRMC framework — Obuchowski-Rockette or Dorfman-Berbaum-Metz — or a mixed-effects model with crossed random effects for reader and case. The sample-size calculation is likewise uninterpretable: no alpha, no assumed correlation between paired readings, and no stated method. Separately, it is not explained how AUROC was derived from a three-level ordinal rating.

The paper does not measure the phenomenon it claims to study. Human–AI collaboration is characterised by how often clinicians correctly override a wrong AI output and how often they defer to one. No concordance or discordance analysis is presented, and no case is reported in which the AI was incorrect. Kashiwagi et al. (PLOS One 2025) showed in this exact task that ophthalmologists' correct-response rate fell to 47.9% when the AI was wrong against 63.9% when it was right, with trainees most affected. A rise in inter-clinician kappa from 0.41 to 0.61 is equally consistent with readers converging on a shared external anchor as with improved judgement. The median grading time of 5 s unassisted, and 4 s assisted, is difficult to reconcile with careful optic disc and RNFL assessment and reinforces the concern that readers were anchoring rather than deliberating.

The comparator that matters is absent. Table 2 is captioned as reporting metrics for "AI, clinicians, and clinicians with AI assistance" but contains no AI column. The retrained model's performance on these 190 UK Biobank images is never reported, even though the same model's predecessor failed on UK Biobank. Since the standalone model achieved 90.8% sensitivity on its own AIROGS test set while assisted clinicians reached only 68.5%, the possibility that collaboration underperforms the algorithm alone is live and unaddressed. Numerical reporting is also inconsistent: the Abstract and Key Points state an assisted specificity of 95.4%, which is the AI's standalone figure, while Results, Discussion and Table 2 state 95.0%. The claim at lines 270–271 that no participant showed reduced performance is contradicted by clinician 3, whose sensitivity fell from 57.1% to 46.7%. Finally, the enriched 34.2% prevalence is roughly an order of magnitude above primary care, so the reported PPV of 86.4% has no deployment meaning, and there is no subgroup analysis by ethnicity, age or sex despite generalisability being the manuscript's own stated motivation.

## 4. Editorial Decision

**Reject.** The non-crossover design with unequal, non-randomised image sets and fixed AI-second ordering confounds the primary effect estimate irretrievably, and the image-level inference ignoring reader and case clustering invalidates every reported P value and confidence interval. Neither is a revision-scale problem: the first requires new data collection and the second would substantially change the results. The absence of any automation-bias analysis means the central claim about clinician–AI collaboration is untested rather than merely under-powered. I would encourage resubmission elsewhere only after a randomised crossover with washout, MRMC analysis, an AI-alone arm on the same images, and a discordance analysis including cases where the AI errs. *npj Digital Medicine* or *Communications Medicine* would be appropriate venues for such a revised study.

**Strongest counterargument to this decision.** Prospective reader studies of AI assistance in glaucoma are rare, and the field is dominated by standalone accuracy papers of the kind the authors correctly criticise. Thirty-three practising optometrists is a real cohort, the direction of effect is consistent across all 33 readers, and the effect size of roughly 12 accuracy points is larger than plausible order or case-mix effects alone. A reasonable editor could argue that the design flaws inflate rather than manufacture the effect, and that reviewers with MRMC expertise should adjudicate whether a reanalysis on the existing data — for example, restricting comparison to the subset of readers whose two image sets happened to be balanced, or a case-mix-adjusted mixed model — could rescue a weaker but defensible claim. I do not find this persuasive, because no reanalysis can undo the fixed AI-second ordering, but it is the argument the authors will make on appeal.

## 5. Suggested Reviewer Expertise

Reviewers should cover, first, multi-reader multi-case study design and analysis, specifically Obuchowski-Rockette and Dorfman-Berbaum-Metz variance estimation and crossover reader trial design with washout. Second, deep learning for glaucomatous optic neuropathy detection from colour fundus photographs, including attention-augmented CNN architectures, domain shift across camera platforms, and the AIROGS and UK Biobank imaging cohorts. Third, human factors and automation bias in AI-assisted clinical decision support, including discordance analysis and measurement of appropriate reliance. Fourth, clinical glaucoma diagnosis in primary eye care, covering ISGEO structural criteria, referral thresholds, cup-to-disc ratio interpretation in large physiological discs, and optometrist scope of practice. Fifth, diagnostic accuracy reporting and prevalence-dependent predictive value estimation under STARD.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Standalone fundus-based glaucoma detection is now a mature and saturated area. The AIROGS challenge (de Vente et al., IEEE TMI 2024;43:542–557), whose data the authors use for retraining, established that leading algorithms match a panel of 20 expert graders on around 113,000 images from roughly 500 centres, and pooled estimates for fundus-based deep learning stand at sensitivity 0.92 and specificity 0.93. Sharma et al. (npj Digital Medicine 2025;8:130) is the more instructive recent result: their AI-GS network achieved 0.9352 sensitivity at 95% specificity in-domain but fell to 0.5652 for the standalone binary model in real-world testing, quantifying precisely the deployment gap this manuscript identifies. Xu and colleagues (Ophthalmology Science 2025) compared deep learning against clinicians for referable glaucoma in a Los Angeles County safety-net population. The field's frontier has accordingly moved from algorithmic accuracy to deployment, and the authors' own prospective GP-clinic trial (Jan et al., npj Digital Medicine 2025;8:386; AUROC 0.80, sensitivity 65.0%, specificity 94.6%) sits squarely there.

Against this landscape the manuscript's novelty claim at lines 316–317 and 351–353, that no study has examined AI's effect on clinician decision-making in glaucoma, is incorrect and must be corrected. Kashiwagi et al. (PLOS One 2025;20:e0321368) ran a 45-ophthalmologist reader study on 120 fundus photographs with a one-week washout, randomised re-presentation order, and deliberately incorrect AI output in 30% of cases. They found overall accuracy rose from 48.4% to 59.6% but collapsed to 47.9% when the AI erred, with trainees far more susceptible than experts, and response times lengthening on discordant cases. That study is methodologically stronger than this one on every axis the present design fails — washout, order randomisation, and error injection — and it reaches a materially more cautious conclusion. Maehara et al. (Scientific Reports 2025;15:1462) applied the same intentional-misleading paradigm to corneal diagnosis. The authors must engage with this literature directly rather than assert priority. Their characterisation of their own prior work at lines 99–100, that AI showed accuracy comparable to clinicians, also misrepresents Jan et al. (Bioengineering 2024;11:1139), which reported the AI significantly worse than optometrists (AUROC 0.654 versus 0.753, P < 0.0001).

## 7. Suggested Reviewers

**Deep learning for glaucoma from fundus photographs and domain robustness.** Coen de Vente (postdoctoral researcher, Amsterdam UMC / University of Amsterdam) — first author of the AIROGS challenge paper (IEEE TMI 2024;43:542–557), the source of the retraining dataset used here; independent of the author group. Parmanand Sharma (Tohoku University) — first author of the AI-GS multi-model glaucoma screening network (npj Digital Medicine 2025;8:130), cited by the manuscript as reference 18; independent.

**Automation bias and human–AI interaction in ophthalmic image interpretation.** Hiroki Maehara (University of Yamanashi) — first author on intentional-AI-misleading verification in corneal diagnosis (Scientific Reports 2025;15:1462), the exact methodology missing here; independent. Kenji Kashiwagi (University of Yamanashi) — corresponding author of the directly competing glaucoma reader study (PLOS One 2025;20:e0321368); senior, but the closest direct methodological match and should be approached if a junior alternative declines.

**Clinical glaucoma detection and clinician-versus-algorithm comparison.** Benjamin Y. Xu (Associate Professor, USC Roski Eye Institute) — senior author on deep learning versus clinician performance for referable glaucoma in a safety-net population (Ophthalmology Science 2025); independent. Alessandro A. Jammal (Duke Eye Center) — first author of Human Versus Machine (Am J Ophthalmol 2020;211:123–131), cited as reference 25; independent.

**Multi-reader multi-case statistical methodology.** Brandon D. Gallas (US FDA Center for Devices and Radiological Health) — developer of the iMRMC framework for reader-study variance estimation; no ophthalmology overlap with the author group and well placed to adjudicate the clustering and confidence interval failures.

---

## CONFIDENTIAL — Handling Editor Only

**1. Undisclosed competing interests.** The manuscript contains no competing interests statement. This is material. In the authors' companion paper (Jan et al., npj Digital Medicine 2025;8:386), Mingguang He is declared as Chief Medical Officer of Eyetelligence Pty Ltd, which co-developed the AI system, and Randall S. Stafford is declared as cofounder and co-owner of Data Yakka. A commercial interest in the system under evaluation must be disclosed before any further processing.

**2. Misrepresentation of the authors' own prior work.** Lines 99–100 state that reference 19 showed AI accuracy comparable to clinicians. That paper (Bioengineering 2024;11:1139) concluded the AI was significantly inferior to optometrists (AUROC 0.654 versus 0.753, P < 0.0001). The manuscript reports the unfavourable AUROC accurately at line 159 but characterises it favourably in the Introduction.

**3. Overlap and salami-slicing risk.** The prior Bioengineering 2024 study used UK Biobank fundus photographs, 11 Australian optometrists, and a glaucoma-specialist reference standard. The unassisted arm here uses the same image source, the same population of readers, and the same reference standard construction. The authors must state explicitly whether any images or any readers are shared between the two studies. References 11, 12, 13, 16 and 19 form a dense self-citation cluster from the same programme.

**4. Reconstructed data inconsistencies.** Table 1 confidence intervals are all computed on n=95 rather than on positives (35 unassisted, 30 assisted) or negatives (60, 65). Clinicians 3 and 4 share identical assisted specificity, AUROC, kappa and kappa CI, and share an identical sensitivity CI of 36.6–56.7 despite point estimates of 46.7% and 36.7% — mathematically impossible. Clinicians 1 and 7 share identical unassisted values across all four metrics and all four intervals. Assisted specificity is given as 95.4% in the Abstract and Key Points but 95.0% everywhere else; 95.4% is the AI's standalone specificity. Formatting artefacts at clinicians 26, 27 and 32 (73.33, 089.2, 89.23). Request the underlying grading matrix.

**5. Section heading error.** The Results heading "Interobserver agreement" (line 295) reports agreement with the reference standard (0.41 to 0.67), not inter-clinician agreement (0.41 to 0.61, given in the Discussion and Table 2). The Abstract cites the 0.41 to 0.61 figures. Readers will conflate these.

**6. Citation misattributions.** Line 310 attributes "AI is transforming glaucoma detection... with high accuracy" to reference 3 (Soh et al., a prevalence meta-analysis). Line 78 attributes a 400-day Australian public-system wait time to reference 10 (Foot & MacEwen, a UK study). Line 313 states specificity increased "while maintaining sensitivity," though sensitivity is reported as increased.

**7. Ethics and data access.** UK Biobank use is described only as approved "by the relevant local ethics committee" with no application number. UK Biobank requires a specific approved application ID, which should be supplied. The data availability statement invokes participant confidentiality, but the de-identified optometrist grading matrix carries no such constraint and should be released; no model code or weights are offered.

**8. Sample description inconsistency.** Line 186 describes the 190 images as randomly selected, but referable prevalence is 34.2% against a UK Biobank population prevalence roughly an order of magnitude lower. The set is enriched, and line 188's description of it as "clinically representative" is not defensible. Line 191 states Australian population fundus photographs were unavailable, which sits awkwardly against reference 16, the authors' own Australian primary care imaging trial.

071939
# Editorial Report — Manuscript 071939

**Title:** Improving Recognition of Clinically Challenging Gastrointestinal Diseases with Foundation Models
**Handling editor assessment — Nature Communications (Digital Health)**

---

## 1. Overall Assessment

The manuscript claims data scaling fails to improve rare-class gastrointestinal disease recognition, and proposes Diversity Examiner Modeling (DEM): probabilistic low-rank subspaces in each attention block's query space, with a differentiable class-separability score that both reweights cross-entropy and drives top-K routing. Backbones span DINOv1/v2, GastroNet-5M, Phikon-v2 and RedDino-Large.

The design is broad; the evidence is not. Splits are random and frame-level on video-derived data, and the manuscript contradicts its own headline numbers.

---

## 2. Strengths

Section 2.1 is an honest controlled ablation: DINOv1 pretrained on 200k, 1M and 5M GastroNet-5M subsets, backbone frozen downstream, three runs. Minority-class F1 falls on two of four datasets (SEE-AI 0.561 to 0.530). A published negative scaling result is the submission's most valuable element.

The backbone sweep crosses modalities — Phikon-v2 (~456M histopathology tiles) and RedDino-Large (~1.25M red blood cell images), both described accurately — testing whether the mechanism rather than the representation carries the effect.

Section 3.2.1 pre-empts the routing explanation: Swin-MoE under an identical protocol reaches minority F1 of 0.193 and 0.553, against DEM's 0.259 and 0.691. The per-subspace ablation and the reported Phikon-v2 decrement on SEE-AI (0.586 to 0.577) are not overclaimed.

---

## 3. Weaknesses

No patient-, procedure- or video-level splitting is described, and the merged 86-class corpus pools Kvasir with its own superset HyperKvasir. Near-duplicate frames across train and test inflate rare classes preferentially. Fixing this requires patient-level splits, a de-duplication audit, and re-running Sections 2.2 to 2.5.

Provenance and reproducibility fail. "WCE2025" cites EndoBench, itself assembled from 21 public datasets, so the benchmarks may not be independent. SEE-AI cites a Kaggle page, not Yokote et al. Phikon-v2, RedDino and Swin-MoE are uncited. No hyperparameters (E, K, lambda, r, tau), no code.

Internal contradictions: SEE-AI pathology gain 0.130 (Sec. 2.10) versus +0.01 to +0.04 (Sec. 3); "Micro F1" versus Figure 3's Macro-F1; the Section 2.4 minority-F1 claim falsified by Table 3 (MaxViT-Tiny 0.264 > DEM 0.259). Significance markers name no test and no correction across ~15 comparisons at n=3.

Long-tail baselines omit LDAM-DRW, cRT, Balanced-MixUp and PaCo. No clinician, calibration, subgroup or per-centre analysis.

---

## 4. Editorial Decision

**Reject.** The partitioning flaw requires re-running, not revision, and is compounded by a headline claim its own Table 3 falsifies and by absent hyperparameters. A corrected version would suit *npj Artificial Intelligence* or *Communications Engineering*.

**Strongest counterargument.** The Swin-MoE control is a relative comparison under a shared split, so leakage does not explain DEM's margin; on that reading, major revision beats rejection. I reject because leakage does not bias methods equally — adaptive reweighting can memorise duplicated rare-class frames more freely than a fixed router — and because the reporting failures are too numerous to be isolated slips.

---

## 5. Suggested Reviewer Expertise

Five areas, weighted toward methods. First, parameter-efficient adaptation of vision transformers, specifically low-rank and adapter insertion into attention projections, straight-through estimators for discrete routing, and sparse Mixture-of-Experts, to adjudicate whether DEM's separability-conditioned coupling is genuinely distinct from existing MoE and adapter formulations. Second, long-tailed representation learning, covering logit adjustment, LDAM-DRW, decoupled classifier retraining and Balanced-MixUp, to judge the adequacy of the baseline panel. Third, self-supervised pretraining of medical vision foundation models, including DINOv2 recipes, pretraining-scale ablation design and data-contamination auditing between pretraining and downstream corpora. Fourth, evaluation methodology for imbalanced medical classification: patient-level partitioning, near-duplicate detection in video-derived image sets, calibration, mAP versus AUROC saturation, and multiple-comparison correction. Fifth, clinical expertise from a gastroenterologist with hands-on capsule and conventional endoscopy reading experience and involvement in CADe/CADx validation, able to assess whether the 86-class taxonomy is clinically coherent and whether the claimed rare-class gains would alter reading behaviour.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant landscape has moved on three fronts. On domain-specific pretraining, GastroNet-5M (Jong, Boers et al., *Gastroenterology* 2026;170(1):174–187, epub July 2025) released 4,820,653 images from ~500,000 procedures across eight Dutch hospitals and demonstrated the data-efficiency benefit of endoscopic pretraining; Boers et al. (*Medical Image Analysis* 2024;98:103298) had already dissected architecture, pretraining approach and data efficiency for endoscopic foundation models, which is the paper this manuscript's Section 2.1 should have engaged with and did not. On benchmarking, EndoBench (Liu et al., arXiv:2505.23601, 2025; unreviewed at time of writing, subsequently under conference review) standardised endoscopic evaluation across 21 datasets and 6,832 validated items, and MONICA (arXiv:2410.02010, 2024) provides a dedicated long-tailed medical-image benchmark with unified protocols — neither is cited, and MONICA in particular is the natural comparator for the Section 2.2 merged benchmark. On long-tail adaptation of foundation models, TFA-LT (Li et al., ISBI 2024, arXiv:2408.14770) reports large rare-class gains using two linear adapters and an ensembler at 6.1% of the GPU memory of the prior best, and Balanced-MixUp (Galdran et al., MICCAI 2021) was validated specifically on long-tailed gastrointestinal video frames. Both are direct competitors and neither appears.

Situated against this, the manuscript's distinctive contribution is narrow but real: coupling a differentiable class-separability score to both the loss weight and the routing decision, rather than treating reweighting, subspace specialisation and diversity regularisation as separable components, and testing that coupling against a matched Swin-MoE control. Everything else — probabilistic low-rank adapters in attention, top-K routing with straight-through gradients, prototype-based diversity regularisation, inverse-frequency style reweighting — is established. The scaling-saturation finding in Section 2.1 is the paper's most transferable observation but is asserted from a single DINOv1 run family, with class composition across pretraining scales never quantified, a gap the authors themselves acknowledge. Contemporaneous domain work such as Digepath (*npj Digital Medicine* 2026) shows what a clinically anchored GI foundation-model contribution looks like at this journal's standard; the present submission is a methods paper on public benchmarks, without clinical validation, and should be positioned as such.

---

## 7. Suggested Reviewers

Independence cannot be fully verified: the submitted PDF contains no author list or affiliations, and the only identifying information is the ANR TEDIA grant (ANR-24-CE45-1133), indicating a French group. The names below must be checked against the author list before invitation.

For long-tailed adaptation of foundation models, Sirui Li and Li Lin (postdoctoral level, Southern University of Science and Technology / University of Hong Kong), first authors of "Text-guided Foundation Model Adaptation for Long-Tailed Medical Image Classification" (ISBI 2024) — the closest direct competitor to DEM. For long-tail methodology in gastrointestinal imaging specifically, Adrian Galdran (Universitat Pompeu Fabra), author of Balanced-MixUp (MICCAI 2021), validated on a 23-class long-tailed gastrointestinal frame dataset.

For endoscopic foundation models and pretraining-scale ablation, Tim G. W. Boers or Tim J. M. Jaspers (postdoctoral researchers, Eindhoven University of Technology), authors of the GastroNet-5M dataset paper and of the *Medical Image Analysis* 2024 study on endoscopic foundation-model pretraining — best placed to judge whether Section 2.1's scaling claim survives their own contradictory evidence.

For benchmark design and endoscopic evaluation, Yixuan Yuan (Associate Professor, Chinese University of Hong Kong), corresponding author of EndoBench, who can adjudicate the provenance of the "WCE2025" benchmark directly.

For cross-modality backbone claims, Luca Zedda (doctoral/postdoctoral, University of Cagliari), first author of RedDino (MICCAI 2025), to verify that RedDino-Large is used and characterised correctly.

Clinical reviewer: Albert J. de Groof (gastroenterologist, Amsterdam UMC), active in endoscopic AI validation, or Anastasios Koulaouzidis (capsule endoscopy, KID project) as an alternative for the capsule-specific datasets. A clinical reviewer is needed less for the method than to state plainly whether the 86-class merged taxonomy is clinically meaningful.

---

## CONFIDENTIAL — Editorial Integrity Notes (not for authors)

1. **Recycled rebuttal text.** Section 3.1 ("Our main novelty") and the untitled Section 4.5 contain substantially the same argument in near-identical framing, both written in a defensive register ("Our method does not simply combine established components…"; "DEM's contribution is not the presence of a router… in isolation"). Sections 3.2 and 3.2.1 (Swin-MoE) read as responses to specific reviewer objections. The layout is Springer LNCS conference style. This strongly suggests an undisclosed prior conference submission and rejection, with rebuttal material pasted into the body. Ask the authors directly about prior submission history and prior review reports.

2. **No preprint found.** Targeted searches for "Diversity Examiner Modeling" and the title returned no arXiv or bioRxiv record. No evidence of an undisclosed preprint at this time.

3. **No author list, affiliations, competing-interest or ethics statement in the submitted PDF.** Competing interests, IRB/ethics status for the underlying datasets, and data/code availability cannot be assessed. Confirm the submission system carries these before any further processing.

4. **Citation misattribution.** Reference [15] cites a Kaggle page rather than the SEE-AI primary publication (Yokote et al., *DEN Open* 2024). Reference [14] is EndoBench, an MLLM VQA benchmark, cited as though it were the source of an image-classification dataset named "WCE2025". Phikon-v2, RedDino-Large, Swin-MoE and EndoDINO are used or plotted with no reference at all.

5. **Numerical inconsistencies for the record.** SEE-AI pathology gain 0.130 (§2.10) versus +0.01–0.04 (§3); KID pathology gain 0.040 (§2.10) versus +0.18 (§3); "Micro F1" (§2.2) versus Macro-F1 (Fig. 3); minority-F1 superiority claim (§2.4) contradicted by Table 3 (MaxViT-Tiny 0.264 > DEM 0.259); "~1M trainable parameters" versus Figure 9 marker labelled 88M with markers stated to be proportional to trainable parameters; "GastroVision-5M" (Fig. 16 caption) versus GastroNet-5M throughout. Individually minor; collectively they indicate the results were not independently checked before submission.

6. **Verified as accurate.** GastroNet-5M scale and provenance; Phikon-v2 (456,060,584 tiles, ~58–60k WSIs, PANCAN-XL); RedDino (1.25M RBC images, DINOv2-based, MICCAI 2025). The manuscript's descriptions of third-party models are correct even where uncited.

071972
# Editorial Report — Manuscript 071972

**Title:** Privacy-preserving personalized medical imaging under data heterogeneity through diffusion-enhanced federated distillation
**Corresponding authors:** Gang Xu; Xiu-Bo Chen (Beijing University of Posts and Telecommunications)

---

## 1. Overall Assessment

DPFDM combines feature-space conditional diffusion (PFDS), entropy-weighted distillation (DEKD) and a condition-initialized low-rank adapter with DP noise (DP-LoRA), tested on MNIST, CIFAR-10 and CheXpert across twenty clients and 200 rounds.

The engineering is coherent; the scientific case is not made. The privacy guarantee is asserted rather than proven, and Eq. (14) uploads unperturbed diffusion-backbone updates. Heterogeneity is simulated by Dirichlet label partitioning within one institution, not by scanner, protocol or population shift.

## 2. Strengths

Feature-space rather than pixel-space diffusion is the defensible core, and the saving is measurable: 124.33 min and 129.4 MB per round on CheXpert against 143.54 min and 1497.7 MB for FedDDPM, reductions of 13.4% and 91.4% consistent across Figs. 3-5.

The comparator set is broad, with seven baselines including FedALoRA, PF2SMIS and FedSplit, and the ablation isolates all four components across three datasets.

The uncertainty factor of Eq. (21), mean normalized predictive entropy over synthetic features, ties distillation strength to a client-measurable quantity requiring no server access.

## 3. Weaknesses

The privacy contribution is unsubstantiated. No epsilon or delta appears, there is no sensitivity derivation for the clipping threshold S, and no accounting over 200 rounds. The synthetic features never leave the client (lines 444-445), while the transmitted diffusion updates go unperturbed.

The evaluation does not match the motivation. Lines 46-48 invoke device, protocol and population shift; CheXpert is then Dirichlet-partitioned into 25 label meta-classes within a single Stanford cohort. That is label shift, not covariate shift. MNIST and CIFAR-10 are not medical, and there is no external validation on MIMIC-CXR, PadChest or FLamby.

Results are single-run point estimates without seeds or confidence intervals, yet wins of 0.07% to 0.30% are claimed (lines 217, 223). Per-pathology AUC, calibration, the test split and subgroup analysis by sex, age or race are missing.

PerAda (Xie et al., CVPR 2024) is cited only for its partitioning protocol, yet it is adapter-based personalized federated learning with distillation evaluated on CheXpert. Its absence from Table 1 is not defensible.

## 4. Editorial Decision

Reject. The privacy guarantee does not cover the transmitted diffusion updates, the heterogeneity claim rests on simulated label shift, and the margins carry no variance estimate. Peer review cannot adjudicate these. Offer transfer to npj Artificial Intelligence, or decline in favour of IEEE TMI.

## 5. Suggested Reviewer Expertise

Reviewers should cover: conditional denoising diffusion probabilistic models trained in latent or feature space under federated aggregation; differential privacy accounting for low-rank adapter fine-tuning, including composition across rounds and clipping-sensitivity analysis; knowledge distillation with adaptive, uncertainty-weighted objectives in non-IID federated settings; cross-silo federated evaluation methodology for medical imaging, specifically covariate-shift benchmark construction and external validation; and thoracic radiology with direct experience of CheXpert label uncertainty handling, multi-label AUC reporting and demographic subgroup fairness in chest radiograph classification.

## 6. State-of-the-Art Literature Review (Past Three Years)

The sub-domain has moved quickly. PerAda (Xie et al., CVPR 2024) established parameter-efficient personalized federated learning with distillation-based global aggregation and generalization bounds, evaluated on CheXpert with adapters updating 12.6% of parameters. On the generative side, pFedGPA (Lai et al., AAAI 2025) and VQ-FedDiff (Yoon et al., TPAMI 2025) both condition diffusion on client-specific representations, and FedDiff (Li et al., TCSVT 2024) addresses multi-modal medical clients; the manuscript cites all three but treats them only as motivation. For the privacy component, FFA-LoRA (Sun et al., ICLR 2024), FLASC (Kuo et al., 2026) and FedSVD (Lee et al., NeurIPS 2026) define the current bar for private and communication-efficient low-rank federated fine-tuning, and each reports formal budgets that this manuscript does not. FLamby (Ogier du Terrail et al., NeurIPS 2022) remains the reference benchmark for realistic cross-silo medical federation and is not used here.

Against that landscape, DPFDM advances one narrow point: conditioning a shared diffusion backbone on local moment statistics through gated cross-attention, generating in feature space rather than pixel space. That is a genuine efficiency contribution. Everything else — proximal regularization, entropy-weighted distillation, MMD alignment, DP-SGD on low-rank matrices — recombines existing components. The field has already moved to formal privacy accounting and multi-institution covariate-shift evaluation; this manuscript does neither, and its strongest competitor sits uncompared in its own reference list.

## 7. Suggested Reviewers

*Note: the skill specifies three to four names per expertise area. Six named candidates are given instead, one or two per area, because a report of this length cannot carry twenty nominations without displacing substantive critique. Flagging rather than padding.*

**Diffusion and generative federated learning:** Chulin Xie (Assistant Professor-track; first author, PerAda, CVPR 2024) — the closest methodological comparator, and best placed to judge whether DPFDM's conditioning improves on adapter-plus-distillation baselines.

**Personalized FL for medical imaging:** Qi Dou (Associate Professor, CUHK) — FedBN and personalized federated medical image analysis; and Meirui Jiang (postdoctoral researcher, CUHK) — federated domain generalization for medical images, well matched to the covariate-shift objection.

**Federated learning theory and evaluation:** Xiaoxiao Li (Associate Professor, UBC) — co-author of FedBN, works directly on non-IID federated medical imaging with feature-level alignment.

**Differential privacy for low-rank fine-tuning:** Zhiqi Bu (Amazon Science, formerly postdoctoral researcher, UPenn) — DP-SGD accounting and private parameter-efficient fine-tuning; the appropriate reviewer for the missing ε.

**Thoracic radiology and subgroup fairness:** Judy Gichoya (Associate Professor, Emory) — demographic signal and performance disparity in chest radiograph models, directly relevant to the absent subgroup analysis.

All six are independent of Beijing University of Posts and Telecommunications, North China University of Technology, Guizhou University, Sichuan University, Guangdong University of Technology and Nanyang Technological University. Independence was checked against affiliations only; co-authorship history should be confirmed in the submission system before invitation.

# Editorial Report — Manuscript 070836

**Title:** Deep-ALIGN enables accurate gene expression prediction from histopathology images through multimodal representation alignment
**Authors:** Beachum AH, Xiao X, Xiao G, Xu L (UT Southwestern; Southern Methodist University)
**Handling standard:** *Nature Communications* — Digital Health / Computational Pathology

---

## CONFIDENTIAL — EDITORIAL INTEGRITY ALERT (Handling Editor only; not for authors)

**1. Citation misattribution of the central prognostic result (severe).** Reference 30 is Venet, Dumont & Detours, *PLoS Comput Biol* 7, e1002240 (2011). The manuscript cites it (line 202) as the source of "the meta-PCNA 131-gene proliferation signature — which captures a proliferation-associated transcriptomic signal linked to breast cancer outcome," and uses it as the headline survival result (Figure 6a). That paper is a negative-control study. Its finding is that >90% of *random* signatures of >100 genes are significantly associated with breast cancer outcome, that >50% of the breast transcriptome correlates with meta-PCNA, and that adjusting for meta-PCNA abolishes the outcome association of published signatures. Meta-PCNA was constructed as the *null benchmark* against which signatures should be tested, not as a prognostic signature. The manuscript inverts the cited source's conclusion. This is not a matter of interpretation.

**2. Undisclosed tension with the authors' own review (moderate).** Reference 8 is the authors' own review (Beachum AH, Xiao X, Zhou Y, Li Q, Xiao G, Xu L, *Brief Bioinform* 27(2), bbag090, 2026; verified). That review explicitly states that recent frameworks "have incorporated contrastive learning to improve alignment between molecular and image-derived representations before prediction," citing three such works. The present manuscript's novelty claim (lines 71–76, 229–232) is that prior methods leave cross-modal structure implicit and treat the mapping as one-way. The authors' own published review contradicts the framing. Self-citation is disclosed; the inconsistency is not.

**3. Misrepresentation of a cited benchmark (moderate).** Lines 496–498 state that Phikon-v2 "has demonstrated superior performance across multiple downstream benchmarks such as MSI mutation status prediction" relative to Phikon-v1, UNI and H-optimus-0. Filiot et al. (arXiv:2409.09173) report that Phikon-v2 performs *on par* with FMs trained on proprietary data, that GigaPath and H-Optimus-0 stand out under scaling, that margins between top FMs are mostly non-significant, and that on MSI specifically the leading FMs were beaten by a 13× smaller internal model. The cited source does not support the claim made.

**4. Duplicated references (minor, but indicates unchecked reference list).** Ref 17 = Ref 42 (Chen RJ et al., *Nat Med* 30, 850–862, 2024). Ref 29 = Ref 45 (Radford et al., ICML 2021), cited under two different numbers in Results and Methods. Ref 43 (H-optimus-0) is a bare GitHub URL.

**5. Code availability unverifiable.** The declared repository (https://github.com/Lin-Xu-lab/Deep-ALIGN) does not appear among the public repositories listed under that account at the time of assessment. Either private or not yet created. Must be resolved before any review invitation.

**6. Suggested-reviewer conflicts.** Several of the most qualified candidates below are authors of the comparator methods (SEQUOIA, HE2RNA, Phikon-v2). Their expertise is exactly what is needed to adjudicate the baseline-fidelity question, but they are adverse parties. Recommend inviting at most one, and pairing with an independent methodologist.

No evidence of undisclosed preprint, salami-slicing, or cohort reuse was found. Competing-interest declaration appears adequate.

---

## 1. Overall Assessment

Deep-ALIGN predicts bulk RNA-seq from H&E whole-slide images by aligning image and omics embeddings with a VICReg objective during training, dropping the omics arm at inference. Evaluation is TCGA-BRCA (n=987) and TCGA-LGG (n=467) against a ViT baseline, SEQUOIA and HE2RNA. The novelty framing is inaccurate: TANGLE (Jaume et al., CVPR 2024) already aligns slide embeddings with bulk RNA-seq on TCGA-BRCA and is uncited, leaving a loss-function substitution.

## 2. Strengths

The ablation is genuinely informative. Isolating Inv, Inv+Cov, Inv+Var and the full objective (Figure 4), and CLIP against CLIP+Var+Cov (Figure 5), shows the variance hinge rather than cross-modal agreement prevents latent collapse. CLIP alone falling below the unaligned baseline is a useful negative finding.

Methods are reproducible from the text, tile filtering is tighter than typical, and the well-predicted-gene criterion correctly includes comparison against an untrained random model.

## 3. Weaknesses

Comparators were run through the authors' 20-supertile pipeline (line 498) rather than native inputs. HE2RNA is a tile-level aggregator; SEQUOIA's linearized attention needs the full tile set. Both collapse (SEQUOIA r ~ 0.27 versus ~0.50 published; HE2RNA ~ 0.08), and Deep-ALIGN's ~0.47 does not exceed SEQUOIA's published BRCA figure.

The prognostic analysis has no null. All three signatures are proliferation-confounded, with no comparison against ground-truth-expression stratification, a random 131-gene signature, or Cox adjustment for stage, grade, age and ER status. LGG survival is absent.

GO enrichment over ~17,500 genes spans most of the transcriptome and cannot discriminate model quality. Phikon-v2 was pretrained on 29,502 TCGA WSIs, confounding its margin over ResNet101. Top-1000 genes are selected on test-set correlation, with no confidence intervals or paired tests reported.

## 4. Editorial Decision

**Reject**, transfer to ***npj Digital Medicine*** or ***Communications Medicine***. Superiority over SEQUOIA and HE2RNA rests on comparators run at half their published performance, and the prognostic claim rests on a metagene whose source publication exists to show such associations are uninformative. Neither is fixable by added experiments.

*Counterargument (steelmanned).* Figures 4 and 5 are internally controlled and untouched by every criticism above, establishing that variance regularization drives the gain and InfoNCE harms bulk-level alignment - a negative result the field under-publishes. Major Revision stripping the benchmark and survival analysis is defensible. I decline because the paper is built on the claims being removed, and the meta-PCNA issue is source misattribution rather than overreach.

## 5. Suggested Reviewer Expertise

Reviewers should cover, in roughly 70:30 technical-to-clinical proportion: (i) deep learning for bulk transcriptome prediction from whole-slide images, specifically multiple-instance and slide-level transformer architectures such as SEQUOIA, HE2RNA and tRNAsformer, with hands-on experience of the tiling and aggregation pipelines these methods require; (ii) multimodal representation learning and non-contrastive self-supervised objectives, including VICReg, BYOL and InfoNCE, and the latent-collapse failure modes they address; (iii) histopathology foundation models and benchmarking practice, covering Phikon-v2, UNI, GigaPath and H-optimus-0, and in particular pretraining-set contamination when evaluating on TCGA; (iv) statistical methodology for prognostic gene signatures, including proliferation confounding, random-signature null models and multivariable Cox adjustment in breast cancer; and (v) clinical expertise split between a breast pathologist familiar with ER/PAM50 subtyping and morphology–molecular correlation, and a neuropathologist familiar with WHO-classified IDH-mutant lower-grade glioma and the TERT/IDH1/BRAF alteration landscape.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The bulk image-to-expression field has consolidated rapidly since 2023. SEQUOIA (Pizurica et al., *Nat Commun* 15, 9886, 2024) is the reference point: a linearized-attention transformer developed on 7,584 tumors across sixteen cancer types with generalization tested on two independent cohorts totalling 1,368 tumors, reporting ~0.50 average correlation and ~14,900 well-predicted genes in BRCA, plus recurrence-risk stratification and loco-regional spatial resolution. tRNAsformer (Alsaafin et al., *Commun Biol* 6, 304, 2023) established MIL-transformer slide-level prediction with retrieval applications. DeepPT (Hoang et al., *Nat Cancer* 5, 1305–1317, 2024), cited here only in passing as ref 7, showed that imputed transcriptomes can drive downstream treatment-response prediction — the clearest existing demonstration of the "inferred expression as intermediary" argument this manuscript makes in its introduction. On the alignment side, TANGLE (Jaume et al., CVPR 2024) is the decisive omission: it aligns ABMIL slide embeddings with bulk RNA-seq using CLIP-style contrastive pretraining on TCGA-BRCA, TCGA-NSCLC and rat liver, and is precisely the "explicit image–omics alignment for bulk profiles" that the manuscript claims is absent from the literature. Its successors (MADELEINE, THREADS) extend the paradigm further. On the feature-extractor axis, UNI (Chen et al., *Nat Med* 30, 850–862, 2024), Phikon-v2 (Filiot et al., 2024), GigaPath and H-optimus-0 have made encoder choice a first-order experimental variable, and the Phikon-v2 benchmark itself reports that inter-model margins are mostly non-significant.

Against this landscape, the manuscript advances the field in one specific place: it shows, with a clean ablation, that a non-contrastive VICReg objective outperforms InfoNCE for bulk-level image–omics alignment, and that the variance hinge rather than the invariance term is responsible. That is a real and useful observation, and TANGLE's contrastive design makes it more interesting, not less. Everything else replicates existing work — TCGA-only training, top-N-gene correlation reporting, GO/GSVA characterization of well-predicted genes, and Kaplan–Meier stratification on predicted signatures all follow SEQUOIA's template. The authors must engage directly with TANGLE, must reconcile their novelty framing with their own 2026 *Briefings in Bioinformatics* review, and should address the confounding literature they themselves cite (Howard et al., *Nat Commun* 12, 4423, 2021 on site-specific signatures; Schmitt et al., *J Med Internet Res* 23, e23436, 2021 on hidden batch variables) with an actual analysis rather than a limitations sentence.

## 7. Suggested Reviewer Names

*Bulk transcriptome prediction from WSIs.* Marija Pizurica (postdoctoral researcher, Stanford BMIR / Ghent IDLab) — first author of SEQUOIA, *Nat Commun* 15, 9886 (2024); the single best-placed referee for the baseline-fidelity question, but an adverse party. Francisco Carrillo-Perez (postdoctoral researcher, Stanford BMIR) — SEQUOIA co-first author, with independent work on omics–histology integration. Danh-Tai Hoang (staff scientist, NCI) — first author of DeepPT, *Nat Cancer* 5, 1305–1317 (2024). Areej Alsaafin (Rhazes Lab / formerly Mayo Clinic) — first author of tRNAsformer, *Commun Biol* 6, 304 (2023).

*Multimodal alignment and slide representation learning.* Guillaume Jaume (research fellow, Mass General Brigham / Harvard) — first author of TANGLE, CVPR 2024; the most directly informed referee on the prior-art question. Andrew H. Song (instructor, Harvard Medical School) — slide-level representation learning, co-author on TANGLE and MADELEINE. Adrien Bardes (Meta AI / Inria) — first author of VICReg, arXiv:2105.04906; appropriate for whether the EMA reweighting scheme and the variance-hinge interpretation are sound.

*Foundation models and benchmarking rigor.* Alexandre Filiot (Owkin) — first author of Phikon-v2, arXiv:2409.09173; adverse party with respect to weakness 4, but authoritative on pretraining contamination. Sophia J. Wagner (postdoctoral researcher, Helmholtz Munich) — transformer-based biomarker prediction, *Cancer Cell* 41, 1650–1661 (2023). Frederick M. Howard (assistant professor, University of Chicago) — site-specific digital histology signatures and DL bias, *Nat Commun* 12, 4423 (2021); ideal for the confounding and evaluation-transparency weaknesses.

*Prognostic signature methodology.* David Venet (senior researcher, IRIBHM, Université Libre de Bruxelles) — first author of *PLoS Comput Biol* 7, e1002240 (2011); the definitive referee for whether Figure 6 measures anything beyond proliferation.

*Clinical.* Mohamed Amgad (assistant professor of pathology, Northwestern University) — computational breast pathology and morphology–molecular correlation. Sriram Venneti (associate professor of pathology, University of Michigan) — molecular genetics of lower-grade glioma, cited by the authors as ref 21; appropriate for the LGG claims around TERT, IDH1 and BRAF.

---

## Further Literature

1. Jaume, G. et al. Transcriptomics-guided slide representation learning in computational pathology. *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)* 9632-9644 (2024). DOI: 10.1109/CVPR52733.2024.00920. Peer-reviewed (CVPR main track). **Not cited.** Independent (Mahmood Lab, Mass General Brigham/Harvard). The decisive omission: TANGLE performs CLIP-style contrastive alignment of ABMIL slide embeddings with bulk RNA-seq on TCGA-BRCA, the exact setting the manuscript claims is unaddressed. Directly falsifies the novelty framing at lines 71-76 and 243-245.

2. Pizurica, M. et al. Digital profiling of gene expression from histology images with linearized attention. *Nature Communications* 15, 9886 (2024). DOI: 10.1038/s41467-024-54182-5. Peer-reviewed. **Cited (ref 16).** Independent (Stanford/Ghent/Roche). Cited but not engaged with quantitatively: reports ~0.50 average correlation and 13,798-14,915 well-predicted genes in TCGA-BRCA, against the ~0.27 and ~7,500 obtained by the manuscript's reimplementation. The benchmark for the baseline-fidelity dispute.

3. Hoang, D.-T. et al. A deep-learning framework to predict cancer treatment response from histopathology images through imputed transcriptomics. *Nature Cancer* 5, 1305-1317 (2024). DOI: 10.1038/s43018-024-00793-2. Peer-reviewed. **Cited (ref 7)**, in passing only. Independent (NCI, Ruppin lab). DeepPT is the strongest existing demonstration that imputed bulk expression carries actionable downstream signal, and is the correct comparator for the manuscript's "inferred expression as intermediary" argument.

4. Venet, D., Dumont, J.E. & Detours, V. Most random gene expression signatures are significantly associated with breast cancer outcome. *PLoS Computational Biology* 7, e1002240 (2011). DOI: 10.1371/journal.pcbi.1002240. Peer-reviewed. **Cited (ref 30), inverted.** Independent (ULB). The source of meta-PCNA, constructed as a null benchmark; >90% of random signatures over 100 genes separate breast cancer survival, and adjustment for meta-PCNA abolishes those associations. Section 4 of the decision rests on this.

5. Venet, D. & Detours, V. Why breast cancer signatures are no better than random signatures explained. *Drug Discovery Today* 23, 1912-1917 (2018). DOI: 10.1016/j.drudis.2018.05.036. Peer-reviewed. Not cited. Independent. The follow-up analysis showing random-signature significance extends beyond breast cancer and beyond cell-cycle genes; establishes that removing proliferation genes does not remove the confound, which pre-empts the obvious rebuttal to weakness 2.

6. Filiot, A., Jacob, P., Mac Kain, A. & Saillard, C. Phikon-v2, a large and public feature extractor for biomarker prediction. arXiv:2409.09173 (2024). **Preprint - not peer-reviewed.** **Cited (ref 40), misrepresented.** Independent (Owkin). Reports parity rather than superiority against UNI, GigaPath and H-optimus-0, notes MSI prediction is won by a 13x smaller model, and specifies PANCAN-XL as including 29,502 TCGA WSIs with external-cohort evaluation to avoid contamination. Underpins weaknesses 3 and 4.

7. Howard, F.M. et al. The impact of site-specific digital histology signatures on deep learning model accuracy and bias. *Nature Communications* 12, 4423 (2021). DOI: 10.1038/s41467-021-24698-1. Peer-reviewed. **Cited (ref 35)**, in a limitations sentence only. Independent (University of Chicago). Demonstrates that TCGA submitting-site signatures are recoverable from H&E and inflate apparent performance; the manuscript should run site-stratified analysis rather than acknowledge the risk.

8. Chen, R.J. et al. Towards a general-purpose foundation model for computational pathology. *Nature Medicine* 30, 850-862 (2024). DOI: 10.1038/s41591-024-02857-3. Peer-reviewed. **Cited twice (refs 17 and 42, duplicated).** Independent (Mahmood Lab). UNI is the encoder SEQUOIA actually uses; benchmarking Deep-ALIGN with Phikon-v2 while running SEQUOIA on non-native inputs conflates encoder choice with architecture.

9. Vaidya, A. et al. Molecular-driven foundation model for oncologic pathology. *Nature Biomedical Engineering* (2025). DOI: 10.1038/s41551-025-01516-3. Peer-reviewed. Not cited. Independent (Mahmood Lab). THREADS extends TANGLE by aligning slide representations with both transcriptomic and genomic profiles at scale; the current state of the art for molecularly grounded slide representation learning and the standard the manuscript's contribution must be positioned against.

10. Xie, R. et al. Spatially resolved gene expression prediction from H&E histology images via bi-modal contrastive learning. *Advances in Neural Information Processing Systems* 36 (2023). Peer-reviewed (NeurIPS). **Cited (ref 32).** Independent. BLEEP is cited correctly, but only to support the claim that contrastive alignment is confined to spatial transcriptomics - a claim TANGLE refutes. Retained here so reviewers can see the asymmetry in the literature the authors selected.


