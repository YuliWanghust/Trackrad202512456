# Trackrad202512456

072871
## Editorial Report — "PyHEARTS: Beat-by-beat ECG waveform morphology mapping for interpretable machine learning and AI"

### 1. Overall Assessment

PyHEARTS fits each ECG cycle to a sum of Gaussians over P, Q, R, S, T, yielding 135 interpretable per-beat features, validated across four cohorts (~2.85M beats, 30,686 participants) plus cardiologist-annotated LUDB, and tested downstream via chronological-age prediction (MAE 8.93 yr) and murine transfer. The contribution is validation scale, not modeling novelty: the Gaussian-beat parametrization mirrors the McSharry–Clifford ECGSYN model and later Gaussian-fitting literature, uncited here. Two issues dominate: an internal T-wave sensitivity discrepancy, and an age-prediction result that underperforms its own cited deep-learning benchmarks.

### 2. Strengths

The multi-cohort validation is rigorous: participant-grouped cross-validation avoids leakage, and cross-cohort reliability concordance (ICC Spearman ρ = 0.875, SPH vs. PTB-XL) is genuine, not single-dataset. The morphology-versus-timing reliability dissociation is a useful, non-obvious finding for ECG-ML pipeline design across devices. Explicit missing-data handling and transparent conditional/unconditional sensitivity reporting reflect good methodological hygiene.

### 3. Weaknesses

The core novelty claim is unsupported: McSharry et al. (2003) already introduced Gaussian PQRST beat modeling, and ECGdeli/NeuroKit2 (both cited) already do overlapping delineation-plus-morphology extraction; none of this lineage is engaged. Table 2 and the Results text/Figure 2 caption give contradictory T-wave sensitivity values (75.0%/84.7%, n=1,390 vs. 61.9%/72.5%, n=1,238) that must be reconciled. The age-prediction result (MAE 8.93 yr, single lead, OOF-only) is framed as "competitive" but underperforms the strongest cited benchmarks (5.8–8.06 yr), and no clinical outcome is demonstrated.

### 4. Editorial Decision

**Reject.** As a steelman, this could be read as infrastructure/validation work in the tradition of dataset papers — but Nature Communications requires a clinical or mechanistic advance beyond tool description, and the one downstream analysis offered underperforms its own comparators while the core method is not new. Combined with the unresolved Table 2 inconsistency, it should not proceed to review.

### 5. Suggested Reviewer Expertise

Nonlinear parametric waveform/curve-fitting for biomedical signals (Gaussian mixture and dynamical ECG models); classical ECG delineation algorithm validation under ANSI/AAMI EC57 methodology; interpretable tabular machine learning (gradient-boosted trees, permutation importance, calibration) for physiological biomarkers; clinical electrophysiology of aging, repolarization (QT/ST), and autonomic function; comparative/translational cardiovascular physiology including murine electrocardiography.

### 6. State-of-the-Art Literature Review (Past 3 Years)

The field has split into two active tracks. End-to-end deep representations continue (AI-ECG heart-age-as-mortality-predictor studies through 2025, echocardiography-derived age in npj Digital Medicine 2025), while a parallel resurgence of interpretable tabular/morphology feature systems has emerged specifically to counter black-box ECG-AI: a 2026 harmonized cross-dataset interpretable feature framework (arXiv:2607.23412, preliminary version at CBMS 2026) pursuing near-identical goals to PyHEARTS on MIMIC-IV and an Alberta cohort; motif-based interpretable morphology signatures (arXiv:2606.00107, 2026); and ECGXtract (arXiv:2511.02850, 2025), which explicitly benchmarks against ECGdeli. PyHEARTS adds beat-level generative reconstruction and cross-species transfer that these lack, but engages none of them, nor the foundational Gaussian-beat modeling line (McSharry 2003) all of this work ultimately descends from.

### 7. Suggested Reviewers

**Nicolas Pilia** (KIT, Karlsruhe) — author of ECGdeli, already cited by the manuscript; directly comparable delineation-validation methodology.
**Dominique Makowski** (Nanyang Technological University) — author of NeuroKit2, already cited; directly comparable open-source physiological-signal toolbox.
For tabular-ML-interpretability and clinical-aging expertise, and for murine comparative electrophysiology, I could not independently verify a junior (postdoc/assistant-professor-level) candidate with a directly comparable publication who is clearly independent of the manuscript's own data sources — flagging this per standing policy rather than defaulting to senior faculty. I'd suggest the editor solicit via the corresponding authors of arXiv:2607.23412 and arXiv:2606.00107 once their seniority can be confirmed.

---

## Editorial Integrity Alert (confidential, handling editor only)

**Numerical inconsistency (primary concern).** T-wave sensitivity is reported inconsistently within the manuscript: Table 2 gives Se±40ms = 75.0%, Se±150ms = 84.7% (matched n = 1,390 of 1,642), while the Results text (lines 127–131) and Figure 2 caption give 61.9%/72.5%, and the mechanistic explanation two paragraphs later (lines 132–135) uses a different detected-peak count (n = 1,238). R and P rows are internally consistent across all locations; only T diverges. This needs author clarification and correction — it is not resolvable by re-reading, since text and Table 2 cannot both be right.

**Reproducibility.** The Data Availability GitHub link (github.com/PyHEARTS-toolbox/pyhearts) could not be confirmed as a live, populated public repository via independent search at the time of this review. This may simply reflect search-indexing lag rather than an actual problem, but should be verified before acceptance.

**Author/dataset overlap.** The murine ECG data are drawn from a previously published study (ref. 67, Lovelace et al., *Nature* 2023); co-author V. Augustine's contribution statement ("provided mouse data and murine cardiac expertise") suggests direct involvement with that source dataset. This is disclosed, not concealed, but it means the "cross-species generalization" claim is validated on an internally-sourced rather than fully independent murine cohort — worth noting when weighing that claim's strength.

**No other concerns identified.** No undisclosed preprint, no salami-slicing indicators, and the self-citation to Cole & Voytek (bycycle, ref. 39) is appropriately disclosed as conceptual motivation rather than concealed reuse.

---

## Further Literature — 10 papers of similar scope (past 3 years)

1. **Lin, J. et al. "Harmonized Interpretable ECG Waveform Features for Robust Cross-Dataset Clinical Prediction."** arXiv:2607.23412 (2026); preliminary 2-page version accepted at IEEE CBMS 2026 (peer-reviewed conference), full version arXiv-only (**unreviewed**). Not cited by manuscript. Authors independent of submitting group. Most directly competing concurrent work: builds a harmonized interpretable morphology + HRV + time-frequency feature set ("FeatureDB") across MIMIC-IV and an Alberta cohort for cross-site clinical prediction — nearly identical motivation to PyHEARTS but validated against clinical outcomes (heart failure, mortality) rather than only age, which PyHEARTS lacks.

2. **"Motif-based morphology signatures for interpretable ECG screening and monitoring."** arXiv:2606.00107 (2026). **Unreviewed** (arXiv only). Not cited. Independent authorship. Uses dynamic-time-warping motif/discord extraction on PTB-XL as an alternative interpretable-morphology representation to parametric Gaussian fitting — a direct conceptual competitor PyHEARTS should differentiate itself from.

3. **"ECGXtract: Deep Learning-based ECG Feature Extraction for Automated CVD Diagnosis."** arXiv:2511.02850 (2025). **Unreviewed** (arXiv only). Not cited. Independent authorship. Explicitly benchmarks against ECGdeli (already cited by the manuscript as ref. 25), which PyHEARTS itself never benchmarks against numerically — a gap this paper highlights by contrast.

4. **"Fusion of automatically learned rhythm and morphology features matches diagnostic criteria and enhances AI explainability" (xFuseMap).** *npj Artificial Intelligence* (2025), DOI 10.1038/s44387-025-00022-w (inferred from article URL; verify before use). **Peer-reviewed.** Not cited. Independent authorship. Combines learned rhythm and morphology streams with explicit color-coded attribution — relevant comparator for PyHEARTS' morphology/timing family separation.

5. **"Bridging clinical knowledge and AI: an interpretable transformer framework for ECG diagnosis."** *npj Digital Medicine* (2025/2026), DOI 10.1038/s41746-025-02215-8 (inferred from URL; verify). **Peer-reviewed.** Not cited. Independent authorship. Interpretable-by-design deep model as an alternative route to the same transparency goal PyHEARTS pursues via explicit parametrization.

6. **Silva, R., Fred, A. & da Silva, H.P. "Morphological Autoencoders for Beat-by-Beat Atrial Fibrillation Detection Using Single-Lead ECG."** *Sensors* 23, 2854 (2023), DOI 10.3390/s23052854. **Peer-reviewed.** Not cited. Independent authorship (Instituto Superior Técnico, Lisbon). Learns beat-level morphological features via sparse autoencoder rather than parametric fitting — directly relevant alternative to PyHEARTS' hand-specified Gaussian features, with a clinical (AFib) endpoint PyHEARTS lacks.

7. **Mohammadi, S. "Pyheartlib: A Python package for processing electrocardiogram signals."** *J. Open Source Software* 9(95), 5792 (2024), DOI 10.21105/joss.05792. **Peer-reviewed** (JOSS). Not cited. Independent authorship. A directly comparable open-source Python ECG-processing package (beat detection/classification) with a confusingly similar name — the authors should distinguish PyHEARTS from it explicitly and consider the naming collision.

8. **"AI-ECG-derived biological age as a predictor of mortality in cardiovascular and acute care patients."** *European Heart Journal – Digital Health* 6(6) (2025). DOI not confirmed in available search results — verify before citing. **Peer-reviewed.** Not cited. Independent authorship (Innsbruck). Directly relevant age-as-biomarker comparator with mortality outcome validation, which PyHEARTS' age analysis does not attempt.

9. **Rawlani, M., Ieki, H., Binder, C. et al. "Artificial intelligence prediction of age from echocardiography as a marker for cardiovascular disease."** *npj Digital Medicine* 8, 688 (2025), DOI 10.1038/s41746-025-02050-x. **Peer-reviewed.** Not cited. Independent authorship. Different modality (echo, not ECG) but same "predicted-age-as-biomarker" logic and MAE benchmarking approach — useful for calibrating whether PyHEARTS' 8.93-year MAE is actually competitive across modalities, not just within ECG-DL.

10. **An iterative warping and clustering algorithm to estimate multiple wave-shape functions from a nonstationary oscillatory signal** (Wu and colleagues' wave-shape-function line). arXiv:2208.06500, revised March 2023. **Unreviewed** (arXiv only; related published work by this group appears in *Applied and Computational Harmonic Analysis*, not independently confirmed here). Not cited. Independent authorship. This is the closest theoretical precedent PyHEARTS fails to engage: a mathematically rigorous non-sinusoidal wave-shape-function framework explicitly applied to ECG, predating and conceptually overlapping the "beat-to-beat morphology parametrization" framing PyHEARTS presents as novel.

072877
## Editorial Report (Condensed): "Live deployment of a clinician-supervised generative AI agent in inpatient admission workflows" (GraphCare-Agent)

### 1–4. Assessment, Strengths, Weaknesses, Decision (≈300 words)

This is a live, clinician-supervised RCT (n=400) plus a five-centre paired external evaluation (n=761) of GraphCare-Agent (GCA), a knowledge graph–guided AI embedded in gastroenterology inpatient admission. GCA cut total workflow time by 213.9 s (29.5%, driven by follow-up work and editing, not interview time), raised PDQI-9 scores, and improved accurate preliminary diagnosis by 15.0 points, with zero attributable adverse events in 200 patients. This is a genuinely distinctive contribution — real-patient prospective RCTs of embedded clinical LLMs remain rare — but two flaws are decision-relevant: potential incorporation bias in the diagnosis-accuracy outcome, and a structurally mismatched documentation-workload metric.

Strengths: masked, adjudicated outcome assessment with de-identified, randomly intermixed records and a mandatory reconciliation delay; prespecified, granular safety reporting (tiered clinical-error severity, per-1,000-character conflict rates, exact CIs); and a prespecified physician-seniority interaction analysis yielding a coherent mechanistic story (junior physicians gain more diagnostic scaffolding, seniors gain more editing relief).

Weaknesses: the text-editing metric compares GCA's edit-delta on a pre-populated draft against SCW's full de-novo character count — not equivalent tasks, inflating the apparent workload reduction. Accurate preliminary diagnosis is scored against discharge diagnoses authored by the same physician who saw GCA's ranked suggestions, risking incorporation bias rather than a blinded ground-truth comparison. Generalizability is narrow (one institution's live RCT, one specialty, 1,055-disease candidate space, 28 physicians across 400 admissions), and no ablation isolates the knowledge graph's specific contribution from the underlying LLM.

**Decision: Send for Review.** The live-deployment rigor clears a high bar, but reviewers must adjudicate whether the diagnosis-accuracy outcome requires an independent reference standard and whether the editing-workload comparison needs reframing before acceptance.

