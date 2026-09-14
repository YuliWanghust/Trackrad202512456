# Trackrad202512456

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

070143
# Editorial Report — Manuscript 070143
**Title:** Integrating Single-Molecule Variant Phenotyping with Clinical Features Predicts Outcomes in KIF1A-Associated Neurological Disorder

---

## 1. Overall Assessment

The manuscript integrates smTIRF motility phenotyping of 91 KIF1A variants with computational scores and longitudinal data from 343 patients to stratify KAND into stable versus declining trajectories (AUC 0.834) and predict VABS ABC (r²=0.484, age ≥10) via a two-stage LOVO-CV/LOO-CV Random Forest.

The advance is real but narrower than framed. The same senior authors previously showed (Sudnawa et al., Genet Med 2024, ref. 13) that EEG/seizure plus ESM explain 34% of VABS ABC variance in 177 patients. The gain to 48.4%, with seizure/EEG again the top predictor, is incremental. The decisive concerns are absent external validation and an arithmetic inconsistency.

## 2. Strengths

The single-molecule dataset is the largest for any kinesinopathy: 91 variants across 66 residues, linked to 343 phenotyped patients.

The two-stage design correctly addresses leakage from recurrent variants (R254W n=31, R316W n=29) by separating variant- and patient-level modeling.

The clustering is mechanistically anchored: Cluster 2 (loss of processivity) is enriched for declining patients (OR=3.08, P=0.002), converging with MisFit-S and cryo-EM data on P305L.

The ablation directly tests the central claim: AUC falls from 0.834 to 0.732 without molecular and computational layers.

## 3. Weaknesses

No independent validation cohort exists; all metrics are internal cross-validation.

The five recurrent variants are said to account for "101 individuals (35%)" of 313, but 101/313 = 32.3%; the 313-versus-343 denominators also need reconciling.

Fig. 3c reports dozens of correlations without confidence intervals or multiple-testing correction; one is already shown to be a single-observation artifact.

Deployment is unaddressed: the molecular arm requires bacterial expression and smTIRF per novel variant, and no demographic breakdown is reported despite known registry skew.

## 4. Editorial Decision

**Send for Review.** The integration clears the bar despite missing external validation, provided reviewers adjudicate: whether the variance gain over the authors' own prior model justifies the added infrastructure; whether patient-level LOO-CV is independent given identical Stage-1 predictions within recurrent variants; and whether the fixed VABS-ABC-50 threshold requires sensitivity analysis now.

## 5. Suggested Reviewer Expertise

A single-molecule TIRF biophysicist for kinesin motors; a computational biologist experienced in leave-one-variant-out CV for small-n rare-disease ML; a deep-mutational-scanning/MAVE specialist for REVEL/gMVP/AlphaMissense/ESM/MisFit context; a pediatric neurogeneticist with KAND/HSP experience; a rare pediatric neurological trial-design expert.

## 6. State-of-the-Art Literature Review (Past 3 Years)

KAND genotype-phenotype work has moved from case series toward quantitative integration. Boyle et al. (2021) and Rao et al. (Biomolecules 2025, same senior authors) linked motility to severity at the residue level. Sudnawa et al. (2024), same corresponding group, is the direct predecessor, already explaining 34% of variance with EEG/seizure plus ESM. Cryo-EM (Benoit et al. 2024) and force-generation work (Budaitis et al. 2021) supply mechanism. Variant-effect prediction advanced via AlphaMissense (Cheng et al., Science 2023), gMVP (Zhang et al. 2022), ESM-1b (Brandes et al. 2023), and MisFit (Zhao et al. 2025), all correctly deployed. Missing is engagement with the broader MAVE-to-clinic literature (ClinGen, Atlas of Variant Effects Alliance); situating this pipeline within that paradigm, rather than as first-of-kind, would better calibrate the novelty claim.

---

## 7. Further Literature (2023–2026)

**1. McEwen AE, Tejura M, Fayer S, Starita LM, Fowler DM. Multiplexed assays of variant effect for clinical variant interpretation. *Nat Rev Genet* 2026;27(2):137–154. DOI 10.1038/s41576-025-00870-x.** Peer-reviewed review; not cited. Fully independent. This is the central framing gap: the manuscript presents functional-assay-to-clinical-outcome integration as novel without engaging the established MAVE clinical-interpretation paradigm it sits inside. Authors must cite and position against this.

**2. Esposito D, Weile J, Rubin AF, et al. MaveDB 2024: a curated community database with over seven million variant effect measurements. *Genome Biol* 2025;26:13. DOI 10.1186/s13059-025-03476-y.** Peer-reviewed; not cited. Independent. Directly relevant infrastructure — the authors' 91-variant smTIRF dataset should arguably be deposited here for reuse, which bears on the weak "available on request" data statement.

