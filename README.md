# Trackrad202512456

024751
**Reviewer 1 — Qingyu Chen (Assistant Professor, did not review code):**
Four core objections. (1) SFT on ~2.8M dialogue pairs yields a trivial 0.72→0.73 MedQA gain — doesn't justify the claimed knowledge-base contribution. (2) The DPO stage is mislabeled: "preferred" responses are just gold-standard multiple-choice answers, not model-sampled or human-preference data, so this is supervised contrastive fine-tuning dressed up as DPO. (3) Undisclosed contamination risk — SFT corpus (huatuo_knowledge_graph_qa, DISC-Med-SFT, UltraMedical) overlaps in domain/format with the evaluation benchmarks; no leakage analysis given. (4) RAG, multi-agent orchestration, and image-based risk assessment are claimed as central contributions but are essentially unvalidated: no retrieval ablation, no retrieval-quality metrics, and the image classifier is tested on 10 images/category (n=40 total) with AUC/F1 reported to four significant figures — statistically indefensible. Conclusion: central claims not supported by the evidence presented.

**Reviewer 2 — Nancy Guo (Professor, reviewed code):**
Three points, one of them severe. (1) Reported alignment gains are modest and not contextualized clinically. (2) The 20 quantitative risk-stratification models (including image-based ones) lack methodological detail — no clear description of architectures, train/test splits, or protocols. (3) Critically: after checking the GitHub repo, she could not find the code for the risk-stratification models at all, and flags that some reported model results appear to be hardcoded. That is not a "needs more detail" complaint — that's a reproducibility failure bordering on a data-integrity concern.

**Decision: Reject.**
Both reviewers, independently, converge on the same failure mode: the manuscript's headline contributions (DPO alignment, RAG, multi-agent orchestration, image/risk stratification) are asserted, not demonstrated. R1's statistical objections (n=40 test sets reported to 4 sig figs, no contamination check, mislabeled DPO) are individually disqualifying for a Nature Communications-tier claim. R2's finding — missing code plus possibly hardcoded results for a model class presented as a central contribution — is not a "major revision" problem; you cannot ask authors to revise their way out of an unverifiable results table. Reject rather than major revision.

**Pushback on my own call:** the counterargument for major revision is that none of these are conceptually fatal — a real DPO implementation, a retrieval ablation, expanded image test sets, and released code could in principle fix all four objections without changing the paper's core architecture. If you think the authors are credible and G-Health's clinical framing is genuinely valuable, major revision with a hard requirement to supply verifiable code and hold out a contamination-checked test set is defensible.

**What you're not asking but should be:** the hardcoded-results finding is a research-integrity flag, not just a peer-review weakness. Standard editorial practice is to route that specific finding to your integrity/ethics process separately from the accept/reject decision — a "reject and resubmit" doesn't require you to formally note the concern, but it should be logged, because if the same group resubmits elsewhere the hardcoding question needs to travel with the manuscript.

037297
**Reviewer 1 (Reiss, neonatology) — 11 numbered points, no explicit accept/reject.** Core theme is unaddressed confounding: gestational age (GA) is a known dominant driver of RD/RDS risk (his own citation of GAD-alone AUC 0.7–0.9), and Table 4 suggests all RD cases cluster in younger-GA infants — meaning the model may be re-deriving a GA correlation rather than detecting an independent EV signal. He also flags a clinically incoherent outcome definition (RD 30% vs. confirmed RDS 3%, undefined overlap with TTN/pneumonia/sepsis), missing confounders (steroids, chorioamnionitis, diabetes, hypertensive disorders, TTTS/TAPS, monoamniotic status), and a CNN trained on ~100 pregnancies as architecturally excessive for the sample size.

**Reviewer 2 (Im, EV/SERS methodology) — explicit reject, states it is "unlikely to be addressable by a revision."** Three fundamental objections: (1) pseudoreplication — many spectra per sample are technical subsamples of one biological specimen, not independent observations, so the effective n is far smaller than reported; (2) no biological validation that SERS signal is RD-specific — SHAP attributions map to generic protein/lipid Raman bands, not RD-relevant biology; (3) same cohort used for training and validation in both steps, with no independent test set, plus unexplained numerical mismatches in Fig. 3 and missing sample-prep detail (drying, capture, why 100 spectra).

**Decision: Reject, not revision.**

The two reports converge on the same failure mode from different angles — Reiss shows the signal is plausibly explained by GA confounding; Im shows there's no held-out validation to rule that out, and no molecular evidence the SERS signal is even RD-specific rather than generic EV/protein content. That combination isn't a "add an analysis" fix — it requires an independent validation cohort that doesn't exist and biological orthogonal confirmation (e.g., targeted proteomics/miRNA on the same EVs) that wasn't done. Per the skill's own standard, a major revision should not be requested when the flaw is foundational rather than presentational; this is foundational.

**Counterargument, steelmanned.** The handling editor (Eric Wang, circulation notes) argued the opposite: prospective design, GA-matched twin pairs as a strong internal control for confounding, appropriate ethics approval, and a genuine domain extension from the group's prior oncology SERS-EV work (Shin et al., Nat Commun 2023) — he sent it to review on that basis. If you weight "twin design controls for GA/maternal environment" heavily, Reiss's confounding critique is partially blunted (discordant outcomes in genetically/environmentally matched twins is a real strength), and one could argue for major revision demanding an independent test split, a stratified-by-GA sensitivity analysis, and biological validation. I don't find this fully persuasive — the twin design controls for shared exposures, not for the GA-at-delivery differences within twin pairs that Table 4 shows tracking with RD — but it's the strongest case against my Reject call, and if Yuli wants to give the authors a path forward rather than close it, this is the opening to use.

**Blind spot you didn't ask about but should flag:** neither referee raised it, but Eric Wang's internal note states corresponding author Yeonho Choi holds a position at EXoPERT and co-author Hyunku Shin is its CTO — the same company supplying the dSEC kit and SERS substrate used in the study — with no disclosure statement in the manuscript. That's an undisclosed competing interest tied directly to the reagents generating the primary data. Independent of the scientific decision, this needs to go in the decision letter as a required disclosure/COI correction, and if Yuli is drafting the letter, it should be stated as non-negotiable rather than folded into the general weaknesses list.

029177
**Reviewer 1 (Xia)** — favorable but exacting. Calls the work "substantial and solid" but pushes back hard on framing: "verifiable reasoning" is oversold when the `<search>` pathway is mediated by a separate Qwen-3-235B summarizer rather than preserving raw evidence, and the reward terms (token overlap, string similarity) are heuristic proxies, not verification. He also flags that the system's heavy structured prompting (Supp. A.1) makes it hard to know how much of the gain is RL versus workflow engineering, and that the 31.78s/4×H200 inference cost needs an explicit deployment discussion. Net: real science, language needs walking back. Major revision.

**Reviewer 2 (Zheng)** — the most positive of the three, "methodologically sound." Wants the common/rare disease framing motivated upfront, a comparison against DeepRare, more discussion of inference-cost tradeoffs, and elaboration on the "debatable ground truth" cases where model output disagreed with labels but looked clinically defensible. All fixable without new experiments. Minor-to-moderate revision.

**Reviewer 3 (Zhu)** — the outlier, and the one that matters most. He argues the paper doesn't clear the novelty bar at all: no new RL algorithm, credit-assignment method, or stopping mechanism relative to existing search agents (Search-R1, R1-Searcher, ReSearch, DeepResearcher), and no baseline comparison against them under matched conditions. He also raises three points that are substantive, not stylistic: (1) the reward design measures whether the correct label surfaces in retrieval, not whether retrieved evidence is actually valid — a straightforward reward-hacking vector; (2) "end-to-end" is inaccurate since retrievers, indexes, and the summarizer are frozen, not jointly trained with the policy; (3) meaningful leakage risk between the patient-retrieval corpus and eval sets (MIMIC-IV, PMC-Patients, RareArena, RareBench all share lineage), unresolved by embedding-threshold dedup alone. He buries the most damaging finding in his minor comments: the rare-disease Top-1 numbers in the text (52.5/34.0/29.4%) don't match Figure 2 (46.05/16.74/14.70%). That's not a typo-tier issue — it's an internal contradiction in the paper's headline result, and it should have been listed as major.