---

### 5. Suggested Reviewer Expertise

Knowledge graph–guided retrieval and reasoning for clinical diagnostic decision support (RotatE embeddings, relational graph convolutional networks, CrossEncoder reranking). Speech recognition and semantic structuring pipelines for ambient, real-time clinical documentation. Design, masking, and cluster-robust statistical analysis of pragmatic, clinician-embedded RCTs of live clinical AI systems (CONSORT-AI/SPIRIT-AI methodology). Inpatient gastroenterology admission workflow, diagnostic reasoning, and documentation practice in tertiary-care hospital settings in China.

### 6. State-of-the-Art Literature Review (Past Three Years)

The field has moved rapidly from benchmark-only LLM evaluation toward embedded, randomized clinical evidence. Google DeepMind's AMIE line (Tu et al., *Nature*, 2025; extended to multimodal reasoning by Saab et al., *Nat. Med.*, 2026) established conversational diagnostic AI as competitive with primary care physicians in simulated dialogue, but neither has been tested in a live, consequential encounter. Zhao et al.'s DeepRare (*Nature*, 2026) is the closest technical analogue to GCA: a multi-agent, knowledge-source-integrating system with traceable reasoning for rare-disease differential diagnosis, evaluated retrospectively across nine datasets rather than prospectively in live care. On the clinical-trial side, Tao et al.'s PreA chatbot (*Nat. Med.*, 2026, three-arm RCT, 2,069 patients), Jia et al.'s Retina4IRD (*Nat. Med.*, 2026, multicentre RCT), and Agweyu et al.'s cluster-randomized generative AI decision-support trial in Kenyan primary care (*Nat. Med.*, 2026) collectively demonstrate that the field's leading edge is now prospective, randomized, real-patient evaluation — the same standard GCA meets. Ambient-documentation RCTs (Lukac et al., *NEJM AI*, 2025, DAX vs. Nabla vs. usual care; Afshar et al., *NEJM AI*, 2025) provide a directly comparable documentation-burden literature but are confined to outpatient settings and measure time-in-note rather than an integrated diagnostic-plus-documentation workflow. GCA's genuine advance is extending this randomized standard into the inpatient admission encounter with HIS write-back; its shortfall relative to this landscape is that, unlike DeepRare or Retina4IRD, it offers no ablation isolating the knowledge-graph contribution, and unlike Tao et al., it does not independently adjudicate diagnostic ground truth.

### 7. Suggested Reviewer Names

- **Knowledge-graph-guided diagnostic reasoning:** Weike Zhao (PhD candidate, School of Artificial Intelligence, Shanghai Jiao Tong University; co-first author, DeepRare, *Nature* 2026). Confirmed junior researcher.
- **Pragmatic RCT design for live LLM systems:** Xinge Tao and Shuya Zhou (co-first authors, PreA chatbot RCT, *Nat. Med.* 2026, Chinese Academy of Medical Sciences & Peking Union Medical College). Career stage inferred, not independently confirmed.
- **Ambient clinical NLP/ASR for documentation systems:** No verifiable junior candidate confirmed from available sources — flagged rather than defaulted to senior faculty.
- **Inpatient gastroenterology clinical workflow:** No verifiable junior candidate identified in this search pass.

---

## Further Literature (Past 3 Years, Similar Scope)

1. **Tao, X. et al.** An LLM chatbot to facilitate primary-to-specialist care transitions: a randomized controlled trial. *Nat. Med.* 32, 934–942 (2026). DOI: 10.1038/s41591-025-04176-7. Peer-reviewed. **Already cited (ref. 15).** Authors independent of submitting group (Chinese Academy of Medical Sciences & Peking Union Medical College). Three-arm RCT of a patient-facing LLM chatbot (PreA) performing history-taking, preliminary diagnosis, and test ordering before specialist consultation — closest comparator for GCA's structured pre-encounter information capture, but outpatient and patient-facing rather than clinician-facing/inpatient.

2. **Tu, T. et al.** Towards conversational diagnostic artificial intelligence. *Nature* 642, 442–450 (2025). DOI: 10.1038/s41586-025-08866-7. Peer-reviewed. **Already cited (ref. 16).** Independent (Google DeepMind). Introduces AMIE, a text-only conversational diagnostic LLM benchmarked against PCPs in simulated OSCE-style encounters — relevant for interview-fluency and diagnostic-accuracy comparators, though evaluated in simulation, not live care.

3. **Saab, K. et al.** Advancing conversational diagnostic AI with multimodal reasoning. *Nat. Med.* 32, 1726–1736 (2026). DOI: 10.1038/s41591-026-04371-0. Peer-reviewed. **Already cited (ref. 4).** Independent (Google DeepMind). Extends AMIE to multimodal (image/document) diagnostic dialogue via a state-aware reasoning framework — directly relevant to GCA's Patient State/Patient Graph updating mechanism, but again exploratory/simulated rather than an RCT.

4. **Jia, H. et al.** AI-based clinician decision support system for diagnosis of inherited retinal diseases: a multicenter, randomized trial. *Nat. Med.* (2026). DOI: 10.1038/s41591-026-04545-w. Peer-reviewed. **Already cited (ref. 17).** Independent (Shanghai Jiao Tong University / Shanghai General Hospital, with Korean and Polish collaborators). Multicentre RCT showing specialist+AI diagnostic accuracy of 88.5% vs. 67.3% unassisted — the field's strongest precedent for randomized, specialist-facing diagnostic decision support, useful as a benchmark for GCA's own preliminary-diagnosis effect size.

5. **Zhao, W. et al.** An agentic system for rare disease diagnosis with traceable reasoning. *Nature* 651, 775–784 (2026). DOI: 10.1038/s41586-025-10097-9. Peer-reviewed. **Already cited (ref. 19).** Independent (Shanghai Jiao Tong University / Shanghai AI Laboratory / Xinhua Hospital). DeepRare: a multi-agent, knowledge-source-integrating diagnostic reasoning system with traceable evidence links — the closest architectural analogue to GCA's knowledge graph pipeline, but validated on retrospective datasets rather than live deployment.

6. **Lukac, P. J. et al.** Ambient AI Scribes in Clinical Practice: A Randomized Trial. *NEJM AI* 2(12), 10.1056/aioa2501000 (2025). Peer-reviewed. **Not cited by the manuscript.** Independent (UCLA). Three-arm pragmatic RCT (DAX Copilot vs. Nabla vs. usual care, 238 physicians) measuring time-in-note and burnout — directly comparable documentation-workload design, but outpatient-only and does not integrate diagnostic decision support or HIS write-back; a natural comparator the authors should engage with for documentation-burden methodology.

7. **Wan, P. et al.** Outpatient reception via collaboration between nurses and a large language model: a randomized controlled trial. *Nat. Med.* 30, 2878–2885 (2024). DOI: 10.1038/s41591-024-03148-7. Peer-reviewed. **Not cited by the manuscript.** Independent (Chinese hospital group). RCT of an LLM-assisted nurse-patient reception workflow (2,185 patients) — relevant Chinese precedent for live LLM deployment with human-in-the-loop supervision and patient-experience outcomes, structurally analogous to GCA's clinician-confirmation design but pre-admission rather than diagnostic.

