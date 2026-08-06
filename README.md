# Trackrad202512456

044278
### Reviewer 1 summary

The reviewer considers the large-scale, real-world deployment potentially important but identifies major threats to validity. The comparison between RAG, Workflow-LLM, and HEALER uses different time periods and patient cohorts, so improvements cannot be attributed causally to HEALER. The reviewer also questions the representativeness of the 1,268 manually evaluated consultations, the limited analysis of 24 mandatory escalation failures, the absence of clinical outcomes, the use of an LLM judge, incomplete statistical reporting, insufficient multi-site ethics documentation, conflicts of interest, and limited reproducibility. 

### Reviewer 2 summary

The reviewer views the manuscript as a distinctive multi-centre deployment study but finds substantial methodological and reporting omissions. Key details are missing on the RAG system, hierarchical agent architecture, models, prompts, deployment costs, data cleaning, physician evaluation, statistical tests, sentiment analysis, and escalation-event sampling. The reviewer also requests stronger controls for temporal confounding, more detailed safety analyses, clearer terminology, and fuller implementation information.

### Reviewer 3 summary

The reviewer highlights the scale and operational relevance of HEALER but recommends substantial revision. Main concerns include causal overstatement, selection bias in the evaluation subset, inadequate confounder adjustment, failure to distinguish operational outcomes from clinical outcomes, limited generalizability, insufficient external validation, LLM-evaluation bias, unclear reproducibility, incomplete implementation reporting, and weak statistical transparency.

### Overall assessment

The reviewers agree that the manuscript has potential significance because of its deployment across 134 hospitals and more than 80,000 interactions. However, the evidence currently supports an observational operational evaluation, not claims of causal improvement, clinical benefit, or established safety. The most serious issues are confounding across deployment periods, unclear sampling, insufficient analysis of escalation failures, and incomplete ethical and methodological reporting.

### Decision

**Major Revision.** The study is potentially publishable because of its scale and real-world setting, but the current analysis and reporting are insufficient for acceptance. Rejection would be appropriate if the authors cannot resolve the sampling, governance, safety, and confounding concerns.

### Revision recommendations

* Provide a STROBE-style participant and consultation flow diagram.
* Explain how the 1,268 consultations were selected and assess representativeness.
* Adjust for temporal, departmental, demographic, and case-complexity confounding.
* Remove or substantially moderate causal claims.
* Expand analysis of mandatory and discretionary escalation failures.
* Report possible patient harm and adverse outcomes, where available.
* Separate workflow outcomes from clinical outcomes.
* Validate the LLM-based evaluator against independent human ratings.
* Report models, prompts, agent orchestration, retrieval logic, tools, latency, and costs.
* Clarify statistical tests, confidence intervals, and multiple-comparison correction.
* Document ethics approval, consent, AI disclosure, privacy, and governance across all hospitals.
* Clarify conflicts of interest, proprietary components, data availability, and reproducibility.

061079
# Editorial Report: BEGINN: BSPM-EGM Inference using Neural Networks for Non-Invasive Atrial Signal Reconstruction in Regular Rhythms

---

## Editorial Integrity Alert (Handling Editor Only)

Two items require resolution before this manuscript proceeds to external review.

First, reference 26 (Gutiérrez-Fernández et al., *Frontiers in Physiology*, 2026), cited as "the most recent and methodologically comparable deep learning approach" with CC = 0.37–0.42, shares three co-authors (Fambuena-Santos, Guillem, Climent) with the submitted manuscript and originates from the same institute (ITACA, Universitat Politècnica de València). The verified figures are accurate, but the manuscript frames this as an independent external benchmark without disclosing the authorship overlap. This is a disclosure issue, not fabrication, and is resolvable by revision.

Second, the simulation database's 42 atrial/torso geometries used to build the training statistical shape model and the clinical validation cohort's 42 patients are described using identical language and count. The manuscript does not clarify whether these are the same or a disjoint population. If the clinical cohort contributed to or overlaps with the SSM training geometries, this constitutes an undisclosed train–test relationship (indirect, via anatomy rather than raw signal) that would need explicit resolution — potentially reverting the decision toward rejection. Authors must clarify this in any revision.

---

## 1. Overall Assessment

BEGINN is a geometry-free 3D CNN–LSTM autoencoder reconstructing atrial electrograms from body surface potentials, targeting classical Tikhonov ECGI's two core weaknesses: over-smoothing and geometric sensitivity. Trained on 16,800 simulations from 42 anatomies, it is validated in silico and in a 60-recording, 42-patient, three-hospital clinical cohort.

The in silico case is strong: BEGINN is invariant to a geometric perturbation that collapses classical ECGI's correlation from 0.73 to 0.42. But the clinical validation, which should carry the paper, shows non-inferiority, not superiority — McNemar's test found no significant localization difference (cavity 88.3% vs. 93.3%, p = 0.55; neighboring 85% vs. 88.3%, p = 0.79), with classical ECGI numerically ahead on both. The superiority narrative instead rests on unvalidated secondary morphology metrics.

---

## 2. Strengths

The training design is disciplined: leakage-free 28/7/7 geometry splits and clinically grounded positional-perturbation ranges (±20 mm, ±20°/±15°). The multicenter clinical validation — 60 pacing recordings, 42 patients, three hospitals, blinded scoring, McNemar's test — is genuinely rare for this sub-field; competing geometry-free deep learning ECGI work remains simulation-only or single-center. The authors are commendably explicit that regional pacing accuracy confirms only labeled activation origin, not full propagation-pattern fidelity, given no invasive electroanatomical ground truth. Electrode-dropout training targets a real deployment failure mode — contact loss, high-impedance leads — rather than an idealized full-vest scenario.

---

## 3. Weaknesses

The primary clinical endpoint does not support the superiority claim: cavity and neighboring accuracy showed no significant difference, with classical ECGI numerically higher on both. The pivot to focality area and maximum slope as evidence is unvalidated against an independent substrate reference, and the Monte Carlo dropout uncertainty described in Methods — the tool that could substantiate this — is never reported in Results. Whether the 42 SSM training anatomies overlap with the 42 clinical validation patients is unclarified (see Integrity Alert). Engagement with the directly competing, concurrent geometry-free diffusion approach (Jara & Meyers, 2026) is superficial, and no external hospital was held out for site-level generalizability.

---

## 4. Editorial Decision

**Major Revision.** The architecture and clinical validation effort are genuine, and no fabrication is evident, but the superiority narrative is unsupported by its own primary endpoint, and the disclosure gaps above must be resolved first. If the geometry/patient overlap proves to be genuine contamination, the decision reverts to Reject.

**Counterargument:** Geometric robustness by design may itself be the clinically relevant contribution, independent of an underpowered (n = 60) localization comparison — a fair point that favors revision over rejection, provided the manuscript is honest about what the clinical data does and does not show.

---

## 5. Suggested Reviewer Expertise

Reviewers should be drawn primarily from technical backgrounds, with clinical expertise calibrated to persistent AF ablation. Needed technical expertise: deep learning architectures for the inverse problem of electrocardiography, specifically geometry-free and generative (diffusion, variational) approaches to BSPM-to-electrogram mapping; boundary element method forward modeling and Tikhonov/L-curve regularization as applied to atrial ECGI, sufficient to assess whether the classical comparator was optimally tuned; statistical shape modeling of cardiac and torso anatomy and its role in quantifying geometric uncertainty; and Bayesian or noise-robust local activation time estimation methodology. Clinical expertise should cover catheter ablation of persistent atrial fibrillation with specific experience in non-pulmonary-vein trigger and driver-guided ablation, ideally including prior use of ECGI or panoramic mapping systems to select ablation targets.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

Geometry-free deep learning ECGI has moved from a theoretical possibility to an active, competitive sub-field within the past several months. Gutiérrez-Fernández et al. (2026) proposed a dual-branch variational autoencoder for atrial electrogram estimation trained on 680 simulated BSPM–EGM pairs spanning sinus rhythm, multirotor AF, ectopic foci, and fibrotic substrates, reporting correlation coefficients of 0.37–0.42 for AF and 0.42–0.66 for sinus rhythm against zero-order Tikhonov — a smaller and more heterogeneous training set than BEGINN's, but notably including irregular rhythms and fibrotic substrate that BEGINN's regular-rhythm-only training database does not cover. Independently, Jara and Meyers (arXiv, January 2026) introduced a geometry-free conditional diffusion model for the same inverse problem, evaluated against CNN, LSTM, and transformer baselines on real ECGI data, with the explicit advantage of probabilistic multi-sample reconstruction rather than a single deterministic estimate. In the ventricular domain, Wang et al. (2025, *Artificial Intelligence in Medicine*) used a Pix2Pix architecture with a cosine-similarity loss for heart-surface potential reconstruction during ventricular pacing, and He et al. (2025) reported correlation coefficients exceeding 0.90 using an attention-based network under known geometry, while Pilia et al. (2023) demonstrated that ventricular localization error rises from under 3 mm to 32–47 mm once patient-specific geometry is removed — the same domain gap BEGINN targets in the atrial setting.

Against this landscape, BEGINN's genuine advance is the first multicenter, pacing-validated clinical demonstration that a geometry-free deep learning atrial ECGI model can match classical ECGI's regional localization accuracy while remaining structurally immune to geometric mismatch. It does not, however, address irregular or fibrotic rhythms as the VAE work does, nor does it exploit uncertainty quantification as the concurrent diffusion approach does, and the manuscript would benefit from directly engaging both as competing rather than merely adjacent directions.

---

## 7. Suggested Reviewers' Names

**Technical expertise:**
- Steffen Schuler (Karlsruhe Institute of Technology) — spatio-temporal basis methods for atrial ectopic ECGI localization; author of the noise-robustness benchmark (7.9 mm at 0 dB) directly cited in this manuscript.
- Adam Meyers (Assistant Professor, University of Miami) — geometry-free conditional diffusion modeling for the inverse ECG problem; directly competing, independent architecture.
- Jaume Coll-Font (Massachusetts General Hospital / Harvard Medical School) — geometric uncertainty and cardiac position sensitivity in ECGI forward/inverse modeling.

**Clinical expertise:**
- Shohreh Honarbakhsh (Consultant Electrophysiologist, Barts Health NHS Trust) — ECGI-guided driver ablation in persistent AF; principal investigator, TARGET-AF1 trial.
- Ghassen Cheniti (Bordeaux University Hospital, LIRYC Institute) — non-invasive mapping and electrocardiographic imaging in atrial and ventricular arrhythmia ablation.

---

## Further Literature (Past 3 Years)

1. **Li, L., Camps, J., Rodriguez, B. & Grau, V.** Solving the Inverse Problem of Electrocardiography for Cardiac Digital Twins: A Survey. *IEEE Reviews in Biomedical Engineering* 18, 316–336 (2025). DOI: 10.1109/RBME.2024.3486439. Peer-reviewed. Not cited by manuscript. Independent (Oxford). Comprehensive recent survey spanning physics-based and deep learning ECGI inverse methods, including graph-based and hybrid architectures; situates BEGINN's specific architectural choices against the full current landscape it otherwise cites only piecemeal.

2. **Jiang, X. et al.** Hybrid Neural State-Space Modeling for Supervised and Unsupervised Electrocardiographic Imaging. *IEEE Transactions on Medical Imaging* (2024). PMID: 38478452. Peer-reviewed. Not cited. Independent. Combines a physics-based forward operator with a learned neural transition function, including unsupervised validation on in-vivo data without EGM ground truth — directly relevant to BEGINN's own acknowledged inability to validate reconstructed propagation fidelity against invasive mapping.