**3. Allen S, Garrett A, Muffley L, et al. Workshop report: the clinical application of data from multiplex assays of variant effect (MAVEs). *Eur J Hum Genet* 2024;32:593–600. DOI 10.1038/s41431-024-01566-2.** Peer-reviewed; not cited. Independent. Establishes the clinical-validation standards (truth sets, evidence strength calibration) that this manuscript's prognostic framework does not meet and does not acknowledge.

**4. Berecki G, Howell KB, Heighway J, et al. Functional correlates of clinical phenotype and severity in recurrent SCN2A variants. *Commun Biol* 2022;5:515. DOI 10.1038/s42003-022-03454-1.** Peer-reviewed; not cited. Independent. The closest methodological precedent and the strongest counterexample: using dynamic action potential clamp across 38 recurrent SCN2A variants in 179 individuals, the authors found biophysical measurement predicted phenotypic *group* but not *severity*. This directly challenges the present manuscript's central premise and must be engaged.

**5. Knox AT, Thompson CH, Scott D, et al. Genotype-function-phenotype correlations for SCN1A variants identified by clinical genetic testing. *Ann Clin Transl Neurol* 2025;12(3):499–511. DOI 10.1002/acn3.52297.** Peer-reviewed; not cited. Independent. Automated patch clamp plus neuronal simulation in a real-world cohort — the channelopathy analogue the manuscript gestures at in its generalization claim without citing.

**6. Xian J, Parthasarathy S, Ruggiero SM, et al. Delineating clinical and developmental outcomes in STXBP1-related disorders. *Brain* 2023;146(12):5182–5197. DOI 10.1093/brain/awad287.** Peer-reviewed; not cited. Independent. 1,281 patient-years of longitudinal trajectory modeling in a monogenic DEE. Sets the methodological bar for trajectory delineation that the present fixed-threshold VABS-50 stratification falls short of.

**7. Kaat AJ, et al. Vineland-3 Growth Scale Values: psychometric properties for clinical trial readiness in SCN2A. *J Child Adolesc Psychopharmacol* 2025;35(7):416–423.** Peer-reviewed; cited (ref. 23). Independent. Supports the GSV analysis, but the authors use it only for justification and do not adopt its psychometric cautions about GSV floor effects — directly relevant to the floor-level Group 2 subset.

**8. Rao L, Li W, Shen Y, Chung WK, Gennerich A. Distinct clinical phenotypes in KAND result from different amino acid substitutions at the same residue. *Biomolecules* 2025;15(5):656. DOI 10.3390/biom15050656.** Peer-reviewed; cited (ref. 6). **Not independent — same authors.** This is the source of the homodimer-versus-heterodimer justification in the Limitations. Reviewers should assess whether the present manuscript is sufficiently distinct from it, or whether the two constitute overlapping publication of the same smTIRF resource.

**9. Lin Q, Agrawal S, Ng PC, et al. KIF1A-associated neurological disorders: therapeutic opportunities and challenges. *Eur J Hum Genet* 2025. DOI 10.1038/s41431-025-01978-8.** Peer-reviewed; cited (ref. 8). Independent. Notes that reported KAND cases concentrate in high-income countries — the explicit basis for the demographic-representativeness weakness raised above, which the authors cite but do not address.

**10. Zuccaro MV, et al. Antisense oligonucleotides to KIF1A polymorphisms expand targets and rescue patient-derived neurons in vitro. *Nat Commun* 2026;17(1):1109.** Peer-reviewed; cited (ref. 21). **Independence requires verification** — overlapping institutional provenance with the corresponding authors is plausible and should be checked before reviewer invitation. Establishes the therapeutic context on which the trial-stratification claim depends.

*Excluded on purpose:* the recent bioRxiv preprint on differential axonal trafficking of KIF1A variants in iPSC-derived neurons (2026) is unreviewed and cites Rao et al. 2025 approvingly; it is worth the authors' awareness as convergent evidence but should not carry weight in the review.

---

## Suggested Reviewer Names

**Biophysics:** Kristen Verhey (Michigan); Ahmet Yildiz (UC Berkeley); William Hancock (Penn State).

**Statistical genetics/ML:** Anne O'Donnell-Luria (Broad/Boston Children's); Karen Eilbeck (Utah).

**MAVE/deep mutational scanning:** Douglas Fowler (Washington); Lea Starita (Washington, Brotman Baty); Jochen Weile (Toronto).

