# Trackrad202512456

067671
Editorial Report — Manuscript 067671

"Addressing challenges in agentic retrieval of structured data from biomedical databases" (BioChirp)

1. Overall Assessment

The manuscript presents BioChirp, an interpretation–execution-separated retrieval system for curated biomedical databases. LLMs handle question interpretation, schema-field mapping, and synonym resolution; a deterministic Steiner-tree planner and executor then perform table selection, joins, and record retrieval. Reported results are substantial: median cross-run Jaccard similarity of 1.0 across three backends, 85.4% versus 44.6% table-hit rate against agentic NL2SQL across 910 BioASQ-derived evaluations, and a 45-fold undercount by an MCP-connected Claude Sonnet 4.5 configuration on an exhaustive Open Targets query.

That empirical case is now moot. Independent verification identifies a bioRxiv preprint (2026.04.25.720782, posted 25 April 2026) describing the identical system, with overlapping authorship, the same GitHub repository and the same deployment URL, neither cited nor disclosed. The preprint declares that D. Sengupta and M. Farooq are GeneSilico shareholders; the submission declares no competing interests despite Farooq's stated GeneSilico affiliation.

2. Strengths

The deterministic Steiner-tree planner (Mehlhorn, 1988) addresses a real failure mode the manuscript itself demonstrates: Sonnet 4.5 returning 99 of 4,473 associations without any operational error signal.

The 910-evaluation BioASQ comparison against a LangChain–Qwen-2.5-7B-instruct baseline is appropriately scaled, and the re-audit of all 157 FAIL verdicts (60 database coverage gaps, 29 genuine misses) interrogates the system's own failures rather than only its wins.

The field-mapping experiment shows that mapper agreement conceals 11/150 HCDT and 8/150 TTD shared errors — a limitation stated plainly rather than hidden behind the 92.7–94.0% headline.

3. Weaknesses

Completeness is bounded by entity-resolution recall, which peaks at 0.40–0.42 precision for SapBERT on diseases and is worse for drugs; no sensitivity analysis links this upstream ceiling to downstream association-level loss.

Claude Sonnet 5 serves as all three graders plus adjudicator in the BioASQ evaluation. This is circular self-assessment; PASS/PARTIAL/FAIL rates require a human-annotated subsample.

Cross-database MCP workflows are two illustrative examples, yet support a generalized interoperability claim in the Discussion.

4. Editorial Decision

Reject. The undisclosed prior disclosure and undisclosed competing interest are each independently disqualifying and are not revisable within this submission. Recommend transfer to npj Artificial Intelligence or Communications Biology, contingent on both integrity issues being resolved with the editorial office first.

Steelman: both omissions could be administrative oversights correctable by author response, and the underlying contribution — quantifying silent evidence loss in agentic biomedical retrieval — is novel enough to warrant revision rather than rejection. Not accepted here: GeneSilico's commercial interest bears directly on a corresponding author's incentive to overstate BioChirp's advantage over commercial-LLM baselines, which is the manuscript's central empirical claim.

067660
# Editorial Report (Condensed)

**Manuscript:** "The choice of large language model reverses the simulated go/no-go decision in digital mental-health trial planning: a four-axis credibility assessment of synthetic-patient simulation across 12 models"
**Authors:** Woo, H.J. & Kim, M.-G.

## 1. Overall Assessment

The manuscript operationalizes ASME V&V 40 into four credibility axes for LLM synthetic patients across 12 models and 623 personas, then re-seeds the simulator on 266 real Brighten iPST enrollees and tests simulated against observed PHQ-9 change. This is a substantive advance rather than a repackaging: the field stops at face plausibility, and this paper supplies the missing ground-truth step, returning a replicated negative result (trajectory drifts upward, individual-level Spearman ρ ≈ 0). Two concerns dominate: the capstone claim rests on one trial, and much of the machinery is inherited from the authors' companion study.

## 2. Strengths

The IPD-seeded validation converts plausibility into falsifiability and replicates across four architecturally distinct models and a held-out Brighten wave. The return-map analysis (Fig. 5d) localizes the trajectory failure to a specific architectural choice — distress re-elicited from the pre-intervention value, never carried forward — rather than a vague model deficit. Cross-generator replication (ρ = 0.95) with a strict-schema runner logging 739,802 provenance records and no imputation sets an unusually high auditability standard. The anchor analysis is self-critical: in-sample recalibration succeeds, out-of-sample transport fails, and the authors report the failure.

## 3. Weaknesses

The predictive-failure claim rests on a single trial whose comparator arm changed as much as iPST. The Type A–C anchors are between-group, full-course meta-analytic estimates reapplied as within-person single-check-in reductions, so the headline 1.7–2.8-fold overestimate is partly a unit-conversion artifact. Pre-specification rests on internal dated logs, not public registration — a weak standard for a paper about quantitative trust. Core architecture, phenotype rules, and anchors are carried over from the companion Scientific Reports paper.

## 4. Editorial Decision

**Send for Review.** The ground-truth test and its mechanistic diagnosis clear the bar. Reviewers must adjudicate: whether a second real-outcome cohort is required; whether the anchor unit conversion invalidates the Axis-2 headline; and whether novelty over the companion study is sufficient standalone.

## 5. Suggested Reviewer Expertise

Reviewers should cover: LLM-based patient/agent simulation and fidelity evaluation; extension of V&V 40-style credibility frameworks to non-physics-based generative and AI/ML models; digital mental-health trial methodology and remote-RCT engagement/adherence measurement (Brighten-type designs); Bayesian and equivalence-testing statistics (bootstrap TOST, effect-size standardization); and clinical psychiatry/psychology expertise in depression and anxiety digital interventions and PHQ-9/GAD-7 measurement-based care.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The dominant recent thread evaluates LLM synthetic patients by perceived realism or downstream training utility: PATIENT-Ψ (Wang et al., EMNLP 2024) builds CBT-cognitive-model-grounded patients for trainee practice; Roleplay-doh (Louie et al., EMNLP 2024) elicits domain-expert principles to constrain simulated patients; Reichenpfader & Denecke (2024) generate diverse patient vignettes; a December 2025 Communications Medicine paper on LLM-agent simulated patients for medical education and a January 2026 JMIR systematic review of LLM virtual-patient systems both confirm the field still measures fidelity via expert or automated realism scores, not real-outcome recovery. A closely analogous December 2025 in-silico PROM pre-validation study (cataract PROMs, Journal of Clinical Medicine) stress-tests instruments on an LLM-generated synthetic cohort but, like the rest of this literature, never checks the simulation against real enrolled patients' actual outcomes — the exact gap this manuscript closes. On the credibility-framework side, Pathmanathan and colleagues' extension of V&V 40 to patient-specific computational models (PLOS Computational Biology) is the nearest methodological precedent and is not cited; the authors should engage it directly. The manuscript should also more explicitly contrast its non-carry-forward architecture against autoregressive digital-twin EHR simulators (e.g., recent arXiv work on timeline-based patient digital twins) that do propagate state forward, since that comparison bears directly on the authors' own stated next step.

## 7. Suggested Reviewer Names

*LLM patient simulation:* Ruiyi Wang (CMU, PATIENT-Ψ lead), Stephanie Milani (Assistant Professor, Johns Hopkins CS; PATIENT-Ψ co-lead), Jocelyn Shen (MIT Media Lab, simulated-agent evaluation) — verify current rank/affiliation for the latter before contacting.

*V&V/credibility frameworks:* Pras Pathmanathan (FDA/OSEL, patient-specific V&V 40 extension) — his regulatory affiliation should be checked for conflict-of-interest screening given the manuscript's regulatory framing.

*Digital mental-health trial methodology:* Abhishek Pratap (co-author, Brighten Sci Data release; verify current institutional position), a Brighten-adjacent adherence/engagement methodologist.

*Statistics/calibration:* a biostatistician with published TOST/equivalence-testing work in digital-therapeutics effect-size estimation — specific name not independently verified; flagged as a gap rather than fabricated.

---

## Further Literature (10 papers, scope-matched)

**1.** Wang, R. et al. PATIENT-Ψ: Using Large Language Models to Simulate Patients for Training Mental Health Professionals. *Proceedings of EMNLP 2024*, 12772–12797. Peer-reviewed conference proceedings. **Not cited.** Authors independent (CMU/Princeton/Pitt/Stanford). The canonical LLM-simulated-mental-health-patient framework; its evaluation is expert-perceived realism, which is precisely the standard this manuscript argues is insufficient. Its absence from the reference list is a material omission.

**2.** Simulated patient systems powered by large language model-based AI agents offer potential for transforming medical education. *Communications Medicine* 5 (2025). DOI: 10.1038/s43856-025-01283-x. Peer-reviewed. **Not cited.** Independent. Contemporary Nature-portfolio treatment of LLM simulated patients; establishes the current publication bar in this exact sub-domain and demonstrates that outcome-anchored validation is still absent from the field.

**3.** Callies, A., Bodinier, Q., Ravaud, P. et al. Real-world validation of a multimodal LLM-powered pipeline for high-accuracy clinical trial patient matching. *Communications Medicine* 5, 536 (2025). DOI: 10.1038/s43856-025-01256-0. Peer-reviewed. **Not cited.** Independent (Université Paris Cité / AP-HP). Adjacent scope — LLMs in trial operations validated against real cohorts (n2c2, 485 real patients). A useful contrast: real-world validation is achievable in this space, which strengthens rather than weakens the reviewers' demand for a second validation cohort here.

**4.** Warner, A., LeDue, J., Cao, Y., Tham, J. & Murphy, T.H. Synthetic patient and interview transcript creator: an essential tool for LLMs in mental health. *Frontiers in Digital Health* 7 (2025). PMC12460306. Peer-reviewed. **Not cited.** Independent (UBC). Directly comparable synthetic-mental-health-patient generation; validates against demographic distributions only, illustrating the plausibility-versus-accuracy distinction this manuscript formalizes.

**5.** Moëll, B. & Aronsson, F.S. High-accuracy prediction of mental health scores from English BERT embeddings trained on LLM-generated synthetic self-reports. *Frontiers in Digital Health* (2026). DOI: 10.3389/fdgth.2025.1694464. Peer-reviewed. **Not cited.** Independent (KTH/Karolinska). Synthetic-only PHQ-9/GAD-7-adjacent method development with no real-patient outcome check — an instance of the failure mode this manuscript documents, and a natural citation for the discussion.

**6.** Using Large Language Models for In Silico Development and Simulation of a Patient-Reported Outcome Questionnaire for Cataract Surgery. *Journal of Clinical Medicine* 15(1), 283 (2026). DOI: 10.3390/jcm15010283. Peer-reviewed (MDPI; note the lower editorial threshold). **Not cited.** Independent. Closest structural analogue outside mental health: LLM-generated synthetic cohort (n = 500, structured JSON personas) used for instrument pre-validation without real-outcome anchoring.

**7.** Galappaththige, S., Gray, R.A., Costa, C.M., Niederer, S. & Pathmanathan, P. Credibility assessment of patient-specific computational modeling using patient-specific cardiac modeling as an exemplar. *PLOS Computational Biology* 18(10), e1010541 (2022). DOI: 10.1371/journal.pcbi.1010541. Peer-reviewed. **Not cited.** Independent (FDA CDRH / KCL). *Note: October 2022 — marginally outside the three-year window, retained because it is the single most relevant methodological precedent for extending V&V 40 beyond its original scope, which is this manuscript's central framing claim.*

**8.** Review: Large Language Model–Based Virtual Patient Systems for Medical History-Taking — a PRISMA systematic review of 39 studies (search window to August 2025). *JMIR Medical Informatics* 12, e79039 (2026). Peer-reviewed. **Not cited.** Independent. Establishes the field-wide evaluation landscape; the authors' claim that "none has quantified how much trust the simulation warrants" should be tested against this review's evidence synthesis rather than asserted.

