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

# Editorial Report — Manuscript 075121

**Title:** Automated Non-invasive Estimation of Cardiac Hemodynamics with Deep Learning
**Handling standard:** Nature Communications (Digital Health), calibrated to The Lancet Digital Health

---

## 1. Overall Assessment

EchoHemodynamic classifies five catheterisation-derived pressures as elevated from echo video, trained on 2,929 UCSF pairs and applied unmodified to 740 MHI pairs. Training against invasive labels rather than echo surrogates is a genuine advance. But the headline claim — superiority over conventional echo for LV filling pressure — rests on 93 internal patients with an undefined endpoint and overlapping CIs (p=0.038), and is unsupported externally, where the model is statistically indistinguishable from conventional echo (p=0.929, p=0.216). No non-imaging baseline is reported.

## 2. Strengths

Training against Mac-Lab catheterisation values avoids the circularity of prior work (Akerman 2023, Pandey 2021) trained on echo-derived surrogates. The multitask design matches clinical practice, and excluding spectral Doppler supports point-of-care use. Frozen-weight external validation across country and vendor is more rigorous than most echo-AI papers attempt, and degradation is reported honestly. Most useful: model AUC held (0.687, 0.667) in the 23–44% of MHI studies where echo RVSP/RAP was unmeasurable.

## 3. Weaknesses

Test-set prevalence is extreme (77% LVEDP>12), yet no calibration, decision-curve, or NPV analysis supports the proposed rule-out use. The E/e' comparison (n=93) uses a categorical NRI with undisclosed threshold provenance, risking optimistic bias. No clinical/tabular baseline is tested against the video model. Reported cohort sizes and Figure 2A denominators are internally inconsistent. Code is licence-only, and the view-classifier preprocessing step (ref. 30) is an unpublished in-press paper from the same group. No subgroup analysis by sex, race, or vendor is given, despite vendor being invoked to explain degradation.

## 4. Editorial Decision

**Reject**, encourage transfer. The distinguishing claim is unsupported externally and fragile internally; without a baseline, calibration, and subgroup reporting the work does not meet the bar. Transfer to **npj Digital Medicine** or **Communications Medicine**, reframed around coverage where conventional echo fails.

**Counterargument.** Cross-national frozen-weight validation on invasive labels is uncommon and honestly reported; every deficiency is fixable from existing data, so a resubmission dropping the superiority claim would merit reconsideration.

## 5. Suggested Reviewer Expertise

Five areas are needed. First, video-based deep learning for echocardiography, specifically transformer and 3D-CNN architectures with clip-level to study-level aggregation and multitask heads. Second, non-invasive estimation of intracardiac pressures by machine learning, including ECG- and CMR-based haemodynamic inference, to judge the novelty claim against modality-adjacent prior art. Third, clinical prediction model methodology, with emphasis on calibration, decision-curve analysis, the validity of categorical NRI, threshold selection and clustered resampling. Fourth, invasive haemodynamics and diastolic function in heart failure, able to assess the >12 mmHg thresholds, LVEDP–PCWP discordance and the one-day pairing window. Fifth, pulmonary hypertension imaging and echocardiographic right-heart assessment, to evaluate the RVSP/MPAP claims and the unobtainable-measurement analysis.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant landscape has moved quickly and the manuscript engages only part of it. On the imaging side, Akerman et al. (JACC Advances 2023) trained a 3D CNN on a single A4C clip for HFpEF detection; that model is now FDA-cleared as EchoGo Heart Failure and has been validated against invasive haemodynamics in a small right-heart-catheterisation cohort (PubMed 41955408, 2026), which is the closest direct competitor to the present left-sided claim and is not cited. Holste et al. (JAMA 2025) demonstrated complete multitask echocardiographic interpretation, establishing the multitask design as expected rather than novel. On the haemodynamics side, Schlesinger et al. (JACC Advances 2022) inferred elevated mean PCWP from the 12-lead ECG in 6,739 catheterised MGH encounters with an explicit unreliability score, and subsequent self-supervised metric-learning work extended this to 5.4 million unlabelled ECGs; Lehmann et al. (Lancet Digital Health 2024) estimated filling pressures from CMR. For the right heart, an npj Digital Medicine 2025 multimodal fusion model for pulmonary hypertension used 2,451 catheterised patients with a prospective cohort, an external dataset, module-level ablation and subgroup evaluation, and Us2.ai-based automated echo workflows have been benchmarked against core-laboratory readers in pulmonary arterial hypertension (CHEST 2025).

Against this landscape, the manuscript's claim to be "the first echocardiographic AI model capable of estimating CC-derived parameters from standard echocardiographic videos" is too strong and should be narrowed to the joint five-parameter panel. Its genuine advances are the invasive label set and the simultaneous panel; its replication is the multitask video architecture and the single-parameter right-sided prediction. The comparators listed above set the methodological floor the authors must meet: uncertainty quantification, ablation, subgroup analysis and prospective or multi-centre evidence are now standard in this sub-domain, and none is present here.

## 7. Suggested Reviewers

Technical — video-based echocardiographic deep learning: Evangelos Oikonomou (Yale, assistant professor; senior author on multitask echocardiographic interpretation work), Márton Tokodi (Semmelweis University, assistant professor; echocardiographic machine learning and diastolic phenotyping), Milos Vukadinovic (Cedars-Sinai; echocardiographic foundation and video models).

Technical — machine learning for intracardiac pressure estimation: Daphne Schlesinger (postdoctoral researcher; first author of RHCNet for ECG-based mPCWP inference), Aniruddh Raghu (haemodynamic inference from physiological signals), Krit Dwivedi (University of Sheffield, clinical lecturer; AI estimation of pulmonary haemodynamics from imaging).

Technical — prediction model methodology and calibration: Ben Van Calster (KU Leuven, associate professor; calibration and validation of clinical prediction models), Benjamin Wessler (Tufts, associate professor; external validation of cardiovascular prediction models and echocardiographic AI), Laure Wynants (Maastricht, assistant professor; model validation and reporting standards).

Clinical — invasive haemodynamics and diastolic function: Yogesh N. V. Reddy (Mayo Clinic; invasive HFpEF haemodynamics and exercise catheterisation), Masaru Obokata (Gunma University; invasive filling-pressure phenotyping), Frederik Fortuni (echocardiographic assessment of filling pressures).

Clinical — pulmonary hypertension and right-heart imaging: Jan Stassen (echocardiographic right-heart assessment and outcomes), Jennifer Arthur Ataam or an equivalent early-career pulmonary vascular specialist with right-heart catheterisation expertise, Samuel Bernard (pulmonary hypertension imaging and haemodynamics).

Reviewers from UCSF, the Montreal Heart Institute, the University of British Columbia and Ultromics should be excluded for institutional or commercial conflict.

# Editorial Report — Manuscript 075879

**Title:** Deep learning estimation of peak oxygen uptake from resting physiological parameters predicts cardiovascular events
**Handling assessment:** Nature Communications, Digital Health