**Decision: Major Revision, not Reject — but conditional, and the bar should be set by Reviewer 3, not averaged against him.** Two of three reviewers see a real, if overclaimed, contribution; nothing here is fatally unfixable in the sense of "wrong idea." But the leakage audit, the matched-baseline comparison against other RL search agents, and the text/figure numerical discrepancy are gating items — if any of those don't resolve cleanly, this becomes a reject, not a second revision cycle. I'd tell the editor to make that explicit in the decision letter rather than treat it as one bullet among many.

**Strongest counterargument to that call:** you could reasonably reject now. A paper whose central quantitative claim doesn't match its own figure, combined with unresolved leakage between train and eval populations, means you don't currently know whether the reported gains are real. Sending that out for another round assumes good faith on numbers you can't yet trust.

**What the file itself half-buries:** Eric and Elena's circulation notes already lean toward giving this "benefit of doubt" before fully reckoning with Zhu's leakage and numerics points — worth flagging to whoever finalizes the letter, since 2-1 reviewer sentiment shouldn't outvote a correctness problem.

041116
**Reviewer 1 — Syeda-Mahmood (skeptical):** Calls the study "inconclusive." Core objection: the AI module has three subsystems (triage, DETR-based slice selection, segmentation/classification), but only the third was evaluated — errors attributable to the first two are invisible. DETR is known to be weak on small/high-frequency-boundary objects, which plausibly explains poor Dice scores, but this isn't discussed. Also flags: absence findings never evaluated (so true sensitivity/specificity is unknown, only positive-finding metrics reported), MRMC dataset doubles as the test set (no independent holdout), per-finding thresholds introduce undisclosed bias, and correction/annotation methodology is unspecified. No code provided.

**Reviewer 2 — Samuelson (favorable, technical):** Calls it well-written and novel in scope. Concerns are narrower and fixable: unclear whether readers (not just cases) were bootstrapped for CIs; precision/PPV are prevalence-dependent and the dataset was enriched for positives (authors should caveat this); balanced accuracy is threshold-dependent and a detectability metric (d′) would be more principled; unclear if Benjamini-Hochberg correction was applied to *all* subgroup comparisons; TPF/TNF operating-point data are described but never reported, which blocks comparison of standalone vs. aided vs. unaided rates.

**Reviewer 3 — Yi (mixed, leaning negative):** Praises the premise (large commercial multi-finding MRMC study) but states outright he's "ambivalent" whether the gaps are fixable in revision and that he'd "expect more" from Nat Comms. Major issues: no disease prevalence/severity reported anywhere; radiologist qualifications and board-certification status undisclosed; no rationale for the 0.8 AUROC threshold or for why only 17/47 findings got instance-level analysis; no p-values for aided-vs-unaided comparisons (inconsistent with how lung nodule results *are* reported); subgroup analysis done only for standalone AI, not for aided/unaided readers, which misses whether AI assistance amplifies hidden stratification; zero human-computer-interaction evaluation despite this being a deployment-facing paper; Discussion recapitulates numbers instead of engaging prior literature.

**Cross-cutting pattern:** All three converge independently on the same failure mode — the manuscript reports impressive topline numbers while withholding the granular data (per-finding TPF/TNF, p-values, prevalence, instance-level rationale) needed to verify them. That's not three unrelated nitpicks; it's a transparency problem running through the whole results section.

**Decision: Major Revision**, not reject. Reasoning: none of the three reviewers identifies a flaw that is *structurally* unfixable — missing prevalence tables, missing p-values, missing rationale for thresholds, and missing subgroup breakdowns are all things the authors already have data for and simply didn't report. Reviewer 3's "ambivalence" is about volume of gaps, not a specific irreparable defect. Mandatory items for the authors: (1) report TPF/TNF and p-values for all comparisons, matching the lung nodule reporting standard; (2) disclose case-selection/exclusion rationale and disease prevalence/severity; (3) clarify whether the MRMC evaluation set is identical to the test set, and if so address the circularity concern directly rather than ignoring it; (4) extend subgroup analysis to aided/unaided readers; (5) explain the three non-inferiority failures, including the critical endobronchial-nodule miss, in regulatory terms.

**Counterargument I'd push back on myself with:** the strongest case for outright Reject is that the MRMC-set-equals-test-set issue (R1) plus the reader pool being entirely Vietnamese radiologists validating a device deployed in Western markets is a *design* flaw, not a *reporting* flaw — you can't fix a non-independent test set or a non-representative reader cohort by adding a table in revision; it requires new data collection. If Elena/the handling editor weighs that as disqualifying rather than as a limitation to be disclosed, Reject is defensible and arguably the more rigorous call.

**Blind spot worth flagging:** none of the three formal reviews mention author conflict of interest, but it's material here — most authors are apparently affiliated with the company selling the AI module, and there's no independent data-access or reanalysis provision. If you're drafting the rationale letter, I'd add a COI/independent-verification requirement as a condition of revision even though the reviewers didn't ask for it — a Nat Comms decision letter that stays silent on this while the reviewers debate p-values would look like an omission later.

058611
# Editorial Report: "An Intelligent Post-Cataract Surgery Follow-Up System Integrating Active Learning and Uncertainty Estimation" (CATALYST)

## 1. Overall Assessment

The manuscript presents CATALYST, a ResNet50-based system that classifies ten postoperative states (nine complications plus normal status) from slit-lamp images, combining pool-based active learning with a Dirichlet-based evidential uncertainty module to flag low-confidence predictions for ophthalmologist review. The central claim is that this dual-uncertainty framework improves both accuracy and cross-center generalizability relative to a deterministic baseline, evidenced by a rise from 72.45%/59.08% (internal/external) baseline accuracy to 80.08%/79.08% after both modules and threshold optimization.

The clinical problem is real and the multicenter validation is genuinely more rigorous than most single-site cataract AI papers. However, the methodological core is largely borrowed rather than new: the uncertainty module reuses the exact Dirichlet-evidential framework and L_TUN loss of Wang et al.'s UIOS system (ref. 24), which the authors themselves use as their principal comparator, and the active learning-plus-evidential-uncertainty combination itself is not novel at the framework level. This raises the central question the decision below turns on: is the contribution a genuine methodological advance or a competent domain transfer of an existing technique to a new clinical task?

## 2. Strengths

The external validation design is a real strength. Testing on 1,465 images from three institutions never seen during development, and showing that the ablated baseline degrades sharply out-of-domain (72.45%→59.08% accuracy) while CATALYST holds stable (80.08%→79.08%), is the kind of evidence that AI-in-ophthalmology papers frequently omit.

The ablation strategy is thorough. Isolating active learning (ResNet50_AL) and uncertainty estimation (ResNet50_UE) individually before combining them, and repeating the entire ablation across DenseNet121 and ViT-B backbones with p<0.001 significance testing, demonstrates the gains are attributable to the modules rather than to a particular architecture.

The parameter search for active learning is transparent and reproducible: five sampling ratios and four uncertainty-sampling strategies (largest margin, smallest margin, least confidence, maximum entropy) were compared against random sampling, with the largest-margin strategy and 90% sampling ratio selected on principled, stated grounds rather than post hoc.

## 3. Weaknesses

The claimed methodological novelty does not hold up under prior-art scrutiny. The Dirichlet evidential uncertainty module is a direct application of Sensoy-style evidential deep learning as operationalized in Wang et al.'s UIOS (Nat. Biomed. Eng. lineage), and the combination of evidential uncertainty with active learning was already established by Hemmer et al.'s DEAL (2022) and extended to medical imaging with explicit domain-shift handling by Chen et al.'s federated evidential active learning work (CVPR 2024) — neither is cited or differentiated. The manuscript's contribution is a domain application, and it should be framed and evaluated as such.

The most clinically consequential class — normal postoperative status — is also the weakest-performing one (92.34%→84.07% external OvR accuracy after thresholding), meaning the system is least reliable exactly where a false negative (missed complication) or false positive (unnecessary alarm on a normal eye) carries the most workflow impact. This is not discussed.

Class composition does not reflect real-world prevalence: endophthalmitis, a complication with a true incidence near 0.1%, is represented as a full model class alongside common findings, yet no prevalence-adjusted PPV/NPV or calibration analysis under realistic base rates is reported, which is essential before any deployment claim.

The cohort is drawn entirely from four institutions within one country and one ethnicity, a limitation the authors acknowledge but do not mitigate, and STARD-AI is cited as the reporting standard without a corresponding checklist provided in the main text or supplement description.