8. **Afshar, M. et al.** A pragmatic randomized controlled trial of ambient artificial intelligence to improve health practitioner well-being. *NEJM AI* 2, 10.1056/aioa2500945 (2025). Peer-reviewed. **Not cited by the manuscript.** Independent (University of Wisconsin). Stepped-wedge RCT using the PDSQI-9 documentation-quality instrument (a direct analogue to this manuscript's PDQI-9) alongside burnout outcomes — valuable for cross-instrument comparison of documentation-quality effect sizes.

9. **Sukhwal, P. C., Rajan, V. & Kankanhalli, A.** A joint LLM-KG system for disease Q&A. *IEEE J. Biomed. Health Inform.* 29(3), 2257–2270 (2025). DOI: 10.1109/JBHI.2024.3514659. Peer-reviewed. **Not cited by the manuscript.** Independent (National University of Singapore). A joint LLM–knowledge-graph architecture for disease question-answering — technically relevant to GCA's RotatE/R-GCN retrieval-and-reasoning design; the authors should address why this line of KG-LLM integration work is absent from their technical framing.

10. **Rau, S. et al.** A retrieval-augmented chatbot based on GPT-4 provides appropriate differential diagnosis in gastrointestinal radiology: a proof of concept study. *Eur. Radiol. Exp.* 8(1), 60 (2024). DOI: 10.1186/s41747-024-00457-x. Peer-reviewed. **Not cited by the manuscript.** Independent (University of Freiburg). A retrieval-augmented GPT-4 system generating GI differential diagnoses — the most domain-specific (gastroenterology) comparator identified and a notable omission given the manuscript's exemplar specialty.

072925
## 1. Overall Assessment

DeepECG-Tok proposes one instruction-tuned model, using a QINCo residual-quantization tokenizer aligned to MedGemma 4B-IT via a Q-Former, to replace the one-model-per-task paradigm in ECG AI. From a single frozen waveform representation it performs interpretation, structured reporting, and four linked endpoints (LVEF, structural heart disease, incident AFib, acute coronary occlusion/culprit-artery), tested on four external cohorts.

This unification is more ambitious than concurrent ECG-language work, and the four-cohort external validation (CLSA, Harvard-Emory, MIMIC-IV, EchoNext) exceeds the field norm. Two results undercut the headline claims: the pre-specified non-inferiority margin against cardiologist reports was missed (CI lower bound -0.16 crossed -0.05), and the structured JSON output, most likely used downstream, degraded most externally (0.76 to 0.42/0.38).

## 2. Strengths

One frozen tokenizer feeds narrative interpretation and four distinct endpoints through a shared Q-Former/LoRA backbone, genuinely dissolving task fragmentation. Four-cohort external validation without retraining is unusually thorough; ECG-Byte, PULSE, and MEIT do not clear this bar. The LLM-as-judge framework is empirically grounded, validated against two cardiologists (κ 0.82), addressing BLEU/ROUGE's known failure on synonymous phrasing. The signal-dependency ablation is a rare safety check: zeroed or mismatched input collapsed judge scores appropriately, with changed outputs in over 91% of cases.

## 3. Weaknesses

The abstract's "no significant difference" framing omits that the non-inferiority margin was missed. JSON interpretation, the most clinically actionable output, scored highest internally (0.76) yet fell hardest externally (0.42/0.38). Confabulation under corrupted input is closer to a deployment blocker than a limitation: zeroed input still returned a confident, unflagged answer 75.6% of the time. All four endpoints derive from one center's linkage; SHD, ACCO, and culprit-artery lack external AUROC validation, and no head-to-head against EchoNext's own model is reported despite using its exact test set.

## 4. Editorial Decision

Send for Review. The unified architecture and four-cohort validation clear the bar a narrower single-site paper would not meet; the case for rejection, that failing non-inferiority and confabulating under corrupted prompts is not yet clinically credible, is legitimate but addressable through revision. Reviewers should adjudicate the abstract's parity language, feasibility of a head-to-head AUROC against EchoNext, and whether JSON degradation is a fixable artifact or genuine fidelity loss.
## 5. Suggested Reviewer Expertise

Reviewers should cover residual vector-quantization/neural codec architectures for physiological time series; multimodal LLM alignment (Q-Former-style bridging) and parameter-efficient fine-tuning of medical LLMs; LLM-as-judge and clinical-NLG evaluation methodology; a board-certified cardiologist/electrophysiologist experienced in structured ECG reporting; and a clinician-scientist in echocardiography-linked ECG screening for structural heart disease, to adjudicate the EchoNext benchmarking gap.

## 6. State-of-the-Art Literature Review (Past 3 Years)

ECG-language modeling has moved from single-task classifiers toward instruction-following systems along two tracks. One discretizes the waveform for LLM input, including ECG-Byte and the concurrent discretized-tokenization framework variably named DiagECG/HeartLLM (arXiv:2508.15338), but these validate generation or classification alone, without linked clinical endpoints. The other bridges continuous or image-based encoders to LLMs for reporting and QA, including MEIT, PULSE, ECG-Chat, Q-Heart, and the multinationally validated ECG-GPT (Khunte et al., Eur Heart J Digit Health, 2026), again without mechanistic endpoints. Separately, SHD and LVEF screening advanced through purpose-built, non-generative models, EchoNext (Poterucha et al., Nature, 2025) and an independently validated single-lead ensemble algorithm (Aminorroaya et al., Eur Heart J Digit Health, 2025), both reporting AUROCs this manuscript's judge-score-only comparison does not engage.

DeepECG-Tok's genuine advance is combining tokenization-based generation with echo/catheterization-linked endpoints in one model across four external cohorts, which no identified competitor does. Its principal omission is failing to benchmark SHD/LVEF against the purpose-built AUROC literature on comparable cohorts, and failing to cite the concurrent tokenization line addressing overlapping architectural questions.

## Suggested Reviewers' Names

Tokenization/codec: Wenrui Han (ECG-Byte); Neil Zeghidour and Alexandre Défossez (neural audio codec lineage underlying QINCo). Multimodal LLM alignment/PEFT: Zongwei Wan (MEIT); Rossella Arcucci; Aditya Khunte (ECG-GPT). LLM-judge/clinical-NLG evaluation: Jack Gallifant (TRIPOD-LLM). Cardiology/reading-room workflow: Rohan Khera (Yale); Antônio Luiz Ribeiro (CODE-15). SHD/echo-linked screening: Pierre Elias and Timothy Poterucha (EchoNext). Note: Ilse Huijben (QINCo's originating author) is technically well-suited but carries a direct conflict of interest given the manuscript's adoption of her method.

---


## Editorial Integrity Alert (handling editor only)

Competing interests are extensively disclosed and unusually dense: Robert Avram reports a pending patent, equity in FrontRx and Divoco AI, a stock option in Spiralis Medical, and speaker fees from four companies. None appear directly competitive with DeepECG-Tok's commercial path, but the volume warrants confirming COI-management procedures are triggered. Self-citation is present but transparent: reference 3 (Nolin-Lapalme et al., Eur Heart J, 2026), anchoring the DeepECG-SSL baseline (0.93-0.94 AUROC), shares co-authors with the submission and is disclosed in-text, so this is a disclosure item rather than a violation. A numerical inconsistency needs verification against the clean source file: the MHI structural-heart-disease confusion matrix in Figure 3 (cells 1,009/572/442/1,016) sums to 3,039 ECGs, which does not visibly reconcile with the panel's printed n in this scanned copy; this may be a scan-legibility artifact rather than an authoring error, but should be confirmed before typesetting. No undisclosed preprints, salami-slicing, or unexplained author overlap with cited comparators beyond the disclosed self-citation were identified.

## Further Literature — Papers of Similar Scope (Past 3 Years)

1. **Poterucha, T.J. et al.** "Detecting structural heart disease from electrocardiograms using AI." *Nature*, 644, 221–230 (2025). doi:10.1038/s41586-025-09227-0. Peer-reviewed. **Cited by manuscript (ref. 13); its EchoNext dataset is used directly as an external cohort**, but no AUROC head-to-head is reported. Independent group (Columbia/NewYork-Presbyterian). This is the field's benchmark, purpose-built SHD model on the exact data-generating process used for external validation here.

2. **Elias, P. & Finer, J.** "EchoNext: A Dataset for Detecting Echocardiogram-Confirmed Structural Heart Disease from ECGs." *PhysioNet*, v1.1.0–1.1.1 (2025–2026). Data descriptor linked to a peer-reviewed parent paper (entry 1). **Cited (ref. 34); dataset used directly.** Independent group. Listed separately because the manuscript's SHD/LVEF external test set is drawn from this exact release, making a direct comparison to entry 1's model straightforwardly feasible and currently absent.

3. **Aminorroaya, A. et al.** "Development and Multinational Validation of an Ensemble Deep Learning Algorithm for Detecting and Predicting Structural Heart Disease Using Noisy Single-Lead Electrocardiograms." *European Heart Journal – Digital Health*, 6, 554–566 (2025). Peer-reviewed. Not cited. Independent authors (Yale). A second, independently validated SHD screening benchmark reporting AUROC on a comparable task; the manuscript scores its own SHD endpoint only via LLM-judge and should engage with this.

4. **Khunte, A. et al.** "Artificial intelligence-based automated interpretation of images of electrocardiograms: development and multinational validation of ECG-GPT." *European Heart Journal – Digital Health*, 7, ztag031 (2026). Peer-reviewed. **Cited (ref. 15) and directly benchmarked** on a six-label protocol (DeepECG-Tok wins 4/6 labels, loses on first-degree AV block, 0.66 vs 0.85). Independent authors (Yale). Strongest existing peer-reviewed, multinationally validated comparator; the manuscript's own numbers show non-uniform superiority.

5. **Liu, C., Wan, Z., Ouyang, C., Shah, A., Bai, W. & Arcucci, R.** "Zero-Shot ECG Classification with Multimodal Learning and Test-Time Clinical Knowledge Enhancement" (MERL). *ICML* 2024 (peer-reviewed conference proceedings); arXiv:2403.06659. Not cited. Independent authors (Imperial College London). Foundational ECG-text contrastive pretraining method (CLIP-style cross-modal alignment) directly analogous to the manuscript's own Stage 2 ECG-text contrastive objective; omission from the manuscript's related-work discussion of alignment strategy is notable.

6. **Zhao, Y., Kang, J., Zhang, T., Han, P. & Chen, T.** "ECG-Chat: A Large ECG-Language Model for Cardiac Disease Diagnosis." *IEEE ICME* 2025 (peer-reviewed conference proceedings); arXiv:2408.08849. Not cited. Independent authors. LLaVA-style contrastive encoder with conversational report generation; lacks linked clinical-endpoint prediction and cohort-level external validation, a materially weaker generalization claim than this manuscript's.

7. **[Author list unconfirmed from indexed excerpt — verify before citing]** "Contrastive Multi-modal Training with Electrocardiography and Natural Language Echocardiography Reports for Zero-shot Prediction of Structural Heart Disease" (MERL-ECHO). *medRxiv* 2025.09.16.25335870 (2025). Preprint, not yet peer-reviewed. Not cited. Multi-center study (Queen Mary Hospital/Tung Wah Hospital, Hong Kong), independent of the submitting group. Directly competing zero-shot, non-generative approach to the same SHD prediction problem via contrastive ECG-ECHO alignment rather than instruction-tuned generation; a relevant alternative paradigm the discussion does not address.

8. **Pham, H.M., Tang, J., Saeed, A. & Ma, D.** "Q-Heart: ECG Question Answering via Knowledge-Informed Multimodal LLMs." arXiv:2505.06296 (2025). Preprint, unreviewed. Not cited. Independent authors. Directly overlapping scope on the diagnostic-question-answering task specifically; a missed comparator for that evaluation category.

9. **[Authorship unresolved in indexed sources — verify before citing]** "DiagECG" / "HeartLLM: Discretized ECG Tokenization for LLM-Based Diagnostic Reasoning." arXiv:2508.15338 (2025). Preprint, unreviewed; title inconsistency across indexed sources should be confirmed against the arXiv abstract page. Not cited. Closest concurrent architectural competitor — discrete ECG tokenization plus LLM-based diagnostic reasoning, the same core mechanism as this manuscript — without linked clinical-endpoint prediction or comparable external-cohort breadth.

10. **[Authors not independently confirmed from indexed excerpt — verify before citing]** "Signal, Image, or Symbolic: Exploring the Best Input Representation for Electrocardiogram-Language Models Through a Unified Framework." arXiv:2505.18847 (2025). Preprint, unreviewed. Not cited. Directly relevant to the manuscript's own tokenizer-architecture-search subsection, since it systematically compares tokenized, image, and raw-signal inputs for ECG-LLMs; should be engaged with when justifying the QINCo choice.

**Peer-review balance:** 5 of 10 entries (1, 2 by extension, 3, 4, 5, 6) are peer-reviewed or descriptor-linked to a peer-reviewed parent; the remaining 4 (7, 8, 9, 10) are unreviewed preprints, reflecting how young this specific sub-literature is. This split should temper any framing of the manuscript's novelty against an already-settled field.

072954
## Editorial Report — Manuscript 072954T
**"Conventional medical benchmarks conceal failures of large language models to adapt to jurisdiction-specific standards of care"**

---

## 1. Overall Assessment

GeoMedBench pairs 90 KR–US guideline-conflict families (450 seeds, eight LLMs, 32,400 responses) to isolate jurisdictional adaptation from case difficulty, via context-switching success (CSS): strict correctness in both jurisdictional versions of the same seed. Its central finding — row-level accuracy (34.9–78.1%) systematically overstates CSS (15.8–62.7%), with non-monotonic, model-specific responses to added cues — is a genuine, clinically important measurement claim and a real advance over single-vignette or exam-style evaluation.

Two concerns dominate my read. First, the paper's most striking result — GPT-5.5 collapsing under jurisdiction-only framing (15.8%) but recovering under identity-only, combined, and instruction-augmented framing (61–64%) — is described but not mechanistically explained. Second, the manuscript omits the closest 2026 counterfactual-evaluation prior art, some of which reuses the "CSS" acronym for a different construct.

## 2. Strengths

The counterfactual pair design, four-reviewer physician/nurse adjudication (κ 0.635–0.741), and the model-specific (not uniformly US-directed) KR–US asymmetry are methodologically rigorous and non-obvious findings that correctly temper causal claims about training-data bias. The concurrent post hoc P2-G experiment isolating instruction-following from identity wording is a rare, welcome self-confound test.

## 3. Weaknesses

The GPT-5.5 collapse-and-recovery pattern lacks mechanistic explanation. Korean-language fragility is not disentangled from jurisdictional-adaptation failure. Turk's Causal Sensitivity Score (arXiv:2605.30590) and MedEinst (ACL 2026) — structurally close counterfactual designs — are uncited. Single-turn, greedy-decoding generation leaves CSS stability across stochastic reruns unverified.

## 4. Editorial Decision

**Send for review.** Design rigor and internally consistent reporting clear the bar; reviewers should adjudicate whether the P1–P4 mechanism needs ablation, whether the literature gap is fixable, and whether single-sample decoding suffices given the safety claims.

---

## 5. Suggested Reviewer Expertise

Reviewers should cover: (1) LLM evaluation methodology, specifically counterfactual/interventional benchmark design and rank-disagreement diagnostics between coverage-based and behavioral metrics; (2) prompt-sensitivity and mechanistic interpretability of instruction-following versus identity-cue processing in frontier LLMs; (3) multilingual and cross-jurisdictional NLP benchmark construction (Korean-language medical or legal domains); (4) family medicine or general internal medicine with working knowledge of both Korean and US guideline-development processes (KDA, USPSTF, ACC/AHA); and (5) biostatistics with expertise in cluster-bootstrap inference for paired diagnostic-accuracy designs. Split: roughly 70% technical, 30% clinical.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Counterfactual clinical LLM evaluation is an active 2025–2026 wave, not a novel category invented by this manuscript. MedEinst (Chen et al., ACL 2026) pairs DDXPlus-derived vignettes to test diagnostic fixation under discriminative-feature perturbation; MamaBench (Adewuyi et al., arXiv:2607.14385, correctly cited as ref. 21) applies the same paired-perturbation logic to maternal/paediatric diagnosis via its Bias Trap Rate; and Turk's Causal Sensitivity Score (arXiv:2605.30590, uncited) applies interventional scoring to oncology tumor-board recommendations, explicitly demonstrating — as this manuscript does — that coverage-based accuracy and counterfactual responsiveness rank models in nearly opposite orders. A parallel strand addresses geography directly: a Kenyan primary-care benchmarking paper (arXiv:2507.14615) proposes "Geographic-Contextual Adaptability" as an explicit metric, and XL-SafetyBench (arXiv:2605.05662) applies country-grounded paired evaluation to safety rather than clinical concordance.

Against this landscape, GeoMedBench's distinct contribution is the two-country, same-language, guideline-conflict-family design with mandatory joint label-and-action correctness — a stricter and more clinically specific instrument than the geographic-adaptability or safety-focused alternatives. It does not, however, engage with the CSS-acronym collision or with MedEinst's structurally identical paired-seed logic, and a revision should situate the paper explicitly within this cluster rather than treating jurisdictional adaptation as an unaddressed gap in the literature.

## 7. Suggested Reviewers (by expertise area)

- **Counterfactual/interventional LLM evaluation methodology:** Matt Turk (Protege Data Lab); authors of MedEinst (W. Chen, G. Huang — ACL 2026); Thanni Adewuyi (HelpMum Africa, MamaBench).
- **Prompt-sensitivity / mechanistic interpretability:** researchers publishing on identity-cue and sociodemographic-shortcut effects in clinical LLMs (e.g., groups extending Omar et al., *Nat. Med.* 2025); no verifiable junior candidate with a directly comparable mechanistic-ablation publication could be confirmed in the time available — flagged rather than defaulting to senior faculty.
- **Korean/multilingual cross-jurisdictional benchmark construction:** Wonseok Hwang (Assistant Professor, University of Seoul; KBL Korean legal-LLM benchmark, directly comparable paired-jurisdiction design methodology, legal rather than clinical domain).
- **Clinical guideline concordance (KR/US primary care or oncology):** a junior faculty member in family medicine or preventive oncology with joint KDA/USPSTF or NCCN/Korean-guideline authorship experience; specific verifiable candidate not identified — flagged for editorial follow-up rather than defaulted to a senior author.
- **Biostatistics (paired diagnostic accuracy, cluster bootstrap):** a statistician with published family-cluster or hierarchical bootstrap work in diagnostic-test-accuracy meta-analysis.

---

## Editorial Integrity Alert (for handling editor only)

**Numerical consistency:** A full independent recheck of Table 2, Table 3, Figure 4's incorrect-row denominators, and the abstract's summary statistics found no arithmetic inconsistencies — all percentages, CSS counts, and error-composition denominators reconcile exactly against the reported n. This is a positive integrity finding, not a concern.

**Model identity verification:** All eight named models (GPT-5.5, Claude Opus 4.8, Gemini 3.1 Pro, Qwen3.5-Plus, Solar Pro 3, Mistral Large 3, Llama 4 Maverick, MedGemma 27B Text) correspond to real, dated 2026 releases; no fabricated or anachronistic model claims detected.

**Reference formatting anomaly:** References 8, 10, 27, and 28 are missing article titles in the printed list (author names, venue, and pagination only). I independently confirmed ref. 8 (Nakajima, Saito & Nishikawa, *J. Can. Assoc. Gastroenterol.*, gwag024, 2026, DOI 10.1093/jcag/gwag024) is a real, correctly attributed paper. Given the source file is a phone/CamScanner scan, this is most likely an OCR or reference-manager truncation artifact rather than fabrication, but the authors should be asked to submit a clean, machine-readable reference list before proceeding, since malformed entries cannot be fully verified from a scan alone.

**Author and competing-interest check:** Corresponding author EunKyo Kang has a verifiable, consistent publication record in cancer screening, health informatics, and text mining at the National Cancer Center Korea. No overlap was found between the author list and any cited comparator group (MamaBench, MedEinst, or the uncited Turk CSS paper). Declared funding (National Cancer Centre Korea; Ministry of Trade, Industry & Energy) shows no LLM-vendor funding; no undisclosed competing interest identified.

**Literature-engagement gap (not misconduct):** The omission of Turk (arXiv:2605.30590) and MedEinst (ACL 2026) from the reference list is a scholarly gap flagged in Section 3/6 above, not an integrity concern — both are 2026 preprints/proceedings that may postdate the authors' literature search cutoff.

---

## Further Literature — Papers of Similar Scope (Past 3 Years)

1. **Turk, M.** "Counterfactual Evaluation Reveals Hidden Capability Profiles in Clinical LLMs and Agents." arXiv:2605.30590 (2026). *Peer review:* workshop preprint, unreviewed. *Cited:* No. *Independence:* Independent. *Relevance:* Same-acronym "Causal Sensitivity Score"; closest structural analogue to this manuscript's core claim.

2. **Chen, W., Huang, G., Wang, W. & Zhu, Z.** "MedEinst: Benchmarking the Einstellung Effect in Medical LLMs through Counterfactual Differential Diagnosis." *Proc. 64th ACL* (2026). *Peer review:* Yes. *Cited:* No. *Independence:* Independent. *Relevance:* Nearest paired-seed design, applied within-jurisdiction.

3. **Adewuyi, T. et al.** "MamaBench." arXiv:2607.14385 (2026). *Peer review:* Preprint, unreviewed. *Cited:* Yes (ref. 21). *Independence:* Independent. *Relevance:* Nearest prior counterfactual-pair instrument in clinical AI.

4. "Retrieval-Augmented Clinical Benchmarking...Kenyan Primary Care." arXiv:2507.14615 (2025). *Peer review:* Preprint, unreviewed. *Cited:* No. *Independence:* Independent. *Relevance:* "Geographic-Contextual Adaptability" metric — directly parallel framing.

5. "MedEqualQA." arXiv:2510.12818 (2025). *Peer review:* Preprint, unreviewed. *Cited:* No. *Independence:* Independent. *Relevance:* Counterfactual pronoun-only perturbation; contrasts with P1 identity-only arm.

6. **Munira, A. & M.D.M.E.** "Mind the gap..." arXiv:2507.16322 (2025). *Peer review:* Preprint, unreviewed. *Cited:* Yes (ref. 11). *Independence:* Independent. *Relevance:* Supports representativeness motivation.

7. "XL-SafetyBench." arXiv:2605.05662 (2026). *Peer review:* Preprint, unreviewed. *Cited:* No. *Independence:* Independent. *Relevance:* Country-grounded paired evaluation generalized to safety.

8. **Nakajima, K., Saito, H. & Nishikawa, Y.** *J. Can. Assoc. Gastroenterol.*, gwag024 (2026). *Peer review:* Yes. *Cited:* Yes (ref. 8, malformed). *Independence:* Independent. *Relevance:* Documents cross-country guideline heterogeneity motivating the design.

9. "Assessing the Limitations of LLMs in Clinical Practice Guideline-concordant Treatment Decision-making..." medRxiv 2024.11.20.24313385 (2024). *Peer review:* Preprint, unreviewed. *Cited:* No. *Independence:* Independent. *Relevance:* Single-jurisdiction concordance already fails on real data.

10. **Kim, H. J. et al.** *Sci. Rep.* **15**, 36082 (2025). *Peer review:* Yes. *Cited:* Yes (ref. 3). *Independence:* Independent. *Relevance:* Examination-performance baseline this manuscript argues is insufficient.

11. **Lim, K. H. et al.** "Susceptibility of LLMs to User-Driven Factors in Medical Queries." arXiv:2503.22746 (2025). *Peer review:* Not confirmed. *Cited:* No. *Independence:* Independent. *Relevance:* Converges with this manuscript's own prompt-driven non-monotonicity finding.

073314
# Editorial Report: OralReasoner: a multimodal foundation model for unified dental panoramic radiograph interpretation

### 1. Overall Assessment

OralReasoner unifies dental structure segmentation, disease localization, and grounded VQA for panoramic radiographs, routing LLaVA/Vicuna-7B <SEG>/<BOX> tokens into SAM-ViT-H and YOLOv8-M, trained on 2,091 images, 49,498 annotations, and 33,432 LLM-generated QA pairs. It competently adapts LISA-style reasoning segmentation to a genuine cross-age-group gap. But refs 8 and 10, DentVLM (Nature Communications, 2026) and DentFound (Nature Biomedical Engineering, 2026), already do this at ~50x scale with clinician validation OralReasoner lacks, and neither is benchmarked against.

### 2. Strengths

The token-routing design is a genuine extension: a parallel <BOX> token/category parser feeds YOLOv8-M alongside LISA's <SEG> mechanism, with an oral structure perceiver resolving root furcation. The cross-age-group dataset (986 pediatric, 1,087 adult images) is uncommon; LISA baselines here were adult-only. Compound-instruction robustness is quantitatively real: triple-mask Dice (0.8764) matches single-mask (0.8726), and cross-quadrant instructions hold at 0.92 versus 0.15-0.74 for LISA/LISA-Plus.

### 3. Weaknesses

Novelty is eroded: DentVLM (110,447 images, 36 tasks, 25-dentist validation) and DentFound (101,000+ patients, 98 diseases, 12-reader validation) occupy the same space at far greater scale and rigor, yet are cited without benchmarking; comparisons run only against general-domain LISA/LISA-Plus and zero-shot HuatuoGPT. No clinical reader study exists anywhere, despite Discussion claims the model reduces "unnecessary specialist consultations." Data provenance is weak: two of three source datasets (IntelliDent, vzrad2) are unreviewed Roboflow uploads, and 33,432 QA pairs were LLM-generated with only "automatic filtering." Stated category counts sum to 45,026, not the reported 49,498 total, and Figure 2b's proportions disagree with Figure 2d/text. External validation covers only 100 adult images, permanent-tooth segmentation alone.

### 4. Editorial Decision

**Reject.** SAM-based mask grounding with cross-age-group coverage is a real niche, but clinical framing is unsupported, novelty is undercut by two unbenchmarked Nature-family competitors, and dataset figures don't reconcile. Suggested transfer: npj Digital Medicine, or Communications Engineering for the architecture.

### 5. Suggested Reviewer Expertise

Referring/reasoning segmentation architectures (SAM prompt encoding, LISA-style token grounding); multimodal LLM domain adaptation via LoRA; medical object detection (YOLO-family lesion localization); pediatric dental radiology and mixed-dentition development; oral/maxillofacial radiology covering caries, periapical lesions, and impacted teeth.

### 6. State-of-the-Art Literature Review (Past 3 Years)

DentVLM and DentFound established that dental VLMs reach near-specialist performance at scale with real clinical validation. Parallel work pushed segmentation- and reasoning-specific directions: Hao et al.'s NeurIPS 2025 panoramic instruction dataset, T-Mamba's 2D/3D tooth segmentation, PerioDet's periapical-lesion benchmark, and 2025-2026 preprints (OralGPT-Omni, DentalGPT, OPGAgent) pursuing agentic dental reasoning. OralReasoner's genuine advance, pixel-level SAM masks coupled to LLM parsing across pediatric and adult dentition simultaneously, is not replicated elsewhere. But it does not engage DentVLM or DentFound directly, and its evaluation stays automated-metric-only where the field's leading papers now report dentist-in-the-loop trials.

---

### 5 (cont.). Suggested Reviewers' Names

- **Referring/reasoning segmentation:** Xin Lai (LISA); Senqiao Yang (LISA++); Feng Li (Segment Anything family extensions); Xin Yu (medical grounding segmentation).
- **Multimodal LLM / dental VLM architecture:** Zijie Meng (DentVLM); Zuozhu Liu (DentVLM, Zhejiang University); Qi Zhu (DentFound); Jing Hao (dental multimodal benchmarks, HKU).
- **Medical object detection:** Kuo Feng Hung (HKU, dental VLM/tooth-detection evaluation); Andy Wai Kan Yeung (HKU, dentomaxillofacial radiology AI); Bingzhi Chen (PerioDet).
- **Pediatric dental radiology / mixed dentition:** a pediatric dental radiologist with mixed-dentition segmentation experience (name not independently verifiable from available literature; flagged for editorial follow-up).
- **Oral/maxillofacial radiology (caries, periapical lesions, impacted teeth):** Ethem Hamamci (DENTEX); a practicing oral radiologist from the impacted-tooth/periapical-lesion clinical literature.

---

## Editorial Integrity Alert (Handling Editor Only)

**Numerical inconsistency, dataset composition.** Main-text category counts (permanent 27,677; deciduous 13,926; oral diseases 2,340; other 1,083) sum to 45,026, not the stated total of 49,498 fine-grained instance annotations — a 4,472-instance (9%) gap. Separately, Figure 2b's pie-chart percentages (61.3/31.0/5.2/2.4%) do not match Figure 2d's bar chart and the main text's stated percentages (61.5/28.0/8.0/2.2%) for what is presented as the same dataset breakdown. Authors should be asked to reconcile both the underlying counts and the two figure panels before any further consideration.

**Undisclosed direct competition, not an integrity violation per se but requiring editorial scrutiny.** References 8 (DentVLM, *Nature Communications*, 2026) and 10 (DentFound, *Nature Biomedical Engineering*, 2026) are near-identical in scope to this submission and were published in comparably prestigious venues within the same window. The manuscript cites both but does not benchmark against either or explain the omission. This should be raised with the authors directly rather than assumed to be innocent.

**Data provenance.** Two of three source datasets (IntelliDent, vzrad2) are Roboflow community uploads without documented peer review, licensing terms, or inter-annotator agreement statistics. QA-pair generation relied on LLM output (Lingshu) with only "automated evaluation and filtering," and no dentist verification rate is reported for the 33,432 pairs used in training and evaluation.

**Author overlap / competing interests.** No author overlap was found between the submitting group (Zhejiang Hospital, Hangzhou City University, Zhejiang University College of Pharmaceutical Sciences) and the authors of LISA, LISA-Plus, HuatuoGPT, DentVLM, or DentFound. Competing interests are declared as none; nothing in the available record contradicts this.

**Ethics.** IRB approval (Zhejiang Hospital, ZJHIRB-2025-169K) and Helsinki Declaration compliance are stated and appear adequate; images are reported as de-identified.

---

## Further Literature (Past 3 Years, Similar Scope) — minimum 10 entries as requested

1. **Meng, Z. et al. "DentVLM: A multimodal vision-language model for comprehensive dental diagnosis and enhanced clinical practice."** *Nature Communications* (2026). DOI: 10.1038/s41467-026-75718-x. Peer-reviewed, published. **Already cited by manuscript (ref. 8), but never benchmarked.** Authors independent of submitting group. 110,447 images, 2.46M VQA pairs, 36 diagnostic tasks across 7 imaging modalities, IoU-based disease localization, rationale generation, validated by 25 dentists across 1,946 patients. Directly competing, larger-scale, clinically validated.

2. **Zhu, Q., Lin, Y., Fu, W. et al. "Towards clinical-level interpretation of dental panoramic radiography using an instance-guided vision-language model" (DentFound).** *Nature Biomedical Engineering* (2026). DOI: 10.1038/s41551-026-01713-8. Peer-reviewed, published. **Already cited (ref. 10), never benchmarked.** Independent authors. 101,000+ patients, ages 2-98, 98 diseases, report generation validated by 12 dentists/radiologists. Most direct competitor to OralReasoner's "instance-level, cross-age-group" framing.

3. **Lai, X., Tian, Z., Chen, Y. et al. "LISA: Reasoning Segmentation via Large Language Model."** *CVPR* (2024); arXiv:2308.00692 (2023). Peer-reviewed (CVPR oral). **Already cited and used as baseline (ref. 30).** General-domain, not dental. Foundational <SEG>-token architecture that OralReasoner's design directly extends.

4. **Yang, S., Qu, T., Lai, X. et al. "LISA++: An Improved Baseline for Reasoning Segmentation with Large Language Model."** arXiv:2312.17240 (2023). Preprint, unreviewed. **Already cited and used as baseline (ref. 31, "LISA-Plus").** General-domain.

5. **Chen, J. et al. "HuatuoGPT-Vision, Towards Injecting Medical Visual Knowledge into Multimodal LLMs at Scale."** arXiv:2406.19280 (2024). Preprint, unreviewed. **Already cited and used as zero-shot baseline (ref. 32).** General medical domain, not dental-specific.

6. **Hao, J., Fan, Y., Sun, Y. et al. "Towards Better Dental AI: A Multimodal Benchmark and Instruction Dataset for Panoramic X-ray Analysis."** *NeurIPS* (2025); arXiv:2509.09254. Peer-reviewed (NeurIPS). Not cited by manuscript. Independent group (University of Hong Kong). Large multimodal instruction dataset and benchmark for panoramic X-ray reasoning; directly overlapping scope not engaged.

7. **Fang, X., Cai, J., Liu, H. et al. "PerioDet: Large-Scale Panoramic Radiograph Benchmark for Clinical-Oriented Apical Periodontitis Detection."** arXiv:2507.18958 (2025). Preprint, unreviewed. Not cited. Independent (Beijing Institute of Technology, South China Normal University). 3,673 images, 5,662 annotated periapical-lesion instances — a disease-specific benchmark far larger than OralReasoner's periapical-lesion test subset (298 regional samples), which the authors should have compared against for the periapical-lesion task specifically.

8. **Hao, J. et al. "T-Mamba: A Unified Framework with Long-Range Dependency in Dual-Domain for 2D & 3D Tooth Segmentation."** arXiv:2404.01065 (2024). Preprint, unreviewed. Not cited. Independent. Directly relevant unified 2D/3D tooth-segmentation architecture omitted from the manuscript's segmentation-methods discussion.

9. **Sun, Y., Zhang, X., Yang, Y. et al. "OralGPT-Omni: A Versatile Dental Multimodal Large Language Model."** arXiv:2511.22055 (2025). Preprint, unreviewed. Not cited. Independent. Versatile dental MLLM covering a broader task set than OralReasoner; contemporaneous and unengaged.

10. **"DentalGPT: Incentivizing Multimodal Complex Reasoning in Dentistry."** arXiv:2512.11558 (2025). Preprint, unreviewed. Not cited. Independent. Reasoning-focused dental MLLM using reinforcement learning; relevant recent advance in dental clinical reasoning not discussed.

11. **Hamamci, I.E. et al. "DENTEX: Dental Enumeration and Tooth Pathosis Detection Benchmark for Panoramic X-ray."** arXiv:2305.19112 (2023). Preprint, unreviewed as a standalone paper (challenge dataset). **Already used as a training-data source (ref. 39) but not discussed as a comparator benchmark for enumeration + pathosis detection**, which is a closely related task to OralReasoner's disease-localization function.

12. **Yu, Z., Yang, L., Babicka, B. et al. "OPGAgent: An Agent for Auditable Dental Panoramic X-ray Interpretation."** arXiv:2603.00462 (2026). Preprint, unreviewed. Not cited. Independent. Agentic, auditable interpretation pipeline for panoramic X-rays — a 2026 contemporaneous alternative to OralReasoner's end-to-end model that the authors could not have missed given the overlapping venue and timeframe of dental-AI arXiv preprints.

*Peer-review status and independence were checked via targeted web search of publisher pages, arXiv abstract pages, and dblp records; entries marked "preprint, unreviewed" have not been confirmed as accepted to a peer-reviewed venue as of this review.*

073334
## Editorial Report — "Small evaluation sets lead to erroneous selection of subgroup-specific clinical prediction models"

## 1–4. Overall Assessment, Strengths, Weaknesses, Editorial Decision

SplitCheck benchmarks the standard heuristic for choosing between a pooled model and per-subgroup models — keep separate models if they beat pooling on held-out loss — showing this decision rule is itself an unbenchmarked estimator. Using a paired oracle across simulated cohorts and MIMIC-IV/eICU-CRD, the authors find a realistic 30% evaluator licenses harmful splits in 28.6% of replicates (versus 6.3% on an idealized 4,000-row set), with 89.9% of the excess attributable to evaluator size alone. Three further decision rules, including Ustun, Liu and Parkes's preference-guarantee procedure, are shown to fail in distinct ways.

The dual-evaluator design isolating evaluator size from group count is a genuine methodological advance, and the reproduction of the source paper's own results before benchmarking the preference-guarantee rule is a strong validity control. The eICU age-band application is a credible real-data anchor with an unambiguous gradient.

Weaknesses are material: the simulation uses one outcome-generating mechanism (binary logistic, 20% prevalence), untested for survival or non-tabular architectures; no real-data case shows the estimator correctly licensing a *beneficial* split, only null and harm cases; both ICU cohorts are US-only and the two grouping axes tested (sex, age) are not the race/ethnicity/site axes central to current clinical-AI fairness debates; and the prose is dense enough to undercut the broad-readership standard this journal applies.

**Decision: Reject**, with encouragement to resubmit to a specialized venue (npj Digital Medicine or a statistics/ML methods journal). The contribution is real but reads as ML-theory/biostatistics work lacking a demonstrated translational payoff; a genuinely strong counterargument is that a rigorous operating-characteristics benchmark for a decision every clinical-AI pipeline makes silently could be broadly consequential regardless of readability, and reviewers should weigh whether that theoretical import outweighs the narrow real-data scope.

## 5. Suggested Reviewer Expertise

Reviewers should cover: (1) generalization theory for group-fair and multi-group learning (Rademacher-complexity bounds, transductive multi-group guarantees); (2) sample-size and events-per-parameter methodology for clinical prediction model development and subgroup interaction testing; (3) decoupled-classifier and preference-guarantee fairness procedures and their surrogate-loss behavior; (4) critical-care outcome modeling using MIMIC-IV/eICU-CRD, including subgroup calibration and site heterogeneity; and (5), on the clinical side, a critical-care or emergency-medicine physician with experience evaluating deployed risk-stratification tools for actual bedside decision impact.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The pool-versus-separate question has moved rapidly in the theoretical fairness literature over the past three years. Cousins, Kumar and Venkatasubramanian's "To Pool or Not To Pool" derives group-specific generalization bounds showing that group-fair training on shared models benefits disproportionately from the majority group's larger sample size, with the improvement most pronounced for smaller groups (AISTATS 2024) — this is the paper's own primary theoretical anchor (ref. 3) and the manuscript correctly credits it, though it does not engage with I. Elizabeth Kumar's subsequent applied work extending this line into health-policy evaluation contexts. Bergam, Deng and Hsu's 2026 preprint on the price of multi-group transductive learning extends error-penalty theory as group counts grow, also already cited. On the applied clinical-fairness side, Benitez-Aurioles and colleagues' subgroup net-benefit framework (Epidemiology, 2026) and the broader npj Digital Medicine scoping review of clinical AI fairness metrics by Liu, Ning and colleagues (2025) both argue, as this manuscript does, that existing fairness paradigms conflate detection of a subgroup difference with a deployment recommendation — a conceptual convergence the discussion section does not explicitly connect to. Liu and colleagues' GroupFasterRisk (JAMIA, 2025) and the ELDER-ICU study (Lancet Digital Health, 2023) both build and evaluate subgroup-aware mortality risk scores directly on eICU/MIMIC-family cohorts with explicit subgroup bias evaluation, making them the closest applied comparators the authors should engage but do not cite. On the biostatistics side, Riley and colleagues' "Importance of sample size on the quality and utility of AI-based prediction models for healthcare" (Lancet Digital Health, 2025) and Barreñada, Steyerberg, Van Calster and colleagues' 2025 preprint on "the fundamental problem of risk prediction for individuals" both make closely related arguments about instability of subgroup-level estimates at realistic sample sizes, and Rountree and colleagues' 2024 "Reporting of Fairness Metrics in Clinical Risk Prediction Models: A Call for Change" documents the exact reporting gap SplitCheck's subscale targets. Hollmann and colleagues' TabPFN v2 (Nature, 2025), used here as the manuscript's tabular foundation-model arm, and Do, Nandi, Putzel, Smyth and Zhong's joint fairness model for underrepresented populations (Biometrics, 2023, already cited as ref. 39) round out the last three years of directly relevant work. Against this landscape, the manuscript's distinctive advance is the paired-oracle design isolating evaluator size from group count; its gap is that it does not empirically engage the applied eICU/MIMIC fairness literature (GroupFasterRisk, ELDER-ICU) that already operationalizes the same cohorts for a closely related question.

## 7. Suggested Reviewers

**Generalization theory / multi-group fairness:** I. Elizabeth Kumar (postdoctoral scholar, Stanford Health Policy); Cyrus Cousins (Brown University); Jose Benitez-Aurioles (Centre for Health Informatics, University of Manchester).
**Clinical prediction model methodology / sample size:** Lasai Barreñada (KU Leuven, Van Calster group); a member of the Riley/Collins TRIPOD+AI collaboration.
**Critical-care AI and subgroup calibration on MIMIC/eICU:** an author from the GroupFasterRisk (JAMIA 2025) or ELDER-ICU (Lancet Digital Health 2023) groups.
**Clinical/critical-care:** a critical-care attending or fellow with eICU-CRD or MIMIC-IV deployment experience, ideally with laryngology/dermatology familiarity given the worked example.

---

## Further Literature

1. Cousins C, Kumar IE, Venkatasubramanian S. To Pool or Not To Pool: Analyzing the Regularizing Effects of Group-Fair Training on Shared Models. *Proc Mach Learn Res* 2024;238:4573-4581. Peer-reviewed (AISTATS). Cited by manuscript (ref. 3). Independent of submitting group. Foundational theory for the manuscript's "architectural value" concept — the closest theoretical relative.

2. Riley RD, et al. Importance of sample size on the quality and utility of AI-based prediction models for healthcare. *Lancet Digit Health* 2025;7(6):e100857. Peer-reviewed. Not cited. Independent. Makes a closely related argument about small-sample instability that would strengthen the introduction's motivation.

3. Benitez-Aurioles J, Joules A, Brusini I, Peek N, Sperrin M. Understanding algorithmic fairness for clinical prediction in terms of subgroup net benefit and health equity. *Epidemiology* 2026;37(3):386-396. Peer-reviewed. Cited by manuscript (ref. 35). Independent. Reframes subgroup fairness around deployment impact, conceptually parallel to this manuscript's benefit/harm oracle.

4. Liu M, Ning Y, Teixayavong S, et al. A scoping review and evidence gap analysis of clinical AI fairness. *npj Digit Med* 2025;8(1):360. Peer-reviewed. Not cited. Independent. Documents the field-wide reporting gap this manuscript's subscale targets; should be engaged directly.

5. Liu X, Zhang Z, et al. Fast and interpretable mortality risk scores for critical care patients (GroupFasterRisk). *J Am Med Inform Assoc* 2025. Peer-reviewed. Not cited. Independent. Applied comparator built and fairness-tested on the same MIMIC/eICU family of databases.

6. Liu X, Hu P, Yeung W, et al. Illness severity assessment of older adults in critical illness using machine learning (ELDER-ICU): an international multicentre study with subgroup bias evaluation. *Lancet Digit Health* 2023;5(10):e657-e667. Peer-reviewed. Not cited. Independent. Closest applied precedent for age-band subgroup bias evaluation in critical care.

7. Hollmann N, Müller S, Purucker L, et al. Accurate predictions on small data with a tabular foundation model. *Nature* 2025;637(8045):319-326. Peer-reviewed. Cited by manuscript (ref. 33). Independent. Basis for the manuscript's TabPFN v2 foundation-model arm.

8. Do H, Nandi S, Putzel P, Smyth P, Zhong J. A joint fairness model with applications to risk predictions for underrepresented populations. *Biometrics* 2023;79(2):826-840. Peer-reviewed. Cited by manuscript (ref. 39). Independent. Alternative statistical approach to the shared-vs-separate modeling problem in underrepresented clinical subgroups.

9. Barreñada L, Steyerberg EW, Timmerman D, Thomassen D, Wynants L, Van Calster B. The fundamental problem of risk prediction for individuals: health AI, uncertainty, and personalized medicine. arXiv:2506.17141, 2025. **Preprint, not peer-reviewed.** Not cited. Independent. Conceptually adjacent argument about individual- versus group-level risk estimate instability; should be flagged to authors as unreviewed.

10. Bergam N, Deng S, Hsu D. The price of multi-group transductive learning. arXiv:2606.04423, 2026. **Preprint, not peer-reviewed.** Cited by manuscript (ref. 4). Independent. Extends error-penalty theory for group counts; authors should note its preprint status when citing.

072615
# Editorial Report — Manuscript 072651

**Title:** Multi-Model Deep Learning-based Fully Automated Design Framework for Patient-Specific Instrumentation in Reverse Total Shoulder Arthroplasty
**Section:** Digital Health / Clinical AI — Musculoskeletal
**Recommendation:** **Reject** (with referral to Editorial Integrity)

---

## Editorial Integrity Alert — Confidential, Handling Editor Only

**1. Code availability statement is not satisfied, and the deposited repository does not match the described methods.** The manuscript directs readers to `https://github.com/Louis-Youn/Code_Storage`. I retrieved this repository directly. It is a generic, undescribed store containing four items: `Sample Data.zip`, `SemanticSeg_Training_Ver2.m`, `Source_Code_for_Deep_Learning_Model.m`, and `[Training Data for YOLO] Elbow_Label.mat`. These are MATLAB assets. The manuscript states that the models were trained using the Ultralytics YOLO v11 implementation with annotation conversion performed in Python 3.11. No Ultralytics configuration, training script, weights, or evaluation code is present. The repository predates this work and appears to be a shared deposit reused across the group's publications. As deposited, none of the reported detection or segmentation results can be reproduced or audited. This should be put to the authors as a direct query before any further consideration.

**2. Absent ethics and consent coverage for the prospective clinical application.** The IRB statement covers a retrospective imaging study, with consent waived on that basis. Figures 7 and 8 date the two surgeries to 24 June 2026 and 29 July 2026, well outside the stated internal cohort accrual window of March 2023 to May 2025. These were prospective implantations of custom-manufactured, SLM stainless-steel and SLA resin surgical guides in two elderly patients. No ethics approval, no informed consent statement, and no regulatory pathway (Korean MFDS custom-device or investigational-device route) is declared for that prospective use. A retrospective consent waiver cannot cover the manufacture and intraoperative use of a bespoke cutting guide. This is the most serious issue in the submission and requires an explicit response.

**3. External cohort ethics not addressed.** Twenty patients from Seoul National University Bundang Hospital were used for external validation. Only "our institution" IRB approval is reported. Approval or a data-transfer agreement from the external site is not stated.

**4. Undisclosed relevant prior work by the same author group.** Jeon and Yoon previously co-published a directly analogous study (Park K-B, Kim M-S, Yoon D-K, Jeon Y-D. *J Orthop Surg Res* 2024;19:648; DOI 10.1186/s13018-024-05128-6) applying deep learning to preoperative arthroplasty planning, in which the two are noted as contributing equally. That work is not cited. This is not self-citation inflation but its inverse — omission of the group's own closest prior art, which bears on the novelty claim.

**5. Commercial entanglement is under-declared relative to the author contribution statement.** D.-K.Y. is affiliated with EASO Co., Ltd., holds patent applications on the technology, and declares the only competing interest. However, the proprietary planning and PSI-generation software — withheld from release explicitly for "intellectual property and commercialization restrictions" — is the company's core asset, and the co-first author S.-G.J. is credited with designing and fabricating the guides and developing the AI models and software while listing only the academic affiliation. The corresponding author Y.D.J. performed all surgeries and provided clinical guidance. In effect, the developers, the operating surgeons, the guide manufacturers, and the outcome assessors are one group with a commercial interest, and the primary accuracy endpoint was measured by that group on their own software without blinding or an independent observer. The competing-interest statement should be broadened.

**6. Reviewer exclusion.** Kyoung Hwan Koh, In-Ho Jeon, and colleagues at Asan Medical Center must not be invited. Asan Medical Center is University of Ulsan College of Medicine — the submitting institution.

**7. Anonymisation is inconsistent.** The surgeon's name and the IRB number are redacted in the body text while the corresponding author is fully identified on the title page. This is cosmetic rather than substantive, but it should be corrected.

**8. Internal inconsistency in reported patient age.** Patient B is a 77-year-old woman in the Results and in the Figure 8 label, but a 79-year-old woman in the Figure 7 legend. With n=2, a discrepancy in one of two case descriptions warrants a source-data check.

---

## 1. Overall Assessment

Four task-specific YOLO v11 models detect five humeral landmarks on axial CT; fixed geometric rules convert them into retroversion, a canal entry axis, and a neck cutting plane; Boolean operations on a thresholded bone mesh yield a printable patient-specific instrument. Detection is tested in twenty internal and twenty external patients, and the workflow is demonstrated in two clinical cases. The humeral-side focus fills a genuine gap and the geometry is unusually transparent. The paper fails structurally: its defining output, the derived surgical parameters, is never validated against any reference.

## 2. Strengths

The four-model decomposition is motivated by measured failure of joint training on the humeral cartilage margin, and instance segmentation replaces box centroids for the shaft landmarks because centroids miss the anatomical centre of mass in elongated cross-sections. Equations 4 to 23 fully specify the geometry, including a signed `arctan2` version formulation preserving the retroversion-anteversion distinction. Encoding native version in the guide, rather than 10, 20, or 30 degree instrument settings, answers a real limitation. The limitations section is candid.

## 3. Weaknesses

Retroversion, canal axis, and cutting plane are compared to no reference — not blinded experts, not commercial software, not a geometric ground truth — while Spangenberg et al. (JSES 2025) set that bar in 62 humeri and are cited but unmatched. Constants (1:9 canal interpolation, 2 mm offset, 30% threshold) are unjustified and untested for sensitivity. Version depends on ordered vector differences, yet medial-lateral assignment is unspecified and flip augmentation destroys the handedness that sets the sign. No confidence intervals appear anywhere; angles carry three decimals from 0.8 mm slices; no cohort demographics permit subgroup analysis. External deltoid tuberosity Dice exceeds internal (0.909 vs 0.827), unexplained. Severe deformity was excluded from training. Clinically: n=2, unblinded, no controls, no outcomes, canal alignment and osteotomy level unmeasured, neck-shaft angle fixed at 135 degrees. Equation 1 is wrong as written — with alpha 1.05 and t2 > t1 the upper bound falls below t1, leaving the cortical mask empty or stripped of its densest voxels.

## 4. Editorial Decision

**Reject**, with integrity items 1 to 3 referred first. The core output is unmeasured, the deposited code does not match the described methods, and prospective implantation of custom guides is not covered by the retrospective consent waiver. Elsewhere, **Communications Engineering** fits best in the Nature portfolio after expert-comparison validation; *JSES International* is the realistic home.

**Counterargument.** Expert manual retroversion is a convention with real inter-observer variability, not a truth, and no commercial PSI publishes an auditable version rule; on that reading a fully specified pipeline plus two implantations at roughly one degree of plan-to-execution agreement is a legitimate proof of concept deserving major revision. Variability is a reason to quantify limits of agreement, not to omit the comparison — and the ethics and code findings block acceptance independently.

## 5. Suggested Reviewer Expertise

Approximately seventy percent technical expertise is required. First, single-stage object detection and instance segmentation applied to volumetric CT, specifically slice-wise inference with cross-slice aggregation, and the calibration and confidence-thresholding behaviour of YOLO-family detectors on small medical datasets. Second, computational geometry for orthopaedic surgical planning — anatomical coordinate-frame construction, signed version-angle formulation, curvature-based landmark localisation on cortical contours, and error propagation through chained geometric estimators. Third, computer-aided design and additive manufacturing of patient-specific surgical guides, including Boolean mesh construction, SLM and SLA process tolerances, dimensional-accuracy verification, and sterilisation constraints. Fourth, biostatistics for imaging-based agreement studies: Bland–Altman limits of agreement, intraclass correlation, and confidence-interval estimation for detection metrics in small samples. The remaining thirty percent should be clinical: a shoulder arthroplasty surgeon with direct experience of humeral-side component version, neck-shaft angle selection, osteotomy technique in cuff-tear arthropathy and glenohumeral osteoarthritis, and hands-on use of commercial PSI and 3D planning platforms in elderly patients.

## 6. State-of-the-Art Literature Review (Past Three Years)

Automated humeral-side planning has moved decisively toward validated geometric prediction against expert reference over the past three years, and this manuscript sits outside that trend. The reference work is Spangenberg, Uddin, Habis, Faber and Langohr, *Automatic determination of the resection plane for shoulder arthroplasty in arthritic humeri: a deep learning model* (J Shoulder Elbow Surg 2025;34:e1301–e1309), which trained on 3D humeral models with resection planes digitised along the anatomic neck by two orthopaedic surgeons, and reported mean absolute errors of 1.4 ± 0.7 mm for the plane centroid and 3.9 ± 1.6° for its normal in arthritic humeri, degrading gracefully from 0.3 mm and 3.1° in non-arthritic bone. The same group's earlier Random Forest bicipital groove classifier (Comput Biol Med 2024) addresses the identical landmark this manuscript uses as its canal-entry anchor, is validated specifically in arthritic humeri where osteophytes obscure the groove, and is released open source in the `shoulder` Python package. These two papers are the direct comparators. The manuscript cites the first as reference 32 and the second not at all, and benchmarks against neither. Adjacent to this, Moglia, Marsilio, Cerveri and colleagues (Bioengineering 2026;13:574) reported CEL-UNet and ArthroNet+ on a multicentre cohort of 600 patients with humeral Dice of 0.99, with code publicly released — a useful calibration point for both the segmentation quality and the reproducibility standard now expected in this sub-domain. Garofalo et al. (J Clin Med 2023;12:2620) is also relevant and uncited: they showed that a Blueprint software update alone shifted glenoid version and inclination measurements materially, which is a direct empirical argument for why an unvalidated automated planner should not be trusted on the strength of internal consistency.

On the instrumentation side, the assumption that PSI reliably transfers a plan is contested rather than settled. Lau and Keith (cited here as reference 28) and Berhouet et al. (reference 29) both report that shoulder PSI underdelivers on rotational accuracy, and Lee, Yu, Kim, Jeon and Koh (J Orthop Res 2025;43:1695–1704) recently found with 3D-printed PSI in RTSA that the posterior baseplate screw was abandoned in 93.3% of cases despite preoperative planning — a concrete demonstration that planned geometry and intraoperative reality diverge, and that two successful cases establish very little. Against this landscape, the manuscript's distinctive contribution is real but narrow: it is the only work I identified that carries the chain all the way from axial-slice landmark detection through explicit version, canal-entry and cutting-plane construction to a manufactured, implanted guide, and it is unusually transparent about the geometry. That contribution is undermined by the absence of the one experiment the field now expects — blinded expert comparison with limits of agreement — and by benchmarking against nothing, when an open-source, arthritis-validated competitor for the same landmarks is publicly available.

## 7. Suggested Reviewer Names

**Automated humeral planning and landmark geometry (technical).** Gregory W. Spangenberg, doctoral researcher, Roth McFarlane Hand and Upper Limb Centre, Western University — author of both direct comparators named above; the single most appropriate reviewer for the geometric validation gap. G. Daniel G. Langohr, Associate Professor, Western University — supervising author on the resection-plane and bicipital-groove work. Jacob M. Reeves, Assistant Professor, Western University — computational shoulder biomechanics and humeral morphology.

**Deep learning for musculoskeletal CT (technical).** Luca Marsilio, postdoctoral researcher, Politecnico di Milano — first author on CEL-UNet and ArthroNet+ for shoulder CT. Andrea Moglia, senior researcher, Politecnico di Milano — co-author on the same multicentre shoulder pipeline. Sandro Hodel, Balgrist University Hospital, Zurich — deep learning applied to orthopaedic CT planning.

**Computer-assisted planning and patient-specific guide fabrication (technical).** Philipp Fürnstahl, Associate Professor and head of Research in Orthopedic Computer Science, Balgrist CARD, University of Zurich — originator of the articular margin plane regression approach and long track record in 3D-printed patient-specific guide validation. Lazaros Vlachopoulos, Balgrist University Hospital — computational three-dimensional humeral anatomy measurement.

**Clinical shoulder arthroplasty and humeral component version (clinical).** Jean-David Werthel, Hôpital Ambroise Paré, Paris — humeral component version, biomechanics, and RTSA planning. Jong Pil Yoon, Associate Professor, Kyungpook National University — author of reference 24 on patient-specific guides in RTSA, institutionally independent of the submitting group. Note the exclusion in the integrity alert: Asan Medical Center investigators share the submitting institution's parent university and must not be invited.

---

## Further Literature (Past Three Years, Similar Scope)

**1.** Spangenberg GW, Uddin FZN, Habis AA, Faber KJ, Langohr GDG. Automatic determination of the resection plane for shoulder arthroplasty in arthritic humeri: a deep learning model. *J Shoulder Elbow Surg* 2025;34:e1301–e1309. DOI 10.1016/j.jse.2025.03.010. Peer-reviewed. **Cited** (ref. 32). Independent of the submitting group. The single closest comparator. Predicts the humeral resection plane against two-surgeon digitised ground truth in 62 humeri, reporting 1.4 ± 0.7 mm centroid and 3.9 ± 1.6° normal-vector error in arthritic bone. The manuscript cites it descriptively but never benchmarks against it; this omission alone would sustain rejection.

**2.** Spangenberg GW, Uddin F, Faber KJ, Langohr GDG. Automatic bicipital groove identification in arthritic humeri for preoperative planning: a Random Forest Classifier approach. *Comput Biol Med* 2024;178:108653. DOI 10.1016/j.compbiomed.2024.108653. Peer-reviewed. **Not cited.** Independent. Automates the exact landmark on which the present canal-entry rule depends, validated specifically in osteophytic humeri where the groove is obscured, and released open source in the `shoulder` Python package. Its omission is the most consequential citation gap in the submission, because a validated, freely available alternative to the manuscript's own groove detector exists and is untested against it.

**3.** Satir OB, Eghbali P, Becce F, Goetti P, Meylan A, Rothenbühler K, Diot R, Terrier A, Büchler P. Automatic quantification of scapular and glenoid morphology from CT scans using deep learning. *Eur J Radiol* 2024;177:111588. DOI 10.1016/j.ejrad.2024.111588. Peer-reviewed, open access. **Not cited.** Independent. Establishes the methodological template the present work should have followed: deep-learning landmark localisation feeding an explicit anatomical coordinate system, with automatic measurements compared against a musculoskeletal radiologist, landmark error reported in millimetres, R² per parameter, and 95% confidence intervals on the paired differences. Code released on a public GitLab. This is what validated geometric derivation looks like.

**4.** Moglia A, Marsilio L, Rossi M, Manzotti A, Mainardi L, Cerveri P. Quantifying the contribution of bone morphology to implant selection in shoulder arthroplasty using CT-based deep learning. *Bioengineering* 2026;13:574. DOI 10.3390/bioengineering13050574. Peer-reviewed. **Not cited.** Independent. CEL-UNet plus the multi-task ArthroNet+ on a multicentre cohort of 600 patients, with humeral Dice of 0.99 and public code release. Sets the current expectation for cohort scale, multicentre design, and reproducibility in shoulder-arthroplasty deep learning, against which a 330-patient single-institution training set with an unmatched repository compares poorly.

**5.** Lee W, Yu W, Lee H, Kim GB, Jeon I-H, Koh KH. Evaluation of the baseplate position and screws in reverse total shoulder arthroplasty using 3D printed patient-specific instrumentation. *J Orthop Res* 2025;43:1695–1704. DOI 10.1002/jor.70023. Peer-reviewed. **Not cited.** *Institutional caution: the senior authors are at Asan Medical Center, University of Ulsan College of Medicine — the submitting institution's parent university. Cite, but do not invite as reviewers.* Demonstrates empirically that planned geometry and intraoperative reality diverge: the posterior baseplate screw was abandoned in 93.3% of cases despite preoperative planning. Directly undercuts any inference from two uncomplicated cases.

**6.** Garofalo R, Fontanarosa A, Castagna A, Lassandro N, Del Buono A, De Crescenzo A. Can we completely trust in automated software for preoperative planning of shoulder arthroplasty? Software update may modify glenoid version, glenoid inclination and humeral head subluxation values. *J Clin Med* 2023;12:2620. DOI 10.3390/jcm12072620. Peer-reviewed. **Not cited.** Independent. Showed that a Blueprint software update alone shifted glenoid measurements materially across 76 CT scans. The strongest available empirical argument that an automated planner cannot be trusted on internal consistency without external ground truth — precisely the manuscript's position.

**7.** Zhao Q, Feng Q, Zhang J, Xu J, Wu Z, Huang C, Yuan H. Glenoid segmentation from computed tomography scans based on a 2-stage deep learning model for glenoid bone loss evaluation. *J Shoulder Elbow Surg* 2023;32:e624–e635. DOI 10.1016/j.jse.2023.05.036. Peer-reviewed. **Not cited.** Independent. A 485-patient two-stage segmentation-then-geometry pipeline for shoulder CT. Relevant as a scale and design comparator: same architecture philosophy, an order of magnitude more patients, and quantitative agreement analysis against manual measurement.

**8.** Wigmore E, et al. Clinical accuracy of humeral and glenoid component placement in total shoulder arthroplasty using ASTRA patient-specific guides. *JSES Int* 2025;9:2127–2140. DOI 10.1016/j.jseint.2025.08.007. Peer-reviewed. **Cited** (ref. 25). Independent. The nearest clinical comparator for humeral-side PSI accuracy in a real patient series. The manuscript cites it in passing but does not position its own two-case deviations against this series' reported accuracy distribution, which it must.

**9.** Song HS, Lee S-U, Kim H. Advancing precision in shoulder arthroplasty: patient-specific instrumentation, navigation, and emerging technologies. *Clin Orthop Surg* 2025;17:727–739. DOI 10.4055/cios25021. Peer-reviewed review. **Cited** (ref. 26). Independent. Useful as the current synthesis of where PSI, navigation, and mixed reality stand, and for its treatment of why PSI adoption has stalled despite favourable in-vitro accuracy — context the Discussion largely elides.

**10.** Can Kolac UC, Paksoy A, Akgün D. Three-dimensional planning, navigation, patient-specific instrumentation and mixed reality in shoulder arthroplasty: a digital orthopedic renaissance. *EFORT Open Rev* 2024;9:517–527. DOI 10.1530/EOR-23-0200. Peer-reviewed review, open access. **Cited** (ref. 31). Independent. The most current European review of the digital shoulder-planning landscape, and the appropriate frame for the manuscript's claim of novelty in humeral-side automation.

**Note on preprints.** One arXiv-only item is worth the authors' attention but was deliberately excluded from the numbered list above because it has not been peer-reviewed: *Fully automated deep learning based glenoid bone loss measurement and severity stratification on 3D CT in shoulder instability* (arXiv:2511.14083). It is methodologically parallel — segmentation, landmark detection, then geometric fitting — and reports automated-versus-consensus ICC alongside surgeon-to-surgeon ICC, which is exactly the agreement framing the present manuscript needs. **Unreviewed preprint; treat as a design template rather than as evidence.**

073475
# Editorial Report — Manuscript 073475

**Title:** Repair gain prediction enables selective correction of medical segmentation foundation models
**Corresponding authors:** Yong Xia, Guoyan Liu, Xiaoyu Yang, Shuzhen Xu
**Handling editor:** Yuli — *Nature Communications*, Digital Health

---

## Editorial Integrity Alert (confidential — not for authors)

Four items require the handling editor's attention.

First, the archived code DOI (10.5281/zenodo.22293534) could not be resolved during independent verification. The record may be under embargo, but it must be confirmed as live before any decision letter is sent, because the Code Availability statement asserts public availability in the present tense while the Data Availability statement uses the future tense ("will be archived"). Reproducibility claims resting on an unresolvable identifier should not be accepted on assertion.

Second, three references appear in the bibliography but nowhere in the visible citation stream: Riquelme et al. on sparse mixture-of-experts (ref. 19), Wang et al. on Tent (ref. 20) and Niu et al. on efficient test-time adaptation (ref. 21). Reference 19 in particular has no topical connection to this manuscript. Uncited and off-topic references inflate the apparent breadth of engagement with the field and should be queried.

Third, the corresponding-author configuration is unusual. Four corresponding authors are listed across seven affiliations spanning vascular surgery, obstetrics and gynaecology, gastrointestinal surgery, public health and a traditional Chinese medicine hospital, with no identifiable medical image computing laboratory. The name "Yong Xia" coincides with a prominent medical image analysis researcher at Northwestern Polytechnical University; the email domain here is Fujian Medical University and the listed affiliation is Obstetrics and Gynaecology. This is most likely name coincidence, but the editor should confirm identity before reviewer selection to avoid conflict-of-interest errors. Competing interests are declared as none.

Fourth, no preprint of this work was located, so no undisclosed-preprint concern arises. No evidence of cohort overlap or salami-slicing was found; all cohorts are public benchmarks.

---

## 1. Overall Assessment

ReGain estimates segmentation reliability without a reference mask, predicts the Dice gain expected from each of five repair actions, routes each case to the highest cost-adjusted utility action, and re-evaluates the result before automatic acceptance. On MedSAM across MSD Liver, MSD Pancreas, KiTS23 and AMOS22, Dice rises from 0.823 to 0.863 and severe failures fall from 15.4% to 7.3%. The framing is sensible and the evaluation careful, but the paper repairs a weak segmenter without ever comparing against nnU-Net, and never reports the segmentation-instance count that every percentage depends on.

## 2. Strengths

Partitioning is patient-level with patient-clustered bootstrap intervals, and the inference-time box prompt comes from an independently trained frozen localizer rather than the held-out mask, avoiding the ground-truth-prompt inflation common in MedSAM evaluations. Generalization spans TotalSegmentator, PROMISE12, ACDC, a held-out anatomy and a MedSAM2 backbone, with external AUROC degradation from 0.901 to 0.851 disclosed rather than buried. The explicit no-intervention action is a genuine contribution: every active repair carries negative mean gain on reliable masks, and the negative-intervention rate of 6.2% against 22.9% for confidence routing quantifies over-correction as a safety endpoint.

## 3. Weaknesses

The missing nnU-Net baseline is decisive; without it, a reliability layer cannot be distinguished from partial recovery of accuracy sacrificed to a promptable backbone. The retrospective oracle takes the per-instance maximum of five noisy gains and is therefore upward-biased, so the claim of recovering 71% of available improvement rests on an inflated denominator; cross-fitted estimation is required. Reported quantities do not reconcile: the two named strata imply a baseline of 0.851 and a gain of 0.028 rather than 0.823 and 0.040, and 5.3% risk at 80% coverage contradicts 71% capture at a 20% budget, which implies 2.6%. No subgroup analysis by sex, age, vendor or site appears, there is no reader study or downstream endpoint, and the utility function's cost weights are never given.

## 4. Editorial Decision

**Reject**, with transfer offered to **Communications Engineering**, or **Communications Medicine** with clinically anchored endpoints. The untested deployment premise, oracle inflation and unreported denominators affect headline claims and cannot be adjudicated by reviewers on the present data. The strongest counterargument is that ReGain answers what the failure-detection literature does not — what to do after rejection — and the negative-intervention result is demonstrated across two backbones, three external cohorts and an unseen anatomy. An editor could reasonably treat the omissions as major revisions and send it out; I do not, because the missing control could invert the framing rather than refine it.

## 5. Suggested Reviewer Expertise

Reviewers should cover, first, failure detection and segmentation quality estimation without reference masks, specifically confidence aggregation, risk-coverage analysis and calibration under distribution shift; second, promptable segmentation foundation models for medical imaging, including MedSAM and SAM 2 adaptation, box-prompt sensitivity and automatic prompt generation; third, learned refinement and interactive-correction policies, including reinforcement-learning prompting agents, since this is the literature the manuscript most closely resembles and least engages; fourth, evaluation methodology and metric selection for biomedical image analysis, including clustered inference when multiple instances arise per patient. Clinical expertise should cover abdominal CT organ and tumour contouring in a radiotherapy or surgical-planning workflow, where automated contour quality assurance and human review budgets are operational realities, and multi-vendor cardiac or prostate MRI segmentation for the external cohorts.

## 6. State-of-the-Art Literature Review (Past Three Years)

The relevant landscape has three strands, and the manuscript engages fully with only one. Failure detection and quality estimation without ground truth has matured from reverse classification accuracy into systematic benchmarking; Zenk et al. (Medical Image Analysis 101, 103392, 2025) established confidence aggregation as the dominant design axis and argued for risk-coverage analysis as the appropriate evaluation, and Maier-Hein et al. and Reinke et al. (Nature Methods 21, 2024) set the metric-selection standard. The manuscript cites all three and its evaluation design visibly follows them. Promptable medical segmentation is the second strand: MedSAM (Nature Communications 15, 654, 2024), MedSAM2, SAM 2, VISTA3D and MedicoSAM, alongside robustness work on box-prompt quality such as RoBox-SAM. The manuscript cites this strand adequately and its use of an independent localizer rather than ground-truth boxes places it on the correct side of a known evaluation pitfall.

The third strand is where the manuscript is deficient, and it bears directly on the novelty claim. A substantial recent literature already learns policies over corrective actions for SAM-family segmenters: AlignSAM formulates automatic prompting as reinforcement learning over a frozen backbone; temporally-extended prompt optimization treats interactive medical segmentation as sequential decision-making; RFMedSAM 2 performs automatic prompt refinement for SAM 2; and MedSAM-Agent (2026) casts interactive medical segmentation as multi-turn agentic decision-making with process-level supervision. Marinov et al.'s taxonomy of deep interactive medical segmentation surveys the broader space. None of these appear in the reference list. ReGain is, in decision-theoretic terms, a one-step contextual bandit with a hand-designed five-action bank and offline gain supervision, which is a simplification of, not an alternative to, these sequential formulations. The authors must engage this work directly, argue why single-step gain regression is preferable to a learned sequential policy — the cost and calibration arguments are available to them and are reasonable — and where feasible benchmark against at least one learned prompting policy. As it stands, the claim that existing methods "do not directly determine which corrective intervention is likely to improve a particular failed prediction" is not accurate as written.

## 7. Suggested Reviewer Names

For failure detection and quality estimation: Maximilian Zenk (German Cancer Research Center), first author of the confidence-aggregation failure-detection benchmark that this manuscript's evaluation design most closely follows; Kim-Celine Kahl (German Cancer Research Center), whose work on uncertainty estimation and downstream failure detection covers the reliability-head design directly; and Bella Specktor-Fadida (Hebrew University of Jerusalem), lead author of SegQC, a multi-metric segmentation quality control and error-detection framework.

For promptable segmentation foundation models: Jun Ma (University of Toronto), lead author of MedSAM and MedSAM2, both of which are the backbones evaluated here — note that his position as the direct author of the systems being corrected is a competing-interest consideration the editor should weigh; Anwai Archit or Constantin Pape (University of Göttingen), authors of MedicoSAM, an evaluation of what does and does not transfer when SAM is adapted to medical images; and Fabian Isensee (German Cancer Research Center), who is the appropriate person to adjudicate the missing nnU-Net comparison.

For learned refinement and interactive-correction policies: Zdravko Marinov (Karlsruhe Institute of Technology), author of the systematic review and taxonomy of deep interactive medical image segmentation; Hussein Mozannar (Massachusetts Institute of Technology), author of the consistent learning-to-defer estimators the manuscript cites and builds its deferral stage on; and Karol Gotkowski (German Cancer Research Center), whose work on interactive 3D segmentation evaluation addresses exactly the prompt-protocol confounds at issue here.

For clinical and evaluation-methodology assessment: Jan Wasserthal (University Hospital Basel), radiologist and lead author of TotalSegmentator, which supplies the external CT cohort and who can judge the operational realism of the review-budget analysis; Annika Reinke (German Cancer Research Center), co-author of Metrics Reloaded and the appropriate reviewer for the instance-level denominator and clustered-inference concerns; and Anindo Saha (Radboud University Medical Center) for the prostate MRI external cohort and multi-reader evaluation design.

Reviewer affiliations reflect the most recent public information located and should be confirmed at invitation. Seniority skews toward postdoctoral and group-leader level as requested, with the exception of Wasserthal and Isensee, whose specific expertise is not readily substitutable.

## Further Literature

The following are the works most directly comparable in scope, ordered by how directly they bear on the manuscript's claims. Peer-review status and citation status in the submitted manuscript are stated for each. Peer-reviewed publications are prioritized; arXiv-only entries are flagged as unreviewed.

1. Zenk, M., Zimmerer, D., Isensee, F., Traub, J., Norajitra, T., Jäger, P. F. & Maier-Hein, K. H. Comparative benchmarking of failure detection methods in medical image segmentation: unveiling the role of confidence aggregation. *Medical Image Analysis* **101**, 103392 (2025). DOI: 10.1016/j.media.2024.103392. Peer-reviewed. Cited (ref. 9). Independent of the submitting group. This is the benchmark the manuscript's reliability evaluation follows, including the risk-coverage framing; the authors should state explicitly whether their reliability head outperforms the pairwise-Dice ensemble baseline identified there as robust.

2. Marinov, Z., Jäger, P. F., Egger, J., Kleesiek, J. & Stiefelhagen, R. Deep interactive segmentation of medical images: a systematic review and taxonomy. *IEEE Transactions on Pattern Analysis and Machine Intelligence* **46**, 10998–11018 (2024). DOI: 10.1109/TPAMI.2024.3452629. Peer-reviewed. Not cited. Independent. Surveys 121 interactive medical segmentation methods and documents the absence of standardized baselines; the manuscript's action bank is a subset of this taxonomy and should be positioned within it.

3. Isensee, F., Wald, T., Ulrich, C., Baumgartner, M., Roy, S., Maier-Hein, K. & Jäger, P. F. nnU-Net revisited: a call for rigorous validation in 3D medical image segmentation. *MICCAI 2024*, LNCS **15009**, 488–498 (2024). DOI: 10.1007/978-3-031-72114-4_47. Peer-reviewed. Not cited. Independent. Directly addresses the manuscript's central omission, showing that claimed advances over a properly configured U-Net frequently fail under adequate baselines. This is the paper an unsympathetic reviewer will cite first.

4. Isensee, F., Rokuss, M., Krämer, L., Dinkelacker, S., Ravindran, A., Stritzke, F., Hamm, B., Wald, T., Langenberg, M., Ulrich, C., Deissler, J., Floca, R. & Maier-Hein, K. nnInteractive: redefining 3D promptable segmentation. arXiv:2503.08373 (2025). DOI: 10.48550/arXiv.2503.08373. **arXiv preprint — not peer-reviewed.** Not cited. Independent. Volumetric open-set promptable segmentation trained on 120+ datasets, integrated into Napari and MITK. Its existence weakens the manuscript's premise that a 2D promptable backbone with slice-level repair is the natural deployment configuration.

5. Wu, J., Wang, Z., Hong, M., Ji, W., Fu, H., Xu, Y., Xu, M. & Jin, Y. Medical SAM Adapter: adapting Segment Anything Model for medical image segmentation. *Medical Image Analysis* **102**, 103547 (2025). DOI: 10.1016/j.media.2025.103547. Peer-reviewed. Cited, but as an arXiv preprint (ref. 3). Independent. The citation must be updated to the journal version; citing a 2023 preprint for a 2025 journal article is a reference-hygiene error the copy-editing stage will catch.

6. Du, Y., Bai, F., Huang, T. & Zhao, B. SegVol: universal and interactive volumetric medical image segmentation. *Advances in Neural Information Processing Systems* **37**, 110746–110783 (2024). Peer-reviewed. Not cited. Independent. A volumetric interactive alternative to the MedSAM/MedSAM2 backbones evaluated here, and a fairer comparator for the volumetric-repair action than a 2.5D residual module.

7. Kahl, K.-C., Lüth, C. T., Zenk, M., Maier-Hein, K. & Jäger, P. F. ValUES: a framework for systematic validation of uncertainty estimation in semantic segmentation. arXiv:2401.08501 (2024). DOI: 10.48550/arXiv.2401.08501. **Preprint record; a peer-reviewed conference version exists and the venue should be confirmed before citation.** Not cited. Independent. Directly relevant to the manuscript's claim that uncertainty and probability statistics dominate its ablation.

8. Huang, Y. et al. Robust box prompt based SAM for medical image segmentation. arXiv:2407.21284 (2024). **arXiv preprint — not peer-reviewed.** Cited (ref. 32). Independent. Already performs box-prompt refinement, which overlaps substantially with the manuscript's A1 prompt-repair action; the distinction between learned prompt refinement and predicted prompt-repair gain needs an explicit statement.

9. Sun, R. et al. AlignSAM: aligning Segment Anything Model to open context via reinforcement learning. arXiv:2406.00480 (2024). **Preprint record; a CVPR 2024 version is reported and the venue and author list should be confirmed before citation.** Not cited. Independent. Formulates prompting as a reinforcement-learning policy over a frozen backbone — the sequential generalization of the manuscript's one-step router.

10. MedSAM-Agent: empowering interactive medical image segmentation with multi-turn agentic reinforcement learning. arXiv:2602.03320 (2026). **arXiv preprint — not peer-reviewed; author list not independently confirmed and must be verified before citation.** Not cited. Independent. Casts interactive medical segmentation as multi-turn decision-making with process-level supervision, which is the closest published formulation to ReGain and the one against which its single-step design must be justified.

071193
# Editorial Report: RADx — Anatomically Structured and Uncertainty-Aware AI Framework for Radiographic RA Assessment

## 1. Overall Assessment

The manuscript presents RADx, a modular pipeline built on HandXFM, a DINOv3-based hand-radiograph foundation model, that performs joint detection (DETR-style), binary abnormality classification, and ordinal severity regression for Sharp–van der Heijde (SvH) erosion and joint space narrowing (JSN) scores at joint, unilateral-hand, and bilateral-hand levels, evaluated on the CATCH cohort (533 participants, 1,405 radiographs with SvH annotation) with conformal-prediction uncertainty quantification and a deployed web interface.

The work is competently engineered but does not clear the bar of a substantial, reproducible advance. A directly comparable and more complete system, autoscoRA (Deimel et al., *Arthritis & Rheumatology*, 2026), already exists in the literature, trained on 769 patients and 12,144 radiographs of both hands and feet, reporting ICC 0.9 agreement with expert SvH scores — substantially stronger than RADx's joint-level PCC of 0.748 (erosion) and 0.816 (JSN). RADx neither cites nor benchmarks against this system, and the SvH implementation it does offer is narrower than the formal protocol. Combined with single-cohort validation and an unresolved self-citation gap, these issues are not correctable through minor revision.

## 2. Strengths

The three-tier anatomical hierarchy (joint, unilateral-hand, bilateral-hand) built on a shared HandXFM backbone is a coherent architectural contribution, and the two-stage zero-inflation-aware modeling (binary presence gate followed by CORAL-style ordinal regression) is a defensible response to the extreme class imbalance documented in Fig. 1B–D.

The conformal prediction implementation is methodologically sound, applying split conformal calibration separately to detection (box inflation), classification, and regression, with joint-type-conditional calibration exposing genuine anatomical heterogeneity in uncertainty (Fig. 3B–D, 5C).

Patient-level 80:10:10 splitting shared across tasks, and strict exclusion of CATCH data from HandXFM pretraining, are appropriate safeguards against information leakage.

## 3. Weaknesses

Validation is confined to a single center's cohort with no external test set; the manuscript's own Discussion concedes this, but a concession is not evidence, and it is precisely the failure mode this journal's bar is designed to exclude.

The SvH implementation is materially incomplete relative to the formal protocol: JSN is restricted to MCP/PIP joints only, wrist erosion uses a composite region rather than individual carpal articulations, and feet are excluded entirely, yet the title and abstract present RADx as a general solution for radiographic RA assessment without this qualification until deep in the Discussion.

HandXFM's pretraining corpus (~25,000 curated images, 6,130 with joint annotations) is two orders of magnitude smaller than SKELEX (Kim et al., Seoul National University, 1.29M MSK radiographs), a directly competing musculoskeletal foundation model published in the same window; no comparison or citation is offered, and the claim of HandXFM being "developed in our prior work" carries no traceable reference anywhere in the bibliography.

Given autoscoRA's markedly higher agreement (ICC 0.9) on a larger, dual-extremity cohort using the complete SvH protocol, RADx's central quantitative claims of state-of-the-art performance are not defensible as written.

## 4. Editorial Decision

**Reject.** The combination of an unaddressed, superior direct competitor (autoscoRA), single-site validation, a simplified SvH protocol presented without qualification in the abstract, and an uncited foundation-model precursor constitutes a compounding set of flaws rather than an isolated fixable weakness; the paper does not represent a distinctive advance over the current state of the art and should not proceed to review at this title.

## 5. Suggested Reviewer Expertise

Not applicable given the rejection decision; should the authors resubmit elsewhere, reviewers would need expertise in DETR-based anatomical detection, self-supervised foundation-model pretraining for radiographs, conformal prediction for clinical regression/detection, ordinal regression under severe class imbalance, and rheumatology with direct SvH-scoring experience.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Automated SvH scoring has advanced quickly: Honda et al. (*Rheumatology*, 2023) established clinically applied CNN scoring; Moradmand & Ren (*Sci Rep*, 2025) proposed multistage Overall Sharp Score prediction with external testing on 291 patients; Lien et al. (*J Med Biol Eng*, 2025) added attention-based joint localization; and autoscoRA (Deimel et al., 2026) is now the field's strongest validated system, covering both hands and feet at ICC 0.9. In parallel, MSK foundation modeling has moved to million-scale corpora (SKELEX, 1.29M images), and conformal landmark localization (M-R2CCP, arXiv 2503.14106) already covers detection-uncertainty ground RADx claims as novel. RADx's multi-scale representation is organizationally interesting but does not advance scoring accuracy or scale beyond this existing body of work, and fails to engage with the two most relevant competing papers.

## 7. Suggested Reviewers

Not applicable — manuscript recommended for desk rejection.