---

## 1. Overall Assessment

AdaVO2Net, a sex-conditioned FiLM MLP, estimates peak VO2 from resting CPET variables (external R² 0.81, MAE 1.39 ml kg⁻¹ min⁻¹; AUROC 0.87 for peak VO2 <14 ml kg⁻¹ min⁻¹) and links predicted reserve to 180-day readmission. Two problems are decisive. Internal MAE (1.06, 4.9% of the mean) sits inside CPET's own test–retest repeatability, exceeding the closest comparator, Lee et al. (*JAHA* 2026;15:e045734, 13,535 tests, R² 0.55–0.69), uncited. The deployment premise is self-refuting: inputs require the same metabolic cart the model claims to replace.

## 2. Strengths

Patient-level fold assignment prevents leakage, and the external cohort (differing BMI, event rate, case mix) is a genuine distribution shift. Linking predicted reserve to readmission and therapy escalation is ambitious and rarely attempted. The audit of 35 high-discrepancy records, separating report-quality failures from genuine resting–exercise dissociation, is a real contribution. The perturbation analysis is physiologically coherent, dominated by stroke volume and O2 pulse.

## 3. Weaknesses

The feature set is never enumerated; Figure 3d contains undefined variables ("HRR," "Resting METs") that, if exercise-derived, invalidate every headline number, and inputs were parsed from PDFs containing the label column itself. The prognostic analysis (Figure 4 tertiles sum to 1,738) is entirely in-sample, ~85 events, no external replication, narrow IPTW adjustment, and an accrual window postdating the stated censoring date. Task 2 merely dichotomises Task 1. No calibration, no code availability, and an ethics approval number postdating enrolment by five years.

## 4. Editorial Decision

**Reject**, not sent for review: reviewers cannot adjudicate without the withheld feature dictionary, and the prognostic claim is unsupported by design. **Steelman:** a single-protocol resting cohort could outperform Lee et al.'s heterogeneous pooled data, and external R² 0.81 argues against simple leakage — but a shared extraction pipeline would transport across sites regardless. **Confidential note:** request the input dictionary, extraction code, and per-fold predictions before any resubmission decision.

## 5. Suggested Reviewer Expertise

Machine learning for cardiopulmonary exercise test data, specifically regression of peak VO2 from resting and submaximal gas-exchange variables. Tabular deep learning and conditional normalisation methods, with the ability to judge whether FiLM conditioning on a binary covariate confers anything beyond covariate inclusion, and to audit baseline tuning. Prediction-model methodology under TRIPOD+AI, covering calibration, leakage detection, clustered observations, and events-per-variable in low-event survival modelling. Automated extraction of structured variables from clinical report PDFs, for leakage provenance. Clinically, exercise physiology and CPET interpretation in cardiology and pre-operative assessment, and heart failure prognostication using peak VO2 thresholds and readmission endpoints.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant literature has converged on a consistent accuracy ceiling. Lee et al. (*JAHA* 2026;15:e045734) is the definitive comparator: 13,535 CPETs, Bayesian Ridge and LightGBM, demographic plus resting variables giving R² 0.546–0.690, rising to 0.732–0.796 only when submaximal variables are added. Khurshid, Diamant and colleagues (*Eur J Prev Cardiol* 2024;31:252) derived peak VO2 from resting 12-lead ECG in 1,891 MGH patients with external validation at BWH, reaching r = 0.552 and MAE 6.49 ml kg⁻¹ min⁻¹. Huang et al. (*npj Digit Med* 2026;9:304), cited here as reference 21, used multimodal multi-instance learning over transthoracic echocardiography and EHR to reach R² 0.603 and AUROC 0.849 for high-risk identification, itself an advance on a prior R² of 0.529. Rosoł et al. (*PLoS ONE* 2024;19:e0291706) obtained R² 0.47 from warm-up and submaximal treadmill signals. Real-time deep learning on CPET time series (Yamashita et al., *Eur J Prev Cardiol* 2024;31:448) improves on this only by consuming the exercise phase itself.

Against that landscape, an external R² of 0.81 and an internal R² of 0.90 from resting data alone would be a step change of roughly 0.25 R² over the best like-for-like result, achieved with a smaller cohort and a simpler architecture. Extraordinary claims of this kind require the extraction pipeline and feature dictionary to be open, and require engagement with Lee et al., which the manuscript does not cite despite it being the closest published work on precisely this task. The genuine white space the authors could occupy is different and more defensible: prospective demonstration in patients who reach the laboratory but cannot complete a ramp protocol — the population the model is nominally for, and the population both cohorts exclude by construction. No published study has done this, and it would be a real contribution.

## 7. Suggested Reviewers

*All suggestions require conflict screening; none share an institution with Shenzhen, HKU or Fuwai to my knowledge, but this should be verified.*

**CPET machine learning and peak VO2 regression:** Yonghun Lee (UNIST / UCLA MII Group) and Jeffrey J. Hsu (Assistant Professor, UCLA Division of Cardiology), first and senior authors of the JAHA 2026 study that is the direct comparator; Marcel Młyńczak (Associate Professor, Warsaw University of Technology), PLoS ONE 2024 submaximal VO2peak machine learning; Przemysław Seweryn Kasiak (Medical University of Warsaw), eLife 2023 VO2max prediction from submaximal CPET.

**Deep learning from resting cardiac data for exercise capacity:** Shaan Khurshid (Assistant Professor, Massachusetts General Hospital) and Nathaniel Diamant (Broad Institute), co-leads of the Deep ECG-VO2 study; Timothy W. Churchill (Assistant Professor, MGH Cardiovascular Performance Program).

**Prediction-model methodology and TRIPOD+AI:** Paula Dhiman (Senior Researcher, University of Oxford), TRIPOD+AI co-author; Ben Van Calster (Associate Professor, KU Leuven), calibration of clinical prediction models; Maarten van Smeden (Associate Professor, UMC Utrecht), events-per-variable and overfitting in low-event settings.

**Clinical exercise physiology and heart failure prognostication:** Erik H. Van Iterson (Director of Cardiac Rehabilitation, Cleveland Clinic), CPET-based prognostication and the 14 ml kg⁻¹ min⁻¹ threshold; Jonathan Myers (Stanford / VA Palo Alto), non-exercise CRF estimation and prognosis — full-professor-equivalent seniority, to be used only if the earlier-career options decline.

---

## 8. Further Literature (past three years, comparable scope)

*Bibliographic details verified against PubMed, publisher records and institutional repositories. Citation status refers to the reference list of manuscript 075879.*

