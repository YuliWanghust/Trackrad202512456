# Trackrad202512456

NCOMMS-26-062269-T — Reviewer Synthesis and Decision

## Where the reviewers converge

All three reviewers raise four concerns independently. These should anchor the decision letter.

**Unit of analysis and split integrity.** Performance is reported per image, but patients contribute many images. ZJH-8K alone contains 7,958 images from 1,149 cases, about 6.9 images per case. Confidence intervals are therefore likely too narrow (R1, R2, R3).

The headline figure of "28,458 non-overlapping test cases" is arithmetically 19,737 test images plus 8,721 NHC-MISD-TUS cases. It adds images and cases together, so R2's objection is confirmed. Patient-level splits, deduplication across datasets, and cluster-aware bootstrap intervals are required.

**The agentic router has not been shown to contribute.** The system combines a DINOv3 expert pool, radiomics via AutoGluon, multicohort training and template reporting. Any gain could come from these components rather than from LLM routing (R1, R2, R3). R1 and R3 converge on the same ablation ladder: a single model, majority voting or probability averaging, rule-based routing, a non-LLM learned router, LLM routing, and an oracle upper bound.

R3 adds a sharper point. The router receives device and data-source metadata, so it may be learning centre identity rather than case-level evidence. It needs an ablation with metadata removed. R2 asks for router reproducibility: prompt, model version, decoding parameters, stability across repeated runs, and representative traces.

**ThyClinScore is validated only against an LLM judge.** The metric was developed by the authors and is validated mainly by correlation with an LLM judge (R1, R2, R3). Blinded multi-radiologist ratings, inter-rater agreement, and sensitivity analysis of the weights λ and η are needed.

R2 notes that λ and η appear to have been tuned on the same data, which risks overfitting. R3 notes that ThyroidXAgent does not beat all baselines on every submetric, and the manuscript should say so.

**The reader study is underpowered and possibly confounded.** It uses two physicians and 145 cases, and it reports no per-reader results, confidence intervals, or paired or mixed-effects statistics (R1, R2, R3).

## Additional substantive issues from individual reviewers

**External cohorts may not be external.** R2 notes that ZJH-8K and TN3K both come from Zhujiang Hospital, Southern Medical University. R1 notes that ZJH-8K malignant images were also used to develop the lymph-node metastasis (LNM) and FTC/PTC tasks. Either finding could invalidate the external-validation claim for the affected tasks.

**The FTC/PTC target changes between training and testing.** R2 reports that training used classic PTC and follicular-variant PTC, while the external test set used FTC and PTC. Follicular-variant PTC is not FTC, so the external result may be measuring a different task.

**The LNM task is underpowered and inconsistently defined.** It uses 4,753 images, and Table S5 has only 20 validation cases. The label switches between overall, lateral, central-compartment, and CN0/CN1 status (R2). This is the weakest task in the paper and cannot be fixed by reanalysis alone.

**Centre-level heterogeneity is not reported.** NHC-MISD-TUS spans 35 centres, but per-centre numbers are missing. Segmentation performance drops at some centres, and abstention and escalation policies are not defined (R1, R2).

**Ethics documentation is incomplete.** Consent or waiver details are missing for each institutional dataset. Authorization of NHC-MISD-TUS by a co-author is not a substitute for ethics approval (R2).

**Reproducibility gaps remain.** The repository has no licence, no tagged release and no tests (R2). The "training-free" claim should be qualified because the system depends on BM25 corpora and hand-built templates. Post-processing thresholds and the AutoGluon branch are not specified.

**Baseline comparisons may be unfair.** R2 asks whether baselines were retrained or used zero-shot. R3 notes that the multimodal LLM baselines receive raw images, while ThyroidXAgent receives structured tool outputs.

## Inconsistencies you should resolve before writing the letter

R1 calls the reader study a crossover, in which the same reader sees both conditions. R2 states that each case was read under the two conditions by different readers. These are incompatible designs, and the correct statistical demand depends on which is true. Check the Methods.

Eric Wang's circulation note reports time reductions of "approximately 36% for physicians and 27% for doctors." Physicians and doctors are the same group, so the two groups are presumably different seniority levels. Correct the wording before it appears in any letter.

R1's recommendation of "major revision" sits in the code-availability field. R1's Remarks to the Editor simply duplicate the author comments. R2 and R3 give no explicit recommendation. You therefore have one explicit vote, and no confidential editor-only input from any reviewer.

R2's first point, that key values are inconsistent across the abstract, main text, figures and supplement, cites no specific values. Ask the authors for a full reconciliation table rather than passing on a vague criticism.

## Decision: Major Revision

No reviewer identifies misconduct or a fatally flawed premise. Most of the major concerns can be resolved by reanalysing data the authors already hold. These include patient-level reanalysis, clustered confidence intervals, router and metadata ablations, per-centre reporting, a data-flow diagram, reclassification of the Zhujiang cohorts, and ThyClinScore sensitivity analysis.

The 35-centre, multi-device scale and the editable evidence-store design are distinctive. Clinician correction of intermediate outputs is also genuinely useful. Together these justify giving the authors a chance.