## 4. Editorial Decision

**Reject**, with recommendation to transfer to *npj Digital Medicine*. The multicenter validation and ablation rigor are solid engineering, but the manuscript overstates methodological novelty relative to UIOS and DEAL/federated evidential active learning, and the weakest subgroup is the clinically pivotal "normal" class — together these are not resolvable through revision without reframing the paper's central contribution claim, which places it below the bar for this venue.

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in evidential deep learning and Dirichlet-based uncertainty quantification for image classification; pool-based and evidential active learning under domain shift; multi-class CNN/ViT architectures for ophthalmic image classification; and calibration/prevalence-adjusted performance evaluation for clinical deployment. On the clinical side, expertise in postoperative cataract complication management and slit-lamp-based anterior segment diagnosis is needed.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Evidential uncertainty in ophthalmic AI has advanced through Wang et al.'s UIOS (open-set retinal anomaly identification with Dirichlet uncertainty scoring) and its extension FMUE (foundation-model uncertainty estimation for OCT), both from the same methodological lineage CATALYST draws on without full attribution. In parallel, evidential active learning has matured independently of ophthalmology: Hemmer et al.'s DEAL established the general combination of evidential deep learning with active sample selection, and Chen et al.'s CVPR 2024 federated evidential active learning work explicitly targeted medical image domain shift — the same problem CATALYST reports solving, but with a federated and multi-institutional design the present manuscript does not engage. Contemporaneously, the SLID dataset (Xu et al., 2026) offers a multi-lesion anterior-segment slit-lamp benchmark that overlaps in imaging modality and disease scope. CATALYST's contribution sits at the intersection of these threads but does not clearly advance any of them individually; its value is the clinical application (postoperative cataract follow-up) rather than the underlying uncertainty or active-learning machinery.

## 7. Suggested Reviewers' Names

**Technical:** Meng Wang (UIOS, Dirichlet evidential uncertainty for retinal anomaly identification); Yong Xia (federated evidential active learning under domain shift, CVPR 2024); Patrick Hemmer (DEAL: deep evidential active learning for image classification).

**Clinical:** Sarah Khavandi (AI-assisted postoperative cataract follow-up, BMJ Open Ophthalmology 2024); Erping Long (CC-Guardian, complication prediction and telemedicine follow-up in cataract patients).

058013
# Editorial Report: "Unequal Care, Unequal Outcomes: Identifying Populations Most Responsive to Stroke Care Equity"

---

## Integrity Alert (Addressed to Handling Editor — Separate from Main Review)

Independent search identified two closely related 2025 publications by an overlapping author core (Ruize Guo, Jingkun Li, Mengyang Liu, Meina Liu — four of six authors here) that are **not cited or disclosed** in this manuscript. "Quality of care for acute ischemic stroke in China during the COVID-19 pandemic" (*BMC Public Health* 2025, DOI 10.1186/s12889-025-23910-x) uses the same National Medical Quality Database, the same AIS cohort definition, a substantially overlapping study window (January 2019–May 2022 vs. the present January 2020–March 2024), and explicitly compares care-quality indicators and mortality **by age and sex** — two of this manuscript's four "novel" dimensions. "Diminishing returns: how treatment delays undermine the mortality benefits of high-quality stroke care" (*BMJ Quality & Safety*, 2025, DOI 10.1136/bmjqs-2025-019307; five of six authors here) examines how **geographic location** modifies stroke-care quality and mortality benefit on what is almost certainly the same registry infrastructure. Neither paper appears in the reference list or is acknowledged as related work distinguishing scope or cohort. This is a disclosure failure with salami-slicing characteristics that the handling editor should raise with the authors before any further processing.

---

## 1. Overall Assessment

The manuscript uses China's National Medical Quality Database (2.88 million AIS admissions, 2020–2024) to quantify disparities in stroke-care quality and outcomes across sex, age, region, and dementia status, and to decompose outcome disparities into direct and treatment-quality-mediated pathways using causal mediation analysis, further contrasting pandemic versus post-pandemic periods. The central claim — that regional disparity is largely explained by treatment-quality differences while age, sex, and dementia disparities are driven by direct pathways — is a genuine analytic contribution if the numbers hold up.

They do not clearly hold up. Beyond the undisclosed-overlap concern above, the mediation-proportion estimate for region (268.462%, 95% CI 167.730–369.195%) is not a physically interpretable proportion; it is an artifact of decomposing a near-null total effect (OR=0.962) into oppositely signed direct (OR=1.065) and indirect (OR=0.904) components, a classic inconsistent-mediation scenario the manuscript never names or caveats.

## 2. Strengths

The scale and national representativeness of the cohort (2,875,427 patients across tertiary, secondary, public, and private hospitals) substantially exceeds prior single-region Chinese stroke-equity studies and supports the multilevel modeling approach used to account for hospital clustering.

The four-dimension, simultaneous equity framework — sex, age, region, dementia — addressed together with dimension-specific propensity-score matching (all achieving SMD<0.100) is methodologically more rigorous than the single-dimension designs (Eriksson et al., Stroke 2021; Xu et al., JAHA 2025) that dominate this literature.

Layering causal mediation analysis onto the disparity framework, decomposing total effects into natural direct and indirect (treatment-quality-mediated) effects, is a legitimate methodological advance over purely descriptive rate-comparison studies, when correctly interpreted.

## 3. Weaknesses

The mediation-proportion metric is uninterpretable wherever direct and indirect effects diverge in sign relative to a near-null total effect — this occurs for region (268%) and produces a nonsensical negative value for age (-1.232%). VanderWeele has repeatedly cautioned against reporting "percent mediated" under inconsistent mediation; the manuscript reports these figures without qualification, which materially undermines its central causal claim.