**1. Lee Y, Feng J, Rahrooh A, Bui AAT, Cooper CB, Hsu JJ. Peak oxygen uptake prediction from resting and submaximal variables of cardiopulmonary exercise testing.** *J Am Heart Assoc* 2026;15(6):e045734. DOI 10.1161/JAHA.125.045734. Peer-reviewed. **Not cited.** Fully independent (UCLA / UNIST). This is the single most important omission. It is the same task on the same input class — demographics plus resting CPET variables — at 13,535 tests, and it reports R² 0.546–0.690, rising to 0.732–0.796 only once submaximal variables are added. The authors must reconcile their R² of 0.90 against this, or explain why their cohort supports a 0.25 R² advantage at one eighth the sample size. Bayesian Ridge and LightGBM were the optimal models there, which also bears on the baseline-tuning question.

**2. Khurshid S, Churchill TW, Diamant N, et al. Deep learned representations of the resting 12-lead electrocardiogram to predict at peak exercise.** *Eur J Prev Cardiol* 2024;31(2):252–262. DOI 10.1093/eurjpc/zwad321. Peer-reviewed. **Not cited.** Independent (MGH / Broad Institute). Derivation in 1,891 CPET patients with true external validation at a second institution (n = 1,076), reaching r = 0.552 and MAE 6.49 ml kg⁻¹ min⁻¹. Critically for this manuscript, it also tested the downstream step the authors claim as novel: estimated peak VO2 <14 ml kg⁻¹ min⁻¹ predicted incident atrial fibrillation, myocardial infarction, heart failure and death. The claim that linking estimated peak VO2 to events is an unmet need is therefore not accurate as written.

**3. Huang Z, Pan W, Alishetti S, et al. Multimodal multi-instance learning for cardiopulmonary exercise testing performance prediction.** *npj Digit Med* 2026;9(1):304. DOI 10.1038/s41746-026-01697-w (as cited by the authors; verify at proof). Peer-reviewed. **Cited (ref 21).** Independent. Establishes the current field benchmark on the identical two-task formulation — R² 0.603 for peak VO2 and AUROC 0.849 for identifying high-risk patients — using echocardiography and EHR. The manuscript cites it but does not benchmark against it, despite having adopted its exact task structure.

**4. Watanabe T, Tohyama T, Ikeda M, et al. Development of deep-learning models for real-time anaerobic threshold and peak VO2 prediction during cardiopulmonary exercise testing.** *Eur J Prev Cardiol* 2024;31(4):448–457. DOI 10.1093/eurjpc/zwad375. Peer-reviewed. **Not cited.** Independent (Kyushu University). Deep learning on breath-by-breath CPET time series in 1,472 records achieved Corr 0.87 and MAE 2.25 ml kg⁻¹ min⁻¹ for peak VO2 — while consuming data up to the anaerobic threshold. A model given strictly less information than Watanabe's cannot plausibly achieve an MAE of 1.06. This is the sharpest single-number check available to reviewers.

**5. Nakayama A, Iwata T, Sakuma H, Kashino K, Tomoike H. Predicting heart rate at the anaerobic threshold using a machine learning model based on a large-scale population dataset.** *J Clin Med* 2025;14(1):21. DOI 10.3390/jcm14010021. Peer-reviewed. **Not cited.** Independent (Sakakibara Heart Institute / NTT). Gradient boosting on 78 non-exercise features drawn from 21,482 CPETs. Directly relevant to the baseline question: it demonstrates that a well-tuned GBM on non-exercise inputs at scale is the correct comparator, and that gradient boosting should not be finishing behind SVM as it does in Figure 2a–c.

**6. Rosoł M, Petelczyc M, Gąsior JS, Młyńczak M. Prediction of peak oxygen consumption using cardiorespiratory parameters from warmup and submaximal stage of treadmill cardiopulmonary exercise test.** *PLoS ONE* 2024;19(1):e0291706. DOI 10.1371/journal.pone.0291706. Peer-reviewed. **Not cited.** Independent (Warsaw University of Technology). Thirteen algorithms across eleven feature sets; best R² 0.47, RMSE 5.78 ml kg⁻¹ min⁻¹ using warm-up and submaximal cardiac and respiratory features. Establishes the low end of the plausible range and quantifies how much of the signal sits in the exercise phase rather than at rest.

**7. Wiecha S, Kasiak PS, Szwed P, et al. VO2max prediction based on submaximal cardiorespiratory relationships and body composition in male runners and cyclists: a population study.** *eLife* 2023;12:e86291. DOI 10.7554/eLife.86291. Peer-reviewed. **Not cited.** Independent (Medical University of Warsaw). Large athletic cohort with body-composition and submaximal CPET predictors. Useful as a spectrum contrast: this manuscript's cohort is cardiovascular-disease dominated with measured peak VO2 SD of only 5.42 ml kg⁻¹ min⁻¹, and reviewers should ask how a narrow outcome distribution coexists with R² 0.90.

**8. Chaliki K, Sharma A, Sharma A, Yee C, Chaliki H, Reddy S. Key resting echocardiographic parameters for the estimation of exercise parameters of peak VO2, heart rate recovery, and ventilatory efficiency.** *J Clin Med* 2025;14(9):3013. DOI 10.3390/jcm14093013. Peer-reviewed. **Not cited.** Independent (Mayo Clinic Arizona / University of Arizona). Regression of percent-predicted peak VO2 on 19 resting echocardiographic parameters in 1,909 patients. The relevant point for this manuscript is the modest variance explained by resting haemodynamics generally, which bears directly on the plausibility of estimated stroke volume carrying as much signal as Figure 3c and 3d imply.

**9. Hollmann N, Müller S, Purucker L, et al. Accurate predictions on small data with a tabular foundation model.** *Nature* 2025;637(8045):319–326. DOI 10.1038/s41586-024-08328-6. Peer-reviewed. **Not cited.** Independent (University of Freiburg / PriorLabs / ELLIS). TabPFN is now the reference method for tabular problems below 10,000 rows — precisely this manuscript's regime of 1,738 records and roughly 17 features. Its omission from a comparator set that includes TabNet, DeepTables and TabTransformer is a substantive gap, and its inclusion would test whether the FiLM architecture contributes anything beyond competent tabular modelling. Note the independent replication literature (e.g. Shaktah et al., medRxiv 2026, preprint, not peer-reviewed) finding TabPFN merely competitive with tuned GBMs on clinical tasks — which makes the 33% RMSE margin claimed here harder to attribute to architecture.

**10. Kapoor S, Narayanan A. Leakage and the reproducibility crisis in machine-learning-based science.** *Patterns* 2023;4(9):100804. DOI 10.1016/j.patter.2023.100804. Peer-reviewed. **Not cited.** Independent (Princeton University). Provides the eight-category leakage taxonomy and the model info sheet instrument. Two categories apply directly to this submission: illegitimate features (undefined variables such as "HRR" and "Resting METs" in Figure 3d, parsed from reports that contain the label) and non-independence between observations (multiple records per patient treated as independent in the survival analysis). I would require a completed model info sheet with any resubmission.

**Summary of the citation audit.** Eight of these ten are absent from the reference list, including the two — Lee et al. 2026 and Khurshid et al. 2024 — that most directly contest the manuscript's novelty and accuracy claims. The Introduction's assertion at lines 71–75 that existing approaches remain unvalidated against downstream clinical events is contradicted by reference 2 in this list. That is a literature-coverage failure, not a matter of emphasis.