Two items require new work or reduced claims. First, the reader study should be expanded to a proper multi-reader multi-case (MRMC) design with readers of varied seniority and randomized case order. Otherwise, all claims of clinical or workflow benefit must be recast as feasibility findings. Second, the LNM task must be either properly powered and consistently labelled, or removed.

The letter should state explicitly that the manuscript will be rejected if the router ablation shows no advantage over non-LLM ensembling. The same applies if external-validation performance collapses at patient level once the Zhujiang cohorts are reclassified. The paper's central claim depends on both.

## Counterargument: the case for rejection

The contribution the authors actually claim, *agentic* orchestration, is the one element with no supporting evidence. Every component beneath the router already exists.

The external-validation claim is compromised for at least two tasks: the Zhujiang cohorts and the FTC/PTC label shift. The LNM task is underpowered. The report metric is self-built and validated by an LLM. The clinical evidence rests on two readers.

If the router ablation fails, what remains is a well-engineered thyroid ensemble with template reporting. That is an npj Digital Medicine paper, not a Nature Communications paper. Four headline claims currently lack support, so a "major revision" risks becoming a new study reviewed as a revision.

I rejected this position for two reasons. The fixes are largely analytic rather than new-data collection. And the reviewers, who read the full paper, did not recommend rejection. Setting explicit failure conditions in the letter keeps that exit open.

## What you are not asking but should

**Data governance for the LLM calls.** No reviewer asked which LLM the router uses, or whether patient images or reports are sent to an external commercial API. For an auditable clinical system, this is a governance question the letter should raise.

**Statistical expertise on the panel.** None of the three reviewers is a biostatistician. This matters because the unit-of-analysis problem and the MRMC redesign are statistical at their core. Consider adding a statistical referee at revision, or asking R1 to adjudicate those points specifically.

**Data availability.** The licence gap is an enforceable Nature Communications policy requirement, not optional polish. Data availability for the private cohorts also needs an explicit statement.

051646
## Reviewer summary

**Reviewer #1 recommends outright rejection.** The core arguments are fourfold. The contribution is incremental: GBTM-plus-classifier pipelines for adherence are established, the four trajectories replicate the literature, and the Bayesian prior is framed as parametric tuning rather than a new framework. Performance is inadequate for individual decisions: external macro-AUROC is about 0.72, multiclass accuracy is below 0.56, performance depends heavily on follow-up dispensing data rather than baseline data, and there are no subgroup analyses for high-risk populations. The translational claims are overstated: the counterfactuals are non-causal yet drive intervention recommendations, the "levers" restate guideline care, and there is no prospective evaluation. Finally, the limitations section is superficial on confounding and correlated-feature bias.

**Reviewer #2 (with ECR Sciacca, who inspected the code)** writes a revision-style report to the authors but tells the editor the paper lacks Nature Communications priority. Their major points are these:

1. The trajectory phenotype is already published. Orman et al. (Br J Clin Pharmacol 2025) used the same IQVIA source, overlapping authors, and the same four trajectories with near-identical proportions.
2. Early prediction is weak. External macro-AUROC is 0.62–0.63 in the initial window versus about 0.72 at landmark, so BRIDGE works as an early-warning tool during follow-up rather than a predictor at initiation.
3. The outcome is prescription persistence, not adherence.
4. The value of the barrier-informed priors is not isolated. The reviewer asks for an ablation against neutral priors.
5. The counterfactuals have a reverse-causality problem: LDL and blood pressure partly reflect persistence. The analysis is also restricted to correctly classified cases.
6. There is no class-specific external calibration.

Minor points include the 80/20 vs 85/15 split in Figure 2 vs Methods, data-end dates (Aug vs Mar 2025), the "CONSORT" label, and "superior performance" claims when tree models win internally.

Your own circulation note anticipated most of this. It flagged that BRIDGE is the weakest model on every internal metric, that the priors come from an unvalidated hypothetical-vignette survey with no sensitivity analysis, that "external" validation stays within IQVIA Australia, and that there is no equity subgroup analysis.

## Decision: Reject, with transfer offer

Both reviewers converge against publication here. R1 does so explicitly; R2 does so in confidential remarks. The decisive issue is that each pillar of the novelty claim fails on its own terms:

- **The phenotype** is prior work by the same group.
- **The central methodological contribution (barrier-informed priors)** is untested. No ablation is reported, and the priors derive from an unvalidated vignette survey.
- **The headline superiority** holds only under distribution shift. Internally, BRIDGE is weakest.
- **The clinically motivating use case, prediction at treatment initiation,** is where discrimination is poorest (0.62–0.63).

A revision cannot repair the last two points without new data. The requested ablation could also remove the paper's remaining novelty.

Suggested transfers are *npj Cardiovascular Health* (best sub-domain fit) or *Communications Medicine*. The decision letter should state that transfer does not waive the ablation, calibration, and terminology corrections.

## Strongest counterargument (steelman for major revision)

R1's report partly overreaches:

- Demanding a prospective implementation trial is out of scope for a development and external-validation study.
- Calling the data "EHR" mischaracterizes a prescription database.
- Faulting the counterfactuals as non-causal ignores the authors' explicit disclaimer.
- Much of the text is generic, and R1 did not review the code.