3. **Li, L., Camps, J., Wang, Z.J., Beetz, M., Banerjee, A., Rodriguez, B. & Grau, V.** Toward Enabling Cardiac Digital Twins of Myocardial Infarction Using Deep Computational Models for Inverse Inference. *IEEE Transactions on Medical Imaging* 43, 2466–2478 (2024). DOI: 10.1109/TMI.2024.3367409. Peer-reviewed. Not cited. Independent. Ventricular/substrate-focused analog of BEGINN's atrial trigger-localization goal; offers a template for linking reconstructed fields to substrate characterization, a step BEGINN defers to future work.

4. **Wang, T., Karel, J.M.H., Bonizzi, P. & Peeters, R.L.M.** Influence of the Tikhonov Regularization Parameter on the Accuracy of the Inverse Problem in Electrocardiography. *Sensors* 23(4), 1841 (2023). Peer-reviewed. Not cited. Independent (Maastricht). Directly examines sensitivity of L-curve-selected Tikhonov regularization — the exact method used for BEGINN's classical ECGI comparator — relevant to whether that baseline was optimally tuned.

5. **Yadan, Z., Jian, L., Jian, W., Yifu, L., Haiying, L. & Hairui, L.** An Expert Review of the Inverse Problem in Electrocardiographic Imaging for the Non-Invasive Identification of Atrial Fibrillation Drivers. *Computer Methods and Programs in Biomedicine* 240, 107676 (2023). Peer-reviewed. Not cited. Independent. Recent expert review focused specifically on AF-driver ECGI; situates BEGINN's regular-rhythm-only scope against the irregular-rhythm AF driver problem it explicitly defers.

6. **Gutiérrez-Fernández, M., López-Linares, K., Fambuena-Santos, C., Guillem, M.S., Climent, A.M. & Barquero-Pérez, Ó.** Deep Learning for Atrial Electrogram Estimation: Toward Non-Invasive Arrhythmia Mapping Using Variational Autoencoders. *Frontiers in Physiology* 16, 1720244 (2026). DOI: 10.3389/fphys.2025.1720244. Peer-reviewed. **Cited by manuscript (ref 26).** **Not independent** — shares three co-authors with the submission (see Integrity Alert). Dual-branch VAE trained on 680 pairs covering sinus, multirotor AF, ectopic foci, and fibrotic substrate — broader rhythm coverage than BEGINN's regular-rhythm-only database, on a smaller dataset.

7. **Valdes Jara, R. & Meyers, A.** Geometry-Free Conditional Diffusion Modeling for Solving the Inverse Electrocardiography Problem. arXiv:2601.18615 (2026). **Preprint, not peer-reviewed.** Cited by manuscript (ref 19), but only briefly. Independent (University of Miami). The most direct architectural competitor: geometry-free, evaluated on real ECGI data against CNN/LSTM/transformer baselines, with native probabilistic uncertainty quantification that BEGINN's MC-dropout output could have been benchmarked against but was not.

8. **Wang, T. et al.** Deep Learning Based Estimation of Heart Surface Potentials. *Artificial Intelligence in Medicine* 163, 103093 (2025). Peer-reviewed. Cited by manuscript (ref 21). Independent (Maastricht). Pix2Pix-based ventricular surface-potential reconstruction (CC ≈ 0.64); useful cross-chamber benchmark for BEGINN's atrial correlation figures.

9. **He, S. et al.** AI-Powered Noninvasive Electrocardiographic Imaging Using the Priori-to-Attention Network (P2AN) for Wearable Health Monitoring. *Sensors* 25, 1810 (2025). Peer-reviewed. Cited by manuscript (ref 32). Independent. Reports CC > 0.90 under known ventricular geometry, illustrating the accuracy ceiling geometry-aware methods can reach and the trade-off BEGINN accepts by discarding geometry.

10. **Pilia, N. et al.** Non-Invasive Localization of the Ventricular Excitation Origin Without Patient-Specific Geometries Using Deep Learning. *Artificial Intelligence in Medicine* 143, 102619 (2023). Peer-reviewed. Cited by manuscript (ref 33). Independent (KIT). Documents the same geometry-dependency domain gap BEGINN targets (localization error rising from <3 mm to 32–47 mm without patient geometry), but in the ventricle; the closest direct precedent for BEGINN's core "geometry-free by design" argument.

062269
## 1. Overall Assessment

The manuscript presents ThyroidXAgent, a clinician-interactive system coordinating thyroid-ultrasound segmentation, benign–malignant classification, lymph-node metastasis prediction, opportunistic screening and structured report generation. Its main contribution is an auditable evidence store that preserves intermediate outputs, measurements, retrieved evidence and clinician corrections. The study combines OpenThyroidDB with multicentre institutional cohorts and evaluates diagnostic performance, report quality and workflow efficiency. 

This is more substantial than an isolated benchmarking study because it integrates multiple diagnostic tasks and permits clinician correction. However, the breadth of the system exceeds the validation depth of several components. The key concerns are uneven external validation across modules and the absence of prospective evidence that the reported efficiency gains improve clinical decisions or patient outcomes.

## 2. Strengths

The multicentre evaluation is strong. Segmentation and classification are assessed across TN3K, TN5K, ThyroidXL, DDTI, PKTN, ZJH-RK and RJH-TK using Dice, HD95, AUROC, AUPRC and confidence intervals.

The architecture is clinically coherent. Segmentation, classification, attribution, lymph-node assessment and report generation remain separate and inspectable. Clinicians can correct masks and measurements before downstream reporting.

The 145-case reader study reports improved diagnostic consistency and reductions in reporting time of approximately 36% for physicians and 27% for doctors. ThyClinScore also evaluates lesion-level factual completeness rather than lexical overlap alone.

## 3. Weaknesses

The reader study is retrospective and interface-mediated. It does not measure biopsy recommendations, surgical referrals, missed malignancies, patient outcomes or routine PACS deployment.

Validation is uneven. Segmentation and classification receive broad testing, whereas lymph-node prediction, opportunistic screening and report generation use fewer institutional cohorts.

Subgroup performance by age, sex, scanner, thyroiditis, nodule size and TI-RADS category is inadequately reported. Calibration, decision-curve analysis and clinically selected operating thresholds are also missing.

ThyClinScore is author-developed and partly dependent on an LLM judge. Independent blinded validation and detailed factual-error analysis are required.

## 4. Editorial Decision

**Send for Review.** Reviewers should adjudicate cohort separation, module-specific external validity, report-evaluation independence and whether the reader study supports the claimed clinical utility.

## 5. Suggested Reviewer Expertise

The review team should include expertise in domain-generalized thyroid-ultrasound segmentation and classification; multimodal foundation models and tool-using clinical agents; radiology-report generation and factuality evaluation; diagnostic-model calibration and multicentre reader-study design; and clinical thyroid ultrasonography, TI-RADS assessment and cervical lymph-node staging.

## 6. State-of-the-Art Literature Review

