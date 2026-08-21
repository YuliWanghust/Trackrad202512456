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


068229

# Editorial Report — Manuscript 068229

**Title:** Development and Validation of a Multilevel Deep-Learning Framework for Individualized Prediction in Clustered Data
**Authors:** Zhu, Schoedel, Sust, Bühner, Terhorst (LMU Munich; Charlotte Fresenius Hochschule; DZPG Munich-Augsburg)
**Venue considered:** *Nature Communications*, Digital Health section

---

## Editorial Integrity Alert (confidential — handling editor only)

Five matters require attention before any further processing.

**Missing mandatory declarations.** The manuscript contains no ethics approval statement, no informed consent statement, and no competing interests declaration. Prior publications from the same Smartphone Sensing Panel Study (SSPS) cohort state explicitly that the study adhered to EU-GDPR and received ethical approval; the present submission omits this entirely. Passive smartphone logging of GPS, Bluetooth device counts, ambient loudness, notification content categories, and app usage is high-sensitivity personal data under GDPR. Absence of these statements is a compliance defect that must be corrected regardless of the scientific decision.

**Extensive prior use of the validation cohort, inadequately disclosed.** The SSPS (Schoedel & Oldemeier, 2020; ref. 52) is a heavily mined benchmark dataset with multiple prior publications, including Reiter & Schoedel (*Behavior Research Methods*, 2024), große Deters & Schoedel (2024), a systematic app-categorisation paper in *Journal of Open Psychology Data*, and a *Psychometrika* paper on SSPS preprocessing pipelines. Co-author R. Schoedel is a principal architect of the SSPS. The manuscript cites only the protocol. It does not state which prior analyses used overlapping participants, overlapping sensing features, or the same daily-affect outcome. This is not necessarily salami-slicing, but the overlap is undeclared and the authors should be required to enumerate it. Note in particular that the preprocessing pipeline appears to be inherited from the group's own *Psychometrika* methodology paper, which is uncited.

**Undisclosed author overlap with a cited comparator work.** Reference 65 (Zhu, N. et al., *npj Digital Medicine* 8, 413, 2025) is a first-author self-citation; co-authors Bühner and Terhorst are also on that paper. Reference 53 (Büscher et al.) and the JMIR depression-sensing paper by Terhorst et al. (2025) originate from the same LMU/Ulm/DZPG network. The manuscript nowhere flags these as own-group work. This is common practice but should be surfaced given the framing of ref. 65 as neutral field evidence.

**Uncited prior art that materially undercuts the novelty claim.** The "slope network" is a feature-wise multiplicative modulation of the input vector generated by a hypernetwork conditioned on cluster covariates. This is FiLM (Perez et al., AAAI 2018), restricted to the scale term and applied at the input layer. FiLM, hypernetworks, and the mixed-effects deep-learning literature (Simchoni & Rosset, *JMLR* 2023; Xiong et al., MeNets, CVPR 2019) are all absent. The authors' own reference 43 (ARMED; Nguyen, Treacher & Montillo, *IEEE TPAMI* 2023) already implements nonlinear cluster-specific random slopes with explicit generalization to unseen clusters — the exact capability claimed as novel here — yet is miscategorised in the taxonomy as "similarity-based transfer" and its unseen-cluster mechanism is misdescribed. The claim at lines 146–149 that mixed-effects approaches "typically default to b_i = 0" for new clusters is directly contradicted by the cited ARMED paper.

**Numerical and internal inconsistencies.** Lines 361–363 state that few-shot learning was the best-performing existing personalized model; Table 1 shows mixed-effects random forest superior on both MAE (0.717 vs 0.721) and R² (0.004 vs −0.080), with an MSE difference of 0.001 against a reported SD of 0.052. That sentence is incorrect as written. Table 1 SDs are stated to come from ten outer folds of a single nested cross-validation, while Fig. 4 reports 100 estimates across ten resamples; which resample Table 1 represents is never specified, and the headline numbers should come from all 100 folds. Supplemental Fig. S2 is cited both as the day-level feature list (line 341) and as the nested cross-validation schematic (line 641); Supplemental Table S1 is cited both as the person-level feature list (line 342) and as the evaluation-metric definitions (line 649). Lines 266–267 label the slope network's parameters W_base and b_base. Lines 272–273 reverse the definitions of d̃_ij and d_ij. Equation at line 631 writes f_dev((p_i) ⊙ d_ij), which is dimensionally impossible (37 vs 560).

---

## 1. Overall Assessment

Three-component architecture (baseline, slope, deviation networks) decomposing clustered-data prediction into a covariate-driven cluster mean and covariate-gated residual. Validated on 483 SSPS participants (6,737 person-days) predicting daily affect from 560 sensing and 37 person-level features. Two concerns dominate: the architecture is unacknowledged input-level FiLM conditioning, unbenchmarked against cited mixed-effects deep learning; and R² = 0.100 is likely dominated by between-person variance from trait-affect predictors overlapping the outcome construct, with no within-person R² reported — the exact critique the authors' own ref. 56 makes.

## 2. Strengths

The decomposition is theoretically coherent and enables three-layer Integrated Gradients interpretation. Evaluation is unusually careful: nested ten-fold cross-validation with participant-level separation, repeated across ten resamples (Fig. 4), correctly exposing few-shot instability. Benchmarks isolate architecture from feature-set contribution well; the concatenation model's near-null R² = 0.009 against the proposed R² = 0.100 is the paper's most informative result. Reproducibility (OSF code, PsychArchives data, preregistration) exceeds field norms.

## 3. Weaknesses

Trait affect dominates the baseline network (Fig. 5) while predicting a daily-affect outcome, so most of R² = 0.100 may be near-tautological rather than incremental sensing signal; no within-person R² is reported. The critical ablation — residualization without gating — is absent, so the gain over concatenation cannot be attributed to personalization. No statistical inference accompanies any comparison, and lines 361–363 misstate the best comparator relative to Table 1. Learned "slopes" have no coefficient interpretation, and Fig. 7 shows sign reversal across resamples for the Saturday feature, undermining the interpretability claim. No external cohort validation, no subgroup analysis despite salient demographic features, unexamined 29% attrition.

## 4. Editorial Decision

**Reject**, with transfer offer. Construct overlap, missing ablation, and absent within-person R² render the central claim untestable; combined with unacknowledged FiLM equivalence, a mischaracterised ARMED comparator, and no external validation, this falls below a *Lancet Digital Health*-calibrated bar. *Communications Psychology* is the natural transfer target.

**Steelman.** As a methods paper, the tenfold R² gain from architecture alone over naive concatenation is real and not explained by trait-affect leakage, which is equally available to the concatenation benchmark. This would justify review elsewhere, but the missing ablation confounds the mechanism and Fig. 7's sign instability contradicts the interpretability claim being sold.

## 5. Suggested Reviewer Expertise

Five areas are needed, weighted toward methods. First, mixed-effects and random-effects deep learning for clustered non-i.i.d. data — specifically researchers who have implemented cluster-specific random slopes in neural architectures and evaluated generalization to unseen clusters, and who can adjudicate the ARMED and LMMNN comparison directly. Second, conditioning and modulation mechanisms in neural networks (FiLM, hypernetworks, gating), to assess the novelty claim and the identifiability of the learned gain vectors. Third, prediction methodology for intensive longitudinal and experience-sampling data, with particular competence in the between-person versus within-person decomposition of predictive accuracy and in the choice of the person-specific mean as reference model. Fourth, digital phenotyping and passive smartphone sensing for affect and mental health, including feature-extraction pipelines, expected effect-size ceilings, and the replication record of the field. Fifth, on the clinical side, ambulatory assessment and just-in-time adaptive intervention design in mental health, to evaluate whether daily aggregated valence in a non-clinical German quota sample can support the intervention claims the discussion makes.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The problem this manuscript addresses has an active and directly competitive methodological literature that the introduction does not engage. Nguyen, Treacher and Montillo's ARMED framework (*IEEE TPAMI*, 2023) combines an adversarially regularised fixed-effects subnetwork, a Bayesian random-effects subnetwork supporting nonlinear random slopes, and a cluster-membership predictor that enables prediction on clusters unseen in training, with reported 2–9% relative gains on unseen clusters across four datasets including dementia prognosis. Simchoni and Rosset's LMMNN (*JMLR*, 2023, extending their NeurIPS 2021 paper) integrates a linear-mixed-model negative log-likelihood loss directly into deep networks for high-cardinality repeated-measures data. Both are more principled treatments of the same problem than the sequential two-stage least-squares-style residualization used here, and neither is benchmarked against. The conditioning mechanism itself dates to FiLM (Perez et al., AAAI 2018), whose scale-and-shift operator γ ⊙ F + β subsumes the proposed slope network as the shift-free, input-layer special case; the manuscript's "slope network" is a hypernetwork FiLM generator by any standard reading, and the omission of this literature is the single largest citation gap.

On the application side, the field has moved decisively toward the question the manuscript sidesteps. Balliu et al. (*npj Digital Medicine*, 2024) showed on 183 individuals with depressive symptoms over 40 weeks that idiographic models substantially outperform nomothetic ones for mood forecasting, and — critically — benchmarked against a model predicting from past depression severity alone. Timmons et al. (*npj Mental Health Research*, 2025) reached the same conclusion for family mental health symptoms and demonstrated that personalization benefit varies systematically with individual characteristics, which is precisely the cross-level moderation this manuscript models but does not test for heterogeneity. Hammelrath et al. (*Neuroscience Applied*, 2026) — the authors' own reference 56 — explicitly criticises prior personalized-versus-population comparisons for omitting the person-specific mean affect benchmark, arguing that without it one cannot know whether passive features add anything beyond a person's average. This manuscript is subject to that critique in full: R² is computed against the global mean, the strongest predictors are trait affect self-reports, and no within-person accuracy is reported. Terhorst et al. (*JMIR*, 2025), from the same institutional network, found only incremental value of smart-sensing features over EMA for depression severity, which is consistent with the low absolute performance here and should be discussed as context rather than left out. Where the manuscript does advance the field is in demonstrating that a fixed feature set yields sharply different performance under different architectural treatments of the multilevel structure; where it merely replicates is in showing, again, that personalization helps and that passive sensing explains little daily affect variance.

## 7. Suggested Reviewer Names

For mixed-effects and random-effects deep learning: **Kevin P. Nguyen** (UT Southwestern), first author of ARMED, *IEEE TPAMI* 45, 8081–8093 (2023) — the single most directly comparable architecture, and best placed to assess whether the proposed decomposition improves on it. **Giora Simchoni** (Tel Aviv University), author of "Integrating random effects in deep neural networks," *JMLR* 24(156), 2023 — the LMMNN benchmark. **Alex H. Treacher** (UT Southwestern), co-author on ARMED and on the UQ-ARMED uncertainty-quantification extension.

For conditioning mechanisms and identifiability of modulation parameters: **Mehmet Ozan Türkoğlu**, whose work extends FiLM-style conditioning to structured and temporal domains and who can evaluate whether the learned gain vectors are identifiable and interpretable. **Francesca Mandel** (University of Pennsylvania), first author of "Neural networks for clustered and longitudinal data using mixed effects models," *Biometrics* 79, 711–721 (2023) — the manuscript's own reference 39, and a reviewer who can judge the residualization scheme's statistical properties directly.

For prediction methodology in intensive longitudinal data: **Brunilda Balliu** (Assistant Professor, UCLA Computational Medicine), senior author of "Personalized mood prediction from patterns of behavior collected with smartphones," *npj Digital Medicine* 7, 49 (2024) — the strongest available referee on within-person versus between-person accuracy decomposition and on appropriate reference models. **Egon Dejonckheere** (Assistant Professor, KU Leuven / Tilburg), for experience-sampling measurement and the psychometrics of single-item momentary affect.

For digital phenotyping and passive sensing: **Adela C. Timmons** (Assistant Professor, UT Austin), first author of "Developing personalized algorithms for sensing mental health symptoms in daily life," *npj Mental Health Research* 4, 34 (2025) — directly comparable personalized-versus-generalized comparison. **Theodora Chaspari** (Associate Professor, University of Colorado Boulder), senior author on the same paper, for the signal-processing and feature-engineering side.

For ambulatory assessment and JITAI: **Claire R. van Genugten** (Amsterdam UMC), first author of "Beyond the current state of just-in-time adaptive interventions in mental health," *Frontiers in Digital Health* 7, 1460167 (2025) — the manuscript's reference 67, and the right person to assess whether the intervention claims are supportable.

