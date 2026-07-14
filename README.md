# Trackrad202512456

054690
## Editorial Integrity Alert — For Handling Editor

*(unchanged)*

Two issues require resolution before this manuscript can proceed to review. First, the abstract and Results text both state 94.25% accuracy for Brain-DLNet on the private cohort, but Figure 8's comparison table reports 95.50% for the same condition — an unresolved internal inconsistency in the flagship clinical result. Second, Figure 3b contains a visible embedded question-and-answer exchange ("Q: Where is federated learning? A: Federated learning represents an established benchmark…") that reads as an unedited artifact of AI-assisted figure generation. Authors should be asked directly about figure provenance and the source of the accuracy discrepancy.

---

## 1. Overall Assessment

The manuscript proposes DLNet, decomposing a centralized neural network into institution-owned layer modules that collaboratively reconstruct end-to-end learning without any participant holding the full model or raw data, demonstrated via a three-institution Swin Transformer brain tumor classifier (Brain-DLNet). The core mechanism — sequential layer partitioning with intermediate-representation exchange — is mathematically equivalent to split learning and cyclical weight transfer, both established since 2018. The paper's most serious problems are evidentiary: an internal accuracy discrepancy on its flagship clinical result, no formal privacy guarantee despite privacy being the central motivation, and a membership-inference evaluation that omits federated learning, the most relevant competitor, an omission the authors acknowledge rather than address.

## 2. Strengths

Architecture-agnostic validation across ResNet18, AlexNet, and ViT-Base on three datasets demonstrates generalizability beyond single-architecture split-learning work. The validation-aligned layer-credit mechanism, converting per-segment gradient alignment into entropy-regularized allocation via a closed-form solution, is a genuinely useful resource-allocation contribution independent of the medical framing. The zero-knowledge verification scheme offers sensible auditability for a trust-minimized multi-institutional setting.

## 3. Weaknesses

The privacy claim rests entirely on empirical membership-inference resistance; the Discussion itself concedes no differential-privacy guarantee exists, while gradient-leakage attacks are never tested despite gradients crossing every module boundary. Figure 3 explicitly omits federated learning as a comparator, calling this the field's "developmental context" rather than fixing it — disqualifying on its own for a privacy-motivated paper. The clinical cohort lacks subgroup analysis and confidence intervals, and the 94.25%/95.50% discrepancy undermines trust in the headline number. Brain-DLNet's fixed three-way split is architecture-driven rather than a negotiated governance structure, leaving inter-institutional disagreement and capacity mismatch unaddressed.

## 4. Editorial Decision

**Reject.** The unresolved clinical-accuracy inconsistency, the acknowledged absence of a federated-learning baseline in the central privacy experiment, and the missing formal privacy guarantee are independent, non-revisable grounds requiring re-run experiments rather than a text revision.

---

## 5. Suggested Reviewer Expertise

*(verbatim, unchanged)*