**Pediatric neurogenetics:** Ingrid Scheffer (Melbourne); Heather Mefford (St. Jude) — verify no KAND-registry co-authorship overlap.

**Trial design:** Timothy Yu (Boston Children's) — verify independence given refs. 20–21 overlap; Nicole Calakos (Duke).

---
*Integrity note: 101/313 recalculates to 32.3%, not the stated 35% — a reporting error, not escalated to a confidential alert. Entry 8 flags a possible overlapping-publication question with the authors' own Biomolecules 2025 paper; this should be put to reviewers explicitly. Reviewers marked "verify" require conflict screening before invitation.*

073151
# Editorial Report — Manuscript 073151

**Title:** Towards Self-Improving Neural Networks: LLM-Guided Design of Medical Image Models
**Handling assessment:** Nature Communications, Digital Health

---

## 1. Overall Assessment

The manuscript claims that a large language model rewriting full Python source inside an automated train-and-evaluate loop can design medical image architectures with no predefined search space. OpenEvolve (LLM mutation with MAP-Elites) and autoresearch (a greedy agentic loop) are run on three histopathology cohorts over frozen UNI embeddings and five MedMNIST v2 benchmarks.

All twelve dataset-averaged AUCs and the 80% parameter reduction recompute exactly; the problem is evidentiary weight, not internal consistency. Every gain is measured against a self-constructed weak seed, and no published baseline appears.

## 2. Strengths

Transparency is unusually good: the authors flag the GPT-5-versus-Claude confound, the prompt-supplied Perceiver motif, and the self-attention track's missing scored baseline.

The parameter-efficiency result is defensible and mechanistically explained: parameter count is an explicit MAP-Elites descriptor axis, giving 340,663 versus 2,290,603 parameters at 0.904 versus 0.900 mean test AUC on MedMNIST.

The free-form code substrate buys something real: the quadratic-attention seed crashes with CUDA out-of-memory over 46,000-patch bags, and the LLM reads the stack trace and installs an O(NM) cross-attention bottleneck, a repair no supernet method can express.

## 3. Weaknesses

No competitive baseline is run. ABMIL is cited but never used, and CLAM and TransMIL are absent, though the paper adopts the splits of Tang et al. [27], for which ABMIL and ABMILX numbers are published on identical data. The evolved ChestMNIST test AUC of 0.766 falls below the benchmark's own ResNet-18 (224) entry of 0.773.

The headline claim comes from the track without a shared baseline. The abstract's 0.942 to 0.955 at p<0.05 is measured against an LLM-generated repair program. On the mean-pooling track, the only shared baseline, the gain carries p=0.17; and on the self-attention track autoresearch's first working program reaches 0.965 with no search, above OpenEvolve's 70-iteration 0.955.

The inference cannot support these effect sizes. Each configuration is a single run at one fixed seed, the reported model is best-of-70 selected on validation, and the one-sided bootstrap is uncorrected. Selection overfitting is visible: autoresearch wins MedMNIST validation (0.927) but loses test (0.900 versus 0.904).

Novelty is thin and clinical grounding absent. LLMatic (GECCO 2024) already pairs LLM code mutation with MAP-Elites and is uncited. No calibration, subgroup analysis or deployment context is reported.

## 4. Editorial Decision

Reject, with transfer to npj Artificial Intelligence or Communications Engineering. Both problems are structural: gains are measured against deliberately weak seeds, and single-run evaluation cannot support differences of this size. Repair requires published baselines and repeated independent searches, beyond the scope of revision.

## 5. Suggested Reviewer Expertise

Reviewers should cover, on the technical side: LLM-driven neural architecture search and code-mutation evolutionary loops, specifically quality-diversity methods such as MAP-Elites; multiple-instance learning aggregator design for gigapixel whole-slide images on frozen foundation-model embeddings (ABMIL, CLAM, TransMIL, ABMILX); benchmarking methodology and statistical inference for stochastic search, including run-to-run variance, selection bias in best-of-N reporting, and resampling-based hypothesis testing; and efficient-attention and parameter-efficient architecture design (Perceiver-style latent bottlenecks, squeeze-and-excitation, depthwise separable and dilated convolutions). On the clinical side: a practising diagnostic pathologist with computational pathology experience in breast and non-small-cell lung cancer subtyping who can judge whether slide-level AUC at this level is clinically meaningful and whether the TCGA/CPTAC framing has any deployment validity.

## 6. State-of-the-Art Literature Review (Past 3 Years)

LLM-driven architecture search has moved quickly since 2024 and the manuscript engages with only a fraction of it. GuidedEvolution (Morris et al., GECCO 2024) established LLM mutation of PyTorch source, and AlphaEvolve (Novikov et al., 2025) generalized it to full codebases under automated evaluation; both are cited. LLMatic (Nasir et al., GECCO 2024) is the critical omission, having already paired LLM code mutation with MAP-Elites quality-diversity — precisely the OpenEvolve configuration studied here. RZ-NAS (ICML 2025), CoLLM-NAS (2025) and LM-Searcher (2025) further develop reflective and cross-domain LLM-guided search. In medical imaging, Pathology-NAS (Su et al., npj Digital Medicine 2025) is the direct competitor and is cited, though dismissed on the grounds of its supernet constraint without any empirical comparison. Agentic pipeline builders such as M3Builder and mAIstro occupy an adjacent niche and are correctly distinguished.

On the evaluation side, the computational pathology field has consolidated around foundation-model encoders with attention-based MIL: UNI (Chen et al., Nature Medicine 2024) is used here as the frozen encoder, with CONCH, Virchow2, Prov-GigaPath and H-Optimus-0 now routine comparators, and recent benchmarking work (for example the npj Precision Oncology 2026 endometrial subtyping study) pairs each encoder with TransMIL and CLAM across discovery and external cohorts. Against that landscape this manuscript advances the field in one narrow respect — demonstrating that a free-form code search can repair a candidate that does not compile, which no supernet method can do — and otherwise replicates established results on established data with no established baseline. The authors must engage LLMatic directly on novelty, and must situate their absolute AUCs against the ABMIL/ABMILX numbers of Tang et al. [27] on the very splits they adopted.

## 7. Suggested Reviewers

For LLM-guided NAS and quality-diversity search: Sam Earle (postdoctoral researcher, New York University; LLMatic, GECCO 2024); Clint Morris (Georgia Tech Research Institute; GuidedEvolution, GECCO 2024, cited as ref. [11]); Antoine Cully (Reader, Imperial College London; quality-diversity and MAP-Elites methodology); Zhichao Lu (Assistant Professor, City University of Hong Kong; evolutionary multi-objective NAS, NSGANetV2).

For MIL aggregator design on foundation-model embeddings: Wenhao Tang (Xiamen University; ABMILX and the cohort splits used here, ref. [27]); Ming Y. Lu (Harvard Medical School / Mass General Brigham; CLAM and UNI); Richard J. Chen (UNI, ref. [2]) — note that citing Chen's own model is not a conflict of interest with the submitting group, though he should be screened for co-authorship with Kather or Truhn; Maximilian Ilse (Microsoft Research; ABMIL, ref. [31]).

For medical-imaging benchmark methodology: Xiu Su (Central South University; Pathology-NAS, npj Digital Medicine 2025, the closest competing work); Jiancheng Yang (postdoctoral researcher, EPFL; MedMNIST v2, ref. [23]); Siem de Jong or an equivalent early-career author from the PathBench-MIL group (ref. [9]) for MIL benchmarking practice.

For clinical computational pathology: Nicolas Coudray (Assistant Professor, NYU Grossman School of Medicine; deep-learning NSCLC subtyping from whole-slide images); Rajarsi Gupta (Assistant Professor, Stony Brook University; practising pathologist and computational pathology methodologist).

Exclusions: any author at RWTH Aachen, TU Dresden, NCT Heidelberg, Stanford Radiology or Penn Radiology, and any recent co-author of Kather or Truhn, including the STAMP pipeline group.

## 8. Counterargument to the Recommendation (Steelman)

The strongest case against rejection is that the baseline objection partly misreads the paper's claim. The authors are not claiming state-of-the-art accuracy; they are claiming that an automated loop reliably converts a reasonable starting point into a better one, and for that claim the correct comparator is the seed, not the field. Under that reading the design is deliberate: identical budget, identical seed, identical training pipeline, with only the search varying. Demanding that the evolved model beat CLAM would be demanding a different experiment. There is also a fair argument that the transparency here should be rewarded rather than punished — the authors flagged the GPT-5/Claude confound, the prompt-supplied Perceiver motif and the non-shared self-attention baseline themselves, and a report that rejects them partly on the strength of their own disclosures creates a bad incentive for the field.

I do not find this sufficient, for two reasons. First, the seed-relative claim still fails on its own terms, because the mean-pooling track's test improvement is not significant (p=0.17) and autoresearch's unsearched repair program outscores 70 iterations of OpenEvolve on the self-attention track. Second, a Nature Communications paper asserting that this step "can be handed to an automated loop" in medical AI is making a claim about practice, and practitioners will compare against CLAM and ResNet-18, not against a mean-pooling stub. The transparency point is well taken and is why this should be transferred rather than dismissed.

---

*Integrity verification: all reported dataset-averaged AUCs, per-cohort gains, parameter ratios and GPU-hour accounting were independently recomputed and are internally consistent. References [16] and [27] were verified against source. No preprint overlap, salami-slicing or undisclosed duplicate publication was identified. Competing-interest disclosures for DT and JNK are extensive and appear complete. One factual inconsistency should be corrected regardless of outcome: the Discussion describes the 341K versus 2.29M parameter gap as "an order of magnitude", while the Results correctly state 6.7×.*

*Note on length: Sections 1–4 condensed to 403 words. Sections 5–8 and the integrity note are preserved verbatim. Further condensation would require dropping either the Tang et al. split evidence or the MedMNIST ResNet-18 comparison, both of which are load-bearing for the decision.*

072874
# Editorial Report — Manuscript 072874

**Title:** Podocytopenia, identified by AI-based automated cell quantification in kidney biopsies, is an independent prognostic marker in membranous nephropathy
**Handling editor:** Nature Communications, Digital Health
**Recommendation:** Reject (transfer offered)

---

## 1. Overall Assessment

The manuscript claims podocyte density, measured by a commercial deep learning platform on PAS-stained biopsies, independently predicts renal outcome in membranous nephropathy, additive to PLA2R1-antibody level. The cohort is strong: 163 immunosuppression-naive patients, triple-assay PLA2R1, EM staging, 60-month follow-up, 43 events.

The exposure variable fails scrutiny. Podocytes are identified by nuclear morphology on PAS alone, with no WT1 or p57 confirmation, validated only against pathologists reading the same ambiguous images. The metric — 2D nuclear profiles per glomerular area from 1–2 µm sections, uncorrected for stereology — is a known biased estimator whose bias tracks nuclear size, and the finding that podocyte nuclear size is itself predictive is the signature of that artifact, not corroboration. Reported values are also inconsistent across text, tables and figures.

## 2. Strengths

The cohort — prospective, immunosuppression-naive, triple-assay PLA2R1, central pathology, 60-month follow-up — is a genuine asset. Ground truth (720 glomeruli, ~65,000 cells) and the four-class panel are comprehensive. Mesangial, endocapillary and parietal densities were null throughout, and glomerular size was non-predictive — a specificity pattern a uniform technical artifact would not easily produce, the paper's strongest argument. The biological framing (podocyte loss driving hyperfiltration-induced sclerosis) is coherent and clinically actionable.

## 3. Weaknesses

Podocyte identity is unverified: no antigen-specific marker, ICC 0.93 (lowest class) computed against human agreement on nine glomeruli, no confusion matrix, no held-out test set. The density estimator is a biased 2D proxy, variable section thickness, uncorrected for nuclear-size-dependent sampling. Survival modelling is overfit (~14 df, 43 events, EPV ≈3.1), with four collinear same-denominator densities entered jointly, no calibration, no competing-risk handling for death, and no treatment adjustment despite unprotocolised immunosuppression. Additivity is undercut by a non-significant antibody effect (p=0.089); independence rests on an underpowered null interaction. Numerical inconsistencies are pervasive: discordant density values, discordant glomeruli-per-biopsy figures, tertile cutpoints incompatible with the reported median, a mismatched Figure 3 risk-set total, EM stages summing to 162. No external cohort, no code/data availability, single scanner, single site.

## 4. Editorial Decision

**Reject, not sent for review.** The central variable's validity is unestablished, its likely bias runs toward the reported effect, and the manuscript's own numbers do not reconcile — this requires re-measurement, not reviewer adjudication. A corrected resubmission (antigen-confirmed subset, corrected estimator, parsimonious model with treatment covariate, competing risks, external validation) could go to **Communications Medicine**, or **npj Digital Medicine** if externally validated with released code; a nephrology-specialist journal is the more realistic near-term home for the clinical finding.

## 5. Suggested Reviewer Expertise

Technical: (i) deep learning for nuclei detection and multi-class cell classification in whole-slide renal histopathology, including confusion-matrix-level validation and stain/scanner generalisation; (ii) quantitative podometrics and model-based stereology for podocyte number and density estimation in human biopsies; (iii) biostatistics of prognostic modelling with time-to-event data — events-per-variable, penalisation, optimism correction, competing risks, and incremental discrimination metrics; (iv) reproducibility and reporting standards for clinical AI in pathology (TRIPOD+AI, CLAIM, model and data availability). Clinical: (v) nephropathology and clinician-science in membranous nephropathy, PLA2R1 biology, and KDIGO-based risk stratification for immunosuppression.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Automated glomerular analysis on routine stains is a mature subfield that this manuscript does not engage with at all. Hermsen et al. (*JASN* 2019) and Jayapandian et al. (*Kidney Int* 2021, NEPTUNE) established multi-class segmentation of glomerular compartments across PAS, silver and trichrome stains; Bouteldja et al. (*JASN* 2021) demonstrated cross-species, cross-stain generalisation; Sarder's group and the Kidney Precision Medicine Project have since extended this to computational biopsy phenotyping with public data and code. Zheng et al. (2024) reported CNN-based classification of the three intrinsic glomerular cell types in diabetic nephropathy on PAS with per-class F1 above 0.84 — the closest direct methodological precedent, uncited here, and the natural baseline against which HyperDeepGlomNet should have been compared.

On the podocyte side, the relevant standard is podometrics, not PAS nuclear counting. Venkatareddy et al. (*JASN* 2014) provided the single-section correction method; Zimmermann, Puelles and colleagues (*JCI Insight* 2021) profiled over 27,000 podocytes across 1,095 glomeruli using dual-antigen immunofluorescence with U-Net segmentation and linked podocyte depletion to outcome in ANCA-associated glomerulonephritis — work that originates in part from the submitting institution and is neither cited nor distinguished. Butt et al. (*Kidney Int* 2023, AMAP) extended deep learning to foot-process morphometry. Against this landscape the present manuscript is methodologically a step backwards: it substitutes an unvalidated morphological proxy on PAS for an antigen-specific measurement, and its novelty reduces to the clinical association in membranous nephropathy. That association is interesting and, to my knowledge, not previously reported at this scale — but it is inseparable from the measurement question, and the authors' failure to cite either the computational pathology or the podometrics literature suggests the work was not developed with either in view.

## 7. Suggested Reviewers

*Computational renal pathology:* Pinaki Sarder (University of Florida); Meyke Hermsen (Radboud UMC); Brandon Ginley (University at Buffalo); Nassim Bouteldja (RWTH Aachen).
*Podocyte quantification and morphometry:* Florian Siegerist (University of Greifswald); Nicole Endlich (University of Greifswald); Jeffrey Hodgin (University of Michigan); Luise Cullen-McEwen (Monash University).
*Prognostic model methodology:* Maarten van Smeden (UMC Utrecht); Ben Van Calster (KU Leuven); Georg Heinze (Medical University of Vienna).
*Membranous nephropathy / nephropathology:* Tiffany Caza (Arkana Laboratories); Barbara Seitz-Polski (Université Côte d'Azur); Hanna Debiec (INSERM, Sorbonne Université).

Excluded for conflict: all investigators at UKE Hamburg-Eppendorf and the University of Würzburg (including the podometrics group there), Charité Berlin, and any affiliate of HS Analysis GmbH or Koania Complement Analytics GmbH.

---

## Confidential Editorial Integrity Alert

1. **No competing interests statement is present.** Two co-authors (S. Biniaminov, N. Biniaminov) are affiliated with HS Analysis GmbH, the vendor of HSA KIT and HSA REG — the commercial platform the manuscript validates and recommends for routine diagnostic use. A further co-author is affiliated with Koania Complement Analytics GmbH. This is a material, undeclared commercial interest and must be disclosed before any further consideration.
2. **No data availability, code availability, or author contributions statements.** The model is proprietary and no weights, code, annotations, or derived measurements are offered. Independent replication is impossible as submitted.
3. **Cohort overlap with reference [12] (Mahmud et al., *PLoS One* 2019) is disclosed**, which is appropriate. However, that parent publication reported interstitial fibrosis and tubular atrophy as an independent predictor (HR 1.32, p = 0.03) in the source cohort, whereas the present analysis finds it non-predictive. The discrepancy is attributed to the inclusion of podocyte density but is never directly reconciled. Authors should state the exact overlap and address the contradiction.
4. **Reference [11] duplicates reference [3] verbatim** (Ronco et al., *Nat Rev Dis Primers* 7:69, 2021).
5. **Reference [16]** (Neuen et al., *JAMA* 2026, online ahead of print) could not be independently verified in the form given; the DOI and PMID should be confirmed at revision.
6. The numerical discrepancies catalogued in Section 3 are, taken individually, plausibly transcription errors. Taken together — five density values, two glomeruli-per-biopsy figures, a tertile definition, a risk-set total, and a stage total, all disagreeing — they indicate that the manuscript was not reconciled against its own analysis output.

---

## Counterargument to the Recommendation

The strongest case against rejection: the specificity of the finding is difficult to explain as artifact. A nuclear-size or sectioning bias should degrade or distort all four cell classes, yet mesangial, endocapillary and parietal densities are null in both the full cohort and the antibody-positive subcohort, and the podocyte effect survives adjustment for IFTA, proportion of normal glomeruli, proteinuria and eGFR, with a consistent dose-response across tertiles (Figure 2, log-rank p = 0.005) and a coherent mechanistic account. Cohorts of immunosuppression-naive membranous nephropathy patients with triple-assay PLA2R1 measurement and five-year follow-up to hard endpoints are scarce, and desk-rejecting one over reconcilable numerical errors and a missing immunostain arguably discards more information than it protects. An alternative disposition would be to return the manuscript for a major pre-review revision — immunohistochemical confirmation in a subset, corrected estimator, penalised model with treatment adjustment, corrected tables — with an explicit statement that review would follow if those are delivered.

I do not adopt that course, for one reason: podocyte nuclear size is reported as independently predictive alongside podocyte density. Under the artifact hypothesis these two findings are the same finding, and podocytes are the largest and most irregularly shaped of the four nuclear populations, which breaks the symmetry the counterargument depends on. Until an antigen-specific measurement separates them, the specificity argument is not decisive.

---

*Word count: Sections 1–4, condensed to ~400 words per editorial request.*

072954
# Editorial Report — Manuscript 072954T
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

**Reject.** Two of the weaknesses above are, on reflection, close to fundamental rather than merely fixable in revision.

First, the benchmark's real-world validity claim is undermined by its own construction: 100 candidate families were screened down to 90 specifically for containing a "meaningful KR–US difference," with 10 excluded for being "too subtle." This is a deliberately conflict-enriched sample — the authors disclose this themselves — which means CSS cannot support any inference about how often jurisdictional-adaptation failure occurs in ordinary clinical use, only that it occurs when adversarially curated for. The Discussion does not adequately caveat this; it argues jurisdictional adaptation "should be treated as a core dimension of clinical reliability" as a general claim, which the sampling design cannot license.

Second, the paper's single most attention-grabbing number — GPT-5.5's CSS collapsing to 15.8% under jurisdiction-only framing and recovering to 61–64% under three other framings — rests on single-run, temperature-0, single-snapshot generation with no repeated stochastic sampling. Frontier closed-source APIs are known to exhibit run-to-run variability even at temperature 0 (server-side batching, silent snapshot updates). Without a replicate-run variance estimate specifically on this headline contrast, there is no way to know whether the reported 48-point swing is a stable capability finding or partly an artifact of one decoding pass on one day against one model snapshot — and the authors' own limitations section concedes "rapidly changing model snapshots...constrain temporal reproducibility" without addressing this for their central claim.

Combined with the uncited, acronym-colliding prior art and the absence of any tested mitigation despite an extensive Discussion of retrieval-augmented solutions, these are not reviewer-fixable footnotes — they bear on whether the headline claim is measured at the current evidentiary standard. I would not send this forward as-is; a resubmission with replicate-run variance on the P1–P4 contrasts and an explicit, quantified statement of enrichment bias (not just a Limitations mention) would be reviewable.

---

## 5. Suggested Reviewer Expertise

Reviewers should cover: (1) LLM evaluation methodology, specifically counterfactual/interventional benchmark design and rank-disagreement diagnostics between coverage-based and behavioral metrics; (2) prompt-sensitivity and mechanistic interpretability of instruction-following versus identity-cue processing in frontier LLMs; (3) multilingual and cross-jurisdictional NLP benchmark construction (Korean-language medical or legal domains); (4) family medicine or general internal medicine with working knowledge of both Korean and US guideline-development processes (KDA, USPSTF, ACC/AHA); and (5) biostatistics with expertise in cluster-bootstrap inference for paired diagnostic-accuracy designs and stochastic-decoding variance in LLM benchmarking. Split: roughly 70% technical, 30% clinical.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Counterfactual clinical LLM evaluation is an active 2025–2026 wave, not a novel category invented by this manuscript. MedEinst (Chen et al., ACL 2026) pairs DDXPlus-derived vignettes to test diagnostic fixation under discriminative-feature perturbation; MamaBench (Adewuyi et al., arXiv:2607.14385, correctly cited as ref. 21) applies the same paired-perturbation logic to maternal/paediatric diagnosis via its Bias Trap Rate; and Turk's Causal Sensitivity Score (arXiv:2605.30590, uncited) applies interventional scoring to oncology tumor-board recommendations, explicitly demonstrating — as this manuscript does — that coverage-based accuracy and counterfactual responsiveness rank models in nearly opposite orders. A parallel strand addresses geography directly: a Kenyan primary-care benchmarking paper (arXiv:2507.14615) proposes "Geographic-Contextual Adaptability" as an explicit metric, and XL-SafetyBench (arXiv:2605.05662) applies country-grounded paired evaluation to safety rather than clinical concordance.

Against this landscape, GeoMedBench's distinct contribution is the two-country, same-language, guideline-conflict-family design with mandatory joint label-and-action correctness — a stricter and more clinically specific instrument than the geographic-adaptability or safety-focused alternatives. It does not, however, engage with the CSS-acronym collision or with MedEinst's structurally identical paired-seed logic, and any resubmission should situate the paper explicitly within this cluster rather than treating jurisdictional adaptation as an unaddressed gap in the literature.

## 7. Suggested Reviewers (by expertise area)

- **Counterfactual/interventional LLM evaluation methodology:** Matt Turk (Protege Data Lab); authors of MedEinst (W. Chen, G. Huang — ACL 2026); Thanni Adewuyi (HelpMum Africa, MamaBench).
- **Prompt-sensitivity / mechanistic interpretability:** researchers publishing on identity-cue and sociodemographic-shortcut effects in clinical LLMs (e.g., groups extending Omar et al., *Nat. Med.* 2025); no verifiable junior candidate with a directly comparable mechanistic-ablation publication could be confirmed in the time available — flagged rather than defaulting to senior faculty.
- **Korean/multilingual cross-jurisdictional benchmark construction:** Wonseok Hwang (Assistant Professor, University of Seoul; KBL Korean legal-LLM benchmark, directly comparable paired-jurisdiction design methodology, legal rather than clinical domain).
- **Clinical guideline concordance (KR/US primary care or oncology):** a junior faculty member in family medicine or preventive oncology with joint KDA/USPSTF or NCCN/Korean-guideline authorship experience; specific verifiable candidate not identified — flagged for editorial follow-up rather than defaulted to a senior author.
- **Biostatistics (paired diagnostic accuracy, cluster bootstrap, decoding variance):** a statistician with published family-cluster or hierarchical bootstrap work in diagnostic-test-accuracy meta-analysis.

---

## Editorial Integrity Alert (for handling editor only)

**Numerical consistency:** A full independent recheck of Table 2, Table 3, Figure 4's incorrect-row denominators, and the abstract's summary statistics found no arithmetic inconsistencies — all percentages, CSS counts, and error-composition denominators reconcile exactly against the reported n. This is a positive integrity finding, not a concern.

**Model identity verification:** All eight named models (GPT-5.5, Claude Opus 4.8, Gemini 3.1 Pro, Qwen3.5-Plus, Solar Pro 3, Mistral Large 3, Llama 4 Maverick, MedGemma 27B Text) correspond to real, dated 2026 releases; no fabricated or anachronistic model claims detected.

**Reference formatting anomaly:** References 8, 10, 27, and 28 are missing article titles in the printed list (author names, venue, and pagination only). I independently confirmed ref. 8 (Nakajima, Saito & Nishikawa, *J. Can. Assoc. Gastroenterol.*, gwag024, 2026, DOI 10.1093/jcag/gwag024) is a real, correctly attributed paper. Given the source file is a phone/CamScanner scan, this is most likely an OCR or reference-manager truncation artifact rather than fabrication, but the authors should be asked to submit a clean, machine-readable reference list before any resubmission, since malformed entries cannot be fully verified from a scan alone.

**Author and competing-interest check:** Corresponding author EunKyo Kang has a verifiable, consistent publication record in cancer screening, health informatics, and text mining at the National Cancer Center Korea. No overlap was found between the author list and any cited comparator group (MamaBench, MedEinst, or the uncited Turk CSS paper). Declared funding (National Cancer Centre Korea; Ministry of Trade, Industry & Energy) shows no LLM-vendor funding; no undisclosed competing interest identified.

**Sampling-enrichment disclosure:** The 100→90 family screening for "meaningful KR–US difference" is disclosed in Methods and Limitations, but the magnitude of enrichment (how much CSS would differ under unenriched sampling) is not quantified or bounded anywhere in the manuscript. This is the basis for the Reject decision above, not a concealment — it is fully stated, just under-caveated relative to the paper's general-claim framing in the Discussion and Conclusion.

**Literature-engagement gap (not misconduct):** The omission of Turk (arXiv:2605.30590) and MedEinst (ACL 2026) from the reference list is a scholarly gap flagged in Sections 3/6 above, not an integrity concern — both are 2026 preprints/proceedings that may postdate the authors' literature search cutoff.

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
