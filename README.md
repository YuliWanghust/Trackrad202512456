# Trackrad202512456

058895
# Editorial Report: "AI-ppendix: Automated Deep-Learning-Based Appendicitis Classification for Patient Stratification"

## Editorial Integrity Alert (Handling Editor Only)

Independent verification found no integrity-level concerns. Citations to Cao et al. (Nat Med 2023), the PANORAMA trial (Lancet Oncol 2025), and Yu et al. (Nat Med 2024) are accurately represented. Table 1–3 case counts cross-check internally without discrepancy. Institutional affiliation (TUM Chair for AI in Healthcare and Medicine) and ethics approval are consistent with public records. The anonymized code repository could not be independently accessed, as expected for double-blind anonymization; the editor should confirm functionality before acceptance. One transparency issue — not integrity fraud — is flagged under Weaknesses.

## Overall Assessment

AI-ppendix pairs a 3D RetinaUNet detection module with a Kinetics-pretrained 3D ResNet18 classifier for CT-based appendicitis diagnosis, evaluated on 601 in-house and 104 external patients and stress-tested in a 12-reader study stratified by experience. The claim that AI assistance narrows the novice-expert gap primarily by cutting false positives is well supported. The two issues most likely to shape the decision are an abstract that misstates the evaluation cohort size and a reader study too small to bear its stratified claims.

## Strengths

The reader-study design is the manuscript's genuine contribution: sequential unaided-then-AI-assisted reads with per-group McNemar testing are the first such comparison for this task, filling a real gap versus the largely standalone-performance appendicitis-AI literature. The model architecture itself closely follows established approaches — video-pretrained 3D-CNN classification, RetinaUNet/nnDetection-style detection — so novelty rests almost entirely on the human-factors evaluation. Honest reporting of a null result in the senior-radiologist arm (p=0.267) and transparent disclosure of external-cohort spectrum bias are genuine strengths that should not be undervalued in review.

## Weaknesses

The abstract states the pipeline "achieved an AUC of 0.92" on a "cohort of 601 patients," but Table 4 shows this figure comes from the n=58 held-out test set, with 543 patients used for training — a conflation that overstates the evaluation cohort as written. The reader cohort (three residents, five seniors) cannot support subgroup inference, and the authors' own acknowledged lack of a washout period risks inflating the reported AI benefit via recall bias. Detection metrics for rare findings (abscess n=7, free air n=28) carry no confidence intervals, unlike the bootstrapped classification metrics.

## Editorial Decision

**Send for Review.** The contribution clears the novelty bar on the strength of the reader study despite an unremarkable model architecture, and the flagged weaknesses are revisable rather than structural. Reviewers should adjudicate whether the no-washout design invalidates the effect sizes, whether the abstract's cohort framing needs correction, and whether small-n detection subgroups warrant bootstrapped intervals.

## Suggested Reviewer Expertise

Reviewers should cover: 3D medical object detection architectures (RetinaUNet/nnDetection-class frameworks); multireader multicase (MRMC) study design and McNemar/recall-bias statistics; automation bias and human-AI collaboration in diagnostic imaging; and, clinically, emergency abdominal CT interpretation and surgical management of complicated versus uncomplicated appendicitis.

## State-of-the-Art Literature Review (Past 3 Years)

The field has moved from binary classification toward clinically embedded evaluation. Cao et al.'s PANDA (Nat Med, 2023) and the PANORAMA pancreatic-cancer trial (Lancet Oncol, 2025) established the template this manuscript follows: standalone AUC plus a stratified-experience reader study. Yu et al. (Nat Med, 2024) demonstrated that experience-based predictors of AI benefit are unreliable at scale (140 readers, 15 tasks) — a finding this manuscript's n=12 cohort cannot engage with statistically, though its qualitative pattern (novice automation-bias risk vs. resident diagnostic-reasoning gain) is consistent with Dratsch et al.'s mammography automation-bias work (Radiology, 2023). Within appendicitis specifically, Kim et al. (Sci Rep, 2025) and the Takaishi et al. 3D localization model (Jpn J Radiol, 2025) are close technical contemporaries the authors should engage with directly; neither, however, includes a comparative reader study, which remains this manuscript's distinguishing claim.

## Suggested Reviewers' Names

**Technical — detection architectures:** Fabian Isensee (DKFZ); Paul F. Jäger (DKFZ); Constantin Ulrich (DKFZ); Michael Baumgartner (DKFZ).

**Technical — MRMC design/AI-assistance statistics:** Feiyang Yu (Stanford/Harvard); Alex Moehring (MIT Sloan); Oishi Banerjee (Harvard Medical School).

**Clinical — automation bias/human-AI interaction:** Thomas Dratsch (University Hospital Cologne); Daniel Pinto dos Santos (University Hospital Cologne); Bettina Baeßler (University Hospital Würzburg).

**Clinical — emergency abdominal/appendicitis imaging:** authors of Takaishi et al. 2025 (Nagoya City University); authors of Kim et al. 2025 Scientific Reports appendicitis 3D-CNN study; a board-certified acute-care abdominal radiologist independent of the submitting group.

## Further Literature (Past 3 Years, Similar Scope)

1. **Kim M, Park T, Kang J, et al.** "Development and validation of automated three-dimensional convolutional neural network model for acute appendicitis diagnosis." *Scientific Reports* 15:7711 (2025). DOI: 10.1038/s41598-024-84348-6. Peer-reviewed. **Cited by manuscript (ref. 13).** Independent author group (Korea). Closest direct comparator to the classification module: a fully automated 3D-CNN (DenseNet169) pipeline with automatic VOI extraction and three-way severity grading (AUC 0.865), though performance is lower than AI-ppendix's, and it lacks a reader study.

2. **Takaishi T, Kawai T, Kokubo Y, et al.** "Deep learning for appendicitis: development of a three-dimensional localization model on CT." *Japanese Journal of Radiology* 43:1859–1869 (2025). DOI: 10.1007/s11604-025-01834-1. Peer-reviewed. **Not cited.** Independent author group (Nagoya City University, Japan). Directly comparable detection task (Faster R-CNN 3D bounding-box localization of the inflamed appendix, radiologist-graded on a Likert scale); the closest published analog to AI-ppendix's detection module and worth engaging directly given the shared localization framing.

3. **Liang D, Fan Y, Zeng Y, et al.** "Development and validation of a deep learning and radiomics combined model for differentiating complicated from uncomplicated acute appendicitis." *Academic Radiology* 31(4):1344–1354 (2024). DOI: 10.1016/j.acra.2023.08.018. Peer-reviewed. **Not cited.** Independent author group (China). Addresses the complicated/uncomplicated stratification that AI-ppendix cites as its clinical motivation, with external validation at three additional centers (AUC 0.72–0.836) — a broader external-validation footprint than AI-ppendix's single external site.

4. **Ghareeb WM, Draz E, Chen X, et al.** "Multicenter validation of an artificial intelligence (AI)-based platform for the diagnosis of acute appendicitis." *Surgery* 176(3):569–576 (2024). DOI: 10.1016/j.surg.2024.05.007. Peer-reviewed. **Not cited.** Independent, international multicenter author group. Different input modality (clinical/lab-score platform rather than CT image analysis) but same diagnostic-accuracy claim space; useful comparator for whether CT-based imaging AI outperforms non-imaging AI tools in the same clinical decision.

5. **Park SH, Kim YJ, Kim KG, et al.** "Comparison between single and serial computed tomography images in classification of acute appendicitis, acute right-sided diverticulitis, and normal appendix using EfficientNet." *PLoS ONE* 18(5):e0281498 (2023). DOI: 10.1371/journal.pone.0281498. Peer-reviewed. **Not cited.** Independent author group (Korea). Extends the diagnostic task to a differential-diagnosis framing (appendicitis vs. mimics) that AI-ppendix's binary appendicitis/non-appendicitis design does not address — a relevant gap for the Discussion.

6. **Zhao Y, Wang X, Zhang Y, et al.** "Combination of clinical information and radiomics models for the differentiation of acute simple appendicitis and non-simple appendicitis on CT images." *Scientific Reports* 14:1854 (2024). DOI: 10.1038/s41598-024-52390-z. Peer-reviewed. **Not cited.** Independent author group (Peking University). Methodologically adjacent 3D appendix-region feature extraction combined with clinical variables; smaller cohort (n=334) but explicitly benchmarks combined vs. imaging-only models, relevant to whether AI-ppendix should incorporate non-imaging features.