Recent work has moved from isolated thyroid-nodule classifiers toward multimodal and clinically interactive systems. ThyGPT demonstrated an interpretable multimodal copilot for thyroid-nodule risk assessment, while prospective multicentre studies have evaluated AI assistance for junior thyroid-ultrasound readers. Multi-view self-supervised learning has also improved thyroid segmentation and classification under limited annotation. ([nature.com](https://www.nature.com/articles/s41746-025-01652-9?utm_source=chatgpt.com))

Ultrasound report generation is advancing through cross-modal alignment and standardized multilingual vision-language models, while recent foundation-model adaptations address real-time ultrasound segmentation. These studies directly challenge any claim that report generation, multimodal interpretation or foundation-model segmentation is individually novel. ThyroidXAgent’s distinctive contribution is their integration into a clinician-correctable evidence workflow. However, its clinical superiority over focused systems such as ThyGPT and recent report-generation pipelines remains unproven without prospective deployment. ([arxiv.org](https://arxiv.org/abs/2406.00644?utm_source=chatgpt.com))

## 7. Suggested Reviewer Names

Dong Ni would provide relevant expertise in multi-view self-supervised thyroid-ultrasound segmentation and classification. Ying Hu or Zhongliang Jiang would be suitable for ultrasound report generation and cross-modal image–text alignment. Pranav Rajpurkar would provide expertise in clinical evaluation of AI-assisted radiology reporting. An independent thyroid-ultrasound clinician involved in multicentre prospective AI evaluation, such as Jianqiao Zhou, would be appropriate for assessing clinical validity and reader-study design. Conflicts of interest and recent collaborations with the submitting authors should be checked before invitation.

## 8. Further Literature: Ten Closely Related Papers Published Since 2023

1. **Yao J, Wang Y, Lei Z, et al. “Multimodal GPT model for assisting thyroid nodule diagnosis and management.” *npj Digital Medicine*. 2025;8. DOI: 10.1038/s41746-025-01652-9.** Peer-reviewed. The manuscript cites this work. The author group appears independent of the submitting team, subject to formal conflict checking. ThyGPT is the most direct comparator because it combines thyroid-ultrasound interpretation, interactive explanation and management support. Unlike ThyroidXAgent, it is primarily a diagnostic copilot rather than an auditable multi-agent reporting workflow. ([Nature][1])

2. **Zhou Y, Chen C, Xu D, et al. “A deep learning based ultrasound diagnostic tool driven by 3D visualization of thyroid nodules.” *npj Digital Medicine*. 2025;8. DOI: 10.1038/s41746-025-01455-y.** Peer-reviewed. This paper does not appear in the manuscript’s reference list. Author independence should be checked because the research network overlaps with several ThyGPT investigators, although no clear overlap with the submitted author list is evident. TNVis uses dynamic ultrasound video, two-stage segmentation and 3D reconstruction, with development or validation involving 4,569 cases and seven hospitals. It is a stronger comparator for prospective workflow evaluation than static-image benchmarks. ([Nature][2])

3. **Wu S-H, Tong W-J, Li M-D, et al. “Collaborative Enhancement of Consistency and Accuracy in US Diagnosis of Thyroid Nodules Using Large Language Models.” *Radiology*. 2024;310(3):e232255. DOI: 10.1148/radiol.232255.** Peer-reviewed. Cited by the manuscript and apparently independent. The study compares human–LLM interaction, image-to-text–LLM processing and conventional CNN diagnosis. Its image-to-text plus GPT-4 strategy achieved an AUC of 0.83, making it directly relevant to ThyroidXAgent’s report-grounded diagnostic claims and human–AI reader design. ([RSNA Publications Online][3])

4. **Dai F, et al. “Improving AI models for rare thyroid cancer subtype by text guided diffusion models.” *Nature Communications*. 2025;16:4449. DOI: 10.1038/s41467-025-59478-8.** Peer-reviewed and cited by the manuscript. Potential author overlap should be examined carefully because the submitted paper includes a Fei Chen and the full comparator author list must be checked rather than inferred from initials. The study addresses rare thyroid-cancer subtypes using text-guided diffusion augmentation, directly informing ThyroidXAgent’s claims about follicular and uncommon malignant lesions. ([Nature][4])

5. **Jiang Y, Feng C-M, Ren J, et al. “From pretraining to privacy: federated ultrasound foundation model with self-supervised learning.” *npj Digital Medicine*. 2025;8:714. DOI: 10.1038/s41746-025-02085-0.** Peer-reviewed and cited by the manuscript. The author group appears independent. This work develops a federated, self-supervised ultrasound foundation model and is relevant to ThyroidXAgent’s cross-centre generalization claims. It also provides an alternative strategy for institutionally distributed data that avoids central aggregation. ([Nature][5])

6. **Zhang H, et al. “TN5000: An Ultrasound Image Dataset for Thyroid Nodule Detection and Classification.” *Scientific Data*. 2025;12:1437. DOI: 10.1038/s41597-025-05757-4.** Peer-reviewed and cited by the manuscript. The author group appears independent, although collaboration history should be checked. TN5000 supplies a large, openly described thyroid-ultrasound benchmark for detection and classification. It is relevant to the transparency, reproducibility and dataset-composition claims surrounding OpenThyroidDB. ([Nature][6])

7. **Yan L, Zhou X, Wang Y, Chang X, Li Q, Han G. “Automated Ultrasound Diagnosis via CLIP-GPT Synergy: A Multimodal Framework for Image Classification and Report Generation.” *IEEE Access*. 2025;13:107950–107960. DOI: 10.1109/ACCESS.2025.3578462.** Peer-reviewed and cited by the manuscript. The author group appears independent. This CLIP–GPT pipeline jointly performs ultrasound classification and personalized report generation, making it one of the closest technical comparators for ThyroidXAgent’s combined diagnostic and reporting modules. ([IEEE Xplore][7])

8. **Pandita A, et al. “Synthetic data trained open-source language models are comparable to GPT-4 for converting free-text thyroid nodule dictations into structured reports.” *npj Digital Medicine*. 2025;8. DOI: 10.1038/s41746-025-01658-3.** Peer-reviewed and cited by the manuscript. The author group appears independent. The study fine-tunes models including Mistral, Llama and Yi using 3,000 synthetic thyroid dictations and evaluates structured ACR TI-RADS conversion. It directly challenges the need for a large proprietary language model in the report-structuring component. ([Nature][8])

9. **Xu Z, et al. “Fair ultrasound diagnosis via adversarial protected attribute learning.” *npj Digital Medicine*. 2025;8. DOI: 10.1038/s41746-025-01641-y.** Peer-reviewed. This paper does not appear to be cited by the manuscript, and its authors appear independent. It demonstrates that ultrasound segmentation models can show performance disparities across age and sex and proposes adversarial mitigation. It is particularly relevant because ThyroidXAgent does not adequately report demographic subgroup performance or fairness analyses. ([Nature][9])

10. **Li J, Zhang H, Liang P, et al. “Artificial intelligence-enabled ultrasound diagnosis and stratification of follicular thyroid neoplasms: a multi-center study.” *npj Digital Medicine*. 2026. DOI: 10.1038/s41746-026-02489-6.** Peer-reviewed. It is not cited, likely because it appeared after preparation of the submitted manuscript. Author independence requires formal verification. This multicentre study directly overlaps with ThyroidXAgent’s follicular-neoplasm classification objective and should be considered when assessing whether its subtype-stratification module remains state of the art. ([Nature][10])

[1]: https://www.nature.com/articles/s41746-025-01652-9?utm_source=chatgpt.com "Multimodal GPT model for assisting thyroid nodule diagnosis and management | npj Digital Medicine"
[2]: https://www.nature.com/articles/s41746-025-01455-y?utm_source=chatgpt.com "A deep learning based ultrasound diagnostic tool driven by 3D visualization of thyroid nodules | npj Digital Medicine"
[3]: https://pubs.rsna.org/doi/abs/10.1148/radiol.232255?utm_source=chatgpt.com "Collaborative Enhancement of Consistency and Accuracy ..."
[4]: https://www.nature.com/articles/s41467-025-59478-8?utm_source=chatgpt.com "Improving AI models for rare thyroid cancer subtype by text ..."
[5]: https://www.nature.com/articles/s41746-025-02085-0?utm_source=chatgpt.com "From pretraining to privacy: federated ultrasound foundation model with self-supervised learning | npj Digital Medicine"
[6]: https://www.nature.com/articles/s41597-025-05757-4?utm_source=chatgpt.com "TN5000: An Ultrasound Image Dataset for Thyroid Nodule ..."
[7]: https://ieeexplore.ieee.org/iel8/6287639/6514899/11029188.pdf?utm_source=chatgpt.com "Automated Ultrasound Diagnosis via CLIP-GPT Synergy"
[8]: https://www.nature.com/articles/s41746-025-01658-3?utm_source=chatgpt.com "Synthetic data trained open-source language models are ..."
[9]: https://www.nature.com/articles/s41746-025-01641-y?utm_source=chatgpt.com "Fair ultrasound diagnosis via adversarial protected ..."
[10]: https://www.nature.com/articles/s41746-026-02489-6?utm_source=chatgpt.com "Artificial intelligence-enabled ultrasound diagnosis and ..."

062618
## Editorial Integrity Alert — Handling Editor Only

No clear evidence of duplicate publication, fabricated comparators, or undisclosed cohort reuse is apparent. However, generation through the public ChatGPT interface does not establish the exact GPT-5.5 model snapshot, system prompt, decoding configuration, or output date for each text. This limits independent regeneration of the intervention.

## 1. Overall Assessment

This manuscript tests whether LLM-generated communication changes family-member interpretation of critical illness. In a randomised scenario-based study, 2,038 Chinese adults evaluated clinician-written, GPT-5.5-generated, or clinician-refined LLM texts across six ICU conditions. Outcomes included comprehension, misinterpretation, risk perception, decision tendency, and trust. 

The principal finding is consequential: LLM texts improved comprehension and trust but increased misinterpretation and reduced perceived risk. Clinician refinement partially corrected these effects. The study therefore shows that apparent communication quality does not guarantee clinically appropriate interpretation. Its main limitations are reliance on simulated written vignettes and an incompletely reproducible public-interface generation procedure.

## 2. Strengths

The three-arm comparison distinguishes autonomous generation from clinician-supervised use. It demonstrates that clinical review changes risk framing rather than merely polishing language.

The multidimensional evaluation is stronger than standard readability or expert-preference benchmarking. Mixed-effects and threshold-based models reveal discordance between comprehension, trust, risk perception, and misinterpretation.

The 2,038 participants generated 4,076 evaluations. Participant and scenario were modelled as random effects, while generalised estimating equation sensitivity analyses produced consistent findings.

Independent physician assessment of completeness, medical quality, appropriateness, and communication effectiveness further supports the superiority of clinician-refined outputs.

## 3. Weaknesses

Static written scenarios cannot reproduce emotional distress, follow-up questions, evolving prognosis, non-verbal communication, or established clinician–family relationships. Clinical and behavioural effectiveness therefore remains untested.

Generalisability is restricted to Chinese-language materials, Credamo recruitment, and hypothetical family members. Cultural variation in physician trust and uncertainty communication could alter the effects.

GPT-5.5 was accessed through a mutable public interface without a fixed model snapshot, seed, or decoding configuration. Outputs are available, but intervention regeneration is impossible.

Exploratory subgroup interactions were not multiplicity-adjusted. Ethnicity, income, geography, and deprivation were not evaluated.

## 4. Editorial Decision

**Send for Review.** The manuscript presents a distinctive safety finding: fluent LLM communication can improve understanding while worsening clinically relevant interpretation. Reviewers should adjudicate instrument validity, scenario-level robustness, generalisability, and whether the generation protocol is sufficiently documented.

## 5. Suggested Reviewer Expertise

Appropriate expertise includes experimental evaluation of patient-facing generative AI; human–LLM interaction and communication-safety measurement; mixed-effects and repeated-measures analysis of randomised vignette studies; health-literacy and risk-communication research; and critical-care family communication, surrogate decision-making, and goals-of-care practice.

## 6. State-of-the-Art Literature Review — Past Three Years

Recent studies have shown that LLM-generated patient-message responses can receive favourable ratings for empathy, style, and apparent quality while remaining longer, less readable, or clinically unsafe. Small et al. compared generative-AI and clinician responses to primary-care inbox messages, while Chen et al. found that LLM-assisted oncology replies improved perceived efficiency but included potentially severe harm in a subset of unedited outputs. ([JAMA Network][1]) Nolan et al. separately examined whether LLMs could incorporate patient values into surrogate decision support for incapacitated critically ill patients. ([PubMed][2])

The present manuscript advances this literature by evaluating actual human recipients, explicitly separating comprehension from misinterpretation and risk perception, and comparing autonomous generation with clinician refinement. It nevertheless remains a simulated, single-language evaluation without behavioural or clinical endpoints. The authors should engage more directly with implementation research on AI-drafted patient replies and with emerging critical-care LLM literature, which consistently identifies hallucination, bias, uncertainty communication, and human oversight as unresolved barriers. ([JAMA Network][3])

## 7. Suggested Reviewer Names

For patient-facing LLM evaluation and clinical NLP: Danielle S. Bitterman, Majid Afshar, and Lucila Ohno-Machado.

For human–AI communication and evaluation methodology: Shan Chen, Christopher Raghu Subramanian, and Virginia LeBaron.

For critical-care decision support and surrogate communication: Victoria J. Nolan, Tabor Flickinger, and Natalie Agaronnik.

For health literacy, risk communication, and patient-centred digital medicine: Maria E. Suárez-Almazor, Mitesh S. Patel, and Michael A. Diefenbach.

## 8. Further Literature — Ten Closely Related Papers, 2023–2026

**1. Chen S, Guevara M, Moningi S, et al. “The effect of using a large language model to respond to patient messages.” *The Lancet Digital Health*. 2024;6:e379–e381. DOI: 10.1016/S2589-7500(24)00060-8.** Peer reviewed and cited by the manuscript. Six oncologists evaluated LLM-assisted responses to realistic oncology portal messages. The study reported improved efficiency but identified potentially severe harm in some unedited drafts, directly supporting the need for clinician refinement. ([PubMed][4])

**2. Small WR, Wiesen JF, Geyer-Kim G, et al. “Large Language Model–Based Responses to Patients’ In-Basket Messages.” *JAMA Network Open*. 2024;7:e2416058. DOI: 10.1001/jamanetworkopen.2024.16058.** Peer reviewed and independent of the submitting group. Generative-AI responses were rated more empathetic and stylistically favourable than clinician responses but were longer, more complex, and less readable. This quality–comprehension discordance closely parallels the present manuscript’s central finding. ([JAMA Network][1])

**3. Garcia P, Ma SP, Shah S, et al. “Artificial Intelligence–Generated Draft Replies to Patient Inbox Messages.” *JAMA Network Open*. 2024;7:e246201. DOI: 10.1001/jamanetworkopen.2024.6201.** Peer reviewed and not cited by the manuscript. This prospective implementation study evaluated EHR-integrated LLM drafts in primary care and gastroenterology. It provides a clinically deployed comparator to the manuscript’s simulated communication experiment. ([JAMA Network][3])

**4. Kim J, Chen ML, Rezaei SJ, et al. “Perspectives on Artificial Intelligence–Generated Responses to Patient Messages.” *JAMA Network Open*. 2024;7:e2438535. DOI: 10.1001/jamanetworkopen.2024.38535.** Peer reviewed and not cited by the manuscript. Clinicians and patient participants separately evaluated information quality, empathy, and satisfaction for AI-generated and clinician-written responses. It is particularly relevant because it includes recipient-facing assessment rather than relying exclusively on automated metrics. ([PubMed][5])

**5. Nolan VJ, Balch JA, Baskaran NP, et al. “Incorporating Patient Values in Large Language Model Recommendations for Surrogate and Proxy Decisions.” *Journal of Medical Systems*. 2024;48:83. DOI: 10.1007/s10916-024-02094-6.** Peer reviewed and cited by the manuscript. This proof-of-concept study tested whether LLM recommendations for incapacitated critically ill patients could incorporate stated patient values. It is the closest recent work on LLM-supported surrogate decision-making in critical care. ([PubMed][2])

**6. Johri S, Jeong J, Tran BA, et al. “An evaluation framework for clinical use of large language models in patient interaction tasks.” *Nature Medicine*. 2025;31:77–86. DOI: 10.1038/s41591-024-03328-5.** Peer reviewed and cited by the manuscript. The framework evaluates realistic patient interactions across clinical correctness, communication quality, safety, bias, and contextual appropriateness. It provides a stronger multidimensional benchmark than readability or aggregate preference scores. ([Nature][6])

**7. Ayre J, Mac O, McCaffery K, et al. “New Frontiers in Health Literacy: Using ChatGPT to Simplify Health Information for People in the Community.” *Journal of General Internal Medicine*. 2024;39:573–577. DOI: 10.1007/s11606-023-08469-w.** Peer reviewed and cited by the manuscript. ChatGPT reduced linguistic complexity and passive constructions in public-facing health materials. Unlike the submitted study, however, it did not establish whether simplification improved risk interpretation or decision quality. ([PubMed][7])

**8. Will J, Wang T, et al. “Enhancing the Readability of Online Patient Education Materials Using Large Language Models: Cross-Sectional Study.” *Journal of Medical Internet Research*. 2025;27:e69955. DOI: 10.2196/69955.** Peer reviewed and cited by the manuscript. Multiple LLMs improved conventional readability scores across 60 patient-education documents. The present manuscript extends this work by demonstrating that readability improvements may coexist with misinterpretation and attenuated risk perception. ([PubMed][8])

**9. Mannhardt N, Bondi-Kelly E, Lam B, et al. “Impact of Large Language Model Assistance on Patients Reading Clinical Notes: A Mixed-Methods Study.” 2024.** This work was available as an arXiv preprint and its peer-review status should be verified before formal citation. Two hundred participants were randomised to different LLM augmentations of clinical notes, with quantitative comprehension and qualitative patient interviews. It shares the submitted study’s recipient-centred experimental design but focuses on note interpretation rather than critical-illness communication. ([arXiv][9])

**10. Saha A, Churchill V, Rodriguez AD, et al. “Large Language Models for Cancer Communication: Evaluating Linguistic Quality, Safety, and Accessibility in Generative AI.” 2025.** This is an arXiv preprint and is not yet confirmed as peer reviewed. It compared general-purpose and medical LLMs across linguistic quality, safety, trustworthiness, accessibility, and affectiveness. Its finding that linguistic performance and safety can diverge is directly aligned with the present manuscript’s multidimensional interpretation framework. ([arXiv][10])

[1]: https://jamanetwork.com/journals/jamanetworkopen/fullarticle/2821167?utm_source=chatgpt.com "Large Language Model–Based Responses to Patients' In- ..."
[2]: https://pubmed.ncbi.nlm.nih.gov/39132980/?utm_source=chatgpt.com "Incorporating Patient Values in Large Language Model Recommendations for Surrogate and Proxy Decisions - PubMed"
[3]: https://jamanetwork.com/journals/jamanetworkopen/fullarticle/2816494?utm_source=chatgpt.com "Artificial Intelligence–Generated Draft Replies to Patient ..."
[4]: https://pubmed.ncbi.nlm.nih.gov/38664108/?utm_source=chatgpt.com "The effect of using a large language model to respond to patient messages - PubMed"
[5]: https://pubmed.ncbi.nlm.nih.gov/39412810/?utm_source=chatgpt.com "Perspectives on Artificial Intelligence-Generated Responses to Patient Messages - PubMed"
[6]: https://www.nature.com/articles/s41591-024-03328-5?utm_source=chatgpt.com "An evaluation framework for clinical use of large language models in patient interaction tasks | Nature Medicine"
[7]: https://pubmed.ncbi.nlm.nih.gov/37940756/?utm_source=chatgpt.com "New Frontiers in Health Literacy: Using ChatGPT to Simplify Health Information for People in the Community - PubMed"
[8]: https://pubmed.ncbi.nlm.nih.gov/40465378/?utm_source=chatgpt.com "Enhancing the Readability of Online Patient Education Materials Using Large Language Models: Cross-Sectional Study - PubMed"
[9]: https://arxiv.org/abs/2401.09637?utm_source=chatgpt.com "Impact of Large Language Model Assistance on Patients Reading Clinical Notes: A Mixed-Methods Study"
[10]: https://arxiv.org/abs/2505.10472?utm_source=chatgpt.com "Large Language Models for Cancer Communication: Evaluating Linguistic Quality, Safety, and Accessibility in Generative AI"

063116
## Editorial Integrity Alert — Handling Editor Only

Several claims require verification before external review. The manuscript states that a 2025 FDA-cleared stroke-detection system requires radiologist confirmation, that WHO deployed tuberculosis-screening AI as “decision-support instruments only,” and that the African CDC is collaborating with developers to validate malaria and neonatal-sepsis tools. These assertions are not supported by clearly corresponding references. The cited 2026 International AI Safety Report concerns general-purpose AI rather than clinical validation or medical-device governance. The duplicated final page also indicates inadequate submission-quality control.

## 1. Overall Assessment

This Comment argues that clinical AI should be aligned with patient safety, clinical intentions and health equity before deployment. It proposes three routes: technical alignment through concept bottleneck models, human-in-the-loop systems and continuous monitoring; regulatory harmonisation across the European Union, United Kingdom and United States; and international governance addressing low-resource settings. Figure 1 presents these elements as a pathway toward safe and trustworthy clinical AI. 

The topic is important, but the manuscript does not provide a sufficiently distinctive or rigorous contribution. Its framework combines established principles without defining measurable alignment criteria or an implementation methodology. Technical alignment, fairness, medical-device regulation, organisational governance and global equity are grouped together without clarifying their causal or institutional relationships.

## 2. Strengths

The manuscript correctly identifies post-deployment monitoring as essential. Its emphasis on distribution shift, evolving clinical practice, feedback loops and recalibration addresses a major weakness in current clinical-AI evaluation.

It also recognises that human oversight must be embedded within clinical workflows rather than added as a nominal safeguard. The global-health section appropriately challenges the transferability of models developed in high-income settings to health systems with different disease prevalence, infrastructure and clinical capacity.

## 3. Weaknesses

The framework is not operational. “Alignment” is not translated into endpoints such as calibration, subgroup performance, intervention utility, override behaviour, failure-detection sensitivity or patient outcomes. Figure 1 therefore functions as a taxonomy rather than an actionable framework.

Concept bottleneck models are presented too broadly. They do not inherently ensure fairness, robustness or causal validity, and the manuscript does not address concept-label quality, incompleteness, leakage or intervention fidelity.

The regulatory analysis also compresses distinct regimes. General AI governance, medical-device conformity assessment, clinical evaluation, quality-management systems and post-market surveillance should be separated. Several specific deployment and policy examples are insufficiently referenced.

## 4. Editorial Decision

**Reject.** The manuscript addresses a timely issue but does not establish a novel framework, systematic evidence synthesis or sufficiently precise recommendations. Its unsupported claims and conflation of technical, regulatory and organisational alignment require fundamental reconstruction. A substantially revised perspective may be more suitable for **npj Digital Medicine**.

## 5. Suggested Reviewer Expertise

Appropriate expertise would include interpretable and concept-based machine learning for clinical applications; prospective evaluation and post-market monitoring of deployed clinical AI; algorithmic fairness and transportability across health systems; medical-device regulation under FDA, MHRA and EU frameworks; and clinical informatics or patient-safety governance within operational health systems.

## 6. State-of-the-Art Literature Review: Past Three Years

Recent work has moved beyond general ethical principles toward operational health-system governance. Kim and colleagues applied a People, Process, Technology and Operations framework through interviews and co-design in a Canadian hospital system. Hussein and colleagues systematically reviewed 35 healthcare-AI implementation frameworks and identified seven governance domains, including the resource constraints faced by smaller organisations. Stanford investigators have developed deployment and monitoring infrastructure that distinguishes system integrity, predictive performance and clinical impact, with prospective experience showing that deployed performance can differ from retrospective estimates. ([nature.com](https://www.nature.com/articles/s41746-025-01909-3?utm_source=chatgpt.com))

Against this literature, the present manuscript offers a readable synthesis but not a substantive advance. Its strongest contribution is connecting technical interpretability, regulation and global inequity in one narrative. However, the three-pathway framework is less operational than recent governance and monitoring models, and it does not provide empirical validation, consensus methods, implementation checklists or accountable decision thresholds.

## 7. Suggested Reviewer Names

Potential reviewers include **Marzyeh Ghassemi**, whose work addresses robustness, fairness and minority-group harms in health machine learning; **Karandeep Singh**, whose work concerns health-system evaluation, governance and anticipated deployment failures; **Nigam H. Shah**, whose research includes prospective deployment and post-market monitoring of clinical AI; and **Jess Morley**, whose scholarship focuses on ethical implementation, accountability and governance of AI in healthcare. Their institutional profiles indicate directly relevant expertise, although conflicts of interest and recent collaborations with the authors must be checked before invitation.

063364
## 1. Overall Assessment

RadPRISM proposes schema-stratified supervision for chest-radiograph vision–language learning. Free-text reports are decomposed into concept fields covering support devices, anatomical structures, pathologies, and locations. These representations supervise image–text alignment, zero-shot classification, retrieval, selective prediction, and visual grounding. The study uses a large internal dataset, CheXpert, CheXlocalize, and a three-radiologist reader study. 

The framework is technically coherent, but the evidence does not establish a substantial and generalisable advance at the required editorial threshold. The main concerns are evaluation circularity arising from report-derived supervision and labels, limited external validation, and the absence of clinically realistic deployment testing.

## 2. Strengths

The manuscript addresses a recognised limitation of report-level contrastive learning by explicitly separating clinically distinct concepts. The architecture and ablation analyses indicate that both schema construction and concept-specific alignment contribute to performance.

The evaluation spans classification, retrieval, selective prediction, and visual grounding. This breadth is stronger than a single-task benchmark and exposes concept-specific failure modes.

The reader study provides some clinician-centred assessment. It examines localisation, retrieval, binary classification, and concept–patient disentanglement rather than relying solely on automated metrics.

## 3. Weaknesses

The external validation is insufficient. CheXpert is closely related to the development setting, and CheXlocalize covers a limited pathology set. No independent multi-institutional cohort demonstrates robustness across acquisition systems, patient populations, or reporting conventions.

The evaluation is partly circular. Training supervision, concept vocabularies, prompts, and several reference labels originate from reports or report-derived annotations. This design may reward ontology reproduction rather than independent visual understanding.

Demographic and clinical subgroup analyses are absent. Performance, calibration, abstention behaviour, and retrieval errors are not reported across age, sex, race, ethnicity, or care setting.

The reader study uses selected cases and isolated tasks. It does not assess complete reporting, diagnostic impact, workflow efficiency, or prospective clinical use. Comparisons with contemporary grounded-reporting systems are also incomplete.

## 4. Editorial Decision

**Reject.** The manuscript presents an interesting supervision strategy, but its central claims are not supported by sufficiently independent validation. The combination of report-derived evaluation, restricted external testing, absent subgroup analysis, and non-clinical reader tasks prevents a reliable assessment of generalisability and clinical utility. These limitations require substantial new datasets and experiments rather than revision of the current manuscript. Transfer to *npj Digital Medicine* may be considered after independent multi-site validation.

## 5. Suggested Reviewer Expertise

Appropriate expertise includes concept-level and region-level supervision for medical vision–language models; representation learning and selective prediction for chest radiography; radiology-report parsing using clinical ontologies and large language models; evaluation of grounded radiology report generation and hallucination; and practising thoracic radiology with experience in observer studies and AI workflow validation.

## 6. State-of-the-Art Literature Review: Past Three Years

Recent radiology vision–language research has moved from global image–report contrastive learning toward grounded, auditable generation. RaDialog introduced a publicly available radiology vision–language model for report generation and interactive dialogue. MAIRA-2 subsequently formulated grounded report generation and introduced RadFact for sentence-level factuality and localisation assessment. CheXpert Plus released more than 223,000 aligned radiograph–report pairs, while CXPMRG-Bench and ReXrank have pushed evaluation toward common datasets, multiple institutions, and clinically informed metrics. PadChest-GR adds radiologist-curated sentence-to-box annotations for grounded report generation. ([arxiv.org](https://arxiv.org/abs/2406.04449?utm_source=chatgpt.com))

RadPRISM advances this landscape by making the granularity of supervision an explicit design variable and by evaluating concept–patient disentanglement. Its strongest novelty lies in schema-stratified representation learning rather than report generation itself. However, the manuscript should engage more directly with MAIRA-2, anatomy-prompted structured reporting, RadGraph-based content–style separation, and radiologist-annotated phrase grounding. These studies address overlapping claims concerning structure, localisation, factuality, and clinical interpretability. ([arxiv.org](https://arxiv.org/abs/2310.17811?utm_source=chatgpt.com))

## 7. Suggested Reviewer Names

Shruthi Bannur would provide expertise in grounded radiology report generation and sentence-level factuality through her work on MAIRA-2. Pierre Chambon would contribute expertise in large-scale chest-radiograph datasets, multimodal representation learning, and CheXpert Plus. Chantal Pellegrini would be suitable for evaluating radiology-specific large vision–language models and report-generation baselines through her work on RaDialog. Daniel C. Castro would provide expertise in radiologist-annotated grounding datasets and evaluation through PadChest-GR. Reviewer independence and recent institutional or collaborative relationships with the submitting authors should be checked before invitation.

063401
## 1. Overall Assessment

The manuscript presents GAT-BiGRU-QR, a model for predicting temperatures at 13 skin sites when observations are missing. Graph attention represents anatomical relationships, a bidirectional GRU models temporal dynamics, and quantile regression generates prediction intervals. The evaluation includes random masking, complete sensor-node loss, environmental transfer and contact-sensor occlusion. 

The approach is technically coherent but does not establish a sufficiently general or reproducible advance for Nature Communications. The principal concerns are the small, single-centre cohort and a validation strategy that may permit participant-level and temporal leakage between training and test sets.

## 2. Strengths

The study addresses an important problem in distributed physiological sensing. It distinguishes isolated missing values from complete sensor failure and evaluates masking ratios up to 40%.

The architecture has a reasonable inductive structure. Graph attention models cross-site physiological relationships, while the bidirectional GRU captures temporal trajectories. Quantile regression is combined with interval coverage, width and alignment objectives.

The evaluation extends beyond point-prediction metrics. The authors report MSE, MAE, MAPE, (R^2), coverage probability and interval width across environmental, activity and missing-node scenarios.

## 3. Weaknesses

The dataset includes only 30 healthy adults, comprising 24 men and six women aged 24–33 years, from one climate-chamber study. This cannot support broad claims concerning thermal health assessment or population-level thermoregulation.

The 5:2:3 split appears to be applied after dividing continuous recordings into overlapping windows. Unless all windows from each participant and session were isolated within one partition, near-duplicate temporal trajectories may occur across training and test sets.

Missingness is predominantly synthetic. Real failures caused by detachment, movement, sweat or perfusion changes are often informative and temporally clustered.

Baseline comparisons are incomplete, and reproducibility is limited by the absence of accessible code, participant-level split information, random seeds and detailed preprocessing documentation.

## 4. Editorial Decision

**Reject.** Participant-independent validation and realistic sensor-failure evaluation are required before the model’s claims can be assessed reliably. Transfer to **Communications Engineering** may be appropriate after leakage-safe reanalysis, stronger imputation baselines and removal of unsupported health claims.

## 5. Suggested Reviewer Expertise

Appropriate expertise includes graph neural networks for physiological sensor topology; multivariate time-series forecasting and imputation; probabilistic forecasting and quantile calibration; wearable skin-temperature instrumentation; and human thermoregulation under controlled environmental exposure.

## 6. State-of-the-Art Literature Review

Recent personal-comfort research has moved toward wearable physiological sensing, data-efficient personalisation and deployment-oriented evaluation. Tekler and colleagues developed active-transfer-learning methods for personal thermal-comfort prediction with limited individual data. Recent work has also combined wrist skin temperature with indoor environmental measurements and assessed wristband-derived skin temperature, electrodermal activity and heart rate in real offices. ([sciencedirect.com](https://www.sciencedirect.com/science/article/pii/S0378778824006236?utm_source=chatgpt.com))

The manuscript advances this literature by treating body sites as a physiological graph and explicitly evaluating complete-node loss. However, graph attention plus BiGRU is an incremental architectural combination, and the study does not match contemporary expectations for external generalisation, data-efficient personalisation or realistic missingness. Recent wearable studies used field settings, while graph-time-series research provides substantially stronger imputation comparators than those included here. ([sciencedirect.com](https://www.sciencedirect.com/science/article/pii/S0263224123014616?utm_source=chatgpt.com))

## 7. Suggested Reviewer Names

Zeynep Duygu Tekler would provide expertise in active transfer learning and data-efficient personal thermal-comfort modelling. Adrian Chong and Clayton Miller have relevant work on personalised comfort prediction, occupant-centric sensing and spatial-context models. Yasunori Akashi would provide expertise in experimentally measured wrist skin-temperature dynamics and human thermal response. These candidates should undergo routine conflict-of-interest and recent-collaboration screening before invitation.

063487
## 1. Overall Assessment

BioGnosis integrates a biomedical knowledge graph with literature retrieval and large language models for biomedical question answering and gene-set annotation. The graph contains approximately 9.8 million relationships, while the literature layer includes about 134,000 full-text articles and 20 million abstract-derived records. The pipeline combines graph expansion, semantic retrieval, reranking, and evidence-grounded generation, and is evaluated on 400 internally generated questions and approximately 3,200 model responses. 

The engineering scope is substantial, but the contribution mainly combines established GraphRAG, vector retrieval, reranking, and prompting methods. The decisive concerns are benchmark circularity, LLM-based adjudication, and absent external evaluation.

## 2. Strengths

The architecture integrates Gene Ontology, KEGG, Reactome, WikiPathways, CTD, NCBI Taxonomy, Cell Ontology, Uberon, and literature-derived entities. Graph-neighbour expansion and article retrieval provide complementary evidence.

The component analysis separates retrieval, reranking, and query enhancement across question types and complexity levels. Retrieval contributes most strongly to faithfulness and overall performance, while query enhancement benefits difficult multi-hop questions.

The gene-set experiments extend the framework beyond question answering. BioGnosis generates explanatory pathway interpretations and reports gains in ROUGE-L and semantic similarity over individual LLM configurations and conventional enrichment outputs.

## 3. Weaknesses

The benchmark is insufficiently independent. Question generation, reference construction, claim decomposition, and semantic scoring all involve LLMs, risking reward for stylistic agreement rather than biomedical correctness. Blinded expert assessment with inter-rater reliability is required.

The study lacks evaluation on BioASQ, PubMedQA, MedQA, or MultiMedQA and common-benchmark comparisons with KRAGEN, SPOKE KG-RAG, or related biomedical GraphRAG systems.

Reproducibility is incomplete because code, prompts, graph snapshots, article identifiers, retrieval parameters, model versions, latency, and computational costs are not fully archived.

## 4. Editorial Decision

**Reject.** The internally generated and substantially LLM-adjudicated benchmark does not independently support the central claims. Without expert validation, external benchmarks, and direct system-level comparisons, the manuscript does not establish a substantial advance. A redesigned study may suit **npj Artificial Intelligence** or **Communications Biology**.

## 5. Suggested Reviewer Expertise

External assessment would require expertise in biomedical knowledge-graph construction and ontology integration; GraphRAG and multi-hop retrieval for biomedical question answering; evaluation of generative systems, including hallucination, factuality and LLM-as-judge bias; computational functional genomics and pathway-enrichment analysis; and biomedical informatics with practical experience interpreting gene sets and literature-grounded biological hypotheses.

## 6. State-of-the-Art Literature Review

Recent biomedical GraphRAG work already establishes several of the manuscript’s core design principles. KRAGEN combines knowledge graphs, RAG and structured prompting for biomedical problem solving. SPOKE KG-RAG uses prompt-aware retrieval from a large heterogeneous graph and reports 97% retrieval accuracy on its internal test set, with substantial gains over prompt-only Llama-2, GPT-3.5 and GPT-4 configurations. Both systems provide direct methodological comparators for BioGnosis. ([PubMed Central (PMC)][1])

For gene-set interpretation, Joachimiak et al. demonstrated LLM-based gene-set summarisation, while AnnDictionary subsequently benchmarked 14 major LLMs for functional gene-set annotation and reported that Claude 3.5 Sonnet recovered close functional annotations in more than 80% of curated test sets. AnnDictionary also provides open preprocessing pipelines and repeated-model evaluations. Literature-scaled immunological annotation has further combined article-derived knowledge graphs with LLMs, demonstrating that domain-restricted graph construction is an important alternative to a broad biomedical graph. ([Nature][2])

BioGnosis advances this landscape by integrating graph retrieval, full-text literature retrieval and gene-set interpretation within one framework, and by analysing retrieval components in detail. It does not yet demonstrate a decisive advance over KRAGEN or SPOKE KG-RAG because these systems are not evaluated under a common benchmark. Its gene-set results also require comparison with AnnDictionary and expert-curated functional interpretation rather than predominantly lexical metrics.

## 7. Suggested Reviewer Names

For biomedical GraphRAG and knowledge-graph retrieval, appropriate candidates include **Karthik Soman**, who led the SPOKE KG-RAG study; **Noriaki Matsumoto**, first author of KRAGEN; and **Jasper Linders**, who developed knowledge-graph-extended RAG with explicit multi-hop decomposition. Their work directly addresses graph selection, retrieval fidelity and grounded generation.

For gene-set annotation and computational genomics, suitable candidates include **Matthew P. Joachimiak**, who developed LLM-based gene-set summarisation; **George Crowley**, who led the AnnDictionary benchmarking study; and **Sarah He**, whose work examines literature-scaled immunological gene-set annotation using knowledge graphs. Reviewer conflicts and recent collaborations with the submitting authors should be checked before invitation.

## 8. Further Literature: Ten Closely Related Papers from the Past Three Years

1. Matsumoto, N. et al. “KRAGEN: a knowledge graph-enhanced RAG framework for biomedical problem solving using large language models.” *Bioinformatics* 40, btae353 (2024). DOI: 10.1093/bioinformatics/btae353. Peer-reviewed. Cited by the manuscript. This is a direct comparator because it integrates graph retrieval, graph-of-thought reasoning and LLM generation for biomedical question answering. ([PubMed Central (PMC)][1])

2. Soman, K. et al. “Biomedical knowledge graph-optimized prompt generation for large language models.” *Bioinformatics* 40, btae560 (2024). DOI: 10.1093/bioinformatics/btae560. Peer-reviewed. Cited by the manuscript. The study introduces SPOKE KG-RAG, prompt-aware graph-context extraction and token-efficient biomedical grounding. ([Providence][3])

3. Hu, M. et al. “Evaluation of large language models for discovery of gene set function.” *Nature Methods* 22, 3–11 (2025). DOI: 10.1038/s41592-024-02525-x. Peer-reviewed. Cited by the manuscript. It directly benchmarks LLM-based functional interpretation of gene sets against curated Gene Ontology concepts and random controls. ([Nature][4])

4. Wang, Z. et al. “GeneAgent: self-verification language agent for gene-set analysis using domain databases.” *Nature Methods* (2025). DOI: 10.1038/s41592-025-02748-6. Peer-reviewed. Cited by the manuscript. GeneAgent is a particularly strong comparator because it combines external biological databases, iterative verification and expert assessment to reduce hallucinated gene-set interpretations. ([PubMed][5])

5. Crowley, G. et al. “Benchmarking cell type and gene set annotation by large language models with AnnDictionary.” *Nature Communications* 16, 9511 (2025). DOI: 10.1038/s41467-025-64511-x. Peer-reviewed. Not clearly cited in the manuscript. It provides a model-agnostic benchmark for gene-list and cell-type annotation and therefore directly challenges BioGnosis’s predominantly internal evaluation. ([DOI][6])

6. Wu, J. et al. “Medical Graph RAG: Evidence-based Medical Large Language Model via Graph Retrieval-Augmented Generation.” *Proceedings of ACL 2025*, 2025.acl-long.1381. DOI: 10.18653/v1/2025.acl-long.1381. Peer-reviewed conference paper. Not cited in the manuscript. It develops a medical GraphRAG framework using graph-structured evidence for grounded generation and is a direct system-level comparator. ([ACL Anthology][7])

7. Matsumoto, N. et al. “ESCARGOT: an AI agent leveraging large language models, dynamic graph of thoughts, and biomedical knowledge graphs for enhanced reasoning.” *Bioinformatics* 41, btaf031 (2025). DOI: 10.1093/bioinformatics/btaf031. Peer-reviewed. Not clearly cited in the manuscript. ESCARGOT extends KRAGEN with dynamically generated graph-of-thought execution, Cypher querying and transparent reasoning traces. ([PubMed][8])

8. Song, J. et al. “Graph retrieval augmented large language models for facial phenotype associated rare genetic disease.” *npj Digital Medicine* (2025). DOI: 10.1038/s41746-025-01955-x. Peer-reviewed. Not cited in the manuscript. The study directly compares Cypher-based and vector-based graph retrieval and evaluates diagnostic accuracy, consistency and temperature sensitivity across eight LLMs. ([PubMed][9])

9. Hou, W. and Ji, Z. “Assessing GPT-4 for cell type annotation in single-cell RNA-seq analysis.” *Nature Methods* 21, 1462–1465 (2024). DOI: 10.1038/s41592-024-02235-4. Peer-reviewed. Cited by the manuscript. Although focused on cell-type rather than pathway annotation, it is methodologically relevant because it evaluates LLM interpretation of marker-gene sets across ten datasets and five species. ([Nature][10])

10. Xie, E. et al. “CASSIA: a multi-agent large language model for automated and interpretable cell annotation.” *Nature Communications* (2025). DOI: 10.1038/s41467-025-67084-x. Peer-reviewed. Not cited in the manuscript. CASSIA combines annotation, validation, quality scoring, refinement and optional RAG agents, with benchmarking across 970 cell populations. Its modular validation design is directly relevant to BioGnosis’s claims regarding reliable biological interpretation. ([Nature][11])

[1]: https://pmc.ncbi.nlm.nih.gov/articles/PMC11164829/?utm_source=chatgpt.com "KRAGEN: a knowledge graph-enhanced RAG framework for biomedical problem solving using large language models - PMC"
[2]: https://www.nature.com/articles/s41467-025-64511-x "Benchmarking cell type and gene set annotation by large language models with AnnDictionary | Nature Communications"
[3]: https://providence.elsevierpure.com/en/publications/biomedical-knowledge-graph-optimized-prompt-generation-for-large-/?utm_source=chatgpt.com "Biomedical knowledge graph-optimized prompt generation for large language models - Providence"
[4]: https://www.nature.com/articles/s41592-024-02525-x?utm_source=chatgpt.com "Evaluation of large language models for discovery of gene set function | Nature Methods"
[5]: https://pubmed.ncbi.nlm.nih.gov/40721871/?utm_source=chatgpt.com "GeneAgent: self-verification language agent for gene-set analysis using domain databases - PubMed"
[6]: https://doi.org/10.1038%2Fs41467-025-64511-x?utm_source=chatgpt.com "Benchmarking cell type and gene set annotation by large language models with AnnDictionary | Nature Communications"
[7]: https://aclanthology.org/2025.acl-long.1381/?utm_source=chatgpt.com "Medical Graph RAG: Evidence-based Medical Large Language Model via Graph Retrieval-Augmented Generation - ACL Anthology"
[8]: https://pubmed.ncbi.nlm.nih.gov/39842860/?utm_source=chatgpt.com "ESCARGOT: an AI agent leveraging large language models, dynamic graph of thoughts, and biomedical knowledge graphs for enhanced reasoning - PubMed"
[9]: https://pubmed.ncbi.nlm.nih.gov/40849403/?utm_source=chatgpt.com "Graph retrieval augmented large language models for facial phenotype associated rare genetic disease - PubMed"
[10]: https://www.nature.com/articles/s41592-024-02235-4 "Assessing GPT-4 for cell type annotation in single-cell RNA-seq analysis | Nature Methods"
[11]: https://www.nature.com/articles/s41467-025-67084-x "CASSIA: a multi-agent large language model for automated and interpretable cell annotation | Nature Communications"

063604
### 1. Overall Assessment

The manuscript introduces a six-task benchmark that progressively delegates analytical authority to large language models across a retinal vessel-density, plasma-proteomic, and cardiovascular–kidney–metabolic workflow. Using UK Biobank and GDIES, it argues that models reproduce prespecified analyses reliably but lose scientific fidelity when required to choose candidate-selection, multiplicity-control, weighting, and outcome-specific rules. 

The contribution is conceptually stronger than a conventional coding benchmark because execution completeness and analytical fidelity are evaluated separately. The main concerns are the narrow biological and statistical scope, and the treatment of one frozen researcher workflow as the reference standard despite plausible alternative analyses.

### 2. Strengths

The staged T1–T6 design localises failure as methodological authority is transferred. This is more informative than aggregate task accuracy and directly tests the manuscript’s proposed operational trust boundary.

The evaluation is unusually granular. Across 5,450 history-free calls, the authors assess code execution, set recovery, coefficient agreement, joint-ratio calibration, format compliance, and outcome specificity rather than relying on final-answer similarity.

The benchmark is grounded in a substantive workflow comprising 2,921 UK Biobank proteins, seven prespecified outcomes, covariate-adjusted models, Benjamini–Hochberg correction, and an external cohort of 1,389 participants.

### 3. Weaknesses

Generalisability is not established because all tasks derive from one observational proteomics workflow. Validation on an unrelated workflow involving survival analysis, missing-data handling, causal inference, or predictive modelling is needed.

The frozen reference is reproducible but not uniquely correct. Independent statisticians should classify deviations as errors, acceptable alternatives, or substantively equivalent analyses.

Reproducibility depends heavily on proprietary, mutable models. Exact model snapshots, API dates, inference settings, prompts, raw outputs, parser code, and executable environments require permanent archiving.

### 4. Editorial Decision

**Send for Review.** The manuscript offers a distinctive benchmark for locating failure in delegated biomedical analysis. Reviewers should adjudicate reference-standard validity, cross-workflow generalisability, and whether the released materials support exact reproduction.

### 5. Suggested Reviewer Expertise

Relevant expertise includes benchmark design for autonomous scientific agents; statistical validation of generated analytical workflows; reproducible computational epidemiology using UK Biobank and high-dimensional proteomics; evaluation of LLM tool use and executable code; and retinal vascular epidemiology with cardiovascular and renal outcomes.

### 6. State-of-the-Art Literature Review

Recent evaluation has moved from medical question answering toward executable, multistep scientific workflows. BioDSA-1K contains 1,029 biomedical hypothesis-validation tasks and separately evaluates conclusions, evidence alignment, reasoning, and code executability. BixBench uses real bioinformatics datasets and long analytical trajectories, with frontier agents achieving low open-answer accuracy. BAISBench evaluates discovery from single-cell data, while BioXArena extends agent evaluation to 76 multimodal biomedical machine-learning tasks with hidden labels and held-out graders. ([arXiv][1])

The present manuscript is narrower in biological breadth but deeper in controlled experimental design. Unlike BioDSA-1K and BixBench, it holds data and upstream inputs constant while selectively relaxing methodological constraints. This allows the authors to attribute failure to delegated choices. Its principal limitation relative to these benchmarks is external breadth: one prespecified epidemiological workflow cannot establish a universal operational boundary. The manuscript should directly compare its task taxonomy and fidelity metrics with BioDSA-1K, BixBench, BioML-bench, and MedAgentBench. ([BioRxiv][2])

### 7. Suggested Reviewer Names

For biomedical data-science agent benchmarking, suitable reviewers include Zifeng Wang and Benjamin Danek, authors of BioDSA-1K; Ludovico Mitchener and Jon Laurent, authors of BixBench; and Erpai Luo, lead author of BAISBench. Their work directly addresses realistic multistep biomedical analysis and scientific-agent evaluation. ([arXiv][1])

For LLM evaluation methodology, Paul Hager would provide relevant expertise from systematic testing of model limitations in clinical decision-making. Qiao Jin and Nicholas Wan have evaluated LLM performance on complex clinical-calculator selection and reasoning tasks.

For computational epidemiology and proteomic workflows, reviewers should include investigators experienced in UK Biobank, Olink proteomics, multiple-testing control, and cardiovascular–renal outcome modelling. Candidate identities require a conflict-of-interest check against the author group and the participating UK Biobank and GDIES teams before invitation.

### 8. Further Literature

The following papers were published or posted during 2023–2026 and share the manuscript’s scope of evaluating LLM agents on executable, multistep scientific, biomedical, or data-analytic workflows.

1. Chen Z, Chen S, Ning Y, et al. **ScienceAgentBench: Toward Rigorous Assessment of Language Agents for Data-Driven Scientific Discovery.** ICLR, 2025. The benchmark contains 102 tasks extracted from 44 peer-reviewed studies and evaluates generated programs, execution results, scientific correctness, and cost. It is the closest general-science comparator to the manuscript’s separation of execution from analytical validity. Peer reviewed. ([OpenReview][3])

2. Wang Z, Danek B, Sun J. **BioDSA-1K: Benchmarking Data Science Agents for Biomedical Research.** arXiv, 2025. BioDSA-1K comprises 1,029 biomedical hypothesis-testing tasks and evaluates hypothesis decisions, evidence–conclusion alignment, reasoning, and code executability. It directly overlaps with the manuscript’s emphasis on trustworthy biomedical analysis rather than runnable code alone. Preprint. ([arXiv][1])

3. Mitchener L, Laurent JM, Tenmann B, et al. **BixBench: A Comprehensive Benchmark for LLM-Based Agents in Computational Biology.** arXiv, 2025. BixBench includes more than 50 biological data-analysis scenarios and nearly 300 open-answer questions requiring long, multistep analytical trajectories. It provides a broader bioinformatics test of the workflow-level generalisability claimed by the manuscript. Preprint. ([arXiv][4])

4. Miller and colleagues. **BioML-bench: Evaluation of AI Agents for End-to-End Biomedical Machine Learning.** bioRxiv, 2025. This benchmark evaluates agents across protein engineering, drug discovery, single-cell omics, medical imaging, and clinical-biomarker modelling. It is particularly relevant to the manuscript’s limitation to a single observational proteomics workflow. Preprint. ([BioRxiv][2])

5. Luo E, Jia J, Xiong Y, et al. **Benchmarking AI Scientists for Omics Data-Driven Biological Discovery.** *Bioinformatics*, 2026. BAISBench assesses cell-type annotation and biological discovery using real single-cell transcriptomic datasets and conclusions derived from published studies. It tests integration of executable analysis with domain interpretation, closely matching the manuscript’s concern about methodologically plausible but scientifically incorrect outputs. Peer reviewed. ([OUP Academic][5])

6. Li L, Zhang D, Du X, et al. **BioXArena: Benchmarking LLM Agents on Multi-Modal Biomedical Machine Learning Tasks.** arXiv, 2026. BioXArena contains 76 end-to-end tasks across nine biomedical domains, with private test labels, held-out graders, executable pipelines, and biology-aware metrics. Its breadth provides a direct counterpoint to the manuscript’s task-specific trust boundary. Preprint. ([arXiv][6])

7. **BiomniBench: Process-Level Evaluation of LLM Agents for Real-World Biomedical Research.** bioRxiv, 2026. BiomniBench-DA includes 100 data-analysis tasks across 17 task types and evaluates intermediate research-process dimensions rather than only final outputs. Its process-level scoring is closely aligned with the manuscript’s staged assessment of analytical decisions. Preprint. ([BioRxiv][7])

8. Jiang Y, Black KC, Geng G, et al. **MedAgentBench: A Virtual EHR Environment to Benchmark Medical LLM Agents.** *NEJM AI*, 2025. MedAgentBench evaluates 300 physician-authored tasks in a FHIR-compliant environment containing realistic longitudinal patient records. Although clinically oriented, it similarly tests autonomous tool use, planning, execution, and task-specific failure within a controlled workflow. Peer reviewed. ([DOI][8])

9. Huang Q, Vora J, Liang P, Leskovec J. **MLAgentBench: Evaluating Language Agents on Machine Learning Experimentation.** Proceedings of ICML, 2024. MLAgentBench assesses whether agents can design experiments, modify code, interpret results, and iteratively improve machine-learning systems. It is relevant to the manuscript’s distinction between following an explicit analytical protocol and independently selecting consequential methodological steps. Peer reviewed. ([Proceedings of Machine Learning Research][9])

10. Boiko DA, MacKnight R, Kline B, Gomes G. **Autonomous Chemical Research with Large Language Models.** *Nature*, 2023. The Coscientist system combines planning, literature retrieval, code execution, and laboratory-tool control to perform multistep chemical research. It is not principally a benchmark, but it is a foundational demonstration of delegated scientific authority and therefore an important conceptual comparator for the manuscript’s trust-boundary framework. Peer reviewed. ([nature.com][10])

[1]: https://arxiv.org/abs/2505.16100?utm_source=chatgpt.com "BioDSA-1K: Benchmarking Data Science Agents for Biomedical Research"
[2]: https://www.biorxiv.org/content/10.1101/2025.09.01.673319v2?utm_source=chatgpt.com "BioML-bench: Evaluation of AI Agents for End-to-End Biomedical ML | bioRxiv"
[3]: https://openreview.net/forum?id=6z4YKr0GK6&utm_source=chatgpt.com "ScienceAgentBench: Toward Rigorous Assessment of ..."
[4]: https://arxiv.org/abs/2503.00096?utm_source=chatgpt.com "BixBench: a Comprehensive Benchmark for LLM-based Agents in Computational Biology"
[5]: https://academic.oup.com/bioinformatics/article/42/Supplement_1/btag227/8726318?utm_source=chatgpt.com "Benchmarking AI scientists for omics data–driven biological ..."
[6]: https://arxiv.org/abs/2605.15766?utm_source=chatgpt.com "BioXArena: Benchmarking LLM Agents on Multi-Modal Biomedical Machine Learning Tasks"
[7]: https://www.biorxiv.org/content/10.64898/2026.05.12.724604v2?utm_source=chatgpt.com "BiomniBench: Process-level Evaluation of LLM Agents for Real-world Biomedical Research | bioRxiv"
[8]: https://doi.org/10.1056/AIdbp2500144?utm_source=chatgpt.com "MedAgentBench: A Virtual EHR Environment to Benchmark Medical LLM Agents | NEJM AI"
[9]: https://proceedings.mlr.press/v235/huang24y.html?utm_source=chatgpt.com "MLAgentBench: Evaluating Language Agents on Machine Learning Experimentation"
[10]: https://www.nature.com/articles/s41586-023-06792-0?utm_source=chatgpt.com "Autonomous chemical research with large language models"

064012
## 1. Overall Assessment

The manuscript evaluates whether ICU delirium prediction models transport between MIMIC-IV and the multicentre eICU Collaborative Research Database. LASSO, XGBoost, GRU, LSTM, and Transformer models are assessed under source-only transfer, target-database redevelopment, recalibration, and alternative endpoint definitions. The principal claim is that transportability depends on endpoint construction: incident-delirium prediction transfers poorly, whereas assessment-conditioned persistence or recurrence prediction retains stronger discrimination.

The study is methodologically informative, but its strongest results depend heavily on prior delirium assessments. When assessment history is removed, external performance declines substantially. The work therefore characterises transport failure more convincingly than it establishes a clinically actionable predictive advance. 

## 2. Strengths

The bidirectional validation design is rigorous. Models are trained in both databases and evaluated in the opposite cohort, reducing dependence on a single favourable source–target pairing.

The endpoint decomposition is a substantive strength. The authors separate incident delirium from persistent or recurrent delirium and vary anchor eligibility, horizon, and review policy. This demonstrates that observation processes and label construction materially alter apparent transportability.

Evaluation extends beyond AUROC to AUPRC, calibration, risk-decile enrichment, alert yield, workload, and decision-curve analysis. Repeated natural-person-grouped runs and fold-paired comparisons provide credible uncertainty estimates.

The attribution and ablation analyses identify why XGBoost transports better. Longitudinal assessment history dominates external performance, while recurrent and Transformer architectures do not consistently improve transfer.

## 3. Weaknesses

The clinically most important task—first-onset delirium prediction without prior delirium assessments—remains weak. The reported high AUROCs largely reflect persistence or recurrence modelling rather than early detection.

Both datasets are retrospective and US-based. Differences in CAM-ICU documentation, sedation practice, assessment frequency, and missingness may encode workflow rather than disease biology. Prospective, geographically independent validation is absent.

No meaningful subgroup analysis is reported across age, sex, race or ethnicity, language, insurance status, socioeconomic position, or ICU type. This is critical because the outcome depends on clinician assessment behaviour.

Clinical implementation remains hypothetical. Calibration is unstable, local adaptation provides limited benefit, and retrospective workload estimates do not establish timely or beneficial intervention.

## 4. Editorial Decision

**Reject.** The manuscript provides a useful analysis of endpoint-dependent transportability but does not meet the threshold for a substantial clinical AI advance. Its strongest performance depends on prior assessment history, while incident prediction and prospective generalisability remain insufficient. Transfer to **Communications Medicine** would be appropriate.

## 5. Suggested Reviewer Expertise

Appropriate expertise includes cross-institutional validation of longitudinal EHR models; XGBoost and recurrent or Transformer-based ICU time-series modelling; calibration, decision-curve analysis, and dataset-shift methodology; delirium phenotyping from CAM-ICU and ICD-derived data; and critical-care delirium prevention, assessment workflows, and implementation science.

## 6. State-of-the-Art Literature Review

Recent work has moved from isolated retrospective classifiers toward dynamic and externally validated ICU delirium prediction. Gong and colleagues reported model development and external validation using routinely collected clinical and physiological data in *Anesthesiology* in 2023. Dynamic models have subsequently predicted delirium over repeated 12-hour windows, while multi-cohort studies have evaluated Mamba and Longformer architectures across institutional, MIMIC-IV, and eICU cohorts. ([pubmed.ncbi.nlm.nih.gov](https://pubmed.ncbi.nlm.nih.gov/36538354/?utm_source=chatgpt.com))

DeLLiriuM represents the strongest direct comparator. It uses structured EHR converted to text across more than 100,000 patients and approximately 195 hospitals, reporting external AUROCs of 0.77 and 0.84. Recent systematic evidence nevertheless concludes that retrospective design, heterogeneous labels, and inadequate external validation continue to prevent clinical generalisation. The present manuscript advances this literature through its analysis of eligibility, assessment history, calibration, and operational workload. It does not, however, establish superior prediction or clinical utility relative to these newer multi-cohort systems. ([arxiv.org](https://arxiv.org/abs/2410.17363?utm_source=chatgpt.com))

## 7. Suggested Reviewer Names

Parisa Rashidi would provide expertise in externally validated longitudinal ICU modelling and is senior author of the DeLLiriuM and multi-cohort acute brain dysfunction programmes. Miguel Contreras would offer direct technical expertise in LLM-based and structured-EHR delirium prediction, although his independence and career stage should be checked. Kyle D. Gong would provide experience in externally validated ICU delirium prediction using clinical and physiological EHR variables. Franck R. Lucini would contribute expertise in recurrent dynamic delirium prediction and clinically timed ICU risk estimation. Reviewer conflicts, recent collaborations, and institutional relationships with Shengliang Ni and Kengo Sato should be verified before invitation.

064063
## 1. Overall Assessment

This manuscript develops an interpretable survival model for predicting major adverse cardiovascular and cerebrovascular events in patients with cardiovascular–kidney–metabolic syndrome stage 4 and established coronary heart disease. The retrospective cohort includes 8,827 patients from seven Chinese tertiary hospitals, divided into a five-hospital training cohort and a two-hospital external validation cohort. Eight baseline variables selected through Boruta, LASSO and variance-inflation filtering were entered into 32 survival-learning algorithms. The Adaptive Oblique Random Survival Forest achieved the highest reported discrimination, with C-indices of 0.892 in development and 0.748 in external validation. The authors supplement conventional evaluation with time-dependent AUROC, calibration, decision-curve analysis, permutation importance, SurvSHAP, SurvLIME and individual conditional expectation analyses. 

The clinical population is relevant and underrepresented in conventional primary-prevention scores. However, the work does not establish a sufficiently substantial advance for Nature Communications. The claimed “dynamic” stratification is principally a post-hoc explanation of a baseline-variable survival model. No longitudinally updated covariates are used. Furthermore, performance decreases markedly under external validation, and comparison with established clinical scores or parsimonious Cox models is inadequate. These limitations substantially weaken both novelty and clinical utility.

## 2. Strengths

The multicentre sample is relatively large for a narrowly defined advanced CKM population. The study includes 1,483 MACCE events over a median follow-up of 40 months, providing a reasonable number of outcomes for model development and validation.

The hospital-level cohort separation is preferable to a random patient split. The external cohort contains data from two institutions not used for training, which provides a more credible test than internal cross-validation alone.

The evaluation extends beyond a single discrimination metric. The manuscript reports time-dependent AUROCs, integrated Brier scores, calibration trajectories, precision–recall analysis and decision-curve analysis. The use of SurvSHAP and SurvLIME also attempts to distinguish population-level variable importance from patient-specific temporal contributions.

The final model uses eight routinely obtainable variables, including fasting plasma glucose, atherogenic index of plasma, diabetes status, HDL cholesterol, monocyte-to-lymphocyte ratio, neutrophil count, diseased-vessel count and implanted-stent count. This compact input set could be operationally feasible if its incremental value were established.

## 3. Weaknesses

The manuscript overstates temporal modelling. All predictors appear to be measured at the index hospitalization. Time-dependent SHAP curves describe how baseline covariates influence estimated survival across follow-up; they do not update risk using changing renal function, glycaemia, inflammation, medication, revascularisation or recurrent events. The resulting model is longitudinal in its outcome formulation, but not dynamically updated in the clinical sense.

External discrimination falls from 0.892 to 0.748. This optimism gap raises concerns about model instability, site effects and overfitting after extensive feature and algorithm selection. The external calibration plot on page 36 also shows visible divergence between observed and predicted survival. Calibration intercepts, calibration slopes and confidence intervals are not reported. Uncertainty around differences between the 32 algorithms is likewise absent.

The comparator framework is insufficient. The manuscript does not establish incremental value over a Cox model using the same eight predictors, established secondary-prevention scores, or the AHA PREVENT framework where applicable. Contemporary evidence indicates that machine-learning cardiovascular prediction studies require rigorous external validation and direct comparison with clinically relevant baselines rather than algorithm-only benchmarking. ([OUP Academic][1])

Potential information leakage is not excluded clearly. The manuscript should state explicitly that Boruta selection, LASSO tuning, variance-inflation filtering, hyperparameter optimisation and model ranking were conducted exclusively within the training hospitals. Missing-data prevalence and imputation procedures are insufficiently documented. Complete-case analysis could introduce selection bias.

No performance analyses are presented by sex, age, renal-function category, diabetes status, hospital, ethnicity or socioeconomic position. All institutions are Chinese tertiary hospitals, limiting transportability to community settings and non-Chinese populations. There is also no prospective workflow evaluation, clinical-impact study, implementation threshold, model code, executable pipeline or sufficiently detailed data dictionary.

## 4. Editorial Decision

**Reject and consider transfer to Communications Medicine.** The multicentre cohort and interpretability analyses are useful, but the manuscript represents an extensive application of established survival-learning and SHAP-based techniques rather than a decisive methodological or clinical advance. The static predictor design, substantial external-validation performance decline, incomplete calibration reporting and absence of strong clinical baselines cannot be resolved through routine editorial revision.

## 5. Suggested Reviewer Expertise

Peer review would require expertise in oblique random survival forests and censored-outcome learning; statistical validation and calibration of clinical prediction models; explainable survival analysis, including SurvSHAP and SurvLIME; multicentre EHR model transportability and dataset-shift assessment; and clinical cardiology covering chronic coronary disease, PCI and advanced cardiovascular–kidney–metabolic syndrome.

## 6. State-of-the-Art Literature Review: Past Three Years

Recent cardiovascular prediction work has shifted from simple algorithm comparisons toward transportability, longitudinal outcome modelling, calibration and clinically meaningful comparison. Forrest and colleagues developed an EHR-derived CAD marker using 95,935 records and validated it in two longitudinal biobanks, demonstrating the scale and independent-population validation now expected for a high-impact contribution. ([PubMed][2]) Shimizu and colleagues reported externally validated and interpretable MACE prediction in a Brazilian hospital network, directly addressing generalisability and individual explanations. ([PubMed][3]) Choi and colleagues subsequently applied time-to-event machine learning to post-PCI MACE and explicitly evaluated time-varying risk-factor contributions, closely overlapping the present manuscript’s methodological positioning. ([PubMed][4])

CKM-specific prediction is also emerging. Recent studies have applied machine learning to mortality and cardiovascular-risk prediction across CKM stages, including analyses using national longitudinal cohorts and interpretable stage-specific models. ([PubMed][5]) Against this landscape, the manuscript’s main distinction is its restriction to stage 4 CKM with established CHD and its combination of AORSF with multiple explanation methods. It does not introduce a new survival architecture, genuinely longitudinal updating, broad international validation or demonstrated clinical benefit. The authors should engage more directly with externally validated MACE models, EHR-derived CAD markers and recent time-to-event post-PCI studies.

## 7. Suggested Reviewer Names

**Gilson Yuuji Shimizu**, University of São Paulo, would provide expertise in externally validated and interpretable MACE prediction across hospital datasets. ([PubMed][3])

**Hong-Jae Choi**, Seoul National University–affiliated research programme, would provide expertise in time-to-event machine learning and temporal interpretation of MACE risk following PCI. ([PubMed][4])

**Michael Schrempf**, associated with the PRECARE-ML work, would provide expertise in model generalisability, external validation and interpretable cardiovascular risk modelling. ([PubMed][3])

**Changhee Lee**, Korea University, would provide methodological expertise in survival machine learning and longitudinal clinical risk prediction. ([PubMed][4])

**Hack-Lyoung Kim**, Seoul National University College of Medicine, would provide clinical expertise in coronary disease, PCI outcomes and the interpretation of MACCE prediction models. ([PubMed Central (PMC)][6])

[1]: https://academic.oup.com/ehjdh/article/6/1/7/7845948?utm_source=chatgpt.com "Machine learning based prediction models for cardiovascular ..."
[2]: https://pubmed.ncbi.nlm.nih.gov/36563696/?utm_source=chatgpt.com "Machine learning-based marker for coronary artery disease: derivation and validation in two longitudinal cohorts - PubMed"
[3]: https://pubmed.ncbi.nlm.nih.gov/39392843/?utm_source=chatgpt.com "Machine learning-based risk prediction for major adverse cardiovascular events in a Brazilian hospital: Development, external validation, and interpretability - PubMed"
[4]: https://pubmed.ncbi.nlm.nih.gov/41308188/?utm_source=chatgpt.com "Risk Prediction of Major Adverse Cardiovascular Events Within One Year After Percutaneous Coronary Intervention in Patients With Acute Coronary Syndrome: Machine Learning-Based Time-to-Event Analysis - PubMed"
[5]: https://pubmed.ncbi.nlm.nih.gov/41289206/?utm_source=chatgpt.com "Cardiometabolic-kidney indices and machine learning ..."
[6]: https://pmc.ncbi.nlm.nih.gov/articles/PMC12699253/?utm_source=chatgpt.com "Risk Prediction of Major Adverse Cardiovascular Events Within One Year After Percutaneous Coronary Intervention in Patients With Acute Coronary Syndrome: Machine Learning–Based Time-to-Event Analysis - PMC"


064561
## 1. Overall Assessment

This manuscript tests whether feature-level fusion of four ophthalmic foundation models—RETFound, VisionFM, RetiZero, and DINORET—outperforms selecting a single model. Gating-based and Top-K router strategies are evaluated across ocular disease diagnosis, systemic disease detection, incidence prediction, multiclass eye-disease classification, low-label learning, and external validation. The main conclusion is that fusion yields selective gains, especially for glaucoma and rare-disease classification, but usually matches rather than exceeds the strongest individual model. 

The study is broad and carefully benchmarked, but it remains an incremental comparison of established mixture-of-experts methods. The central editorial concerns are limited methodological novelty and the absence of convincing clinical benefit relative to the added computational burden.

## 2. Strengths

The evaluation spans AMD, diabetic retinopathy, glaucoma, systemic disease detection, cardiovascular risk prediction, and common and rare eye-disease classification. External cohorts include UK Biobank, SP2, Chaksu, and PAPILA, providing some assessment of domain shift.

The statistical analysis uses 1,000 bootstrap iterations, paired two-sided tests, and Benjamini–Hochberg correction. The models also represent distinct pretraining paradigms, including masked autoencoding, generalist medical-image pretraining, image–language supervision, and DINO-style self-supervision.

The manuscript reports parameters, FLOPs, and inference time. This appropriately exposes the efficiency cost of combining four large encoders.

## 3. Weaknesses

The fusion methods—feature concatenation, soft gating, and Top-K routing—are established. The study does not introduce a new learning objective, routing theory, uncertainty framework, or clinically informed fusion mechanism.

Performance gains are small and task-dependent. Fusion does not consistently outperform the best individual model across AMD, diabetic retinopathy, systemic disease detection, or incidence prediction, and some internal gains disappear externally.

Generalizability remains incompletely assessed. There are no subgroup analyses by age, sex, ethnicity, device, disease severity, or socioeconomic status. Calibration, decision-curve analysis, prospective workflow testing, and comparison with clinicians are absent.

## 4. Editorial Decision

**Reject and consider transfer to npj Digital Medicine.** The work is technically competent and comprehensive, but it is primarily a benchmarking study using familiar fusion methods. The inconsistent gains and limited evidence of clinical utility do not meet the significance threshold for Nature Communications.

## 5. Suggested Reviewer Expertise

Appropriate reviewers should cover mixture-of-experts and dynamic routing for medical imaging; self-supervised and vision–language foundation models for retinal imaging; cross-domain validation, calibration and statistical comparison of diagnostic AI systems; computational efficiency and representation redundancy in model ensembles; and clinical ophthalmology expertise in retinal disease, glaucoma screening and fundus-based systemic-risk prediction.

## 6. State-of-the-Art Literature Review: Past Three Years

RETFound established retinal foundation modelling through masked autoencoder pretraining on 1.6 million unlabelled retinal images and demonstrated adaptation to ocular and systemic disease tasks. ([nature.com](https://www.nature.com/articles/s41586-023-06555-x?utm_source=chatgpt.com)) Subsequent work has shifted toward multimodality, scale and richer supervision. EyeFound was trained on approximately 2.78 million images from 227 hospitals and 11 modalities, while EyeCLIP combined 2.77 million multimodal ophthalmic images with clinical text. ([arxiv.org](https://arxiv.org/abs/2405.11338?utm_source=chatgpt.com)) UrFound incorporated multimodal retinal images and knowledge-guided masked modelling, and RETFound-Green investigated computationally efficient pretraining using substantially less data and compute. ([arxiv.org](https://arxiv.org/abs/2408.05618?utm_source=chatgpt.com)) Morano and colleagues have also introduced a multimodal foundation model and benchmark for comprehensive retinal OCT analysis. ([nature.com](https://www.nature.com/articles/s41746-025-01852-3?utm_source=chatgpt.com))

Against this landscape, the manuscript addresses a relevant but narrower question: whether independently developed encoders should be fused after pretraining. Its finding that fusion is not uniformly advantageous is useful and challenges assumptions that additional experts necessarily improve performance. However, it does not advance foundation-model pretraining, multimodal alignment or clinical adaptation. The closest competing evidence is the recent head-to-head comparison showing that DINOv2 and RETFound have complementary, task-specific advantages, which already supports selective model choice rather than universal dominance. ([pmc.ncbi.nlm.nih.gov](https://pmc.ncbi.nlm.nih.gov/articles/PMC12548085/?utm_source=chatgpt.com))

## 7. Suggested Reviewer Names

For ophthalmic foundation models and self-supervised retinal representation learning, suitable candidates include Justin Engelmann, Miguel O. Bernabeu, Kai Yu and Yang Bai. For multimodal ophthalmic foundation models and benchmarking, suitable candidates include José Morano, Hrvoje Bogunović, Danli Shi and Weiyi Zhang. For mixture-of-experts fusion, efficient medical-imaging architectures and model-selection methodology, suitable candidates include Yuyin Zhou, Jiancheng Yang, Siyu Huang and Yong Liu. For clinical retinal imaging and external validation, suitable candidates include Ursula Schmidt-Erfurth, Mingguang He, Carol Cheung and Andrzej Grzybowski. Reviewer independence and recent coauthorship with the submitting group should be checked before invitation.