Discounting R1 leaves R2, whose concerns are all addressable in revision: ablation, calibration, terminology, and a reframing toward dynamic early warning. Temporally and geographically disjoint external validation with GBTM refit exceeds field norms, as your own note acknowledged.

My rebuttal is that R2 independently concluded insufficient priority after seeing the fixable list. Priority, not fixability, is the bar.

## What you should also check

**Panel weakness.** Both named reviewers are residents or registrars, and R1's career stage is undisclosed. None of your suggested senior prediction-methodology or pharmacoepidemiology experts (Van Calster, Martin, Nagin, Pearson) appears on the panel. A rejection on priority is defensible anyway, but if the authors appeal, the panel's methodological depth is the vulnerability. Anchor the decision letter on the internal-inferiority, early-window, and untested-prior points, which rest on the authors' own numbers, rather than on R1's arguments.

**Self-overlap disclosure.** Verify in the manuscript whether Orman et al. is cited and whether its overlap is disclosed. Five of its authors appear on this submission. If it is cited and discussed, this is a novelty issue. If it is not, it becomes an integrity note for the letter.

**Mixed signals in R2's report.** R2's author-facing tone reads as "revise." The decision letter must explicitly cite R2's confidential priority judgment in general terms, or the authors will perceive the rejection as contradicting the reports.

037516
## Check of Elena's comments

Elena asked for three things across her comments. Your current summary meets none of them fully.

**Reviewer expertise (4 September, sent twice).** You replied on 14 September that you had "added it back", but the 3 September summary still gives no expertise per reviewer. The rewrite fixes this.

**A paediatric cardiologist (22 May).** None of your listed candidates is one. Ouyang, Tison and Elias are adult cardiologists. R4 is the closest match on the panel but is not a paediatric cardiologist either. The Rima Arnaout of UCSF is a UCSF cardiologist whose team trained machine-learning models to mimic how clinicians diagnose complex CHD on fetal ultrasound. The form does not confirm she is the same person, so state this as a presumption. Say plainly that the request was only partly met rather than leaving it unaddressed.

**Her 14 September reasoning.** One claim is inaccurate as worded: "the improvement in diagnostic performance is minimal." The overall AI-assisted gain is +8.0 points (86.8→94.8%), which is not minimal. The minimal part is the increment from visual guidance (+1.4 points). Her conclusion still holds, because visual guidance is the paper's claimed novelty.

Her "2 reviewers clearly raise the same concerns" is also slightly generous. R3 makes the added-value argument explicitly. R1 makes it only partly, through the Phase C vs B point. R4 rejects on different grounds: the clinical value of the task itself.

Your 3 September rationale dismissed R4 as unsupported by the reviewers who "examined the architecture". Drop that framing. R4's objection is about the study design and cohort selection, and R1's points 1 and 5 corroborate it.

## Rewritten summary

EWA>EBF

Hi Elena,

Thank you for the second look. Below are the reviewers' expertise, a summary of each report, and my revised recommendation.

**Decision: Reject, with transfer offered to Communications Medicine.**

**Reviewer 1 (Lovedeep Dhingra, postdoctoral researcher, Yale; spatiotemporal video transformers and echocardiographic AI): Major Revision, constructive.** The reviewer argues the task is easy relative to practice. It covers four classes with close to 50% disease prevalence and excludes concomitant CHD. They ask for performance on unselected paediatric echoes and quantification of the concomitant-CHD exclusions. They ask for results on the cases dropped for lack of unanimous expert consensus, since these are the cases where support is most needed. They note the lower-tier-hospital claim is not supported, because readers were stratified by experience, not tier. They question whether the Phase C gain over Phase B is significant rather than automation bias. They ask that the perception analyses be labelled exploratory.

**Reviewer 3 (Abdelouahab Bellou, laboratory director, China; clinical cardiology and ECG-AI; ran the code successfully): Major Revision.** This is the most detailed report. It finds the study rigorous but its narrative mismatched to its data. Probability assistance drives the reader gain (+8.0 points), and visual guidance adds only +1.4 points. Visual guidance's measurable effect is lower under-reliance (13.4% to 7.1%), so the reviewer asks for reframing as a trust-calibration tool.

The reviewer also asks for the following:
- architecture and pretraining ablations against a plain ResNet-50;
- justification of the lenient IoU 0.25 localisation threshold;
- a supervised comparator in place of Grad-CAM;
- per-site sample sizes, since the Sanya external AUROC is 0.863 with CI 0.644–1.000;
- controls for recall across the repeated reading phases;
- external reader validation;
- a corrected "appropriate reliance" definition;
- reading time, multiplicity correction, and calibration.

**Reviewer 4 (presumably Rima Arnaout, UCSF; cardiologist and cardiac imaging AI investigator, including deep learning for fetal CHD detection; closest to the paediatric cardiology expertise you requested): Reject.** Most of these comments were addressed to the editor, not the authors. The reviewer argues that expert echo already diagnoses CHD with high accuracy. VSD, ASD and PDA are anatomically distinct and rarely confused. Colour Doppler is typically applied once a sonographer has recognised a defect, so the model may detect that recognition rather than the disease.

**Rationale.** I agree with your assessment. The central problem is not methodological repair but the contribution that remains after repair. Once reframed as the reviewers request, the paper's distinctive claim is a modest reduction in under-reliance. That finding was measured on internal cases only, and the reader study was not shown to be powered for it. The diagnostic gain comes from probability outputs, which is the generic AI-assist result.