# Editorial Report — Manuscript 076026

**Title:** Spectral Conventions Reveal Distinct Structural Signatures in Directed Congenital Cardiac Architectures
**Handling recommendation:** Reject without external review

---

## 1. Overall Assessment

The manuscript defines a Directed Sombor Matrix, s_ij = sqrt((d_i^+)^2+(d_j^-)^2) per arc, and compares eigenvalue-modulus energy against singular-value (nuclear-norm) energy on it, proving five properties and applying both to three directed cardiac graphs reconstructed from Lee and Chen (Sci Rep 2023): normal heart, extreme TOF with a right mBT shunt, and d-TGA with VSD. The two conventions rank these three graphs differently.

The claim is true but not consequential. All five theorems specialise standard linear algebra to one weighted adjacency matrix, and the singular-value energy is already characterised for general vertex-degree-based digraphs by Monsalve and Rada and by Espinal, Monsalve and Rada. The cardiac component is one hand-built graph per condition, no patients, and contains an anatomical construction error that propagates into the reported ranking.

## 2. Strengths

Numerical reporting is internally consistent: every Table 1 percentage, gap and McClelland bound reproduces exactly, and Directed Sombor energies were cross-checked in MATLAB. The theorems carry an honest numerical verification suite (400–300 trials per claim), including disclosure of three 1e-6-tolerance failures correctly attributed to eigenvalue conditioning in non-normal matrices. Limitation statements are disciplined: N=1 per condition and the zero-CV weight-perturbation result are both correctly flagged as artefacts rather than robustness. The separation of numerical variability from rank preservation is a genuine point, benchmarked against a 16.7% uniform-ordering null.

## 3. Weaknesses

There is no mathematical novelty: the theorems are the standard nilpotency-acyclicity equivalence, McClelland's 1971 bound, the Weyl-Horn majorization inequality, condensation block-triangularity, and the nuclear-norm triangle inequality, all specialising a framework already published by Monsalve/Rada and Espinal/Monsalve/Rada. Theorem 3's proof is also defective: it invokes log-concavity where exponential convexity is needed, and anchors equality via det S = 0, degenerate for all three DSMs (numerical rank 16/17/16 of 24/25/24). The TOF topology claims pulmonary atresia yet retains PT→RPA/LPA arcs with no inflow to PT, contradicting Table 1's claim of one SCC. Internal figures conflict with the text (4.07-fold vs. 4.1-fold speedup; Fig. 3's "reversal" vs. the Results' explicit denial of one). There is no empirical content, and the deferred weighted formulation already exists in the authors' own source reference.

## 4. Editorial Decision

**Reject without review.** The theory specialises published VDB-digraph results, the application is three non-patient graphs with an internally contradictory TOF construction, and there is no clinical or predictive claim to evaluate — a scope deficiency, not a fixable execution flaw. Realistic homes are Scientific Reports, Journal of Complex Networks, Applied Mathematics and Computation, or MATCH; no Nature Portfolio transfer is warranted.

## 5. Suggested Reviewer Expertise

Technical expertise should cover spectral theory of vertex-degree-based and Sombor matrices for digraphs, specifically energy and spectral-norm characterisations of general adjacency matrices induced by symmetric bivariate degree functions; numerical linear algebra for non-normal matrices, including pseudospectra, eigenvalue conditioning and the practical meaning of stable rank against spectral radius; directed network science concerned with strongly connected component structure, condensation, trophic coherence and directed centrality; and computational benchmarking of eigendecomposition and block-decomposition strategies for sparse directed graphs. Clinical expertise should cover congenital cardiac morphology and flow, specifically tetralogy of Fallot with pulmonary atresia and systemic-to-pulmonary shunts, d-transposition physiology, and quantitative 4D-flow cardiovascular MRI in paediatric and adult congenital populations, sufficient to adjudicate whether the three reconstructed topologies are anatomically defensible.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant mathematical sub-field has consolidated rapidly since 2021. Gutman's Sombor index (MATCH 86:11, 2021) generated an immediate spectral literature, including Gutman's own treatment of the Sombor matrix spectrum, p-Sombor spectral results by Liu, You, Huang and Fang (MATCH 87:59, 2022), the empirical comparison of ordinary and Sombor energy by Redzepovic and Gutman (MATCH 88:133, 2022), and elliptic Sombor energy work in 2024. On the directed side, Monsalve and Rada established vertex-degree-based indices of digraphs (Discrete Appl. Math. 295:13, 2021) and the energy of a digraph with respect to a VDB index (Spec. Matrices 10:417, 2022); Cruz, Monsalve and Rada treated the Sombor index of directed graphs and Randic energy of digraphs in Heliyon in 2022; Espinal, Monsalve and Rada characterised the spectral norm and energy of a digraph with respect to a VDB index (Heliyon 10:e32016, 2024), including digraphs with a single non-zero singular value and with all singular values equal; and Cruz, Espinal and Rada set out a general matrix approach to VDB indices (Mathematics 12:2043, 2024). Martinez-Martinez, Mendez-Bermudez and Sigarreta (Phys. Rev. E 109:064306, 2024) provide a random-matrix treatment of degree-based matrices that supplies exactly the statistical framing this manuscript lacks.

Against that landscape the manuscript replicates rather than advances. Its singular-value energy is the Sombor instance of a framework already characterised in 2022 and 2024, and its eigenvalue-modulus variant is the obvious complementary definition with no new sharp bound or extremal characterisation. The authors cite Espinal and Monsalve but do not engage with what those papers already prove, and they do not cite Gutman's Sombor matrix spectral work or the p-Sombor line at all. In directed network science, the natural comparators are trophic-coherence and giant-SCC approaches, exemplified by Liu, Hu, Wang, Liu and Zhang (Nat Commun 17:7866, 2026), which the manuscript cites only decoratively despite the paper's direct relevance to why localised feedback governs SCC structure. On the cardiac side, the field has moved to patient-specific 4D-flow quantification and cardiovascular digital twins; Lee and Chen (Sci Rep 13:11135, 2023) remains the only graph-theoretic CHD reference engaged, and its own weighted matrices are ignored. The manuscript should be evaluated against these works before any resubmission.

## 7. Suggested Reviewers

**Spectral theory of VDB and Sombor matrices for digraphs:** Juan D. Monsalve (Universidad de Antioquia; *Energy of a digraph with respect to a VDB topological index*, Spec. Matrices 2022); Carlos Espinal (Universidad de Antioquia; Heliyon 2024, spectral norm and energy of a digraph with respect to a VDB index); Roberto Cruz (Universidad de Antioquia; *Sombor index of directed graphs*, Heliyon 2022); Izudin Redzepovic (University of Belgrade; comparative study of ordinary and Sombor energy). Note that the first three share an institution; at most one should be invited, and Redzepovic or Zhen Lin (Qinghai Normal University, Sombor spectral radius and energy) used as the independent second.

