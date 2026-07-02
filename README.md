# Trackrad202512456

050239
Cumulative Conceptual Drift Limits the Clinical Reliability of Large Language Models
## Editorial Report — Condensed (Sections 1–4, ~300 words)

**1. Overall Assessment.** The manuscript reports that eight flagship LLMs generate fluent, clinically plausible medical descriptions from standardized concepts (96% CTD pass) but fail to reliably recover those concepts from their own descriptions (39% DTC pass, κ=0.057), and that this instability compounds across five rounds of paraphrasing, with interventions only partially restoring fidelity. The CTD/DTC asymmetry and the layer-wise finding that corrections shift only terminal-layer output determinism, not mid-layer semantic integration, is a genuinely distinctive, mechanistically grounded contribution.

**2–3. Strengths and Weaknesses.** Strengths: the reversibility design tests a falsifiable cognitive hypothesis rather than measuring accuracy alone; the sanitized iterative-paraphrasing chain is a credible multi-turn handover proxy; the hidden-state analysis on Qwen2.5/Llama grounds behavioral drift in representational mechanism. Weaknesses: multi-round DTC scoring uses exact string matching against a standard dictionary, conflating valid synonym use with genuine conceptual loss; the corpus originates from Chinese-language sources mapped to English-facing ontologies, and prompt/generation language is unspecified, leaving translation ambiguity as an uncontrolled confound; the study is confined to one specialty (neurology/neurosurgery) with no cross-specialty or cross-language replication; and paraphrasing temperature (0.7) versus CTD/DTC temperature (0.0) is not disentangled from true drift, weakening the causal "cumulative instability" claim.

**4. Editorial Decision.** **Send for Review.** The behavioral and mechanistic findings clear the bar for scrutiny, but reviewers must adjudicate three points before any acceptance: (1) whether exact-match DTC scoring is defensible or requires semantic-equivalence rescoring; (2) whether the Chinese-language corpus provenance confounds the drift findings, independent of genuine conceptual instability; (3) whether temperature-driven stochasticity in the paraphrasing task has been adequately separated from representational drift.

---

## 5. Suggested Reviewer Expertise
*(unchanged)*

Reviewers should have expertise in: mechanistic interpretability of transformer hidden states and logit-lens analysis; clinical NLP concept normalization against UMLS/SNOMED CT; LLM hallucination detection via semantic entropy or self-consistency methods; multilingual/cross-lingual LLM evaluation; and clinical neurology or neurosurgery with experience in diagnostic handover and documentation workflows.

## 6. State-of-the-Art Literature Review (Past 3 Years)
*(unchanged)*

Recent work has approached LLM medical instability from adjacent but distinct angles: DriftMedQA (2025) modeled *temporal* guideline drift rather than *conceptual* drift within a single interaction, finding RAG plus preference optimization partially mitigates outdated recommendations and revealed LLM limitations in reconciling conflicting medical knowledge, highlighting gaps in clinical readiness. Farquhar et al. (Nature, 2024, already cited as ref. 56) established semantic entropy as a hallucination-detection tool, which this manuscript could have used as an alternative to exact-match scoring. Bedi et al. (JAMA Network Open, 2025) showed LLMs suffer significant accuracy drops under answer-choice perturbation, challenging claims of artificial intelligence's readiness for autonomous clinical deployment, reinforcing this manuscript's pattern-matching-versus-cognition framing but via a different (MCQA robustness) paradigm. This manuscript's distinctive advance is treating concept fidelity as a bidirectional, multi-round property rather than a static robustness or temporal-currency question; it should engage explicitly with DriftMedQA and semantic-entropy methods as competing operationalizations of "drift."

## Suggested Reviewer Names
*(unchanged)*

**Interpretability:** Neel Nanda; Kenneth Li; Yonatan Belinkov.
**Clinical NLP/concept normalization:** Emily Alsentzer; Noémie Elhadad; Hyeju Jang.
**Hallucination/uncertainty in medical LLMs:** Sebastian Farquhar; Karan Singhal; Stephen Pfohl.
**Clinical (neurology/neurosurgery informatics):** Christopher Chen; a practicing neurohospitalist or neurosurgical informatics lead with clinical-handover research experience.

---

## Further Literature (5 papers, past 3 years, same scope)

1. **McCoy AB, Manrai AK, Rodman A.** Large Language Models and the Degradation of the Medical Record. *N Engl J Med.* 2024. DOI: 10.1056/NEJMp2405999. Peer-reviewed perspective. Directly anticipates this manuscript's central thesis — that fluent LLM-generated documentation silently erodes the precision of medical concepts required for downstream care — but argues from clinical-workflow observation rather than the quantitative CTD/DTC reversibility metric this manuscript introduces. Should be cited as prior conceptual grounding for the "clinically consequential drift" claim in the Discussion.

2. **Bedi S, Jiang Y, Chung P, Koyejo S, Shah NH.** Fidelity of Medical Reasoning in Large Language Models. *JAMA Netw Open.* 2025;8(8):e2526021. DOI: 10.1001/jamanetworkopen.2025.26021. Peer-reviewed. Uses a "none of the above" answer-choice perturbation to show LLM medical benchmark performance reflects pattern matching over reasoning — an input-perturbation robustness test complementary to this manuscript's generation-based reversibility test. Both converge on shallow conceptual grounding but via non-overlapping methodologies; the manuscript should distinguish "reasoning fidelity" (Bedi) from "concept-semantic fidelity" (this paper) explicitly, as reviewers will likely conflate the two.

3. **Ben Shoham O, Rappoport N.** MedConceptsQA: Open source medical concepts QA benchmark. *Comput Biol Med.* 2024;182:109089. DOI: 10.1016/j.compbiomed.2024.109089. Peer-reviewed. A static QA benchmark testing LLM understanding of ICD/SNOMED concept codes at varying difficulty. Directly overlapping scope (medical concept understanding against standardized ontologies) but measures single-turn recognition accuracy, not bidirectional generation-recovery reversibility or iterative drift — the manuscript should cite this as the closest existing static baseline it improves upon dynamically.

4. **Wu W, et al.** Assessing and Mitigating Medical Knowledge Drift and Conflicts in Large Language Models. *arXiv:2505.07968*, 2025. **Unreviewed preprint — flag accordingly.** Introduces DriftMedQA to test LLM handling of *evolving clinical guidelines* (temporal drift), combining RAG and DPO as mitigation, paralleling this manuscript's proactive/post-hoc intervention comparison. Key distinction: DriftMedQA drift is externally caused (guidelines changed); this manuscript's drift is internally generated (paraphrasing alone). The manuscript should clarify this is a different drift mechanism, not a replication.

5. **Laban P, Hayashi H, Zhou Y, Neville J.** LLMs Get Lost in Multi-Turn Conversation. *arXiv:2505.06120*, 2025. **Unreviewed preprint — flag accordingly.** General-domain (non-medical) finding that LLMs premature-commit to assumptions early in multi-turn dialogue and then anchor on them, causing compounding errors — mechanistically analogous to this manuscript's "limited spontaneous correction" finding in iterative paraphrasing (Fig. 3D, S6). Strengthens the generalizability argument that conceptual drift is a broader multi-turn LLM failure mode, not medical-domain-specific; worth citing to preempt reviewer skepticism that the phenomenon is an artifact of the medical corpus design.

051810
# Editorial Report: "A bilingual AI audiologist built through reflective playbooks outperforms human audiologists in blinded evaluation" (Condensed)

## 1. Overall Assessment