The scope limits cannot be fixed by revision. The study covers isolated VSD, ASD and PDA only, excludes non-consensus cases, and included 2,081 of 4,968 screened subjects. Extending it requires new data and retraining. R4's concern about spectrum and selection bias is consistent with R1's points on the cohort, so I no longer consider it an outlier view.

One further issue was not raised by any reviewer. The B→C effect (NRI about 0.015, roughly 3–4 reclassified cases out of 240) reportedly reaches p<0.001. That suggests reads were pooled across readers rather than analysed with a multi-reader multi-case method that treats readers and cases as random. If so, the visual-guidance effect may not survive a correct analysis.

The study's strengths remain: eight centres across hospital tiers, external AUROCs of 0.950–0.984, and a three-phase crossover reader study with reliance decomposition. These suit Communications Medicine well. If you agree, I will consult them before we issue the decision. In the transfer letter I will paraphrase R4's editor-only points so the authors can respond to them. I will also ask for multi-reader multi-case statistics, a between-lesion confusion matrix, and performance on the excluded non-consensus and multi-defect cases.

Best,
Eric

**Counterpoint to weigh before sending.** Two of three reviewers, including the only one who ran the code, recommended revision, and none called the scope limitation fatal. The authors could fairly argue that rejection overrides the referee majority on significance alone. The summary answers this by stating that scope cannot be fixed by revision and by flagging the statistical issue. If Elena is less certain than her note suggests, the summary should not look like it simply adopts her view. That is why it gives its own reasons, including the corroboration of R4 and the reader-study statistics.

The screenshot matches the comment I used. On a closer reading, two points need adjusting.

**Who the "2 reviewers" are.** The parenthetical "(R4 is extremely negative)" suggests Elena means R3 and R4, not R1 and R3 as I assumed. Either way, "the same concerns" is loose. R3 questions the added value of visual guidance over probability outputs, while R4 questions the value of the task itself. The two reach a similar conclusion for different reasons, and that is actually a stronger basis for the decision.

**"Improvement in diagnostic performance is minimal."** This conflates the two phases. AI assistance overall gives +8.0 points. Only the visual-guidance increment is minimal, at +1.4 points. Her decision survives the correction because visual guidance is the paper's claimed novelty. Your reply should state the distinction so the transfer letter doesn't tell the authors their AI-assisted gain is minimal. They would rebut that easily.

Her remaining points are accurate: the gain comes from probability outputs, the selected cohort limits generalisability, and after reframing the paper falls below the bar for Nature Communications. Her proposed route, Communications Medicine, is sound.

Since she has already decided, your reply should be short. It should agree, add the expertise she asked for twice, and add the two points she didn't raise. The full rewritten summary can follow separately or be dropped.

**Reply draft**

EWA>EBF

Hi Elena,

Thank you. I agree with Reject and transfer, and I will consult Communications Medicine.

The reviewers' expertise, as you requested:
- R1 (Dhingra, postdoctoral researcher, Yale) works on echocardiographic video AI.
- R3 (Bellou, laboratory director, China) works on clinical cardiology and ECG-AI, and ran the authors' code.
- R4 (Arnaout, presumably UCSF) is a cardiologist whose work includes deep learning for CHD detection on fetal ultrasound. She is the closest the panel came to the paediatric cardiology expertise you asked for, though not a paediatric cardiologist.

In the decision letter I will be precise on one point. Overall AI assistance improved reader accuracy by 8.0 points (86.8% to 94.8%). Visual guidance, the paper's claimed novelty, added only 1.4 points. I want the authors to read the limitation as being in the novelty, not in the assistance overall.

I will also paraphrase R4's editor-only remarks so the authors can address them at the transfer journal. Finally, the reported p<0.001 for a Phase B-to-C improvement of roughly 3–4 cases out of 240 suggests reads were pooled rather than analysed with a multi-reader multi-case method. I will ask for that analysis.

Best,
Eric

**Counterpoint.** Adding points Elena didn't raise could read as reopening the decision. The wording above treats them as instructions for the letter, not as reasons to reconsider. If you want the reply to be purely procedural, delete the paragraph on the multi-reader analysis and put it only in the transfer letter.


# Editorial Report — Manuscript 075630

**"Knowledge recognition as a metacognitive framework for reliable medical large language models"**

## 1. Overall Assessment

The manuscript proposes knowledge recognition (KR): an LLM partitions question content into "known" and "unknown," then judges answerability, answers, abstains, or searches using only the known partition. Claude-4.5-Sonnet and GPT-5 are tested zero-shot on MedXpertQA, an NEJM-derived set, MMLU-Pro (Health), and Glianorex.

This is one prompt template, tested once, on two closed models. The headline metric, self-assessment accuracy (SAA), falls below a trivial constant predictor, and the reported effects are smaller than prompt-induced noise in the authors' own tables.

## 2. Strengths

The extended Answerable–Unanswerable Confusion Matrix decomposes reliability into AR, MUAC, MAAC and AAAC — more informative than accuracy alone.