Dementia prevalence is 1.77%, roughly five- to eight-fold below published pre-stroke dementia prevalence in comparable Chinese and international stroke cohorts (including the authors' own cited reference 19, ~7–15%). A binary "pre-stroke diagnosis" flag drawn from administrative records almost certainly undercaptures true prevalence, which would bias the dementia-dimension estimates toward the null and calls the "no significant difference" findings into question.

The protective effect of rural-hospital care (OR=0.962 for poor outcome, OR=0.561 for death) is attributed post hoc to higher thrombolysis rates offsetting other quality deficits, but referral-pattern confounding — sicker patients being transferred to urban tertiary centers — is an equally plausible explanation that PSM on measured covariates cannot rule out, and is not tested via any negative-control or falsification analysis.

With N=2.88 million, several "significant" differences (e.g., 0.073% sex difference in composite score, P=0.019) are clinically negligible; the manuscript should report standardized effect sizes throughout rather than leaning on significance thresholds that are near-automatic at this sample size.

## 4. Editorial Decision

**Reject.** The undisclosed overlap with two 2025 publications by an overlapping author group on the same database and two of the four disparity dimensions is a non-revisable integrity issue in this submission's current form, and it compounds a substantive, unresolved statistical flaw (uninterpretable mediation proportions exceeding 100%) that undermines the paper's central causal claim. This is not a "revise and clarify" situation.

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in causal mediation analysis under non-collapsibility on the odds-ratio scale, particularly with inconsistent mediation; multilevel/hierarchical modeling of large-scale national administrative registries; propensity-score methods for multi-dimensional confounding adjustment; and health-services epidemiology of rural-urban stroke-care delivery in China. Clinical expertise should cover acute ischemic stroke management protocols, geriatric stroke care in the presence of pre-existing cognitive impairment, and Chinese stroke-center quality-improvement infrastructure.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Single-dimension disparity work remains the norm: Xu et al. (JAHA, 2025) and Eriksson et al. (Stroke, 2021) address sex; Zhu et al. (*International Journal of Stroke*, 2025) and Hammond et al. (Stroke, 2020) address rural-urban gaps in China and the US respectively; Wilcock et al. (JAMA Neurology, 2020) tracks rural-urban Medicare trends longitudinally. None combine four dimensions with formal mediation decomposition, which is genuinely where this manuscript could advance the field — if the mediation estimates were defensible and the overlap with the authors' own 2025 BMC Public Health and BMJ Quality & Safety papers were disclosed and clearly differentiated rather than silently reused.

## 7. Suggested Reviewers

**Causal mediation/biostatistics:** Abdel Douiri (King's College London); Marie Eriksson (Umeå University).
**Rural-urban health services research:** Karen Joynt Maddox (Washington University in St. Louis); Roland Faigle (Johns Hopkins).
**Clinical stroke equity/dementia-stroke intersection:** Amytis Towfighi (USC/Keck); Elin Zupanic (Karolinska Institutet).

057814:
# Editorial Integrity Alert — For Handling Editor Only

Two issues surfaced during independent verification and should be resolved before further processing.

**Citation/venue error.** Reference 15 (Bo, Y. et al., cited as *Hepatol Int* 2025;84(6):e206–e208) matches, by title, a Letter to the Editor — "Development and validation of a prognostic model for MASLD identifying hypertension as a pivotal factor: A population-based study" — published in *Journal of Hepatology*, not *Hepatology International*. These are distinct journals with easily confused abbreviations (J Hepatol vs. Hepatol Int). The page range (e206–e208) also confirms this is a short correspondence rather than a full original article, raising a question the authors must answer: did the source letter contain sufficient methodological detail (complete covariate list, stepwise-selection criteria, imputation rules) to support a genuine independent replication, or were gaps filled by assumption?

**Unacknowledged directly competing prior art.** The manuscript's comparison section cites KNIME, Galaxy, LinkR, OpenAI Codex/Claude Code, and Polly Co-Scientist, but omits AI-HOPE (Yang & Velazquez-Villarreal, *Bioinformatics* 2025;41(7):btaf359; medRxiv preprint Nov 2024) and its extensions AI-HOPE-WNT (*Frontiers in AI*, 2025) and AI-HOPE-TGFbeta (*AI* journal, MDPI, 2025). These describe an LLM-driven conversational agent that translates natural-language queries into executable code for automated Kaplan-Meier estimation, Cox/hazard-ratio analysis, and odds-ratio testing — with AI-HOPE-TGFbeta explicitly incorporating RAG grounding — published 6–14 months before this submission. No author overlap was found. This is not a self-plagiarism concern but a material novelty-misrepresentation risk: the architectural claim underpinning this manuscript's contribution is substantially anticipated.

---

# Editorial Report

**1. Overall Assessment.** The manuscript describes a conversational, zero-code system that translates clinician natural-language requests into executable R scripts, orchestrated via n8n, grounded by RAG over a Pinecone knowledge base, and executed locally to preserve patient-level privacy. Validation consists of replicating one published MASLD Cox prognostic model on NHANES III data, with hazard ratios and AUCs approximating the original.

This is fundamentally a workflow-engineering demonstration rather than a methodological or clinical advance, and its central architectural idea — natural language to auto-generated code to automated survival/regression output — is not new; AI-HOPE and its variants implement the same pattern. Combined with a validation design limited to a single replicated study, this is a difficult case for acceptance at this bar.

**2. Strengths.** The separation of LLM reasoning from patient-level computation is concretely engineered, not merely asserted: the structure-extraction node passes only column-level metadata (types, missingness, distributional summaries) to the external API, never row-level records, which is a real privacy-by-architecture contribution.

The quantitative fidelity check against the source model — hazard-ratio differences of 0.003–0.183, AUC differences below 0.034 — is a genuine, falsifiable reproducibility test rather than a qualitative demo, which is uncommon rigor for proof-of-concept tool papers.

The four-tier layered architecture explicitly targets LLM code hallucination through three named mechanisms (schema profiling, RAG grounding, mandatory local execution), giving reviewers something specific to interrogate rather than a generic hallucination disclaimer.

**3. Weaknesses.** The AI-HOPE omission (above) undercuts the paper's novelty claim at its core; the Discussion's "Comparison with Existing Approaches" section cannot be evaluated as complete without engaging this precedent.

Validation rests on one replicated study in one disease area from a cohort (NHANES III) with which several co-authors have hepatology-related affiliations; there is no external cohort, no second clinical domain, and prospective usability testing is explicitly deferred to future work — "validated" in the framing overstates what one replication supports.

The stepwise-selected model diverged from the original (BMI and platelet count substituted for sex and alkaline phosphatase), attributed to "differences in the initial candidate variable pools" without a sensitivity analysis ruling out a deeper flaw in variable handling or missing-data logic.

Non-determinism is self-reported: one of four analytical tasks required manual re-submission to succeed, yet the abstract markets "100% script-level auditability" and "reproducible R code." A 3-of-4 first-attempt success rate on an n=1 case study is not evidence of reliability, and no automated error-correction loop exists.

**4. Editorial Decision.** Reject. Unacknowledged directly competing prior art, a single-study validation design, and a confirmed citation/venue error together fall below the bar for external review at this stage. Recommend the authors substantively differentiate from AI-HOPE/AI-HOPE-WNT/AI-HOPE-TGFbeta, correct the reference, and either broaden validation across domains or reframe the claims to match a single-domain feasibility study, then consider a transfer venue.

**5. Suggested Reviewer Expertise.** Reviewers should have hands-on experience with LLM agent architectures for automated code generation and execution in biomedical settings; retrieval-augmented generation for hallucination mitigation in scientific/statistical code; workflow orchestration engines (n8n or comparable) for reproducible pipelines; survival analysis and Cox proportional-hazards model validation methodology. On the clinical side, reviewers should have expertise in MASLD epidemiology and NHANES-based prognostic modeling.

**6. State-of-the-Art Literature Review (Past 3 Years).** The dominant recent direction in this space is LLM agents that convert natural language into executable biomedical analysis pipelines: AI-HOPE (*Bioinformatics*, 2025) and its WNT/TGF-β pathway extensions are the closest direct precedent, automating Kaplan-Meier and hazard-ratio analyses from natural-language queries against harmonized clinical-genomic data. Tayebi Arasteh et al. ("Large language models streamline automated machine learning for clinical studies," *Nat Commun* 2024) demonstrated LLM-automated ML pipeline construction for clinical prediction tasks in the same journal this manuscript targets. Broader multi-agent biomedical systems — Biomni, BioMedAgent, CellVoyager (*Nat Methods*, 2026), and DrBioRight 2.0 (*Nat Commun*, 2025) — extend agentic execution to omics and cancer proteomics. Against this landscape, the manuscript's contribution narrows to local-execution privacy architecture and RAG-constrained R code generation specifically for tabular clinical biostatistics; it does not advance beyond AI-HOPE's core mechanism and should explicitly stake out that narrower claim.

**7. Suggested Reviewers.**
*Technical:* Enrique Velazquez-Villarreal (AI-HOPE, *Bioinformatics* 2025); Ei-Wen Yang (AI-HOPE co-developer, same article); Soroosh Tayebi Arasteh (automated ML for clinical studies, *Nat Commun* 2024); a co-author of BioMedAgent (BioMed-AQA benchmark, 2025/2026) for LLM biomedical-agent evaluation methodology.
*Clinical:* a MASLD/NHANES prognostic-modeling biostatistician familiar with the ref. 15 letter's cohort methodology, to adjudicate whether the replication claim is methodologically sound.

056208
# Editorial Report

**Manuscript:** "Efficacy inference in early-phase non-controlled clinical trials via Bayesian biomarker deconvolution"
**Authors:** Humphries et al. (University of Edinburgh)

---

## EDITORIAL INTEGRITY ALERT (for handling editor only)

1. **Undisclosed preprint.** An essentially identical manuscript — same title, same author order, same abstract, same competing-interest statement, same Zenodo code DOI (10.5281/zenodo.20918409) — is posted on medRxiv (doi.org/10.64898/2026.06.26.26356652), publicly available under CC-BY 4.0 since 29 June 2026. This submission discloses no preprint anywhere. Authors should be asked to confirm and disclose before review proceeds.
2. **Financial interest tied to the primary validation benchmark.** SJF is founder/director of Resolution Therapeutics; AMK is a paid consultant to Resolution Therapeutics; CH, JWD, SJF are investigators on the MAIL trial. The manuscript's headline power-analysis result (Fig. 6, the 2.76× MDE improvement) is benchmarked directly against the MAIL trial's own published protocol, using a clearance-accelerating mechanism that matches the macrophage therapy these authors are financially and professionally invested in. This is disclosed in the competing-interests section but not flagged where the benchmark is introduced in the main text.
3. **Closely related concurrent work, same author group, overlapping cohort infrastructure.** Humphries, Kilpatrick, Scullion, Forbes, Dear (*Clin Pharmacol Ther*, 2026) builds a parallel prognostic-enrichment ML tool on an overlapping APAP-DILI population (MAPP2 biobank + MAIL screening cohort) toward the same trial-efficiency goal. Cited once, in passing; not discussed as related work.
4. No evidence of duplicate publication or improper cohort reuse was found between the 195-patient registry used here and the group's other NHS Lothian outputs (SNAP, HiSNAP) — these appear to be distinct cohorts. Spot-checked citations (FDA Jan 2026 guidance, MAIL protocol, Link et al. fomepizole series, Golubev 2010) are accurately represented.

---

## 1. Overall Assessment

The manuscript develops a Bayesian EMG deconvolution framework that separates injury from clearance kinetics in serial ALT trajectories, paired with sparse-data functional PCA and leave-one-out regression to build a within-patient counterfactual score anchored on a 195-patient historic registry. The problem — biomarker-slope confounding by ongoing injury versus clearance in small, uncontrolled acute-injury trials — is real and unaddressed elsewhere. The pipeline is a genuine synthesis, not a repackaging, but every quantitative validation is mechanism-matched and self-benchmarked, and the manuscript omits a material disclosure (see Integrity Alert above).

## 2. Strengths

The preclinical anchor (44 mice, histology-validated ALT-AUC/necrosis R²=0.91) grounds the model's core assumption in tissue-level ground truth. The EMG–fPCA–LOO pipeline yields a concrete, falsifiable claim (67.5%→24.5% minimum detectable effect) rather than a vague efficiency assertion. Applied unmodified to an independent fomepizole case series, it recovers a mechanistically predicted, stage-dependent signature — evidence the parameters carry real biology. The limitations section is candid about observation bias and the mechanism-matched nature of the authors' own validation.

## 3. Weaknesses

Every detection-performance claim is circular: both the semi-synthetic test and the power analysis impose the exact clearance-acceleration effect PC1adj is built to detect, benchmarked against the authors' own trial protocol. No adversarial or null scenario is tested. The 195-patient cohort is single-centre, retrospective, spans 16 years of likely regimen drift, and its use as a historic anchor rests on an asserted, untested exchangeability assumption. Informative observation bias is named but not corrected. The dataset cannot be shared, limiting independent reproducibility.

## 4. Editorial Decision

**Send for Review**, conditional on disclosure of the pre-existing medRxiv posting. Reviewers should adjudicate whether self-benchmarked, mechanism-matched validation supports claims of general applicability, whether the exchangeability assumption needs a temporal-drift check, and whether the Resolution Therapeutics/MAIL financial relationship warrants main-text disclosure.

## 5. Suggested Reviewer Expertise

Reviewers should cover Bayesian nonlinear PK/PD modelling of convolution-type release-and-clearance processes; functional data analysis for sparse, irregularly-timed biomarkers, specifically informative-observation-time methods; Bayesian historical/external-control borrowing for early-phase trial design and its current regulatory treatment (FDA/ICH/EMA); and clinical hepatology/toxicology with direct experience in paracetamol-induced acute liver injury and phase 1 trial conduct in this population.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Bayesian external/historical-control borrowing for early-phase and hybrid trials has accelerated since the FDA's January 2026 draft guidance (confirmed, Docket FDA-2025-D-3217), with 2024–2026 work on dynamic power priors for historical borrowing (Lu et al., *Pharm Stat* 2025) and parallel ICH (2025) and EMA (July 2025 consultation) guidance on external control arms. This manuscript's within-patient counterfactual is a distinct, PK/PD-motivated route to the same borrowing problem but does not engage with this contemporaneous literature. Functional PCA for sparse, informatively-sampled biomarkers has also advanced directly on point (Sang, Kong & Yang, *Biometrika* 2025, on informative observation times; Ségalas et al., *Stat Med* 2024) — precisely the manuscript's own acknowledged limitation — without citation. Within the narrower APAP-DILI niche, the same authors' concurrent paper (Humphries, Kilpatrick, Scullion et al., *Clin Pharmacol Ther* 2026) pursues the same trial-efficiency goal via single-timepoint ML on an overlapping population; the two should be explicitly cross-referenced and differentiated, not left as one passing citation.

## Suggested Reviewers' Names

**Bayesian PK/PD deconvolution:** Kert Viele (Berry Consultants); Yuan Ji (University of Chicago). Both senior — the biomarker-deconvolution literature is thin at junior levels; pair with a functional-data-analysis reviewer below for balance.

**Functional data analysis, sparse/informative sampling:** Peijun Sang (University of Waterloo); Corentin Ségalas (Univ. Bordeaux/INSERM); Cécile Proust-Lima (INSERM Bordeaux).

**Bayesian historical/external-control borrowing:** Zhaohua Lu (Daiichi Sankyo); Philip He (Daiichi Sankyo).

**Clinical hepatology/toxicology, paracetamol overdose:** Geoffrey Isbister (SARPO trial); David M. Wood (King's College London); Ruben Thanacoody (Newcastle, HiSNAP trial). None have co-authored with the manuscript's authors on the trials reviewed here.

---

## Further Literature (Past 3 Years, Similar Scope)

1. **Lu Z, Toso J, Ayele G, He P.** A Bayesian Hybrid Design With Borrowing From Historical Study. *Pharmaceutical Statistics* 2025;24(6):e2466. DOI: 10.1002/pst.2466. Peer-reviewed. Not cited by manuscript; no author overlap. Dynamic power-prior framework for historical borrowing in single-arm/hybrid early-phase trials — a directly competing solution to the historic-control anchoring problem, using borrowing-weight control rather than within-patient EMG counterfactual deconvolution.

2. **Sang P, Kong D, Yang S.** Functional principal component analysis with informative observation times. *Biometrika* 2025;112(1):asae055. DOI: 10.1093/biomet/asae055. Peer-reviewed. Not cited; no overlap. Addresses directly the informative-observation-bias limitation the manuscript names but does not correct in its PACE-fPCA step.

3. **Ségalas C, Helmer C, Genuer R, Proust-Lima C.** Functional Principal Component Analysis as an Alternative to Mixed-Effect Models for Describing Sparse Repeated Measures in Presence of Missing Data. *Statistics in Medicine* 2024;43(26):4899–4912. DOI: 10.1002/sim.10214. Peer-reviewed. Not cited; no overlap. Benchmarks FPCA against mixed-effects models for sparse, error-prone repeated clinical measures — bears directly on the manuscript's choice of PACE-fPCA over parametric alternatives.

4. **Humphries C, Kilpatrick AM, Scullion KM, Aird R, Bruce L, Candela ME, Man TY, Forbes SJ, Dear JW.** Prediction of Acute Liver Injury Trajectory in Patients Following Acetaminophen Overdose: A Multibiomarker Machine Learning Proof-of-Concept Study. *Clinical Pharmacology & Therapeutics* 2026. DOI: 10.1002/cpt.70320. Peer-reviewed. Cited once (ref. 16), methods context only. **Author overlap: same group** (Humphries, Kilpatrick, Forbes, Dear on both) on an overlapping APAP-DILI population (MAPP2 biobank/MAIL cohort). Parallel trial-efficiency solution via single-timepoint multibiomarker ML rather than serial-trajectory deconvolution; should be cross-referenced and differentiated, not left as a single passing citation.

5. **Ross JL, Sabbaghi A, Zhuang R, Bertolini D, et al.** Enhancing Longitudinal Clinical Trial Efficiency with Digital Twins and Prognostic Covariate-Adjusted Mixed Models for Repeated Measures (PROCOVA-MMRM). arXiv:2404.17576, 2024. **Unreviewed preprint** (still preprint-only as of late 2025 per citing literature). Not cited; no overlap. Individualized AI-generated counterfactual ("digital twin") predictions used as a covariate to improve longitudinal repeated-measures trial efficiency — the closest existing conceptual analogue to this manuscript's per-patient counterfactual scoring, but for RCT covariate adjustment rather than uncontrolled single-arm anchoring.

6. **Ji Y.** Regulatory Expectations for Bayesian Methods in Drug and Biologic Clinical Trials: A Practical Perspective on FDA's 2026 Draft Guidance. arXiv:2601.14701, 2026. **Unreviewed preprint.** Not cited; no overlap. Synthesizes the FDA guidance's requirements (pre-specified success criteria, simulation-based operating characteristics, prior justification) against which this manuscript's Bayesian framework is never explicitly positioned, despite citing the guidance itself (ref. 1).

7. **Murasaki W, Ohigashi T, Ishii R, Maruo K, Gosho M.** Modification and extension of the Bayesian clinical trial design using external data for single-arm and hybrid-controlled trials. arXiv:2607.12521, 2026. **Unreviewed preprint.** Not cited; no overlap. Addresses the same core problem — designing single-arm/hybrid early-phase trials using external/historical data under controlled type I error — via prior-specification modification rather than biomarker deconvolution; illustrates that the manuscript's approach is one of several live, competing solutions to this design problem that it does not engage with.

8. **U.S. Food and Drug Administration, Center for Biologics Evaluation and Research, Office of Therapeutic Products.** Innovative Designs for Clinical Trials of Cellular and Gene Therapy Products in Small Populations. Draft Guidance for Industry, September 2025. Docket FDA-2025-D-3403. **Regulatory guidance, not peer-reviewed.** Not cited; no overlap. Explicitly endorses "participant as own control" single-arm designs, disease-progression modelling, and externally-controlled studies for cell and gene therapy trials in small populations — the regulatory category the MAIL macrophage trial itself falls under, and a more directly applicable, more recent regulatory anchor than the general Bayesian-methodology guidance (ref. 1) the manuscript cites instead.

9. **Zhu K, Izem R, Yang P, Yuan Y, Pang H, van der Laan M, Nie L, Emir B, Mishra-Kalyani P, Lee H, Yang S.** Externally Controlled Trials: A Review of Design and Borrowing Through a Causal Lens. arXiv:2605.03282, 2026. **Unreviewed preprint.** Not cited; no overlap. A six-step causal-inference roadmap unifying single-arm and hybrid external-control methodology, covariate shift, and outcome drift — the closest available synthesis of the exact methodological space this manuscript operates in, and the natural benchmark against which its within-patient counterfactual approach should be positioned.

10. **Sherman MS, Goessling W.** Discovery of biophysical rate laws from the electronic health record enables real-time liver injury estimation from transaminase dynamics. *Cell Reports Medicine* 2024;5(11):101828. Peer-reviewed. **Already cited (ref. 12), but under-engaged**: bundled into a five-reference citation cluster in the Introduction rather than discussed as a direct methodological comparator. This paper derives biophysical rate laws for transaminase dynamics from EHR data for real-time injury estimation — conceptually the nearest existing published precedent to the manuscript's own EMG kinetic decomposition of ALT, and worth explicit differentiation rather than a bundled citation.

059325
# Editorial Report: "A smartphone-integrated defibrillator with AI guidance for out-of-hospital cardiac arrest"

---

**Editorial Integrity Alert (For Handling Editor)**

Four issues require resolution before this manuscript proceeds further. First, reference 25, cited as the basis of the rhythm-classification algorithm ("Zheng Y, et al., J Am Heart Assoc. 2021;10(6):e019529"), does not match any retrievable publication. The actual paper matching this title and description is Hajeb-M, Cascella, Valentine, and Chon, JAHA 2021;10(6):**e019065**. Both authorship and article identifier are wrong. Second, the defibrillation circuit specification is physically inconsistent with the stated waveform: two 100 F/125 V supercapacitors in series driving a 3 ms/3 ms biphasic pulse into a 25–150 Ω load implies an RC time constant on the order of 10³–10⁴ seconds, roughly six orders of magnitude longer than the reported pulse duration. Either the units are wrong by a factor of ~10⁶ (μF intended) or the reported engineering-validation data (energy accuracy, charge time, IEC 60601-2-4 compliance) were not generated from the circuit as described. This should be resolved with raw data before any further review. Third, the manuscript does not cite or differentiate itself from Altrix Medical's NSF SBIR-funded "Smartphone-based Automated External Defibrillator" program (Award #1842149, Phase I 2018, Phase II ongoing), which pursues an essentially identical concept — a phone-case-integrated AED with GPS/EMS alerting — predating this submission by years. This is a material omission bearing directly on the novelty claim. Fourth, the corresponding author's stated credential, "Academician of the Russian Academy of Natural Sciences," appears consistently across this author's other publications and is not fabricated for this submission; it denotes membership in a private organization distinct from the state Russian Academy of Sciences and carries limited independent scientific weight — noted for the handling editor's awareness, not as a standalone integrity violation.

---

**1. Overall Assessment**

This manuscript proposes a smartphone-case-integrated AED combining a GaN/supercapacitor defibrillation module, a CNN-based shockable-rhythm classifier, and a MobileNetV2 vision model for real-time CPR feedback, targeting the retrieval-delay barrier to bystander defibrillation. In a 40-person usability trial, the device reduced median time-to-first-shock from 212 s to 92 s versus a conventional AED. The central engineering claim — that medical-grade defibrillation hardware fits a sub-250 g phone case — is undermined by the capacitor specification described above, which is not a minor rounding issue but a fundamental circuit-physics inconsistency. Combined with a miscited foundational algorithm reference and no delivery of a real shock to any living subject, the paper's most consequential claims rest on data whose provenance cannot presently be trusted.

**2. Strengths**

The human-factors design is genuinely rigorous: a blinded stopwatch reviewer decomposed the rescue sequence into six discrete phases (device access, power-on, electrode placement, rhythm analysis, charging, shock delivery), each independently compared by Mann-Whitney U test. This isolates which specific workflow elements drive the aggregate time saving rather than reporting only a pooled effect, and it honestly reports the one phase (charging, 27 s vs. 8 s) where the smartphone device underperforms.

The rhythm-classification validation spans two independent tiers — a porcine VF model (n = 8) and a 1,247-recording clinical pre-hospital ECG dataset with expert-over-reader consensus, 95% confidence intervals, and a full confusion matrix (AUC 0.989) — which is more rigorous than typical single-dataset AED algorithm papers and benchmarks appropriately against AHA sensitivity/specificity targets.

**3. Weaknesses**

The capacitor/waveform inconsistency described in the integrity alert is disqualifying on its own: it is not possible to evaluate "engineering validation" (energy accuracy 98.3 ± 1.5%, IEC 60601-2-4 compliance) for a circuit whose stated components cannot physically produce the stated waveform.

The device has never delivered a real shock to tissue, human or animal; "medical-grade defibrillation" is asserted, not demonstrated, and the usability trial used a simulated shock-button press as the endpoint, which validates none of the high-voltage subsystem.

The novelty claim is overstated. Altrix Medical's federally funded, multi-year smartphone-AED program pursues the identical concept and is not engaged anywhere in the 43 references, leaving the paper's central positioning claim ("here we present") unsupported against the closest prior art.

Generalizability is unaddressed: the usability trial (n = 40) occurred in a single quiet office with pre-connected pads, and the AI CPR-feedback validation on live subjects (n = 12) did not vary lighting, clothing, or body habitus — limitations the authors acknowledge but which remain disqualifying for population-level claims at this stage.

**4. Editorial Decision**

**Reject.** The physically inconsistent capacitor specification, the miscited foundational rhythm-analysis reference, the absence of any real shock delivery, and the unacknowledged multi-year Altrix Medical precedent collectively preclude sending this for external review in its current form. Authors should be invited to resubmit only after correcting the capacitor/waveform specification with verifiable raw data, correcting the citation, and directly engaging the closest prior art.

**5. Suggested Reviewer Expertise**

Reviewers should cover: deep-learning ECG rhythm classification for AED shock advisory during CPR artifact; high-voltage capacitor and flyback-converter design for defibrillation circuits and IEC 60601-2-4 compliance; human-factors/usability engineering for emergency medical devices; smartphone-based volunteer-responder and citizen-defibrillation systems; and emergency medicine/OHCA resuscitation science.

**6. State-of-the-Art Literature Review (Past 3 Years)**

The AED shock-advisory field has moved toward CPR-artifact-tolerant rhythm analysis without requiring compression pauses — exemplified by the Analyze-Whilst-Compressing algorithm validated in the DEFI 2022 study, evaluating clinical performance of an AED shock advisory system with an integrated algorithm for ECG rhythm analysis during ongoing out-of-hospital CPR, and by Hajeb-M et al.'s deep neural network for continuous shock advisory during compressions. Parallel work on device miniaturization includes CellAED, marketed as the world's first personal defibrillator designed to be kept close for use in sudden cardiac arrest, Corscience's compact AED program, and — most directly relevant and unaddressed by the authors — Altrix Medical's NSF-funded smartphone-case AED, which aims to develop miniaturized high-voltage components, firmware, and GPS-to-EMS functionality within a hand-held smartphone-case AED form factor. On the community-response side, Andelius et al. and the Danish HeartRunner program, together with China's 5-minute social rescue circle implementation in Shenzhen, which quantified the impact of a community rescue-circle intervention integrating OHCA cases, CPR-trained residents, and AED deployments, represent the current benchmark for networked bystander response. This manuscript advances device miniaturization incrementally but does not clearly outperform the DEFI 2022 algorithm's reported metrics, and its "always-carried" positioning is not new relative to Altrix Medical's multi-year program.

**7. Suggested Reviewer Names**

*Rhythm analysis / AED shock-advisory algorithms:* Shirin Hajeb-M (University of Connecticut; first author, deep neural network AED shock-advisory system, JAHA 2021); Vessela Krasteva (Bulgarian Academy of Sciences; co-author, DEFI 2022 Analyze-Whilst-Compressing algorithm, Sensors 2023) — noted as more senior; a more junior co-author from the same Schiller Médical/Paris Fire Brigade collaboration (e.g., Sarah Ménétré) may be preferable if available.

*Volunteer-responder / citizen-defibrillation systems:* Linn Andelius (Copenhagen Emergency Medical Services/University of Copenhagen; first author, smartphone activation of citizen responders, JACC 2020 and European Heart Journal – Acute Cardiovascular Care 2023).

*High-voltage power electronics for medical devices:* no junior-faculty candidate with directly comparable published work on GaN-based defibrillator capacitor charging could be confidently identified; recommend sourcing via IEEE APEC/ISPSD early-career track or the power-electronics reviewer pool rather than naming here.

059463
**Editorial Report — Manuscript 059463**
**Title:** Interpretable multi-objective reinforcement learning optimizes dexmedetomidine dosing policy across postoperative cohorts
**Corresponding authors:** Bin Yi, Di Wu (Southwest Hospital, Army Medical University)

---

### Prefatory Editorial Integrity Alert (for handling editor)

Independent verification found no undisclosed preprint of this manuscript, no evidence of cohort reuse with other publications from this author group, and no fabricated or misrepresented citations among the spot-checked references (Lee et al., *NPJ Digit Med* 7, 325, 2024; Bing et al., *NPJ Digit Med*, 2026; Kalimouttou et al., *JAMA* 333, 2025 — all independently confirmed as described). The cited code repository (github.com/Mutopia-H/dex_rl) could not be located via independent search; the editor should ask the authors to confirm public accessibility before further processing. Competing interests are declared as none and funding sources are disclosed. No further integrity concerns were identified.

---

### 1. Overall Assessment

The manuscript develops and externally validates an offline reinforcement-learning policy (CQL) for postoperative ICU dexmedetomidine dosing across three cohorts (MIMIC-IV, eICU, a Chinese hospital; n=7,274), using a dense multi-objective reward and dual off-policy evaluation (FQE, truncated WIS).

The work is careful but incremental. CQL is a five-year-old algorithm, and RL-guided dexmedetomidine dosing was already established by Lee et al. (*NPJ Digit Med*, 2024); the advance is reward densification and a postoperative-specific cohort. More consequential: the primary endpoint (30-day ICU-free days) reached significance in only two of three cohorts, with a near-null result in the authors' own cohort (SWH, +0.13 days, P=0.104).

### 2. Strengths

Three-cohort external validation spanning a US academic center, over 200 US community ICUs, and a Chinese hospital (n=7,274) directly addresses the single-site generalizability failures common in this literature.

The dense four-component reward (sedation, systemic status, safety, respiratory support) plus terminal ICU-free-days reward improves on Lee et al.'s sparse binary delirium reward, enabling component-level attribution of benefit.

Dual off-policy evaluation with bootstrap confidence intervals, Bonferroni correction, and ESS-based exclusion of underpowered WIS components reflects appropriate caution against overoptimism common in offline clinical RL.

SHAP interpretability with individual-trajectory comparisons, consistent with clinical plausibility (early low-dose initiation with hemodynamically responsive de-escalation in high-SOFA patients), supports face-validity beyond a black-box claim.

### 3. Weaknesses

The flagship endpoint is non-significant in SWH, the authors' own institution and largest external set; a null result in one's own data undercuts generalizability more than an external failure would, and the abstract's framing somewhat obscures this.

Composite reward weights were fixed a priori by clinical consensus, with no inter-rater agreement or sensitivity analysis reported; offline RL policies are highly reward-sensitive, and this is uninterrogated.

The comparator set omits Implicit Q-Learning and model-based offline RL, now standard in 2024-2026 clinical RL work, weakening the claim that CQL is optimal.

The evaluation is entirely retrospective; OPE validity rests on an unverifiable overlap assumption, and absolute complication rates (hypotension, bradycardia) are not reported alongside WIS reward deltas, limiting interpretability of the safety claim.

### 4. Editorial Decision

Reject, with transfer to npj Digital Medicine. This is a sound but incremental extension of an already-published paradigm whose primary endpoint fails to generalize significantly to the authors' own cohort, short of the substantial advance required here. Counterargument: three-cohort international validation and dense-reward interpretability are uncommon strengths that npj Digital Medicine, publisher of the entire comparator literature cited, would value without the higher generalizability bar.

### 5. Suggested Reviewer Expertise

Reviewers should have expertise in offline reinforcement learning and conservative Q-learning, off-policy evaluation and its overlap-assumption limitations, and SHAP-based interpretability for RL policies; clinically, expertise in perioperative/ICU sedation management and dexmedetomidine pharmacology.

### 6. State-of-the-Art Literature Review (Past 3 Years)

Clinical RL has moved from single-site proof-of-concept toward multi-cohort, prospectively-tested systems: Kalimouttou et al. (*JAMA*, 2025) validated RL-guided vasopressin initiation in septic shock; Bing et al. (*NPJ Digit Med*, 2026) reported a prospective multicenter RCT of RL-controlled automated anesthesia delivery with non-inferior safety, the field's clearest translational benchmark; Desman et al. (*NPJ Digit Med*, 2025) extended distributional RL to glucose control. Nauka et al. (*NPJ Digit Med*, 2025) interrogated RL transportability failures across ICU sites, work this manuscript should have engaged with given its own null result. This manuscript advances reward design but does not clear the bar Bing et al. sets: prospective validation, not further offline replication.

### Suggested Reviewers' Names

1. **Peter C. Nauka** — postdoctoral researcher, University of Pittsburgh; authored the RL transportability critique directly relevant to this manuscript's cross-cohort inconsistency (*NPJ Digit Med*, 2025).
2. **Arne Peine** — physician-scientist, RWTH Aachen; developed and validated an RL algorithm for mechanical ventilation optimization in critical care (*NPJ Digit Med* 4, 32, 2021).
3. **Aymen Kalimouttou** — postdoctoral researcher, Stanford University; led the OVISS RL vasopressin-initiation trial in septic shock (*JAMA* 333, 1688, 2025).
4. **Jonathan M. Desman** — clinical research fellow, Yale University; developed a distributional RL model for glucose control after cardiac surgery (*NPJ Digit Med* 8, 313, 2025).

059464
# Editorial Report — Manuscript 059464
## "Quantum Entangled Generative Reinforcement Intelligence Framework for Adaptive Drug Discovery and Molecular Treatment Optimizations"

---

## Prefatory Editorial Integrity Alert (Handling Editor Only)

Independent verification flags this manuscript for research-integrity screening before any peer-review assignment. Reference [3] (Philippidis, *GEN Edge*, 2023) is a journalistic Q&A with Schrödinger's CEO and R&D president, not an empirical study. Reference [8] (Martinelli, *Intelligence-Based Medicine*, 2023) is a narrative review of metabolomics machine learning, not a benchmarking paper. Neither source reports quantitative binding-affinity, ADMET, convergence, or clinical-validation metrics, yet Tables 1–6 attribute specific percentage figures to "Philippidis," "Martinelli," and "Turzo" as if these were reproduced experimental baselines. These comparator numbers are fabricated or misattributed. Separately, references [17]–[21] concern hybrid/electric-vehicle energy-management systems by "Ghode and Digalwar," topically unrelated to drug discovery and sharing the corresponding author's surname — undisclosed self-citation padding. The manuscript lists code availability as "not applicable" and data as privately held (Declarations), despite describing training on five fully public repositories (ChEMBL, DrugBank, PubChem, BindingDB, ADMET). This is an internal contradiction. Recommend routing to integrity review rather than standard peer review.

---

### 1. Overall Assessment

The manuscript proposes QEGRI, a five-module pipeline (QEMSE-Net, RGPD-Engine, CBRIT, AQPRO, MTFS Validator) claimed to unify quantum-inspired molecular embedding, diffusion-based pharmacophore generation, causal pathway modeling, reinforcement-based dosing, and multimodal clinical validation.

The central claim is architectural integration, not a demonstrated algorithmic contribution, and the evidence does not survive scrutiny. Equation 1's Hamiltonian H and "protein priors" are never defined; no qubit encoding, quantum circuit, or simulator backend is specified, so "quantum entangled" is decorative language rather than an operational method. Combined with the fabricated benchmark comparisons documented above, this is sufficient on its own for rejection.

### 2. Strengths

The framing correctly identifies a real gap: existing drug-discovery pipelines do treat molecular generation, biochemical reasoning, and toxicity/clinical validation as separate, poorly integrated stages, and multimodal fusion of genomic, imaging, and clinical data is a legitimate open problem in the field.

The choice of evaluation resources — ChEMBL, DrugBank, PubChem, BindingDB, ADMET — is appropriate in principle; these are standard, community-recognized benchmarks for bioactivity and ADMET/Tox prediction, even though their actual use here cannot be verified.

### 3. Weaknesses

The comparative results (Tables 1–6, Figure 2) are not traceable to their cited sources, as detailed in the Integrity Alert; this alone invalidates every quantitative claim of superiority in the paper.

No statistical rigor is reported anywhere: no confidence intervals, no variance across seeds or folds, no significance testing, and no description of train/test splits, despite 24 metrics improving monotonically and implausibly uniformly from Philippidis to Martinelli to Turzo to "Proposed Model" in every single table.

The mathematical formalism (Eqs. 1–8) is non-operational. Terms such as Φ(t), Γ_k, and the "counterfactual" Y_t^cf in Eq. 6 are introduced without definition, units, or an algorithmic procedure for computing them, so the equations cannot be implemented or reproduced from the text.

The manuscript claims "clinical stability," "personalized treatment," and "clinical decision reliability" (Table 5–6) while stating ethics approval is "not applicable," with no patient cohort, IRB record, or real clinical data described anywhere in the paper.

### 4. Editorial Decision

**Reject**, with no transfer recommendation. Fabricated or misattributed comparative benchmarks are a data-integrity failure that disqualifies the paper from any venue, not a fixable weakness; combined with an undefined core method and clinical claims made without patient data or ethics approval, there is no revision path. Recommend the handling editor escalate to the journal's research-integrity process rather than issue a standard rejection letter.

### 5. Suggested Reviewer Expertise

Reviewers should cover: quantum-inspired and quantum machine learning methods for molecular representation (variational quantum circuits, Hamiltonian embeddings); diffusion and flow-matching generative models for de novo molecule and pharmacophore design; causal graph neural networks for biochemical pathway inference; reinforcement learning for treatment-policy and dosing optimization; and, on the clinical side, pharmacology/clinical pharmacokinetics with experience evaluating AI-driven personalized-dosing claims.

### 6. State-of-the-Art Literature Review (Past 3 Years)

Generative chemistry has moved decisively to 3D structure- and diffusion-based design: geometry-complete diffusion models (Morehead & Cheng, *Communications Chemistry*, 2024), discrete diffusion generalists such as GenMol, and flow-matching foundation models like FLOWR.root now jointly generate ligands and predict affinity, evaluated against BindingDB and ChEMBL with explicit validity, novelty, and Tanimoto-similarity metrics. In oncology-specific generation, G2D-Diff (*Nature Communications*, 2025) conditions molecule generation directly on genotype and drug-response distributions. On the quantum side, a 2025 *Chemical Reviews* survey of quantum machine learning in drug discovery lays out data encoding, variational circuits, and hybrid quantum-classical pipelines as the field's actual technical vocabulary — vocabulary this manuscript's Eq. 1 does not engage with. The manuscript cites none of this literature, instead comparing against a magazine interview and a metabolomics review; it neither advances nor meaningfully engages the current state of the art in generative molecular design or quantum-enhanced drug discovery.

### 7. Suggested Reviewers' Names

For quantum molecular representation learning: Elham Torabian (University of British Columbia; quantum-circuit molecular representations for QML, 2025) is a directly comparable, verifiable junior researcher. For diffusion-based molecule generation: Alex Morehead (postdoctoral researcher; geometry-complete diffusion for 3D molecule generation, *Communications Chemistry*, 2024) is directly comparable. For causal pathway modeling and RL-based dosing/treatment policy, I could not independently verify a current junior-faculty candidate with a directly matching publication within this search; recommend the handling editor draw on the journal's existing reviewer database for these two sub-areas rather than accept an unverified suggestion here.

---

## Further Literature

1. Torabian, E., Krems, R.V. (2025). Molecular representations of quantum circuits for quantum machine learning. *arXiv:2503.05955*. **Unreviewed preprint.** No author overlap. Methodologically relevant: direct precedent for quantum-circuit-to-molecule mapping the manuscript's Eq. 1 gestures at without defining.

2. Sajjan, M. et al. (2025). Quantum Machine Learning in Drug Discovery: Applications in Academia and Pharmaceutical Industries. *Chemical Reviews*, 125(12), 5436–5460. https://doi.org/10.1021/acs.chemrev.4c00678. Peer-reviewed. No author/cohort overlap. Establishes the field's actual technical baseline (variational circuits, hybrid quantum-classical models) absent from the manuscript.

3. Morehead, A., Cheng, J. (2024). Geometry-complete diffusion for 3D molecule generation and optimization. *Communications Chemistry*, 7(1), 150. Peer-reviewed. No overlap. Directly comparable generative architecture the manuscript should benchmark against but does not.

4. Lee, S. et al. (2025). A genotype-to-drug diffusion model (G2D-Diff) for generation of tailored anti-cancer small molecules. *Nature Communications*. Peer-reviewed. No overlap. Demonstrates rigorous ChEMBL/NCI60-grounded evaluation with explicit distributional metrics, a standard this manuscript's tables do not meet.

5. Reidenbach, D. et al. (2025). FLOWR.root: A flow matching based foundation model for joint 3D ligand generation and affinity prediction. *arXiv:2510.02578*. **Unreviewed preprint.** No overlap. Competing joint generation-plus-affinity architecture relevant to RGPD-Engine's claims.

6. Duong, H.P.Y. et al. (2024). Quantum Machine Learning for Drug Discovery: Taxonomy, Research Challenges, and the Road Ahead. **Unreviewed preprint/in-press.** No overlap. Provides the taxonomic framing the manuscript's "quantum entangled" claims should be situated against but are not.

7. Diffusion Models at the Drug Discovery Frontier: A Review on Generating Small Molecules versus Therapeutic Peptides (2025). *MDPI*. Peer-reviewed. No overlap. Documents known BindingDB/ChEMBL data-scarcity limitations the manuscript's tables do not acknowledge.

8. Martinelli, D.D. (2023). Machine learning for metabolomics research in drug discovery. *Intelligence-Based Medicine*. Peer-reviewed. **Already cited by manuscript as [8], but misattributed as a quantitative benchmarking source in Tables 1–6; it contains no such data.** Flagged in Integrity Alert.

9. Philippidis, A. (2023). Schrödinger's Equation: Physics + Machine Learning = Drug Discovery. *GEN Edge*. Trade/journalistic piece, not peer-reviewed research. **Already cited by manuscript as [3], same misattribution issue.** Flagged in Integrity Alert.

10. Zhou, Y. et al. (2024–2025). Quantum-machine-assisted Drug Discovery. *arXiv:2408.13479*. **Unreviewed preprint.** No overlap. Actual experimental quantum-machine pipeline for drug discovery, offering a real methodological contrast to the manuscript's undefined Hamiltonian formalism.

---

*Report prepared per Nature Communications Digital Health editorial standard, calibrated to The Lancet Digital Health bar for clinical/methodological significance.*