**Numerical linear algebra for non-normal matrices:** Yuji Nakatsukasa (University of Oxford; eigenvalue conditioning and low-rank matrix computation); Nicholas J. Higham group alumni working on non-normality diagnostics; Mark Embree (Virginia Tech; *Spectra and Pseudospectra*) as a last-resort senior option if junior invitations decline.

**Directed network science and SCC structure:** Samuel Johnson (University of Birmingham; trophic coherence in directed networks); Xueming Liu (Huazhong University of Science and Technology; *Optimal dismantling of directed networks*, Nat Commun 2026); Giulia Cencetti or an equivalent early-career researcher working on directed and higher-order network spectra.

**Congenital cardiac morphology and 4D-flow MRI:** Yao-Ting Lee (National Taiwan University Hospital; author of the source topologies and the natural adjudicator of whether the TOF and d-TGA reconstructions are faithful); Alejandro Roldan-Alzate (University of Wisconsin–Madison; 4D-flow and computational modelling in congenital heart disease); Liliana Ma (Northwestern University; 4D-flow quantification in congenital populations).

Authors at Vellore Institute of Technology and co-authors of the acknowledged clinical advisers at Kauvery Hospital must be excluded.

---

## Editorial Integrity Alert (confidential to the handling editor)

Line 903 of the submitted manuscript thanks "the anonymous reviewers and the handling editor for constructive feedback." No prior submission history is disclosed in the cover material available to me. This text indicates a previous peer-review cycle elsewhere that was not declared. Recommend querying the authors on submission history and on whether reviewer reports from that cycle exist, before any decision letter is issued. Separately, references 4, 11, 13, 14, 15, 16, 18, 19, 26, 27 and 30–33 were independently verified as real and correctly attributed; no fabricated citations were detected, and no arithmetic in Table 1 or the perturbation analysis failed verification.

## Counterargument to the Recommendation

The strongest case against rejection is that this manuscript is more honest than most of what reaches review. It declines every clinical overclaim available to it, correctly diagnoses its own zero-variance result as an artefact, benchmarks rank preservation against an explicit null, and pins its computational environment. A reviewer sympathetic to network science could argue that the substantive finding — that for severely non-normal degree-weighted matrices the eigenvalue and singular-value energy conventions can order the same objects differently, and that this is not a numerical curiosity but a modelling decision — is a useful corrective to a literature that reports "graph energy" as if the convention were immaterial, and that this point is made nowhere as directly. On that reading the correct action is to send the paper out with instructions to strip the cardiac framing, fix the Theorem 3 proof, and reposition it as a methods caution for the digraph-energy community.

I do not adopt this view, for two reasons. The corrective is already implicit in Espinal, Monsalve and Rada's 2024 characterisation, which works with singular values precisely because the eigenvalue convention is ill-behaved for non-normal general adjacency matrices; and a paper whose only defensible contribution is a repositioning of existing theory does not belong in Nature Communications regardless of how well it is written. The honesty of the manuscript is an argument for a constructive rejection letter, not for review.


# Editorial Report — Manuscript 076668

**Title:** Distributed Lag Neural Additive Models
**Section:** Nature Communications — Digital Health

---

## 1. Overall Assessment

DLNAMs replace a DLNM's spline cross-basis with a neural additive component (ExU layers, Mish activations, learned subnetwork mixture) plus a last-layer Laplace/ensemble uncertainty estimate, removing basis-specification choices while preserving additive interpretability. Construction is careful, reporting candid, but the evidentiary base is thin: three of four benchmarks are author-designed simulations, and neither real-data application shows prediction, ground-truth recovery, or health utility. Two concerns dominate: the comparison is not likelihood- or tuning-matched, and this is a statistical estimator paper, not a demonstrated health advance — outside Digital Health scope.

## 2. Strengths

The component ablation is informative: removing ExU layers, the subnetwork mixture, or smooth activations each degrades error and coverage distinctly, supporting a genuine architectural contribution. The uncertainty derivation is rigorous — exact Jacobian, MacKay evidence fixed point, explicit handling of mixing-weight non-identifiability. The joint five-exposure experiment tests degradation under correlated exposures without a combinatorial cross-basis search. Reporting transparency exceeds the literature's norm.

## 3. Weaknesses

T-DLNM is fitted Gaussian on log(1+Y) while comparators are Poisson/quasi-Poisson; comparator tuning was frozen at defaults while DLNAM's budget was raised. All DGPs are self-designed "smooth," excluding the regime T-DLNM targets — and T-DLNM wins on the one non-adversarial DGP. No estimator reaches nominal coverage, undermining the calibration claim. The Chicago application is in-sample with no ground truth; the malaria application confounds estimator choice with differing adjustment specifications. Key competing methods (ACE-DLNM, SB-DLNM, mixture-DLNM) are omitted.

## 4. Editorial Decision

**Reject, with transfer.** Competent and honest, but the advantage rests on unmatched comparators and author-designed simulations, with no out-of-sample or health-consequential evaluation. Recommend **Communications Medicine** (with a health application) or **Communications Earth & Environment**; natural home is *Biostatistics* or *Environmental Epidemiology*.

**Steelman:** Every weakness is self-disclosed, and the joint-exposure result solves a real multi-exposure problem no comparator handles cleanly — a methods-paper standard may be the wrong bar. I don't adopt this because the scope mismatch stands regardless of a corrected comparison.

## 5. Suggested Reviewer Expertise

Reviewers should cover, first, distributed lag non-linear modelling and cross-basis construction for time-series environmental epidemiology, including penalized and Bayesian tree-structured variants and their simulation evaluation; second, neural additive models and interpretable-by-construction deep architectures, specifically ExU parameterisation, subnetwork mixtures, and additive component identifiability; third, approximate Bayesian inference for neural networks, particularly last-layer and linearised Laplace approximations, MacKay evidence-based hyperparameter selection, deep ensembles, and frequentist coverage of the resulting intervals; fourth, simulation study design and reporting for statistical methods, covering Monte Carlo standard errors, bias–variance decomposition, and fair comparator calibration. On the clinical and applied side, reviewers should include an environmental epidemiologist working on temperature–mortality associations in multi-city time-series designs, and a climate–infectious disease epidemiologist with experience analysing DHS/MIS childhood malaria outcomes and survey-hierarchy adjustment.

## 6. State-of-the-Art Literature Review (Past Three Years)