Splitting no-abstention and abstention-allowed settings exposes a real trade-off: KR raises MUAC (Claude 10.8% to 24.1%; GPT-5 3.2% to 33.7%) while lowering MAAC in seven of eight comparisons, a pattern many prompting papers conceal.

Negative results are reported openly: GPT-5 loses accuracy under KR. Data and code are public.

## 3. Weaknesses

SAA counts "unanswerable and incorrect" as aligned, so it is prevalence-dependent and rewards KR-induced accuracy loss. A constant predictor matching each benchmark's majority outcome scores 71.6% (Claude) and 64.8% (GPT-5), above the reported 51.0% and 58.1%.

There are no confidence intervals or repeated runs. Claude's mean KR abstention rate is 9.25% from Table 3, not the stated 18.5%. TN and FN share one definition (340–342), and the overconfidence formulas are mislabelled (365–366). Abstention-allowed accuracy exceeds its arithmetic ceiling in five of eight cells, implying about 6 points of unquantified variance — comparable to every claimed effect.

Information seeking lacks a RAG or chain-of-thought control; GPT-5 gains only 0.6 points over no-KR. Open-web DuckDuckGo retrieval on public benchmarks risks unaudited leakage.

Glianorex sits at ceiling (482/482) and tests lexical novelty, not knowledge boundaries; KR increased GPT-5 plausibility errors from 1 to 6.

## 4. Editorial Decision

**Reject.** The central metric does not beat a constant baseline, effects sit within unquantified variance, and key controls are absent. A redesign with discrimination metrics, repeated runs, and RAG/CoT controls could suit *npj Digital Medicine* as a new submission.

## 5. Suggested Reviewer Expertise

Reviewers should cover abstention and knowledge-boundary detection in LLMs, including answerable–unanswerable evaluation. A second should cover uncertainty quantification and selective prediction, including semantic entropy, AURC and calibration. A third should cover retrieval-augmented generation for medical QA with benchmark-leakage control. A fourth should cover metacognitive medical benchmarks and fictional-entity probes. A fifth should be a clinician in internal or emergency medicine with expertise in diagnostic reasoning under uncertainty.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Medical LLM reliability research has shifted from accuracy to self-knowledge. Griot et al. (MetaMedQA, *Nat Commun* 2025) showed that twelve models fail to recognise missing answers and their own knowledge limits. Farquhar et al. (*Nature* 2024) introduced semantic entropy for hallucination detection. Feng et al. (ACL 2024) identified knowledge gaps through multi-LLM collaboration. MediQ (Li et al., NeurIPS 2024) coupled abstention with follow-up information seeking in clinical interaction. MedRAG and i-MedRAG (Xiong et al., 2024–2025) established query-generating medical retrieval. AbstentionBench (Kirichenko et al., NeurIPS 2025) showed reasoning fine-tuning degrades abstention, which bears directly on GPT-5.

The manuscript cites Griot and Madhusudhan but omits MediQ, semantic entropy, AbstentionBench and i-MedRAG. KR restates i-MedRAG's decompose-then-retrieve strategy and MediQ's abstain-then-ask design. Its novelty lies in naming rather than mechanism.

## 7. Suggested Reviewers

Abstention and knowledge boundaries: Shangbin Feng (University of Washington; "Don't Hallucinate, Abstain", ACL 2024), Polina Kirichenko (Meta FAIR; AbstentionBench), Nishanth Madhusudhan (ServiceNow; AUCM, ref. 10).

Uncertainty quantification: Sebastian Farquhar (Google DeepMind; semantic entropy), Jiahui Geng (calibration survey, ref. 6), Mark Steyvers (UC Irvine; ref. 8; full professor, last resort).

Medical RAG: Qiao Jin (NLM, NIH; i-MedRAG), Guangzhi Xiong (University of Virginia; MedRAG/i-MedRAG), Minbyul Jeong (Self-BioRAG).

Metacognitive medical benchmarks: Maxime Griot (UCLouvain; MetaMedQA, Glianorex), Shuyue Stella Li (University of Washington; MediQ), Pang Wei Koh (University of Washington; MediQ).

Clinical reasoning: Jonathan Ilgen (University of Washington; MediQ clinical co-author), Adam Rodman (Beth Israel Deaconess; LLM diagnostic reasoning), Jonathan H. Chen (Stanford; LLM diagnostic reasoning trials).

Oxford-affiliated candidates (e.g., semantic-entropy co-authors at OATML) are excluded because of the co-corresponding author's University of Oxford affiliation. Avoid assigning more than one reviewer from the University of Washington MediQ group.

---

## Steelman (for the handling editor)

The strongest case for review is precedent. *Nature Communications* published MetaMedQA, a benchmark-only multiple-choice metacognition study. A paper that moves from diagnosing the deficit to intervening on it arguably clears the same bar, and the arithmetic and definitional errors are correctable. The rebuttal is that MetaMedQA contributed a new resource across twelve models. This submission contributes a prompt, evaluates two closed models once, and its principal metric cannot beat a constant predictor. Correcting typos does not repair that.

## Verification Notes (confidential)