Reviewers should cover: split learning and split-federated learning theory (to assess DLNet's actual novelty margin over Vepakomma et al. and SplitFed); membership-inference and gradient-leakage attack methodology in distributed training; entropy-regularized resource allocation and contribution estimation (Shapley-value or credit-assignment methods) in federated systems; Swin Transformer-based medical image classification; and neuro-oncology / neuroradiology, specifically glioma–meningioma differential diagnosis on MRI, to evaluate the clinical plausibility of the reported subtype confusion pattern.

## 6. State-of-the-Art Literature Review (Past Three Years)

*(verbatim, unchanged)*

The dominant trend since 2023 has been communication-efficient and robustness-focused federated/split learning rather than new partitioning paradigms: block-coordinate accelerated federated methods (FedBCGD, cited as ref. 6), split-federated co-learning under label noise (Kafshgari et al. 2026, ref. 10), and privacy-hardened federated frameworks combining homomorphic encryption with differential privacy (Gomathi et al. 2026, ref. 20) all extend the communication-protocol axis the authors say they are moving beyond. Zero-knowledge-verified federated learning has also emerged concurrently (zkFL-health, ref. 22, arXiv 2025), meaning DLNet's verification contribution is contemporaneous with, not ahead of, the field. On the clinical-imaging side, Swin-based brain tumor classifiers reporting comparable or higher single-site accuracy (MTA-Swin at 98.57%, and Swin-Tiny zero-shot transfer work on BRISC-2025) have appeared in 2025–2026 without any distributed-learning framing, suggesting the accuracy ceiling Brain-DLNet approaches is not itself remarkable — the contribution has to rest entirely on the multi-institutional governance angle, which is exactly where the missing federated-learning baseline hurts most.

## Suggested Reviewers' Names

*(verbatim, unchanged)*

*Split/federated learning theory:* Praneeth Vepakomma; Chandra Thapa; Otkrist Gupta; Zeyu Han (Kafshgari et al. collaborator network).

*Privacy attacks in distributed training:* Reza Shokri; Ligeng Zhu; Milad Nasr.

*Resource allocation / contribution estimation in FL:* Fan Lai; Zelei Liu.

*Medical imaging / Swin-based classification:* Ali Hatamizadeh; authors of the MTA-Swin (2026) and Tumor-Swin Transformer lines of work.

*Neuroradiology (glioma/meningioma differential):* a practicing neuroradiologist with multi-centre brain tumor MRI cohort experience — name to be identified by the editorial office given no author in the cited literature set matches this specific clinical role.

055772
# Editorial Report — Manuscript 055772
## "Anticipatory decoding of walking direction from gait-phase-aligned shank sEMG"

---

## EDITORIAL INTEGRITY ALERT (to Handling Editor)

The Declarations state: *"Ethical approval: This article does not contain any studies involving human, animal participants performed by any of the authors."* Section 4.1 directly contradicts this: eight human participants (4 male, 4 female, students, age 25±3) were recruited and physically instrumented to walk with the intelligent walker. This is either a template error left uncorrected or a genuine absence of ethics review for human-subjects data collection. Either reading is disqualifying at submission: the manuscript cannot be sent for review until the authors clarify which is true and, if human data were collected, supply the IRB/ethics-committee approval reference. No blinded author list was provided with this review copy, which also prevented an independent check for undisclosed preprints or overlapping publications from the same group; this should be verified by the handling editor once authorship is unblinded.

---

## 1. Overall Assessment

The manuscript aligns shank sEMG to IMU-detected heel-strike/toe-off events to decode walker turning direction, amplitude, and fall risk before the action occurs. A bidirectional GRU reaches 94.0% accuracy at a 200 ms lead time, and phase-alignment outperforms fixed time-window cropping across eight architectures. The mechanism is demonstrated, not asserted, and the physiological validation is more rigorous than most work in this space. But the evidentiary base is thin: eight healthy students on one flat surface, no cross-subject testing, for a device motivated by mobility impairment in a population never sampled. Combined with a Declarations statement contradicting the Methods on human-subjects involvement, the manuscript does not clear this venue's bar.

## 2. Strengths

Phase-alignment is shown, via Figure 4, to reduce feature aliasing relative to fixed-window cropping, a believable mechanism for the reported gains. The eight-architecture ablation is systematic, yielding a +6.7 pp average and +13.8 pp maximum gain from phase labeling, and identifies 200 ms as the accuracy/lead-time operating point. The MUAP clustering and waveform analysis of four target muscles grounds discriminability in neuromuscular function, not accuracy alone. The hardware is properly characterized, with sub-10 microsecond synchronization and IEC 60601-2-40-consistent validation.

## 3. Weaknesses

The cohort, eight students from one site and age band, cannot support the claim about mobility-impaired users, a population never tested despite the authors' own cited evidence that gait synergy timing shifts with age. The design never specifies subject-independent versus subject-dependent splits, the most consequential detail for this claim, and the BiGRU-BiLSTM-Advanced-TCN ranking carries no significance test. Two directly competing papers, a rollator turning-intention system and a similarly structured BiGRU decoder, are absent.

## 4. Editorial Decision

Reject. The ethics contradiction is independently disqualifying until resolved by the editorial office. Even setting it aside, the cohort and design cannot support the claimed generalizability, and the missing literature weakens the novelty argument. Resubmission should resolve the ethics statement, report subject-independent accuracy, and engage the omitted prior art.

---

## 5. Suggested Reviewer Expertise

Reviewers should cover: gait-phase-aware temporal deep learning for multimodal sEMG-IMU fusion in lower-limb intent decoding (the paper's core methodological claim); wearable biosensor hardware and synchronization validation for surface EMG acquisition systems; motor-unit action potential decomposition and EMG-based interpretability methods, to assess whether the physiological-validation chapter is methodologically sound; and, on the clinical side, geriatric gait, balance, and turning-related fall risk in walker/rollator-assisted mobility, to evaluate whether the cohort and task design are adequate for the paper's stated clinical motivation.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

Two recent large reviews frame the field: Chen et al.'s human motion intent prediction (HMIP) survey (*npj Artificial Intelligence*, 2026) and Zhang, Sid'El Moctar, Boudaoud & Rida's 181-study review of sEMG-IMU sensor fusion (*Information Fusion*, 2026) both identify multimodal phase-aware temporal modeling as the field's active frontier, consistent with this manuscript's framing. Gao, Chen, Farina, Zhao et al.'s wearable-mobility perspective (*Nature Communications*, 2025) makes the complementary point this manuscript itself echoes: EMG-only or IMU-only sensing each face a delay-versus-noise tradeoff that multimodal fusion is meant to resolve. At the architecture level, PiMAN (*Neurocomputing*, 2025) and the DCAF-Net stroke-rehabilitation exoskeleton decoder (arXiv:2512.12184, 2025) both apply gated/attentive recurrent fusion to anticipatory pre-movement sEMG, and Wang et al.'s fuzzy multitask lower-limb intent recognizer (*IEEE Trans. Fuzzy Syst.*, 2024, already cited by the manuscript) established multi-output intent decoding as a recent trend this paper extends to turning amplitude and fall risk.

Most directly, Chen, Clos, Price & Caleb-Solly's digital-twin rollator study (arXiv:2509.05116, 2025) is the closest existing system: sEMG+IMU fusion for turning-intention classification on an actual rollator, evaluated with an explicit cross-subject protocol. Against this landscape, the manuscript's genuine advance is the phase-alignment mechanism as a model-agnostic accuracy enhancer and the systematic lead-time ablation, neither of which the Nottingham study or PiMAN provide. But its complete omission of both papers is a real gap, and the absence of any cross-subject number — the one metric the closest competing paper foregrounds — leaves the manuscript's central generalizability claim untested relative to where the field already stands.

---

## 7. Suggested Reviewers' Names

**Technical:**
- Imad Rida (Université de Technologie de Compiègne) — co-author, sEMG-IMU sensor-fusion review, *Information Fusion* (2026).
- Praminda Caleb-Solly (University of Nottingham) — senior author, digital-twin rollator turning-intention system, arXiv:2509.05116 (2025); directly matches the walker-turning application.
- Dario Farina (Imperial College London) — corresponding author, wearable-assisted-mobility perspective, *Nature Communications* (2025); leading authority on surface EMG neuromuscular decoding. Included as a senior domain anchor per the "last resort" full-professor allowance, given the centrality of his group's review to this exact sub-field.
- Hubin Zhao (UCL) — co-corresponding author on the same *Nature Communications* (2025) piece; wearable assistive-system integration.

**Clinical:**
- Teresa Liu-Ambrose (University of British Columbia, Aging, Mobility and Cognitive Neuroscience Laboratory) — falls- and gait-intervention research in older adults (e.g., *Phys. Ther.*, 2025).
- A second clinical reviewer with hands-on geriatric or post-stroke rollator/walker deployment experience should be sourced through the journal's rehabilitation-medicine network; I could not verify a specific matching name with sufficient confidence from the open literature to recommend one here rather than fabricate a plausible-sounding candidate.

---

### Strongest counterargument to this rejection

A defender of the paper would say: the ethics line is very plausibly a boilerplate template artifact rather than a real compliance failure, the phase-alignment mechanism and lead-time ablation are legitimate, reproducible engineering contributions independent of cohort size, and eight-subject pilot cohorts are conventional for first-in-kind sensor-fusion demonstrations in this literature (including the Nottingham rollator paper itself, n=11). Under that reading, a "reject with resubmission encouraged" rather than a hard reject, contingent solely on the ethics clarification, would be defensible. I still weight the cohort/generalizability gap and missing competing citations as independently sufficient for rejection at this venue's bar, but the editorial office should not treat the ethics line as certain fraud before asking the authors directly.

055918
## 1. Overall Assessment

This multicenter study trains a ResNet-50+CBAM multimodal fusion model on 1289 Chinese adolescents (single 1.5T GE scanner) and validates on two independent external cohorts spanning 1.5T/3.0T and GE/Siemens, targeting continuous age and China's four legal-responsibility thresholds (12/14/16/18 years). The validation breadth exceeds most prior single-site knee-MRI literature, but center and scanner manufacturer are fully collinear, and sensitivity at the forensically critical 18-year threshold falls to 0.47 externally.

## 2. Strengths

The two-cohort external validation, training-set-only Youden cutoffs, and patient-level splitting represent genuinely rigorous design choices rarely seen together in this literature. Threshold selection is legally grounded in the 2020 criminal-responsibility amendment rather than arbitrary. Calibration plots, decision curve analysis, and DeLong-based subgroup testing exceed the evaluation depth of cited comparators, and the authors report rather than suppress unfavorable findings (18-year sensitivity drop, field-strength AUC gap, regression-to-mean bias).

## 3. Weaknesses

Center and manufacturer are structurally confounded (center 2 all-GE, center 3 all-Siemens), so the claimed field-strength/vendor robustness cannot be attributed to either factor alone. No ablation isolates CBAM, multimodal fusion, or auxiliary inputs, yet the Discussion claims the model "mirrors" radiologist reasoning without attention-map evidence. The 18-year threshold—most consequential for criminal responsibility—performs worst, with no same-cohort benchmark against manual Vieth/Schmeling staging. The severe training-age imbalance (57.7% >18y vs 5.4% <12y) drives an acknowledged but uncorrected regression-to-mean bias.

## 4. Editorial Decision

**Reject**, transfer to *Communications Medicine*. The confounded design, absent ablations, and weakest performance at the highest-stakes threshold are structural flaws, not revisable in minor revision.

056486
## Editorial Report — Manuscript 056486 (Revised)

*"Agentic AI for point-of-care design of patient-specific orbital implants" (OPDA)*

---

### 1–4. Assessment, Strengths, Weaknesses, Decision (condensed)

OPDA is a multi-agent, human-supervised system converting natural-language clinical instructions into manufacturing-ready orbital PSI meshes, coordinating EPC-Net segmentation, VLM-guided landmark registration, SSM-based orbital prediction, case-matched base generation, VLM-assisted perforation/screw-hole design, and outcome-grounded memory across a 15-centre, 168-assembly preclinical study. The engineering integration is genuine and the validation scale unusually thorough for this literature, but the central acceptability claim is undercut by the manuscript's own numbers, and reliance on undisclosed proprietary cloud APIs for safety-relevant steps raises governance concerns only partly acknowledged.

The agentic decomposition is validated, not asserted: Extended Data Table 3 shows simplified variants of all four non-deterministic modules scoring materially lower (2.23–3.08) than the full pipeline (4.03–4.34). EPC-Net segmentation is benchmarked against DentalSegmentator, Mimics, 3D U-Net, UNETR and nnU-Net with both quantitative metrics (Dice 0.93, HD95 2.62mm) and blinded clinician scoring. The demographic generalizability check (European/East-Asian/African, n=40 each, ANOVA, all P>0.1) is unusually rigorous, and model selection is systematic, benchmarking 27 candidate LLMs with multilingual adversarial querying.

The headline usability figure is internally inconsistent with the paper's own acceptance criterion: mean score 3.88/5 across 168 assemblies falls below the ≥4/5 threshold defined as "first-pass acceptable," yet the Discussion calls the designs "broadly usable." Two different V1.0 baselines (70.8% manufacturability vs. 55% expert-rated acceptance) are used inconsistently, with the memory-adaptation headline built on the lower, more dramatic figure. The fabrication-feasibility claim rests on n=3 cases via one partner, and the study is preclinical throughout, with no intraoperative or outcome data — appropriately scoped in the Discussion but understated in the Abstract. Literature engagement omits directly comparable cranial-implant deep-learning work from a co-author's own group.

**Decision: Send for Review**, contingent on resolving the integrity alert above and requiring reviewers to adjudicate the sub-threshold usability claim, the divergent acceptance baselines, the data-governance question, and the AAAI-26 overlap. None of these is a non-revisable structural flaw.

---

### 5. Suggested Reviewer Expertise

Multi-agent LLM/VLM orchestration for tool-use and 3D geometric reasoning pipelines; statistical shape modelling and point-cloud/mesh registration for craniofacial anatomy; medical image segmentation benchmarking methodology (nnU-Net-class comparative validation); data-governance and regulatory compliance for cloud-hosted foundation models in clinical deployment; and oral/craniomaxillofacial trauma surgery with hands-on orbital PSI design and fixation experience.

### 6. State-of-the-Art Literature Review (Past 3 Years)

The closest direct comparator is Reinhard et al. (*Nature Communications*, 2024), which automated data-driven design and 3D printing of custom ocular prostheses — a single-task, non-conversational pipeline the manuscript cites but does not sharply differentiate from beyond "orbital implant vs. prosthesis." Xu et al. (*Medical Image Analysis*, 2025), also cited, used a prior adversarial generative network for automatic orbital blowout-fracture reconstruction, but without clinician-in-the-loop revision or manufacturing handoff. The sibling cranial-implant literature descending from the MICCAI AutoImplant challenges (Li et al., *IEEE TMI* 2021; Memon, Shi, Egger & **Chen**, *Med Biol Eng Comput* 2025 — the last from a co-author's own lab) established deep-learning shape-completion baselines (Dice ~0.91, HD95 ~1.5mm) for a closely related bony-defect problem and is conspicuously absent from this manuscript's framing. Broader 2025–2026 "agentic medical AI" work (Ferber et al., Ghareeb et al., both *Nature* 2026, both cited) remains largely text- or decision-support-oriented; OPDA's claim to be first to execute inspectable operations directly on 3D anatomical meshes is plausible relative to that literature, but the paper would be considerably strengthened by directly benchmarking against AutoImplant-lineage cranial methods rather than relying on the orbital sub-domain alone to establish novelty.

### 7. Suggested Reviewers' Names

*Multi-agent LLM/VLM orchestration:* Yubin Kim, Chanwoo Park, Marzyeh Ghassemi, Pranav Rajpurkar
*Statistical shape modelling / craniofacial registration:* Jan Egger, Hannes Ulrich, Franca Wagner, Mauricio Reyes
*Segmentation benchmarking:* Fabian Isensee, M. Jorge Cardoso, Klaus Maier-Hein
*Data governance / regulatory science for clinical foundation models:* Karim Lekadir, Judy Wawira Gichoya, Roxana Daneshjou
*Craniomaxillofacial / orbital trauma surgery:* Alfred G. Becking, Ruud Schreurs, Constantinus Politis

---

### Further Literature (Past 3 Years, Similar Scope)

1. **Reinhard, J. et al.** Automatic data-driven design and 3D printing of custom ocular prostheses. *Nature Communications* 15, 1360 (2024). — *Cited by manuscript (ref. 10).* Closest single-task comparator: fully automated, data-driven design-to-print pipeline for a related periorbital prosthetic device. Not conversational/agentic and has no clinician-revision loop; manuscript should more explicitly state what OPDA's multi-agent architecture adds beyond this precedent rather than treating it as a generic prior citation.

2. **Xu, J. et al.** Intelligent surgical planning for automatic reconstruction of orbital blowout fracture using a prior adversarial generative network. *Medical Image Analysis* 99, 103332 (2025). — *Cited (ref. 8).* Directly competing orbital-fracture reconstruction method (GAN-based) on the same anatomical target. Automated but single-shot, non-agentic, with no manufacturing handoff or expert-in-the-loop revision — the natural head-to-head baseline reviewers should ask OPDA to be benchmarked against quantitatively, not just narratively distinguished.

3. **Vanslambrouck, P. et al.** Virtual reconstruction of orbital defects using Gaussian process morphable models. *International Journal of Computer Assisted Radiology and Surgery* 19, 1909–1917 (2024). — *Cited (ref. 9); author overlap with Van Dessel/Willaert/Sun.* This is the authors' own prior SSM method, retrained here as OPDA's Mesh Predictor backbone. Incremental relationship (retraining on a larger, 5,850-mesh cohort) is disclosed but not quantitatively separated from the new agentic contribution — reviewers should request an ablation isolating gains attributable to the larger SSM cohort versus the new agentic wrapper.

4. **Memon, A. R., Shi, H., Memon, T. R., Egger, J. & Chen, X.** Deep learning-based automatic cranial implant design through direct defect shape prediction and its comparison study. *Medical & Biological Engineering & Computing* 63, 2815–2826 (2025). DOI: 10.1007/s11517-025-03363-5. — **Uncited; author overlap (Xiaojun Chen, co-author).** Directly comparable automated implant-design pipeline for a sibling bony defect (cranial vs. orbital), benchmarked with Dice/HD95 against AutoImplant baselines. Its absence from the reference list, despite shared authorship, is a literature-engagement gap that should be corrected.

5. **Gao, Y., Li, F., Van Dessel, J., [...] & Willaert, R.** Can Large Language Models Grasp 3D Medical Anatomy Shapes? (Student Abstract). *Proceedings of the AAAI Conference on Artificial Intelligence* (March 2026). — **Uncited; author overlap (same corresponding-author group). Unreviewed/limited-review venue (student abstract track).** Directly anticipates the manuscript's VLM-3D-anatomy-reasoning premise underlying the Spatial Aligner. See Editorial Integrity Alert — must be disclosed and differentiated.

6. **Liu, Y. et al.** Benchmarking large language model-based agent systems for clinical decision tasks. *npj Digital Medicine* 9, art. 02443-6 (2026). DOI: 10.1038/s41746-026-02443-6. — *Uncited; no author overlap.* Methodologically parallel: systematically benchmarks agentic AI systems (planner–executor–verifier architectures) against baseline LLMs across clinical tasks, finding only modest accuracy gains at significant resource cost. Directly relevant counterpoint to OPDA's own 27-model MCDM benchmarking exercise (Extended Data Table 1) and worth citing to temper claims of straightforward agentic superiority.

7. **FUAS-Agents: Autonomous Multi-Modal LLM Agents for Treatment Planning in Focused Ultrasound Ablation Surgery.** arXiv:2505.21418 (2025/2026). — **Uncited; preprint, unreviewed.** Closest scope match outside orbital surgery: a multimodal, multi-agent LLM system for procedural treatment planning validated on a multicentre dataset (>3,000 cases across three institutions). Useful comparator for OPDA's claim of novelty in connecting agentic reasoning to procedural/device planning, though the comparison should be treated cautiously given non-peer-reviewed status.

8. **Ferber, D. et al.** Towards autonomous medical artificial intelligence agents. *Nature* (2026). — *Cited (ref. 37).* General framework/positioning paper for medical agentic AI; OPDA's introduction leans on this citation but could more precisely locate itself within Ferber et al.'s proposed autonomy taxonomy (the manuscript explicitly self-classifies as "human-supervised," not autonomous, which should be cross-referenced to this framework's terminology).

9. **Ghareeb, A. E. et al.** A multi-agent system for automating scientific discovery. *Nature* (2026). — *Cited (ref. 38).* General multi-agent scientific-reasoning system, not device-design-specific; useful for the architectural comparison (specialist sub-agents with cross-agent reflection and judge integration) that OPDA's PSI Base Generator MDT-inspired matching module also uses, but the parallel is not drawn out in the manuscript.

10. **Consorti, G., Monarchi, G. & Catarzi, L.** Presurgical virtual planning and intraoperative navigation with 3D-preformed mesh: a new protocol for primary orbital fracture reconstruction. *Life* 14, 482 (2024). DOI: 10.3390/life14040482. — **Uncited; no author overlap.** Non-AI, mirroring-based manual/semi-manual CAD workflow for orbital fracture PSI planning with intraoperative navigation. Useful as the "conventional workflow" baseline against which OPDA's time/cost claims are implicitly but not explicitly benchmarked — a concrete published comparator rather than the internal UZ Leuven 5-hour estimate currently used.

056298
## Editorial Report: Koulaouzidis et al., "Agentic trial emulation requires outcome-calibrated validation before informing clinical trial design" (Matters Arising)

### 1. Overall Assessment
This Matters Arising challenges EmulatRx (Li et al., *Nat Commun* 2026) on a specific, verifiable point: its nesiritide showcase reports HR 0.59 (95% CI 0.46–0.76), a significant benefit, while the ASCEND-HF trial it emulates found HR 0.93 (95% CI 0.90–1.08), a null result its own authors deemed non-recommendable. I confirmed both figures against primary sources; the letter's framing is accurate. The broader argument — that a single-run agentic pipeline should not be treated as validated causal-evidence generation absent RCT calibration — is sound and appropriately scoped for the format.

### 2. Strengths
The discordance argument is independently verifiable and clinically consequential: it converts a randomized null into an observational "significant benefit," exactly the failure mode that would mislead trial designers. The critique of the Statistician-agent's cross-LLM reproducibility claim is sharp and correct — identical HRs across four LLM backbones reflect deterministic downstream statistical libraries, not convergent causal reasoning, a reading the original paper's own methods text supports. Citations to Hernán/Robins, Austin, Cole/Hernán, and VanderWeele/Ding are accurate and appropriately deployed.

### 3. Weaknesses
The letter never engages EmulatRx's clone-censor-weight/IPCW machinery for immortal-time bias, leaving it open to a strawman objection on censoring. More seriously, it misses a medRxiv preprint of the same system under a different name ("TrialGenie," 2025), whose identical nesiritide showcase reports HR 0.73 (95% CI 0.63–0.84) on a smaller, differently-balanced cohort — direct evidence of within-pipeline instability that would have strengthened the reproducibility argument substantially. Page 3 of the submitted PDF is missing, so roughly half the letter's argument (cohort construction, safety signals, reproducibility) could not be fully verified.

### 4. Editorial Decision
Send for review, contingent on the complete manuscript and engagement with the TrialGenie discordance, alongside a solicited formal Reply from Li et al. The core claim clears the bar for a Matters Arising; the gaps are fixable pre-review, not disqualifying.

---

### 5. Suggested Reviewer Expertise

Reviewers should include someone with hands-on expertise in target trial emulation methodology specifically — estimand specification, clone-censor-weight/IPCW implementation, and calibration of observational estimates against RCT benchmarks (not generic "causal inference" background, since the dispute turns on implementation details). A second technical reviewer should have specific experience with LLM-agent pipelines applied to structured EHR data (SQL/OMOP cohort construction, concept mapping error taxonomies), since the letter's cohort-construction critique (page 3, unverified by me) likely turns on this. A third should have expertise in real-world evidence reproducibility and regulatory-grade RWE standards (e.g., FDA/EMA real-world evidence frameworks), to adjudicate whether "workflow-support tool" versus "validated causal-evidence system" is the correct regulatory-relevant framing. On the clinical side, a heart-failure trialist familiar with ASCEND-HF and nesiritide's post-trial reputation would confirm the letter's clinical framing is not overstated.

### 6. State-of-the-Art Literature Review (Past 3 Years)

The specific problem this letter raises — calibrating agentic or ML-based trial emulation against RCT benchmarks before trusting the output — already has an emerging methodological answer that neither Li et al. nor Koulaouzidis et al. engage with. TrialCalibre (Habibdoust & Song, ICML 2025) automates exactly the "Benchmark, Expand, Calibrate" workflow the letter calls for in the abstract: compare an observational emulation against an existing RCT, then use the measured divergence to calibrate a second emulation for a related indication. This is precisely the "explicit calibration against the randomized-trial estimand" the letter demands in its abstract, and its absence from both papers is notable. Separately, Orcutt et al. (*Nat Med* 2025) evaluated generalizability of ML-based oncology trial emulations against real trial results at scale, and is the closest existing empirical precedent for systematically checking RWE-pipeline output against RCT ground truth — a natural citation the letter omits. The broader field of agentic clinical-trial systems (AUTOCT, ClinicalAgent, and the TrialGenie predecessor itself) has moved fast on architecture and slower on validation; a 2025 survey (arXiv 2509.00987) already documents TrialGenie/EmulatRx's agent design without flagging the preprint-to-publication discordance found here, suggesting this gap has gone unnoticed community-wide, not just by these two papers. The letter's contribution, once completed, would be one of the first post-publication challenges specifically targeting result stability and RCT-discordance in this class of system — that is a real gap in the literature worth filling, provided the missing arguments are as rigorous as the two I could verify.

### 7. Suggested Reviewers' Names

**Target trial emulation / calibration methodology:** Issa Dahabreh (Harvard T.H. Chan, RCT-duplicate and target trial emulation methods); Jessica Young (Harvard, causal inference and TTE); Xavier Orcutt is himself a candidate given direct authorship of the RCT-vs-RWE generalizability paper cited above.

**LLM-agent pipelines on EHR data:** Suraj Rajendran should be recused (co-author on the target paper's cited prior work); consider Monica Agrawal (Duke, clinical NLP and LLM agents on structured/unstructured EHR data) or Zifeng Wang (postdoc-level, clinical trial LLM agents, AUTOCT-adjacent work).

**RWE reproducibility / regulatory standards:** Shirley Wang (Brigham and Women's/Harvard, RWE reproducibility — she is a co-author on the Wang/Sreedhara/Schneeweiss paper both manuscripts cite, and lead author on the RCT-DUPLICATE and TrialCalibre-adjacent standardization work below, making her well-positioned but requiring a conflict check).

**Clinical heart failure / trial context:** G. Michael Felker (Duke, heart failure trialist, ASCEND-HF co-investigator — conflict check required given trial involvement) or Justin Ezekowitz (University of Alberta, acute heart failure trials, also ASCEND-HF-adjacent — same caveat).

---

### Further Literature

1. **Wang SV, Schneeweiss S; RCT-DUPLICATE Initiative.** "Emulation of Randomized Clinical Trials With Nonrandomized Database Analyses: Results of 32 Clinical Trials." *JAMA*. 2023;329(16):1376–1385. doi:10.1001/jama.2023.4221. Not cited by manuscript. Independent of both author groups. This is the systematic, 32-trial version of exactly the single-showcase discordance problem the letter raises, and the strongest available empirical anchor for its "outcome-calibrated validation" demand — it should be cited, not left implicit.

2. **Orcutt X, Chen K, Mamtani R, Long Q, Parikh RB.** "Evaluating generalizability of oncology trial results to real-world patients using machine learning-based trial emulations." *Nat Med*. 2025;31(2):457–465. doi:10.1038/s41591-024-03352-5. Not cited by manuscript (cited by the target EmulatRx paper as ref. 4). Independent. Stratifies ML-based trial emulation against 11 landmark RCTs by prognostic risk, quantifying exactly where real-world benefit undershoots RCT benefit — a working example of the stratified, RCT-anchored validation Table 1 calls "needed" but does not itself demonstrate.

3. **Habibdoust A, Song X.** "TrialCalibre: A Fully Automated Causal Engine for RCT Benchmarking and Observational Trial Calibration." ICML 2025; arXiv:2604.25832. Peer-reviewed conference proceeding. Not cited by manuscript. Independent. Automates the "Benchmark, Expand, Calibrate" workflow the letter's own abstract demands — the closest thing in the literature to a ready-made answer to its central ask, and its omission is the letter's single biggest missed citation on the solutions side.

4. **Li H, Pan W, Rajendran S, Zang C, Wang F.** "TrialGenie: Empowering Clinical Trial Design with Agentic Intelligence and Real World Data." medRxiv 2025.04.17.25326033 (posted April 17, 2025). **Unreviewed preprint — flag explicitly.** Not cited by manuscript. Shares all listed authors with the target EmulatRx paper; independent of Koulaouzidis et al. The direct predecessor system, identical architecture, same NCT00475852 nesiritide case study, but reports HR 0.73 (95% CI 0.63–0.84, PSM, n=6,971) versus the published HR 0.59 (95% CI 0.46–0.76, IPTW, n=13,942) — the single most important omission in the letter's reproducibility argument.

5. **Rajendran S, Xu Z, Pan W, Zang C, Siempos I, Torres L, Xu J, Bian J, Schenck EJ, Wang F.** "Multicenter target trial emulation to evaluate corticosteroids for sepsis stratified by predicted organ dysfunction trajectory." *Nat Commun*. 2025;16:4450. doi:10.1038/s41467-025-59643-z. Not cited by manuscript (cited by the target EmulatRx paper as ref. 8 — a self-citation; four of ten authors overlap with the EmulatRx author list). A non-agentic, human-run TTE from the same lab; useful to check whether this group's manual TTE work independently calibrates against RCT benchmarks (e.g., ADRENAL, APROCCHSS) in a way EmulatRx's automated showcase did not.

6. **Feuerriegel S, Frauen D, Melnychuk V, Schweisthal J, Hess K, Curth A, Bauer S, Kilbertus N, Kohane IS, van der Schaar M.** "Causal machine learning for predicting treatment outcomes." *Nat Med*. 2024;30(4):958–968. doi:10.1038/s41591-024-02902-1. Not cited by manuscript (cited by the target EmulatRx paper as ref. 5). Independent. A methods-level Perspective explicitly warning against biased or incorrect causal-ML predictions absent careful validation — independent authority the letter could cite instead of relying solely on older Hernán-era TTE literature.

7. **Htoo PT, Wang SV, Schneeweiss S, et al.** "Post hoc Population Standardization of Trial Emulation Studies in Claims Data: An RCT-DUPLICATE Analysis." *Clin Pharmacol Ther*. 2026. doi:10.1002/cpt.70241. Not cited by manuscript. Independent. The most current (2026, contemporaneous with both papers under discussion) methodological advance on post hoc calibration of trial-emulation cohorts against RCT populations — directly responsive to the letter's calibration demand and worth citing as evidence the field already has active tooling for this problem.

056516
## EDITORIAL INTEGRITY ALERT (to Handling Editor)

**Citation misattribution on a stated baseline.** The manuscript lists EATA-C as a comparator ("EATA-C performs efficient adaptation with anti-forgetting constraints," Methods, classification-only) and cites reference [45] — Niu et al., ICML 2022, "Efficient test-time model adaptation without forgetting" — as its source. That ICML 2022 paper describes **EATA**, which has no calibration mechanism. EATA-**C** (the consistency-loss, min-max entropy re-calibration, and disagreement-based uncertainty indicator the manuscript's baseline actually implements) was introduced in a distinct, later work — Tan, Chen, Wu, Zhang, Chen, Zhao & Niu, "Uncertainty-Calibrated Test-Time Model Adaptation without Forgetting" — which does not appear anywhere in the reference list. This should be put to the authors directly before review proceeds.

---

## 1. Overall Assessment

The manuscript documents "calibration collapse" — medical foundation models retaining task performance while confidence becomes unreliable after domain transfer, worsened by entropy-based TTA — across 13 models, 15 datasets, and three task families, proposing a bounded Gini objective (GITTA) as a partial fix. The phenomenon is real and the benchmark is broad and clinically instrumented (HCER0.9, deferral simulation). But the core mechanism — entropy minimization causes overconfidence, bounded objectives mitigate it — is not new; it restates results already established in general-domain TTA and now systematizes them for medicine. Two issues will most influence the decision: the misattributed baseline citation above, and the absence of any demographic subgroup analysis.

## 2. Strengths

HCER0.9 and the confidence-gated deferral simulation (missed-error rate 62.3%→78.1% under Tent) convert an abstract calibration metric into an operational safety quantity — the paper's strongest contribution. Separating deployment setting (Fig. 1) from adaptation mechanism (Fig. 2) isolates pre-existing collapse from adaptation-induced collapse, precluding an implementation-artifact objection. The GITTA-Embed/GITTA-Input ablation and organ-level BTCV breakdown appropriately resist hiding heterogeneity behind macro scores.

## 3. Weaknesses

No subgroup analysis by age, sex, or skin tone appears anywhere despite using HAM10000/PAD-UFES-20 and pediatric CXR data — a serious gap given the paper's central claim about where confidence fails. Results are reported over fixed seeds despite the paper's own evidence of adaptation instability (GraTa: Dice 0.869→0.742), conflating resampling CIs with adaptation-seed variance. Main-text figures lean on unexplained "representative" single-dataset panels. Temperature scaling is excluded by design, but the more realistic middle ground — a small labeled target-site calibration set — is never tested despite being flagged as the practical deployment scenario.

## 4. Editorial Decision

Send for Review, contingent on the authors correcting the EATA-C attribution and confirming implementation fidelity. Reviewers should adjudicate whether the missing subgroup analysis is disqualifying given the datasets used, whether single-seed reporting is adequate given the instability findings, and whether GITTA is sufficiently distinct from EATA-C and the Gini/Tsallis-entropy family.

## 5. Suggested Reviewer Expertise

Reviewers should include expertise in fully test-time adaptation and confidence calibration under distribution shift (specifically LayerNorm-only/parameter-efficient online adaptation and entropy-versus-bounded-objective comparisons); segment-anything-style medical foundation models and their failure modes under domain transfer; calibration metrics and selective-prediction/deferral system design for clinical AI; and generative-model uncertainty quantification for vision-language medical QA. On the clinical side, reviewers should include a dermatologist or dermoscopy-AI specialist familiar with skin-tone representation in ISIC/HAM10000-derived datasets, and a gastroenterologist or radiologist experienced with confidence-gated triage workflows in endoscopy or chest imaging.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The field has moved rapidly toward exactly this problem in the last 12 months. Lou et al. (UAD-FM, *npj Digital Medicine* 8, 784, 2025) proposed an uncertainty-decomposed, causally-adapted foundation model for colorectal pathology pursuing nearly the same goal via epistemic/aleatoric decomposition rather than a bounded Gini objective; the manuscript cites it only as background and should engage with it as a direct competitor. Sheng et al. ("The Illusion of Progress?", NeurIPS Datasets & Benchmarks 2025) established that most TTA benchmarking suffers from inconsistent protocols and inflated claims — the manuscript's strict source-free protocol answers this critique but never says so explicitly. Two very recent segmentation-specific works are close prior art the authors should address: Chen et al. (ICCV 2025) perform input/embedding-level refinement of MedSAM without touching model parameters, conceptually adjacent to GITTA-Input; and an evidential active-TTA framework for medical SAMs (EviATTA, 2026) decomposes uncertainty via Dirichlet modeling for the same segment-anything backbones. The lit-review as written understates how crowded this space has become.

## Further Literature (Past 3 Years, Similar Scope)

1. **Lou, S. et al.** "Uncertainty-aware and causal test-time adaptive foundation model for robust colorectal cancer pathology diagnosis." *npj Digital Medicine* 8, 784 (2025). DOI: 10.1038/s41746-025-02149-1. **Cited** (ref. 20). Independent group (Harbin Medical University). Directly competing scope: uncertainty-decomposed, causally-intervened TTA for a medical foundation model, evaluated with ECE/Brier/NLL and a deferral simulation — methodologically the closest published analogue to GITTA, using causal do-interventions instead of a bounded Gini loss.

2. **Sheng, L., Liang, J., He, R., Wang, Z. & Tan, T.** "The Illusion of Progress? A Critical Look at Test-Time Adaptation for Vision-Language Models." NeurIPS Datasets & Benchmarks Track (2025); arXiv:2506.24000. **Cited** (ref. 19). Independent group (USTC/CASIA). Establishes the general-domain reproducibility critique of TTA benchmarking that the manuscript's strict online, source-free protocol implicitly answers but never cites as justification.

3. **Tan, M., Chen, G., Wu, J., Zhang, Y., Chen, Y., Zhao, P. & Niu, S.** "Uncertainty-Calibrated Test-Time Model Adaptation without Forgetting." arXiv:2403.11491 (v2, 2025). Preprint/journal-extended manuscript — **unreviewed**, not cited. Independent of manuscript (assuming no author overlap; unverifiable under double-blind). **This is the actual source of the EATA-C baseline** the manuscript implements and misattributes (see Integrity Alert). Directly on-scope: consistency-loss-based model-uncertainty reduction plus min-max entropy re-calibration for source-free TTA.

4. **Chen, K., Luo, X., Qin, T., Liu, J., Liu, H., Lee, V.H.F., Yan, H. & Li, H.** "Test-time Adaptation for Foundation Medical Segmentation Model without Parametric Updates." ICCV 2025; arXiv:2504.02008. **Not cited.** Independent group (City University of Hong Kong / University of Hong Kong). Directly relevant to the GITTA-Input variant: performs image-embedding refinement of MedSAM at test time without updating backbone parameters, addressing the same LayerNorm-efficiency motivation from a different angle.

5. **Chen, J., George, Y., Chong, W. & Cai, J.** "EviATTA: Evidential Active Test-Time Adaptation for Medical Segment Anything Models." arXiv:2603.14666 (2026). Preprint — **unreviewed, very recent**, not cited. Independent group (Monash University). Decomposes predictive uncertainty into distribution and data uncertainty via Dirichlet evidential modeling for the same SAM-Med2D/MedSAM-class backbones used in the manuscript's segmentation arm; a direct methodological alternative to the bounded-Gini approach.

6. **Nielen, T., Ambekar, S., Kiechle, J., Lang, D.M. & Schnabel, J.A.** "Entropy Minimization without Model Collapse: Mitigating Prediction Bias in Medical Imaging." arXiv:2606.02339 (2026). Preprint — **unreviewed**, not cited. Independent group (TU Munich / Helmholtz Munich). Mechanistically complementary: attributes entropy-minimization collapse in medical-imaging TTA to prediction-class-bias-driven feature-cluster merging and proposes an importance-reweighting fix (DSBR) — a different causal account of the same failure mode the manuscript calls "calibration collapse."

7. **Chen, G., Niu, S., Chen, D., Yang, J., Zhang, Z., Tan, M., Wu, P. & Shen, Z.** "ZeroSiam: An Efficient Siamese for Test-Time Entropy Optimization without Collapse." arXiv:2509.23183 (2025). Preprint — **unreviewed**, not cited. **Author overlap with entry 3** (Niu, Tan — same TTA-calibration research lineage). General-domain (not medical), but addresses entropy-minimization collapse via architectural asymmetry rather than a bounded loss — a useful contrast case for whether GITTA's loss-level fix is preferable to an architecture-level one.

8. **Shakeri, F., Baklouti, G. et al.** "Test-Time Adaptation of Medical Vision-Language Models." MICCAI Workshop, Springer LNCS (2025). DOI: 10.1007/978-3-032-07845-2_18. **Not cited.** Independent group. Directly on-scope for the manuscript's VQA branch: the first structured benchmark of TTA for medical VLMs, using mutual-information maximization and KL-regularized zero-shot deviation — a substantive comparator the manuscript's medical-VQA GITTA surrogate should be benchmarked against.

9. **Hekler, A., Kuhn, L. & Buettner, F.** "Beyond Overconfidence: Model Advances and Domain Shifts Redefine Calibration in Neural Networks." arXiv:2506.09593 (2025). Preprint — **unreviewed**, not cited. Independent group (Goethe University Frankfurt / DKFZ). Evaluates foundation-model calibration under distribution shift on biomedical imaging datasets (breast ultrasound, chest X-ray, dermoscopy, OCT) and finds foundation models can be *underconfident* in-distribution and *better*-calibrated under shift — a partial counter-finding to the manuscript's framing that deserves acknowledgment and discussion, not omission.

10. **[Authors withheld in source].** "Ranked Entropy Minimization for Continual Test-Time Adaptation." arXiv:2505.16441 (2025). Preprint — **unreviewed**, not cited. General-domain (ImageNet-C), independent group. Reports the identical ECE-degradation pattern under Tent/SAR relative to source models that the manuscript's Finding 2 documents in medical settings, and proposes a masking/ranking-based alternative objective — a general-CV precedent the authors should cite to show the medical-domain result is a specific instance of a broader known effect, not a novel discovery.

056749
## Editorial Report: HEMO-ACT (Manuscript 056749) — Revised

### 1–4. Assessment, Strengths, Weaknesses, Decision (condensed)

This manuscript proposes HEMO-ACT, a Kalman-regularized CNN-GRU model predicting multi-horizon (0h/24h/48h) survival risk scores in 827 ICU patients with hematologic malignancies from a single Beijing center. It claims dynamic risk trajectories outperform static scores (SAPS II, HHM) that dominate this niche. The architecture combines established components reasonably, but the evaluation framework is a poor match to the clinical claim, and a near-contemporaneous competing paper occupying the same niche is neither cited nor engaged with. This does not clear the bar at this journal's standard.

The 827-patient, 12-year, 6,128-patient-day cohort is genuinely large for this sub-domain, and the causal, EM-fitted Kalman imputation (fit on training data only, never conditioning on future values) correctly avoids a common time-series leakage failure. The multi-horizon shared-backbone design suits the stated bedside workflow, and the CNN-ablation result is an honest, if marginal, component-level finding.

The metric mismatch is disqualifying: the introduction frames the problem in AUROC terms (citing SAPS II 0.676, HHM 0.81) yet Results report only R² and RMSE for an undefined "survival risk score," with no AUROC, sensitivity/specificity, or calibration reported anywhere, making the central comparative claim unverifiable. SHAP-ranked "top features" (oxygenation index, troponin I, BNP) have 65–90% raw missingness and are therefore mostly Kalman-imputed, so their dominance may reflect imputation smoothness rather than physiology; no sensitivity analysis on observed-only data is offered. No external validation is performed, and the current cohort's IRB approval number is identical to a 2024 publication by three overlapping authors describing an overlapping patient population, undisclosed here. Multiple pairwise model comparisons run at uncorrected α=0.05 with several barely-significant P-values (0.038, 0.031, 0.022), and in-text citations 24–33 are systematically misnumbered against the reference list, including a duplicated AdamW citation.

**Reject.** The core claim cannot be assessed from the metrics reported, and this requires a new evaluation design, not a revision. Transfer to Communications Medicine or npj Digital Medicine is appropriate, contingent on AUROC/calibration reporting, disclosure of the cohort overlap with reference 10, and reference-list correction.

---

### 5. Suggested Reviewer Expertise

Reviewers should be sought with expertise in: (1) temporal deep learning architectures (CNN-recurrent hybrids, state-space models) applied to irregularly sampled, high-missingness multivariate EHR time series; (2) Kalman-filter and other model-based imputation methods for clinical time series, specifically their downstream effect on post-hoc interpretability; (3) SHAP and related attribution methods for sequential/temporal neural models, including known failure modes under heavy imputation; (4) benchmarking methodology for clinical prediction models, including discrimination/calibration reporting standards and multiple-comparison correction in model-comparison studies; and, on the clinical side, (5) critical care management of hematologic malignancy and allogeneic HSCT patients, including familiarity with existing ICU severity scores (SAPS II, APACHE II, HCT-CI) in this population.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

Dynamic, repeated-measurement ICU mortality prediction has advanced substantially since 2023, and the most relevant recent paper is one the manuscript does not cite: Britsch et al. developed and validated an interpretable machine learning algorithm for dynamic 48-hour mortality prediction, updated every 24 hours throughout the ICU stay, using electronic health records from 9,786 ICU patients treated between 2018 and 2022 at a German university hospital, with external validation on the MIMIC-IV database (Communications Medicine, October 2025). This is nearly the same clinical framing as HEMO-ACT (repeated daily risk updates, short-horizon deterioration prediction, interpretability via a tree-based rather than deep model) at roughly twelve times the cohort size and with genuine external validation — a direct comparator the authors needed to engage with and did not. In the HSCT-specific sub-domain, Zhou et al. showed that incorporating longitudinal post-transplant clinical measurements, rather than baseline-only features, improves both short- and long-term mortality risk prediction after allogeneic HCT, validated externally across two institutions (Blood Advances, 2024) — again a directly relevant, uncited precedent for the "dynamic beats static" argument HEMO-ACT is built around. Within the manuscript's own reference list, Boldingh et al. (Crit Care Explor, 2024) and Shickel et al.'s DeepSOFA (Sci Rep, 2019) are the closest acknowledged comparators, but neither is discussed in enough depth to establish what HEMO-ACT adds beyond architectural novelty. A 2025 systematic review of ICU mortality ML models further notes that gradient-boosted trees and logistic regression, not deep sequence models, remain the dominant and best-externally-validated approach in this literature — a pattern consistent with HEMO-ACT's own finding that a CNN-GRU variant beats XGBoost by only a modest margin (R² 0.257 vs. 0.191) on a cohort two orders of magnitude smaller than typical deep-learning training sets, raising a legitimate overfitting concern the manuscript does not address.

---

### 7. Suggested Reviewers' Names

**Temporal modeling / imputation:** Simone Britsch; Tobias Becher; Yiwang Zhou; Benjamin Shickel.
**Interpretability (SHAP/temporal attribution):** Jesse Smith; Cai Li; Roni Shouval.
**Clinical (hematology-critical care/HSCT ICU):** Lisa F. Boldingh; Bruno L. Ferreyro; Djamel Mokart; Akshay Sharma.

---

### Further Literature (Past 3 Years, Similar Scope)

1. **Britsch S, Britsch M, Lindner S, et al.** "An interpretable machine learning algorithm enables dynamic 48-hour mortality prediction during an ICU stay." *Communications Medicine* 5:426 (2025). DOI: 10.1038/s43856-025-01192-z. Peer-reviewed. Uncited by manuscript. No author overlap. LightGBM, n=9,786, updated every 24h, external validation on MIMIC-IV. The closest direct competitor to HEMO-ACT's central claim — same "dynamic beats static, updated daily" framing, general ICU rather than hematology-specific, but with external validation HEMO-ACT lacks.

2. **Zhou Y, Smith J, Keerthi D, et al.** "Longitudinal clinical data improve survival prediction after hematopoietic cell transplantation using machine learning." *Blood Advances* 8(3):686–698 (2024). DOI: 10.1182/bloodadvances.2023011752. Peer-reviewed. Uncited. No author overlap. Random forest on serial post-transplant labs, externally validated across St. Jude and MSKCC cohorts. Hematology-specific precedent for "longitudinal beats baseline-only," using classical ML rather than a CNN-GRU sequence model.

3. **Boldingh JHL, et al.** "Development and Validation of a Prediction Model for 1-Year Mortality in Patients With a Hematologic Malignancy Admitted to the ICU." *Critical Care Explorations* 6:e1093 (2024). DOI: 10.1097/CCE.0000000000001093. Peer-reviewed. **Already cited by manuscript (reference 21)** but underdeveloped in the Discussion; longer-horizon (1-year) static outcome versus HEMO-ACT's short-horizon dynamic outcome — a scope distinction the manuscript should make explicit rather than lumping together.

4. **Mussetti A, Rius-Sansalvador B, Moreno V, et al.** "Artificial Intelligence Methods to Estimate Overall Mortality and Non-Relapse Mortality Following Allogeneic HCT in the Modern Era: An EBMT-TCWP Study." *Bone Marrow Transplantation* 59(2):232–238 (2024). DOI: 10.1038/s41409-023-02147-5. Peer-reviewed. Uncited. No author overlap. Multicenter EBMT registry AI model for post-HCT mortality; static, pre-transplant-weighted features rather than daily ICU trajectories, but directly relevant as a multicenter benchmark HEMO-ACT's single-center design lacks.

5. **Asteris PG, Armaghani DJ, Gandomi AH, et al.** "Survival Prediction in Allogeneic Haematopoietic Stem Cell Transplant Recipients Using Pre- and Post-Transplant Factors and Computational Intelligence." *Journal of Cellular and Molecular Medicine* 29(16):e70672 (2025). DOI: 10.1111/jcmm.70672. Peer-reviewed. Uncited. No author overlap. n=564, soft-computing ensemble, 93.26% accuracy on survivorship classification using 7 parameters. Notably parsimonious relative to HEMO-ACT's 25-variable input; worth citing as a counterpoint on whether HEMO-ACT's feature complexity is necessary.

6. **Zheng Z, Luo J, Zhu Y, et al.** "Development and Validation of a Dynamic Real-Time Risk Prediction Model for Intensive Care Units Patients Based on Longitudinal Irregular Data: Multicenter Retrospective Study." *Journal of Medical Internet Research* 27:e69293 (2025). DOI: 10.2196/69293. Peer-reviewed. Uncited. No author overlap. Time-aware bidirectional attention-LSTM, n=176,344 ICU stays across MIMIC-IV and eICU-CRD, hourly updates, external cross-validation and subgroup fairness analysis — the subgroup/fairness analysis HEMO-ACT's pediatric-inclusive cohort notably omits.

7. **Choi H, Kim Y, Kang H, et al.** "Monitoring ICU Mortality Risk with A Long Short-Term Memory Recurrent Neural Network." *Scientific Reports* 14(1):17723 (2024). DOI: 10.1038/s41598-024-68663-6. Peer-reviewed. Uncited. No author overlap. Continuous (rather than fixed-horizon) LSTM-based mortality monitoring across the full ICU encounter; a methodological alternative to HEMO-ACT's fixed 0/24/48h heads worth discussing as a design choice, not just a baseline.

8. **Mesinovic M, et al.** "Explainable machine learning for predicting ICU mortality in myocardial infarction patients using pseudo-dynamic data." *Scientific Reports* 15:27887 (2025). DOI: 10.1038/s41598-025-13299-3. Peer-reviewed. Uncited. No author overlap. XGBoost with time-resolved Shapley values, externally validated eICU→MIMIC-IV, AUROC 0.92 at 6h. Directly relevant methodological comparator for time-resolved SHAP practice — notably, this paper validates interpretability outputs against held-out external data, which HEMO-ACT's single-center SHAP analysis does not attempt.

9. **Cifci MA, Öney B, Yildirim F, Yilmaz Başer H, Zontul M.** "Interpretable Adaptive Graph Fusion Network for Mortality and Complication Prediction in ICUs." *Diagnostics* 15(22):2825 (2025). DOI: 10.3390/diagnostics15222825. Peer-reviewed. Uncited. No author overlap. Combines a short-horizon convolutional encoder with a long-horizon recurrent module plus SHAP, architecturally the closest published analogue to HEMO-ACT's CNN-GRU-SHAP design, but trained on >200,000 eICU admissions with in-hospital mortality AUROC 0.96 — the scale gap underscores HEMO-ACT's overfitting risk on n=827.

10. **[UNREVIEWED PREPRINT]** Anonymous authors. "Think as a Doctor: An Interpretable AI Approach for ICU Mortality Prediction" (ProtoDoctor). *arXiv:2510.11745* (October 2025). No peer review; flagged as such. No author overlap. Prototype-based intrinsic interpretability framework explicitly targeting the same "black-box distrust" motivation HEMO-ACT cites for using SHAP, but via architectural interpretability rather than post-hoc attribution — relevant as an alternative interpretability paradigm the Discussion should at least acknowledge, with the caveat that it remains unreviewed.

056899
## Editorial Integrity Alert (to Handling Editor)

Two issues require resolution before this manuscript can proceed, independent of scientific merit.

**Citation accuracy.** The manuscript attributes the concept of "technical capital in the computer-driven era" to Bourdieu (2005:75-80), citing *The Social Structures of the Economy*. That book is a study of the French housing market in Val-d'Oise and contains no treatment of technical capital or computing. Either the citation is mischaracterized or the page reference is wrong; this needs correction before the theoretical apparatus can be trusted.

**Sampling-claim inconsistency.** The methods section claims purposive sampling "to hold the sample from rural and western regions" (l.897-898), yet every attributed quotation in the Results is sourced to "a doctor/specialist at a Grade A hospital" — the elite, urban, center-of-the-field institutions the paper's thesis argues dominate the periphery. No rural, primary-care, or patient-side voice appears anywhere in the evidence presented.

---

## 1. Overall Assessment

The manuscript argues, via Bourdieu's concepts of capital, habitus, and field, that China's AI-driven digital medicine and remote healthcare is a state-directed process that redistributes symbolic legitimacy but not real capital, reproducing and in places widening urban-rural and center-periphery inequality. The evidentiary base is 48 semi-structured interviews with medical practitioners, analyzed thematically in NVivo.

The theoretical application is fluent but the empirical foundation is thin. Every quantitative claim driving the argument — AI diagnostic accuracy falling from over 90% in eastern cities to 70% in the west, over 90% of AI research concentrated in developed areas, over 95% of specialists in Grade A urban institutions — is a single informant's unverified assertion, repeated in the Results and Discussion as established fact ("the data show," "this article reveals") rather than as reported perception. No technical audit, published dataset, or independent source is cited to corroborate any of these figures.

## 2. Strengths

The mapping of China's 2025 "Implementation Opinions on Promoting and Regulating the Application of 'AI + Healthcare'" (Table 1) onto Bourdieu's symbolic-capital argument is concrete and well-evidenced; naming the actual policy document and its stated 2027/2030 rollout targets grounds an otherwise abstract claim about state-conferred legitimacy.

Table 2's catalog of named platforms — Ant Group's AI Health Steward AQ, Tencent's Smart Wearables + AI Medical Large Model, JD Internet Hospital, Alibaba's remote healthcare cloud-network — with deployment figures (hospitals connected, users served, compliance rates) supplies genuine empirical texture rarely present in theory-driven qualitative work.

The DRG/DIP reimbursement-exclusion chain for geriatric care (no reimbursement → no geriatricians → no AI validation → no elderly-care AI) is a specific, non-trivial institutional mechanism, and is the paper's strongest original contribution.

## 3. Weaknesses

The accuracy-disparity and resource-concentration statistics are the paper's central empirical claims, yet none are triangulated against any technical source. Directly relevant validation work exists — for example a 2025 *npj Digital Medicine* simulated-patient study quantifying AI chatbot diagnostic disparities in China — and its absence from both the literature review and the discussion of these figures is a material omission.

The sampling problem noted above is not cosmetic: it removes the only evidence that could substantiate the paper's claim about lived peripheral exclusion. A study about the periphery that quotes only the center cannot support its own thesis.

Qualitative rigor is underspecified. One author conducted, coded, and interpreted all 48 interviews with no second coder, no inter-rater statistic, and no member-checking; there is no reflexivity statement addressing the author's positionality as a Cambridge sociologist of education (with a prior monograph applying Bourdieu to education choice) newly applying the same framework to clinical AI.

The Bourdieu (2005) citation error compounds this: the "technical capital" construct that anchors the entire analytic apparatus rests on a citation that does not support it.

## 4. Editorial Decision

**Reject.** The unverifiable central statistics, a sample that structurally cannot evidence the paper's own thesis, and a mischaracterized foundational citation are not resolvable through revision within a normal review cycle; they require new data collection and reconstruction of the theoretical grounding, not editing. Transfer recommendation: *Communications Medicine*, section on health policy and systems, contingent on the authors correcting the citation, adding rural/primary-tier informants, and substantiating or removing the disputed statistics.

## 5. Suggested Reviewer Expertise

Bourdieusian/STS methodology applied to health systems (field, capital, habitus in clinical settings); algorithmic fairness and subgroup performance disparity in clinical AI; qualitative research rigor and trustworthiness criteria (coding reliability, saturation, reflexivity) in health services research; China health-system political economy and rural-urban resource governance; geriatric care financing and DRG/DIP reimbursement policy.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The empirical study of AI performance disparity in Chinese healthcare has moved past anecdote: a 2025 *npj Digital Medicine* simulated-patient study directly measured diagnostic accuracy and over-prescription tendencies across AI chatbots (ERNIE Bot, ChatGPT, DeepSeek) versus human physicians, building on an established standardized-patient audit tradition (Sylvia et al., Si et al.) documenting real quality-of-care gaps in rural Chinese clinics. The foundational text on algorithmic bias from unrepresentative training data, Obermeyer et al. (*Science*, 2019), demonstrating that a widely used US health algorithm systematically underserved Black patients due to biased training labels, is the direct technical antecedent to this manuscript's central claim about elite-hospital training data — yet is not cited. Recent reviews of AI deployment across Chinese tertiary hospitals (DeepSeek integration case series, 2025) document the platform landscape this manuscript describes but with operational rather than sociological framing. The manuscript's contribution is the Bourdieusian institutional lens itself, which is genuinely underused in this literature; its failure is not engaging the quantitative disparity literature that could have substantiated rather than merely asserted its claims.

## 7. Suggested Reviewers' Names

STS/Bourdieusian health methodology: Alex Broom; Simon Carmel; Davina Allen.
Algorithmic fairness in clinical AI: Ziad Obermeyer; Marzyeh Ghassemi; Irene Chen.
China health-system political economy: Winnie Yip; Yang Zhou; Karen Eggleston.

Would you like this condensed to 300-400 words for sections 1-4 with Further Literature appended, per your usual second pass?

057058
Good — 312 words, tight against the 300 target. Here is the revised report.

---

## Editorial Report — Manuscript 057058

**"Auditable medical reasoning with knowledge-grounded large language models" (REMEDY)**

---

**1. Overall Assessment**

REMEDY grounds LLM medical QA in a UMLS-derived knowledge graph via two channels: a Basic Channel matching LLM-generated relation plans to KG paths scored by a RotatE embedding model, and an Enhanced Channel that iteratively explores the graph when matching fails, producing per-path confidence scores. Evaluated across five QA benchmarks, six baselines, four open-source backbones, and five closed-source LLMs, REMEDY shows consistent gains and strong robustness to KG edge removal. The clinical-auditability claim, however, is tested only on multiple-choice benchmarks, with no subgroup analysis and weak separation between random-path and candidate-path confidence scores — the two issues most likely to drive the decision below.

**2. Strengths**

The dual-channel fallback is architecturally meaningful: unlike RoG's fixed pipeline or ToG's undifferentiated beam search, REMEDY degrades gracefully under KG sparsity, losing only 5 accuracy points after 80% edge removal versus 13–21 points for KG-SFT and KAPING. The cross-backbone analysis uses matched optimizer settings to isolate method effects from training confounds, and the reasoning-depth stratification offers a credible mechanistic account of when each channel activates.

**3. Weaknesses**

Evaluation never leaves structured exam-style QA or Freebase-based open-domain QA; the Discussion names the resulting "evaluation illusion" without addressing it, and no free-text clinical note or subgroup breakdown by age, sex, ethnicity, or specialty appears anywhere. The auditability claim rests on a narrow score gap between random paths (0.45) and candidate paths (0.49), with no calibration metric reported. Reproducibility is weakened by sourcing the MMLU-Pro, MedMCQA, and PubMedQA splits from MedReason's repository, an unreviewed preprint, and by withholding the constructed 92,324-entity KG itself.

**4. Editorial Decision**

**Reject.** A system framed around clinical decision support and auditability cannot rest its evidentiary claims on exam-style accuracy with no subgroup analysis and no calibration validation of its own confidence score; this is a design-level gap, not a revisable reporting omission. Transfer to **npj Digital Medicine** is recommended, where the technical contribution can be judged without this venue's clinical-translational bar.

**5. Suggested Reviewer Expertise**

Reviewers should cover: knowledge graph embedding methods (RotatE and translational/rotational KGE models) for biomedical plausibility scoring; planning-retrieval-reasoning and iterative graph-search pipelines for LLM-KGQA (RoG/ToG-style methods); LoRA-based fine-tuning and evaluation methodology for medical reasoning benchmarks, including calibration assessment; and clinical informatics expertise in evaluating AI diagnostic-reasoning tools against real (non-multiple-choice) clinical text, ideally with internal medicine or nephrology background given the electrolyte-disorder case study in Fig. 5.

**6. State-of-the-Art Literature Review (Past 3 Years)**

The field has moved from static KG-injection (KAPING, StructGPT) toward iterative, LLM-guided graph traversal (ToG, ICLR 2024; RoG, ICLR 2024) and, more recently, toward KG-driven fine-tuning (KG-SFT, ICLR 2025, average 8.7-point gain in low-data settings) and reasoning-dataset construction (MedReason, arXiv 2025, still unreviewed). A directly relevant and uncited 2024/2025 contribution is KARE (Jiang et al., ICLR 2025), which integrates hierarchical KG-community retrieval with LLM reasoning for interpretable clinical mortality and readmission prediction — conceptually adjacent to REMEDY's confidence-scored path retrieval but targeting real EHR outcome prediction rather than exam QA, and its omission from the competitive landscape is a real gap. REMEDY's dual-channel fallback is a legitimate advance over ToG's undifferentiated beam search, but its clinical-auditability framing has not engaged the EHR-grounded work (DR.KNOWS, JMIR AI 2025; KARE) that actually tests interpretability against clinical outcomes rather than multiple-choice accuracy.

**7. Suggested Reviewer Names**

Linhao Luo (RoG, ICLR 2024) — path-planning KGQA; Hanzhu Chen (KG-SFT, ICLR 2025) — KG-driven fine-tuning; Pengcheng Jiang (KARE, ICLR 2025) — KG-community retrieval for clinical prediction; Yanjun Gao (DR.KNOWS, JMIR AI 2025) — clinical informatics and EHR-grounded diagnostic reasoning evaluation.

---

## Further Literature (Past 3 Years, Similar Scope)

**1.** Jiang, P., Xiao, C., Jiang, M., Bhatia, P., Kass-Hout, T., Sun, J., Han, J. "Reasoning-Enhanced Healthcare Predictions with Knowledge Graph Community Retrieval." *ICLR 2025*. DOI: 10.48550/arXiv.2410.04585. **Uncited by manuscript.** No author overlap detectable (REMEDY's manuscript is blinded with no author list; independence cannot be fully confirmed but no institutional signal suggests overlap). KARE integrates hierarchical KG-community retrieval with LLM reasoning for clinical mortality/readmission prediction — the closest peer-reviewed prior work to REMEDY's core premise of combining KGE-style retrieval with LLM reasoning for auditable clinical output, but validated against real EHR outcomes (MIMIC-III/IV) rather than exam QA, directly exposing REMEDY's evaluation gap.

**2.** Luo, L., Zhao, Z., Gong, C., Haffari, G., Pan, S. "Graph-Constrained Reasoning: Faithful Reasoning on Knowledge Graphs with Large Language Models." *ICML 2025*. DOI: 10.48550/arXiv.2410.13080. **Uncited by manuscript.** Same lead author as RoG (which REMEDY does cite and benchmark against, ref. 26); no overlap with REMEDY's own (unknown) authorship. GCR constrains LLM decoding directly with a KG-trie rather than post-hoc path scoring, achieving zero reasoning hallucination and strong zero-shot transfer to unseen KGs — a more recent and architecturally distinct alternative to REMEDY's two-channel scoring approach that the manuscript should have positioned itself against.

**3.** Ma, S., Xu, C., Jiang, X., Li, M., Qu, H., Yang, C., Mao, J., Guo, J. "Think-on-Graph 2.0: Deep and Faithful Large Language Model Reasoning with Knowledge-Guided Retrieval Augmented Generation." *ICLR 2025*. DOI: 10.48550/arXiv.2407.10805. **Uncited by manuscript; direct successor to the ToG baseline REMEDY does benchmark (ref. 20).** No detectable author overlap. ToG-2 hybridizes structured KG traversal with unstructured document retrieval in a tight coupling loop; REMEDY compares only against the older, weaker ToG-1, which inflates its reported margin of improvement over the true current state of the art.

**4.** Wu, J., Zhu, J., Qi, Y., Chen, J., Xu, M., Menolascina, F., Grau, V. "Medical Graph RAG: Towards Safe Medical Large Language Model via Graph Retrieval-Augmented Generation." *ACL 2025* (originally arXiv:2408.04187, Aug 2024). **Uncited by manuscript.** No author overlap. MedGraphRAG builds a triple-linked medical KG with source-document grounding specifically to produce citable, evidence-traceable clinical responses — directly competing with REMEDY's "auditable evidence path" framing but validated with human evaluation of response safety, a dimension entirely absent from REMEDY's evaluation.

**5.** Xiong, G. (or Xu, X. in some citation variants), et al. "MedRAG: Enhancing Retrieval-Augmented Generation with Knowledge Graph-Elicited Reasoning for Healthcare Copilot." *Proceedings of the ACM Web Conference (WWW) 2025*. DOI: 10.1145/3696410.3714782. **Uncited by manuscript.** No author overlap. MedRAG uses KG-elicited diagnostic reasoning chains for a clinical decision-support copilot rather than static exam benchmarks, offering a template for the kind of interactive, clinician-facing validation REMEDY's Discussion says is needed but does not attempt.

**6.** Mavromatis, C., Karypis, G. "GNN-RAG: Graph Neural Retrieval for Efficient Large Language Model Reasoning on Knowledge Graphs." *Findings of ACL 2025*. DOI: 10.18653/v1/2025.findings-acl.856. **Uncited by manuscript, despite being evaluated on the identical WebQSP and CWQ benchmarks REMEDY reports in Fig. 4f.** No author overlap. GNN-RAG uses a GNN rather than an LLM planner to retrieve reasoning paths, reporting 8.9–15.5 point F1 gains on multi-hop questions with 9× fewer KG tokens than long-context baselines — a directly comparable, higher-efficiency alternative that REMEDY's open-domain generalization claim (Section 2.4) should have benchmarked against rather than only RoG and an LLM-only baseline.