The distributed-lag field has moved in three directions since 2022, none of which is neural. The first is structural flexibility: Mork and Wilson's treed DLNM (Biostatistics 2022) and its multi-exposure and monotone extensions, now consolidated in the dlmtree package (R Journal 2025), and the penalized distributed lag interaction model of Demateis and colleagues (Environmetrics 2024). The second is reformulation of the estimand: the adaptive cumulative exposure DLNM (ACE-DLNM) of Wilson, Stringer and colleagues replaces the bivariate surface with a smooth function of a data-adaptively weighted cumulative exposure, precisely because the bivariate surface is hard to interpret; a unified multi-exposure ACE framework followed in 2026. The third is spatial and hierarchical pooling: the Spatial Bayesian DLNM of Quijal-Zamorano et al. (Int J Epidemiol 2024), the spatially varying heat-effect model of Chen, Blangiardo, Gascoigne and Konstantinoudis (JRSS-A 2025), and the mixture-of-DLNMs construction (Statistics in Medicine 2026). On the machine-learning side, the relevant lineage is Agarwal et al.'s Neural Additive Models (NeurIPS 2021), the Laplace-approximated NAM of Bouchiat et al. (ICML 2024), Laplace Redux (NeurIPS 2021), and deep ensembles; DLNAM is a faithful composition of these with the DLNM estimand.

Against that landscape, the manuscript advances one thing that is genuinely unoccupied: a learned, additively separable exposure–lag component with usable pointwise intervals that scales to five concurrent surfaces without a cross-basis specification search. Everything else is recombination. The ACE-DLNM line is the most serious omission, because it addresses the same interpretability complaint from the opposite direction and would supply a strong non-spline, non-neural comparator; the spatial and hierarchical DLNM work is directly relevant to the authors' own Hierarchical DLNAM extension, which they list as future work while citing only Economou et al.'s arXiv preprint. The authors should also engage the ACE and mixture literature before repeating the claim that existing approaches leave smoothness, local adaptivity, and learned representation in tension.

## 7. Suggested Reviewers

For distributed lag methodology and cross-basis evaluation: **Daniel Mork** (Harvard T.H. Chan School of Public Health; first author of the treed DLNM used here as a comparator — note this is a comparator-authorship interest and he should be asked to declare it), **Alex Stringer** (Assistant Professor, University of Waterloo; ACE-DLNM), **Yin-Hsiu Chen** (distributed lag interaction models with two pollutants), and **Marcos Quijal-Zamorano** (postdoctoral researcher, ISGlobal Barcelona; SB-DLNM, Int J Epidemiol 2024).

For neural additive models and interpretable architectures: **Kouroche Bouchiat** (ETH Zürich; LA-NAM, ICML 2024), **Christoph Kolb / Anton Thielmann** (NAMLSS, distributional neural additive models), and **Rishabh Agarwal** (original NAM construction; note industry affiliation).

For approximate Bayesian inference and interval calibration: **Alexander Immer** (postdoctoral researcher, ETH Zürich; linearised Laplace and marginal-likelihood selection), **Agustinus Kristiadi** (Vector Institute; Laplace approximations in ReLU networks), and **Erik Daxberger** (Laplace Redux).

For applied temperature–mortality epidemiology: **Ana M. Vicedo-Cabrera** (Assistant Professor, University of Bern), **Pierre Masselot** (Assistant Professor, LSHTM), and **Garyfallos Konstantinoudis** (Assistant Professor, Imperial College London).

For climate and childhood malaria in sub-Saharan Africa: **Colin J. Carlson** (Assistant Professor, Yale School of Public Health) and **Adrian Tompkins** (ICTP; climate-driven malaria modelling).

**Exclusions.** Antonio Gasparrini and co-authors (author of three comparator methods and the dlnm package, and cited eight times). Manuel Martellini O Nocentini and co-authors of the DHS/MIS malaria source study — he is acknowledged as having shaped the experimental design, comparator selection, and evaluation criteria of this manuscript, and is first author of reference [18], on which the malaria application depends. Any KTH, Karolinska Institutet, Uppsala, or Cambridge affiliate.

---

## Confidential Editorial Integrity Note (handling editor only)

Four items warrant attention, none of which I judge to constitute misconduct.

First, the acknowledged contributor Manuel Martellini O Nocentini is credited with shaping the experimental design, comparator selection, and evaluation criteria, and is first author of reference [18], the medRxiv preprint supplying the malaria data, the target-specific adjustment sets, and the empirical reference against which the DLNAM fit is judged. This is a substantive intellectual contribution to design and interpretation and sits close to the authorship threshold; at minimum the non-independence of the applied comparison should be declared, not left in Acknowledgments.

Second, reference [18] is an unreviewed medRxiv preprint posted in June 2026. One of the manuscript's two applications rests entirely on it, including the adjustment sets and the "source analysis" agreement claim.

Third, the manuscript is available on arXiv as 2609.07381, posted in early September 2026. The Prior dissemination statement discloses only the KTH master's thesis. Preprint posting is permitted, but the statement is incomplete as written.

Fourth, the malaria data are restricted and "may be available upon request from the authors of that study," and the simulated data are reproducible only by rerunning the authors' code. The Chicago component is fully reproducible; the malaria component is not independently verifiable.

Arithmetic and internal consistency were checked. The 81^5 ≈ 3.5 × 10^9 exhaustive-search figure, the 5 × 81 = 405 coordinate-wise count, and the 4.3 × 2 = 8.6 scaling extrapolation are all arithmetically correct as stated. The two presentational issues flagged in Section 3 (null-exposure leakage ordering; matched-budget comparison of the 8.6-fold figure) are framing problems, not errors.

# Editorial Report — Manuscript 076860

**Title:** Large language models exhibit unreliable clinical belief updating as patient evidence evolves
**Handling assessment:** Nature Communications, Digital Health

---

## 1. Overall Assessment

The manuscript claims that longitudinal belief updating is a reliability dimension distinct from static accuracy. In matched MIMIC-IV ICU cohorts, self-context worsens paired prediction error more often than it improves it, revision is asymmetric toward deterioration, a supplied prior causally shifts estimates with current evidence fixed, mitigation prompts fail, and a rule-based gate (EVLU) retains a smaller, more reliable subset of revisions.

The architecture is better than most work here. My decision turns on the substrate. Independent AUROC is 0.545 and Brier is 0.281; no constant predictor exceeds 0.25 at any prevalence, so the model is worse calibrated than the base rate. The primary model is Qwen3-8B with chain-of-thought disabled, and no frontier model is evaluated.

## 2. Strengths

The prior-belief intervention isolates prior influence from evolving physiology, holding snapshot, prompt and assessment fields fixed while varying only the supplied prior from 10 to 90 percent. The dose-response is orderly at 3.05 points per increment, monotonic in 70.4 percent of snapshots.

The counterfactual design carries controls this literature usually omits: across 4,545 transitions under eight conditions, redundant evidence produced 0.74 points of revision and no numerical change in 96.99 percent of cases.

Replication is serious. An independent vasopressor cohort reproduces every effect, mean absolute error rose in all eight models from 4B to 32B, inference uses ICU-stay cluster bootstrap, and the matched-random retention test (P < 0.001) shows the EVLU-2 gain is not merely reduced coverage.

## 3. Weaknesses