The manuscript claims a GPT-5 agent, adapted purely through in-context "reflective playbook" induction from 73 training cases, outperforms practising audiologists on all 58 blinded evaluation cases (Δ = +1.35, Cohen's d = 1.84). The component ablation crediting playbook induction over RAG and tool access is a genuine contribution to the experiential-agent literature. But the same 21-item rubric generated the training reward signal and scored the human comparison — a circularity that undermines the headline claim.

## 2. Strengths

The evaluation design is rigorous: four blinded raters, matched patient-simulator instances per case, Benjamini–Hochberg-corrected item tests, and leave-one-rater-out sensitivity analyses all converge (d range 1.39–1.93). The ablation isolating reflective playbook induction as the dominant driver — not multimodal tools, not RAG — is a real mechanistic finding. Bilingual coverage (30 Chinese, 28 English cases) surfaces a genuine transfer asymmetry rarely tested elsewhere.

## 3. Weaknesses

The rubric circularity is fatal: the automated evaluator that shaped the playbook is the same instrument used to score humans, and the item-level gains track almost exactly the behaviours the playbook was built to produce. No real patients appear anywhere — training and evaluation both used an LLM-simulated patient, against which the AI had 73 cases of practice the human comparators never had, confounding format familiarity with clinical skill. The ablation's automated evaluator (Gemini 3.1 Pro) was never validated against human raters. Three authors are Orka Labs employees, and code, case materials, and transcripts are withheld — blocking independent replication.

## 4. Editorial Decision

**Reject.** The central claim rests on a circular evaluation instrument in a fully simulated environment with no independently reproducible materials — a non-revisable structural flaw at this bar, not a scope issue.

---

## 5. Suggested Reviewer Expertise

Reviewers should cover: reflective and experiential in-context learning agent architectures (Reflexion/ExpeL-style rule induction without parameter updates); multimodal vision-language grounding for clinical image interpretation; LLM-versus-clinician blinded comparative evaluation methodology, including circularity and reward-instrument bias in rubric-trained agents; retrieval-augmented generation design and evaluation in healthcare settings; and clinical audiology practice, specifically adult/paediatric audiometric interpretation and patient-centred audiological counselling.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The dominant precedent is Google's AMIE line of work: a large language model system optimized for diagnostic dialogue that outperformed primary care physicians across most evaluated axes in a randomized, double-blind crossover OSCE study, later extended to multi-visit management reasoning grounded in clinical guidelines via long-context retrieval. AMIE relied on large-scale self-play training infrastructure; this manuscript's contribution is to ask whether a comparable specialist-consultation advantage is achievable through sparse, parameter-free reflective rule induction instead — a legitimate and underexplored question, positioned against the broader 2025–2026 experiential-agent literature (ExpeL, AutoGuide, Experiential Reflective Learning) that this manuscript does not engage with directly despite methodological overlap.

Within audiology specifically, recent work has been considerably more cautious: a multicenter blinded evaluation of eight LLMs interpreting pure-tone audiogram reports found diagnostic accuracy well below professional audiologists, concluding current general-purpose models are unsuitable for independent clinical diagnosis despite auxiliary value, and a comparative study of ChatGPT-5.0 and Gemini 2.5 on audiogram interpretation similarly concluded these models are not suitable as standalone diagnostic tools but may serve as adjuncts in primary care and telehealth. The manuscript's substantially stronger claim — categorical superiority over human specialists across nearly the entire rubric — is not engaged against this more cautious contemporaneous audiology-specific literature, and that omission should be raised explicitly with the authors.

## 7. Suggested Reviewers' Names

Reflective/experiential agent architecture: Noah Shinn, Andrew Zhao, Karthik Narasimhan.

Multimodal clinical image interpretation: Pranav Rajpurkar, Eric J. Topol, Ceren Karaçaylı.

Conversational diagnostic AI evaluation methodology: Tao Tu.

Clinical audiology practice: L. Turton.

Retrieval-augmented generation methodology: Patrick Lewis.

---

## Further Literature

1. Liang, J., Xing, M., Xiang, P. et al. A multicenter multifunctional assessment of large language models in pure-tone audiogram interpretation for patients. *npj Digit. Med.* 9, 348 (2026). DOI: 10.1038/s41746-026-02537-1. Blinded, multicenter evaluation of eight LLMs on 140 real audiogram reports found even the best model (DeepSeek-V3) reached only 67% severity accuracy and 54% type accuracy against professional audiologists — directly contradicts this manuscript's implicit claim that LLM-based audiological reasoning can exceed specialist accuracy, and uses real patient data rather than a simulated environment.

2. Tu, T. et al. Towards conversational AI for disease management. *Nature* (2026). DOI: 10.1038/s41586-026-10764-5. Extends AMIE to multi-visit management reasoning grounded in clinical guidelines and drug formularies via long-context retrieval, evaluated against 21 primary care physicians in a blinded virtual OSCE. Architecturally closer to this manuscript's RAG-plus-agent design than the original AMIE paper, yet not cited or engaged.

3. Systematic review and meta-analysis of human–LLM collaboration in clinical medicine. *npj Digit. Med.* 9, 195 (2026). DOI: 10.1038/s41746-026-02382-2. (First author not independently confirmed from available metadata — flagged.) Pooled across ten peer-reviewed clinical studies, diagnostic/interpretation accuracy gains from LLM assistance were statistically imprecise (RR 1.59, 95% CI 0.08–32.74) with prediction intervals crossing the null. Directly relevant field-level counter-evidence to this manuscript's d = 1.84 effect size; the discrepancy warrants explicit discussion.

4. Allard, M.-A., Teinturier, A., Xing, V. & Viaud, G. Experiential Reflective Learning for Self-Improving LLM Agents. arXiv:2603.24639 (2026). **Unreviewed preprint.** Directly competing reflective-heuristic architecture (selective retrieval of accumulated heuristics vs. this manuscript's three-tier backlog/staging/core playbook); the manuscript should engage with this contemporaneous parallel design rather than treating its playbook mechanism as sui generis.

5. Fu, Y., Kim, D.-K., Kim, J., Sohn, S., Logeswaran, L., Bae, K. & Lee, H. AutoGuide: Automated Generation and Selection of Context-Aware Guidelines for Large Language Model Agents. *Adv. Neural Inf. Process. Syst.* 37, 119919–119948 (2024). Competing context-engineering approach generating guidelines from contrasting paired trajectories with per-turn retrieval; offers a direct methodological alternative to the reflect-curate-prune pipeline this manuscript proposes and is not discussed.

6. Karaçaylı, C., Tahir, E. & Altuntaş, E. E. Diagnostic interpretation of pure tone audiograms by multimodal LLMs: a comparative study of ChatGPT-5.0 and Gemini 2.5. *Eur. Arch. Otorhinolaryngol.* 283, 2227–2236 (2026). DOI: 10.1007/s00405-025-09932-6. (Already cited by the authors as ref. 15, flagged here for emphasis.) Concludes multimodal LLMs are not suitable as standalone diagnostic tools for audiogram interpretation — a conclusion in direct tension with this manuscript's claim of categorical superiority over human specialists, and worth pressing the authors on explicitly rather than leaving as a passing citation.

052204
# Editorial Report: "Machine Learning Identifies Multidomain Exposome Profiles for COPD Risk in Over One Million Participants Across Three Continents"

### 1. Overall Assessment

The manuscript derives a 20-item COPD-Related Exposome Index (CREI) from 249 candidate variables in the UK Biobank using LightGBM-based SHAP ensemble feature ranking, then reports external validation across seven cohorts spanning three continents (HRS, ELSA, SHARE, IFLS, CKB, LASI, NHANES), with each 1-SD increase in CREI associated with a 56.5% reduction in incident COPD risk in the discovery cohort (HR=0.435) and HR/OR ranging 0.46–0.80 externally.

This is a large-scale, well-resourced effort, but the central claim of "global validation" is weaker than framed. The 20-item instrument is never actually replicated as a fixed instrument outside UKB; each external cohort tests a different proxy-matched subset (9–19 of 20 items), so the reported consistency reflects the robustness of a general "favorable exposure" construct rather than validation of the CREI itself. Outcome ascertainment also varies from ICD-linked diagnoses to self-reported physician diagnosis to cross-sectional questionnaire modules, undermining direct comparability across the reported hazard ratios.

### 2. Strengths

The exposure-wide association study is genuinely large in scope, screening approximately 32,000 UKB data fields down to 249 candidate variables and applying Bonferroni-corrected Cox models before machine-learning-based ranking, which is methodologically sound as a two-stage discovery pipeline.

The eight-cohort geographic breadth (UKB, HRS, ELSA, SHARE, IFLS, LASI, NHANES, CKB; >1.2 million combined participants) is unusual for an exposome index and represents real effort toward external generalizability, even if imperfectly executed.

Spirometric validation against FEV1, FVC, FEV1/FVC, and PEF in both UKB and NHANES anchors the index to objective physiology rather than relying solely on diagnostic codes, which strengthens construct validity.

The communality-weighted Potential Impact Fraction approach to PAF estimation is a meaningful methodological improvement over naive Levin's formula, and the authors are appropriately transparent that PAF may still be inflated by residual co-occurrence among exposures.

### 3. Weaknesses

Outcome heterogeneity across the eight cohorts (incident ICD-linked COPD in UKB; incident chronic lung disease by self-report in HRS/ELSA/SHARE/IFLS/CKB; prevalent questionnaire-based "COPD-like disease" in LASI/NHANES) means the pooled narrative of "consistent protective effect" is comparing structurally different endpoints, not one endpoint across settings.

The 20 CREI components are dichotomized into favorable/unfavorable bins with cutoffs derived in UKB and then applied across cohorts with markedly different clinical, cultural, and measurement contexts (e.g., housing tenure, disability allowance), raising portability concerns the manuscript does not address empirically.

No benchmarking exists against established COPD risk tools (e.g., COPD-PS, ADO index) or against simpler prior lifestyle scores already shown to predict COPD in UK Biobank, so the incremental value of a 20-item, machine-learning-curated index over existing simpler instruments is unproven.

Reverse causation mitigation is limited to 2- and 5-year lag exclusions; COPD has a subclinical, often decades-long prodrome, and this window may be insufficient given the stronger protective effect observed in the <55-year subgroup, which is at least as consistent with survivor/detection bias as with a true early-life exposome effect.

### 4. Editorial Decision

**Send for Review.** The multi-cohort scale and spirometric validation merit expert adjudication, but reviewers must specifically evaluate whether the outcome heterogeneity across cohorts invalidates the "global validation" framing, whether cutoff-based harmonization of proxy components is defensible, and whether the absence of comparison against existing COPD risk scores is a fatal omission for a claim of clinical translatability.

### 5. Suggested Reviewer Expertise

Reviewers should have expertise in: exposome-wide association study methodology and multiple-testing correction in biobank-scale data; gradient-boosted ensemble feature selection (LightGBM/SHAP) and its clinical interpretability limitations; polygenic risk score derivation and gene-environment interaction modeling; population attributable fraction and potential impact fraction methodology; and clinical pulmonology/COPD epidemiology across low- and middle-income country settings, given the IFLS, LASI, and CKB cohorts.

### 6. State-of-the-Art Literature Review (Past 3 Years)

Recent work in this space has moved in two parallel directions: ML-based individual risk prediction and simpler composite lifestyle scores. Liu et al. (2024, PeerJ) developed eight machine learning models combining polygenic risk scores, electronic health records, and clinical data in roughly 329,000 UK Biobank participants for early-onset COPD, achieving an AUC of 0.85, a discrimination benchmark this manuscript does not report or compare against. Separately, a 2025 UK Biobank study found inverse associations between a healthy lifestyle score and incident COPD that were stronger in women than men, and NHANES-based work using the Life's Essential 8 score showed a dose-response relationship between cardiometabolic lifestyle scoring and all-cause mortality in COPD patients. The present manuscript's contribution is breadth of candidate variables and cross-continental external application, but it does not engage with the discriminative-performance literature (AUC-based) at all, framing its contribution purely in hazard-ratio terms, and it does not cite or contrast against the closest prior lifestyle-score COPD work in the same UKB source population.

### 7. Suggested Reviewers' Names

**Exposome/ML methodology:** John Wright; Roel Vermeulen; Marc Chadeau-Hyam; Xifeng Wu.

**Genetic risk / gene-environment interaction:** Michael H. Cho; Edwin Silverman; Brian D. Hobbs.

**COPD clinical epidemiology (global/LMIC):** Louisa Ewald; MeiLan K. Han; Sundeep Salvi.

**Biostatistics / PAF-PIF methodology:** Bruce Levin; Sander Greenland.

052991
# Editorial Report: TCMT-AI: A Hallucination-Free Digital Framework for Structured Chief Complaint Analysis in Traditional Chinese Medicine

## 1. Overall Assessment

The manuscript presents TCMT-AI, a rule-constrained retrieval system that maps unstructured TCM chief complaints onto a curated database of 4,566 standardized terms, using bge-large-zh-v1.5 and all-MiniLM-L6-v2 for bilingual semantic encoding combined with exact and fuzzy string matching. The central claim is that constraining generation to a closed terminology space eliminates hallucination relative to eight general-purpose LLMs, which showed 10.81–22.67% hallucinatory disease terms on a 25-case benchmark.

This is fundamentally a database-curation and retrieval-engineering paper, not a validated clinical decision-support system. The "zero hallucination" result is close to definitional: a closed-set retriever cannot hallucinate outside its own vocabulary by construction, and the manuscript reports no precision/recall for whether retrieved terms are clinically *correct*, only whether they exist in the database. The 25-case evaluation cohort is too small to support the generalizability claims made throughout the discussion.

## 2. Strengths

The terminology curation itself is methodologically sound and traceable: 4,566 terms were extracted from an authoritative national standard (Clinic Terminology of TCM Diagnosis and Treatment) via a documented regex-based hierarchical parsing pipeline, with explicit rules for bilingual name alignment and alias extraction.

The hybrid retrieval architecture (exact match → semantic similarity → fuzzy substring), with an explicit "no matching terms found" fallback, is a sensible and reproducible design for controlled generation, and the hierarchical semantic consistency analysis (Figure 1) provides a reasonable internal validity check on the knowledge base's organization.

The efficiency comparison against 8 SOTA LLMs (median 0.24s vs. 7.4–168.79s) is a genuine, verifiable operational advantage for high-throughput documentation workflows.

## 3. Weaknesses

The 25-case benchmark is grossly underpowered for the strong generalizability claims made in the abstract and discussion; no confidence intervals, no power calculation, and no external validation cohort are reported anywhere.

The comparison between TCMT-AI and general LLMs is not a fair like-for-like evaluation: a deterministic retriever constrained to 4,566 terms is being compared against open-ended generative systems on a "hallucination rate," but the manuscript never reports whether TCMT-AI's retrieved terms are diagnostically *correct*—only whether they exist in-vocabulary. This conflates retrieval-set membership with clinical accuracy.

The clinician-agreement analysis (80% attending, 52% resident) uses text-only chief complaints with no physical exam, pulse, or tongue data, which the authors acknowledge but do not correct for; comparing an information-restricted human judgment against a system trained on the same restricted input is not evidence of clinical utility.

Database coverage is narrower than incumbent resources (1,352 disease terms vs. 8,045–14,086 in ETCM/SymMap), and coverage gaps are not quantified against real-world complaint diversity or regional/school-specific terminology variation, which the authors themselves note as a limitation without addressing its magnitude.

## 4. Editorial Decision

**Reject.** The core contribution is a well-documented terminology database and retrieval pipeline, not a clinically validated advance; the hallucination-elimination claim is largely tautological given closed-set constraint, and the 25-case cohort cannot support the manuscript's generalizability language. This work is better suited to a specialized biomedical informatics venue.

## 5. Suggested Reviewer Expertise

Sentence-transformer-based dense retrieval and hybrid lexical-semantic search architectures; TCM-specific NLP and terminology normalization; clinical evaluation design and statistical methodology for diagnostic agreement studies; TCM clinical practice and syndrome differentiation methodology; regulatory/informatics standards for clinical terminology systems (e.g., SNOMED-CT mapping precedent).

## 6. State-of-the-Art Literature Review (Past 3 Years)

TCM-specific LLM work has moved well beyond static terminology retrieval toward integrated diagnostic reasoning: BianCang combines two-stage domain injection with RAG for syndrome differentiation and disease diagnosissignificantly improving TCM syndrome differentiation and disease diagnosis accuracy in real-world scenarios, with retrieval-augmented generation further enhancing performance; JingFang uses a multi-agent chain-of-thought architecture with a dedicated Syndrome Agent and dual-stage retrieval for consultation-grounded diagnosisrather than static terminology lookup; and TCM-DiffRAG combines knowledge graphs with chain-of-thought reasoning for personalized syndrome differentiationspecifically because TCM diagnosis centers on syndromes rather than diseases, unlike modern medicine. Benchmark infrastructure has also matured substantially, with TCM-5CEval, TCM-3CEval, MTCMB, and TCM-Ladder providing multi-task and multimodal evaluation frameworks for LLM knowledge, reasoning, and safety in TCM. A recent scoping review concluded that current TCM-oriented LLMs excel at basic syndrome differentiation reasoning and cross-language knowledge conversion but face significant challenges in capturing TCM's holistic diagnostic paradigm and individualized diagnosis. Against this landscape, TCMT-AI does not engage with or benchmark against any of these TCM-specific LLM systems (BianCang, JingFang, TCM-DiffRAG); it compares only against general-purpose LLMs on a narrower terminology-extraction task, which understates the actual state of the art and leaves the paper's positioning incomplete.

## Suggested Reviewers' Names

**Retrieval/NLP methods:** Ningyu Zhang; Nils Reimers; Jimmy Lin.
**TCM-specific LLM systems:** authors of BianCang (Sicen Guo lab, Peking University); authors of JingFang; authors of TCM-DiffRAG.
**Clinical evaluation/informatics:** Xiaoling Wang (JMIR Med Inform, TCM syndrome differentiation evaluation); a senior TCM clinician-informatician affiliated with a national TCM standards body (e.g., National Administration of TCM–affiliated academic hospital).

053414
# Editorial Report: "AIBuildAI-2 Enables Autonomous AI Model Development Through Knowledge-Enhanced Agentic Learning"

## 1. Overall Assessment

The manuscript introduces AIBuildAI-2, a hierarchical multi-agent system for autonomous AI model development, built on a two-level evolving knowledge base (L1 topical instructions, L2 low-level documents) that is dynamically retrieved and updated after each run. The central claim is that this knowledge system, rather than the backbone LLM alone, drives state-of-the-art performance: 70.7% medal rate on MLE-Bench, top 6.6% of 4,370 teams on a Kaggle heart disease competition, and top 38.8% on the OpenADMET ExpansionRx blind challenge.

This is fundamentally a general-purpose AI/ML-engineering systems paper, not a digital health study. Two of three evaluations (heart disease prediction, ADMET property prediction) are generic Kaggle-style benchmarks used to stress-test generalization, with zero clinical framing, deployment discussion, or health-outcome relevance. The paper does not belong in this section regardless of its technical merit, and the MLE-Bench leaderboard claim cannot currently be independently verified.

## 2. Strengths

The hierarchical knowledge architecture is genuinely novel in its separation of a human-authored L1 taxonomy (~30 categories) from a dynamically expanding L2 corpus (~1,000 documents), with dedicated builder agents that fold both post-run experience and newly published content back into the system. This addresses a real limitation of prior agents (AIDE, MLEvolve) that rely on either static parametric knowledge or frozen document snapshots.

The three-domain evaluation (MLE-Bench, a live Kaggle competition with 4,370 human teams, and a blind ADMET challenge) is a reasonable breadth test, and the live-competition result against thousands of active human competitors is a stronger signal than benchmark leaderboards alone.

The matched-backbone protocol for the heart disease and ADMET experiments (AIBuildAI-2 vs. AIBuildAI vs. MLEvolve, all on Claude Opus 4.7, identical compute budget) isolates the knowledge system's contribution reasonably well for those two comparisons.

## 3. Weaknesses

The MLE-Bench comparison is not backbone-matched: baselines including MARS, Famou-Agent, ML-Master, Leeroo, InternAgent, and R&D-Agent are pulled from the public leaderboard without confirmation they use the same backbone LLM. Since AIBuildAI-2 uses Claude Opus 4.7, a substantial fraction of the reported gain over the original MLE-Bench paper's best result (16.9% medal rate, o1-preview+AIDE) is plausibly attributable to backbone advancement rather than the knowledge system.

The official MLE-Bench GitHub leaderboard suspended new submissions in April 2026 pending a revised process "for ensuring submissions are fair and comparable" — precisely the confound above. The manuscript's rank-first claim rests on a leaderboard the maintainers themselves have flagged as unreliable, and this cannot be independently confirmed.

The heart disease dataset (Kaggle Playground Series S6E2) is a synthetically generated variant of the UCI Cleveland dataset, not real patient data. Reporting AUC 0.955 as evidence of "clinically meaningful" performance without any real-world cohort, subgroup breakdown, or calibration analysis is a significant overreach for a health-adjacent claim.

No fairness, subgroup, or demographic analysis appears anywhere in the two health/bio evaluations. Several cited baselines (AIDE, R&D-Agent, MARS, AIRA-dojo) are unpublished arXiv preprints as of this report, not peer-reviewed comparators.

## 4. Editorial Decision

**Reject.** The manuscript is a general AI/ML systems contribution misfiled into a digital health venue; neither health-adjacent evaluation involves real clinical data, deployment context, or fairness analysis, and the flagship leaderboard claim rests on a benchmark currently suspended for comparability concerns. These are not revisable within scope. Authors should be redirected to a general AI/ML systems venue (e.g., Nature Machine Intelligence, NeurIPS/ICML systems track) rather than sent for review here.

## 5. Suggested Reviewer Expertise

Agentic retrieval-augmented generation and hierarchical memory systems for LLM agents; autonomous ML engineering benchmarks and Kaggle-style agent evaluation protocols; graph neural network / message-passing molecular representation learning for ADMET and drug property prediction; clinical AI generalizability and external validation methodology for tabular EHR-derived prediction models; multi-agent LLM system design and evaluation.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The autonomous ML-engineering agent space has moved rapidly since MLE-Bench's introduction as an offline Kaggle competition environment for AI agents, where the best-performing evaluated agent, o1-preview with AIDE, achieved a medal rate of 16.9%. Concurrent 2026 systems (MARS, R&D-Agent, AIRA-dojo, InternAgent, Famou-Agent, ML-Master) have pushed scores substantially higher, largely tracking backbone LLM improvements. Separately, the self-evolving agent memory literature (A-mem, Mem0, AgentFold, EvolveMem) has converged on structured, retrievable, continually updated memory as the dominant paradigm, which is the same design AIBuildAI-2 applies specifically to ML engineering knowledge. The paper's L1/L2 hierarchical retrieval is a reasonable domain instantiation of this trend but is not conceptually distinct from it, and the manuscript does not engage this broader memory-agent literature at all.

## 7. Suggested Reviewer Names

**Autonomous ML-engineering agents / benchmarking:** Jun Shern Chan; Zhengyao Jiang; Dominik Schmidt; Xiao Yang (R&D-Agent).
**Molecular representation / ADMET:** Regina Barzilay; Kevin Yang.
**Clinical AI generalizability and validation:** Suchi Saria; Nigam Shah.

053471
Confirmed: Qibo DOI is 10.1016/j.eswa.2025.127672 (Expert Systems with Applications 284:127672, 2025), originally posted as arXiv:2403.16056 but now peer-reviewed and published.

Noted on the per-manuscript sandboxing instruction — this stays scoped to this chat.

---

## 1–4. Condensed Assessment, Strengths, Weaknesses, Decision (300 words)

This manuscript compares 16 LLMs against 60 TCM physicians on 60 real-world cases, with blinded five-expert scoring across nine dimensions (ICC 0.748–0.940) and Benjamini-Hochberg-corrected Wilcoxon tests. Top LLMs (DeepSeek-R1, Claude Opus 4, GPT-5) score above the physician baseline, but the prescription-level analysis shows systematic divergence in herb selection, dosage (e.g., Bupleuri Radix +7.56 g vs. physicians), and hallucination patterns (BianCang assigning "Feiwei disease" in 42/60 cases).

The comparator cohort is genuinely strong: 60 licensed physicians, 47 hospitals, blinded scoring infrastructure. The prescription-divergence analysis (Fig. 4) is the paper's best contribution, demonstrating that blinded expert scores do not track prescribing safety.

Two flaws are fatal, not revisable. First, physicians self-selected cases by subspecialty (Fig. 6A) while every LLM answered all 60 cases cold — an uncontrolled asymmetry that directly inflates the "LLMs beat physicians" headline and is never addressed statistically. Second, the source cohort spans 2018–2023 with 75 contributing physicians, yet the claim that the 2021–2023 benchmark subset avoids pretraining leakage is asserted, not tested (no membership-inference or corpus-matching procedure reported). Both flaws sit under the primary endpoint, not a secondary analysis — the headline finding is not trustworthy as reported.

**Decision: Reject.** The physician case-selection asymmetry is a structural design flaw that cannot be corrected through revision without re-running the physician arm under blinded, non-preferential case assignment, and the leakage claim requires an empirical test the authors did not perform. These are not editable weaknesses; they invalidate the primary comparator. The prescription-divergence and hallucination-taxonomy analyses have merit and may be resubmittable as a narrower, methodologically corrected study, or transferred to a venue with a lower evidentiary bar for comparator design (e.g., *npj Digital Medicine*).

---

## 5. Suggested Reviewer Expertise

Reviewers should cover: LLM benchmarking methodology and contamination/leakage detection for clinical text; blinded expert-rating study design and psychometrics (ICC, Likert rubric validation); TCM syndrome differentiation (bianzheng) and herbal prescription safety pharmacology; comparative clinician-AI diagnostic accuracy studies; and biostatistics for paired non-parametric multi-model comparisons (Friedman/Nemenyi, mixed-effects sensitivity analysis).

## 6. State-of-the-Art Literature Review (Past 3 Years)

The most directly competing work is Liu et al.'s npj Digital Medicine study comparing seven LLMs (GPT-4o, Gemini 1.5 Flash, LLaMA 3.2, Claude 3.5 Sonnet, ERNIE 3.5, Qwen 2.5 Max, Doubao 1.5 Pro) against three acupuncturists on a real-world case, published July 2025 — essentially the same design (real cases, physician comparator, blinded scoring) at smaller scale. That study found GPT-4o, Qwen 2.5 Max, and Doubao 1.5 Pro showed strong alignment with experts, particularly in TCM diagnosis and acupoint selection. The submitted manuscript does not cite or engage this paper despite near-identical methodology; reviewers should require the authors to differentiate their contribution explicitly. Other relevant recent benchmarks include TCM-Eval, a dynamic expert-level benchmark, and TCM-3CEval, a triaxial evaluation framework, alongside ShizhenGPT, a multimodal TCM-specialized foundation model tested against MedQA-Chinese, CMB, and CMExam subsets. Against this landscape, the manuscript's advance is scale (60 physicians, 349-case source pool) and its prescription-divergence and hallucination-taxonomy analyses, which none of the cited benchmarks perform; its weakness is failing to position these results against the directly comparable npj Digital Medicine physician-comparator study.

## 7. Suggested Reviewers' Names

*Methodology/LLM evaluation:* Yu Liu (Massachusetts General Hospital/Harvard, lead author of the npj Digital Medicine TCM-LLM comparator study); Jian Kong (MGH, corresponding author, same study).
*TCM informatics/knowledge modeling:* authors of the TCM-Eval or TCM-3CEval benchmark teams; Xin Dong (TCM-FTP herbal prescription prediction, JAMIA).
*Clinical TCM/herbal safety:* a senior bianzheng-trained clinician-researcher with published herb-safety or prescription-audit work, independent of this manuscript's author list given the overlapping BenCao model development.

---

## Further Literature (5–7 closely scoped papers, past 3 years)

1. **Liu Y, Yuan Y, Yan K, et al.** "Evaluating the role of large language models in traditional Chinese medicine diagnosis and treatment recommendations." *npj Digital Medicine* 8, 466 (2025). DOI: 10.1038/s41746-025-01845-2. *Directly comparable design — real clinical case, physician comparator (3 acupuncturists), blinded scoring across TCM diagnosis, Western diagnosis, and treatment. Smaller scale but the closest prior-art precedent the manuscript fails to cite; the discrepancy in physician-comparator size (3 vs. 60) and the difference in leakage-control rigor should be reconciled by the authors.*

2. **Hua R, Dong X, Wei Y, et al.** "Lingdan: enhancing encoding of traditional Chinese medicine knowledge for clinical reasoning tasks with large language models." *Journal of the American Medical Informatics Association* 31(9), 2019–2029 (2024). DOI: 10.1093/jamia/ocae087. *Fine-tuned TCM-specific LLM (Lingdan-PR) for herbal prescription recommendation, benchmarked against electronic medical record ground truth. Directly relevant to the submitted manuscript's prescription-divergence findings — Lingdan reports quantitative prescription-matching metrics the submitted paper omits in favor of Likert-scale expert scoring alone.*

3. **Long H, Deng Y, Guo Y, et al.** "Large Language Model Evaluation in Traditional Chinese Medicine for Stroke: Quantitative Benchmarking Study." *JMIR Formative Research* 9, e81545 (2025). DOI: 10.2196/81545. *Compares GPT-4o and DeepSeek-R1 — two models also evaluated in the submitted manuscript — on a 203-question TCM-stroke benchmark. Useful cross-check: relative ranking of these two models on structured knowledge questions versus the submitted paper's real-case ranking (DeepSeek-R1 top-ranked) should be reconciled or discussed.*

4. **Dai Y, Shao X, Zhang J, et al.** "TCMChat: A Generative Large Language Model for Traditional Chinese Medicine." *Pharmacological Research* 210, 107530 (2024). DOI: 10.1016/j.phrs.2024.107530. *TCM-domain generative model benchmarked against general-purpose baselines on diagnosis and prescription generation tasks. Relevant comparator for the submitted manuscript's TCM-specialized model arm (BenCao, HuatuoGPT-2, BianCang, Huatuo), none of which include TCMChat despite its recency and peer-reviewed status.*

5. **Jia Y, Ji X, Wang X, et al.** "Qibo: A large language model for traditional Chinese medicine." *Expert Systems with Applications* 284, 127672 (2025). DOI: 10.1016/j.eswa.2025.127672. *TCM-domain LLM built via continuous pretraining and SFT, with its own Qibo-Benchmark reporting 63% average subjective win rate against baselines. A fifth TCM-specialized comparator the submitted manuscript's four-model domain-specific panel (BianCang, HuatuoGPT2, BenCao, Huatuo) omits without justification.*

6. **Zhou X, Dong X, Li C, et al.** "TCM-FTP: Fine-Tuning Large Language Models for Herbal Prescription Prediction." *2024 IEEE International Conference on Bioinformatics and Biomedicine (BIBM)*, 4092–4097 (2024). *Peer-reviewed conference paper (IEEE, not preprint) directly targeting herbal-prescription prediction accuracy against ground-truth prescriptions — methodologically the closest published precedent for the submitted manuscript's prescription-divergence analysis (Fig. 4), and should be cited as the metric baseline the authors' novel divergence metrics are compared against.*

7. **[Preprint — flag as unreviewed]** Huang T, Lu L, Chen J, et al. "ShizhenGPT: Towards Multimodal LLMs for Traditional Chinese Medicine." arXiv:2508.14706 (2025). *Multimodal TCM foundation model tested on MedQA-Chinese, CMB, and CMExam subsets. Not peer-reviewed at time of this review; cite only as an unreviewed benchmark reference if included, and note that the submitted manuscript's own evaluation is text-only despite the source dataset including imaging and tongue/pulse findings — ShizhenGPT's multimodal scope highlights this as an unaddressed limitation.*

052813
Now compiling the revised report.

## 1. Overall Assessment

DermoSight-Agent adapts a DermLIP/OpenCLIP ViT-B/16 encoder with supervised contrastive projection to build a train-only case-memory archive, retrieves Top20 similar cases, and converts them into ranked diagnoses via rank-aware aggregation and taxonomy-aware reranking, reaching Top-3 coverage of 0.896 on a 77-class internal cohort. The framing — traceable retrieval evidence rather than opaque classification — is worthwhile, and the ablation cleanly isolates the value of supervised contrastive projection over raw DermLIP (Top-1 67.61 → 75.47). Two problems dominate: the external validation compares Top-1 accuracy across incompatible label spaces (5–9 mapped classes versus 77 internal), and no diagnosis-stratified performance is reported for melanoma or basal cell carcinoma despite dermoscopy's core clinical purpose being skin-cancer triage.

## 2. Strengths

The rank-aware aggregation is fully specified mathematically (log rank-decay weighting, capped label scores, bounded taxonomy correction), giving genuine reproducibility rarely seen in retrieval-based clinical AI. Patient-level splitting with a train-only memory archive correctly prevents retrieval leakage. The ablation table (raw DermLIP vs. mixed SupCon) with paired bootstrap and McNemar testing is a well-isolated, genuine methodological contribution.

## 3. Weaknesses

External Top-1 accuracy (0.760, 0.765) is not comparable to the internal figure (0.755) because the external label space is collapsed to 5–9 classes; the honest comparator, kappa, drops from 0.723 internally to 0.377/0.320 externally, which the manuscript underplays. No malignant-condition-specific sensitivity is reported — BCC/melanoma don't appear in Table 1's top-10 diagnoses, and the only high-risk evidence is one illustrative Figure 3 case. No skin-tone, age, or sex subgroup analysis is given despite citing the Fitzpatrick17k and Daneshjou disparities literature directly. Pathology-discordant cases were excluded up front, likely inflating performance by removing the hardest, most clinically ambiguous cases. No IRB/consent statement or data/code availability statement appears anywhere.

## 4. Editorial Decision

**Reject**, with a suggestion to transfer to *npj Digital Medicine* after the authors add malignant-stratified performance, subgroup/fairness analysis, and a same-cardinality external validation. The label-space mismatch and absent high-risk breakdown are not superficial fixes for a diagnostic decision-support claim at this venue.

---

## 5. Suggested Reviewer Expertise

Reviewers should have expertise in contrastive vision-language representation learning for medical imaging, case-based/nearest-neighbor retrieval systems for clinical decision support, and evaluation methodology for long-tailed multi-class diagnostic systems (macro-metrics, calibration, bootstrap inference). Clinically, reviewers should have practicing dermoscopy expertise in pigmented lesion and skin-cancer triage, plus familiarity with AI fairness and skin-tone representation in dermatology datasets.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has consolidated around large dermatology-specific vision-language foundation models since 2023. Derm1M/DermLIP — the exact encoder family this manuscript builds on — was published at ICCV 2025 with over one million image-text pairs across 390 conditions in a four-level clinical ontology, yet the manuscript treats it only as a frozen backbone rather than benchmarking against its own zero-shot and retrieval results. PanDerm (Nature Medicine, 2025) trained on 2.1 million images from 11 institutions and validated with three clinician reader studies showing measurable improvement in dermatologist accuracy — a direct precedent for the reader-study validation this manuscript lacks entirely. MONET (Nature Medicine, 2024) demonstrated that concept-grounded retrieval evidence can be made clinically interpretable and auditable, which is conceptually adjacent to this manuscript's case-memory evidence but with stronger interpretability grounding. None of these three is cited.

## Further Literature (5–7 closely scoped recent papers)

1. **Kim, C., Gadgil, S.U., DeGrave, A.J., Omiye, J.A., Cai, Z.R., Daneshjou, R. & Lee, S.-I.** (2024). Transparent medical image AI via an image–text foundation model grounded in medical literature. *Nature Medicine*, 30(4), 1154–1165. DOI: 10.1038/s41591-024-02887-x. MONET grounds dermatology image-text retrieval in concept-level evidence auditable by dermatologists — a stronger interpretability standard than DermoSight-Agent's case-similarity evidence, and directly relevant to the manuscript's traceability claim.

2. **Yan, S., Yu, Z., Primiero, C., Vico-Alonso, C., et al.** (2025). A multimodal vision foundation model for clinical dermatology. *Nature Medicine*, 31(8), 2691–2702. DOI: 10.1038/s41591-025-03747-y. PanDerm validated its foundation model with three prospective clinician reader studies (improving dermatologist accuracy by 11% on dermoscopy) — the missing validation standard this manuscript should be held to before any clinical traceability claim is credited.

3. **Yan, S., Hu, M., Jiang, Y., Li, X., Fei, H., Tschandl, P., Kittler, H. & Ge, Z.** (2025). Derm1M: A million-scale vision-language dataset aligned with clinical ontology knowledge for dermatology. *Proceedings of ICCV 2025*. This is the source dataset/encoder family (DermLIP) the manuscript adapts, but the manuscript never benchmarks against Derm1M's own zero-shot classification or cross-modal retrieval baselines, an omission reviewers should require be corrected.

4. **Gassner, M., Barranco Garcia, J., Tanadini-Lang, S., et al.** (2023). Saliency-enhanced content-based image retrieval for diagnosis support in dermatology consultation: reader study. *Journal of Medical Internet Research*, 25, e42129. DOI: 10.2196/42129. Directly comparable retrieval-for-diagnosis-support design, but validated with an actual clinician reader study — the exact evaluation this manuscript substitutes with text-similarity metrics (ROUGE/METEOR/BERTScore) instead.

5. **Zeng, W., Sun, Y., Ma, C., Tan, W. & Yan, B.** (2025). MM-Skin: Enhancing dermatology vision-language model with an image-text dataset derived from textbooks. *Proceedings of the 33rd ACM International Conference on Multimedia*, 3769–3778. DOI: 10.1145/3746027.3755187. Multimodal dermatology dataset spanning dermoscopy, clinical, and pathology images with fine-grained VQA supervision; relevant as a comparator for whether case-memory retrieval evidence could instead be grounded in richer textbook-derived language rather than rule-extracted phrases.

6. **Xu, G., Jin, P., Wu, Z., Li, H., Song, Y., Sun, L. & Yuan, L.** (2025). DermINO: Hybrid pretraining for a versatile dermatology foundation model. *arXiv:2508.12190* [preprint, not yet peer-reviewed]. Trained on 432,776 images with an explicit fairness evaluation component — flagged here specifically because the manuscript under review omits any comparable fairness analysis despite citing the underlying disparities literature.

052259
# Editorial Report — Manuscript 052259
## "Knowledge-grounded agentic instruction generation for multimodal pathology AI"

### 1. Overall Assessment

PGenAgent generates pathology instruction-tuning QA data from multimodal TCGA resources via four stages: feasibility-aware task triage, knowledge-base retrieval, generation and reflection. From 8,774 patients it produces 116k QA pairs, outperforming a conventional LLM-only pipeline on four LLM-judged axes and improving downstream Qwen3-VL-8B fine-tuning across nine tasks. The core claim — that task triage and disease-specific retrieval, not raw multimodality, drive instruction quality — is a real contribution to a genuine bottleneck. But all generation, evaluation and fine-tuning occur exclusively within TCGA, and the one directly comparable prior method, PathGen-1.6M, is cited but never benchmarked.

### 2. Strengths

Scale is substantial: 8,774 patients, 31 TCGA cohorts, 23 organ systems, 116k QA pairs across nine tasks. Evaluation triangulates three independent LLM judges with blinded pathologist review (κ = 0.76, 0.68), giving convergent validity to reported gains (e.g., microscopic feature description quality 48.3%→65.6%). The ablation isolates triage, retrieval and reflection, showing retrieval drives the largest marginal gain (67.0%→73.5%) — supporting the mechanistic claim rather than treating the agent as a black box. The quality–performance correlation (r = 0.99) is a clean, testable link.

### 3. Weaknesses

External validation is absent: generation, training and the 1,000-patient test split all come from the same 31 TCGA cohorts, with no independent institution, scanner or non-US cohort tested. This is a first-order generalizability gap for a method claiming clinically reliable supervision. Baseline comparison is narrow — only a single generic LLM pipeline is used; PathGen-1.6M, the closest published multi-agent precedent (ref. 26), is never run as a comparator. Code and the generated dataset are not currently available, precluding reproducibility review now. No demographic subgroup analysis (age, sex, race) is reported despite TCGA carrying this metadata. LLM-judge validity is asserted, not calibrated against per-item pathologist scores.

### 4. Editorial Decision

**Send for Review.** The contribution and multi-method evaluation merit external scrutiny; TCGA-only scope is a limitation, not a disqualifying flaw, since this is a data-generation framework rather than a diagnostic claim. Reviewers must adjudicate: (1) whether TCGA-only evaluation supports "clinically reliable" framing or requires an external cohort; (2) whether omitting a PathGen-1.6M comparison is a material gap; (3) whether current code/data unavailability is acceptable at this stage.

### 5. Suggested Reviewer Expertise

Retrieval-augmented generation and agentic LLM architectures for structured knowledge grounding; multimodal vision-language pretraining for gigapixel whole-slide images; LLM-based automatic evaluation and hallucination benchmarking methodology. Clinically: anatomic/surgical pathology spanning multi-organ diagnostic criteria (WHO classification), and computational pathology translational deployment (dataset curation, TCGA-derived model generalizability).

### 6. State-of-the-Art Literature Review (Past 3 Years)

Computational pathology has moved from patch-level foundation models toward multimodal, slide-level systems: TITAN (Ding et al., Nat Med 2025) pretrains on 335,645 WSIs with vision-language alignment and deliberately excludes TCGA/PAIP/CPTAC to avoid benchmark contamination — a direct methodological contrast to PGenAgent's TCGA-only design. mSTAR (Nat Commun 2025) integrates slides, reports and gene expression across 32 cancer types. HistoGPT (Tran et al., Nat Commun 2025) and SlideChat generate dermatopathology and general WSI-level reports respectively. Most relevant is PathGen-1.6M, which already used multi-agent collaboration on TCGA to generate 1.6M image-text pairs and downstream instruction-tuning data — establishing agentic pathology data generation as a known approach that this manuscript does not empirically engage.

PGenAgent's distinct contribution is feasibility-aware task triage combined with a manually curated, pathologist-reviewed knowledge base for retrieval grounding, rather than caption generation alone. This is a meaningful extension, but the field's trajectory toward external, contamination-free validation (TITAN) sharpens the need for PGenAgent to demonstrate generalization beyond TCGA before its "clinically reliable" framing is fully earned.

### 7. Suggested Reviewers

**Agentic/RAG architectures:** Yikang Shen; Yuxuan Sun (PathGen-1.6M); Shunyu Yao (ReAct).
**Multimodal WSI foundation models:** Tong Ding / Faisal Mahmood group (TITAN); Yingxue Xu (mSTAR); Ming Y. Lu (multimodal generative AI copilot for pathology).
**Clinical pathology / diagnostic criteria:** a board-certified anatomic pathologist with multi-organ WHO classification expertise, distinct from co-authors.

### Further Literature (Past 3 Years, Closely Scoped)

1. Ding, T., Wagner, S.J., Song, A.H. et al. A multimodal whole-slide foundation model for pathology. *Nat Med* 31, 3749–3761 (2025). DOI: 10.1038/s41591-025-03982-3. TITAN pretrains on 335,645 WSIs with vision-language alignment and deliberately excludes TCGA/PAIP/CPTAC from pretraining to avoid benchmark contamination — a direct methodological counterpoint to PGenAgent's exclusive reliance on TCGA for both generation and evaluation.

2. Seyfioglu, M.S., Ikezogwo, W.O., Ghezloo, F. et al. Quilt-LLaVA: Visual instruction tuning by extracting localized narratives from open-source histopathology videos. *Proc. IEEE/CVF Conf. Comput. Vis. Pattern Recognit.* 13183–13192 (2024). Constructs Quilt-Instruct, a 107,131-pair histopathology instruction dataset sourced from educational videos rather than structured reports; offers an alternative, non-TCGA evidence source that PGenAgent's discussion of generalizability should engage.

3. Naeem, A., Li, T., Liao, H. et al. Path-RAG: Knowledge-guided key region retrieval for open-ended pathology visual question answering. *Proc. Mach. Learn. Res.* 259, 735–746 (2025). A retrieval-augmented pathology QA framework using HistoCartography for region-level knowledge grounding; the closest methodological analog to PGenAgent's retrieval agent, but at patch level rather than patient-level multimodal integration, and lacks PGenAgent's triage/reflection stages.

4. Jiang, K. et al. Automating expert-level medical reasoning evaluation of large language models (MedThink-Bench). *npj Digit. Med.* 8, [in press] (2025/2026). DOI: 10.1038/s41746-025-02208-7. Directly interrogates the reliability of LLM-as-judge scoring against expert clinical judgment — bearing on whether PGenAgent's own three-LLM-judge evaluation framework requires similar independent calibration.

5. Shaikovski, G., Vorontsov, E., Casson, A. et al. PRISM2: Unlocking multi-modal general pathology AI with clinical dialogue. *arXiv* 2506.13063 (2025). **Unreviewed preprint.** A general-purpose multimodal pathology model trained with clinical-dialogue-style supervision rather than single-turn QA; relevant as an alternative instruction paradigm not discussed by the authors.

6. Evidence-driven agent for radiology report generation (EviAgent). *arXiv* 2603.13956 (2026). **Unreviewed preprint.** A cross-domain analog applying agentic, evidence-grounded generation to radiology rather than pathology; useful for reviewers assessing whether PGenAgent's architecture generalizes across imaging modalities or is pathology-specific by necessity.

052691
# Editorial Report — "Mapping the healthy aging heart: a normative electrophysiological digital twin atlas for pathological remodeling assessment"

## 1. Overall Assessment

The manuscript builds the first population-level 3D electrophysiological digital twin (DT) atlas of healthy cardiac aging from 30 MyoFit46 participants (age 75+), using quasi-simultaneous CMR and 256-lead ECGI to personalize conduction velocity, PMJ-based activation, and a two-layer repolarization model (baseline gKs plus an "aging repolarization" gKr surrogate), then applies it to an age-matched hypertensive (eHTN) subgroup as proof-of-concept. The acquisition is genuinely novel, but the atlas's normative and pathology-discrimination claims outrun what n=30 and largely non-significant eHTN comparisons can support.

## 2. Strengths

Quasi-simultaneous CMR-ECGI in a deeply phenotyped 75+ cohort is a rare resource, exceeding the spatial resolution of prior 12-lead ECG-based DT pipelines. Six-case synthetic verification against known ground truth — spanning CV range, activation strategy, and repolarization pattern — is disciplined practice before real-data application. The Procrustes-aligned mean healthy anatomy with PCA-decomposed gKs variability (three modes, 75% of variance) gives a defensible statistical framework for the atlas.

## 3. Weaknesses

n=30 (of 505 screened), ethnically homogeneous, undermines "normative" claims and inflates the fragility of multiple sex/segment/PCA comparisons. PMJ and activation-sequence estimates rest on an unvalidated reverse-propagation heuristic, verified only synthetically, never against invasive electroanatomical mapping. The eHTN proof-of-concept — the paper's translational payload — shows no region reaching corrected significance for gKs differences; the AgR shift relies only on directional sign tests. Data and code (Alya) are proprietary to ELEM Biotech, and several authors hold direct financial ties (ELEM co-founder/employees, a MyCardium AI CEO), limiting independent reproducibility.

## 4. Editorial Decision

**Transfer to Medical Image Analysis or npj Digital Medicine.** The pipeline is technically sound, but sample size, unvalidated activation-sequence estimation, and non-significant eHTN localization fall short of the reproducible, clinically decisive advance Nature Communications requires.

---

## 5. Suggested Reviewer Expertise

Reviewers should cover: (1) monodomain/reaction-eikonal cardiac electrophysiology modeling and DT personalization pipelines; (2) ECGI inverse-problem reconstruction and its known spatial resolution limits (septal/basal blind spots); (3) statistical shape modeling and population-level cardiac atlas construction (Procrustes alignment, PCA-based variability decomposition); (4) ionic/cellular modeling of cardiomyocyte aging and sex-specific repolarization (O'Hara-Rudy family models); and (5) geriatric or hypertensive cardiology, specifically preventive risk stratification in adults aged 75+.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The closest direct comparator is Qian et al. (*Nat. Cardiovasc. Res.*, 2025), which built 3,461 cardiac digital twins from the UK Biobank and another 359 from an ischemic heart disease cohort using cardiac magnetic resonance images and electrocardiograms, showing that myocardial conduction velocity remains similar across sexes but changes with age and obesity, and that longer QTc intervals in obese females were attributable to larger delayed rectifier potassium conductance. That paper establishes population-scale age-related electrophysiological remodeling at two orders of magnitude greater cohort size using a less spatially rich but far more scalable ECG-based approach, yet the manuscript under review does not engage with it despite direct conceptual overlap on age-conductance relationships. Camps et al. (*Med. Image Anal.*, 2024) established an open-source automated pipeline for personalising ventricular electrophysiological function based on routinely acquired MRI data and the standard 12-lead ECG, using sequential Monte Carlo inference — a stronger uncertainty-quantification framework than this manuscript's deterministic point-estimate approach. Grandits et al. (*Med. Image Anal.*, 2025) directly addressed identifiability of ventricular conduction-system parameters from surface ECGs, a question closely related to this manuscript's unvalidated PMJ estimation but left unaddressed here. The manuscript's genuine advance is its ECGI-based spatial resolution and healthy-aging framing; its main omission is failing to benchmark against the much larger-scale CDT population literature that has already established age-repolarization relationships.

---

### Suggested Reviewers' Names

**CDT personalization / monodomain modeling:** Steven Niederer (Imperial College London/King's), Gernot Plank (Medical University of Graz), Natalia Trayanova (Johns Hopkins)

**ECGI inverse-problem reconstruction:** Yoram Rudy (Washington University in St. Louis), Rob MacLeod (University of Utah), Simone Pezzuto (Università della Svizzera italiana)

**Statistical shape modeling / population cardiac atlases:** Pablo Lamata (King's College London), Vicente Grau (University of Oxford), Avan Suinesiaputra (University of Leeds)

**Aging/sex-specific cellular electrophysiology:** Colleen Clancy (UC Davis), Eleonora Grandi (UC Davis)

**Geriatric/hypertensive cardiology:** Bryan Williams (UCL, hypertension), John Chambers (National University of Singapore, cardiovascular epidemiology in aging)

---

## Further Literature

1. Qian, S. et al. Developing cardiac digital twin populations powered by machine learning provides electrophysiological insights in conduction and repolarization. *Nat. Cardiovasc. Res.* 4, 624–636 (2025). DOI: 10.1038/s44161-025-00650-0. Directly overlapping scope: builds 3,461 CDTs from UK Biobank showing age- and obesity-driven changes in conduction velocity and GKrKs. The manuscript should discuss why its ECGI-based, n=30 atlas is needed given this far larger ECG-based population already characterizing age-repolarization effects.

2. Camps, J. et al. Harnessing 12-lead ECG and MRI data to personalise repolarisation profiles in cardiac digital twin models for enhanced virtual drug testing. *Med. Image Anal.* 100, 103361 (2024). DOI: 10.1016/j.media.2024.103361. Competing repolarization-personalization pipeline using Bayesian (sequential Monte Carlo) inference rather than the manuscript's deterministic gKs/gKr scaling — relevant comparator for uncertainty quantification the manuscript lacks.

3. Camps, J. et al. Digital twinning of the human ventricular activation sequence to clinical 12-lead ECGs and magnetic resonance imaging using realistic Purkinje networks for in silico clinical trials. *Med. Image Anal.* 94, 103108 (2024). DOI: 10.1016/j.media.2024.103108. Uses an explicit, probabilistically inferred Purkinje network for activation-sequence personalization, in contrast to this manuscript's heuristic, synthetically-validated-only reverse-propagation PMJ estimation.

4. Grandits, T., Gillette, K., Plank, G. & Pezzuto, S. Accurate and efficient cardiac digital twin from surface ECGs: insights into identifiability of ventricular conduction system. *Med. Image Anal.* 105, 103641 (2025). DOI: 10.1016/j.media.2025.103641. Directly addresses identifiability limits of ECG/ECGI-derived conduction-system parameters — a methodological question the manuscript's PMJ/CV estimation does not confront despite comparable inverse-problem uncertainty.

5. Sánchez, J. et al. Enhancing premature ventricular contraction localization through electrocardiographic imaging and cardiac digital twins. *Comput. Biol. Med.* 190, 109994 (2025). DOI: 10.1016/j.compbiomed.2025.109994. Combines ECGI with DT simulation for localization tasks and reports quantitative geodesic/RMSE validation against known origins — a stronger validation template than this manuscript's uncorroborated PMJ mapping.

6. Salvador, M. et al. Digital twinning of cardiac electrophysiology for congenital heart disease. *J. R. Soc. Interface* 21, 20230729 (2024). DOI: 10.1098/rsif.2023.0729. Demonstrates DT personalization in a structurally distinct population (congenital disease) using similar monodomain/reaction-diffusion methodology, illustrating the broader applicability standard this manuscript's small, ethnically homogeneous cohort does not meet.

7. Coleman, J. A., Camps, J., Hasaballa, A. I. & Bueno-Orovio, A. Simulation-based digital twinning of activation and repolarisation sequences from the ECG across healthy and diseased hearts. *Comput. Biol. Med.* 198, 111222 (2025). DOI: 10.1016/j.compbiomed.2025.111222. Infers both activation and repolarization from ECG with quantitative benchmark validation (Spearman r=0.63–0.65 against ground truth) in both healthy and diseased (HCM) hearts — a directly comparable healthy-vs-pathology framework with more rigorous accuracy reporting than this manuscript's eHTN comparison provides.

052019
**Editorial Alert — requires handling editor action before/alongside review:** The open-goal case study's cohort (Nephrology Dept., First Affiliated Hospital of Sun Yat-sen University, 2009–2022; external validation at Zhongshan City People's, Foshan, and Youjiang hospitals) and five-subtype taxonomy (DN, HN, IgAN, MCD/FSGS, MN) are identical to KIDS (Wu et al., *Nat. Commun.* 2025, 16:6962), which shares corresponding author Haotian Lin and several co-authors with this manuscript. KIDS is not cited. This needs author clarification on redundant publication/cohort reuse before review proceeds.

---

## 1–4. Condensed Assessment, Strengths, Weaknesses, Decision (300 words)

Eureka is a GPT-4o-driven agentic framework implementing a three-stage human-AI collaboration protocol and a six-level autonomy taxonomy, evaluated on six fixed-goal digital-medicine benchmarks plus an open-goal nephropathy biomarker case study. The central claim is methodological: structured, checkpointed oversight, not full autonomy, is the correct architecture for AI-driven biomedical discovery.

The ablation study is the strongest evidence offered: removing expert checkpoints degraded performance on three of six tasks (retinal disease classification, vessel segmentation, hereditary hearing loss), quantifying human value-add in a way most comparable 2026 agent papers do not. The Table 1 protocol (five-iteration stall trigger, 25-iteration restart) is specific enough to reproduce. The six-task benchmark spans imaging, tabular, genetic, and EHR modalities against held-out sets and published expert baselines.

Against this, the open-goal case study — framed as a genuine AI-discovered cross-organ biomarker — uses the same cohort, validation centers, and taxonomy as KIDS (uncited, overlapping authorship). DeepDKD (Meng et al., *Lancet Digit. Health* 2025) had already shown fundus-only diabetic/non-diabetic nephropathy differentiation at far larger scale; also uncited. The taxonomy's empirical support rests on one LLM backbone, one researcher on the fixed-goal tasks, two on the open-goal study, and a non-blinded post-hoc acceptance survey (n=80) administered after a curated project log. External validation is uneven (HN external n=6; MCD/FSGS AUC 0.707, 95% CI 0.621–0.790).

**Decision: Send for Review.** Reviewers should adjudicate: (1) whether the relationship between this manuscript's cohort/findings and KIDS constitutes redundant publication; (2) whether the autonomy taxonomy is adequately supported given the small evaluator samples; (3) whether the benchmark and ablation design meet the bar for a systems contribution absent a genuinely novel clinical finding.

---

## 5. Suggested Reviewer Expertise

Agentic LLM architectures and tool-use orchestration for scientific workflows; multimodal fusion of imaging and tabular clinical data (random forest/SHAP feature selection methodology); nephrology, specifically biopsy-confirmed glomerular disease classification and retinal-renal microvascular pathophysiology; human-computer interaction methodology for evaluating human-AI collaboration (survey design, inter-rater reliability); retinal imaging biomarkers for systemic disease screening.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Agentic scientific-discovery systems moved from arXiv preprints to peer-reviewed *Nature* papers in 2026: ERA (Aygün et al.) for expert-level scientific software generation, Co-Scientist (Gottweis et al.) for multi-agent hypothesis generation now deployed via Gemini for Science, and Robin (Ghareeb et al.) for closed-loop biological discovery, alongside the Virtual Lab (Swanson et al., *Nature* 2025) demonstrating wet-lab-validated nanobody design. These systems report experimentally validated outputs that Eureka's case study does not match in independent novelty. In retinal-renal AI specifically: Sabanayagam et al. and Zhang et al. (*Nat. Biomed. Eng.* 2021) established CKD detection from fundus images; DeepDKD (Meng et al., *Lancet Digit. Health* 2025) extended this to subtype differentiation at population scale; and KIDS (Wu et al., *Nat. Commun.* 2025) — from this same author group — already delivers the five-subtype classification presented here as a novel AI-generated hypothesis. Eureka's contribution, if any, is confined to the collaboration-protocol framework, and even there it trails the empirical rigor of the 2026 Nature agent papers.

---

## Further Literature (7 papers, past 3 years)

1. Gottweis, J. et al. "Accelerating scientific discovery with Co-Scientist." *Nature* (2026). DOI: 10.1038/s41586-026-10644-y. — Already cited by authors (ref. 12) but not structurally compared: Co-Scientist's oversight is continuous "trust-but-verify" rather than staged/checkpointed, and its outputs include wet-lab-validated drug repurposing hypotheses absent from Eureka's computational-only case study.

2. Ghareeb, A. E. et al. "A multi-agent system for automating scientific discovery." *Nature* (2026). DOI: 10.1038/s41586-026-10652-y. — Robin; already cited (ref. 13) but not compared: closer clinical domain (macular degeneration) and completes literature-to-hypothesis-to-lab cycle that Eureka's open-goal study stops short of.

3. Swanson, K., Wu, W., Bulaong, N. L., Pak, J. E. & Zou, J. "The Virtual Lab of AI agents designs new SARS-CoV-2 nanobodies." *Nature* 646, 716–723 (2025). DOI: 10.1038/s41586-025-09442-9. — Not cited. Closest architectural analogue (PI agent + specialist agents + human high-level feedback), validated with 92 experimentally synthesized nanobodies; Eureka offers no comparable prospective or wet-lab endpoint.

4. Wu, Q. et al. "A noninvasive model for chronic kidney disease screening and common pathological type identification from retinal images." *Nat. Commun.* 16, 6962 (2025). DOI: 10.1038/s41467-025-62273-0. — Not cited. Same institutional cohort and disease taxonomy as Eureka's open-goal case study, with comparable or superior subtype-level AUCs. Central to the disclosure issue flagged above.

5. Meng, Z. et al. "Non-invasive biopsy diagnosis of diabetic kidney disease via deep learning applied to retinal images: a population-based study." *Lancet Digit. Health* (2025). DOI: 10.1016/j.landig.2025.02.008. — Not cited. Differentiates diabetic from non-diabetic nephropathy from fundus images alone at population scale (734,084 pretraining images, five-country external validation); pre-empts the "latent cross-organ association" framing of Eureka's discovery.

6. Zhao, X. et al. "Screening chronic kidney disease through deep learning utilizing ultra-wide-field fundus images." *npj Digit. Med.* 7, 275 (2024). DOI: 10.1038/s41746-024-01271-w. — Not cited. Multimodal (imaging + retinal vessel parameters + history) CKD screening validated across 23 tertiary hospitals; relevant baseline Eureka's model is not benchmarked against.

7. Schmidgall, S. et al. "Agent Laboratory: Using LLM Agents as Research Assistants." *Findings of ACL: EMNLP 2025*, 5977–6043. DOI: 10.18653/v1/2025.findings-emnlp.320. — Not cited. Structurally comparable three-stage pipeline (literature review, experimentation, report writing) with human checkpoints, evaluated across many tasks; useful comparator for whether Eureka's protocol formalization is a genuine advance over existing staged-autonomy designs.