Recomputed from Tables 2–3: Claude KR+search minus KR = 7.5 pp and GPT-5 = 2.7 pp (both match the text). GPT-5 no-KR mean accuracy is 64.8%, not 65.0%. Claude KR abstention rate is 9.25%; the stated 18.5% equals the four-benchmark sum divided by two. MUAC and AAAC means match. No preprint or prior publication overlap was found. SAA per-benchmark values are figure-only in the scanned PDF, so the stated 6.0% and 8.6% SAA gains could not be verified independently.

# Editorial Report — Manuscript 074726

**Title:** Epiflow: Human–Artificial Intelligence Collaboration for Observational Study Design and Analysis
**Section:** Nature Communications — Digital Health
**Date of assessment:** 17 September 2026

---

## 1. Overall Assessment

Epiflow, a Claude Sonnet 4.5 agentic framework, turns a hypothesis into a UKB protocol, STROBE checklist, and R script via hybrid retrieval for variable selection. Its central claim, Pearson r = 0.819 across 305 HRs from 55 published studies, is confounded, not merely imperfect: humans with the reference papers open finalise definitions at every stage with no intervention log or AI-only arm, all 55 studies fall inside the backbone's training window, and 69.4% parametric-only accuracy suggests recall over reasoning.

## 2. Strengths

Reproducing published HRs across 55 sampled UKB studies is the right evaluation target. The retriever ablation (dense vs. parametric vs. hybrid, three backbones, 222 pairs) is well structured, hybrid winning under every backbone (76.1–78.8% vs. 62.6%, verified). Failure cases and Claude-as-judge self-preference bias are reported transparently.

## 3. Weaknesses

The reproduction benchmark cannot separate Epiflow from human intervention and likely contamination (above). Pearson r on raw HRs, treating 305 clustered estimates as independent, is the wrong agreement metric; limits of agreement (−0.66 to 0.55) mean a true HR of 1.00 could reproduce as 0.45–1.55. The three human comparators appear to be co-authors. The retriever evaluation lacks a lexical baseline or significance tests. The STROBE analysis is circular (self-scored against its own prior feedback) and arithmetically wrong: rates rose *to* 85.5%/63.9%, not *by* that amount (true gains: 12.6/15.0 points), and Figures 6a/6b do not reconcile.

## 4. Editorial Decision

**Reject, transfer to *npj Digital Medicine*.** Reproduction accuracy cannot be attributed to Epiflow over human intervention and pretraining exposure, and the agreement statistics are wrong for correlated ratio data; this needs new experiments, not reanalysis. *Counterargument:* human-in-the-loop is the stated design — but without an AI-only arm, no one can tell whether Epiflow added anything beyond a researcher with the paper open.

## 5. Suggested Reviewer Expertise

Reviewers should cover retrieval-augmented and agentic LLM systems for structured biomedical data, including dense retrieval and LLM re-ranking over data dictionaries. A second reviewer should have expertise in benchmark design for LLM agents on real-world databases, including contamination control and LLM-as-judge bias. A third should specialise in agreement statistics for ratio measures and clustered reproducibility data. Clinically, one reviewer should be a UK Biobank cohort epidemiologist familiar with outcome ascertainment and field-level operational definitions. Another should have expertise in the reproducibility of observational real-world evidence and reporting guidelines such as STROBE and RECORD.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The manuscript states that no prior study has examined AI agents in epidemiological research. Its own reference 7 contradicts this. Bann et al. (*Int J Epidemiol* 2026; 55: dyaf210) demonstrated agentic systems designing and executing epidemiological analyses, including fully AI-generated papers, and a published response by Janse and Meulenbeld (*Int J Epidemiol* 2026; dyag065) argued against that degree of automation. The closest competitor, uncited, is Jeong et al. (PMLR 297, Machine Learning for Health Symposium 2026), an agentic system that searches the UKB data dictionary to build computable phenotypes and executes analyses from hypothesis to report. RWE-bench (Li et al., arXiv 2603.22767, 2026; unreviewed) evaluates agents on 162 MIMIC-IV observational studies with protocols supplied, reporting a best task success of only 39.9%. That result suggests Epiflow's high agreement reflects human scaffolding. Corpas and Iacoangeli (*PLOS Comput Biol* 2026) benchmarked frontier LLMs, including Claude Sonnet 4.5, on UKB-specific knowledge, which bears directly on the memorisation question. FastOMOP (arXiv 2604.24572, 2026; unreviewed) addresses governance of agentic evidence generation on OMOP data.

The most important uncited benchmark is non-AI. The REPEAT initiative (Wang et al., *Nat Commun* 2022; 13: 5126) reproduced 150 real-world evidence studies by expert teams and reported Pearson r = 0.85, with a median HR ratio of 1.0 (IQR 0.9–1.1). Epiflow's r = 0.819 therefore falls below expert human reproduction, and REPEAT's ratio metric is the appropriate comparator. Cui et al. (*Nat Comput Sci* 2025) showed that LLM replications of 156 psychology experiments inflate effect sizes, a failure mode the authors should test. Epiflow's distinct contribution is field-level retrieval over UKB metadata within a gated workflow. Its end-to-end reproduction claim is evaluated more leniently than the competing work.

## 7. Suggested Reviewers