The substrate is uninformative. AUROC 0.545, a Brier score above the constant-predictor ceiling, and mean absolute error of 0.326 describe an estimator that cannot discriminate the outcome, and no non-LLM baseline is reported although gradient-boosted models on comparable MIMIC-IV features exceed 0.80.

Generality is unsupported. All models are open-weight and 32B or smaller; Qwen3-8B runs in non-thinking mode, suppressing the capability under study; every mechanistic, prompting and EVLU experiment uses that one model, with single-run deterministic decoding.

The headline asymmetry rests on one stratum: 0.324 at 0 to 25 percent prior risk against 0.046, 0.036 and 0.067 above, with stratum sizes unreported. The outcome-misalignment result is arithmetically the dose-response restated, not corroboration.

Clinical grounding is thin. MIMIC-IV only; matching distorts prevalence, so Brier and mean absolute error are not transportable; structured variables only; perturbations ignore physiological coupling; no subgroup analysis by age, sex or ethnicity; no clinician adjudication of whether revisions were appropriate.

## 4. Editorial Decision

**Reject**, with transfer to *Communications Medicine* or *npj Digital Medicine*. The central clinical claim rests on a model that cannot discriminate the outcome, in a non-reasoning configuration, on one dataset. If sent out, reviewers should adjudicate whether belief metrics are interpretable at AUROC 0.545, whether disabling thinking mode invalidates generalization, and whether the asymmetry is a low-prior-risk artifact.

## 5. Suggested Reviewer Expertise

Technical expertise should cover dynamic risk prediction from longitudinal structured EHR data, including landmarking and joint modelling on MIMIC-IV; evaluation methodology for open-weight LLMs, specifically calibration, proper scoring rules and multi-turn context effects; counterfactual and causal probing of language-model behaviour with clustered bootstrap inference; and probabilistic forecasting and calibration assessment in clinical prediction models, including the base-rate and constant-predictor benchmarks this manuscript omits. Clinical expertise should come from an intensivist with a research record in the timing of invasive mechanical ventilation and vasopressor initiation, and in the prospective evaluation of ICU risk scores.

## 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant landscape has three strands. First, longitudinal clinical LLM benchmarking: MedAlign (Fleming et al., AAAI 2024), TIMER (Cui et al., npj Digital Medicine 8:577, 2025), Kruse et al. (EMNLP Findings 2025), and Rao et al. (JAMA Network Open 9:e264003, 2026) established that extended histories do not yield reliable temporal reasoning. Second, bias and context dependence: Hager et al. (Nature Medicine 30:2613, 2024), Mahajan et al. (npj Digital Medicine 8:428, 2025), Tan et al. (ACL 2024) on generated-context preference, and Sheppert et al. (International Journal of Medical Informatics 219:106550, 2026), which found LLMs more anchoring-prone than physicians. Third, self-correction limits: Kamoi et al. and Pan et al. (TACL 12, 2024).

The manuscript engages all three strands competently but omits the two most directly competing recent works. CAREBench (arXiv:2510.14286) evaluates temporal stability of risk trajectories on MIMIC-IV and EHRShot, explicitly comparing zero-shot Qwen3-32B against XGBoost, random forests and deep sequence models, and reports the same instability with the trained baselines this manuscript lacks; it is the single most damaging omission, since it supplies the comparator that would determine whether the reported unreliability is LLM-specific. BayesBench (arXiv:2606.30850, preprint, not peer reviewed) evaluates belief trajectories against a rational Bayesian reference across seven open-weight models from 3B to 70B and reports that latent inference improves with scale while downstream prediction remains uncalibrated, which directly bears on the manuscript's scaling claim and provides the normative updating reference it never defines. Geng et al. (arXiv:2511.01805) on accumulating context and belief change is also relevant. Against this landscape, the controlled prior-injection experiment is the manuscript's real advance; the natural longitudinal degradation result largely replicates CAREBench and the anchoring literature in a new endpoint.

## 7. Suggested Reviewers

Longitudinal EHR modelling and dynamic risk prediction: Eleni-Rosalina Andrinopoulou (Erasmus MC; dynamic prediction with joint models, cited as reference 21), Shengpu Tang (Emory; clinical time-series ML), Shalmali Joshi (Columbia; temporal reliability of clinical ML).

LLM evaluation, calibration and context effects: Paul Hager (TUM; Nature Medicine 2024, reference 8), Bryan Wilie (HKUST; belief revision in LLMs, reference 12), Hexiang Tan (CAS; generated-context conflicts, reference 16), Wai-Chung Kwan (MT-eval multi-turn benchmark, reference 17).

Counterfactual probing and Bayesian belief evaluation: Ankur Samanta (BayesBench), Seewon Choi (CAREBench).

Calibration and proper scoring in clinical prediction: Ben Van Calster (KU Leuven), Laure Wynants (Maastricht), Kim Luijken (UMC Utrecht).

Critical care: Michael Sjoding (Michigan; ML and respiratory failure), Sarah Seelye (Michigan; respiratory failure prediction), Gary Weissman (Penn; ICU prediction model evaluation).

Conflicts: exclude all University of Minnesota affiliates and prior co-authors of R. Zhang, including N. Ingraham and G. Melton. Note that reference 22 (Kamoi et al., TACL 2024) lists a different Rui Zhang, at Pennsylvania State University; this is a name collision, not a self-citation, and that group is not conflicted.

# Editorial Report — Manuscript 077884

**Title:** Identifier memorization masquerades as biological signal in metabolite–disease prediction
**Handling section:** Nature Communications, Digital Health

---

## 1. Overall Assessment

The manuscript argues that standard metabolite–disease evaluation measures curation artefacts, not biology: AUROC 0.967 retains 0.968 after label permutation, 0.958 with the disease block deleted. Correcting three confounds, the authors report 0.762 for unseen metabolites of a known disease and 0.501 for entirely unseen diseases, attributing this to identifier memorisation; MeSH hierarchy position lifts extrapolation to 0.584. No patient, endpoint, or deployment context appears anywhere — this is bipartite-graph benchmark methodology, not digital health — and the central diagnostic is uncited prior art (Aiyappa et al., ICML 2025).

## 2. Strengths

The control architecture is strong: full, permuted, and representation-blind arms per regime, pre-specified equivalence testing, and demonstrated rather than asserted seed sufficiency. Shuffling training labels returns every sub-chance arm to within 0.006 of 0.5, cleanly separating overfitting from pipeline fault. The constructive arm earns the central claim: hierarchy position lifts extrapolation while a matched Gaussian block does not, confirmed independently by graph convolution. Calibration reported separately from discrimination — extrapolation worse than base rate despite near-chance AUROC — is uncommon and consequential here.

## 3. Weaknesses

Scope is disqualifying: no human subjects, no clinical data, no deployment pathway. Novelty is overstated: Aiyappa et al. (ICML 2025) already shows a degree-only null approaches optimal performance under the conventional design, uncited. The extrapolation null is partly sampler-guaranteed, since within-disease degree matching also nulls disease-general chemistry that is genuine biology. Reported quantities fail to reconcile: 46,432 − 2,317 = 44,115, not the stated 44,093; pooled n = 16,627 at prevalence 0.2881 is incompatible with the 1:1 matched 9,582-pair design; the audit package's 26%/52% shares contradict Figure 6f's 33%/25% for the same corpus.