7. **Dandil E, Baştuğ BT, Yildirim MS, Çorbacı K, Güneri G.** "MaskAppendix: backbone-enriched Mask R-CNN based on Grad-CAM for automatic appendix segmentation." *Diagnostics* 14(20):2346 (2024). Peer-reviewed. **Not cited.** Independent author group (Turkey). Close architectural and explainability parallel to AI-ppendix's detection module and Grad-CAM analysis; segmentation-level (rather than bounding-box) localization is a relevant point of methodological contrast.

8. **Dratsch T, Chen X, Rezazade Mehrizi M, et al.** "Automation Bias in Mammography: The Impact of Artificial Intelligence BI-RADS Suggestions on Reader Performance." *Radiology* 307(4):e222176 (2023). DOI: 10.1148/radiol.222176. Peer-reviewed. **Not cited.** Independent author group (University Hospital Cologne). Essential empirical counterpoint for the manuscript's automation-bias discussion: shows even highly experienced radiologists are measurably misled by incorrect AI suggestions, evidence the Discussion raises only speculatively.

9. **Yu F, Moehring A, Banerjee O, Salz T, Agarwal N, Rajpurkar P.** "Heterogeneity and predictors of the effects of AI assistance on radiologists." *Nature Medicine* 30(3):837–849 (2024). DOI: 10.1038/s41591-024-02850-w. Peer-reviewed. **Cited by manuscript (ref. 17).** Independent author group (Harvard/MIT). The field's largest-scale MRMC evidence base (140 readers, 15 tasks); the statistical power gap between this study and AI-ppendix's n=12 cohort should be addressed explicitly rather than acknowledged only as a limitation.

10. **Alves N, Schuurmans M, Rutkowski D, et al.** "Artificial intelligence and radiologists in pancreatic cancer detection using standard of care CT scans (PANORAMA): an international, paired, non-inferiority, confirmatory, observational study." *Lancet Oncology* (2025). Peer-reviewed. **Cited by manuscript (ref. 15).** Independent, international consortium. Sets the Lancet-tier methodological bar for stratified-experience reader studies (paired, non-inferiority design, larger reader and case pools) against which AI-ppendix's reader study should be explicitly benchmarked for statistical adequacy.

060822
# Editorial Report

**Manuscript:** Development of an AI-Driven System to Augment Informed Consent in Clinical Trials
**Authors:** Chen, Moscatel, Voutsas, Akhter, Anwar, Lapp, Lee, Bell, Detsky, Quinn (corresponding)

---

## 1. Overall Assessment

This manuscript reports an agentic three-stage LLM system (Coordinator drafts, Moderator scores and blocks out-of-scope queries, Coordinator revises) answering simulated informed-consent questions grounded in two real trials, DEFEND (NCT06792214) and CAN-SILENCE (adapted from van Esch et al., *JAMA* 2021). Across three OpenAI models, the best combination reached near-ceiling accuracy (4.9–5.0/5), and the revise-and-rerate loop improved or held accuracy on average.

The architecture applies an established pattern (critique-revise loops, LLM-as-judge) to a new, high-stakes domain rather than a new technique; its value is empirical. Two concerns dominate: the queries and reference knowledge base were both produced by the same trial-coordinator team that wrote the system prompts, a circularity problem rather than a stated limitation; and the statistics treat clustered, non-independent Likert ratings as independent, likely inflating the significance of the small accuracy differences the results rest on.

## 2. Strengths

The knowledge bases are grounded in genuine trial protocols and consent forms rather than synthetic text. The Moderator-versus-human benchmark is methodologically serious, and finding GPT-5 Chat statistically indistinguishable from human raters is a useful data point for the LLM-as-judge-in-healthcare literature. The guardrail comparison is clean: categorical prompts blocked nearly all adversarial queries versus 5–7% leakage with a vague guardrail.

## 3. Weaknesses

The circular evaluation design cannot test real participant phrasing or ambiguity. The primary statistics (Wilcoxon, Bonferroni across up to 954 ratings) ignore query-level clustering, likely overstating the p<0.001 findings the paper's claims depend on. Figure 5's confusion matrices show a minority of already-correct (5/5) responses dropped as low as 1–2 after revision, undercutting the claim that revision "consistently improved or maintained" accuracy. Only OpenAI models were tested, with no speech modality despite consent typically being verbal, and no subgroup analysis by health literacy or demographics.

## 4. Editorial Decision

Send for Review, conditional on reanalysis correcting for non-independence and a qualitative account of the Figure 5 regressions. Reviewers should adjudicate whether corrected statistics change the headline results, whether accuracy holds against participant-authored queries, and whether the guardrail generalizes beyond the five pre-specified categories.

## 5. Suggested Reviewer Expertise

LLM-as-judge evaluation methodology and inter-rater reliability statistics for clustered ordinal data; retrieval-augmented generation system design for clinical/regulatory documents; adversarial red-teaming and prompt-based safety guardrails for clinical-facing LLMs; research ethics of AI-mediated informed consent; and palliative-care or post-acute COVID-19 cardiovascular trial methodology, matching the two source trials.

## 6. State-of-the-Art Literature Review (Past 3 Years)

LLM-as-judge validity in healthcare has expanded rapidly; a 2026 PRISMA-guided scoping review (Li et al., arXiv 2605.25273) covering 134 studies found judge–human alignment strongest on objective criteria and weaker on nuanced clinical judgment — directly relevant to interpreting why GPT-5 Chat aligned with humans here while GPT-4o and GPT-5 Thinking did not, a pattern the manuscript reports but does not explain mechanistically. Multi-agent LLM systems for clinical trial operations (ClinicalAgent/CT-Agent, Yue & Fu, arXiv 2404.14777) predate this work but target trial administration rather than participant-facing consent; the present manuscript's contribution is the participant-facing domain plus the human-benchmarked Moderator, not the generator-critic architecture itself. On the ethics side, Allen, Schaefer, Porsdam Mann, Earp, and Wilkinson (*Research Ethics*, 2025) propose a five-model taxonomy for LLM-mediated research consent and critique an earlier rule-based consent chatbot (Savage et al., 2024) as non-adaptive; this manuscript's dynamic Coordinator-Moderator loop is a genuine advance over that prior system and should be positioned against it, but neither this ethics paper nor its taxonomy is cited despite being squarely on-topic.

## 7. Suggested Reviewers

**LLM-as-judge / evaluation methodology:** Lingyao Li, University of South Florida — lead author, PRISMA-guided scoping review of LLM-as-judge validity and human alignment in healthcare (arXiv 2605.25273, 2026).

**RAG for clinical/trial documents:** Ozan Unlu, Mass General Brigham/Harvard — first author, retrieval-augmented GPT-4 for clinical trial screening (*NEJM AI*, 2024).

**Guardrails / adversarial safety:** Junhyeok Lee, co-author, benchmark for medical prompt-injection attacks and clinical LLM safety (arXiv 2602.06268, 2026).

**Research ethics of AI-mediated consent:** Jemima W. Allen, Monash University — lead author, five-model taxonomy for LLM-based research consent (*Research Ethics*, 2025).

**Clinical domain (palliative care / post-acute cardiovascular COVID-19):** a trial methodologist independent of the SILENCE and DEFEND investigator groups should be sought; authors of the source trials (e.g., the SILENCE trial team) carry a direct conflict of interest given CAN-SILENCE is adapted from their own published protocol.

---

## Further Literature (Past 3 Years, Similar Scope)

None of the following appear in the manuscript's reference list. All authors are independent of the submitting team (Chen, Moscatel, Voutsas, Akhter, Anwar, Lapp, Lee, Bell, Detsky, Quinn).

1. **Li L, Li D, Chen C, Ma R, Yu R, Lin M, Yin R, Fan L, Shyr C, Ma S, Liu M, Bethard S.** LLM-as-a-Judge in Healthcare: A Scoping Analysis of Applications, Methods, and Human Alignment. *arXiv:2605.25273*, 2026. **Preprint, unreviewed.** Not cited. A PRISMA-guided review of 134 studies finding judge–human alignment is strongest on objective criteria and weaker on nuanced judgment — directly relevant to why the manuscript's GPT-5 Chat Moderator matched humans while GPT-4o and GPT-5 Thinking did not, a pattern the manuscript reports but does not explain.