For agentic systems and retrieval over biobank data dictionaries, Chang-Uk Jeong and Dokyoon Kim (University of Pennsylvania) authored the directly comparable UKB agent in PMLR 297 (2026); Qiao Jin (NCBI/NLM, NIH) has published on biomedical LLM agents (GeneAgent, AgentMD); and Kexin Huang (Stanford University) led the Biomni general biomedical agent. For agent benchmarking on real-world databases, Dubai Li is first author of RWE-bench (affiliation to be confirmed before invitation). For LLM-as-judge self-preference bias, Arjun Panickssery authored the self-recognition study cited as reference 28. For UKB epidemiology and outcome definitions, Thomas J. Littlejohns (Nuffield Department of Population Health, University of Oxford) has published extensively on UKB health-outcome ascertainment. For automated epidemiology, Liam Wright or Ed Lowther (University College London) co-authored Bann et al. (2026). For reproducibility of observational evidence, Shirley V. Wang (Harvard Medical School/Brigham and Women's Hospital) led REPEAT. Institutional conflicts with Ajou University were not identified; co-authorship links of Dokyoon Kim with Korean institutions should be checked before invitation. Full professors were deprioritised.

---

## CONFIDENTIAL — Editorial Integrity Alert (to handling editor only)

The following items were verified independently and do not appear in the author-facing report above. None rises to suspected misconduct, but together they indicate inadequate manuscript preparation.

Reference numbering is systematically misaligned from approximately reference 23 onward. BM25 is cited as reference 26 (BEIR) instead of 25. Self-recognition is cited as 29 (Wataoka) instead of 28 (Panickssery). "Retrieval quality" and "retrieval precision" are cited to 28, a paper on LLM self-preference. SFR-Embedding-Mistral is cited as 34 (FAISS), FAISS as 35 (STROBE E&E), the STROBE classification scheme as 23 (an asthma operational-definitions paper), the reproducibility inhibitor claim as 25 (a BM25 monograph), and multi-agent debate as 33 (a Salesforce blog). Reference 1 misattributes first authorship of *Basic Epidemiology* (Bonita et al.), reference 22 garbles Cicchetti's name, and reference 4 is numbered "4.00".

Reference 20 (Ma et al., *BMC Med* 2022) reports time in outdoor light and incident dementia, not mortality. The manuscript describes this case study as "mortality" in both the Results and the Figure 3 legend. The reference study also used a 16-covariate model; the authors should confirm that an age–sex model was actually reported.

The novelty claim (lines 66–68) is contradicted by the authors' own reference 7.

The code repository (github.com/timothy0922/Epiflow) returned HTTP 404 on 17 September 2026. It is either private or nonexistent.

The three human comparators appear to be co-authors, and one also reviewed the software. This undermines the independence of the human-versus-Epiflow comparison.

The submission is a CamScanner scan of printed pages. Supplementary Tables 2–9, Supplementary Notes 1–2 (all prompts), and the PRISMA flow diagram were not provided. Core evidence for the retriever benchmark, the HITL feedback, and the STROBE ratings cannot be inspected.

# Editorial Report — Manuscript 073903

**MUCRETFound: Uncertainty-aware multimodal retinal representations for cross-domain validation and longitudinal risk stratification**

## 1. Overall Assessment

MUCRETFound is a DINOv2 ViT-S model combining LoRA student–teacher reconstruction, BioClinicalBERT-templated contrastive alignment, and MC-Dropout/mixture-of-experts uncertainty. Reported mean AUCs: 96.04% CFP, 95.30% OCT, 84.40% external, 71.69% UK Biobank future disease.

It assembles known components with a small margin over the best comparator, no confidence intervals. Two problems dominate: UK Biobank supplies ~368,000 of ~805,000 pretraining images and is reused as the prognostic test cohort; baselines appear broken rather than weak.

## 2. Strengths

Twelve fine-tuning datasets span ROP, glaucoma, myopic maculopathy, DR grading and OCT, with per-dataset DeLong tests and full confusion matrices, which expose the baseline failures below, to the authors' credit.

Pretraining and evaluation sets are separated by construction, and threshold-dependent metrics are reported honestly, including cases where FLAIR beat MUCRETFound on F1.

Reporting is internally consistent: the UK Biobank split arithmetic and the 12-task mean accuracy reconcile against the ablation endpoint.

## 3. Weaknesses

The prognostic result is circular. UK Biobank CFP/OCT (368,157 images) appear in Table S1 with categorical annotations but not in Table 1, so they entered pretraining — the same cohort reused as the prognostic test set. The outcome is undefined: no disease list, follow-up horizon, or prevalent-case exclusion. Back-calculating Table 6 gives sensitivity near 8.8%.

Baseline integrity is doubtful: RETFound scores 58.71% AUC on AIROGS predicting every image negative, and below-chance on REFUGE2/PARAGUAY — a pipeline error, not weak transfer. No seeds, confidence intervals, or multiple-comparison correction are reported.

The uncertainty objective is degenerate: its losses directly minimise predicted uncertainty, rewarding variance collapse rather than calibration. No ECE, Brier score, or OOD AUROC is reported; evidence is eight selected images.

Scope exceeds evidence: FFA is pretrained but never evaluated; "zero-shot" mislabels source-fine-tuned transfer; no demographic subgroup analysis or ethics statement for the private paediatric data.

## 4. Editorial Decision

**Reject.** Test-cohort reuse invalidates the longitudinal claim, below-chance baselines invalidate the comparative claim, and a confidence-rewarding loss undermines the titular contribution. After re-analysis, npj Digital Medicine or Communications Engineering would fit. The counterargument — that scope and candor resemble published work — fails: fixes would change every headline number.

## 5. Suggested Reviewer Expertise

Self-supervised and parameter-efficient pretraining of vision transformers for retinal CFP and OCT, including MAE, DINOv2 and LoRA adaptation, with experience fine-tuning RETFound baselines. Retinal vision–language contrastive pretraining with knowledge-templated prompts. Uncertainty quantification and probabilistic embeddings, covering MC Dropout, calibration, selective prediction and distribution-shift detection in medical imaging. Clinical ROP screening and AI validation in paediatric ophthalmology. Oculomics and incident-disease prediction in UK Biobank, including survival-model evaluation.

## 6. State-of-the-Art Literature Review (Past 3 Years)

RETFound (Zhou et al., Nature 2023) established MAE pretraining on 1.6 million retinal images. Efficiency variants followed: RETFound-DE (Nat. Biomed. Eng. 2025) and RETFound-Green (Nat. Commun. 2025). Vision–language models FLAIR (Med. Image Anal. 2025) and RetiZero (Nat. Commun. 2025) introduced knowledge-encoded text supervision. VisionFM (NEJM AI 2024), EyeFM (Nat. Med. 2025) and EyeCLIP (npj Digit. Med. 2025) extended coverage to multiple modalities and clinical workflows. EyeCLIP combines reconstruction, cross-modal image contrast and image–text contrast across 11 modalities. MIRAGE (npj Digit. Med. 2025) covered OCT and SLO with segmentation benchmarks. FMUE (Cell Rep. Med. 2025) paired a retinal foundation model with evidential uncertainty and OOD thresholds.

The manuscript does not cite UrFound (MICCAI 2024), which already unifies CFP and OCT with knowledge-guided text supervision. It also omits EyeCLIP, MIRAGE and EyeFound. Against FMUE, it offers a more elaborate uncertainty architecture with weaker validation. Comparisons showing DINOv2 matching or exceeding RETFound (arXiv 2025) should have been engaged, because the manuscript's own DSM results reproduce that finding. For prognosis, the relevant comparators are dedicated incident-glaucoma models (Li et al., Med 2022) and recent UK Biobank multimodal incident-POAG work, not diagnostic foundation models.

## 7. Suggested Reviewers' Names

Early-career researchers are listed first. Comparator-model authors are flagged; their input on baseline configuration is valuable, but they have a competitive interest. Excluded for conflict: Huazhu Fu, Bin Sheng and Baiying Lei (co-authors), and Meng Wang (RetiZero first author, co-authored with Fu).

**Retinal foundation-model pretraining:** José Morano (Medical University of Vienna; MIRAGE, npj Digit. Med. 2025). Justin Engelmann (University of Edinburgh; RETFound-Green, Nat. Commun. 2025; comparator flag). Yukun Zhou (UCL/Moorfields; RETFound, Nature 2023; comparator flag).

**Retinal vision–language alignment:** Danli Shi (Hong Kong Polytechnic University; EyeCLIP, npj Digit. Med. 2025; verify no co-authorship with Sheng). Julio Silva-Rodríguez (ÉTS Montréal; FLAIR, Med. Image Anal. 2025; comparator flag). Kai Yu (UrFound, MICCAI 2024).

**Uncertainty and distribution shift:** Lisa M. Koch (University of Bern; distribution-shift detection on fundus images, npj Digit. Med. 2024). Murat Seçkin Ayhan (University of Tübingen; expert-validated uncertainty for DR detection, Med. Image Anal. 2020). Uddeshya Upadhyay (ProbVLM, ICCV 2023).

**Clinical ROP:** Aaron S. Coyner (Casey Eye Institute, OHSU; multinational external validation of autonomous ROP screening, JAMA Ophthalmol. 2024). Benjamin K. Young (Casey Eye Institute, OHSU; AI-assisted smartphone ROP telescreening, JAMA Ophthalmol. 2023). Andrew S. H. Tsai (Singapore National Eye Centre; AI in ROP care, 2024).

**Oculomics and UK Biobank prognosis:** Zhuoting Zhu (Centre for Eye Research Australia; retinal age gap in UK Biobank). Siegfried K. Wagner (UCL/Moorfields; AlzEye and RETFound; comparator flag). Anran Ran (Chinese University of Hong Kong; deep-learning glaucoma detection on OCT, Lancet Digit. Health 2019).

---

## Confidential Editorial Integrity Alert (handling editor only)

First, UK Biobank test-cohort reuse in pretraining (Table S1 entries 45) must be clarified before any further consideration. Second, below-chance RETFound AUCs suggest a pipeline error affecting published comparator claims. Third, RetiZero is a comparator from co-author Fu's group, and this is not disclosed. Fourth, the manuscript contains no ethics or IRB statement for the private Shenzhen Eye Hospital paediatric data or the UK Biobank analysis. Fifth, reference 1 (WHO patient-safety action plan) does not support the ocular-burden claim. References 5/71, 8/82, 10/58, 13/51 and 53/84 are duplicates, and two Table S1 entries share the number 45.