## 4. Editorial Decision

**Reject, with transfer recommended.** No clinical content, and the core correction is anticipated by uncited prior art. Transfer to **Communications Biology** or **npj Systems Biology and Applications**, conditional on reconciling the numerical inconsistencies and engaging the missing literature.

**Counterargument.** The field publishes metabolite–disease models at AUROC >0.99 on this flawed protocol; a powered negative result with a released audit tool has field-level value disproportionate to its novelty. I do not adopt this view: the scope mismatch is not reparable by revision.

---

## 5. Suggested Reviewer Expertise

Approximately 70% technical, 30% domain. (i) Positive-unlabelled learning and negative-sampling design for biomedical link prediction, specifically reliable-negative selection on sparse bipartite association graphs. (ii) Evaluation methodology for graph machine learning, covering degree-corrected benchmarks, entity-disjoint and cold-start splitting, and degree-only null models. (iii) Cheminformatics representation and split design — ECFP4 fingerprints, Tanimoto nearest-neighbour analogue bias, and the applicability limits of Bemis–Murcko scaffold splitting to acyclic metabolites. (iv) Biomedical ontology representation learning, particularly MeSH and Disease Ontology positional encodings and ontology-derived transfer to unseen entities. (v) Clinical and experimental metabolomics, covering HMDB curation practice, biospecimen reporting bias, and the downstream use of prioritised metabolite candidate lists.

---

## 6. State-of-the-Art Literature Review (Past Three Years)

Three lines of work define the current landscape. The first is the continuing stream of metabolite–disease predictors reporting near-ceiling performance under exactly the protocol this manuscript attacks: GMAMDA (Hu et al., *J. Chem. Inf. Model.* 65, 5242–5254, 2025) reports AUC 0.9962 with an adaptive-hardness negative sampler; SMDPG (Huang et al., *IEEE/ACM TCBB* 22, 672–683, 2025) and WGCNCDLC (Liu et al., *TCBB* 22, 744–756, 2025) both target negative-sample reliability; DHG-LGB (*Metabolites* 16, 116, 2026) claims its model learns biological patterns rather than memorising, on the basis of dropout settings and a 96.7% literature-validation rate in case studies. The manuscript's critique lands squarely on these, yet it engages none of the 2025 negative-sampling papers, which is a significant omission given that its own headline correction is a negative sampler.

The second line is benchmark-validity work outside metabolomics, where the manuscript's originality is most exposed. Aiyappa, Wang, Kim, Seckin, Ahn and Kojaku, "Implicit degree bias in the link prediction task" (*Proc. ICML* 267:874–908, 2025), shows that uniform negative-edge sampling biases evaluation toward degree, that a degree-only null approaches optimal performance, and proposes a degree-corrected benchmark — the same diagnostic and the same remedy, one year earlier and uncited. Timely-MDA (Zhou et al., *IEEE BIBM* 2024, doi:10.1109/BIBM62325.2024.10822171) built a generalisable-split benchmark for miRNA–disease association, the closest sibling task. Kapoor and Narayanan (*Patterns* 4, 100804, 2023) is cited and used appropriately. The third line is clinically anchored metabolomics prediction, for example MetaboLM (*Nat. Commun.* 2026, s41467-025-66163-3), a transformer pre-trained on UK Biobank plasma metabolomics for multi-disease early prediction; it illustrates the kind of patient-level work this section publishes and how far the present manuscript sits from it.

Situating the manuscript: it advances the field by supplying a mechanistic account (identifier memorisation) and a falsifiable constructive test (ontology-position exchange with dimensionality and vocabulary controls) that the general degree-bias literature does not provide, and by transferring the diagnostic to an independent gene–disease corpus. It replicates, without attribution, the degree-corrected sampler and degree-only null of Aiyappa et al. and the interpolation/extrapolation distinction of Pahikkala et al. The authors should also apply their own logic to their repair: MeSH hierarchy position is itself a product of curation attention, no per-disease confidence structure or precision-at-depth is reported for the 0.584 arm, and 0.584 is not a usable operating point for discovery.

---

## 7. Suggested Reviewers

**Negative sampling and PU learning for biomedical link prediction.** Wei Lan (Guangxi University; SMDPG, *TCBB* 2025, optimised negative sampling for metabolite–disease). Yiran Huang (Guangxi University; co-author, SMDPG). Chen Chen (Xinjiang University; GMAMDA, *JCIM* 2025, adaptive-hardness negative sampling). Qiao Ning (Dalian Maritime University; DCMDA, *TCBB* 2025).

**Graph benchmark validity and degree bias.** Sadamori Kojaku (Assistant Professor, Binghamton University; Aiyappa et al., ICML 2025, degree-corrected link-prediction benchmark). Rachith Aiyappa (Indiana University Bloomington; first author, same). Tyler Derr (Assistant Professor, Vanderbilt University; Wang & Derr, ICDMW 2022, the manuscript's reference 13). Munjung Kim (Indiana University Bloomington; co-author, ICML 2025).

**Cheminformatics evaluation and split design.** Tapio Pahikkala (University of Turku; reference 14, the interpolation/extrapolation framework this protocol reproduces). Antti Airola (University of Turku; co-author, same). José Jiménez-Luna (Imperial College London; molecular property benchmarking and split sensitivity). Andrea Volkamer (Saarland University; fingerprint similarity and benchmark design) as a senior fallback.

**Ontology representation and transfer.** Maxat Kulmanov (KAUST; ontology embeddings, DeepGO and OPA2Vec line of work). Şenay Kafkas (KAUST; disease-ontology text and hierarchy representations). Robert Hoehndorf (Associate Professor, KAUST; DL2Vec, ontology-based disease representation) as a senior fallback.

**Clinical and experimental metabolomics.** Jennifer Kirwan (Berlin Institute of Health; clinical metabolomics quality and reporting standards). Julijana Ivanisevic (University of Lausanne; clinical metabolomics and biomarker validation). Michael Witting (Helmholtz Munich; metabolite annotation confidence and database curation). David Wishart (University of Alberta) should be **excluded**: HMDB is the source resource under critique, a direct conflict.

Exclude all authors affiliated with BRIC-NABI, Mohali, and any co-author of the submitting group within the past five years. Reviewer ranks and current affiliations should be confirmed by the editorial office before invitation.

---

*Verification performed for this report: arithmetic recomputation of cohort counts, pair counts, prevalence, network density, regime gaps and ablation deltas; independent search of 2024–2026 metabolite–disease and link-prediction benchmark literature; citation-content checks on references 6, 8, 13, 14, 22 and 29; preprint-overlap search on the manuscript title and author group, with no overlap found.*