Conflicts to exclude: all LMU Munich, Charlotte Fresenius Hochschule, DZPG Munich-Augsburg, and Ulm University personnel; all SSPS and PhoneStudy collaborators, including Clemens Stachl, Florian Pargent, Sandra Matz, Gabriella Harari, and Harald Baumeister.

---

## Further Literature (past three years, annotated)

**1.** Nguyen, K. P., Treacher, A. H. & Montillo, A. A. Adversarially-Regularized Mixed Effects Deep Learning (ARMED) Models Improve Interpretability, Performance, and Generalization on Clustered (non-iid) Data. *IEEE Transactions on Pattern Analysis and Machine Intelligence* 45, 8081–8093 (2023). DOI: 10.1109/TPAMI.2023.3234291 *(verified)*. Peer-reviewed. Cited as ref. 43 but miscategorised as "similarity-based transfer." Authors independent of the submitting group. This is the closest competitor: it already provides nonlinear cluster-specific random slopes, quantification of inter-cluster variance, and explicit prediction for unseen clusters. The manuscript's Type-2 criticism that mixed-effects models default to zero random effects for new clusters is falsified by this reference. Must be reclassified and benchmarked.

**2.** Simchoni, G. & Rosset, S. Integrating Random Effects in Deep Neural Networks. *Journal of Machine Learning Research* 24(156), 1–57 (2023). Available at jmlr.org/papers/v24/22-0501.html *(verified; JMLR does not issue DOIs)*. Peer-reviewed. Not cited. Authors independent. LMMNN embeds an LMM negative log-likelihood loss in deep networks for high-cardinality repeated measures; it is the principal statistical-learning alternative to the sequential residualization used here and should appear both in the taxonomy and in Table 1.

**3.** Mandel, F., Ghosh, R. P. & Barnett, I. Neural Networks for Clustered and Longitudinal Data Using Mixed Effects Models. *Biometrics* 79, 711–721 (2023). DOI *not independently verified*. Peer-reviewed. Cited as ref. 39. Authors independent. Cited only in passing to support the claim that mixed-effects neural approaches rely on linear random-effect structure; that characterisation should be checked against what this paper actually implements, since the manuscript's Type-2 critique leans on it.

**4.** Balliu, B. et al. Personalized mood prediction from patterns of behavior collected with smartphones. *npj Digital Medicine* 7, 49 (2024). DOI: 10.1038/s41746-024-01035-6 *(verified)*. Peer-reviewed. Cited as ref. 33. Authors independent. Demonstrates idiographic superiority over nomothetic models for mood forecasting in 183 symptomatic individuals over 40 weeks, and benchmarks against prediction from past symptom severity alone. The reference-model discipline shown here is exactly what the present manuscript lacks.

**5.** Timmons, A. C. et al. Developing personalized algorithms for sensing mental health symptoms in daily life. *npj Mental Health Research* 4, 34 (2025). DOI: 10.1038/s44184-025-00147-5 *(verified)*. Peer-reviewed. Cited as ref. 54. Authors independent. Shows that personalization benefit varies systematically with individual characteristics — the heterogeneity the slope network is designed to capture but never tests for. The manuscript should report whether personalization gain correlates with person-level features.

**6.** Hammelrath, L. et al. Comparing personalized and population-based models for predicting momentary negative affect in internalizing disorders: A digital phenotyping study. *Neuroscience Applied* 5, 107006 (2026). DOI *not independently verified*. Peer-reviewed. Cited as ref. 56. Authors independent. Contains the explicit methodological critique — that comparisons omitting a person-specific mean benchmark cannot establish incremental value of passive features — that the present manuscript falls foul of. Its citation without engagement is the most consequential omission in the discussion.

**7.** Terhorst, Y. et al. Investigating Smartphone-Based Sensing Features for Depression Severity Prediction: Observation Study. *Journal of Medical Internet Research* 27, e55308 (2025). DOI: 10.2196/55308 *(high confidence; not independently confirmed)*. Peer-reviewed. Not cited in this manuscript. **Not independent** — shares the senior author (Terhorst) and institutional network with the submission. Reports only modest incremental validity of smart-sensing features over EMA. Directly relevant context for the low absolute R² observed here, and its omission alongside the citation of ref. 65 from the same group is asymmetric.

**8.** Zhu, N. et al. The relation between passively collected data and PTSD: a systematic review and meta-analysis. *npj Digital Medicine* 8, 413 (2025). DOI: 10.1038/s41746-025-01825-6 *(verified)*. Peer-reviewed. Cited as ref. 65. **Not independent** — first author and two co-authors are authors of the present submission. Legitimate as a citation, but self-authorship should be evident to reviewers given its use to support the claim that existing systems are insufficiently personalized.

**9.** McNeish, D. A practical guide to selecting and blending approaches for clustered data: Clustered errors, multilevel models, and fixed-effect models. *Psychological Methods* 31, 225–251 (2026). DOI *not independently verified*. Peer-reviewed. Cited as ref. 24. Authors independent. Provides the framework against which the proposed decomposition should be positioned; the manuscript cites it once for a general claim but never uses it to justify why a two-stage residualization is preferable to joint estimation.

**10.** Digital phenotyping of affect and stress in emerging adults. *Frontiers in Digital Health* (2026). DOI: 10.3389/fdgth.2026.1799541 *(verified)*. Peer-reviewed. Not cited. Authors independent. Compares idiographic and nomothetic XGBoost models for daily affect and stress with sleep, activity, mobility, and phone-use features. A near-identical application with a tree-based rather than neural treatment; its inclusion would let the authors address whether gradient boosting with random effects — repeatedly found superior to neural approaches on tabular clustered data — would outperform the proposed framework. That comparison is currently absent and is a foreseeable reviewer objection.

067390
# Editorial Report — Manuscript 067390 (v2, condensed)

**Title:** ECG-informed pretraining enables precise cardiac assessment from wearable photoplethysmography
**Corresponding authors:** H. Zhou (Samsung Research America / UT Dallas); S. Arcot Desai (Samsung Research America)
**Venue considered:** *Nature Communications* (Digital Health)

---

## Editorial Integrity Alert — Confidential, Handling Editor Only

**1. Undisclosed peer-reviewed status of the foundational prior work (material).** Reference 27 (Zhou et al., "Physiology-aware masked cross-modal reconstruction for biosignal representation learning") is cited only as *arXiv:2605.00973*. Independent search confirms this paper was accepted to ICML 2026 and has been publicly announced as such by Samsung Research America. The submitted manuscript describes its own architecture as "our previously introduced xMAE architecture and directional reconstruction objective, extended from 10 seconds to 30 seconds, while leaving the underlying architecture unchanged." The novel model contribution of the present submission is therefore an input-length change to an already peer-reviewed and accepted model. The authors should be required to disclose the ICML acceptance, supply the accepted version, and state explicitly and quantitatively what is new here relative to that paper.

**2. Probable salami-slicing across a coordinated release.** The ICML paper reports xMAE across 19 downstream tasks including cardiovascular outcome prediction and demographic inference; the present manuscript reports HRV, rhythm, hypertension and age. Public materials from the same group also describe a companion model (HiMAE) released in the same announcement cycle. The overlap in pretraining corpus (MC-MED), architecture, objective, and at least two task families is substantial. The authors must supply a full list of submitted, in-press, and published companion manuscripts and a task-by-task overlap statement.

**3. Selective statistical testing favouring the authors' model.** All comparisons against SL-baseline and NeuroKit2 carry Benjamini–Hochberg-adjusted *P* values. No inferential comparison is reported against PaPaGei or AnyPPG. In Extended Data Table 2 — the only like-for-like (linear-probing) comparison — AnyPPG achieves lower MAE than xMAE-LP on four of five HRV measures (SDNN 0.3701 vs 0.3966; RMSSD 0.4720 vs 0.4754; pNN50 6.6101 vs 7.0802; SD1/SD2 0.1978 vs 0.2031), with xMAE-LP superior only on pNN20. The manuscript text (lines 220–222) states that xMAE "outperformed or performed comparably to" these models. This ordering misrepresents the tabulated result and requires correction before reviewers see the paper.

**4. Apples-to-oranges baseline configuration.** The headline model is fully fine-tuned xMAE, whereas PaPaGei and AnyPPG were evaluated by linear probing only (Methods, lines 974–981). Fine-tuned external baselines are not reported.

**5. Abstract figure not traceable to the Results.** The abstract claims a three-class rhythm AUROC of 0.808 and a 19.4% relative improvement under limited annotations. The Results report only AFib-versus-rest at 64 labelled segments (0.9060 vs 0.7439, a 21.8% relative gain). Neither the 0.808 value nor the 19.4% figure appears in the main text or tables.

**6. Large, unexplained participant exclusions.** 559 participants were excluded from Samsung-Cardio-2 (54.5% of that cohort) and 391 from Samsung-Rhythm-4 (15.5%), attributed to protocol non-compliance and signal quality. No comparison of excluded versus retained participants is provided. Signal-quality screening in PPG correlates with skin tone, adiposity, motion and age, so this is a plausible route to selection bias affecting every reported estimate.

**7. Citation hygiene.** Reference 30 (PaPaGei) is given as "pages 48230–48261, 2025" with no venue; it is an ICLR 2025 conference paper. References 19 and 40 cite *Nature Communications* 2026 with no volume or article number. Reference 4 cites *Nature Medicine* "pages 1–9, 2026." Reference 31 (AnyPPG) is correctly identified as an arXiv preprint.

**8. Competing interests and data access — adequately disclosed.** Samsung employment, funding, and a pending patent naming H.Z., C.T., M.M.R. and S.A.D. are declared. No undisclosed conflict was identified. IRB approval and informed consent are asserted, though no IRB identifiers or protocol numbers are given.

---

## 1. Overall Assessment

The claim is that pretraining a PPG encoder to reconstruct masked, synchronised ECG yields wrist-PPG representations recovering ECG-referenced HRV and three-class rhythm better than pulse-rate-variability proxies or supervised training. The problem is real. Execution is careful across six cohorts and 5,541 participants. Two concerns dominate: the conceptual contribution is not new, and the external-baseline comparison is reported inaccurately.

## 2. Strengths

Pretraining–evaluation separation is cleanly enforced: MC-MED contributed nothing to evaluation, partitions and 2,000-resample bootstraps are participant-level, and thresholds were fixed on validation participants within fold.

The xMAE-shuffle ablation is the most informative experiment. Randomly mismatched ECG–PPG pairs, with architecture and data volume held constant, degrade all five HRV measures (RMSSD 0.5415 vs 0.4754), isolating physiological synchrony from multimodal exposure.

Label efficiency addresses the real bottleneck: at 64 expert-labelled segments per participant, AFib AUROC is 0.9060 versus 0.7439. On-device reporting is candid — 42% and 28% hourly battery, 828.3 ms latency — with continuous inference conceded impractical.

## 3. Weaknesses

Novelty is thin. The architecture is unchanged from reference 27 apart from input duration, and AnyPPG established ECG-guided pretraining at ten times the scale. Abbaspourazad et al. (ICLR 2024, ~141,000 Apple Watch participants) is uncited.

The HRV reference is Galaxy Watch single-lead ECG, not clinical ECG, and its beat-detection error is never quantified. The MC-MED-to-wrist domain shift is unexamined.

The AFib analysis gives 14.8% sensitivity and 10.4% PPV on eight events; the 4.74-fold enrichment framing obscures both. Fairness strata include N=3 and N=2, with a 54.5% exclusion rate in Samsung-Cardio-2 unexplained. Five of six datasets are proprietary. Hypertension and age transfer show fully overlapping intervals with no testing.

## 4. Editorial Decision

**Send for Review**, contingent on the authors first correcting Alert items 1, 3 and 5 — the undisclosed ICML acceptance, the inverted reading of Extended Data Table 2, and the untraceable abstract figures. Reviewers should adjudicate: whether the input-length extension plus new evaluations constitute a contribution distinct from the ICML paper; whether the data-efficiency defence against AnyPPG survives fine-tuned baselines or a matched-data scaling test; whether consumer single-lead ECG is an acceptable reference for sub-50-ms metrics such as pNN20; and whether the AFib section warrants retention as more than exploratory.

**Steelman against this decision.** I still prefer reject with transfer to *npj Digital Medicine*. Neither decisive problem is revisable by peer review: the architecture is peer-reviewed elsewhere, and no external party can reproduce any evaluation number. The counter-case is that this is a measurement-fidelity paper, not a foundation-model paper, and on that framing it is close to best-in-class — the pNN20 result is mechanistically predicted rather than merely observed, and the shuffle ablation excludes the trivial explanation.

## 5. Suggested Reviewer Expertise