2. **Genovese A, Hegstrom L, Prabha S, Gomez-Cabello CA, Haider SA, Collaco B, Wood NG, Forte AJ.** Artificial Authority: The Promise and Perils of LLM Judges in Healthcare. *Bioengineering (Basel)*. 2026;13(1):108. doi:10.3390/bioengineering13010108. **Peer-reviewed.** Not cited. Narrative review concluding LLM judges should remain supportive, not substitutive, of human evaluators — bears directly on how much evidentiary weight the manuscript's Moderator LLM should be given as a stand-in for human accuracy adjudication.

3. **Yue L, Xing S, Chen J, Fu T.** ClinicalAgent: Clinical Trial Multi-Agent System with Large Language Model-based Reasoning. *Proc 15th ACM Int Conf Bioinformatics, Computational Biology and Health Informatics (BCB '24)*. 2024:1-10. doi:10.1145/3698587.3701359. **Peer-reviewed.** Not cited. The closest prior multi-agent LLM architecture for clinical trials, though targeting trial operations (outcome prediction, matching) rather than participant-facing consent; establishes that the manuscript's generator-critic pattern is not itself novel to clinical trial applications.

4. **Allen JW, Schaefer O, Porsdam Mann S, Earp BD, Wilkinson D.** Augmenting research consent: should large language models (LLMs) be used for informed consent to clinical research? *Research Ethics*. 2025;21(4):644-670. doi:10.1177/17470161241298726. **Peer-reviewed.** Not cited (distinct from the manuscript's ref. 10, a different Allen/Wilkinson paper on medical-practice rather than research consent). Proposes a five-model taxonomy for LLM-mediated research consent and critiques a prior rule-based consent chatbot as non-adaptive — the manuscript's dynamic architecture is a genuine advance over that baseline and should be positioned against this taxonomy.

5. **Unlu O, Shin J, Mailly CJ, et al.** Retrieval-Augmented Generation-Enabled GPT-4 for Clinical Trial Screening. *NEJM AI*. 2024;1(7):AIoa2400181. **Peer-reviewed.** Not cited. Independent validation that RAG over trial documentation improves GPT-4 accuracy for trial-related tasks, methodologically parallel to the manuscript's RAG pipeline but applied to eligibility screening rather than consent Q&A.

6. **Sehgal NKR, Rai S, Tonneau M, Agarwal AK, Cappella J, Kornides M, Ungar L, Buttenheim A, Guntuku SC.** Brief Large Language Model-Based Chatbot Conversations and Parental Intentions for HPV Vaccination for Children: A Randomized Clinical Trial. *JAMA Netw Open*. 2026. doi:10.1001/jamanetworkopen.2026.16822. **Peer-reviewed.** Not cited. A real-participant (not simulated) RCT finding LLM chatbot effects on health decisions did not outperform, and did not persist as long as, standard materials — a useful counterweight to the manuscript's simulated-query accuracy ceiling, since it measures downstream behavioral impact rather than Likert-rated correctness.

7. **Hou Z, Wu Z, Qu Z, Gong L, Peng H, Jit M, Larson HJ, Wu JT, Lin L.** A vaccine chatbot intervention for parents to improve HPV vaccination uptake among middle school girls: a cluster randomized trial. *Nat Med*. 2025. doi:10.1038/s41591-025-03618-6. **Peer-reviewed.** Not cited. Large real-participant chatbot RCT with actual uptake as the endpoint; illustrates the evidentiary gap between the manuscript's simulated Likert accuracy and the participant-outcome trials this line of work will eventually need.

8. **Li S, Li Y, Zhou S, Tao X, Yu C, Shen M, Chen W, Meng E, Wu B, Huang Q, Mair FS, Zhang J, Zhou J, Zou L, Han S.** A community-codesigned LLM-powered chatbot for primary care: a randomized controlled trial. *Nat Health*. 2026. doi:10.1038/s44360-025-00021-w. **Peer-reviewed.** Not cited. Demonstrates a stakeholder-codesign process for chatbot content, in contrast to the manuscript's prompts, which were designed only by the study team without prospective participant input — relevant to the manuscript's own stated limitation about not capturing real participant phrasing.

9. **Tao X, Zhou S, Ding K, et al.** An LLM chatbot to facilitate primary-to-specialist care transitions: a randomized controlled trial. *Nat Med*. 2026;32(3):934-942. doi:10.1038/s41591-025-04176-7. **Peer-reviewed.** Not cited. A large (n=2,069) real-patient RCT of an autonomous patient-facing LLM performing structured medical intake, with reduced clinician time as a primary endpoint — a model for the kind of prospective, real-participant validation the manuscript's Discussion identifies as necessary but does not attempt.

10. **Lee J, Jang H, Choi KS.** MPIB: A Benchmark for Medical Prompt Injection Attacks and Clinical Safety in LLMs. *arXiv:2602.06268*, 2026. **Preprint, unreviewed.** Not cited. A dedicated adversarial benchmark for prompt-injection and safety failures in clinical LLMs, more systematic than the manuscript's five hand-specified out-of-scope categories; relevant to whether the categorical guardrail would hold against adversarial inputs beyond the pre-specified taxonomy.

061079
# Editorial Report — BEGINN: BSPM-EGM Inference using Neural Networks for Non-Invasive Atrial Signal Reconstruction in Regular Rhythms

## Editorial Integrity Alert (to handling editor, prior to review)

Two items require author clarification before this manuscript proceeds.

First, the Discussion's central fidelity claim — that BEGINN "roughly doubled" the correlation coefficient of "the most recent and methodologically comparable deep learning approach" (Gutiérrez-Fernández et al., ref. 26, *Front. Physiol.* Jan 2026) — omits that two BEGINN co-authors (Guillem, Climent) are also co-authors on ref. 26. This is not disclosed anywhere as an intra-group comparison, unlike ref. 22, which the Introduction correctly flags as "our own preliminary work." The comparison should be reframed as inter-study, not presented as independent external benchmarking.

Second, the simulation database draws its torso and atrial statistical shape models from "the same 42 real patient anatomies," and the clinical validation cohort separately comprises "42 patients" from overlapping institutions (Corify Care/ITACA co-authorship spans both, and Hospital Clínic Barcelona appears in both this cohort and the group's prior digital-twin work). The manuscript never states whether these are disjoint populations. The editor should request explicit confirmation of no overlap, or disclosure if overlap exists.

---

## 1. Overall Assessment

BEGINN is a geometry-free, dual-branch 3D CNN-LSTM autoencoder reconstructing atrial electrograms from body-surface potentials, trained on 16,800 simulations and validated in silico and in a 42-patient, 60-recording multicenter pacing cohort against zero-order Tikhonov ECGI. The rare multicenter clinical validation is the manuscript's genuine contribution, but the comparative narrative rests on a weak classical baseline, an inadequately disclosed benchmark, and clinical localization results that numerically favor the method BEGINN argues against.

## 2. Strengths

The 60-recording, three-hospital, blinded-scoring clinical validation is uncommon rigor; most competing atrial deep-learning ECGI work, including the authors' own VAE model, is simulation-only. The 16,800-simulation database, built with randomized geometric perturbation and 0–20dB noise across a patient-independent 28/7/7 geometry split, is purpose-built to stress geometry independence. The electrode-dropout-augmented dual-branch design targets a real deployment failure mode (lead detachment, high impedance) rather than assuming clean, complete input.

## 3. Weaknesses

The classical comparator is limited to zero-order Tikhonov; stronger published alternatives the authors themselves cite (Schuler's spatio-temporal basis, 7.9mm error at 0dB; L1-norm regularization) are never run head-to-head, inflating BEGINN's apparent margin. Clinical morphology claims (steeper slope, smaller isochrone area) have no intracardiac ground truth, so "physiologically sharper" cannot be distinguished from a prior shaped by simulation training. BEGINN was numerically inferior to classical ECGI on both cavity accuracy (88.3% vs. 93.3%) and neighboring accuracy (85.0% vs. 88.3%); a non-significant McNemar's test in 60 cases is underpowered evidence for equivalence, not confirmation. Validation is confined to paced, regular rhythms, though the Introduction motivates the entire study around AF trigger localization — the actual clinical target — which remains untested.

## 4. Editorial Decision

**Send for Review**, contingent on resolution of the Integrity Alert. Reviewers must be explicitly asked to adjudicate: (1) whether SSM-source and clinical-validation cohorts overlap; (2) whether the ref. 26 comparison should be reframed given shared authorship; (3) whether a stronger classical baseline narrows the reported margin.

## 5. Suggested Reviewer Expertise

Deep-learning inverse ECGI reconstruction and geometry-independent source modeling; 3D convolutional/recurrent architectures for spatiotemporal biosignal estimation; atrial reaction-diffusion simulation and statistical shape modeling; and, clinically, ablation strategy for non-pulmonary-vein AF triggers and electroanatomical map interpretation.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Atrial ECGI deep learning has moved from driver-region classification (Cámara-Vázquez et al., 2021; Gutiérrez-Fernández-Calvillo et al., 2024) toward full electrogram-field reconstruction. The closest competitor, Gutiérrez-Fernández et al.'s dual-branch VAE (*Front. Physiol.*, Jan 2026), reconstructed atrial EGMs from 680 simulated pairs at CC 0.37–0.42; BEGINN's 16,800-simulation, multicenter-validated pipeline is a substantial scale-up, though the comparison is undisclosed as intra-group (see Alert). Geometry-free formulations are also emerging outside the atrial domain — conditional diffusion modeling (Jara & Meyers, 2026) and attention-based ventricular reconstruction (He et al., *Sensors*, 2025) — against neither of which BEGINN is benchmarked. Pilia et al. (*Artif. Intell. Med.*, 2023) documented ventricular localization errors below 3mm in silico growing to 32–47mm clinically; BEGINN reports only categorical clinical localization accuracy, not an analogous mm-level clinical metric, leaving this domain-gap question open.

## Suggested Reviewers

**Technical:** Steffen Schuler (Karlsruhe Institute of Technology) — spatio-temporal regularization for atrial ECGI, *Front. Physiol.* 2018. Nicolò Pilia — deep-learning localization without patient-specific geometry, *Artif. Intell. Med.* 2023. Simone Pezzuto (University of Trento) — computational/reduced-order atrial electrophysiology modeling.

**Clinical:** Michael Thind — noninvasive ECGI localization of non-pulmonary-vein AF triggers, *J. Cardiovasc. Electrophysiol.* 2024. Andrew J. Sharp — extra-pulmonary-vein ablation targets in persistent AF, *Europace* 2025.

---

## Further Literature (Past 3 Years, Similar Scope)

1. **Yin M, Charon N, Brody R, Lu L, Trayanova N, Maggioni M.** "DIMON: Learning Solution Operators of Partial Differential Equations on a Diffeomorphic Family of Domains." *Nature Computational Science* (2024). DOI: 10.1038/s43588-024-00732-y (arXiv:2402.07250). **Peer-reviewed.** Not cited by manuscript. **Independent** — Johns Hopkins, no author overlap. Directly relevant to BEGINN's central geometry-independence claim: learns operators across diffeomorphic heart geometries for EP wave propagation via diffeomorphic mapping to a reference domain, rather than BEGINN's approach of training a fixed-topology network on augmented geometric variation. A principled alternative worth engaging with, though applied to forward simulation, not the BSPM inverse problem.

2. **Zhou B, Corrado C, Qian S, Balmus M, Lee AWC, Rodero C, Roney C, Götte MJW, Hopman LHGA, Plank G, Qiao M, Niederer S.** "A unified framework for geometry-independent operator learning in cardiac electrophysiology simulations." arXiv:2512.01702 (Dec 2025). **UNREVIEWED preprint.** Not cited. **Independent** — Imperial College London/Alan Turing Institute, no author overlap. Highly relevant near-contemporary parallel: reformulates operator learning in an intrinsic coordinate space to decouple prediction from mesh/geometry for full-field activation-time maps — the same geometry-independence goal BEGINN pursues, via a different mechanism (intrinsic manifold coordinates vs. learned latent mapping from augmented simulations).

3. **Li L, Camps J, Rodriguez B, Grau V.** "Solving the Inverse Problem of Electrocardiography for Cardiac Digital Twins: A Survey." *IEEE Reviews in Biomedical Engineering* 18:316–336 (2024). DOI: 10.1109/RBME.2023.3336281. **Peer-reviewed review.** Not cited. **Independent** — Oxford, no author overlap. The most comprehensive recent taxonomy of ECGI inverse-problem methods (classical, Bayesian, and deep-learning); BEGINN should be positioned within this survey's framework rather than compared piecemeal against individually selected prior papers.

4. **Chang Y, Dong M, Fan L, Kang B, Sun W, Li X, Yang Z, Ren M.** "Research on noninvasive electrophysiologic imaging based on cardiac electrophysiology simulation and deep learning methods for the inverse problem." *BMC Cardiovascular Disorders* 25:1 (2025). DOI: 10.1186/s12872-025-04728-2. **Peer-reviewed.** Not cited. **Independent** — no overlap with submitting group. Methodologically parallel (bidomain simulation training data; PSO-BP, CNN, and LSTM compared head-to-head for surface-potential reconstruction), but ventricular rather than atrial, and — notably — actually benchmarks multiple architectures against each other rather than a single classical baseline, a design choice BEGINN's Weaknesses section suggests it should emulate.

5. **Deisenhofer I, Albenque J-P, Busch S, et al.** "Artificial intelligence for individualized treatment of persistent atrial fibrillation: a randomized controlled trial" (TAILORED-AF). *Nature Medicine* 31:1286–1293 (2025). DOI: 10.1038/s41591-025-03517-w. **Peer-reviewed RCT.** Not cited. **Independent** — multicenter European/US consortium, no author overlap. Materially relevant omission: this is the first large multicenter RCT (n=370) to show AI-guided individualized ablation (targeting spatio-temporal dispersion on intracardiac EGMs) outperforms PVI-only for persistent AF. The manuscript's Discussion cites only older negative trials (REAFFIRM, REDO-FIRM) to argue driver-guided ablation lacks proven benefit; this 2025 positive trial should be addressed, as it directly bears on whether BEGINN's sharper, more focal maps could plausibly translate to outcome benefit.

6. **Gutiérrez-Fernández M, López-Linares K, Fambuena-Santos C, Guillem MS, Climent AM, Barquero-Pérez Ó.** "Synthetic Electrogram Generation with Variational Autoencoders for ECGI." arXiv:2512.14537 (Dec 2025). **UNREVIEWED preprint.** Not cited. **Author overlap flagged** — Guillem and Climent are co-authors of both this preprint and the BEGINN manuscript, the same pattern noted in the Integrity Alert for ref. 26. Directly relevant (VAE-based synthetic EGM generation to address atrial BSPM-EGM data scarcity, with a demonstrated downstream reconstruction benefit from augmentation), but should be cited and framed as intra-group work, not treated as an independent data point.

7. **Dermul N, Dierckx H.** "Reconstruction of Excitation Waves from Mechanical Deformation using Physics-Informed Neural Networks." *Scientific Reports* 14:1–16 (2024). DOI: 10.1038/s41598-024-67597-3. **Peer-reviewed.** Not cited. **Independent** — KU Leuven, no author overlap. A conceptually adjacent non-invasive activation-reconstruction approach using PINNs on echocardiographic deformation data instead of BSPMs; useful as a comparator for how physics-embedded regularization (versus BEGINN's purely data-driven latent mapping) handles noise and resolution degradation.

8. **Wang Y, Wang H, Yang Y, Liu Z, Pang J, Cui P, Xiang M.** "Research on spatial resolution in cardiac source imaging for multiple measurement modes using a realistic multi-tissue human model." *Measurement* 243:116353 (2025). DOI: 10.1016/j.measurement.2024.116353. **Peer-reviewed.** Not cited. **Independent.** Not deep-learning-based, but directly relevant to a gap in BEGINN's clinical evaluation: quantifies achievable spatial resolution for cardiac source imaging under realistic multi-tissue torso conductivity assumptions — a resolution ceiling BEGINN's mm-level in silico EAS claims should be discussed against.

9. **[Multi-society scientific statement].** "State of the Art of Artificial Intelligence in Clinical Electrophysiology in 2025." A joint scientific statement of the European Heart Rhythm Association (EHRA), Heart Rhythm Society (HRS), and ESC Working Group on E-Cardiology (2025). PMC12123071. **Peer-reviewed consensus statement.** Not cited. **Independent.** Provides the current clinical-community framing of AI's realistic near-term role in EP labs, useful for calibrating whether BEGINN's claims of clinical readiness are consistent with what practicing electrophysiologists and their societies currently expect of AI-ECGI tools.

10. **Gutiérrez-Fernández-Calvillo M, Cámara-Vázquez MÁ, Hernández-Romero I, Guillem MS, Climent AM, Fambuena-Santos C, Barquero-Pérez Ó.** "Non-invasive estimation of atrial fibrillation driver position using long-short term memory neural networks and body surface potentials." *Computer Methods and Programs in Biomedicine* 246:108058 (2024). DOI: 10.1016/j.cmpb.2024.108058. **Peer-reviewed.** Already cited as ref. 22 and correctly disclosed as "our own preliminary work" — included here only as the properly-disclosed counterpart to the undisclosed overlap in entries 6 and ref. 26, for the editor's side-by-side comparison of how the same authorship pattern was handled differently across citations in this manuscript.

060879
# Editorial Report — Manuscript 060879
**Title:** Multi-granularity few-shot synthesis of ocular adnexal disease phenotypes under clinical image-sharing constraints

---

## Editorial Integrity Alert (to Handling Editor)

Two items require author confirmation before further processing, not evidence of misconduct. First, references 6 and 10 (ROFI, *npj Digit. Med.* 8, 705, 2025; and the multinational ocular-sign segmentation study, *npj Digit. Med.* 9, 130, 2026) share two authors with this submission (C. Lei, H. Zhou) and involve overlapping TED patient populations at Shanghai Ninth People's Hospital. Patient-level independence between the 236-patient SH9H TED cohort used here and the cohorts in refs. 6/10 is not stated and should be confirmed. Second, the stated code repository (github.com/Doro-maodie/FOCUS, per OCR) could not be located via independent search; confirm accessibility with authors before publication.

---

## Overall Assessment

FOCUS is a two-stage few-shot diffusion framework (Ocular Bias Suppression + Lesion Knowledge Injection) synthesizing disease-specific periocular phenotypes for trichiasis, ptosis, and TED from 40 real images/disease, anchored during facial completion for privacy-constrained data sharing. The FOCUS-N ablation and an external, prospectively enrolled CMU-SAH cohort under simultaneous disease-cohort and control-source shift (AUROC 0.4590→0.7398) give this unusual rigor for the genre. The decision hinges on two issues: non-clinically-verified public "healthy" controls, and frame-level rather than patient-level statistics in the sole external validation.

## Strengths

External validation is independent of generator development and stress-tests cohort and control-source shift simultaneously — stronger than most single-site synthetic-augmentation designs. FOCUS-N and the domain-confounding negative control (AUROC 0.50–0.57 with the diagnostic region removed) isolate OBS's contribution and rule out the obvious hospital-vs-public confound. Dual ArcFace privacy stress tests (pooled membership-inference AUROC 0.561 vs. 0.676 for SDXL; zero FOCUS candidates among Top-100 highest-similarity vs. 82–97/100 for SDXL) are appropriately hedged as empirical, not formal, guarantees.

## Weaknesses

Public control datasets (including a facial-beauty-rating set) are not clinically verified normal ophthalmic subjects and were acquired under different protocols, leaving absolute AUROC uninterpretable as diagnostic performance. The 1,076 external frames come from only 128 patients; reported CIs ignore within-patient correlation, inflating apparent precision of the headline result. Few-shot adaptation is fixed at 40 images/disease across three diseases in an Asian-only cohort, with extreme-age/morphology failures acknowledged but unquantified. The report-generation benchmark is circular (disease category supplied as input) and adds little evidentiary weight, as the authors themselves concede.

## Editorial Decision

**Send for Review.** No flaw is structurally fatal — diagnostic claims are already hedged — but control-cohort validity, patient-level independence in the external benchmark, and potential cohort overlap with refs. 6/10 require reviewer adjudication before acceptance.

## Suggested Reviewer Expertise

Few-shot/LoRA-adapted diffusion generation and evaluation (KID, DINOv2, coverage); ArcFace-based re-identification and membership-inference auditing of medical generative models; ResNet-based classification benchmark design with patient-level cross-validation; oculoplastic/ophthalmology clinical expertise in TED, ptosis, and trichiasis; biomedical data-governance and de-identification policy.

## State-of-the-Art Literature Review (Past 3 Years)

Two largely separate tracks bear on this work. Identity-preserving anonymization keeps real images intact while suppressing identity (ROFI, Tian et al., *npj Digit. Med.* 8, 705, 2025 — from the same SH9H group); generative augmentation instead synthesizes new images for data-scarce disease imaging (LoRA-diffusion for rare-class augmentation, arXiv:2605.11898; few-shot brain-tumor synthesis for secure data sharing, arXiv:2504.00150; multimodal text-to-image augmentation for rare eye disease, *npj Digit. Med.* 9, 218, 2026). FOCUS sits between these tracks, combining few-shot phenotype learning with anatomical anchoring and empirical identity-risk screening. It does not, however, engage ROFI's anonymization alternative in its discussion despite shared authorship — an omission reviewers should query, since the manuscript should justify generation over anonymization for this use case.

## Suggested Reviewer Names

*Diffusion/few-shot generative modeling:* Christian Bluethgen (Stanford AIMI — RoentGen/chest X-ray latent-diffusion generation, *Nat. Biomed. Eng.* 2024); Pierre Chambon (co-developer, same vision-language diffusion adaptation line).

*Privacy auditing of medical generative models:* Georgios Kaissis (Technical University of Munich — differential privacy and re-identification risk in medical imaging, *Nat. Mach. Intell.* 2024).

*TED/oculoplastic AI classification:* Xiao Dan Sui (facial-image TED detection, 2025); an independent oculoplastic surgeon with TED/ptosis clinical-photography experience.

*Data governance:* a reviewer with institutional experience in tiered data-access and DUA design for identifiable clinical imaging.

---

## Further Literature (Past 3 Years, Similar Scope)

1. **Tian, Y., Zhou, M., Chen, Y. et al.** ROFI: a deep learning-based ophthalmic sign-preserving and reversible patient face anonymizer. *npj Digit. Med.* 8, 705 (2025). DOI: 10.1038/s41746-025-02062-7. Peer-reviewed. **Already cited by manuscript (ref. 6).** Author overlap: C. Lei, H. Zhou shared with this submission. Anonymizes real periocular images rather than synthesizing new ones — the direct alternative-paradigm comparator FOCUS does not engage with in its Discussion.

2. **Lei, C., Zhao, C., Chen, J. et al.** Enhancing ocular sign detection: AI-based strategic segmentation for improved accuracy and privacy protection. *npj Digit. Med.* 9, 130 (2026). DOI: 10.1038/s41746-025-02310-w. Peer-reviewed. **Already cited by manuscript (ref. 10).** Author overlap: C. Lei, C. Zhao, H. Zhou. Multinational TED cohort (2,360 eyes/1,180 patients, 5 hospitals); segmentation-based privacy rather than generative synthesis — raises the patient-overlap question flagged above.

3. **Chen, R., Zhang, W., Liu, B. et al.** Boosting foundation models for rare eye disease diagnosis via a multimodal text-to-image generative framework (EyeDiff). *npj Digit. Med.* (2026); preprint arXiv:2411.10004 (2024). Peer-reviewed (published version). Not cited by manuscript despite being the closest ophthalmic generative-augmentation comparator — text-to-image synthesis across 14 modalities/80+ diseases for rare-disease classifier augmentation. No author overlap. Directly comparable methodologically; should be discussed.

4. **Wang, J., Wang, K., Yu, Y. et al.** Self-improving generative foundation model for synthetic medical image generation and clinical applications (MINIM). *Nat. Med.* 31, 609–617 (2025). DOI: 10.1038/s41591-024-03359-y. Peer-reviewed, highly cited. No author overlap. General-purpose (non-ocular) synthetic-augmentation foundation model; relevant as a scale/generality contrast to FOCUS's narrow three-disease scope.

5. **Ktena, I., Wiles, O., Albuquerque, I. et al.** Generative models improve fairness of medical classifiers under distribution shifts. *Nat. Med.* 30, 1166–1173 (2024). DOI: 10.1038/s41591-024-02838-6. Peer-reviewed. No author overlap. Directly addresses the demographic-generalizability gap this manuscript leaves unquantified — best-fit comparator for the "Asian-only cohort" weakness.

6. **Bluethgen, C., Chambon, P., Delbrouck, J.-B. et al.** A vision–language foundation model for the generation of realistic chest X-ray images (RoentGen). *Nat. Biomed. Eng.* (2024). DOI: 10.1038/s41551-024-01246-y. Peer-reviewed. No author overlap. Domain-adapted latent-diffusion backbone comparator; illustrates the field's move toward text-conditioned rather than anchor-based control, worth contrasting with FOCUS's structural-anchor approach.

7. Anonymous. Few-Shot Generation of Brain Tumors for Secure and Fair Data Sharing. arXiv:2504.00150 (2025). **Unreviewed preprint.** No author overlap. Closest few-shot generative-synthesis-for-data-sharing comparator outside ophthalmology; useful for benchmarking FOCUS's few-shot sample efficiency (40 images/disease) against another rare-disease, privacy-motivated setting.

8. **Dushenev, D., Karpov, N., Zinovjev, D. et al.** Few-Shot Synthetic Data Generation with Diffusion Models for Downstream Vision Tasks. arXiv:2605.11898 (2026). **Unreviewed preprint.** No author overlap. LoRA-adapted diffusion from 20–50 images for rare-class augmentation (chest X-ray, industrial defects); a lighter-weight architectural alternative to FOCUS's staged OBS/LKI design worth citing as a simplicity baseline.

9. **Ziller, A., Mueller, T. T., Stieger, S. et al.** Reconciling privacy and accuracy in AI for medical imaging. *Nat. Mach. Intell.* 6, 764–774 (2024). DOI: 10.1038/s42256-024-00858-y. Peer-reviewed. No author overlap. Frames the differential-privacy vs. empirical-stress-test distinction directly relevant to FOCUS's explicit disclaimer that its ArcFace screening is not a formal privacy guarantee.

10. **Chen, H., Wang, Z., Sun, L. et al.** Artificial intelligence–enabled facial privacy protection for ocular diagnosis: development and validation study (Digital FaceDefender). *J. Med. Internet Res.* 27, e66873 (2025). DOI: 10.2196/66873. Peer-reviewed. No author overlap. Avatar-fusion privacy protection specifically for ocular/strabismus/ptosis diagnosis in Asian cohorts — closest population- and disease-matched comparator to FOCUS not already in its reference list; should be discussed alongside ROFI as an anonymization-paradigm alternative.

030772
**Reviewer 1 (Xiao, postdoc, US).** Concedes the problem is real but calls the effect modest: mean cross-platform correlation rises from r≈0.36 to r≈0.48, which doesn't support language like "resolve," "reliable replication," or "prioritize signal over platform noise." No true external paired validation cohort exists — CHS/UKB are single-platform and can only confirm that imputed values produce *plausible associations*, not that they match ground truth. The four-tier reliability system is validated on a small ELISA/Quanterix subset (tier-1 proteins plus a few discordant markers) and needs systematic, multi-assay validation with uncertainty intervals. Pearson r alone is inadequate — wants calibration, RMSE/MAE, variance preservation, subgroup and uncertainty reporting. HGB is unbenchmarked against ridge/elastic net, random forest, XGBoost/LightGBM, PLS/CCA, or nearest-neighbor baselines. Flags a likely train/test leak: elastic-net tuning in Application 1 is described as happening on the full cohort *before* the 80/20 split. Calls the protein "importance" analysis (HPA drug-target status, publication count) conceptually weak and recommends demoting it to supplementary. Verdict: not acceptable as submitted; open to reconsideration if these are fixed. Code link broken.

**Reviewer 2 (Sánchez Cabo, assistant professor, Spain).** Sharpest of the three. Core objection: neither SomaScan nor Olink is a gold standard, so "improved concordance" may just mean the model is regressing both platforms toward a shared artifact, not recovering truer biology — wants an orthogonal method (LC-MS) for at least a subcohort. Pushes back on Pearson r specifically: scale-insensitive but not sensitive to systematic bias, so wants Spearman, RMSE/MSE, or concordance correlation coefficient (CCC) instead, and questions why the model's loss function wasn't optimized on anything beyond Pearson. Flags a genuine methodological ambiguity: it's unclear how proteins present in one platform but absent in the other are handled by HGB, since the model handles missing predictors but not missing targets. Notes a circularity risk — KNN-imputed Olink values are used to train the SomaScan-imputation direction. Also catches an internal contradiction the authors should be embarrassed by: Supplementary Fig. 5 claims Spearman >0.8 for all tier-1 proteins under ELISA validation, but the figure shows values below 0.8, and IL1RN — apparently one of the offending proteins — isn't even mentioned in the text. No usable code repository. Verdict to editor: "lack of novelty, limited impact, lack of methodological rigour and important details" — harsher framing than her itemized comments actually require, since nearly everything she raises is a specific, addressable fix rather than a fatal design flaw.

**Reviewer 3 (Wang, postdoc, UK).** Most favorable. Same substantive concerns as R1/R3 but lower alarm: wants the correlation-gain range quantified in the intro, wants the tier system's added value tested against simple baseline-correlation grouping (echoing R1's tier-validity concern — tier-1 proteins show strong correlation *with or without* imputation, undercutting the tiering rationale), wants Application 2/3 findings extended from a handful of cherry-picked proteins to a systematic pre/post-imputation concordance analysis across the full protein set, and flags pQTL replicability as an under-explored future direction. Left the "Remarks to the Editor" field blank — no separate top-line verdict recorded. Code link also unavailable.

**Convergent findings (3/3 reviewers).** No independent orthogonal validation beyond a small existing ELISA/Quanterix sample; sole reliance on Pearson r as the performance metric; unresolved concerns about the tier system's actual discriminative value; cherry-picked rather than systematic protein-level reporting in the applications; and a non-functional code repository — unanimous across all three, which is a hard requirement for a Nature Communications submission, not a nice-to-have. The handling editor's own pre-review circulation note (Eric Wang, 27 Apr) independently flagged the missing comparison against cpiVAE, a contemporaneous variational-autoencoder approach on the same CKB paired-proteomics problem, as an "unacceptable omission" — this wasn't raised by name in any of the three formal reviews but reinforces R1's benchmarking complaint with a specific, citable competitor.

**Decision: Major Revision, not Reject.**

None of the three flaws that would normally force a reject — fabrication, an irreparable design flaw, or a reviewer explicitly closing the door — is present. R1 explicitly conditions reconsideration on fixes; R3 treats the issues as revision items; R2's comments, despite the harsh top-line language, are itemized and addressable (orthogonal validation subcohort, additional metrics, clarified methodology, corrected figure/text discrepancy). The "no gold standard" problem is a real limitation of the domain, not of this paper specifically, and is manageable by reframing claims and adding LC-MS/expanded ELISA-Quanterix validation rather than by starting over. Required before re-review: genuine orthogonal validation across all four tiers (not just tier 1); benchmarking HGB against at least elastic net, random forest, and cpiVAE; metrics beyond Pearson r (CCC, calibration, subgroup performance); a leakage audit of the Application 1 pipeline; tier-threshold sensitivity analysis; resolution of the Supp Fig. 5 / IL1RN contradiction; and a working code repository — the last one non-negotiable given unanimous reviewer complaint.

**Counterargument for Reject, steelmanned.** One could argue this is a structural problem rather than a fixable one: the paper's central claim — that imputation recovers true cross-platform biology rather than shared model artifact — rests entirely on an evaluation framework (same-cohort Pearson r, no held-out gold standard) that all three reviewers independently found insufficient to support *any* of the downstream claims. If the authors cannot produce genuine orthogonal validation, the core contribution is unfalsifiable with the data at hand, which argues for reject encouraging resubmission rather than revision-in-place. I don't think this wins, mainly because the authors already possess partial ELISA/Quanterix data and R2 herself proposes LC-MS as an achievable extension — the fix is a matter of scope, not data availability. But if the revised manuscript comes back without a real independent validation cohort, that's the point to reject outright rather than send for a third round.

**Blind spot.** This assessment is built entirely from the review record, not the manuscript itself — I haven't independently verified the reviewers' characterizations (e.g., whether the GitHub repo is actually dead right now, or whether cpiVAE is a fair comparator) against primary sources, which your workflow normally requires before a report is finalized. If you want that verification run before the decision letter goes out, say so and I'll check the repo and the cpiVAE preprint directly

030231
This upload is the reviewer/editor tracking record, not the manuscript itself — so this is a synthesis-and-decision task on completed reviews, not a fresh independent-verification report.

**Reviewer #1 (Qiao Jin, code checked but not run).** Three substantive concerns. First, novelty against MetaMedQA (Nat Commun 2024) is unresolved — that paper already scores confidence, missing-answer recognition, and unanswerable-question detection in medical QA; CLEAR cites it but doesn't establish what's qualitatively new. Second, construct validity: collapsing NA/IDK/INA into equivalent "abstention" outcomes is unsupported — these may reflect option familiarity or refusal bias rather than genuine epistemic humility, and no clinician validated that perturbed items are actually unanswerable. Third, the baseline set is thin for a calibration paper — no log-probability or self-consistency comparators, and abstention labels are synthetic with no item-level clinical adjudication.

**Reviewer #2 (Jie Yang, did not review code).** Longer but converges on the same core problem from a different angle, plus adds: possible train/test leakage since MedMCQA/MedQA/JAMA-CC are old public benchmarks that later models may have seen; no test for answer-position/order effects on distractor perturbation (cites Pezeshkpour & Hruschka, NAACL 2024); Methods content misplaced under Results; and several undefined procedures (distractor generation, accuracy calculation when no ground truth is present, sampling for the 1,200-query subset). Scope is also narrowed to English, classification-format tasks only.

**Reviewer #3 (Bowen Gu, ECR).** No independent assessment — explicitly co-reviewed and deferred to the paired reviewer's report. Treat as non-independent; it doesn't add evidentiary weight.

**Convergence point.** The handling editor's own pre-review note (Eric Wang, 8 May — written before either report came back) flagged the identical weakness independently: the "humility deficit" metric can't distinguish genuine uncertainty from prompt-pattern matching, distractors aren't stratified by semantic proximity to ground truth, and the GPT-5.2 result conflates a cross-family comparison with the paper's within-family scaling claim. Three independent assessors landing on the same structural issue — unvalidated abstention-category equivalence — is a stronger signal than any one complaint in isolation.

**Decision: Major Revision, not outright reject.** Every flaw raised is addressable with concrete added work — clinician-adjudicated distractor plausibility, a naturally open-ended unanswerable task, log-prob/entropy baselines, and a leakage discussion — none require the authors to abandon the framework wholesale. That's the line the skill draws between revisable and structural flaws, and this falls on the revisable side.

**Pushback on my own call.** The strongest counterargument: if the humility-deficit metric is epistemically invalid as constructed, adding baselines doesn't fix it — it requires re-deriving the central measure the paper's headline claim rests on. That's not a patch, it's a different experiment, and reviewers don't get to see whether the "fix" still supports the original narrative until it's redone. If you don't have confidence the authors can produce a genuinely reworked uncertainty metric (vs. cosmetic additions), reject-with-encourage-resubmission is the more defensible call than major revision, since it doesn't bind the journal to accepting a patched version of a possibly unsalvageable core claim.

**Blind spot worth flagging:** no reviewer independently ran the code — Reviewer #1 only inspected it, Reviewer #2 skipped it, Reviewer #3 deferred. Reproducibility is unverified going into any revision decision.

0266623
## Reviewer Summary

**Reviewer #1 (Astrid Vicente, lab director)** — Calls the hair-based elemental homeostasis approach genuinely novel, but says the paper overstates clinical stratification utility given the sample size and lack of validation. Six specific objections: (1) the title's "temporal molecular dynamics" oversells what is really 12 elements measured over time; (2) no biological/etiological grounding for why these elements would track ASD, despite two of the cohorts (MARBLES, CHARGE) having exposure data that was never integrated; (3) unclear whether the 12-element panel is jointly necessary or whether one or two elements are doing all the work; (4) no per-element results shown, so age-driven variability can't be assessed; (5) discussion overstates diagnostic-tool potential; (6) claims of cross-age, cross-geography generalizability are unsupported — only median ages are given, and cohorts differ wildly in size and case/control balance.

**Reviewer #2 (Shyam Sundar Rajagopalan, assistant professor)** — Same enthusiasm for the concept, but flags the results themselves as weak and the methods underspecified. Key point: Stage 2 AUC is 0.67 overall, 0.56 in males, 0.61 in females — barely above chance — while specificity is reported as high (86–96%) with no sensitivity/F1 given, which is a selective reporting problem. No standard deviation across CV folds is reported, so robustness is unverifiable. Most serious: the Stage 2 training population's median ages run from roughly 12–14 years down to several years across RATSS/CHARGE/MARBLES, yet the manuscript's claimed use case is stratifying children **1–18 months** old. He asks directly whether results generated in adolescents can support inference in infants. That's not a wording problem — it's a mismatch between the population studied and the population the paper claims to serve.

**Reviewer #4 (Parnian Azizian, PhD candidate) + Reviewer #5/ECR (Honarmand, co-review)** — Three points. First, the two-stage validation isn't clean: Stage 2 was built after Stage 1 had already been evaluated on the same validation set, so the combined pipeline's reported performance is likely optimistic — an untouched end-to-end test set was never used. Second, ~70% of participants land in the "intermediate" bucket where the likelihood ratio is ~1.09 (i.e., non-informative), male Stage 2 AUC is 0.56, and the female analysis has only 12 cases across three cohorts — underpowered to the point of being uninterpretable. Third, autism status is confounded with site/lab, and cases and controls differ in age across cohorts; sulfur normalization helps but there's no explicit age-matched or leave-one-site-out analysis to rule out the model learning site signature rather than biology.

**Handling editor (Eric Wang)**, in the pre-review circulation note, independently converged on the same two headline concerns: near-chance Stage 2 discrimination and data-leakage risk from the multi-step cohort splitting. That was a pre-review screening note ("OTR"), not a post-review decision — no decision letter has been issued yet, which is what you're asking me to render now. (Side note: the record jumps from Reviewer #1 to #2 to #4 — there's no Reviewer #3 in this file. Worth confirming that reviewer didn't submit, rather than the report being incomplete.)

## Decision: **Reject**

Not revise-and-resubmit. Three of the four substantive reviewers independently converge on the same failure, from different angles, and at least two of the problems are structural rather than fixable by rewriting or adding analyses:

1. **The primary clinical claim doesn't survive its own data.** Stage 2 — the stage that's supposed to deliver the "high-likelihood" clinical value — is at AUC 0.56–0.61, indistinguishable from chance in any Lancet-caliber read. A revision doesn't fix an underpowered, non-discriminative model; it needs new data and a redesigned stage.

2. **The evidence doesn't match the claimed use case.** The model is trained and validated in children with median ages in years, sometimes into adolescence, but the paper's translational pitch is 1–18-month risk stratification. That's not a discussion-section caveat, that's the wrong population for the stated indication. No amount of revision to the existing dataset resolves this — it requires a genuinely different, age-appropriate cohort.

3. **Case/control status is confounded with site**, and the validation design lets Stage 2 see information from data used to tune Stage 1 — meaning even the numbers reported for the "good" stages (accuracy ~0.70–0.78, Stage 1 sensitivity ~90–96%) are of uncertain trustworthiness. Until a genuinely held-out, site-stratified pipeline is run, none of the topline numbers in this paper can be taken at face value.

Individually, #3 might be revisable. Combined with #1 and #2 it isn't — you'd be asking authors to fix the population studied and the analysis pipeline and the central performance result, which is a new study, not a revision.

**Transfer suggestion**: the multinational hair-biomarker angle has genuine translational interest for a methods-focused, lower-bar venue — *npj Digital Medicine* or *Communications Medicine* — with an explicit requirement that they either reframe as infant/toddler-only proof-of-concept in age-matched data, or drop the early-stratification claim entirely and present Stage 1 as an exploratory biomarker-discovery result.

Yes — on reconsideration, most of what I flagged is addressable through re-analysis of existing data and reframing of claims, not new patient enrollment. That changes the calculus. The one thing that would still be fatal is spelled out at the end.

**Revised decision: Major Revision**, contingent on the tripwire below.

## Required revisions

**1. Drop or rescope the infant-screening claim.** The manuscript's stated use case (1–18-month stratification) doesn't match the age of the cohorts actually analyzed (median ages spanning several years up to ~14). Authors must either restrict all clinical-utility claims to the age ranges actually sampled, or explicitly show — with data, not assertion — that the biomarker signal extrapolates downward to infancy. If they can't do the latter, the fix is claims, not new data.

**2. Rebuild the validation so it's actually held out.** Reviewer #4's core objection stands: Stage 2 was developed after Stage 1 had already seen the validation set, so the two-stage AUCs are optimistic by construction. Require a genuine end-to-end test split, untouched until final evaluation, with the full two-stage pipeline run on it once.

**3. Rule out site as the real signal.** Cases and controls differ in age by cohort, and autism status tracks site. Require leave-one-site-out cross-validation and an age-matched or age-adjusted sensitivity analysis. If performance collapses under leave-one-site-out, that tells you the model was learning batch/site signature, not biology — this is the one result that would flip Major Revision back to Reject (see below).

**4. Report the statistics they're currently omitting.** SD of AUC across folds, sensitivity and F1 alongside specificity (not specificity alone, which is currently cherry-picked to look better than it is), and confidence intervals on all reported AUCs — Stage 2 in particular, where 0.56/0.61 needs an honest interval, not just a point estimate.

**5. Identify which elements are actually driving stratification.** Per-element results, not just the aggregate 12-element panel. If one or two elements carry the signal, say so; if all 12 are needed, demonstrate that with an ablation.

**6. Address the female Stage 2 model directly.** 12 cases across three cohorts is not a result, it's a pilot observation. Either drop it, flag it explicitly as underpowered and non-conclusive, or pool additional female cases before reporting an AUC at all.

**7. Ground the biology.** Integrate the environmental exposure data already available in MARBLES and CHARGE. Right now the paper claims a biomarker without any etiological hypothesis for why these 12 elements should track ASD — reviewers want at minimum a plausibility argument, ideally a correlation with known exposure variables.

**8. Fix reproducibility gaps.** Final hyperparameters for ExtraTrees/other classifiers, the feature-engineering and standardization pipeline per CV fold, and — since it was asked directly — a commitment on whether code will be released.

**9. Fix the title and moderate the framing.** "Temporal molecular dynamics" oversells a 12-element hair panel. Retitle to reflect what was actually measured, and moderate every claim of clinical/diagnostic readiness to "proof of concept, pending replication," consistent across abstract, results, and discussion — not just hedged once in the limitations paragraph.

## The tripwire

If item 3 (leave-one-site-out) shows performance drops toward chance across the board, that means the reported accuracy (~0.70–0.78) was substantially a site artifact, not a biological signal — at that point there's no revision that saves the paper, since the central claim was never real. That result should be requested from authors before deciding whether to send this back to reviewers at all, or handled as a condition reviewers explicitly check in re-review.

041269
I compared the completed author checklist with the revised manuscript. The authors have addressed many administrative and structural points, but **they have not addressed every requirement completely**. Several responses overstate what is actually present in the manuscript.  

## Items that still require correction

1. **Randomization and blinding statements are missing**

The checklist explicitly requests statements addressing whether randomization and blinding were used. The “Statistics and reproducibility” section discusses sample size, exclusions, statistical analysis, and sensitivity analyses, but it does not state either:

* “The experiments were not randomized.”
* “The investigators were not blinded to allocation during experiments and outcome assessment.”

Therefore, the author’s response that this requirement was addressed is incomplete.  

2. **The SAGER sex/gender requirements are not adequately addressed**

The Methods identify the cohort as 284,002 women aged 35–64 years and provide recruitment and informed-consent information. However, the manuscript does not explain:

* Whether sex or gender was considered in the study design.
* Whether participant sex/gender was self-reported, assigned from administrative records, or determined by another method.
* Why no sex- or gender-based analysis was performed.
* Whether participants received compensation. Free screening is described, but that is not a compensation statement.

Thus, the response claiming compliance with the SAGER guidance is not supported by the manuscript. 

3. **The data-availability statement remains incomplete**

The statement appropriately provides a privacy-based reason, a contact person, an academic-use restriction, an approval requirement, and a one-month access period. However, it does not provide the requested **expected timeframe for responding to a data request**. It also refers generally to “ethical and legal concerns” without identifying the specific ethical, consent, legal, or institutional restrictions governing access.  

Suggested additions include:

> Requests will be reviewed within approximately X weeks of receipt.

and a clearer description of the applicable ethics approval, data-use agreement, eligibility criteria, and permitted research purposes.

4. **The Zenodo code record is not cited in the reference list**

The manuscript now provides both a GitHub repository and a Zenodo DOI, which is an improvement. However, the checklist specifically requested that the DOI-minting repository be **cited in the reference list**. The reference list begins immediately after the Code Availability section, but no Zenodo dataset/software citation is included.  

5. **“Novel” and exaggerated language remain**

The response states that “new/novel/first” and exaggerated language were removed. However, the manuscript still contains:

* “the **novel** AI-LBC method”
* “**much improved** accuracy”
* “can **massively scale-up**”
* “**crucial** empirical evidence”
* “**high-grade**, practice-oriented evidence”
* “demonstrated **excellent** screening performance”

These should be replaced with neutral, evidence-based wording.  

6. **Not all acronyms are defined before first use**

Examples include:

* **NILM** is used in the Results before its full definition appears later in Methods.
* **PPV** is used in the Results before “positive predictive value” is defined.
* “ASC-US+” is used without immediately explaining that “+” means “or worse.”

The figure captions define many of these terms, but the main text must independently define them at first occurrence.  

7. **The Methods still rely on previous publications**

The checklist asks for sufficient methodological detail to reproduce the study without referring to earlier publications. However, the Methods state that:

* “The complete technical details, training process, and external validation have been previously published.”
* “More detailed screening procedures were described in previous studies.”

This is not fully compliant. Essential model, workflow, preprocessing, quality-control, and implementation details should be included directly in the Methods or Supplementary Information. 

8. **Self-selection bias is not explicitly discussed**

The recruitment procedures are described, and the manuscript states that participation was voluntary. However, the requested discussion of potential **self-selection bias and its likely effect on the results** is absent. The limitations discuss verification bias and single-city generalizability, but not whether volunteers may differ from eligible nonparticipants.  

9. **There is a substantive numerical inconsistency in Figure 2**

On manuscript page 33, Figure 2 reports a sensitivity of **60.05%** for Strategy 2. However:

* The Results state **62.05%**.
* Table 2 reports **62.05%**.
* Figure 3 reports **62.05%**.

Figure 2 should therefore be corrected from 60.05% to 62.05%. This is a material inconsistency, not merely a formatting issue. 

10. **Figure 1 contains several typographical and labeling errors**

On manuscript page 32:

* “ASCH” should be “ASC-H.”
* “HPV1618” should be “HPV16/18.”
* “diffenent” should be “different.”
* “diferent” should be “different.”

These errors conflict with the claim that the figures have been fully prepared according to the journal’s artwork requirements. 

11. **The source-data response is incomplete**

The checklist specifically asks that the response include the Source Data file’s **title and a brief description**. The response only says that an Excel workbook was prepared and uploaded. It does not provide the requested title and description. The manuscript correctly includes the required source-data wording in the Figure 1 legend and Data Availability section, but the workbook itself was not provided for inspection. 

12. **The software/version statement is not fully supported**

The manuscript identifies R version 4.2.2 and the scanner/analyzer version V1.2. However, it does not list the names and versions of the R packages used for Bayesian modeling, multiple imputation, recalibration, Rubin’s rules, graphics, or other analyses. The AI diagnostic system or algorithm also lacks a specific software/model version. Therefore, the claim that all software, algorithms, tools, and packages are listed with versions appears too broad.  

13. **Minor structural issue**

The manuscript heading is “Reference” rather than the requested “References.” This is minor but should be corrected. 

## Requirements that appear adequately addressed

The following points are supported by the revised manuscript:

* The title has 14 words and no punctuation.
* The abstract uses present tense for the current study and appears to meet the 200-word limit.
* Affiliations are sequentially numbered.
* Corresponding and equal-contribution authors are marked with symbols.
* All authors appear in the Author Contributions statement.
* The main manuscript contains four figures and two tables.
* The requested main-section order is substantially followed.
* The ethical approval committee, institution, approval number, and signed informed consent are provided.
* Sample-size selection and the exclusion of 571 participants are described.
* The Figure 1 legend and Data Availability section contain the requested source-data statements.
* Funding, author contributions, and a negative competing-interests statement are present.   

## Items that cannot be verified from the supplied files

The supplied PDF appears to contain the main manuscript, tables, legends, and figures, but not all of the other submission materials. Therefore, I cannot verify:

* The Supplementary Information PDF and its references.
* The Reporting Summary and its software/data entries.
* The actual Source Data Excel workbook.
* Separate editable vector figure files.
* The cover-letter website summary.
* Whether the Competing Interests statement matches the submission system.
* Whether all uploaded files are below 30 MB.
* Third-party rights or BioRender documentation.
* Whether tracked changes were removed from Supplementary Information.
* Whether the author names and affiliations were independently confirmed by all coauthors.

**Overall assessment: the response is partially satisfactory but should not be considered fully complete.** The randomization/blinding statements, SAGER information, data-access details, Zenodo reference, numerical figure inconsistency, and remaining “novel” or promotional language are the most important points to return to the authors.