**9.** Park, J.S., Zou, C.Q., Shaw, A. et al. Generative Agent Simulations of 1,000 People. arXiv:2411.10109 (2024). DOI: 10.48550/arXiv.2411.10109. **PREPRINT — not peer-reviewed; flag as unreviewed if cited.** Independent (Stanford/Google DeepMind/Northwestern). The strongest existing individual-level LLM-simulation-fidelity result (agents reproduce GSS responses at ~85% of participants' own two-week test–retest reliability). This directly contradicts the manuscript's implied generality: individual-level accuracy has been achieved elsewhere with interview-grounded conditioning, suggesting the failure reported here may be an artifact of thin persona conditioning rather than a property of LLM simulation. The authors must engage this.

**10.** Argyle, L.P. et al. Out of One, Many: Using Language Models to Simulate Human Samples. *Political Analysis* 31(3), 337–351 (2023). DOI: 10.1017/pan.2023.2. Peer-reviewed. **Not cited.** Independent (BYU). Origin of "algorithmic fidelity" and silicon sampling; the conceptual parent of persona-conditioned LLM simulation. The manuscript's four axes substantially reinvent vocabulary already established in this literature without acknowledgment.

**Editorial note (not for the authors):** Reference 6 — Woo, H.J. & Kim, M.-G., *Scientific Reports* 16, 64139 (2026) — is the companion study supplying this manuscript's architecture, anchors, and phenotype rules. I could not independently verify this citation via search; the volume/article numbering should be confirmed against the publisher record before the manuscript proceeds, and the degree of methodological overlap should be assessed for salami-slicing at the same time.

**Counterargument to the "Send for Review" decision (steelmanned):** A reasonable editor would reject. Item 9 above is the strongest case — if interview-grounded agents already achieve near-test-retest individual fidelity, then this manuscript's headline negative finding is a statement about one under-specified simulator, not about LLM synthetic patients as a class, and the abstract's generalization ("LLM synthetic-patient simulation as implemented here therefore has qualified credibility") is doing heavy lifting via the qualifier. Combined with a single validation cohort, an uncontrolled comparator arm, unregistered pre-specification, and heavy inheritance from the companion paper, the residual novelty may reduce to "we ran the authors' prior pipeline in English against one trial and it failed" — a finding better matched to *Communications Medicine* or *npj Digital Medicine* than to this journal. I weigh against rejection because the return-map mechanism (Fig. 5d) is a genuine, transferable architectural insight that survives even if the generality claim is trimmed, but the margin is narrow and reviewers should be told so explicitly.

067388
# Editorial Report — Manuscript 067388
**Title:** Lead-conditioned diffusion generates multilead electrocardiograms from single-lead recordings
**Authors:** Anonymous

---

## 1. Overall Assessment

ECG-DDPM is a conditional diffusion model that estimates Lead II and V1–V6 from an observed Lead I signal, with Leads III, aVR, aVL, aVF then computed by fixed limb-lead algebra. It is trained on paired PTB-XL recordings and transferred, without paired ground truth, to PhysioNet/CinC 2017 for four-class rhythm classification. The claimed advance — lead-conditioned diffusion recovering multiview ECG structure from a single wearable lead more accurately than VAE/GAN baselines — does not survive scrutiny of the literature. This is a populated subfield, and at least one directly comparable PTB-XL Lead I→12-lead study, published in a Nature-family journal, reaches a contradictory conclusion; it is not cited. Compounding this, four of eight reported leads are not independently generated but deterministic transforms of Lead II, so error propagates silently through half the lead set — precisely where the paper's own correlations are weakest.

## 2. Strengths

The bias/noise-prediction two-network split is a sound way to handle cross-lead amplitude and morphology differences within one diffusion framework, and is documented with reproducible specificity. Evaluation is properly multi-layered — pointwise error, distributional divergence, named waveform features, lead-wise correlation, and downstream classification across five PTB-XL superclasses — and candidly shows reconstruction fidelity and diagnostic utility do not always track together. The PhysioNet/CinC transfer experiment is honestly scoped: the authors state plainly that only classification utility, not anatomical accuracy, is supported there.

## 3. Weaknesses

Joo et al. (MICCAI 2023, GAN on the identical task), Presacan et al. (*Communications Medicine*, 2025, GAN on the identical PTB-XL task, concluding poor clinical accuracy), and SSSD-ECG (Alcaraz & Strodthoff, 2023) are all uncited despite direct relevance. The four algebraically derived limb leads inflate aggregate metrics without separation from genuinely generated channels. No clinician-in-the-loop evaluation exists; utility rests on generic classifier features, well below the bar set by cardiologist-adjudicated comparators (Mason et al., *npj Digital Medicine*, 2024). Validation is single-source, unstratified, with no external paired cohort, and Table 1's 10 ms median QRS-duration gap against a 1.84 ms mean gap suggests an uninvestigated skewed error distribution.

## 4. Editorial Decision

**Reject.** The unaddressed, directly contradictory prior art and the algebraic-lead confound are not revisable without substantial re-framing and new head-to-head comparisons. Counterargument: the architecture and transfer experiment are real if incremental contributions that could clear a lower-tier bar with added baselines, separated metrics, and clinician evaluation — better served by transfer than review here. **Suggested transfer:** *Communications Medicine* or *npj Digital Medicine*.

---

## 5. Suggested Reviewer Expertise

Conditional/denoising diffusion architectures for physiological time series (noise-prediction U-Nets, DDPM/DDIM sampling) specifically applied to ECG; generative adversarial and autoencoder baselines for lead reconstruction and their known failure modes; PTB-XL benchmarking methodology and diagnostic superclass evaluation; signal-processing validation of derived limb-lead algebra and propagated error; clinical electrophysiology of inferior-lead and precordial morphology (Brugada pattern, AVNRT, bundle branch block) relevant to what is lost when leads are estimated rather than measured.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

Single-lead-to-12-lead ECG reconstruction has moved from patient-specific and GAN-based approaches toward diffusion and masked-modeling frameworks over the last three years, largely using PTB-XL as the common benchmark. Alcaraz and Strodthoff's SSSD-ECG (2023) established structured-state-space diffusion for conditional 12-lead ECG generation. Joo et al. (MICCAI 2023) reconstructed 12-lead ECGs from Lead I with a dual-generator GAN and a 1D U-Net discriminator, evaluating CVD-relevant characteristics via a downstream classifier — methodologically close to this manuscript's own GAN baseline and evaluation design. A masked-autoencoder approach (*npj Cardiovascular Health*, 2024) generalized reconstruction to arbitrary single-lead inputs with more extensive lead-wise evaluation. Mason et al. (*npj Digital Medicine*, 2024) reconstructed 12-lead ECGs from three leads and validated STEMI detectability with three cardiologists, setting a clinical-evaluation standard this manuscript does not meet. Most consequential for this submission, Presacan et al. (*Communications Medicine*, 2025) directly replicated the Lead I(/I+II)-to-12-lead task on PTB-XL with a GAN and concluded reconstruction accuracy was clinically inadequate — a negative result on essentially the same problem that this manuscript's positive framing must, at minimum, address and did not. Against this landscape, ECG-DDPM's contribution is an architectural variant (diffusion in place of GAN/VAE, with a learned lead-bias term) rather than a demonstrated advance in what the field has already identified as the harder problem: whether any current architecture reconstructs unmeasured leads to clinical fidelity.

---

## 7. Suggested Reviewers' Names

**Technical (diffusion/generative modeling for ECG):**
Nils Strodthoff (University of Oldenburg) — co-developer of SSSD-ECG and PTB-XL deep-learning benchmarking.
Juan Miguel Lopez Alcaraz — co-author, diffusion-based conditional ECG generation with structured state space models.
Hyeonseung Im (Kangwon National University) — corresponding author, MICCAI 2023 GAN-based Lead I-to-12-lead reconstruction.
Vajira Thambawita (SimulaMet) — co-author, Communications Medicine reconstruction-feasibility study on PTB-XL.

**Clinical (electrophysiology / wearable cardiac monitoring):**
Arun R. Sridhar (University of California, San Francisco / Communications Medicine reconstruction study) — cardiac electrophysiology.
Jørgen K. Kanters (University of Copenhagen) — ECG morphology and clinical ECG measurement.

---

## Editorial Integrity Alert (Handling Editor Only)

The omission of Presacan et al. (*Communications Medicine*, 2025) is flagged specifically: it is the closest possible prior-art match (same dataset, same Lead I→12-lead task, GAN architecture) and reaches a conclusion — poor reconstruction accuracy — that directly contradicts this manuscript's positive framing. Whether this reflects an incomplete literature search or a scoping choice made to present the method more favorably cannot be determined from the manuscript alone, but the omission should be raised explicitly with the authors rather than treated as an ordinary literature-review gap. No other integrity concerns (undisclosed preprint status, salami-slicing, author overlap with cited comparators, competing interests) were identified; the manuscript is anonymized for review and author affiliations could not be independently checked.

067316
# Editorial Report: "Deep learning-derived electrocardiogram markers predict atrial cardiomyopathy in patients with coronary heart disease"

## 1. Overall Assessment

This manuscript reports an external validation of a previously developed deep-learning model (DL-AtCM) that infers left atrial structural and functional phenotypes from 12-lead ECG, applied without retraining to 3,797 digitized ECGs from INTERASPIRE, a 14-country coronary heart disease (CHD) cohort. The central claim is that DL-AtCM-derived predictors improve discrimination for incident AF (AUC 0.713 vs. 0.616 for CHARGE-AF simple score) and heart failure hospitalization (AUC 0.705 vs. 0.679 for the Ho et al. clinical score) when layered onto conventional risk scores, and that this holds even when the ECGs originate from heterogeneous paper/photograph scans requiring digitization.

The technical contribution — bridging a waveform-trained model to 2D-scanned ECGs across 3×4, 6×2, and 12×1 layouts — is a genuine and underexplored problem. However, the clinical claim rests on 44 AF events and 63 HF events, producing AUC confidence intervals that overlap substantially with the comparator scores, and no formal test (e.g., DeLong) of the AUC differences is reported. The underlying DL-AtCM model itself is, as of this review, an unpublished, non-peer-reviewed medRxiv preprint (Deseoe et al., posted January 2026) authored by overlapping personnel (Deseoe, Wegener, Lip) on this manuscript. These two issues — statistical fragility and dependence on an unreviewed proprietary model — will dominate the decision.

## 2. Strengths

The digitization and layout-robustness analysis is the manuscript's most substantive contribution. Applying Open-ECG-Digitizer (Stenhede et al., npj Digital Medicine 2026) across three distinct display formats, and showing endpoint-specific recalibration was broadly preserved in the larger 3×4 and 6×2 groups, directly addresses a real deployment barrier: most clinical ECG archives exist as paper or photographed records, not raw waveforms.

The perturbation-based explainability analysis (lead masking and beat-aligned windowing) is methodologically sound and clinically interpretable. Convergence of model sensitivity on lead II, V1, and the P-wave region (peak contribution −20% to −10% of the RR interval) is physiologically coherent with known P-wave morphology markers of atrial cardiomyopathy, and strengthens the case that the model is not exploiting layout artifacts.

The echocardiographic concordance analysis, while modest in magnitude, is an honest attempt at biological validation given that INTERASPIRE lacks CMR. Reporting both same-day (rho=0.297, n=117) and 30-day window (rho=0.196, n=202) correlations, rather than only the more favorable comparison, reflects appropriate transparency.

## 3. Weaknesses

The primary AUC comparisons are underpowered to the point of fragility. With 44 AF events, the DL-enhanced CHARGE-AF AUC (0.713, CI 0.621–0.804) and the simple CHARGE-AF AUC (0.616, CI 0.522–0.707) have overlapping confidence intervals; the manuscript states differences were assessed by bootstrap but never reports the resulting p-value or a reclassification metric (NRI/IDI). The abstract and discussion assert the DL model "outperformed" and "achieved the strongest signal," language not supported by the interval overlap shown in Figure 2A.

The core predictive engine is an unpublished preprint. Reviewers cannot independently verify architecture, training procedure, or internal calibration of DL-AtCM without access to non-peer-reviewed material from the same author group, which is a circularity concern for external validation claims.

No subgroup analysis is presented despite recruitment across 14 countries and documented sex imbalance (~20% female). A model validated in aggregate on a CHD population cannot be assumed to generalize across sex or region without testing; this is a standard failure mode for AI-cardiology papers and is not addressed even qualitatively.

HF ascertainment was not adjudicated, and follow-up duration varied widely (56–1,313 days) without landmark analysis or time-dependent AUC framing, raising immortal-time and follow-up-heterogeneity concerns for the HF endpoint specifically.

## 4. Editorial Decision

**Send for Review**, contingent on the authors substantially reworking the statistical framing before reviewers are engaged. Reviewers should be asked to adjudicate: (1) whether formal significance testing (DeLong, bootstrap p-values, NRI) supports the claimed superiority given n=44/63 events; (2) whether validation against an unpublished companion model constitutes adequate independent verification, and whether the editors should require the companion preprint's peer-review status prior to acceptance; (3) whether country- or sex-stratified performance should be mandatory given the multinational recruitment.

**Steelman counterargument**: one could argue rejection is premature — external validation studies are inherently constrained by event counts in the source cohort, and the paper's own limitations section candidly acknowledges this. The digitization-robustness finding stands independently of the AUC significance question and may itself be publishable as a methods contribution. A reviewer round focused on tightening statistical claims, rather than a preprint desk-reject, may be the more proportionate response.

## 5. Suggested Reviewer Expertise

Deep learning models for ECG-based cardiac phenotype prediction (waveform-to-imaging translation); statistical methodology for external validation of prediction models with small event counts (calibration, DeLong testing, reclassification metrics); ECG digitization and signal-processing pipelines for paper/scanned records; clinical epidemiology of atrial cardiomyopathy and AF risk prediction in secondary-prevention CHD populations; cardiovascular imaging (echocardiography/CMR) correlation with ECG-derived atrial biomarkers.

## 6. State-of-the-Art Literature Review (Past 3 Years)

DL-ECG AF prediction has matured rapidly. Brant et al. (Circ Arrhythm Electrophysiol, 2025) validated a deep neural network for AF risk across FHS, UK Biobank, and ELSA-Brasil, explicitly reporting DeLong-based significance testing against clinical scores — a methodological bar this manuscript does not meet. Khurshid et al. (Circulation, 2022) and Raghunath et al. (Circulation, 2021) established large-cohort DL-ECG AF prediction with tens of thousands of events, dwarfing the 44-event INTERASPIRE cohort used here. The companion DL-AtCM preprint (Deseoe et al., medRxiv 2026) itself reports external validation in a Brazilian primary-care cohort (n=64,851) and a stroke cohort, which is far better powered than the present CHD analysis; the current manuscript would benefit from direct comparison of effect sizes against that companion work rather than treating INTERASPIRE in isolation. Ahmad et al. (Circ Arrhythm Electrophysiol, 2021) previously validated an AI-ECG AF model specifically in coronary microvascular disease, a directly comparable high-risk cardiac population the authors cite but do not benchmark against numerically. The manuscript's genuine advance — layout-heterogeneous digitized-ECG robustness — is not directly addressed in any of these predecessor studies and is the strongest basis for eventual publication.

---

## Suggested Reviewer Names

**DL-ECG methodology:** Luisa C.C. Brant (Universidade Federal de Minas Gerais) — multinational DL-ECG AF prediction, Circ Arrhythm Electrophysiol 2025; Antônio H. Ribeiro (Uppsala University) — DL-ECG model development and validation infrastructure.

**Statistical/validation methodology:** a biostatistician with published work on external validation and recalibration of clinical prediction models in low-event cohorts (target assistant/associate professor level in clinical epidemiology; specific candidate not independently verifiable from available search — flag as a gap for the handling editor to fill via institutional biostatistics contacts).

**Clinical CHD/AF context:** a cardiologist with published AI-ECG validation work in coronary or microvascular disease populations, comparable to Ahmad et al. 2021 — no INTERASPIRE-affiliated or DL-AtCM-affiliated individual should be used given direct conflict.

---

### Editorial Integrity Alert (handling editor only)

The manuscript's core predictive model (DL-AtCM) is validated in this paper but was itself first described in a non-peer-reviewed medRxiv preprint (Deseoe et al., 2026.01.12.26343962) sharing three authors with the present submission (Deseoe, Wegener, Lip). This is not disclosed as a companion-paper relationship in the competing-interests or acknowledgments sections. Recommend requiring authors to explicitly state the peer-review status of the source model and its relationship to this submission, and consider whether acceptance should be contingent on the companion preprint completing peer review first, given that this paper's entire predictive apparatus is inherited from it without independent methodological scrutiny.

067295
## 1. Overall Assessment

The manuscript formalizes Sepsis-3 as a measuring model with six implementation dimensions, enumerates 2,520 variants, and decomposes labeling variance via linear mixed-effects models across SepsisExp, MIMIC-III, and eICU. It then benchmarks variants against GTSQ expert labels and shows models trained on Sepsis-3 labels underperform expert-trained models by up to 18 AUROC and 13 F1 points. The claim that Sepsis-3 implementations are not interchangeable is well-evidenced and materially extends Cohen et al. (2024), who varied onset definitions alone on a single dataset.

## 2. Strengths

The measurement-theoretic separation of fundamental measurements, derived functions, and axioms gives the field usable vocabulary, and Table 1 is the most complete catalogue of Sepsis-3 implementation heterogeneity published to date. Anchoring Experiment 2 to GTSQ expert labels (Krippendorff's α = 0.94) rather than to another consensus variant converts a combinatorial exercise into a clinically grounded one. Experiment 3 closes the loop to downstream transformer-based prediction, demonstrating that label-definition variance propagates into measurable model degradation.

## 3. Weaknesses

Expert ground truth exists only for SepsisExp (1,961 patients, one German ICU); α was assessed on 126 patients, roughly 5% of the analytic cohort. Claims about which implementation "best matches ground truth" cannot be separated from site-specific annotation culture. Experiment 3's nine variants are selected by K-means on BLUP-estimated F1 against ground truth, then used to show that Implementation F1 predicts Prediction F1 — a correlation partly guaranteed by construction. The interaction LMEM showing pronounced OD-Function × Sepsis-Onset coupling is deferred entirely to Supplementary Information despite qualifying the independent-effects narrative. Tables 2–6 report no confidence intervals; BLUP point estimates carry no uncertainty at all.

## 4. Editorial Decision

**Send for Review.** The flaws are revisable, not structural. Reviewers should adjudicate whether single-center ground truth supports field-level claims, whether the Experiment 3 selection circularity weakens its central result, and whether the interaction model belongs in the main text.

*Steelmanned counterargument:* a reviewer favoring rejection could argue that an empirical anchor drawn from one hospital's annotation practice documents a Mannheim-specific labeling artifact rather than a general property of Sepsis-3, and that the Lancet Digital Health bar requires multi-site expert ground truth before the Abstract's conclusions are drawn this strongly.

## 5. Suggested Reviewer Expertise

Reviewers are needed with: (1) hands-on experience implementing Sepsis-3 SOFA/suspected-infection pipelines on EHR data (e.g., MIMIC/eICU cohort construction); (2) linear mixed-effects modeling and variance-component estimation applied to clinical measurement data; (3) transformer-based clinical time-series forecasting and sequence classification for ICU prediction tasks; (4) label noise, circularity, and consensus-definition validity in clinical machine learning; and (5) critical care medicine with direct ICU sepsis diagnosis and SOFA-scoring experience, ideally with exposure to SOFA-2 or Sepsis-3 revision efforts.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved rapidly on two fronts relevant here. First, definitional sensitivity: Cohen et al. (Sci Rep, 2024) showed sepsis-onset definition choice alone shifts AUROC by up to 6% on MIMIC-III; Alrawashdeh et al. (Crit Care Med, 2024) showed SOFA-calculation variants have negligible labeling impact, a finding this manuscript corroborates and extends. Second, ground-truth-based validation: Lindner et al. (J Transl Med, 2022) established the GTSQ expert-labeling framework this manuscript reuses, and Centner et al. (PLOS ONE, 2020) is the same Mannheim group's earlier probabilistic approach to consensus-definition validation. The October 2025 JAMA publication of SOFA-2 (Ranzani et al.) is current and correctly cited; the manuscript's finding that SOFA version contributes negligible variance is a timely, testable claim against this revision. Tranchellini et al. (npj Digital Medicine, 2026) recently examined distribution shift in deployed sepsis models across sites, a complementary but distinct problem from the label-definition variability addressed here. This manuscript's distinguishing contribution is combining the full six-dimension implementation space with expert-anchored validation and downstream model training in one study; competing work has addressed onset-definition sensitivity or SOFA-version sensitivity in isolation, not the joint decomposition offered here. The authors should more directly engage the Centner et al. and Alrawashdeh et al. lines, both from closely related groups, to clarify incremental positioning beyond restating them in the Discussion.

## 7. Suggested Reviewer Names

**Sepsis-3/EHR implementation methodology:** Michael Moor; Supreeth P. Shashikumar; Franz-Simon Centner (Mannheim group, close prior-art overlap — disclose if invited); Marzyeh Ghassemi (broader clinical-AI label-validity relevance).

**Mixed-effects / measurement-theoretic statistics:** Erin Craig; a biostatistics-track assistant professor with applied LMEM/variance-components publication record in clinical epidemiology (name not independently verifiable from available search; flag to editorial staff for direct database query).

**Transformer/time-series clinical forecasting:** Sindhu Tipirneni; Satya Narayan Shukla; Michael Staniek is a co-author and excluded.

**Critical care / SOFA and sepsis diagnosis:** Manu Shankar-Hari (SOFA-2 consensus author); Hallie C. Prescott (sepsis definition and epidemiology); Christopher W. Seymour (original Sepsis-3 clinical-criteria co-author, full professor — last-resort option per reviewer-seniority preference).

---

## Further Literature (2023–2026)

1. **Dutta S, McMurry R, Tasi MC, et al. Performance of a Sepsis Prediction Model Across Different Sepsis Definitions. *JAMA Network Open* 9(4):e265599 (2026).** DOI: 10.1001/jamanetworkopen.2026.5599. Peer-reviewed. **Not cited by the manuscript.** Fully independent. The most important omission. A 198,494-encounter, nine-hospital silent deployment of a commercial gradient-boosted sepsis model evaluated against Sepsis-3, SEP-1, and CDC Adult Sepsis Event, with AUROC ranging 0.85–0.94 and AUPRC 0.11–0.24 depending on outcome definition alone. This is the deployed-model analogue of the manuscript's Experiment 3, at two orders of magnitude greater scale, and it demonstrates that definition-induced performance swings persist in production systems. The authors must engage it.

2. **Cohen SN, et al. Subtle variation in sepsis-III definitions markedly influences predictive performance within and across methods. *Scientific Reports* 14:1–10 (2024).** DOI: 10.1038/s41598-024-51989-6. Peer-reviewed. Cited (ref. 41). Independent. The closest direct precedent: three onset-definition interpretations on MIMIC-III, showing 0–6% AUROC variation exceeding inter-model variation. The manuscript's incremental claim rests on generalizing from one axis to six and adding expert ground truth.

3. **Alrawashdeh M, Klompas M, Rhee C. The Impact of Common Variations in Sequential Organ Failure Assessment Score Calculation on Sepsis Measurement Using Sepsis-3 Criteria. *Critical Care Medicine* 52:1380–1390 (2024).** DOI: 10.1097/CCM.0000000000006338. Peer-reviewed. Cited (ref. 19). Independent. Directly corroborates the manuscript's finding that data-imputation and SOFA-calculation choices contribute negligible variance, and should be used to sharpen rather than merely echo that result.

4. **Ranzani OT, Singer M, Salluh JIF, et al. Development and Validation of the Sequential Organ Failure Assessment (SOFA)-2 Score. *JAMA* 334(23):2090–2103 (2025).** DOI: 10.1001/jama.2025.20516. Peer-reviewed. Cited (ref. 14). Independent. Federated analysis across 1,319 ICUs in nine countries. The manuscript's claim that SOFA-1 versus SOFA-2 contributes trivial labeling variance is a strong, falsifiable statement against this revision and deserves explicit framing as such.

5. **Cabitza F, Jurman G, Molinari F, Bellazzi R. Why almost all ML models for medicine are wrong — and what we need for evidence-based medical AI. *International Journal of Medical Informatics* 219:106538 (2026).** DOI: 10.1016/j.ijmedinf.2026.106538. Peer-reviewed. Cited (ref. 18). Independent. Provides the conceptual scaffolding the manuscript invokes (variability as structural, not exceptional). Currently cited in passing; it warrants substantive engagement given how closely its thesis matches the manuscript's.

6. **Moor M, et al. Predicting sepsis using deep learning across international sites: a retrospective development and validation study. *eClinicalMedicine* 62:102124 (2023).** DOI: 10.1016/j.eclinm.2023.102124. Peer-reviewed. Cited (ref. 43). Independent. Source of the *Multiple Antibiotics* SI-Definition used for eICU. Also the strongest existing multi-site external-validation design in this space — a useful contrast against the manuscript's single-site ground truth.

7. **Tranchellini F, et al. Evaluating deep learning sepsis prediction models in ICUs under distribution shift: a multi-centre retrospective cohort study. *npj Digital Medicine* 9:306 (2026).** DOI: 10.1038/s41746-026-02364-4. Peer-reviewed. Cited (ref. 59). Independent. *Citation details taken from the manuscript's reference list; not independently confirmed against the publisher record — verify before use.* Addresses covariate/label shift across sites, the complementary failure mode to the label-definition variance studied here.

8. **Staniek M, Fracarolli M, Hagmann M, Riezler S. Early Prediction of Causes (not Effects) in Healthcare by Long-Term Clinical Time Series Forecasting. *PMLR* 252:1–29, MLHC (2024).** DOI: 10.48550/arXiv.2408.03816. Peer-reviewed conference proceedings (MLHC 2024); an arXiv version also exists. Cited (ref. 56). **Not independent** — Staniek and Riezler are authors on the submitted manuscript, and this supplies the transformer architecture for Experiment 3. Self-citation of the model backbone is legitimate but should be flagged in the competing-interests review, and reviewers should confirm the architecture transfer is described sufficiently for independent reproduction.

9. **Sepsis prediction combining machine learning and physiological network models. *Frontiers in Network Physiology* 6 (2026).** DOI: 10.3389/fnetp.2026.1852577. Peer-reviewed. Not cited. Independent. *Author list not independently verified — confirm before citing formally.* Explicitly frames incomparability and limited reproducibility arising from undisclosed and heterogeneous task definition and preprocessing as the field's central obstacle — the same diagnosis the manuscript makes, reached from a different methodological direction.

10. **Bomrah S, et al. A scoping review of machine learning for sepsis prediction — feature engineering strategies and model performance: a step towards explainability. *Critical Care* 28:180 (2024).** DOI: 10.1186/s13054-024-04948-6. Peer-reviewed. Cited (ref. 8). Independent. One of the four reviews used to construct the 68-publication screening frame. Reviewers should verify that the 30-of-68 inclusion decision is reproducible from these four sources, since Table 1 — the manuscript's taxonomic foundation — depends entirely on it.

**Editorial integrity note (handling editor only).** Two items warrant checking. First, the manuscript is not flagged as a preprint anywhere in the submitted text; the GitHub repository `StatNLP/sepsis3-inconsistent-measuring-model` could not be resolved through search, so its public availability and any accompanying preprint deposit should be confirmed before review. Second, the SepsisExp cohort (Lindner et al. 2022; Schamoni et al. 2022) has now supported at least three publications from overlapping author groups; reviewers should be asked whether the present analysis constitutes an independent contribution or an extension within a single-cohort publication series.

067148
## Editorial Report — LOVEKIDS: Infant Motor Assessment and Multi-Domain Clinical Prediction via 3D Pose Estimation from Monocular Video

## 1. Overall Assessment

LOVEKIDS reconstructs infant 3D body mesh and kinematics via a swing–twist inverse-kinematics extension of SMIL, feeding a Transformer-based classifier for CP screening, DDH screening, and PIM regression across an 11,938-infant multicenter cohort. Pose-estimation gains are real (MPJPE 20.9/35.1 mm on MINI-RGBD/SyRIP, outperforming HybrIK and SPIN), and DDH/PIM are genuinely novel video-based applications.

The headline CP result (AUC 0.968) is not the advance it is presented as. The same senior authors (Yao, Lu, Yu) published a fidgety-movement CP-screening model in *Nature Communications* (2023, Gao et al., AUC 0.967, same institutional network) cited here only as an anonymous third-party comparator. This undisclosed self-overlap dominates the decision below.

## 2. Strengths

The swing-twist formulation is a credible anatomical adaptation of HybrIK to infant biomechanics, validated by a Chamfer Distance of 17.6 mm against RealSense L515 ground truth on 150 clinical infants. DDH and PIM prediction from monocular RGB are, to my knowledge, unprecedented, and Figure 6a's kinematic grounding (elevated hip/knee/ankle jerk variability in DDH-risk infants) gives the DDH result mechanistic plausibility. The two-round, washout-controlled reader study (15 senior, 15 junior physicians) is sound trial design, uncommon in this literature.

## 3. Weaknesses

Absent disclosure of cohort overlap and architectural increment relative to Gao et al. (2023), the CP result reads as salami-sliced rather than novel. The prospective cohort contains only 6 confirmed CP cases among 99 infants; sensitivity of 1.000 ± 0.000 with PPV 0.545 ± 0.150 reflects statistical fragility, not reliability, and is not flagged as such. DDH performance (AUC 0.829) lacks any comparison against known clinical risk factors (breech, family history) already in Table 2, so incremental value over existing screening is unestablished. The cited code repository could not be located, and the prospective registration number does not match standard formatting.

## 4. Editorial Decision

**Reject.** The CP claim cannot be assessed for novelty without full disclosure of its relationship to the authors' own 2023 paper — this requires re-scoping, not revision. DDH and PIM components have merit and could anchor a resubmission if the CP claim is removed or transparently reconciled with the prior work.

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in: parametric 3D human/infant body models and inverse kinematics (SMPL/SMIL-family methods); multi-instance learning for weakly-labeled video classification; spatiotemporal Transformer architectures for skeletal time-series; pediatric General Movements Assessment and its automation; and pediatric orthopedic diagnosis of developmental dysplasia of the hip, specifically ultrasound/Graf-method classification standards.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The dominant recent trend in automated GMA is multimodal sensor fusion rather than vision-only pipelines: Kulvicius et al. (Communications Medicine, 2023) demonstrated pressure-distribution-based infant movement classification, and a 2024 arXiv sensor-fusion study (Kulvicius et al.) combined accelerometry with video to improve on vision-only baselines. On the pose-estimation side, Zhou et al.'s ZeDO (WACV 2024) and Chopard et al.'s uncontrolled-setting GMA pipeline (ICLR 2025 workshop) both push toward deployment in non-standardized, home-recorded video — a generalizability axis this manuscript does not test, since its cohort was captured under fixed-camera clinical conditions exclusively. The single most consequential omission is Gao et al. (Nat Commun, 2023), cited here as an unrelated comparator at AUC 96.7% (line 104) when it is, in fact, the same author group's own prior CP-screening system on an overlapping patient network; any credible state-of-the-art positioning of this manuscript must directly reconcile the two papers' cohorts, methods, and claimed increments rather than treating the earlier work as external prior art.

## 7. Suggested Reviewers

**3D infant pose estimation / parametric body models:** Sarah Ostadabbas (Northeastern University); Nikolas Hesse (SMIL model originator); Bernhard Kainz group (Imperial College London, infant pose estimation from limited annotations).

**Multimodal/sensor-fusion movement classification:** Tomas Kulvicius (University of Göttingen); Daphné Chopard (ETH Zürich).

**Pediatric GMA / clinical neurodevelopmental screening:** Lars Adde (Norwegian University of Science and Technology, GMA implementation studies); a pediatric orthopedic surgeon with DDH ultrasound-screening expertise, to be identified via institutional DDH-registry authorship independent of the SJTU network.

---

**EDITORIAL INTEGRITY ALERT — FOR HANDLING EDITOR ONLY, NOT FOR AUTHOR TRANSMISSION**

Flagging for your review before any further processing: (1) Undisclosed cohort/author overlap with Gao, Q., Yao, S., Tian, Y. et al., *Nat Commun* 14, 8294 (2023) — Siqiong Yao (co-first author here) and Hui Lu / Guangjun Yu (corresponding/senior authors here) are co-authors of that prior paper, which performs the same FM-based CP-screening task on the same institutional network with near-identical external AUC. The current manuscript cites this only as ref. 24, framed as third-party related work, with no statement of author overlap, competing-interest disclosure, or cohort-reuse accounting. This should be resolved directly with the corresponding author before proceeding. (2) The GitHub repository cited for code availability (github.com/tylerzhang77/LOVEKIDS) could not be located via search; verify it is live and public prior to any acceptance decision. (3) The prospective trial registration number "2024087" does not conform to ChiCTR or ClinicalTrials.gov formatting conventions; request the full registry and accession format from the authors. (4) The n=99 prospective CP cohort has only 6 positive cases; the reported sensitivity of 1.000 ± 0.000 should be scrutinized for overstatement given this base rate before it is permitted to stand as a headline result.

066986
## 1. Overall Assessment

The manuscript defines "diagnostically quiescent regions" — subregions where imperceptible watermarking leaves diagnostic output unchanged — and validates this across four modalities, five tasks, and blinded reader studies with twelve specialists. The framework decomposes safety into three independently falsifiable invariance criteria: perceptual, computational, clinical.

Execution is rigorous. The novelty framing is not. The claim that prior medical watermarking assumed uniform spatial sensitivity is factually wrong, and an undisclosed authorial dependency on the cited base architecture compounds the concern.

## 2. Strengths

The three-tier invariance decomposition is operational rather than descriptive, and the paper explicitly treats anatomy-informed masks as a prior requiring empirical validation, not as proof.

The sensitivity sweep (Fig. 7) is genuinely falsifying: BUSI preserves hard-prediction accuracy (Δ = −1.5 pp) while its predictive distribution drifts substantially (KL = 0.39 at 4α₀), demonstrating the three criteria are non-redundant.

The train-from-scratch experiment addresses distributional shift in learned representations, not merely test-time inference — a scenario most watermarking papers omit.

## 3. Weaknesses

The assertion that prior medical watermarking applied frequency-domain embedding "uniformly across the image" is inaccurate. ROI/RONI watermarking, which confines embedding to non-diagnostic subregions, has been standard since at least Coatrieux et al. (2007) and spans dozens of papers, none cited. The genuine advance — multi-observer invariance testing with deep embedding across modalities — survives repositioning, but the current framing does not.

Reader studies are underpowered (n = 60–100 per modality; CIs spanning −25 to +19 pp). Pooled non-significance is not equivalence, and the between-image design cannot exclude image-level confounding.

Two co-authors (R. Hu, J. Zhang) are authors of MaskWM, the architecture this work adapts. This is not disclosed as distinct from ordinary prior art.

## 4. Editorial Decision

**Send for Review**, requiring major revision. Reviewers should adjudicate: whether the framework advances beyond ROI/RONI once fairly positioned; whether reader-study power supports the clinical-invariance claim; and whether the MaskWM overlap constitutes a disclosure gap.

## 5. Suggested Reviewer Expertise

Deep-learning-based image watermarking and steganography (encoder–decoder architectures, robustness under differentiable distortion layers); ROI/RONI and region-selective medical image watermarking specifically; ophthalmic AI validation (OCT and fundus grading, inter-reader variability in DR staging); statistical methodology for diagnostic non-inferiority and equivalence testing in multi-reader studies; and regulatory science for AI/ML-enabled medical devices (FDA GMLP, EU AI Act data-provenance requirements).

## 6. State-of-the-Art Literature Review (Past 3 Years)

Natural-image deep watermarking has advanced rapidly via encoder–decoder frameworks with learned robustness to distortion layers, including WAM (Sander et al., 2025) for local/regional watermarking and MaskWM (Hu et al., NeurIPS 2025), which this manuscript directly adapts. Separately, medical image watermarking research has continued to iterate on classical ROI/RONI and reversible-watermarking paradigms (e.g., 2025 Scientific Reports papers on chaotic-system and dual-watermarking frameworks for e-health), generally without deep validation against downstream AI model behavior or clinician reader studies. This manuscript's genuine contribution is bridging these two threads — applying a modern, robust encoder–decoder architecture to anatomically informed regions and validating against both AI models and blinded human readers — a combination rarely attempted with this rigor. However, the manuscript should engage directly with the ROI/RONI literature rather than presenting uniform-sensitivity embedding as the field's default assumption, and should discuss how its invariance criteria relate to non-inferiority frameworks already used in diagnostic-AI device comparisons.

## 7. Suggested Reviewers

**Watermarking/deep learning:** Nils Lukas; Pierre Fernandez; Tu Bui; Vedrana Andersen Dahl.

**ROI/RONI medical watermarking:** Gouenou Coatrieux; R. Eswaraiah; Aikaterini-Efstathia Giakoumaki.

**Ophthalmic AI validation:** Aaron Lee; Cecilia Lee; Zhaoran Wang.

**Regulatory/statistical methodology:** Alastair Denniston; Xiaoxuan Liu.

## Further Literature (2023–2026)

**1. Sander, T., Fernandez, P., Durmus, A., Furon, T. & Douze, M. Watermark Anything with Localized Messages. ICLR 2025, pp. 45800–45830. arXiv:2411.07231.**
Venue: ICLR (peer-reviewed conference). Cited by manuscript: **No.** Author independence: fully independent (Meta FAIR / Inria). Relevance: WAM is the direct competitor to MaskWM for localized watermarking and extracts 32-bit messages from regions under 10% of image area at 256×256 — the same payload and resolution regime used here. Its omission is a material gap; the authors compare against no localized-watermarking baseline at all.

**2. Hu, R., Zhang, J., Zhao, S., Lukas, N., Li, J., Guo, Q., Qiu, H. & Zhang, T. Mask Image Watermarking. NeurIPS 2025. arXiv:2504.12739.**
Venue: NeurIPS (peer-reviewed). Cited by manuscript: Yes (ref. 12). Author independence: **No — R. Hu and J. Zhang are co-authors of the manuscript under review.** Relevance: the architectural base ("inspired by MaskWM"); the RGB backbone checkpoint is taken directly from this work. This dependency should be disclosed explicitly rather than cited as neutral prior art.

**3. Longpre, S. et al. A large-scale audit of dataset licensing and attribution in AI. Nature Machine Intelligence 6, 975–987 (2024). DOI: 10.1038/s42256-024-00878-8.**
Venue: Nature Machine Intelligence (peer-reviewed). Cited: Yes (ref. 3). Independent: Yes. Relevance: source of the >70% licence-omission / >50% error statistics motivating the manuscript. Note this audit covers **text** datasets, not imaging — the manuscript's framing at lines 71–73 blurs this and should be corrected.

**4. Jiménez-Sánchez, A. et al. Copycats: the many lives of a publicly available medical imaging dataset. Advances in Neural Information Processing Systems 37, 113383–113404 (2024).**
Venue: NeurIPS Datasets & Benchmarks (peer-reviewed). Cited: Yes (ref. 4). Independent: Yes. Relevance: documents ISIC proliferation across Kaggle (640 derivative datasets, 2.35 TB from a 38 GB original) with missing licences — the strongest empirical case for image-level provenance in this literature and the manuscript's best motivating citation.

**5. Chaudhary, H., Garg, P. & Vishwakarma, V.P. Enhanced medical image watermarking using hybrid DWT-HMD-SVD and Arnold scrambling. Scientific Reports 15, 9710 (2025).**
Venue: Scientific Reports (peer-reviewed). Cited: Yes (ref. 15). Independent: Yes. Relevance: representative of the transform-domain medical watermarking the manuscript characterises as the field default. Useful as a fidelity benchmark, though it reports no downstream AI or reader validation.

**6. Liu, Z., Li, J. & Nawaz, S.A. A watermarking framework for encrypted medical images via HC chaotic system and deep learning. Scientific Reports 15, 35851 (2025). DOI: 10.1038/s41598-025-19790-1.**
Venue: Scientific Reports (peer-reviewed). Cited: **No.** Independent: Yes. Relevance: zero-watermarking via DWT-ResNet-DCT, explicitly motivated by leakage and tampering of shared medical imaging — the closest recent competitor on problem framing. A zero-watermarking approach modifies no pixels at all, which is arguably a stronger diagnostic-safety guarantee than the manuscript's; the trade-off (no persistence through redistribution) deserves discussion.

**7. Lightweight dual-watermarking framework for medical image authentication and integrity preservation. Scientific Reports (2025). DOI: 10.1038/s41598-025-30615-z.**
Venue: Scientific Reports (peer-reviewed). Cited: **No.** Independent: Yes. Relevance: directly addresses the diagnostic-quality constraint the manuscript claims has blocked adoption, and surveys context-encoder zero-watermarking approaches. Its existence undercuts the "long been avoided" framing at line 41.

**8. Singh, — et al. A Novel Deep Learning Based Dual Watermarking System for Securing Healthcare Data. Computational Intelligence 41 (2025). DOI: 10.1111/coin.70011.**
Venue: Computational Intelligence, Wiley (peer-reviewed). Cited: **No.** Independent: Yes. Relevance: LWT plus a Hybrid Convolutional Cascaded Capsule Network for medical watermarking; representative of deep-learning medical watermarking already in the literature, which the manuscript's Discussion implies does not exist.

**9. Deep learning-based dual watermarking solution for securing medical images in e-healthcare. Knowledge-Based Systems (2025). DOI: 10.1016/j.knosys.2025.114686 (article S0950705125017885).**
Venue: Knowledge-Based Systems, Elsevier (peer-reviewed). Cited: **No.** Independent: Yes. Relevance: **Uses Grad-CAM attention maps for perceptual guidance of embedding placement.** This is close prior art for the manuscript's own "future direction" of automated quiescent-region discovery via saliency maps, and closer still to the anatomy-guided placement concept than any work the authors cite. This is the single most important omission after WAM.

**10. Survey on Adversarial Attack and Defense for Medical Image Analysis: Methods and Challenges. ACM Computing Surveys (2024). DOI: 10.1145/3702638.**
Venue: ACM Computing Surveys (peer-reviewed). Cited: **No.** Independent: Yes. Relevance: establishes that imperceptible perturbations reliably flip medical classifier predictions — the exact premise the manuscript must refute. Engaging this literature would strengthen, not weaken, the paper: the authors' non-adversarial threat model is defensible, but currently the distinction is asserted rather than argued against the relevant evidence base.

---

**Note on preprint status:** all ten are peer-reviewed. Items 1, 2 and 4 have arXiv versions predating publication; cite the conference proceedings versions, not arXiv. The manuscript's own reference 19 (Wang, Y.-C.C. et al., arXiv:2502.10277) is preprint-only and must be flagged as unreviewed, since it is used to justify the 5–10 pp non-inferiority margin the authors position their ±2 pp band against.

**Editorial integrity alerts (handling editor only):** (i) MaskWM authorial overlap, as above, absent from the competing-interests statement; (ii) Table 1 reports fundus SSIM 0.9905 ± 0.0050, which places one standard deviation below the 0.99 perceptual-invariance threshold the framework requires — the abstract's "SSIM > 0.99" claim is not supported at the distributional level for this modality; (iii) code availability is deferred to "upon acceptance," which is below Nature Communications policy for a methods paper of this type.

066894
# Editorial Integrity Alert — For Handling Editor Only

Independent verification identified a serious undisclosed-overlap concern. The corresponding/co-author Ligang Jiang (Quzhou Affiliated Hospital of Wenzhou Medical University) has, within the same calendar year, published at least two methodologically near-identical benchmarking studies using the same blueprint-guided, matched-task, five-LLM, 60-task/300-item design: "Evaluating large language models for diabetic retinopathy multiple-choice question generation in clinical ophthalmic education" (*Front Med* 2026, doi:10.3389/fmed.2026.1874243) and "Benchmarking publicly accessible large language models for high-myopia multiple-choice question generation in digital ophthalmic education and public health training" (*Front Public Health* 2026, doi:10.3389/fpubh.2026.1843045). Both share the identical four-domain/15-task blueprint structure, the same six expert-rating domains, the same objective-indicator taxonomy, the same statistical pipeline (Friedman/Wilcoxon/ICC/Spearman), and near-identical Discussion prose. The submitted glaucoma manuscript is a third iteration of this template with the disease label substituted. Neither prior publication is disclosed or cited despite obvious relevance to novelty and shared senior authorship. This is a salami-slicing/non-disclosure concern to be raised with the authors independent of the scientific review below.

---

## 1. Overall Assessment

The manuscript benchmarks five LLMs on generating glaucoma MCQs against a prespecified 60-task blueprint, layering objective metrics, blinded expert Likert ratings, and a 10-resident pilot validation. Its claim — that structural completeness and answer accuracy are insufficient proxies for educational value — is reasonable but not novel; it is a template application, not a methodological advance, given the undisclosed prior DR and high-myopia iterations by the same senior author.

## 2. Strengths

The paired task-level design (all five models complete identical tasks) is analytically sound, using Friedman tests with Bonferroni-corrected pairwise comparisons, avoiding unmatched-content confounds. Inter-rater agreement is respectable (ICC 0.815–0.871). The phenotype-stratified analysis across open-angle, angle-closure, secondary, and diagnostically uncertain scenarios is a reasonable generalizability test.

## 3. Weaknesses

The learner validation (10 residents, 50 items, no control, single administration) is descriptive usability feedback, not psychometric validation, though occasionally framed as more. Glaucoma is fundamentally image- and data-dependent (OCT, visual fields, gonioscopy), yet image-based items are explicitly prohibited, sidestepping the discipline's highest-stakes content. Response time conflates platform/network conditions with inference speed. Correctness was adjudicated by the same team that wrote the reference key, with no external arbitration — a circularity risk for the primary hard outcome.

## 4. Editorial Decision

**Reject.** The undisclosed near-duplicate publication pattern is disqualifying pending resolution, and the underlying design — single-administration, no-control, text-only benchmarking — does not independently clear the required bar. **Steelman:** repeated blueprint application across disease domains could be framed as legitimate generalizability replication, but this collapses without disclosure of the prior instances.

## 5. Suggested Reviewer Expertise

Reviewers should include an expert in automatic item generation and psychometric validation of AI-generated assessment content (item discrimination, IRT calibration); a medical education researcher with experience in MCQ validity studies (item-writing flaw detection, cognitive-level alignment); an NLP/LLM evaluation methodologist familiar with prompt-engineering confounds and benchmarking reproducibility; and a glaucoma subspecialist with residency-training and OCT/visual-field teaching responsibility to assess whether text-only items adequately represent the discipline's diagnostic core.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved past simple structural-completeness benchmarking. Kıyak and Emekli's 2024 review of ChatGPT-prompt MCQ generation established that validity evidence, not generation fluency, is the open problem, and follow-up work by the same group examined item discrimination and difficulty in anatomy MCQs specifically. Gholami et al. (*JAMA Ophthalmol* 2025) showed GPT-4-generated board-style ophthalmology MCQs reaching quality parity with human writers only after expert revision, directly anticipating this manuscript's conclusion. Linde et al. (*npj Digit Med* 2026) pushed further into psychometric detectability of GPT-4o-generated items across imaging specialties, a level of rigor (item response theory, discrimination indices) this manuscript does not attempt despite having resident data that could support it. The submitted manuscript replicates the Kıyak/Gholami-era finding that structural completeness outpaces content reliability, without engaging the more recent psychometric-validation literature its own dataset could support, and without acknowledging its own group's prior identical exercises in DR and high myopia.

## 7. Suggested Reviewers' Names

Item-generation/psychometrics: Yavuz Selim Kıyak; Fatima I. Jackson (Acad Med clinical-vignette MCQ work).
Medical education/LLM benchmarking: Michael J. Borowitz (pathology MCQ generation, *Mod Pathol* 2025); Philip Linde (NPJ Digit Med psychometric detectability study).
Ophthalmology/glaucoma clinical: a glaucoma-subspecialist associate professor with residency curriculum responsibility, to be identified via the manuscript's own cited PAAO/EGS guideline authorship networks given no independently verifiable candidate emerged from this search.

066728
# Editorial Report — "Can artificial intelligence narrow quality gaps among ultrasound physicians? Province-wide multicenter real-world evidence from a resource-limited setting"

---

## EDITORIAL INTEGRITY ALERT (Handling Editor Only)

**Undisclosed overlapping publication / possible salami-slicing.** Reference 14 (Zhao, Tang, Li, et al., *BMC Med* 2026;24(1), DOI 10.1186/s12916-026-04768-1, already published) is by an almost identical author group (Jianxin Zhao, Yao Tang, Ke Wang, Jing Tao, Chunyi Chen, Lang Cui, Yuji Wang, Cheng Huang, Zheng Liu, Hong Kang, Shengli Li, Jun Zhu), describing the same AI-QC platform deployed in the same province (Guizhou), evaluated over an overlapping period. The preprint version of that paper (SSRN 5618314) describes 72,373 examinations across 49 hospitals and 255 sonographers (September 2020–May 2025), spanning first-trimester, biometry, anomaly, and standard scans. The present manuscript restricts itself to NT/CRL first-trimester images (October 2021–March 2026, 43 hospitals, 185 physicians) and adds CRL geometry and NT-MoM calibration analyses. The manuscript does not cite or differentiate itself from reference 14 anywhere in the text despite near-total overlap in platform, geography, and cohort window. This is a cohort-reuse and salami-slicing concern that must be resolved before any further processing: request that authors explicitly disclose the relationship between the two cohorts, quantify the degree of case-level overlap, and justify why this constitutes a distinct contribution rather than a reslicing of the same dataset.

**Numerical inconsistency requiring verification.** The Results text (lines 246–247) reports the robust SD of log10(MoM) as ranging 0.058–0.068, but Figure 10 plots robust SD values visually clustering between approximately 0.09 and 0.15 across all groups, none of which appear to fall in the stated range. This should be checked against the underlying data before proceeding. The magnification gap for secondary-level hospitals is also reported inconsistently: text states baseline gap "10.5" points and secondary-level increase "+10.4" points, but the source figures (46.3% to 56.8%) yield a 10.5-point increase, not 10.4. Minor, but indicative of insufficiently checked arithmetic in a manuscript otherwise reliant on precise point estimates.

**Ethics approval number.** The IRB approval number (2019YFS0530) predates the platform's stated deployment start (October 2021) by two years and follows a format resembling a national research-grant code rather than an institutional ethics approval number. Authors should be asked to confirm this is the correct, currently valid ethics approval covering the full 2021–2026 data-collection window.

---

## 1. Overall Assessment

This retrospective study evaluates a cloud-based AI-QC system across 43 Guizhou hospitals, testing whether it narrowed secondary–tertiary gaps in first-trimester NT/CRL image quality. Across 41,187 images from 24,698 cases, quality scores converged (secondary–tertiary gap: 17.8→1.8 points NT, 22.9→2.8 CRL within one year) and CRL geometry improved, but NT-MoM bias stayed below the 0.9–1.1 target throughout. The core claim — acquisition standardization without bias correction — is meaningful and not oversold. Two issues dominate: undisclosed cohort/platform overlap with an already-published companion paper by the same group (ref. 14), and a self-selected, observational exposure definition vulnerable to secular trends and regression to the mean.

## 2. Strengths

Deployment scale is real: five years of data across all nine Guizhou prefectures, with adoption timing operationalized via a defensible forward-looking upload-volume algorithm rather than naive calendar anchoring. The three-domain framework — quality score, CRL geometry, NT-MoM calibration — cleanly separates "standard-looking" from "accurate"; the divergence between them (quality converges, bias persists) is the paper's most defensible finding. The FMF-certified reference center (Fig. 10) gives the NT bias external validity.

## 3. Weaknesses

The undisclosed overlap with reference 14 — same platform, province, cohort window, near-identical authorship — is the most serious problem. The adoption definition encodes untested selection bias: physicians reaching sustained upload volume are plausibly more engaged or supervised, which alone could produce "improvement" without AI causation; no falsification test is reported. The NT-MoM trajectory in secondary hospitals is non-monotonic (0.795→0.725→0.834), unexplained mechanistically. Only physician-selected images were analyzed, with no capture-rate quantification against total examinations.

## 4. Editorial Decision

**Reject.** Undisclosed overlap with an already-published companion paper is an integrity concern requiring direct clarification before further consideration. Independently, the self-selected exposure and unexplained non-monotonic NT-MoM trajectory are limitations a major revision is unlikely to fix, since the exposure cannot be retrospectively randomized.

**Steelman counterargument.** This manuscript arguably asks a distinct question from ref. 14 — geometry- and calibration-specific outcomes with ten more months of data — and merits publication if the cohort relationship is disclosed and self-selection addressed via sensitivity analysis.

## 5. Suggested Reviewer Expertise

Reviewers should have direct expertise in: (1) AI-based ultrasound image-quality auditing and deployment in real-world clinical workflows; (2) first-trimester NT/CRL measurement standardization, calibration, and quality-assurance programs (MoM-based audit methodology); (3) causal inference and confounding in observational, non-randomized digital-health implementation studies, particularly self-selected exposure definitions; (4) province- or national-scale health-system deployment of clinical decision-support tools in low-resource settings; and (5) obstetric ultrasound practice standards and ISUOG first-trimester scan guidelines to assess clinical plausibility of the reported deficiency categories.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Real-world AI-QC deployment for obstetric ultrasound has moved rapidly from algorithm development to field evaluation. Cao et al. (BMC Pregnancy Childbirth, 2025) reported a deep-learning AI-IQA system audited across the four key first-trimester planes with demonstrated clinical impact on auditing efficiency. Chen, He, Lei, Wang et al. (npj Digital Medicine, 2025) developed and deployed the First Trimester Ultrasound Quality-control System (FUQS) across Liaoning Province using 41,968 images from 7,251 pregnancies — a near-identical province-scale design to the present manuscript, and a direct comparator the authors do not cite or engage with. Tan et al. (BMC Medical Education, 2024) conducted a prospective cost-effectiveness comparison of AI versus manual QC in perinatal ultrasound. Outside China, He, Wang, and Yaqub (MBZUAI, 2025) applied a vision-language foundation model (FetalCLIP) with LoRA adaptation for blind-sweep fetal ultrasound IQA in low-resource settings, and Gomes et al. (Google Health/Zambia, 2022–2023) developed an AI system for fetal ultrasound biometry specifically targeting low-resource obstetric care.

Against this landscape, the present manuscript's contribution is incremental rather than novel in method: it applies an already-deployed platform (shared with ref. 14) to a slightly different image subset and adds geometry and MoM-calibration outcomes not present in the FUQS or Cao papers. Its distinguishing empirical finding — that image-acquisition standardization does not translate into measurement-bias correction — is genuinely underexplored in this literature and, if the integrity concerns above are resolved, would be the paper's most citable contribution. The authors should be required to directly engage with FUQS (Chen et al., npj Digital Medicine 2025) as the closest methodological and geographic comparator, and to explain what their study adds beyond it and beyond their own reference 14.

## 7. Suggested Reviewers

**Technical/methodological:**
- Mohammad Yaqub (Associate Professor, MBZUAI) — fetal ultrasound image-quality assessment using foundation models in low-resource settings (He, Wang, Yaqub, FetalCLIP-based IQA, 2025).
- Lizhu Chen / Fujiao He (co-first authors, Liaoning FUQS system) — province-scale first-trimester ultrasound quality-control deployment directly comparable in design (npj Digital Medicine, 2025).
- Xiaoyan Cao / Binghan Li — deep-learning first-trimester image-quality auditing with demonstrated clinical impact (BMC Pregnancy Childbirth, 2025).
- A biostatistician with expertise in interrupted time-series or difference-in-differences methods for non-randomized digital-health exposure definitions, to adjudicate the physician self-selection concern.

**Clinical:**
- Ranjit Akolekar (Associate Professor, Medway/King's College Hospital) — NT audit, feedback, and image-quality formative-assessment programs (Dobert, Wright, Akolekar et al., J Ultrasound Med 2013; ongoing FMF-affiliated NT quality-assurance work).
- Carmen Comas (Fetal Medicine Unit, Institut Universitari Dexeus) — operator-level NT-MoM quality analysis and FMF-certification effects on measurement accuracy.

066515
# Editorial Report: "Disentangling co-occurring pathology representations with generative deconfounded supervision in chest radiography"

**Authors:** Chen, Min, Han (Nanchang University)

---

## EDITORIAL INTEGRITY ALERT (Handling Editor Only — not for authors)

The manuscript's zero-shot baseline set in Figure 3 includes GAVLP, which is the authors' own prior model (Chen, R. et al., *Pattern Recognition* 171, 112263, 2026; reference [49]). GAVLP is also the source of the pseudo-report construction procedure used to build the M+C+C14 pretraining corpus for the submitted work (Methods 4.3). The manuscript does not disclose this author overlap when GAVLP is presented as an independent comparator method in Fig. 3a-c and 3e, nor in the Competing Interests statement, which states no competing interests. This is a comparator-independence failure requiring disclosure and, at minimum, a note in the baseline description. It does not by itself indicate fabrication, but it must be resolved before any further processing. No undisclosed preprint of this manuscript was located in independent searches. No cohort-reuse or salami-slicing concern was identified beyond the shared pretraining configuration with GAVLP, which appears to be legitimate iterative methods development rather than duplicate publication.

---

## 1. Overall Assessment

DisCo is a two-stage framework: a LoRA-adapted diffusion model generates class-balanced single-pathology chest radiograph-report pairs, and a label-conditioned bottleneck with one-way KL distillation transfers this disease-specific signal into a real multi-label vision-language model. The claim is that co-occurrence in observational CXR data confounds disease-specific representations, and that generative single-pathology anchors, transferred via a low-dimensional bottleneck rather than raw augmentation, attenuate this confounding while preserving genuine comorbidity.

The mechanistic decomposition (Figs. 4-5) is the strongest asset: synthetic data alone is nearly inert, and the gain is attributable specifically to bottleneck distillation, distinguishing this from typical augmentation studies. Disposition turns on two issues: the undisclosed GAVLP self-comparator noted above, and an entirely public-benchmark, retrospective evaluation that falls short of Lancet Digital Health-caliber clinical significance despite technical care.

## 2. Strengths

The co-occurrence-conditioned evaluation (Fig. 4) is disciplined: Target|Confounder pairs were fixed by a pre-specified lift criterion (Eq. 1) and minimum case count before analysis, foreclosing post hoc pair selection.

The component-wise ablation (Base, +Synthetic, +Dual-branch, DisCo) isolates architecture versus data versus distillation objective across five datasets (Fig. 5b) and three frequency strata (Fig. 5a), showing the bottleneck term, not synthetic volume, drives the gain (2.55-5.59 pp).

The independent off-target audit using a frozen TorchXRayVision classifier (Fig. 2d-e) is a credible external check on anchor specificity (Wilcoxon P = 4.88 × 10⁻⁴, 11 pathologies).

## 3. Weaknesses

All evaluation is confined to public benchmarks with no institution-level external cohort. Public CXR-label reliability is well documented as inconsistent (ref. [54] cited but not engaged with), and no prospective or held-out hospital validation is offered.

No subgroup analysis by age, sex, or acquisition device is reported, despite MIMIC-CXR and CheXpert both carrying demographic metadata permitting this at negligible cost — a material omission for a clinically-framed representation claim.

The single non-improving pair, Infiltration|Pneumonia (-0.5 pp), is dismissed as "near-synonymous," but this is precisely the case that should concern reviewers most: it suggests the mechanism may fail where clinical ontological overlap is real, and the paper does not stress-test this further.

The zero-shot comparator list omits recent large-scale generative CXR foundation models (e.g., billion-parameter rectified-flow synthesis), leaving novelty under-triangulated against the newest generative literature.

## 4. Editorial Decision

**Reject**, contingent on resolution of the GAVLP disclosure issue before resubmission; independent of that, evaluation scope (public retrospective benchmarks only, no demographic subgroup analysis, no external cohort) falls below this journal's clinical-significance bar and is not fixable within a standard revision cycle. Steelman: the mechanistic ablation is unusually rigorous and the co-occurrence-conditioned protocol is a genuine methodological contribution a computational venue would value without clinical deployment evidence.

## 5. Suggested Reviewer Expertise

Vision-language contrastive pretraining for medical imaging (CLIP-style architectures, InfoNCE objectives); latent diffusion model domain adaptation and LoRA fine-tuning for medical image synthesis; causal representation learning and deconfounding methods in computer vision; long-tailed and class-imbalanced multi-label classification; thoracic radiology with specific experience interpreting co-occurring pathology patterns (e.g., cardiopulmonary comorbidity, pleural-parenchymal overlap) on chest radiographs.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Medical vision-language pretraining for chest radiography has matured rapidly since KAD (Zhang et al., *Nature Communications*, 2023) and CXR-CLIP (You et al., 2023), both cited and used as baselines here. Since 2024, the field has moved toward (a) larger and more heterogeneous multi-source pretraining, exemplified by UniChest's conquer-and-divide strategy for cross-dataset heterogeneity, and (b) generative augmentation at greater scale, exemplified by a 2026 billion-parameter rectified-flow chest radiograph foundation model trained on 1.2M images with demographic-subgroup-controllable synthesis — a scale and controllability the present LoRA-adapted RoentGen approach does not approach and does not cite. Causal and disentanglement approaches to CXR co-occurrence (refs. [21]-[23], all 2023-2026) remain the closest conceptual predecessors; DisCo's contribution relative to this line is operationalizing deconfounding through generative single-pathology anchors plus bottleneck distillation rather than architectural disentanglement alone, which is a real but incremental methodological variation rather than a new evaluation paradigm. The manuscript should engage more directly with fairness-aware disentanglement work in CXR (e.g., recent PEFT-based fairness approaches for chest X-ray diagnosis), given the complete absence of demographic evaluation noted above.

---

## Suggested Reviewer Names

**Vision-language pretraining for medical imaging:** Zhihong Chen (Johns Hopkins); Xiaoman Zhang (Shanghai AI Laboratory, co-author of KAD); Che Liu (Imperial College London); Tianjie Dai (Shanghai Jiao Tong University, UniChest).

**Diffusion-based medical image synthesis / LoRA domain adaptation:** Fabio De Sousa Ribeiro (Imperial College London); Christian Bluethgen (co-author, RoentGen — note: as originator of the base generator, disclose and assess independence before inviting); Emma A. M. Stanley (Imperial College London).

**Causal/disentangled representation learning in CXR:** Wenrui Nie (author of ref. [23], causal-perspective CXR classification); Qingyu Li (author of ref. [21], category-disentangled causal learning) — verify independence from submitting group before inviting.

**Thoracic radiology / clinical CXR interpretation:** a board-certified thoracic radiologist with published experience in comorbid-finding interpretation and CXR dataset annotation quality (e.g., contributors to the RSNA Pneumonia Detection or SIIM-ACR Pneumothorax challenge panels); a clinical epidemiologist with experience in AI fairness auditing across demographic subgroups in imaging cohorts.

066472
# Editorial Report

**Manuscript:** Redistributing the benefits of collaborative critical-care AI across data-unequal hospital sites
**Corresponding author:** Zitong Yu (Great Bay University)

---

## 1. Overall Assessment

The manuscript defines collaboration benefit as the site-level held-out AUROC gain over an architecture-matched local-only model, shows that FedAvg and FedProx concentrate this gain in higher-resource eICU sites, and proposes BRIDGE — shared–private representation learning, latent stream completion, and reliability-adjusted benefit-aware aggregation under a −0.01 mean-AUROC non-inferiority margin. Across 52,430 stays at 20 sites, BRIDGE raises Q1 uplift from 0.025 to 0.041, worst-site AUROC from 0.608 to 0.740, and cuts negative transfer from 11.4% to 3.1%.

The estimand is a genuine, reusable evaluative construct. Two concerns dominate: the redistribution endpoint rests on five sites within a single database, and the aggregation mechanism is inadequately separated from existing contribution-allocation work.

## 2. Strengths

The site-anchored estimand is inexpensive, method-agnostic, and retrofittable onto any existing federated study without redesign.

The training signal and reported endpoint are kept disjoint by patient-level partition: round-wise benefit on the aggregation-validation split, checkpoints on a separate split, held-out test untouched. This avoids the circularity that would otherwise invalidate the result.

The robustness program is unusually thorough — 1,000 resampled configurations, leave-one-Q1-site-out, five local-only reference specifications including an XGBoost comparator that beats collaboration at 3 of 20 sites, a parameter-matched completion ablation, and replication across four tasks.

Four personalized baselines (FedPer, FedRep, Ditto, FedProx-FT) reach at most 56% of BRIDGE's Q1 uplift, discriminating redistribution from personalization.

## 3. Weaknesses

The Shapley-value and incentive-mechanism literature — which targets the identical unequal-return problem — is entirely uncited.

Q1 uplift has n=5 and worst-site AUROC n=1 per seed; the abstract's language outruns this.

The SDR score measures data completeness, not hospital resource level, yet the title invokes "data-unequal hospital sites."

All clients are eICU partitions; MIMIC-IV uses care units as pseudo-sites and tests schema transportability only. No secure aggregation or differential privacy is applied to the enlarged exchanged-statistic surface.

## 4. Editorial Decision

**Send for Review.** Reviewers should adjudicate: whether BRIDGE is differentiated from Shapley-based contribution allocation; whether five-site endpoints support the equity framing or require scaling back to hypothesis-generating; and whether eICU-internal stress tests substitute for external multi-network validation.

## 5. Suggested Reviewer Expertise

Reviewers should include an expert in personalized and fairness-aware federated learning theory (client-level aggregation weighting, Shapley/incentive-based contribution allocation, non-IID convergence guarantees) to adjudicate the method's novelty and the missing prior-art comparison; a critical-care informatics methodologist with direct eICU/MIMIC experience to assess the landmark-design, leakage-control, and cohort-construction choices; a biostatistician experienced in clustered, hierarchical-bootstrap inference for small effective-sample-size endpoints to evaluate the Q1-uplift and worst-site AUROC claims; and a health-services or health-equity researcher to assess whether the structured-data-resource score and its framing appropriately (or inappropriately) proxy real-world hospital resource disparity. The clinical-methodological components should carry roughly 30% weight relative to the technical federated-learning and statistical review.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Personalized and fairness-aware federated learning for healthcare has matured rapidly since 2023, moving from generic client-drift corrections (FedProx, q-FFL) toward mechanisms that explicitly target resource asymmetry among institutions. DynamicFL (Zhang et al., *Nat. Commun.* 2025) proposes resource-adaptive architectures so that computationally constrained sites are not structurally disadvantaged in aggregation — a framing very close to this manuscript's own motivation, though evaluated on non-clinical imaging benchmarks. FlexFair-site (Xing et al., *Nat. Commun.* 2025) integrates multiple fairness criteria via a flexible regularization term in federated medical imaging, and FedTM (Souza et al., *npj Digit. Med.* 2026) combines federated learning with a sequential "travelling model" to reduce misclassification disparities across 83 international neuroimaging sites. Separately, a growing Shapley-value and incentive-mechanism literature (profit allocation for FL, performance-based fair incentive mechanisms, trajectory-based Shapley contribution metrics) addresses essentially the same allocation problem from cooperative game theory, largely outside the clinical AI venues this manuscript cites.

Against this landscape, the manuscript's distinctive contribution is the site-anchored, local-only-referenced estimand itself — collaboration benefit as a retrospectively computable, method-agnostic reporting quantity — rather than the aggregation mechanism, which shares its resource-adaptive weighting logic with DynamicFL and its game-theoretic cousins. The authors should engage directly with the Shapley/incentive-allocation literature, which they currently omit entirely, and should clarify what BRIDGE's benefit-aware aggregation adds mechanistically beyond a resource-adaptive target already present in DynamicFL.

## 5. Suggested Reviewers' Names

**Federated learning / contribution-allocation theory:** Tian Li (postdoctoral researcher, co-author of FedProx and q-FFL, continues to publish on heterogeneous and fair federated optimization); Feilong Zhang or Deming Zhai (authors of DynamicFL, directly comparable resource-adaptive federated framework); Huijun Xing or Jinke Ren (authors of FlexFair-site, directly comparable fairness-metric federated imaging framework).

**Critical-care informatics / eICU-MIMIC methodology:** Matthew Churpek (associate professor, extensive work on ICU deterioration prediction and multi-site clinical model validation); João Matos or Leo Anthony Celi's group (MIT/BIDMC, active eICU/MIMIC-IV methodological and equity-in-AI work); Raissa Souza (postdoctoral researcher, first author of FedTM, direct multi-site federated clinical-imaging experience).

**Biostatistics / small-sample hierarchical inference:** Ewout Steyerberg-affiliated or comparably positioned assistant/associate professor working on clustered bootstrap inference for multi-center prediction model evaluation.

---

## Editorial Integrity Alerts (Handling Editor Only)

1. **Corresponding-author domain mismatch.** The corresponding author's verifiable publication record (Google Scholar, arXiv, IEEE) is concentrated almost entirely in computer vision — face anti-spoofing, deepfake detection, video camouflaged object detection, remote photoplethysmography, multimodal fusion — with no evident prior record in federated learning theory, critical-care informatics, or clinical AI evaluation. This is not disqualifying given the large co-author list, but it warrants a targeted question to the authors about which co-author(s) hold primary responsibility for the clinical framing, cohort construction, and federated-learning claims, and should inform how heavily reviewers scrutinize the eICU/MIMIC-specific methodology.

2. **Reused funding acknowledgment across unrelated submissions.** The two NSFC grant numbers cited in this manuscript's Acknowledgements (62306061, 62576076) also appear as sole funding acknowledgments on recent, topically unrelated computer-vision preprints from the same corresponding author's group (e.g., audio-visual question answering, RGB-RF cardiac sensing). This is common for general-purpose AI grants and not itself an integrity violation, but it is a signal to confirm that the grants' stated scope covers clinical federated learning, and that funding disclosure is complete and accurate.

3. **No prior preprint or duplicate publication identified.** Independent search found no existing preprint, conference paper, or overlapping publication of this specific manuscript, its BRIDGE method, or its eICU 20-site benefit-redistribution results. No salami-slicing or undisclosed-preprint concern is raised at this time.

4. **Citation verification.** Spot-checked comparator citations (DynamicFL, FlexFair-site, FedTM) were verified against their original *Nature Communications* and *npj Digital Medicine* publications and are accurately attributed, with correct authorship, venue, and year, and no author overlap with the submitting group. No citation misattribution was found in the checked subset.

---

## Further Literature (Past 3 Years)

**1. Zhang, F. et al. Towards fairness-aware and privacy-preserving enhanced collaborative learning for healthcare. *Nat. Commun.* 16, 2852 (2025). DOI: 10.1038/s41467-025-58055-3.** Venue: Nature Communications. Peer-reviewed: yes. Cited by manuscript: yes (ref 23, adapted as the DynamicFL comparator). Author independence: independent (Harbin Institute of Technology / Tsinghua; no overlap). Relevance: the closest conceptual competitor — resource-adaptive architectures so that computationally constrained institutions are not structurally disadvantaged. The manuscript reimplements it as a comparator but does not argue why BRIDGE's benefit-aware target differs mechanistically from DynamicFL's resource-adaptive one. This is the single most important comparison to strengthen.

**2. Xing, H. et al. Achieving flexible fairness metrics in federated medical imaging. *Nat. Commun.* 16, 3342 (2025). DOI: 10.1038/s41467-025-58549-0.** Venue: Nature Communications. Peer-reviewed: yes. Cited: yes (ref 24, as FlexFair-site). Author independence: independent (CUHK-Shenzhen / Sun Yat-sen). Relevance: FlexFair integrates multiple fairness criteria via a flexible regularization term. Establishes the Nature Communications precedent for fairness-in-federated-medicine, and therefore the novelty bar this manuscript must clear.

**3. Souza, R. et al. Combining federated learning and travelling model boosts performance and opens opportunities for digital health equity. *npj Digit. Med.* 9, 294 (2026). DOI: 10.1038/s41746-026-02483-y.** Venue: npj Digital Medicine. Peer-reviewed: yes. Cited: yes (ref 25, as FedTM). Author independence: independent (University of Calgary). Relevance: FedTM reduces misclassification disparities across 83 international sites and explicitly reduces training load for smaller sites — a real multi-site network rather than a within-database simulation, which is precisely the external-validity gap this manuscript has.

**4. Hosseini, S. M., Sikaroudi, M., Babaie, M. & Tizhoosh, H. R. Proportionally fair hospital collaborations in federated learning of histopathology images. *IEEE Trans. Med. Imaging* 42, 1982–1995 (2023). DOI: 10.1109/TMI.2023.3234450.** Venue: IEEE TMI. Peer-reviewed: yes. Cited: **no**. Author independence: independent (University of Waterloo / Mayo Clinic). Relevance: Prop-FFL directly targets the same failure mode — averaged loss producing a model excellent for some hospitals and poor for others — via a proportional-fairness objective. Its omission is a substantive gap in the manuscript's positioning of "which hospitals actually benefit" as a novel question.

**5. Zhang, F., Shuai, Z., Kuang, K., Wu, F., Zhuang, Y. & Xiao, J. Unified fair federated learning for digital healthcare. *Patterns* 5, 100907 (2024). DOI: 10.1016/j.patter.2023.100907.** Venue: Patterns (Cell Press). Peer-reviewed: yes. Cited: **no**. Author independence: independent (Zhejiang University; distinct from the Zhang, F. of entry 1). Relevance: unifies client-level and subgroup-level fairness in one federated objective across four digital-health tasks. The manuscript's Discussion asserts that fairness-oriented objectives "act on absolute performance" whereas its own estimand does not; this paper is the strongest test of that distinction and should be engaged directly.

**6. Teo, Z. L. et al. Federated machine learning in healthcare: a systematic review on clinical applications and technical architecture. *Cell Rep. Med.* 5, 101419 (2024). DOI: 10.1016/j.xcrm.2024.101419.** Venue: Cell Reports Medicine. Peer-reviewed: yes. Cited: **no**. Author independence: independent (Duke-NUS / SERI). Relevance: of 612 included studies, only 5.2% involved real-world deployment. This is the field-level evidence that the manuscript's simulation-only design is the norm rather than the exception — useful for the authors' own limitations framing, and useful to editors in calibrating how much a retrospective simulation can claim.

**7. Pirmani, A. et al. Personalized federated learning for predicting disability progression in multiple sclerosis using real-world routine clinical data. *npj Digit. Med.* 8, 478 (2025). DOI: 10.1038/s41746-025-01788-8.** Venue: npj Digital Medicine. Peer-reviewed: yes. Cited: **no**. Author independence: independent (KU Leuven / MSBase consortium). Relevance: over 26,000 patients across a genuine international multi-centre registry; finds baseline FL underperforms personalized FL. This is the most direct real-world counterpoint to the manuscript's claim that personalization cannot reproduce redistribution, and reviewers will likely raise it.

**8. Yang, Y., Zhang, H., Gichoya, J. W., Katabi, D. & Ghassemi, M. The limits of fair medical imaging AI in real-world generalization. *Nat. Med.* 30, 2838–2848 (2024). DOI: 10.1038/s41591-024-03113-4.** Venue: Nature Medicine. Peer-reviewed: yes. Cited: yes (ref 15). Author independence: independent (MIT / Emory). Relevance: demonstrates that fairness properties do not survive distribution shift. Directly relevant to whether BRIDGE's redistribution would persist outside the eICU resampling regime — a question the manuscript raises but does not answer.

**9. Eden, R. et al. A scoping review of the governance of federated learning in healthcare. *npj Digit. Med.* 8, 427 (2025). DOI: 10.1038/s41746-025-01836-3.** Venue: npj Digital Medicine. Peer-reviewed: yes. Cited: yes (ref 36). Author independence: independent (University of Queensland). Relevance: the governance frame on which the manuscript's participation-incentive argument depends. If "uncertainty about local benefit is a governance concern," this is the source that must substantiate it; the manuscript currently cites it in passing rather than building the argument from it.

**10. Li, M., Xu, P., Hu, J., Tang, Z. & Yang, G. From challenges and pitfalls to recommendations and opportunities: implementing federated learning in healthcare. *Med. Image Anal.* 101, 103497 (2025). DOI: 10.1016/j.media.2025.103497.** Venue: Medical Image Analysis. Peer-reviewed: yes. Cited: yes (ref 35). Author independence: independent (Imperial College London / SJTU). Relevance: catalogues the operational barriers — coding practice, vendor system, case mix — that the manuscript concedes cannot be induced by masking and subsampling within eICU. Useful for specifying what an adequate external validation would actually require.

*Note on peer-review status: all ten entries are peer-reviewed journal publications. No arXiv, medRxiv, or bioRxiv preprints are included. Preprint-only work in this area (e.g., Tastan et al., "Redefining Contributions: Shapley-Driven Federated Learning," arXiv:2406.00569) was deliberately excluded as unreviewed, though it is worth noting to the authors as further evidence that the contribution-allocation framing is well established.*

066393
## 1. Overall Assessment

ZyGuard fuses CBCT, orthopantomograms, and clinical text via SwinUNETR–ResNet50–graph-attention architecture to classify ZI pathway (ZAGA/AGA) and predict Schneiderian membrane perforation risk, trained on 962 ZIs from 379 patients across seven international centers, with five-patient prospective validation.

Automating this classification is a legitimate, underserved problem, and the engineering exceeds most CBCT classification papers in this space. But ground truth comes from the same subjective process the model replaces, with no inter-rater reliability reported for the original 962-case labeling. Combined with a striking internal inconsistency in reported anatomical trends (below), this tempers confidence in the results.

## 2. Strengths

The dataset is genuinely multicenter and multimodal across three countries and multiple CAIS systems (Brainlab, Dcaret, X-guide), uncommon rigor for ZI literature.

The contact-area algorithm (Eq. 1) carefully solves metallic-artifact contamination in postoperative CBCT, and its convergence with prior BIC-Z measurements (Gu et al., 2023) is a sound consistency check.

Comparison against 11 classical ML models, three 2D and three 3D deep learning baselines, and unimodal ablations (Figs. 5, S7–S9) properly isolates the fusion module's contribution.

The prospective arm, though small, moves beyond retrospective benchmarking with real dynamic-navigation-guided surgery.

## 3. Weaknesses

Lines 197–204 report maxillary sinus contact area highest for ZAGA 0, decreasing to ZAGA 4 — contradicting both ZAGA's anatomical logic (Aparicio, 2011) and the manuscript's own premise that intrasinus pathways carry higher perforation risk (lines 101–102). This requires resolution.

External generalizability is uneven: BOC-HK ZAGA accuracy is 0.624, AUC 0.817; HGH and JJ contain zero low-risk perforation cases, making AUC uncomputable at two of six sites.

The human-comparison (n=20) and prospective (n=5) cohorts are too small for "noninferior to specialists," with no confidence intervals on the accuracy gap, and S2 outperformed ZyGuard retrospectively.

A single IRB (SH9H) covered international sites (Spain, Hong Kong) via acceptance rather than independent local review — unclear GDPR-adjacent compliance at the Spanish site.

## 4. Editorial Decision

**Reject.** The sinus-contact trend inconsistency undermines the paper's anatomical premise, compounded by unreported labeling reliability — first-order problems, not revision-level polish. Suggested transfer after correction: **npj Digital Medicine**.

**Steelman:** the sinus-contact trend may reflect surface geometry (extrasinus implants tracking the lateral wall) rather than penetration depth; if clarified, the technical contribution stands on solid ground.

## 5. Suggested Reviewer Expertise

Graph attention network / multimodal fusion architectures for clinical imaging plus tabular data; 3D medical image segmentation and SwinUNETR-based volumetric modeling; CBCT-based automated surgical-approach classification specifically in implant dentistry; oral and maxillofacial surgery with hands-on ZI/ZAGA clinical experience independent of the ZAGA/AGA originating groups; biostatistics for small-cohort multicenter diagnostic AI validation (AUC confidence intervals, class-imbalanced external cohorts).

## 6. State-of-the-Art Literature Review (Past 3 Years)

The closest direct precedent is SinusC-Net (Hwang et al., *Sci Rep* 2023), which automatically classifies maxillary sinus augmentation surgical approach from CBCT using a 3D distance-guided landmark network, achieving AUC 0.95 — methodologically the nearest comparator to ZyGuard's ZAGA/AGA task, yet it is not cited or discussed. Multimodal graph-attention fusion for clinical outcome prediction has matured rapidly: Keicher et al. (*Sci Rep* 2023) used a multimodal GAT for COVID-19 outcome prediction, and Fu et al. (*Comput Biol Med* 2023) — the explicit architectural inspiration for ZyGuard per the manuscript's own citation — applied graph-based multimodal fusion to survival prediction from multiplexed imaging and patient variables. The authors' own prior work, ZygoPlanner (Li et al., *Med Image Anal* 2025), addresses path planning rather than technique classification and is appropriately disclosed as prior art. ZyGuard's contribution is a legitimate extension of this fusion paradigm into a genuinely novel clinical classification task, but the manuscript would benefit substantially from directly engaging SinusC-Net as the nearest analogous system rather than situating itself only against generic ZI robotics/navigation literature.

## 7. Suggested Reviewers

**Multimodal GNN/fusion methodology:** Xiaohang Fu (University of Sydney); Matthias Keicher (Technical University of Munich); Sophia Bano (comparable multimodal medical GNN work).
**CBCT automated surgical classification:** Se-Ryong Kang or Su Yang (Seoul National University, SinusC-Net group).
**3D medical segmentation/SwinUNETR:** a researcher with published SwinUNETR-based CBCT or craniomaxillofacial segmentation work, distinct from Ali Hatamizadeh's original group given likely unavailability.
**Independent ZI clinical expertise:** an oral/maxillofacial surgeon with published ZAGA-classified case series, unaffiliated with Aparicio, Davó, or the submitting centers.

058926
**Reviewer 1 (Pawuś, PhD candidate, Poland).** Reject. The core objection is that the concordance analysis conflates two mechanistically distinct groups — patients where clinician and model timing genuinely agreed, and patients where both simply withheld RRT — and the latter, dominated by low-acuity patients, likely drives the reported 46% mortality reduction. Compounding this: the 7-day exposure window creates immortal-time/future-information bias, exact-day concordance is clinically arbitrary, positivity/overlap is unverified, WIS lacks effective-sample-size diagnostics, the reward function's investigator-defined weights are clinically unjustified, and the model-selection criterion (minimizing RRT initiation rate) is misaligned with the stated goal of maximizing outcomes. He also flags that renal recovery ignores the competing risk of death, and that "optimal," "safe," and "improves survival" are unsupported given a purely retrospective evaluation.

**Reviewer 2 (Feng, Associate Professor, Singapore).** No stated recommendation, but substantively aligned with Reviewer 1. Central point: the abstract's headline 4.3% vs 4.6% comparison and the 12.9% concordance figure answer different questions (whether to treat vs. when) and should not be run together. She argues the concordance group is dominated by mutual non-initiation among patients who likely never needed RRT, making the mortality benefit largely uninformative once restricted to patients for whom RRT was a genuine consideration. She also notes the Decision Transformer is model-free and cannot perform true counterfactual simulation, so "counterfactual impact" language is unsupported by the architecture; that WIS effective sample size is never reported despite RRT being rare (~4%); and that the sensitivity analysis changing the reward bound from [-50,+60] to [-10,+60] invalidates the "robustness" claim since WIS scores aren't comparable across differently-scaled rewards.

**Reviewer 3 (Klamrowski, PhD candidate, Canada).** No stated recommendation, but raises the most granular methodological attack on the reward function itself: the recovery/discharge/death scoring scheme (e.g., day-25 recovery scoring 7 points below a day-28 discharge with no recovery) embeds unstated value judgments that are never defended, and there is no reward component tied to RRT timing at all despite that being the manuscript's central clinical question. He also challenges the immortal-time-bias fix (excluding patients who died within 3 days may introduce survivorship bias rather than removing confounding), questions the eGFR<25 exclusion rationale, and asks whether pre-existing ESRD/dialysis status was ascertained consistently across all contributing datasets — a basic cohort-validity question left unanswered.

**Reviewer 4 (Xu, ECR)** co-reviewed with Reviewer 2 and submitted no independent comments.

**Decision: Reject.** This is not a revisable-gap situation. Three independent reviewers converge on the same structural defect from different angles: the concordance metric — the paper's central causal claim — is confounded by construction, since "concordance" indiscriminately mixes genuine agreement with mutual inaction on low-risk patients, and no amount of added text can retroactively unconfound an analysis whose exposure groups are misdefined. This compounds with a reward function that is clinically unjustified and untested for sensitivity (per Feng and Klamrowski), immortal-time bias in the exposure window (per Pawuś), and a possible survivorship-bias introduction from the death-exclusion fix (per Klamrowski) — three separate bias vectors pointing the same direction, not one fixable flaw. Per your fatal-vs-revisable framework, this is a redesign, not a revision: it requires re-defining concordance to isolate patients for whom RRT was a genuine clinical consideration, a target-trial-emulation exposure structure, and a defensible, pre-registered reward specification — effectively a new analysis, not a response letter. Recommend transfer to **npj Digital Medicine**, where a reinforcement-learning RRT paper (Grolleau et al., cited by the circulation notes) and a hierarchical-RL RRT paper have already been published, indicating topical fit and a review culture more tolerant of methods-in-progress work.

**Steelman against rejection:** The dataset is unusually large and heterogeneous (89,185 derivation patients, five external cohorts, N=42,121), which is a genuine scale advantage over prior single-cohort RL-RRT work, and the four pre-specified sensitivity analyses show the authors anticipated some of these concerns. A determined reviewer could argue for major revision on the theory that the concordance analysis can be re-run stratified by the six subgroups Pawuś specifies (concordant initiation, concordant non-initiation, etc.) without redesigning the underlying DT architecture — i.e., the flaw is in the *analysis layer*, not the *model*, and is therefore separable and fixable within a revision cycle. I don't find this persuasive as grounds to send for review: the reward function and model-selection criterion (both flagged independently by three reviewers as internally inconsistent with the paper's stated clinical objective) sit upstream of the DT's outputs, so even a stratified concordance re-analysis inherits a policy that was optimized against the wrong target.

053601
## Reviewer Summary

**Reviewer 1 (Thakoor, Assistant Professor)** — Most constructive. Confirms the four-UQ-method ranking (FMUE > Ensemble > TTA > BNN) and the clinician tier hierarchy (retinal experts > senior > junior doctors). Notes AI assistance raised confidence in junior doctors only, and cut interpretation time for junior/senior but not experts — read as evidence that experienced clinicians critically evaluate AI rather than defer to it. Main critique: entropy/efficiency terminology is introduced too late, leaving ambiguous whether "uncertainty" refers to model epistemic uncertainty or clinician epistemic uncertainty. No explicit recommendation given, but no rejection either — this is a "revise for clarity" review.

**Reviewer 2 (Zeng, Professor)** — Explicit reject. Three objections: single-institution physician cohort introduces systematic bias; the diagnostic task is artificially simplified relative to real practice, weakening translational validity; no mechanistic/spatial explainability analysis backs the uncertainty claims. States plainly the study does not meet the broad-impact threshold.

**Reviewer 3 (Khalifa, Assistant Professor)** — Most technically detailed, and the most consequential. Flags that the manuscript shares the same 82,813-image training corpus and a near-identical human-comparison design with the authors' own prior paper (ref. 14, Peng et al., Cell Reports Medicine 2025) — same "OCT reading group" consortium, nearly identical 160-image/16-condition test set, overlapping panel structure (9–12–11 vs. 3–9–20 experts/seniors/juniors). This is not disclosed as a follow-up or extension. Second, the headline self-calibration claim (OR 16.111, 95% CI 2.839–91.440) rests on only 6 misclassified images out of 160 — a CI that wide off 6 events is not a stable estimate. Third, multiplicity correction (Benjamini-Hochberg) is applied only to Figure 3, while dozens of other correlation tests across 32 physicians are uncorrected. Fourth, generalizability is capped by single-institution recruitment, and ground truth incorporated fundus photography that OCT-only readers didn't have access to — which mechanically inflates the AI-over-physician margin. Despite this, Reviewer 3 frames these as addressable and lays out exactly what full revision would require.

## Editorial Integrity Alert (to handling editor only)

The overlap with ref. 14 — same training corpus, same consortium, near-identical test-set construction and comparison design by the same author group — needs to be resolved before any further processing. This is either an undisclosed extension of prior work or borders on salami-slicing. Request from the corresponding author an explicit statement distinguishing this submission's novel contribution from ref. 14, and confirmation that the 160-image test set is not reused verbatim. This is independent of, and prior to, any scientific revision decision.

## Editorial Decision: **Reject**

Reviewer 2's rejection stands, and Reviewer 3's more granular findings support it rather than soften it. The self-calibration claim central to the paper's contribution is built on 6 misclassification events — underpowered by design, not by execution, since a 160-image/16-condition test set cannot generate the event count needed for a stable OR. Combined with the undisclosed corpus/design overlap with the authors' own ref. 14 and single-institution generalizability limits, these are structural rather than fixable-by-rewrite problems. Uncorrected multiplicity across dozens of physician-level tests further undermines confidence in the "dual-level correlation" result the abstract leads with. This does not meet the bar of a distinctive, reproducible advance at the Lancet Digital Health standard. Suggested transfer: **npj Digital Medicine** (human-AI interaction / uncertainty framing) or **Communications Medicine** (clinical evaluation framing), contingent on resolution of the integrity question above before any transfer letter is sent.

**Steelman counterargument:** One could argue for Major Revision instead — Reviewer 1 found no fatal flaw, and Reviewer 3 explicitly treats the weaknesses as addressable (external validation, corrected multiplicity, clarified terminology). If the ref. 14 overlap turns out to be a legitimate, disclosable extension rather than an integrity problem, and the authors can supply a properly powered self-calibration analysis, the human-AI interaction findings (differential reliance by clinician tier) are genuinely novel and worth preserving. The rejection here is defensible mainly because two independent, serious flaws (fragile core statistic + undisclosed corpus overlap) compound rather than because either alone is unrecoverable.

052019
**Reviewer synthesis**

Bin Sheng (R1, no code review despite ECR pairing note) raises the most consequential concern: the described workflow shows human experts intervening on architecture selection, hyperparameter choice, and feature engineering, not merely supervisory checkpoints, undermining the claim that Eureka is the primary discovery agent. He separately identifies a probable adaptive-overfitting problem — supplementary logs show the held-out test set was used repeatedly to guide iterative model refinement, which invalidates the reported test performance as an unbiased estimate. He also flags that novelty over AutoGPT-class agents is asserted, not demonstrated, absent an ablation against a standard coding-assistant baseline, and that the external nephropathy cohort (n=312, only 6 HN and 21 MCD/FSGS cases, external MCD/FSGS AUC 0.707) is too small and imbalanced to support the biomarker claim.

Han Lv (R2) converges on the missing baseline-comparison problem and adds that the second open-goal study's prompt was explicitly refined using results from the first, contaminating claimed task independence. He also notes the four-trial early termination of the open-goal experiment (out of 25) is undocumented in the reliability accounting.

Wisit Cheungpasitporn (R3) independently corroborates the adaptive-overfitting concern and adds that "prospective" is a mischaracterization of a 2009–2022 retrospective cohort, that "multicenter generalizability" is overstated because external cohorts were pooled rather than evaluated separately, and that patient-level partitioning for bilateral fundus images is undocumented — a leakage risk. He confirms the GitHub repository is substantive.

Xuhai Xu (R4, co-written with Will Wang) is the most structurally critical: the title and framing claim general "scientific discovery" capability, but the fixed-goal tasks are supervised classification/segmentation, and the expert-free ablation lacks a human-alone comparator, so synergy ("greater than the sum of its parts") is asserted, not shown. He also notes the entire framework is evaluated on a single backbone (GPT-4o), so generalizability of the architecture is untested, and that "trustworthy" is unsupported by any hallucination, robustness, or failure-mode analysis.

Will Wang (R5/ECR) adds a reproducibility-integrity note: the human-AI collaboration protocol described as three-stage is not implemented in the released code, and the repository references model families that postdate GPT-4o, suggesting version drift between the reported experiments and the archived artifact.

**Decision: Reject, with transfer suggestion to *npj Digital Medicine*.**

Three of five reviewers independently identify test-set contamination (adaptive overfitting via iterative use of the held-out set) and undocumented patient-level leakage risk in bilateral image splitting — this is a validity-of-evidence problem, not a presentation problem, and no revision instruction can retroactively unbias an already-refined test set without new locked data. Compounding this, R1, R2, and R4 independently find that the central claim — that structured human-AI collaboration constitutes discovery beyond what either party achieves alone — is unsupported, since no human-alone or standard-agent baseline exists; without that comparator the paper's title claim is unfalsifiable as written. R5's finding that the archived code does not implement the described collaboration protocol, combined with unexplained model-version drift, raises an independent reproducibility-integrity flag. These three issues are compound and mutually reinforcing rather than isolated fixable items, which is why this clears the bar for reject rather than major revision.

Steelman against rejection: all five reviewers describe the engineering execution (sandboxing, logging, timestamped runs, six-modality coverage) as genuinely careful, and R5 confirms good-faith code hygiene. A determined author response could, in principle, supply a truly locked validation partition, add an AutoGPT-baseline and human-alone arm, and narrow title/abstract claims to match the supervised-task evidence actually generated — that combination is not conceptually impossible in one revision cycle. If Yuli judges the engineering contribution (three-stage checkpointed protocol, expert-free ablation design) sufficiently novel independent of the compromised nephropathy case study, major revision restricted to the fixed-goal benchmark (dropping the open-goal claims entirely) is a defensible alternative to outright rejection.

045466
## Reviewer Summary

**Reviewer 1 (Toro Tobon, US, Assistant Professor)** — Interesting and timely, but flags four major issues: (1) the core claim that AI literacy drives comprehension gaps rests entirely on unadjusted bivariate Spearman correlations, with no multivariable model controlling for experience, specialty, or prior AI exposure; (2) the manuscript conflates distinct AI modalities under one "AI" umbrella, weakening generalizability claims; (3) intercoder agreement in the qualitative phase was only 33–42%, with no documented reconciliation method; (4) the static Figma-based web survey does not replicate live-EHR cognitive load, undermining ecological validity. Ten additional minor issues (missing Cronbach's alpha, missing CIs, table numbering errors, conflated reporting-guideline citations).

**Reviewer 2 (Iqbal, career stage undisclosed)** — Recommends **rejection**. Argues the central claims exceed the evidence: "meaningful human oversight" was never measured, only self-reported preference and performance on four unvalidated comprehension items; the qualitative sample is single-institution (n=12) and the survey sample skews academic (81%) with a weak completion funnel (710 opened → 109 completed), undermining any "national sample" framing; AI literacy is asserted as the explanatory factor from bivariate correlation alone, with no multivariable adjustment or prespecified hypothesis; and novelty is overstated given prior model-card work (Sendak's Model Facts Label, Crisan's Interactive Model Cards).

**Reviewer 3 (Kharko, Sweden, non-profit researcher)** — No major concerns. Minor suggestions only, on methods reporting clarity and discussion elaboration. Recommends acceptance in substance.

**Handling editor's own triage note (Eric Wang, pre-review)** — Independently flagged the same structural issues: unrepresentative academic-center-heavy sample, no sensitivity analysis by setting, CMC evaluated outside a functioning CDSS, uncorrected multiple correlations, and an unreliable four-item comprehension scale. Preliminary system recommendation is already set to **Reject**.

## Decision: **Reject**

Two independent reviewers (Toro Tobon, Iqbal) and the pre-review editorial triage converge on the same fatal flaw, not three separate complaints: the manuscript's central causal claim — that AI literacy, not documentation design, is the structural barrier to oversight — is inferred from unadjusted bivariate correlations on an unvalidated, memory-confounded four-item comprehension instrument (the Card was unavailable during testing), evaluated in a static mockup disconnected from any functioning CDSS. This is not a fixable reporting gap; the operationalization of the outcome variable is broken at the design level, and "meaningful human oversight" — the paper's title claim — was never actually measured. Reviewer 3's absence of concerns does not offset this, since her comments engage with presentation rather than the design's internal validity. Recommend rejection with transfer suggestion to **npj Digital Medicine** (best fit for the clinician-facing documentation/oversight angle) or **Communications Medicine** (if authors prefer a broader digital-health venue), contingent on redesigning the comprehension measure, adding multivariable adjustment, and embedding the CMC in a live CDSS before resubmission.

**Steelman against rejection:** One could argue this is exploratory, hypothesis-generating work — the authors never claim confirmatory causal inference, and the qualitative-to-quantitative traceability chain (structured survey items derived from coded interview findings) is genuinely uncommon rigor for this literature. Under that reading, the correlational limitation is a disclosed scope constraint rather than a fatal flaw, and major revision (add multivariable models, validate the comprehension instrument, report intercoder reconciliation) could suffice. I don't find this persuasive at Lancet Digital Health–caliber bar: the abstract and title assert AI literacy as a structural barrier in declarative terms, not exploratory ones, and the measurement confound (memory test masquerading as comprehension test) can't be revised away — it requires a new instrument and likely new data collection, which is a reject-and-resubmit, not a revision.