Self-supervised and masked-reconstruction pretraining for physiological time series, specifically cross-modal ECG–PPG objectives and the design of ablations that isolate temporal correspondence from multimodal exposure. Benchmarking methodology for PPG foundation models, including fine-tuning versus linear-probing protocol fairness, matched-compute scaling comparisons, and evaluation against PaPaGei, AnyPPG, and Apple Heart and Movement Study encoders. Signal processing for pulse rate variability versus heart rate variability, covering beat-detection algorithm error, reference-standard uncertainty in single-lead wearable ECG, and the sensitivity of RMSSD, pNN20 and SD1/SD2 to timing jitter. Optical physiology and PPG signal quality, particularly skin-pigmentation and perfusion effects on reflective green-LED wrist sensing and the selection bias induced by quality-control exclusion pipelines. Clinically, cardiac electrophysiology with direct experience of consumer-wearable AFib screening trials, competent to adjudicate the ectopy-versus-AFib discrimination claim, the positive predictive value of opportunistic flagging in low-prevalence ambulatory populations, and the downstream burden of false alerts.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant landscape has consolidated rapidly around PPG foundation models. Abbaspourazad et al. (ICLR 2024) trained participant-level contrastive PPG and ECG encoders on approximately 141,000 Apple Heart and Movement Study participants over three years — by an order of magnitude the largest consumer-wearable PPG pretraining effort, and directly comparable in deployment setting to the present work. Pillai et al. introduced PaPaGei (ICLR 2025), the first openly released PPG foundation model, pretrained on 57,000 hours with a morphology-aware objective and validated across ten downstream datasets. Nie et al. released AnyPPG (arXiv:2511.01747, 2025), which pretrains PPG with explicit ECG guidance on over 100,000 hours from six synchronised sources including MC-MED, reporting state-of-the-art results across eleven physiological tasks and screening 1,014 ICD-10 categories. Saha et al.'s Pulse-PPG (IMWUT 2025) contributed field-trained rather than laboratory-trained pretraining, and Narayanswamy et al.'s LSM (ICLR 2025) established scaling behaviour for multimodal wearable sensor models. On the measurement-fidelity side, Charlton et al. (*Proceedings of the IEEE*, 2022; *Physiological Measurement*, 2022) provide the benchmark characterisation of open-source PPG beat detection and its error structure, and Mejía-Mejía et al. (*npj Digital Medicine*, 2021) documented how blood-pressure state dissociates PRV from HRV — the precise physiological mechanism this manuscript invokes.

Situated against that landscape, the manuscript's contribution narrows considerably. Its core premise, that ECG supervision during pretraining yields better PPG timing representations, is AnyPPG's premise, published roughly nine months earlier and at ten times the data scale; the manuscript treats it as an external baseline rather than as prior art establishing the idea. The specific masked cross-modal reconstruction mechanism is the authors' own ICML 2026 contribution, extended here only in input duration. What is genuinely additive is the downstream evaluation design: no prior work has systematically measured ECG-referenced HRV recovery across five variability-sensitive metrics with participant-level bootstrap inference on ambulatory wrist PPG, nor characterised label efficiency for three-class rhythm assessment at 64 to 512 expert-labelled segments per participant, nor reported honest on-device power and latency. That is a real but incremental contribution. The authors must engage directly with Abbaspourazad et al., which is absent from the reference list despite being the closest precedent, and must reframe AnyPPG as prior art rather than as a competitor whose superiority on four of five endpoints goes unremarked. They should also address why the AHMS-scale precedent does not undermine their framing of 20,884 pretraining participants as large-scale.

## 7. Suggested Reviewer Names

**Self-supervised cross-modal biosignal pretraining.** *Arvind Pillai* (Dartmouth College) — first author of PaPaGei (ICLR 2025), the directly comparable open PPG foundation model and one of this manuscript's own baselines. *Mohammad Malekzadeh* (Nokia Bell Labs, Cambridge) — senior author of PaPaGei, with specific expertise in evaluation protocol fairness across probing and fine-tuning regimes. *Dimitris Spathis* (Nokia Bell Labs / University of Cambridge) — PaPaGei co-author with a longer track record in self-supervised wearable sensing and transfer evaluation. *Maxwell A. Xu* (University of Illinois Urbana-Champaign) — author of RelCon and related work on contrastive objectives for wearable time series, well placed to adjudicate the shuffle ablation.

**PPG foundation-model benchmarking and ECG guidance.** *Guangkun Nie* (Peking University) — first author of AnyPPG (arXiv:2511.01747), the ECG-guided PPG foundation model that is both the closest prior art and the strongest baseline; ideally suited to assess whether the manuscript's characterisation of Extended Data Table 2 is accurate. *Shenda Hong* (Associate Professor, National Institute of Health Data Science, Peking University) — senior author of AnyPPG and of multiple ECG foundation models; note the direct competitive relationship and consider as an alternative if the editor prefers distance. *Mithun Saha* (University of Memphis) — first author of Pulse-PPG (IMWUT 2025), with specific expertise in field- versus laboratory-collected PPG and the domain-shift question this manuscript leaves open.

**PRV/HRV measurement fidelity and PPG signal quality.** *Peter H. Charlton* (University of Cambridge) — author of the benchmark study on open-source PPG beat-detection algorithms (*Physiological Measurement* 43:085007, 2022), cited by this manuscript; the correct reviewer for whether NeuroKit2 defaults constitute a fair rule-based baseline and for reference-standard error. *Elisa Mejía-Mejía* (City, University of London) — first author on the differential effects of blood-pressure state on PRV versus HRV (*npj Digital Medicine* 4:82, 2021), the mechanistic foundation of the manuscript's motivating argument. *Berken Utku Demirel* (ETH Zürich) — work on temporal cardiovascular dynamics for PPG-based heart-rate estimation, competent on timing-error propagation into RMSSD and pNN metrics.

**Clinical cardiac electrophysiology and wearable rhythm screening.** *Shaan Khurshid* (Assistant Professor, Massachusetts General Hospital / Harvard Medical School) — co-author on consumer wearable cardiac sensor adoption in primary care (*Circulation: Cardiovascular Quality and Outcomes*, 2022, this manuscript's reference 1) and on large-scale AF screening; the right person to assess the 10.4% PPV and false-alert burden. *Arunashis Sau* (NIHR Clinical Lecturer, Imperial College London) — AI-ECG for AF and arrhythmia phenotyping, with a clinical trials perspective on opportunistic screening thresholds. *Marco V. Perez* (Associate Professor, Stanford University) — principal investigator of the Apple Heart Study (*NEJM* 2019, reference 3), authoritative on what constitutes adequate evidence for wearable AFib detection claims.

---

## Further Literature — 10 Papers of Similar Scope, Past Three Years

**1.** Pillai, A., Spathis, D., Kawsar, F. & Malekzadeh, M. PaPaGei: Open foundation models for optical physiological signals. *The Thirteenth International Conference on Learning Representations (ICLR)*, 2025. arXiv:2410.20542.
*Peer-review status:* Peer-reviewed conference paper (ICLR 2025). *Cited by manuscript:* Yes, reference 30, but with the venue omitted and given only as page numbers. *Independence:* Independent (Nokia Bell Labs / Dartmouth College).
*Relevance:* The only open-weight comparator and one of the manuscript's two external baselines. Pretrained on 57,000 hours of public PPG with a morphology-aware objective. Directly tests whether ECG guidance is necessary or whether PPG-only pretraining with a strong inductive bias suffices. The citation must be corrected, and PaPaGei must be fine-tuned rather than only linear-probed if the comparison is to be fair.

**2.** Nie, G., Tang, G., Xiao, Y., Li, J., Huang, S., Zhang, D., Zhao, Q. & Hong, S. AnyPPG: An ECG-guided PPG foundation model trained on over 100,000 hours of recordings for holistic health profiling. arXiv:2511.01747, 2025.
*Peer-review status:* **arXiv preprint — not peer-reviewed.** *Cited by manuscript:* Yes, reference 31, correctly identified as a preprint. *Independence:* Independent (Peking University).
*Relevance:* The single most consequential item. Establishes ECG-guided PPG pretraining as prior art at roughly ten times the scale, also draws on MC-MED, and beats xMAE-LP on four of five HRV measures in the manuscript's own Extended Data Table 2. Its preprint status is a caveat for citation weight, not for priority of the idea.

**3.** Abbaspourazad, S., Elachqar, O., Miller, A. C., Emrani, S., Nallasamy, U. & Shapiro, I. Large-scale training of foundation models for wearable biosignals. *The Twelfth International Conference on Learning Representations (ICLR)*, 2024. arXiv:2312.05409.
*Peer-review status:* Peer-reviewed conference paper (ICLR 2024). *Cited by manuscript:* **No — a material omission.** *Independence:* Independent (Apple).
*Relevance:* Trains PPG and ECG encoders on approximately 141,000 Apple Watch participants over three years — the closest precedent in device class, deployment setting and scale, roughly seven times this manuscript's pretraining cohort. Its absence props up the paper's framing of 20,884 participants as large-scale.

**4.** Zhou, H., Lee, S. A., Tanade, C., Chun, K. S., Lee, J., Gwak, M., Thukral, M., Sung, J., Hwang, E., Bin Morshed, M., Zhu, L., Nathan, V., Rahman, M. M., Venkatraman, S. & Arcot Desai, S. Physiology-aware masked cross-modal reconstruction for biosignal representation learning. *International Conference on Machine Learning (ICML)*, 2026 (accepted). arXiv:2605.00973.
*Peer-review status:* Accepted at ICML 2026; cited by the manuscript only as an arXiv preprint. *Cited by manuscript:* Yes, reference 27, with peer-review status undisclosed. *Independence:* **Same submitting group — overlapping author list.**
*Relevance:* Defines the xMAE architecture and objective reused unchanged here apart from input duration, and reports 19 downstream tasks including cardiovascular outcome prediction and demographic inference. Reviewers must be given this paper alongside the submission.

**5.** Chen, Z. et al. GPT-PPG: a GPT-based foundation model for photoplethysmography signals. *Physiological Measurement* 46(5), 055004 (2025). DOI: 10.1088/1361-6579/add988.
*Peer-review status:* Peer-reviewed. *Cited by manuscript:* No. *Independence:* Independent.
*Relevance:* An autoregressive rather than masked-reconstruction pretraining objective for PPG, published in the same period. Establishes that the design space of PPG pretraining objectives is broader than the manuscript's masked-versus-contrastive framing acknowledges, and provides an additional reference point for AFib detection performance from PPG alone.

**6.** Saha, M., Xu, M. A., Mao, W., Neupane, S., Rehg, J. M. & Kumar, S. Pulse-PPG: An open-source field-trained PPG foundation model for wearable applications across lab and field settings. *Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies (IMWUT)* 9 (2025). arXiv:2502.01108.
*Peer-review status:* Peer-reviewed (IMWUT). *Cited by manuscript:* No. *Independence:* Independent.
*Relevance:* Directly addresses laboratory-to-field generalization, the question this manuscript raises through its MC-MED-to-free-living transfer but never tests. Relevant to the claim that gains hold across diverse real-world wearable environments, currently asserted from subgroup consistency alone.

**7.** Narayanswamy, G., Liu, X., Ayush, K., Yang, Y., Xu, X., Liao, S., Garrison, J., Tailor, S., Sunshine, J., Liu, Y. et al. Scaling wearable foundation models (LSM). *The Thirteenth International Conference on Learning Representations (ICLR)*, 2025. arXiv:2410.13638.
*Peer-review status:* Peer-reviewed conference paper. *Cited by manuscript:* No. *Independence:* Independent (Google).
*Relevance:* Establishes scaling laws for multimodal wearable sensor foundation models across imputation, interpolation and extrapolation. Pertinent because the manuscript's defence against AnyPPG is a data-efficiency argument (10,000 versus 100,000 hours) that is asserted but never demonstrated; a scaling analysis in this style is what would substantiate it.

**8.** Gruwez, H. et al. FibriCheck detection capabilities for atrial fibrillation (FDA–AF): a multicenter validation study. *npj Digital Medicine* (2025). DOI: 10.1038/s41746-025-02059-2.
*Peer-review status:* Peer-reviewed. *Cited by manuscript:* No. *Independence:* Independent.
*Relevance:* A prospective multicentre validation of PPG-based AFib detection against clinical reference, and the appropriate evidentiary benchmark for this manuscript's rhythm claims. Critically, it reports reduced sensitivity in individuals with darker skin tones and higher BMI — the exact fairness axis the present manuscript cannot address because its race strata contain as few as two participants and its quality-control pipeline may remove affected participants before analysis.

**9.** Nie, G., Zhao, Q., Tang, G., Li, Y. & Hong, S. Artificial intelligence-derived photoplethysmography age as a digital biomarker for cardiovascular health. *Communications Medicine* 5, 481 (2025). DOI: 10.1038/s43856-025-01188-9.
*Peer-review status:* Peer-reviewed. *Cited by manuscript:* No. *Independence:* Independent (Peking University).
*Relevance:* PPG-derived age estimation on UK Biobank (N = 212,231) with external validation in a MIMIC-III-derived cohort, with the age gap linked to major cardiovascular events. The manuscript presents age estimation (MAE 6.03 years in N = 370) as evidence of transfer without engaging this far larger, outcome-anchored precedent, and without acknowledging that age-gap magnitude, not age MAE, is the clinically meaningful quantity.

**10.** Miller, A. C., Futoma, J., Abbaspourazad, S., Heinze-Deml, C., Emrani, S., Shapiro, I. & Sapiro, G. A wearable-based aging clock associates with disease and behavior. *Nature Communications* 16, 9264 (2025).
*Peer-review status:* Peer-reviewed (*Nature Communications*). *Cited by manuscript:* No. *Independence:* Independent (Apple).
*Relevance:* Establishes what a *Nature Communications*-tier wearable phenotyping claim currently looks like — population-scale, outcome-linked, and behaviourally validated. A useful calibration point for the editor and for reviewers assessing whether the hypertension and age sections here, resting on a single 370-participant cohort with overlapping confidence intervals and no significance testing, meet that standard.

*Note on the pretraining corpus:* MC-MED is described in Kansal, A., Chen, E., Jin, B. T., Rajpurkar, P. & Kim, D. A., *Scientific Data* 12, 1094 (2025), DOI 10.1038/s41597-025-05419-5 (peer-reviewed; cited as references 25 and 26). It comprises 118,385 adult emergency-department visits recorded on Philips IntelliVue bedside monitors. Reviewers should be pointed to this when assessing the unexamined shift from ED fingertip transmissive PPG to ambulatory wrist reflective PPG.

---

*Report prepared for internal editorial use. The Confidential Editorial Integrity Alert should not be transmitted to authors or reviewers.*

068295
# Editorial Report — Manuscript 068295

**Title:** Automated language impairment screening in acute stroke using connected speech
**Authors:** L. S. Pugalenthi (Rice University), T. T. Schnur (UTHealth Houston; corresponding)
**Venue considered:** *Nature Communications*, Digital Health
**Handling editor assessment date:** 20 August 2026

---

## Editorial Integrity Alert (confidential — handling editor only)

Several matters require resolution before this manuscript proceeds, whatever the eventual decision.

**Citation misattribution, high severity.** On page 11 the authors describe "Local Interpretable Model-agnostic Explanations (LIME^30)" and cite reference 30 as Lundberg & Lee (2017), *A Unified Approach to Interpreting Model Predictions*. That paper introduces SHAP, not LIME; LIME is Ribeiro, Singh & Guestrin (2016). The authors then propose to use "LIME" to highlight word-level impairments. SHAP and LIME are different methods with different theoretical properties, and the substituted citation cannot support the sentence. This is not a typographical slip: the acronym is expanded in full and attached to the wrong primary source.

**Second citation misattribution.** Reference 20 (Huang, Pareek, Seyyedi, Banerjee & Lungren, 2020, *npj Digital Medicine*) is a review of multimodal fusion of imaging and EHR data. It is used on page 3 to support the general claim that ensemble modelling boosts predictive accuracy, on pages 17 and 19 to support "late-fusion" ensembling, and on page 20 to support scikit-learn's `permutation_importance`. It cannot support the last of these at all, and is a weak authority for the first two. In the Results (page 6, line 10) permutation importance is instead cited to reference 21 (Breiman, 2001). The manuscript therefore attributes the same method to two different and largely inappropriate sources in different sections.

**Systematic off-by-one citation shift in the Introduction and Methods.** Page 4 cites "GloVe^21" and "(BERT, Mistal, and OpenAI)^22-24", whereas the reference list assigns GloVe = 22, BERT = 23, Mistral = 24, OpenAI = 25, and the Results sections use the correct numbering. The same shift appears on page 13, where dynamic aphasia is cited to reference 34 (Walker et al., naming test) rather than reference 35 (Robinson et al., dynamic aphasia). At least two independent numbering systems appear to have been merged. Every in-text citation requires re-verification, not only the instances identified here.

**Uncited reference.** Reference 61 (Jiang et al., *Mistral 7B*) does not appear to be cited anywhere in the main text; Mistral is cited to reference 24 (Choi et al., Linq-embed-mistral technical report). Uncited entries are a routine marker of reference-manager contamination and reinforce the concern above.

**Undisclosed author overlap with a cited work.** Reference 28 (Hilsabeck et al., 2025, *Alzheimer's & Dementia: TRCI*) lists "Pugalenthi, L." among its authors — the first author of the present submission. It is cited twice as third-party evidence: once as an example of "screening apps in other clinical populations" (page 11) and once as the source of "code adapted from previous studies" (page 15). Neither instance is marked as self-citation. This is not misconduct, but the second use has methodological consequence: if feature-extraction code is shared with a prior study by the same author, its provenance and validation status must be stated.

**Cohort reuse and salami-slicing risk.** The Methods state the cohort is drawn from "a larger prospective project" (R01DC014976). References 10 (Ding, Martin, Hamilton & Schnur, 2020, *Brain*), 11 (Martin & Schnur, 2019, *Cortex*) and 12 (Schnur & Lei, 2022, *Neuropsychology*) are all acute-stroke connected-speech or naming studies from the senior author's group. Reference 12 supplies the identical 69-item confrontation naming battery used here to define one of the three ground-truth criteria, and the Methods state explicitly that the present study departs from Schnur & Lei only in how articulatory errors are scored. The degree of participant overlap with these prior publications is not disclosed anywhere. A participant-level overlap statement should be requested before any review.

**Self-citation density.** The senior author is an author on at least five of the 65 references (7, 8, 10, 11, 12), plus the shared cohort. This is within normal bounds for a specialised sub-field, but combined with the absence of an overlap statement it warrants notice.

**Non-standard source for a methodological choice.** Reference 59 (Bedrick, 2024) is a lecture-series webpage, not a citable publication, and is the sole authority for the ROC threshold-selection procedure that determines every headline number in the paper. The procedure must be described in full in the Methods rather than delegated to a URL.

**Undisclosed preprint.** Searches did not surface a preprint of this manuscript on medRxiv, bioRxiv or arXiv. The Acknowledgements disclose presentation of portions of this work at the 2025 Cognitive Neuroscience Society meeting, which is adequate.

**Absent statements.** There is no data availability statement, no code availability statement, and no reporting-guideline adherence statement (STARD and TRIPOD+AI both apply). Race and ethnicity are not reported at all for a Houston-based cohort, despite the Discussion invoking "culture diversity" as future work. These are mandatory before any *Nature*-portfolio decision.

**Numerical inconsistency, main text.** Page 8, lines 2–4: independent embedding classifiers are said to range from "72-83% balanced accuracy," followed immediately by the statement that Mistral achieved the highest at 84%. One of these numbers is wrong. The downstream claim that the ensemble beat independent classifiers "by ≥6%" is consistent with 84 and inconsistent with 83.

---

## §1 Overall Assessment

The manuscript transcribes acute stroke story retellings (n=86) with Whisper large-v3, derives linguistic features and GloVe/BERT/Mistral/OpenAI embeddings, and stacks classifiers into ensembles reaching 90% balanced accuracy (79% sensitivity, 100% specificity) for impaired-versus-unimpaired acute stroke patients. The target problem is right; execution doesn't support the claim. Algorithm selection, ROC threshold, and stacking all reuse the same LOOCV predictions later reported as performance, so 90% is an unquantified upper bound. No WER is reported for Whisper, and articulatory errors are scored as naming errors, so the classifier may detect dysarthria and ASR degradation rather than language impairment.

---

## §2 Strengths

The impaired-versus-unimpaired-within-stroke comparison, recruited consecutively across four sites, is the clinically correct design, unlike prior stroke-versus-control work (refs 13–17). Test timing to the reference standard is documented (mean 4 days post-stroke; NIHSS Item 9 within 0.2 days), meeting a STARD standard most papers skip. The embeddings-vs-discrete-features comparison runs against a most-frequent-class baseline; embeddings gain entirely in specificity (74%→100%) at constant sensitivity, a real result. Permutation importance across ensemble members (OpenAI 16%, Mistral 13%, GloVe 6%, BERT 3%) tests complementarity directly.

---

## §3 Weaknesses

Algorithm, threshold, and stacking selection all reuse the same LOOCV outputs later reported as performance — the near-identical balanced-accuracy/AUC pairs (90/90) are consistent with this. No WER is reported, and articulatory scoring is built into the naming-error criterion, so dysarthria can independently drive both transcription failure and a positive label. The reference standard is heterogeneous (40/63 positives meet only one of three criteria) and partly circular via NIHSS Item 9; 9 participants were excluded post hoc using that same standard. The claim that false negatives cluster in mild cases is arithmetically wrong (9/13 observed vs. 8.3 expected). No trustworthy confidence intervals, no calibration, no subgroup or race/ethnicity reporting, and no comparison against NIHSS Item 9 alone.

---

## §4 Editorial Decision

**Reject**, with offer of transfer. The unquantified performance inflation and the unexcluded dysarthria confound are design-level flaws, not fixable by re-analysis alone; reviewers cannot currently adjudicate the central claim.

**Steelman.** The within-stroke design and test timing are above field norms, and the specificity gain is informative even under an inflated scale. If manual transcripts and dysarthria ratings exist, Major Revision would be more proportionate; I don't adopt this because the ASR confound can't be pre-adjudicated without corrected results.

**Transfer:** *npj Digital Medicine* or *Communications Medicine*, conditional on correcting the LIME/SHAP misattribution and citation numbering.

---

## §5 Suggested Reviewer Expertise

Reviewers should be sought across five areas, weighted roughly seventy percent technical to thirty percent clinical. First, automatic speech recognition for disordered and pathological speech, specifically Whisper-family model behaviour on aphasic and dysarthric speech, word error rate characterisation, and the effect of ASR normalisation on paraphasia preservation — this is the axis on which the manuscript's central confound lives. Second, sentence and document embedding methods for clinical text classification, covering CLS-token versus mean-pooled representations, embedding model selection, and dimensionality reduction under small-sample regimes. Third, machine learning methodology for small clinical cohorts, specifically nested cross-validation, stacked generalisation and its leakage modes, decision-threshold selection, calibration, and confidence interval construction under dependent resampling; a reviewer with TRIPOD+AI or STARD adjudication experience is preferred. Fourth, quantitative connected-speech and discourse analysis in aphasia, covering core lexicon, main concept, informativeness and global coherence measures, and the psychometrics of discourse-derived indices. Fifth, clinical acute stroke care with direct speech-language pathology experience in the first week post-stroke, including NIHSS Item 9 administration and its known ceiling behaviour, differential diagnosis of aphasia from dysarthria and apraxia of speech, and the referral pathways the authors propose to influence.

---

## §6 State-of-the-Art Literature Review (Past 3 Years)

The sub-field has moved in three directions since 2023, and the manuscript engages with only one of them. The first is the systematic characterisation of ASR failure on pathological speech. Sanguedolce, Naylor & Geranmayeh (ACL Clinical NLP Workshop, 2023) established that Whisper's word error rate in post-stroke aphasia is approximately 38.5% against 10.3% in age-matched controls, that WER scales with expressive and receptive impairment severity, and that left frontal lesions specifically degrade performance; the follow-up Interspeech 2024 work and the SONIVA database (approximately 1,000 stroke survivors) extend this substantially. Davudova et al. (2025) further show that baseline Whisper performs poorly on short clinical utterances and generalises badly out of domain. None of this work is cited. Its omission is not a bibliographic oversight: it is the literature that establishes the alternative explanation for the present results, and the manuscript's sole justification for choosing Whisper — one sentence citing Cong et al. (2024) in chronic stroke — does not engage with it.

The second direction is the fusion of transformer embeddings with handcrafted linguistic features, which is precisely the manuscript's third aim. Agbavor & Liang (2022, *PLOS Digital Health*) and Llaca-Sánchez et al. (2025) are cited; the more directly comparable LLMCARE work of Zolnour et al. (2025, *Frontiers in Artificial Intelligence*) is not, and it reaches the opposite conclusion — that integrating transformer embeddings with handcrafted features improves detection of cognitive impairment from speech, whereas here the addition degrades balanced accuracy. A submission whose stated aim is to test complementarity must engage with a contemporaneous contrary result. The third direction is detection of mild and subclinical language impairment, where Bunker et al. (2025, *AJSLP*) show that discourse measures capture deficits the WAB-R Aphasia Quotient misses, and Stark, Dalton & Lanzi (2025, *Frontiers in Human Neuroscience*) characterise latent aphasia through context-specific lexical-semantic access during discourse. Both are cited but neither is used as a benchmark, and neither informs the composite reference standard, which is where their contribution would have been most valuable.

Situating the manuscript: its genuine advance is the within-acute-cohort contrast on a consecutively recruited multi-site sample, a real step beyond the stroke-versus-control designs of Boucher et al. (2022) and the chronic-stage classification of Cong et al. (2024) and Wagner, Zusag & Bloder (2023). Its claim to be first to differentiate acute patients with and without impairment at the individual level appears defensible on current evidence. Where it replicates rather than advances is in the embedding-versus-discrete-feature comparison, run repeatedly in neurodegenerative cohorts with broadly the same answer, and in the observation that ensembling helps. The competing work it must engage with before publication anywhere is the Imperial College ASR-validation series, because that literature is what turns the present results from a screening finding into an open question.

---

## §7 Suggested Reviewer Names

For automatic speech recognition in pathological speech, **Giulia Sanguedolce** (Imperial College London), first author of *Uncovering the Potential for a Weakly Supervised End-to-End Model in Recognising Speech from Patients with Post-Stroke Aphasia* (ACL Clinical NLP Workshop, 2023) and of the SONIVA database, is the single most relevant reviewer available and is not cited by the authors. **Dragos C. Gruia** (Imperial College London), co-author on *When Whisper Listens to Aphasia* (Interspeech 2024) and on the IC3 post-stroke cognition programme, is a suitable alternative from the same methodological tradition. **Laurin Wagner** or **Marc Zusag**, authors of *Careful Whisper* (Interspeech 2023; the manuscript's reference 14), can adjudicate whether Whisper's normalisation behaviour erases the paraphasic evidence the embeddings are assumed to encode.

For embeddings and LLM-based clinical text classification, **Yan Cong** (Purdue University), first author of *Clinical efficacy of pre-trained large language models through the lens of aphasia* (*Scientific Reports*, 2024; the manuscript's reference 15 and the entire basis for its Mistral recommendation), is the direct comparator and should be asked whether the present comparison is like-for-like. **Maryam Zolnoori** (Columbia University), senior author of LLMCARE (*Frontiers in Artificial Intelligence*, 2025), has run the embedding-plus-handcrafted-feature fusion experiment in a neurodegenerative cohort and reached the opposite result. **Kathleen C. Fraser** (National Research Council Canada), author of the automated PPA subtype classification work cited as reference 54, brings long experience of exactly this feature-set comparison.

For small-sample clinical ML methodology and computational aphasiology, **Steven Bedrick** (Oregon Health & Science University) is the natural choice given that the manuscript's threshold-selection procedure is attributed to him; note as a mild conflict consideration that the attribution is to an unpublished lecture and may indicate prior contact. **Charalambos Themistocleous** (University of Oslo), author of the automatic aphasia subtyping work cited as reference 52, is an unconflicted alternative with directly comparable classification experience.

For mild and subclinical impairment detection and acute clinical context, **Lisa D. Bunker** (Johns Hopkins University), first author of *Discourse Measures From the Modern Cookie Theft Picture Description Are Sensitive to Mild Communication Deficits Not Captured by the Western Aphasia Battery–Revised Aphasia Quotient* (*AJSLP*, 2025; reference 17), directly addresses the manuscript's weakest construct — what counts as mild impairment and how it should be labelled. **Brielle C. Stark** (Indiana University), first author of the 2025 latent aphasia paper (reference 44), is the closest analogue to the present classification target and should be asked specifically about the adequacy of the three-criterion composite reference standard.

Reviewers should be selected so that at least one is asked explicitly to adjudicate the leakage question, at least one the ASR-confound question, and at least one the adequacy of the ground-truth label. Note that Bunker, Stark, Fraser, Themistocleous, Cong and Bedrick are all cited by the manuscript; this is not disqualifying but should be weighed when balancing the panel. **Hanjie Chen** (Rice University) is thanked in the Acknowledgements for suggesting the multi-LLM evaluation and must be excluded on conflict grounds.

---

## Further Literature (Past 3 Years, Annotated)

**1.** Bunker, L. D., Berube, S. K., Neal, V., Kelly, L., Kelly, C., Meier, E. L., & Hillis, A. E. (2025). Discourse Measures From the Modern Cookie Theft Picture Description Are Sensitive to Mild Communication Deficits Not Captured by the Western Aphasia Battery–Revised Aphasia Quotient. *American Journal of Speech-Language Pathology*, 34(3), 1100–1120. DOI: 10.1044/2024_AJSLP-24-00322. *Peer-reviewed.* Cited by the manuscript (ref. 17). Authors independent of the submitting group. Establishes that discourse-derived measures detect deficits standardised batteries miss — the premise on which this submission rests. Cited but never used as a benchmark; the authors should be asked why their discrete linguistic feature set does not overlap with Bunker's validated measures.

**2.** Cong, Y., LaCroix, A. N., & Lee, J. (2024). Clinical efficacy of pre-trained large language models through the lens of aphasia. *Scientific Reports*, 14(1), 15573. *Peer-reviewed.* Cited (ref. 15). Independent. The manuscript's sole justification both for choosing Whisper and for recommending Mistral-based embeddings in future work. Because the entire "prioritize Mistral" recommendation rests on consistency with this one chronic-stage study, reviewers should verify that the embedding models, task, and cohort stage are genuinely comparable.

**3.** Sanguedolce, G., Naylor, P. A., & Geranmayeh, F. (2023). Uncovering the Potential for a Weakly Supervised End-to-End Model in Recognising Speech from Patients with Post-Stroke Aphasia. *Proceedings of the 5th Clinical Natural Language Processing Workshop*, ACL, 182–190. DOI: 10.18653/v1/2023.clinicalnlp-1.24. *Peer-reviewed (workshop proceedings).* **Not cited.** Independent. Reports Whisper WER of 38.5% in post-stroke aphasia versus 10.3% in controls, scaling with severity and worsening with left frontal lesions. This is the single most consequential omission in the reference list and is the basis of the ASR-confound weakness above.

**4.** Sanguedolce, G., Brook, S., Gruia, D. C., Naylor, P. A., & Geranmayeh, F. (2024). When Whisper Listens to Aphasia: Advancing Robust Post-Stroke Speech Recognition. *Proceedings of Interspeech 2024*, 1995–1999. *Peer-reviewed (conference proceedings).* **Not cited.** Independent. Demonstrates that Whisper requires fine-tuning to reach acceptable WER on stroke speech (approximately 21.5% after adaptation). Directly undermines the manuscript's one-sentence justification for using off-the-shelf Whisper large-v3 without validation.

**5.** Sanguedolce, G., et al. (2025). SONIVA: Speech recOgNItion Validation in Aphasia. *medRxiv*. DOI: 10.1101/2025.06.03.25328889. **Preprint — not peer-reviewed; flagged accordingly.** Not cited. Independent. Approximately 1,000 stroke survivors with orthographic and IPA transcription. Relevant chiefly because the manuscript claims to represent "the largest acute stroke cohort to date"; that claim is defensible only under a narrow definition of "acute," and the authors should state the definition explicitly rather than leave the superlative unqualified.

**6.** Davudova, M., Cai, Z., Giunchiglia, V., Gruia, D. C., Sanguedolce, G., Hampshire, A., & Geranmayeh, F. (2025). Application of Whisper in Clinical Practice: the Post-Stroke Speech Assessment during a Naming Task. *arXiv:2507.17326*. **arXiv only — not peer-reviewed; flagged accordingly.** Not cited. Independent. Shows baseline Whisper performs poorly on short utterances and generalises poorly out of domain (TORGO). Useful as a caution rather than as evidence, given its preprint status.

**7.** Zolnour, A., Azadmaleki, H., Haghbin, Y., et al. (2025). LLMCARE: early detection of cognitive impairment via transformer models enhanced by LLM-generated synthetic data. *Frontiers in Artificial Intelligence*, 8, 1669896. DOI: 10.3389/frai.2025.1669896. *Peer-reviewed.* **Not cited.** Independent. Reports that integrating transformer embeddings with handcrafted linguistic features *improves* detection of cognitive impairment from speech — the opposite of the present finding. A submission whose third aim is complementarity must engage with a contemporaneous contrary result.

**8.** Merhbene, G., Lecron, F., Fortemps, P., Dickerson, B. C., Kurpicz-Briki, M., & Rezaii, N. (2026). Detecting Primary Progressive Aphasia (PPA) from Text: A Benchmarking Study. *Findings of the ACL: EACL 2026*, 355–374. DOI: 10.18653/v1/2026.findings-eacl.19. *Peer-reviewed (conference findings).* Cited (ref. 31). Independent. Invoked to support the proposed LIME-based interpretability extension — the same sentence containing the LIME/SHAP misattribution. Reviewers should confirm which attribution method this benchmarking study actually employs before the authors' future-work plan is accepted as coherent.

**9.** Stark, B. C., Dalton, S. G., & Lanzi, A. M. (2025). Access to context-specific lexical-semantic information during discourse tasks differentiates speakers with latent aphasia, mild cognitive impairment, and cognitively healthy adults. *Frontiers in Human Neuroscience*, 18, 1500735. DOI: 10.3389/fnhum.2024.1500735. *Peer-reviewed.* Cited (ref. 44). Independent. The closest published analogue to the present classification target, since "latent aphasia" is operationally similar to the single-criterion subgroup that supplies most of this model's false negatives. Should have informed the composite reference standard rather than appearing only as a feature-derivation citation.

**10.** Hilsabeck, R. C., Keller, J. N., Henry, M. L., Li, J. J., **Pugalenthi, L.**, Toprac, P., et al. (2025). Development and classification accuracy of an automated cognitive screening tool combining working memory and connected speech tasks for early detection of cognitive impairment in primary care. *Alzheimer's & Dementia: Translational Research & Clinical Interventions*, 11(3), e70145. DOI: 10.1002/trc2.70145. *Peer-reviewed.* Cited (refs. 28, 48). **Author overlap: the submitting first author is a co-author; this is not disclosed as self-citation in either instance, including where it is cited as the source of feature-extraction code.** Independent verification of that code's provenance and validation status should be requested.

068534
# Editorial Report — Manuscript 068534

**Title:** Retinal boundary-context modulation enables signed contextual adjustment of edge evidence
**Corresponding authors:** Baoqi Zheng, Shumao Xu (Fudan University)
**Handling venue:** *Nature Communications*

---

## Editorial Integrity Alert (Confidential — Handling Editor Only)

**1. Competing-interests declaration appears incomplete.** The authors state "The authors declare no competing interests." Two co-authors hold commercial affiliations: Mengrong Zhang (Lizhi Biotechnology Co., Ltd., Shanghai) and Zhicai Lv (Bioprofile Biotechnology Co., Ltd., Shanghai). Nature Portfolio policy requires disclosure of employment by, or financial interest in, commercial entities regardless of whether the authors judge the interest to be material. A corrected declaration should be requested, together with a statement of what role, if any, either company played in funding, hardware provision, or data generation. The omission is more consequential because the Author Contributions statement assigns "investigation, data curation, validation and resources" to M.Z. and Z.L., the two industry-affiliated authors.

**2. Affiliation 5 is non-specific and likely inaccurate.** "Max Planck Institute, Stuttgart, 70569, Germany" does not name an institute. Postcode 70569 corresponds to the Heisenbergstraße campus, which hosts the Max Planck Institute for Intelligent Systems and the Max Planck Institute for Solid State Research. The corresponding author S.X. lists this alongside Fudan University but uses a fudan.edu.cn address. The specific institute, and the nature and dates of the appointment, should be confirmed directly.

**3. Internal figure-citation error.** In Results, the text states that "each direction comprised 21 nested conditions (3 preparations × 7 grid scales) (Fig. 2d), and each grid scale comprised 24 conditions (3 preparations × 8 directions) (Fig. 2e)." The Figure 2 legend defines panel **d** as grid-scale stability (24 conditions per scale) and panel **e** as directional stability (21 conditions per direction). The two panel calls are transposed.

**4. Apparent numerical discrepancy between Table 1 and Figure 4c.** Table 1 reports same-domain NYUDv2 ODS of 0.8320 (Anchor) and 0.8425 (H-RBCM). The NYUDv2 row of the Fig. 4c ODS heatmap appears to read approximately 83.3 (Plain) and 83.4 (Main). If both refer to the NYUDv2-source model on NYUDv2, the H-RBCM values differ by roughly 0.85 percentage points. The submitted copy is a low-resolution scan, so this reading is provisional; the authors should be asked to reconcile the two or to state explicitly that Fig. 4c derives from a different checkpoint or scalar configuration.

**5. Metric ordering anomaly in Table 1.** For MultiCue, H-RBCM reports ODS 0.9019 with OIS 0.8993 — OIS below ODS. This is the only such inversion among the twelve rows. OIS is not strictly bound to exceed ODS under a per-image-F-averaging definition, but the pattern is atypical, and it occurs on the same dataset where AP simultaneously degrades. The exact OIS aggregation formula should be disclosed and the value confirmed as not a transcription error.

**6. Benchmark values substantially exceed published state of the art, with the official-matcher numbers withheld.** Reported BIPED ODS is 0.9426 for H-RBCM and **0.9296 for the untuned plain HED-lite anchor**. Published BIPED results cluster far lower: PiDiNet trained on BIPED reports ODS ≈ 0.868, DexiNed ≈ 0.857, and diffusion-based methods ≈ 0.892–0.896. A 6.64M-parameter HED variant with no contextual operator therefore exceeds published SOTA by roughly four points *before* the paper's contribution is applied. The Methods concede a local evaluator with non-standard distance tolerances (0.0035 of the image diagonal for BIPED, versus the conventional 0.0075) and state that local-evaluator values are not combined with official leaderboard scores. Critically, the Methods also state that BIPED and BSDS500 "were additionally evaluated with the official Berkeley bipartite matcher" — **yet no official-matcher value appears anywhere in the main text, tables, or figure legends.** Either those numbers were computed and omitted, or the claim is inaccurate. This is the most serious issue in the submission and must be resolved before any review.

**7. No undisclosed preprint located.** Searches for "retinal boundary-context modulation," H-RBCM, and the title string returned no arXiv, bioRxiv, or conference version. The GitHub release (liukaiming6563/RBCM-Edge, commit 9a8326a110be12d6fa088d1839a9ad03859a196f) was not independently accessible during preparation of this report and should be confirmed by the editorial office.

**8. No evidence of salami-slicing or cohort reuse.** Three retinas, single institution, no overlapping prior publication identified. Cited references 9, 10 and 16 were independently verified as accurate, including page ranges (MatchED, CVPR 2026, 42093–42103; Huang et al., *Nat. Commun.* **10**, 2431, 2019). Reference-list hygiene is good.

---

## 1. Overall Assessment

The manuscript pairs a retinal observation with a vision contribution and declines to connect them causally. Three mice, unbalanced UME/CME blocks, no cell matching: condition "remains inseparable from block, elapsed time, adaptation and drift." What survives is a three-animal between-block difference used only as a sign constraint motivating a hand-built filter — not mechanism, despite the abstract's causal verb "enables." Cluster yields differ sharply between paired blocks (e.g., 382/652 units), a composition shift sufficient alone to produce the reported differences, undetectable by the within-bin permutation test.

The vision contribution is a fixed post-hoc logit correction improving oracle ODS 0.78–2.22 points while degrading AP up to 4.24 points, conceded but unresolved. More critically, the plain anchor alone reports BIPED ODS 0.9296, exceeding published SOTA (≈0.857–0.896) before any contribution, and the promised official Berkeley-matcher results never appear.

## 2. Strengths

The shared-anchor design correctly isolates the output transformation from backbone capacity. Evaluation freezing is rigorous: scalars fixed on source validation before target inference, seeds recorded, one 30-image UDED set reused throughout. The spatial-localization check (Δz_RBCM +0.291 higher at edges than background, positive in all 30 images, P = 9.31 × 10⁻¹⁰) is a genuine, non-circular mechanism verification.

## 3. Weaknesses

Benchmarks are irreconcilable with the literature and the promised matcher numbers are withheld. The retinal design cannot isolate a surround effect; yield asymmetry alone explains the difference. RBCM's biology is decorative — annuli, weights, and the gate are conceded "engineering hypotheses," fitted to nothing retinal. Gains are oracle-only, with no fixed-threshold results despite the deployment framing. No clinical content fits this venue.

## 4. Editorial Decision

**Reject**, transfer recommended. Benchmark inflation, an unsupportable retinal framing, and a self-withdrawn biological rationale are independent, non-remediable. Best fit: **Communications Engineering**; secondarily **npj Artificial Intelligence** if reframed around post-hoc adjustment. **Steelman**: the disclosed-confound honesty exceeds field norms, and read as a pure vision contribution it is more rigorous than much published work; if matcher results confirm the margins, revisit.

## 5. Suggested Reviewer Expertise

Reviewer one should be an expert in deep edge and boundary detection benchmarking, specifically the ODS, OIS and AP evaluation protocol, the Berkeley bipartite matching implementation, and the sensitivity of reported scores to distance tolerance, non-maximum-suppression settings and precision–recall integration rules; the central task is to adjudicate whether the reported BIPED, MultiCue and NYUDv2 values are comparable to the published literature. Reviewer two should work on crisp and uncertainty-aware edge detection architectures — HED, RCF, BDCN, PiDiNet, EDTER, UAED, DiffusionEdge, RankED, MuGE — and should assess whether a deterministic post-hoc logit correction is a contribution distinct from learned refinement, and whether the shared-anchor controls suffice. Reviewer three should be a retinal electrophysiologist using high-density multi-electrode arrays and Kilosort-family spike sorting in ex vivo mouse retina, competent to judge whether independently sorted, sequentially acquired blocks with large differences in cluster yield can support any population-level comparison. Reviewer four should be a statistician or computational neuroscientist specialising in permutation inference and nested pseudoreplication, able to evaluate whether unit-label permutation within spatial bins provides a valid null when block composition itself differs, and whether Benjamini–Hochberg correction across 168 non-independent re-analyses of three animals is interpretable. Reviewer five, if sought, should work on centre–surround and non-classical receptive-field computation in early vision, to assess whether the square-annular formulation bears a defensible relationship to measured retinal surround organisation.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The edge-detection sub-domain has moved decisively toward modelling annotation ambiguity, crispness and end-to-end differentiability, and this manuscript engages the first only superficially and the second not at all. Zhou et al.'s uncertainty-aware edge detector (UAED, CVPR 2023) reframed multi-annotator disagreement as learned uncertainty; MuGE (CVPR 2024) extended this to controllable multi-granularity outputs; SAUGE (AAAI 2025) adapted SAM for uncertainty-aligned multi-granularity prediction. The manuscript cites UAED and SAUGE but omits MuGE, which is the closest competitor to its central conceptual move, since both attempt to make the granularity or strength of a boundary decision explicit and controllable. More seriously, the ambiguity gate U(P) = [4P(1−P)]^γ is a fixed function of anchor probability, and the authors state it is not an uncertainty estimate. Against UAED and MuGE, which estimate ambiguity from data, a hand-specified parabola in probability space is a step backwards, and the manuscript does not argue otherwise. On crispness, Cetinkaya, Kalkan and Akbas's RankED (CVPR 2024) and MatchED (CVPR 2026) show that one-pixel-wide edges can be obtained through differentiable matching-based supervision with roughly 21,000 additional parameters, eliminating the non-differentiable NMS-and-thinning pipeline entirely. The submitted work depends on a source-frozen NMS setting throughout and cites MatchED only in passing; a direct comparison against a MatchED-augmented HED-lite anchor is the obvious missing experiment, since both are lightweight plug-in modules applied to an existing detector. Generative approaches now define the upper end of the BIPED and NYUDv2 leaderboards at roughly 0.892–0.896 and 0.800 ODS respectively, which is the baseline against which this manuscript's 0.9426 and 0.8425 must be justified.

On the retinal side the field has advanced well past what this manuscript demonstrates, and the omissions here are the more damaging. Huang, Rangel, Briggman and Wei (*Nat. Commun.* **10**, 2431, 2019), cited as reference 16, is the direct precedent: it established contextual modulation of direction-selective ganglion cells by moving-contour discontinuities and identified the responsible starburst and wide-field amacrine circuit motifs using synapse-specific genetic manipulation, patch-clamp recording and connectomics. That study answered, causally and at cell resolution, the question this manuscript approaches with three confounded block comparisons; the manuscript cites it as background rather than confronting it as the standard its own experiment must meet. Two further works should have been engaged and are absent. Karamanlis et al. (*Nature*, 2024) showed that nonlinear receptive-field pooling drives correlated, redundant ganglion-cell responses to natural scenes in both marmoset and mouse, which bears directly on whether averaging heterogeneous units within an n×n bin yields an interpretable population "context" signal. Riccitelli et al. (*PNAS*, 2025) demonstrated that non-direction-selective mouse ganglion cells exhibit asymmetric, direction-tuned responses to stimuli crossing regions far beyond the classical receptive field, mediated by glycinergic amacrine cells — an extraclassical mechanism that would produce the reported bidirectional differences without any of the surround structure the CME stimulus manipulates, and therefore a competing explanation the authors do not address. Within bio-inspired computer vision, the manuscript cites the Lin group's DPED, XYW and lightweight contour work (references 19 to 22) but omits COS-net (*Digital Signal Processing*, 2025) and Huang, Lin and Peng's bio-inspired lightweight edge network (*SIViP*, 2025), both of which implement surround-modulation operators on overlapping benchmarks and would provide the like-for-like comparison the PiDiNet contrast — which the authors concede cannot isolate an RBCM effect — does not.

## 7. Suggested Reviewer Names

**Edge-detection benchmarking and evaluation protocol.** *Emre Akbaş*, Associate Professor, Middle East Technical University — senior author of MatchED (CVPR 2026), which introduces an evaluation-aware matching formulation and is directly comparable to the present operator as a lightweight plug-in module. *Bedrettin Çetinkaya*, doctoral researcher, METU — first author of both RankED (CVPR 2024) and MatchED (CVPR 2026), the most directly comparable published work on modifying edge-detector outputs without retraining the backbone. *Xavier Soria Poma*, Universidad Nacional de Chimborazo — creator of BIPED, DexiNed, TEED and UDED, that is three of the five datasets used here, and therefore the best-placed reviewer to judge whether the reported BIPED ODS is attainable under the standard protocol.

**Crisp and uncertainty-aware edge architectures.** *Mengyang Pu*, Associate Professor, North China Electric Power University — first author of EDTER (CVPR 2022) and MuGE (CVPR 2024); MuGE is the closest published competitor to the manuscript's controllable-adjustment framing. *Caixia Zhou*, postdoctoral researcher, Beijing Jiaotong University — first author of UAED (CVPR 2023), the reference point against which the deterministic ambiguity gate must be assessed. *Zhuo Su*, postdoctoral researcher, University of Oulu — first author of PiDiNet (ICCV 2021), the manuscript's external comparator in Fig. 4f, and best placed to judge whether that comparison is fair. *Yunfan Ye*, Hunan University — first author of DiffusionEdge (AAAI 2024), for the generative-refinement comparison the manuscript omits.

**Retinal MEA electrophysiology and population coding.** *Dimokratis Karamanlis*, postdoctoral researcher, Göttingen — first author of the 2024 *Nature* study on nonlinear receptive fields and redundant retinal coding of natural scenes, using large-scale mouse and marmoset MEA recordings; directly qualified to judge spatial-bin pooling of heterogeneous units. *Xiaolin Huang* — first author of *Nat. Commun.* **10**, 2431 (2019) on contextual modulation in the retinal direction-selective circuit, the manuscript's own reference 16 and the causal study this work does not match. *Serena Riccitelli*, postdoctoral researcher, Weizmann Institute (Rivlin-Etzion laboratory) — first author of the 2025 *PNAS* study on extraclassical direction-tuned ganglion-cell responses, which supplies the competing explanation for the reported bidirectional differences.

**Permutation inference and nested pseudoreplication.** *Philipp Berens*, Professor, University of Tübingen — proposed as a last-resort senior reviewer given the scarcity of researchers combining retinal population statistics with machine-learning evaluation; a group member working on retinal functional classification would be an acceptable junior substitute. The specific charge is whether within-bin unit-label permutation is a valid null when block composition differs, and whether Benjamini–Hochberg correction across 168 re-analyses of three animals is interpretable.

---

## Further Literature (Past 3 Years, Annotated)

**1.** Cetinkaya, B., Kalkan, S. & Akbas, E. MatchED: Crisp Edge Detection Using End-to-End, Matching-based Supervision. *Proc. IEEE/CVF Conf. Comput. Vis. Pattern Recognit.* 42093–42103 (2026).
*Peer-reviewed (CVPR main track). Cited by the manuscript as reference 10. Authors independent of the submitting group.* A 21,000-parameter plug-in module achieving crisp edges without NMS or thinning. The correct head-to-head comparator for a lightweight post-hoc operator appended to a fixed anchor; its existence makes the manuscript's dependence on a source-frozen NMS setting harder to defend. Cited only as background.

**2.** Cheng, J., Wu, Y. & Zhou, Y. MEMO: Human-like Crisp Edge Detection Using Masked Edge Prediction. *Proc. IEEE/CVF Conf. Comput. Vis. Pattern Recognit.* 27740–27749 (2026).
*Peer-reviewed (CVPR main track). Cited as reference 9. Authors independent.* Addresses boundary thickness and train–evaluation alignment. Directly relevant to the manuscript's crispness analysis in Supplementary Fig. 5, which is benchmarked against no crisp-edge method.

**3.** Cetinkaya, B., Kalkan, S. & Akbas, E. RankED: Addressing Imbalance and Uncertainty in Edge Detection Using Ranking-based Losses. *Proc. IEEE/CVF Conf. Comput. Vis. Pattern Recognit.* 3239–3249 (2024).
*Peer-reviewed (CVPR). Not cited. Authors independent.* Ranking-based losses that target precisely the AP and confidence-ordering degradation the manuscript reports and does not remedy (−0.92 on MultiCue, −4.24 on MultiCue-to-BSDS500). A serious omission given that AP loss is the manuscript's central acknowledged failure mode.

**4.** Zhou, C., Huang, Y., Pu, M., Guan, Q., Deng, R. & Ling, H. MuGE: Multiple Granularity Edge Detection. *Proc. IEEE/CVF Conf. Comput. Vis. Pattern Recognit.* (2024).
*Peer-reviewed (CVPR). Not cited. Authors independent.* Controllable multi-granularity edge prediction, conceptually the closest competitor to "signed contextual adjustment," since both make the strength or scale of the boundary decision explicit and tunable. Its absence from the introduction materially weakens the novelty claim.

**5.** Zhou, C. et al. The Treasure Beneath Multiple Annotations: An Uncertainty-aware Edge Detector. *Proc. IEEE/CVF Conf. Comput. Vis. Pattern Recognit.* 15507–15517 (2023).
*Peer-reviewed (CVPR). Cited as reference 6. Authors independent.* The benchmark for data-driven ambiguity estimation. The fixed gate U(P) = [4P(1−P)]^γ should be compared against a learned uncertainty estimate on identical anchors; no such ablation is reported.

**6.** Liufu, X. et al. SAUGE: Taming SAM for Uncertainty-Aligned Multi-Granularity Edge Detection. *Proc. AAAI Conf. Artif. Intell.* **39**, 5766–5774 (2025).
*Peer-reviewed (AAAI). Cited as reference 7. Authors independent.* Foundation-model-based uncertainty-aligned edge detection, establishing the current ceiling for ambiguity-aware methods and the scale at which the field now operates.

**7.** Ye, Y., Xu, K., Huang, Y., Yi, R. & Cai, Z. DiffusionEdge: Diffusion Probabilistic Model for Crisp Edge Detection. *Proc. AAAI Conf. Artif. Intell.* **38**, 6675–6683 (2024).
*Peer-reviewed (AAAI). Cited as reference 8. Authors independent.* Generative refinement defining the upper end of BIPED performance in the published literature. The manuscript's reported 0.9426 requires explicit reconciliation against this line of work under a common evaluator.

**8.** Karamanlis, D. et al. Nonlinear receptive fields evoke redundant retinal coding of natural scenes. *Nature* (2024). doi:10.1038/s41586-024-08212-3
*Peer-reviewed. Not cited. Authors independent.* Large-scale MEA recordings in marmoset and mouse showing that nonlinear pooling of ganglion-cell inputs produces correlated, redundant responses under natural gaze dynamics. Directly undermines the assumption that averaging heterogeneous units within an n×n spatial bin yields an interpretable local population signal.

**9.** Riccitelli, S. et al. Retinal ganglion cells encode the direction of motion of stimuli far beyond their receptive field. *Proc. Natl Acad. Sci. USA* (2025).
*Peer-reviewed. Not cited. Authors independent. DOI not independently confirmed during preparation of this report; editorial office should verify.* Demonstrates glycinergic-amacrine-mediated extraclassical direction-tuned responses in non-direction-selective mouse ganglion cells. Supplies a competing mechanistic account of the reported UME/CME differences that does not require the manipulated surround structure.

**10.** Huang, K., Lin, C. & Peng, J. Bio-inspired visual mechanism lightweight network for edge detection. *Signal Image Video Process.* **19**, 450 (2025). doi:10.1007/s11760-025-04050-6
*Peer-reviewed. Not cited. Same research lineage as the manuscript's references 19–22 but no co-authorship overlap with the submitting group.* A recent surround-modulation lightweight edge network on overlapping benchmarks. Together with COS-net (*Digital Signal Processing* **159**, 104994, 2025; doi:10.1016/j.dsp.2025.104994) it provides the like-for-like bio-inspired comparison the manuscript lacks.

*Note on peer-review status: all ten entries are peer-reviewed journal or main-track conference publications. No arXiv-only preprints are included. Where arXiv versions exist (entries 1, 3, 4), the peer-reviewed proceedings version is cited.*

068766
# Editorial Report — Manuscript 068766

**Title:** GaitEncoder: A Foundation Model of Gait Kinematics for Diverse Clinical Applications and Pathologies
**Authors:** R. D. Magruder, S. Gilon, A. Falisse, S. D. Uhlrich (University of Utah; Model Health Inc.)
**Venue considered:** *Nature Communications* — Digital Health

---

## Editorial Integrity Alert — Confidential, Handling Editor Only

**1. Undisclosed preprint.** A version of this manuscript is publicly posted on medRxiv (posted 7 July 2026, DOI 10.64898/2026.07.07.26357479), under the identical title and abstract. The submitted manuscript contains no preprint declaration. This is not disqualifying under Nature Communications policy but must be recorded, and the authors should be asked to confirm the version relationship and any differences.

**2. Undisclosed self-benchmarking.** The manuscript's principal comparator throughout Section 2.1 and the Discussion — reference 17, "clinician-informed hand-engineered features" (Ruth et al., *NEJM AI* 2025) — is co-authored by Scott D. Uhlrich and Antoine Falisse, two of the four authors of this submission. The text consistently frames this comparison as though it were against an external clinical standard ("models using clinician-informed, hand-engineered features"). The authors should be required to state this relationship explicitly in the main text.

**3. Cohort reuse across publications.** The myotonic dystrophy (n=55) and FSHD (n=26) cohorts used for the headline "unseen pathology" evaluation are drawn from the same Stanford collection reported in Ruth et al. 2025 (58 DM, 28 FSHD). Both the evaluation data and the comparator method therefore originate from the authors' own prior study. This is not fraud, but it materially weakens the claim of independent out-of-distribution validation and should be disclosed. There is a genuine salami-slicing question the authors should answer directly: what is the incremental unit of new data here?

**4. Selective reporting in the Discussion.** The Results report that hand-engineered features using nine activities achieved 0.75 accuracy for myotonic dystrophy and 0.67 for FSHD — comparable to, and in one case not statistically distinguishable from, the fine-tuned GaitEncoder (0.81 and 0.75; FSHD comparison p=0.066). The Discussion then states that hand-engineered features "did not accurately differentiate myotonic dystrophy or FSHD from controls (44–53% accuracy)," citing only the walking-only baseline and omitting the nine-activity results entirely. This is a material misrepresentation of the authors' own data and must be corrected regardless of the decision.

**5. Citation status error.** Reference 28 (Cotton et al., Self-Supervised Learning of Gait-Based Biomarkers) is cited as an arXiv preprint; it was published in the peer-reviewed MICCAI PRIME 2023 proceedings (DOI 10.1007/978-3-031-46005-0_24). Reference 16 (Gilon, Miller & Uhlrich, OpenCap Monocular) is a self-cited arXiv preprint used to support a claim about clinical measurement feasibility.

**6. Commercial entanglement in the evaluation path.** Competing interests are declared (SDU and AF are co-founders of Model Health Inc.), but the declaration understates the entanglement: the kinematics for the sole longitudinal clinical demonstration (Section 2.3) were computed using the Model Health commercial platform rather than open-source OpenCap, and the DMU score is deployed on the authors' own platform. This should be surfaced to reviewers.

**7. Ethics coverage.** IRB approval and informed consent are stated only for the single post-stroke participant. No ethics statement covers the eight aggregated datasets or the secondary use of the DM/FSHD cohorts. A blanket statement is required.

**8. Numerical consistency.** Table 1 participant counts sum correctly to 657 once the 91 post-arthroplasty returners are recognised as a subset of the 105 hip osteoarthritis participants. Training (381), validation (155) and testing (121) sum to 657. No arithmetic errors detected. The cerebral palsy cohort is n=6 (4 in training), which is not adequately signposted against the abstract's claim of "seven unique pathologies."

---

## 1. Overall Assessment

A weakly-supervised VAE compresses 32 joints × 24 time points into 16 latent dimensions, trained on 381 individuals across four pathologies, and is claimed to transfer to four downstream tasks and three withheld conditions. The problem is well posed and the data aggregation is useful, but the foundation-model framing is not earned at this scale, and every downstream claim thins precisely where it becomes clinical.

## 2. Strengths

Eight heterogeneous sources harmonised around a single Rajagopal model, ages 8–86, seven conditions, released on SimTK — infrastructure that does not currently exist.

Serious out-of-distribution design: Parkinson's, myotonic dystrophy and FSHD withheld entirely, reconstruction MAE quantified per condition (4.8°, 4.3°, 5.1° vs 3.5°), tested across marker-based and video modalities.

Excluding diagnostic labels from the loss and supervising on gait speed keeps the latent space usable for unseen conditions.

The surgical effect predictor is the strongest result: frozen encoder/decoder, correct average-treatment-effect baseline (4.7±1.0° vs 5.9±2.5°, p=.004, d=.60), modest 1.2° gain honestly reported.

## 3. Weaknesses

DMU is confounded by construction — normed on ages 18–65 with speed ≥1.2 m/s while gait speed is the supervision target, then applied to cohorts aged 44–86. Never age-adjusted, never tested against speed alone.

Zero-shot and fine-tuned results conflict. True zero-shot accuracies (0.68, 0.62) fall below the nine-activity baselines (0.75, 0.67). FSHD DMU separation is non-significant zero-shot (p=.267), significant only after fine-tuning on that cohort and testing on it — circular.

Statistics are permissive: one-sided t-tests, correction only in §2.2, no confidence intervals or calibration anywhere, n=13 controls, and no demographic subgroup analysis of any kind.

Section 2.3 is n=1 with no testing — less evidence than Felius et al. 2024, cited in its own reference list on the same question.

No modern learned baseline. GaitDynamics, self-supervised embeddings and plain PCA are all absent; the only comparator is a 2008 linear decomposition.

## 4. Editorial Decision

**Send for Review, after two mandatory pre-review corrections.** These flaws are largely revisable and turn on an open question reviewers are better placed to settle: whether pathology-diverse pretraining beats healthy-only pretraining at greater scale. But integrity items 2 and 4 must be fixed first. The authors must disclose that reference 17 is their own prior work, and correct the Discussion's 44–53% baseline claim to the 67–75% their Results report. Reviewers cannot fairly judge a comparison misrepresented as external against a baseline understated by twenty points. Reviewers should then adjudicate: does DMU survive age adjustment and beat gait speed alone; is the fine-tuned separation test circular; does a 16-dimensional MLP autoencoder at n=381 warrant "foundation model" given GaitDynamics and AddBiomechanics; can §2.3 support any claim at n=1.

**Steelman (the case for rejection).** The DMU confound is a design decision baked into the normative cohort, not an analysis error, and no revision short of reweighting that cohort repairs it. The circular separation test cannot be fixed by further experiment — it must be withdrawn. Two of four downstream tasks therefore cannot survive review intact, and a paper whose headline claims require deletion rather than strengthening has not yet been done. Adding the missing subgroup analyses, intervals and baselines approaches a new study. Transfer to *Communications Medicine* would return a decision in weeks instead of consuming two reviewers for a probable reject-after-review. The counterweight is that the dataset and the surgical predictor are real contributions, and the scale-versus-diversity question deserves expert adjudication rather than an editor's guess.

## 5. Suggested Reviewer Expertise

Reviewers should collectively cover five areas. First, generative and self-supervised representation learning for human movement time series — specifically variational autoencoders, diffusion models and transformer architectures applied to joint-angle trajectories, with the ability to judge whether a 16-dimensional bottleneck trained on n=381 warrants the foundation-model designation. Second, markerless and smartphone-based motion capture validation, including OpenCap, AddBiomechanics, Theia3D and the propagation of pose-estimation error into inverse-kinematic joint angles across capture modalities. Third, biostatistics for clinical prediction models: cross-validation design under severe class imbalance, calibration and confidence-interval reporting, multiplicity correction, and the distinction between within-distribution and held-out evaluation. Fourth, clinical outcome measurement in neuromuscular disease, particularly myotonic dystrophy type 1 and FSHD, including the psychometric requirements (reliability, minimal detectable change, responsiveness) that a candidate digital endpoint must meet for trial use. Fifth, movement disorders and rehabilitation medicine, covering UPDRS-II/III construct validity, subacute post-stroke recovery trajectories and compensation versus true recovery, and hip osteoarthritis surgical outcome prediction.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant field has moved decisively toward large, harmonised, multi-study biomechanics corpora and generative models trained on them. The AddBiomechanics dataset (Werling et al., ECCV 2024) harmonised fifteen studies into more than 70 hours of physics-consistent motion, and GaitDynamics (Tan et al., *Nature Biomedical Engineering* 2026) trained a diffusion transformer on it, demonstrating flexible-input inference, inpainting under missing kinematics, and — critically for the present manuscript — generalisation to osteoarthritis despite training exclusively on healthy participants. In parallel, movement-language models have emerged: BiomechGPT (Yang, Abilitylab, Kennedy & Cotton, arXiv 2025) tokenises biomechanical motion for a multimodal foundation model over clinically relevant tasks, building on Cotton's earlier self-supervised gait biomarkers (MICCAI PRIME 2023). On the measurement side, OpenCap (Uhlrich et al., *PLOS Computational Biology* 2023) established smartphone-video musculoskeletal analysis, Stenum et al. (*PLOS Digital Health* 2024) surveyed the clinical validity of video pose estimation for gait, and Ruth et al. (*NEJM AI* 2025) showed that clinician-informed video features discriminate neuromuscular diseases across nine activities. For latent gait representations specifically, Felius et al. (*PLOS ONE* 2024) established the psychometric template — reliability, group discrimination, responsiveness — that this literature now expects.

Against that landscape, this manuscript advances on exactly one axis: pathological diversity in the training distribution. Every prior gait foundation model was trained overwhelmingly on unimpaired movement, and the question of whether pathology-diverse pretraining improves transfer to unseen conditions is genuinely open and worth answering. But the paper does not answer it, because it never compares against a model pretrained on the larger healthy corpus. Where it replicates rather than advances: latent-space reduction of pathological gait with weak clinical supervision is essentially the Felius design at larger scale, and impairment scoring against a normative embedding is the Gait Deviation Index with a nonlinear encoder. The authors should be required to engage substantively with GaitDynamics and AddBiomechanics as pretraining alternatives rather than as background citations, to benchmark against BiomechGPT-style tokenised representations, and to explain why nine-activity assessment — which their own comparator shows outperforms walking-only analysis for FSHD — was excluded from a model whose stated limitation is that it sees only walking.

## 7. Suggested Reviewer Names

*Ranks and current affiliations should be verified by the editorial office before invitation; conflict notes are flagged where I identified them.*

**Representation learning for gait kinematics.** R. James Cotton (Assistant Professor, Northwestern University / Shirley Ryan AbilityLab) — directly comparable work in *Self-Supervised Learning of Gait-Based Biomarkers* (MICCAI PRIME 2023) and *BiomechGPT* (2025); best-placed reviewer for the foundation-model claim. **Conflict note:** he has co-authored markerless motion capture methods papers with S. Uhlrich (2023 EMBC/ICORR), which the editorial office should weigh. Robert Felius (Vrije Universiteit Amsterdam) — first author of *Exploring unsupervised feature extraction of IMU-based gait data in stroke rehabilitation using a variational autoencoder* (*PLOS ONE* 2024), the single closest published analogue to this submission's latent-representation and responsiveness claims, and independent of both Utah and Stanford. Sina David (Assistant Professor, Vrije Universiteit Amsterdam) — senior author on convolutional VAE latent gait representations across IMU, markerless and optical capture modalities (2026), directly comparable on the cross-modality generalisation claim.

**Generative gait modelling and benchmarking.** Tian Tan (Stanford University) — first author of *GaitDynamics* (*Nature Biomedical Engineering* 2026), the direct competitor model. **Conflict note:** Stanford Neuromuscular Biomechanics Lab, S. D. Uhlrich's former group; likely excluded, but named because his review would be the most substantive available on the scale-versus-diversity question. Eni Halilaj (Associate Professor, Carnegie Mellon University) — machine learning for musculoskeletal movement analysis and video-based knee loading estimation; independent of the Utah and Stanford groups.

**Clinical outcome measurement — neuromuscular disease.** Karlien Mul (neurologist, Radboud University Medical Center) — FSHD clinical outcome measures including the FSHD-COM; the right reviewer to judge whether DMU meets the psychometric bar for a trial endpoint. **Exclusion note:** Tina Duong and Parker Ruth (Stanford) are the natural clinical experts for the DM/FSHD cohorts but are co-authors of reference 17 and should not be invited.

**Clinical outcome measurement — movement disorders and rehabilitation.** Martina Mancini (Associate Professor, Oregon Health & Science University) — instrumented gait and mobility assessment in Parkinson's disease; appropriate for the UPDRS-II/III construct validity claims in Section 2.2 and for judging whether r=.63–.65 constitutes clinically useful agreement.

---


---

## Further Literature (Past 3 Years, Similar Scope)

Ten papers sharing this manuscript's scope: learned representations of gait kinematics, video-based clinical gait analysis, and digital gait outcome measures in movement-disordered populations. Peer-reviewed work is prioritised; preprints are flagged explicitly.

**1.** Tan, T., Van Wouwe, T., Werling, K. F., Liu, C. K., Delp, S. L., Hicks, J. L. & Chaudhari, A. S. *GaitDynamics: a generative foundation model for analyzing human walking and running.* Nature Biomedical Engineering 10, 1659–1671 (2026). DOI: 10.1038/s41551-025-01565-8.
**Peer-reviewed. Cited (ref 29). Independent** — Uhlrich is not an author, though the Stanford NMBL lineage overlaps.
*Relevance:* the direct competitor. A diffusion transformer on 10,352 trials from 178 AddBiomechanics participants, with flexible inputs, inpainting under missing kinematics, and — decisively for this submission — generalisation to osteoarthritis from healthy-only training. The submission dismisses it in one clause. Reviewers should require a head-to-head against a GaitDynamics-derived representation, since it directly tests whether pathological diversity or raw scale drives transfer.

**2.** Werling, K. et al. *AddBiomechanics Dataset: Capturing the Physics of Human Motion at Scale.* Computer Vision – ECCV 2024, LNCS 15146, 490–508 (2025). DOI: 10.1007/978-3-031-73223-2_27.
**Peer-reviewed (conference). NOT cited** — the manuscript cites the AddBiomechanics *tool* (ref 51) but not the dataset. **Independent.**
*Relevance:* the pretraining corpus the authors did not use. They ran their marker data through the AddBiomechanics pipeline yet ignored the 70-hour, 270-participant harmonised corpus attached to it. The obvious ablation — pretrain here, fine-tune on pathology — is missing and must be requested.

**3.** Ruth, P. S., Uhlrich, S. D., de Monts, C., Falisse, A., Muccini, J., Covitz, S., Vogt-Domke, S., Day, J., Duong, T. & Delp, S. L. *Video-Based Biomechanical Analysis Captures Disease-Specific Movement Signatures of Different Neuromuscular Diseases.* NEJM AI 2(9) (2025). DOI: 10.1056/AIoa2401137.
**Peer-reviewed. Cited (ref 17). NOT independent** — Uhlrich and Falisse co-author both papers.
*Relevance:* supplies both the comparator features and the DM/FSHD evaluation cohorts. Its nine-activity results (0.75 DM, 0.67 FSHD) are the honest baseline omitted from the Discussion. Also establishes that multi-activity assessment outperforms walking-only for FSHD — which undercuts the submission's walking-only design more than its stated limitation admits.

**4.** Felius, R. A. W. et al. *Exploring unsupervised feature extraction of IMU-based gait data in stroke rehabilitation using a variational autoencoder.* PLoS ONE 19, e0304558 (2024). DOI: 10.1371/journal.pone.0304558.
**Peer-reviewed. Cited (ref 33). Independent.**
*Relevance:* the closest published analogue — a VAE reducing post-stroke gait to twelve latent features, evaluated with test–retest ICC, group discrimination and responsiveness during rehabilitation in a proper cohort. Sets the psychometric bar that Section 2.3 fails at n=1. The submission cites it as background rather than as the comparator it plainly is.

**5.** Uhlrich, S. D., Falisse, A., Kidziński, Ł., Muccini, J., Ko, M., Chaudhari, A. S., Hicks, J. L. & Delp, S. L. *OpenCap: Human movement dynamics from smartphone videos.* PLOS Computational Biology 19, e1011462 (2023). DOI: 10.1371/journal.pcbi.1011462.
**Peer-reviewed. Cited (ref 18). NOT independent** — Uhlrich and Falisse co-author both.
*Relevance:* the measurement substrate for all video-derived cohorts and the deployment platform for DMU. Reviewers should check whether OpenCap's own joint-angle error is small relative to the 3.5–5.1° reconstruction MAE reported here; if it is not, the reconstruction metric is partly measuring the capture pipeline rather than the model.

**6.** Cotton, R. J. et al. *Self-Supervised Learning of Gait-Based Biomarkers.* Predictive Intelligence in Medicine (MICCAI PRIME 2023), LNCS, 277–291. DOI: 10.1007/978-3-031-46005-0_24.
**Peer-reviewed — miscited by the manuscript as an arXiv preprint (ref 28). Cited, incorrectly. Independent.**
*Relevance:* prior self-supervised gait representation learning with clinical evaluation, and the nearest precedent for the submission's core method. Should function as a benchmark, not a background citation. The miscitation matters because it understates how much of this territory is already peer-reviewed.

**7.** Yang, R., Abilitylab, S. R., Kennedy, A. & Cotton, R. J. *BiomechGPT: Towards a Biomechanically Fluent Multimodal Foundation Model for Clinically Relevant Motion Tasks.* arXiv:2505.18465 (2025).
**arXiv only — NOT peer reviewed; flagged as unreviewed evidence. Cited (ref 35). Independent.**
*Relevance:* the tokenised-movement route to gait foundation models, and the most direct challenge to the submission's architectural choice. Useful for situating the work, but its preprint status means it cannot settle priority or serve as a validated comparator.

**8.** *Deep learning-enabled accurate assessment of gait impairments in Parkinson's disease using smartphone videos.* npj Digital Medicine 8 (2025). DOI: 10.1038/s41746-025-02150-8.
**Peer-reviewed. NOT cited. Independent.**
*Relevance:* directly parallel to Section 2.2 and a serious omission. Reports micro-average AUC 0.87 and F1 0.806 for PD severity from smartphone video, comparable to three clinical specialists, and discriminates medication effects at a resolution finer than UPDRS. The submission's r=.63–.65 UPDRS correlations must be positioned against this, not against the absence of prior work.

**9.** *3D pose estimation for scalable remote gait kinematics assessment.* npj Digital Medicine 8 (2025). DOI: 10.1038/s41746-025-02211-y.
**Peer-reviewed. NOT cited. Independent.**
*Relevance:* establishes markerless pose estimation for pathological gait analysis outside the clinic, identifying reduced hip and knee flexion as biomarkers. Overlaps the submission's remote-monitoring premise and its joint-level interpretability claim in Figure 5d, and should be engaged with when arguing that DMU's joint attribution is novel.

**10.** Stenum, J., Hsu, M. M., Pantelyat, A. Y. & Roemmich, R. T. *Clinical gait analysis using video-based pose estimation: Multiple perspectives, clinical populations, and measuring change.* PLOS Digital Health 3, e0000467 (2024). DOI: 10.1371/journal.pdig.0000467.
**Peer-reviewed. Cited (ref 13). Independent.**
*Relevance:* addresses head-on whether video-derived kinematics can detect longitudinal change in clinical populations — the exact claim of Section 2.3. Provides the measurement-error framework against which a single patient's 16-week DMU trajectory should be judged, and the reason an n=1 demonstration cannot carry that claim.
