# Trackrad202512456
046544
Reduced-montage EEG

### 1. Overall Assessment

This manuscript presents SleepBendr, a transformer-based pediatric sleep staging model produced by fine-tuning the BENDR EEG foundation model on 1,846 recordings from the National Children's Hospital Sleep Databank (NCH). The authors report weighted F1 scores of 0.81, 0.81, and 0.77 on NCH Partition 2, CHAT, and PATS respectively, claiming expert-level performance on a reduced 5-channel EEG montage. The scientific proposition is that foundation-model transfer enables pediatric-specific staging with superior cross-cohort generalization relative to YASA and USleep-1EEG.

The primary concern is contextual priority. Pediatric SleepNet (*SLEEP*, March 2026) was trained on 9,150 PSGs across overlapping NSRR cohorts, validated on the same CHAT and PATS datasets, and includes ICD-10-stratified disease robustness analyses. SleepBendr's novelty claim rests on comparison with models not designed for pediatric populations; this stronger contemporaneous baseline is absent. That gap is not revisable without rerunning comparative analyses.

---

### 2. Strengths

The external validation design is the manuscript's most defensible contribution. SleepBendr was trained exclusively on NCH Partition 1 and evaluated on CHAT and PATS — cohorts absent from its training set but present in YASA's and USleep-1EEG's training data, making the comparison explicitly unfavorable to SleepBendr and strengthening the generalization argument.

Extension to downstream clinical sleep metrics is clinically meaningful. Reporting prediction error for sleep onset (2.84 min), final awakening (3.46 min), WASO (14.38 min), and TST (17.59 min), with variance comparisons via paired permutation tests, moves evaluation beyond classification and toward operationally relevant outputs.

Use of Matthews Correlation Coefficient alongside weighted F1 is appropriate for the class imbalance inherent in PSG data. MCC scores of 0.71–0.75 for SleepBendr versus 0.56–0.68 for YASA and 0.59–0.65 for USleep-1EEG address the risk that F1 improvements are driven by majority-class bias.

---

### 3. Weaknesses

The absent comparison to pediatric SleepNet is a fundamental positioning failure. That model, trained on five times as many PSGs with external validation on the same CHAT and PATS cohorts, directly occupies the same methodological and clinical niche. The claim that SleepBendr provides "a stronger case for generalizable pediatric sleep staging than has previously been available" cannot be evaluated without this baseline.

The channel mismatch between BENDR's required 20-channel input and SleepBendr's 5-channel EEG is resolved by zero-padding 15 channels — a design decision with unstated implications. There is no ablation of whether this structural domain mismatch degrades BENDR's spatial attention patterns, nor justification for preferring BENDR over newer EEG foundation models with sparse-montage pretraining.

The study population derives entirely from NSRR, which over-represents children referred for adenotonsillectomy evaluation. No demographic breakdown by race or ethnicity is provided across the three cohorts, and no differential performance analysis is reported. The claim that SleepBendr enables research in "diverse pediatric populations" is unsupported by validation limited to three clinical trial cohorts from the same repository.

---

### 4. Editorial Decision

**Reject.** Pediatric SleepNet, trained on five times as many PSGs with overlapping external validation cohorts and ICD-10-stratified subgroup analyses, was published before this submission's revision cycle and directly supersedes the novelty claim. Transfer to *npj Digital Medicine* or *SLEEP* could be considered if the authors reframe SleepBendr's contribution narrowly as a reduced-montage, open-source tool with downstream clinical metric validation, and benchmark it against pediatric SleepNet.

---

### 5. Suggested Reviewer Expertise

Reviewers should cover the following areas: transformer-based sequence modeling and foundation model fine-tuning for biomedical time-series, with specific familiarity with EEG contrastive pretraining architectures such as BENDR or SleepFM; automated sleep staging methodology, including evaluation design for cross-cohort generalization, epoch-level versus subject-level data partitioning, and clinical metric derivation from hypnograms; pediatric polysomnography and AASM pediatric sleep scoring guidelines, including the neurophysiological basis of developmental differences in sleep architecture across infancy through adolescence; clinical pediatric sleep medicine, with experience in interpreting TST, WASO, and sleep onset in the context of sleep-disordered breathing trials; and AI clinical translation methodology, including subgroup fairness analysis and reproducibility requirements for open-source clinical tools.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

Automated pediatric sleep staging has advanced substantially since 2023, and the manuscript's literature review does not reflect the current state of the field with adequate fidelity. The most direct concurrent work is pediatric SleepNet (Shook et al., *SLEEP*, Advance Access March 2026), which trained a U-Net encoder-decoder on 9,150 PSGs stratified across three developmental age groups, validated externally on CHAT and PATS, and reported disease-stratified performance across seven ICD-10 categories — a level of clinical granularity absent from SleepBendr. PedSleepMAE (Pandey, Saeed, and Lee, IEEE EMBS BHI 2024) demonstrated masked autoencoder pretraining on multimodal pediatric PSG signals using NCH as backbone, representing a directly competing foundation-model approach. On the EEG foundation model side, SleepFM (Thapa et al., ICML 2024) established multimodal representation learning across EEG, ECG, and respiratory signals for sleep staging, and BiTimeCrossNet (arXiv:2602.02769, 2026) applied time-aware self-supervised learning specifically to pediatric NCH and CHAT data. The broader EEG foundation model landscape has also moved well beyond BENDR: REVE (Ouahidi et al., arXiv:2510.21585, 2025) pretrained on 25,000 subjects, offering a richer pretraining corpus that the authors do not engage with. Vaquerizo-Villar et al. (*Computers in Biology and Medicine*, 2023) published an explainable deep-learning model for sleep staging in pediatric sleep apnea using CHAT with Grad-CAM attribution, raising an interpretability bar that SleepBendr does not address. SleepBendr's use of BENDR — pretrained on 10,874 mostly adult patients from Temple University Hospital, collected 2000–2013 — appears underspecified relative to these alternatives, and the manuscript does not justify this architectural choice in light of newer EEG foundation models with larger and more developmentally relevant pretraining corpora.

---

### 7. Suggested Reviewer Names

**Transformer-based EEG modeling and foundation model transfer:**
Demetres Kostas (McGill University / Mila), Huy Phan (Queen Mary University of London), Stanislas Chambon (Dreem / Beacon Biosignals), Maarten De Vos (KU Leuven)

**Automated sleep staging and cross-cohort generalization:**
Mathieu Perslev (University of Copenhagen), Raphael Vallat (University of California Berkeley), Haoqi Sun (Massachusetts General Hospital / Harvard), Andreas Brink-Kjaer (Technical University of Denmark)

**Pediatric polysomnography and developmental sleep neurophysiology:**
Ilan Dinstein should be recused as co-author. Suggested: Rosemary Horne (Monash University), Carole Marcus (Children's Hospital of Philadelphia), Suresh Kotagal (Mayo Clinic), Louise O'Brien (University of Michigan)

**Clinical pediatric sleep medicine and adenotonsillectomy trials:**
Susan Redline (Brigham and Women's Hospital / Harvard), Raouf Amin (Cincinnati Children's Hospital), Leila Kheirandish-Gozal (University of Missouri)

---

### Further Literature

**1. Shook et al. (2026) — Pediatric SleepNet**
Shook, B., Turner, A., Chen, J., Wiliński, M., Goswami, M., Elmer, J., & Dubrawski, A. "Pediatric SleepNet: A Deep Learning Network for Reliable Pediatric Sleep Staging Across Developmental Stages." *SLEEP*, Advance Access, March 2026. DOI: 10.1093/sleep/zsag064.
*The most direct competitive work. Trains a U-Net encoder-decoder on 9,150 pediatric PSGs, stratified by three age groups including infants under 6 months. External validation on CHAT and PATS. Disease-stratified performance reported across seven ICD-10 categories. Uses 9-channel EEG/EOG/EMG input. Directly supersedes SleepBendr's novelty claim on cross-cohort generalization and age-stratified robustness.*

**2. Thapa et al. (2024) — SleepFM**
Thapa, R., He, B., Kjær, M.R., Moore, H., Ganjoo, G., Mignot, E., & Zou, J. "SleepFM: Multi-Modal Representation Learning for Sleep Across Brain Activity, ECG and Respiratory Signals." *Proceedings of the 41st International Conference on Machine Learning (ICML)*, JMLR.org, 2024.
*Establishes multimodal EEG/ECG/respiratory foundation-model pretraining for sleep staging. Directly relevant to SleepBendr's core methodological claim that foundation-model transfer improves cross-cohort generalization; SleepFM operates at a broader multimodal scope and on larger training corpora. SleepBendr's decision to anchor on the 2021 BENDR model rather than engaging with SleepFM is not justified.*

**3. Pandey, Saeed & Lee (2024) — PedSleepMAE**
Pandey, S.R., Saeed, A., & Lee, H. "PedSleepMAE: Generative Model for Multimodal Pediatric Sleep Signals." *IEEE EMBS International Conference on Biomedical and Health Informatics (BHI)*, pp. 1–8. IEEE, 2024.
*Applies masked autoencoder pretraining to multimodal pediatric PSG signals from the NCH dataset. A directly competing foundation-model approach to the same problem on the same primary dataset. SleepBendr's Discussion characterizes PedSleepMAE as limited to a single dataset without cross-cohort validation, but does not include it as a quantitative benchmark, which weakens the comparative framing.*

**4. Vaquerizo-Villar et al. (2023) — Explainable pediatric sleep staging**
Vaquerizo-Villar, F., Gutiérrez-Tobal, G.C., Calvo, E., et al. "An Explainable Deep-Learning Model to Stage Sleep States in Children and Propose Novel EEG-Related Patterns in Sleep Apnea." *Computers in Biology and Medicine*, 165, 107419, 2023. DOI: 10.1016/j.compbiomed.2023.107419.
*Develops a Grad-CAM-attributed CNN for sleep staging in pediatric OSA using single-channel EEG from CHAT. Relevant on two counts: it demonstrates competitive performance on single-channel input — challenging SleepBendr's implicit argument that 5 channels are necessary — and raises an interpretability standard (transformer attention map visualization) that SleepBendr cites only as a future direction.*

**5. Van Der Aar et al. (2024) — Reduced-montage transfer learning**
Van Der Aar, J.F., Van Den Ende, D.A., Fonseca, P., Van Meulen, F.B., Overeem, S., Van Gilst, M.M., & Peri, E. "Deep Transfer Learning for Automated Single-Lead EEG Sleep Staging with Channel and Population Mismatches." *Frontiers in Physiology*, 2024. DOI: 10.3389/fphys.2023.1287342.
*Directly addresses the montage-mismatch problem in wearable EEG sleep staging via deep transfer learning fine-tuning, with specific analysis of how channel reduction degrades performance and what fine-tuning strategies partially recover it. Highly relevant to SleepBendr's zero-padding approach for handling BENDR's 20-channel input requirement — a methodological choice this paper rigorously examines and SleepBendr does not.*

**6. Bechny, Fiorillo & van der Meer (2025) — Algorithmic bias in sleep scoring**
Bechny, M., Fiorillo, L., & van der Meer, J. "Beyond Accuracy: A Framework for Evaluating Algorithmic Bias and Performance, Applied to Automated Sleep Scoring." *Scientific Reports*, 15, Article 1–18, 2025. DOI: 10.1038/s41598-025-06019-4.
*Provides a formal framework for evaluating demographic and algorithmic bias in automated sleep staging, explicitly applied to YASA and USleep. Directly relevant to the absence of race/ethnicity subgroup analyses in SleepBendr's evaluation design. SleepBendr cites this paper in the context of adult-model failure on pediatric data but does not apply its bias evaluation framework to its own model.*


046240 Acetabular Development
**1. Overall Assessment**

This manuscript presents a foundation model–guided single-cell framework to localize early developmental deviations in developmental dysplasia of the hip (DDH) within a human fetal acetabular chondrogenic reference. The central claim is that DDH-associated chondrocytes preferentially displace toward early and transitional fetal-like states within a continuous developmental manifold rather than forming a novel pathological cell population. Geneformer V2 (104M parameters) is fine-tuned on five high-confidence chondrogenic states and applied to generate predicted labels, class probabilities, Shannon entropy, and latent embeddings for joint interpretation of DDH cells. The held-out macro-F1 of 0.8843 supports methodological soundness, and in silico perturbation analysis generates a falsifiable hypothesis around HTRA1 as a disease-context candidate regulator.

The conceptual framing is genuinely interesting, and the use of entropy-based uncertainty as a biologically interpretable dimension is a meaningful contribution. However, two structural problems limit suitability at this tier. The DDH cohort comprises only three patients, insufficient to support the inter-patient composition analyses and developmental-state redistribution claims made throughout. No independent external validation is performed; all DDH conclusions are drawn from the same three patients whose data informed the analytical framework design.

**2. Strengths**

The construction of a human fetal acetabular chondrogenic reference atlas spanning gestational weeks 9–21 is the paper's most substantive contribution. This anatomically specific, temporally extended dataset fills a genuine gap not covered by existing skeletal atlases including Zhang et al. (*Nature*, 2024) and To et al. (*Nature*, 2024), neither of which profiles acetabular cartilage beyond 11 post-conception weeks.

The integration of predicted developmental-state labels, maximum class probability, and Shannon entropy into a unified uncertainty framework is well-considered. Entropy concentration near the ECP/TSC interface is biologically interpretable as a lineage bottleneck rather than annotation failure.

The background-stratified in silico perturbation design distinguishes healthy-state gene dependency from disease-context perturbation sensitivity within a shared embedding space, producing falsifiable predictions around HTRA1 and COL2A1 that are appropriately caveated as model-inferred.

**3. Weaknesses**

The DDH cohort of three patients is the paper's most consequential limitation. Patient-level composition analyses show dramatically divergent state distributions across DDH1, DDH2, and DDH3, making it impossible to distinguish disease-relevant signal from inter-patient variability. A minimum of 8–10 patients would be required to stabilise these composition estimates.

No external validation is performed against an independent DDH cohort. Directly competing analyses — including a 2025 Osteoarthritis and Cartilage integrative scRNA-seq/scATAC-seq DDH study and an Advanced Science 2025 acetabular labrum spatial transcriptomics study — are neither cited nor engaged with.

The in silico perturbation is Geneformer token deletion, not gene knockout. Despite appropriate caveats, the framing of HTRA1 as exhibiting "rescue-like tendencies" overstates what token ablation can support without chondrocyte cell-line validation. The five-gene perturbation panel excludes known DDH-associated loci (COL11A2, GDF5, LRP1) without justification.

**4. Editorial Decision**

Reject. The three-patient DDH cohort is a structural limitation that cannot be resolved by revision — it requires new sample collection and constitutes a new study. The absence of engagement with directly competing 2025 DDH single-cell analyses and the lack of comparative benchmarking against scGPT or scFoundation on this developmental dataset further weaken the manuscript's positioning. Transfer to *npj Digital Medicine* or *Communications Biology* may be appropriate once the disease cohort is adequately powered.

---

**5. Suggested Reviewer Expertise**

*(Preserved verbatim)*

The manuscript requires reviewers with expertise in: (1) transformer-based single-cell foundation models, specifically Geneformer fine-tuning and latent-space interpretation for developmental contexts; (2) pseudotime and trajectory inference methods (Monocle3, PAGA, DPT) applied to embryonic or fetal tissue datasets; (3) human fetal musculoskeletal development, particularly chondrogenic lineage specification during the second trimester; (4) computational cartilage biology and single-cell transcriptomics of connective tissue disorders, including osteoarthritis and congenital joint malformations; and (5) pediatric orthopedic surgery with clinical expertise in DDH pathogenesis, staging, and natural history.

---

**6. State-of-the-Art Literature Review (Past 3 Years)**

*(Preserved verbatim)*

The single-cell atlas landscape for human embryonic and fetal skeletal development has advanced substantially in the past two years, providing direct context for evaluating this manuscript's claims. Zhang et al. (*Nature*, 2024) generated a 125,955-cell atlas of human embryonic limb development across first trimester timepoints, resolving chondrogenic, osteogenic, and mesenchymal lineages with spatial transcriptomics integration. To et al. (*Nature*, 2024) applied paired snRNA-seq and snATAC-seq to ~336,000 nuclei from human embryonic joint and cranium (5–11 PCW), characterizing region-specific chondroprogenitor trajectories and osteogenic regulatory networks. Feng et al. (*Nature Communications*, 2025) performed high-resolution spatial transcriptomics of craniofacial development, resolving spatiotemporal cell fate determination relevant to joint morphogenesis. These three works collectively define the current benchmark for fetal skeletal atlas construction. The present manuscript's acetabular-specific fetal reference (9–21 gestational weeks) extends beyond the embryonic window covered by these atlases and is therefore genuinely complementary, not redundant.

In the DDH single-cell space, a 2025 Osteoarthritis and Cartilage study integrated scRNA-seq and scATAC-seq to identify seven molecularly distinct chondrocyte populations in DDH acetabular tissue and characterized their epigenetic regulatory elements. A concurrent study in Advanced Science (2025) applied single-cell and spatial transcriptomics to the acetabular labrum, identifying aberrant fibrocartilage stem/progenitor proliferation and the midkine (MDK) signaling pathway as a functionally validated therapeutic target. The present manuscript does not cite or engage with either of these directly competing analyses, which is a critical omission. On the foundation model side, the scEval benchmarking framework (Advanced Science, 2026) established that scGPT and Geneformer remain among the top-performing single-cell foundation models across eight downstream tasks, but also demonstrated that zero-shot evaluation reveals substantial limitations in generalisation. The manuscript's exclusive reliance on Geneformer without comparison to scGPT (Cui et al., *Nature Methods*, 2024) or scFoundation (Hao et al., 2024) on this specific developmental dataset leaves the added value of Geneformer over alternatives unsubstantiated.

---

**7. Suggested Reviewer Names**

*(Preserved verbatim)*

**Transformer-based single-cell foundation models:** Christina Theodoris (Gladstone Institutes, UCSF); Bo Wang (University of Toronto / Vector Institute); Fabian Theis (Helmholtz Munich, Technical University of Munich).

**Fetal skeletal development and chondrogenic lineage:** Sarah Teichmann (Wellcome Sanger Institute / University of Cambridge); Aris Economides (Regeneron Genetics Center).

**Pediatric orthopedics / DDH clinical expertise:** Pablo Castañeda (NYU Langone Health); Reinhard Berner (University Hospital Dresden — pediatric musculoskeletal disease).

---

**Further Literature****Further Literature**

The following six papers, published within the past three years, share direct methodological or thematic scope with the present manuscript and constitute the primary comparative literature an informed reviewer would expect to see engaged.

1. **Theodoris CV, Xiao L, Chopra A, et al.** Transfer learning enables predictions in network biology. *Nature*. 2023; 618(7965):616–624. — The foundational Geneformer V1 paper establishing the rank-value encoding, fine-tuning pipeline, and in silico perturbation paradigm that the present manuscript applies to acetabular chondrogenesis. Essential reference for evaluating whether the authors' fine-tuning and token-deletion approach is faithful to the original framework.

2. **Zhang B, He P, Lawrence J, et al.** A human embryonic limb cell atlas resolved in space and time. *Nature*. 2024; 635(8039):668–678. — A 125,955-cell atlas of first-trimester human hindlimb development incorporating spatial transcriptomics and temporal profiling of chondrogenic lineages. Directly relevant as the closest existing reference for fetal human chondrogenesis; notably does not cover the acetabular compartment or extend beyond 11 post-conception weeks, which frames the added value of the present dataset.

3. **To K, Fei L, Pett JP, et al.** A multi-omic atlas of human embryonic skeletal development. *Nature*. 2024; 635(8039):657–667. — Paired snRNA-seq and snATAC-seq of ~336,000 nuclei from human embryonic joint and cranium (5–11 PCW), with in silico perturbation of craniosynostosis-associated genes using trajectory-anchored cell states. The most direct methodological comparator for the in silico perturbation component of the present manuscript.

4. **Lawrence JEG, Woods S, Roberts K, et al.** Single-cell transcriptomics identifies chondrocyte differentiation dynamics in vivo and in vitro. *Developmental Cell*. 2025 Jul 22. — An endochondral ossification atlas constructed from first-trimester embryonic long bones and used as a developmental reference to evaluate the fidelity of in vitro chondrogenesis protocols. Shares the key design principle of using an embryonic scRNA-seq reference to assess cellular state positioning — analogous to the present manuscript's projection of DDH cells onto a fetal chondrogenic reference.

5. **Kalfon J, Samaran J, Peyré G, Cantini L.** scPRINT: pre-training on 50 million cells allows robust gene network predictions. *Nature Communications*. 2025; 16(1):3607. — A single-cell foundation model pre-trained on 50 million cells with competitive zero-shot cell-label prediction and gene network inference, benchmarked against Geneformer V2 and scGPT. Directly relevant to the question of whether Geneformer V2 was the optimal foundation model choice for the fine-tuning approach described in this manuscript.

6. **Yang R, Liu H, Ge M, et al.** Deciphering the Acetabular Labrum's Cellular Atlas: MDK Inhibition as a Novel Therapeutic Method for Developmental Dysplasia of the Hip. *Advanced Science*. 2025. — Integrates single-cell and spatial transcriptomics of the acetabular labrum in DDH, identifies aberrant fibrocartilage stem/progenitor proliferation, and validates MDK/midkine signaling as a therapeutic target through in vivo and in vitro experiments. The most directly competing disease-focused analysis in the same anatomical compartment; its absence from the manuscript's reference list and discussion is a material gap.

045655 suicidal-crisis disclosures"

### 1. Overall Assessment

This manuscript reports a large-scale controlled audit of eight LLMs responding to 200 real Reddit suicidal-crisis posts under 34 sociodemographic identity conditions, generating 655,023 scored outputs across a four-layer pipeline (behavioral regex, Empath lexicon, EPITOME empathy judge, semantic similarity). The central claim is a dissociation between triage equity and response equity: severity classification was demographically invariant, while crisis-resource provision, empathy register, and emotional language shifted systematically by identity. The deepest deficit fell on Middle Eastern-labeled users (CRP OR 0.86, 95% CI 0.82–0.90), nadir at Middle Eastern Muslim women (OR 0.82).

Two concerns are decisive. This is a direct programmatic extension of prior publications by the same group — Omar et al. (*Nat Med* 2025) and Omar et al. (*Nat Health* 2026) — using the same counterfactual vignette paradigm in adjacent clinical domains. The intellectual novelty is real but must be sharply delineated from those antecedents. Second, the Reddit corpus with single-sentence identity injection does not model how identity surfaces in deployed chatbot interactions, and the generalizability argument requires tighter empirical qualification.

---

### 2. Strengths

The crossover within-post design eliminates between-post variance, allowing precise estimation of identity effects. GEE with post as cluster is the correct choice; the finding that model identity explains more CRP variance (Wald χ² 131.6–496.2) than race (21.6–22.8) is a regulatory-grade result unavailable from simpler designs.

The four-layer scoring architecture is the field's most comprehensive to date. The cross-layer divergence — EPITOME judging non-White responses as more empathic while Empath showed less sympathy language (Spearman ρ = −0.80, commercial panel) — is both unexpected and clinically meaningful, identifying a failure mode invisible to any single-instrument audit.

Blinded physician validation (n = 160, κ = 0.84 severity, ρ = 0.78 EPITOME concordance) anchors the automated pipeline to expert clinical judgment in a way prior NLP audits have not achieved.

The five-model open-weights replication panel, spanning US, Chinese, and French laboratories, and the unique direction reversal in Mistral Saba — the only model pretrained on Middle Eastern languages — constitutes convergent cross-architecture evidence of a training-level signal.

---

### 3. Weaknesses

The single-sentence identity injection does not model naturalistic crisis disclosure. Real consumer chatbot interactions involve user-initiated, longitudinally accumulated identity signals absent explicit demographic labels. The authors acknowledge this but do not quantify expected effect-size direction; their own argument that persistent memory amplifies identity signals implies conservative estimates, but this remains speculative.

The multi-turn acceleration finding — Middle Eastern users referred 18% faster (HR 1.18) despite single-turn CRP deficits — is clinically the most alarming result yet receives the least analysis. No content comparison of the referral turn by identity condition is provided, and the premature-disengagement hypothesis is not tested.

Religious disclosure is collapsed into a single category in Figure 5 despite the authors' own data showing Christian and Muslim labeling produce directionally opposite CRP effects. This misrepresents the mechanism and affects the main conclusions.

---

### 4. Editorial Decision

**Send for Review.** The manuscript clears the bar on scale, design rigour, and clinical relevance. Reviewers should adjudicate: (1) whether single-sentence identity injection supports the causal claims about deployed systems; (2) whether the multi-turn acceleration finding can be distinguished from premature disengagement; and (3) whether religious-disclosure collapsing in Figure 5 misrepresents effect directionality. Editors should request explicit confirmation of non-overlap between the scoring infrastructure and corpus used here and those in the prior *Nat Med* 2025 and *Nat Health* 2026 publications from the same group.

---

### 5. Suggested Reviewer Expertise

Reviewers should collectively cover: (1) large-scale counterfactual auditing of LLM outputs, specifically sociodemographic vignette methodology and GEE-based repeated-measures analysis for clustered text outputs; (2) computational psycholinguistics and validated NLP measurement instruments for mental health support quality, including the EPITOME framework and Empath lexicon; (3) LLM-as-judge evaluation design, including cross-architectural judge concordance, demographic conditioning of judge models, and known failure modes of automated empathy scoring; (4) crisis counseling and suicide intervention standards, specifically Safe Messaging guidelines, Columbia Suicide Severity Rating Scale administration, and clinical standards for digital mental health handoff; and (5) health equity research methodology, particularly intersectional analysis and the epidemiology of mental health service access in Middle Eastern, Muslim, and LGBTQ+ communities in the United States.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

The literature on LLM demographic bias in clinical contexts has grown rapidly since 2023, but the suicidal-crisis sub-domain has lagged behind. The most methodologically proximate works are the counterfactual vignette audits of emergency triage and pain management by Omar et al. (*Nat Med* 2025; doi:10.1038/s41591-025-03626-6) and Omar et al. (*Nat Health* 2026; doi:10.1038/s44360-025-00017-6), which established that nine to ten LLMs shift structured clinical recommendations based on race, housing status, and LGBTQ+ identity across 1.7 million outputs. Gabriel et al. (EMNLP Findings 2024; arXiv:2405.12021) showed that GPT-4 responses to peer mental health support posts on Reddit exhibited inequitable empathy across inferred racial subgroups, representing the closest prior study in the open-ended crisis-response domain, though it assessed inferred rather than injected identity and did not stratify by crisis severity or use validated clinical instruments. McBain et al. (*JMIR* 2025; doi:10.2196/67891) evaluated ChatGPT-4o, Claude 3.5 Sonnet, and Gemini 1.5 Pro on the SIRI-2 suicidal ideation response inventory, finding upward bias in appropriateness ratings but not testing demographic conditioning. Abutaleb et al. (*npj Digital Medicine* 2025; doi:10.1038/s41746-025-01746-4) qualitatively assessed racial bias in psychiatric diagnosis and treatment across four LLMs, finding inferior treatment recommendations under explicit racial labeling — consistent with the CRP deficit here but lacking quantitative rigour. The HALF framework (arXiv:2510.12217) introduced harm-aware LLM fairness evaluation across clinical tasks including suicide-risk detection, applying demographic-variant generation across gender, ethnicity, and age, but focused on classification rather than open-ended response generation. Against this landscape, the present manuscript is the first to apply a four-layer measurement pipeline to open-ended crisis responses at this scale, with physician validation and multi-turn follow-up. Its primary gap is the absence of Latin American or South Asian identity conditions and the absence of any purpose-built crisis chatbot comparator.

---

### 7. Further Literature

The following five papers from the past three years share the closest thematic and methodological scope with this manuscript:

**1. Omar M, Soffer S, Agbareia R, et al. Sociodemographic biases in medical decision making by large language models. *Nature Medicine*. 2025;31(6):1873–1881. doi:10.1038/s41591-025-03626-6**
The direct methodological antecedent. Nine LLMs evaluated on 1,000 emergency-department vignettes across 32 sociodemographic conditions (1.7 million outputs), using the same counterfactual injection paradigm. Established that Black, unhoused, and LGBTQ+ identity labels shift triage and mental health referral recommendations. Reviewers will compare the present manuscript against this work directly.

**2. Omar M, Soffer S, Agbareia R, et al. Socio-demographic gaps in pain management guided by large language models. *Nature Health*. 2026;1(2):216–225. doi:10.1038/s44360-025-00017-6**
Extends the same vignette paradigm to 1,000 acute-pain cases across 34 sociodemographic features and ten LLMs. Directly overlapping authorship, taxonomy, and statistical infrastructure with the present submission. Editors should require a formal overlap declaration.

**3. Gabriel S, Misra V, Shah N, et al. Can AI Relate: Testing Large Language Model Response for Mental Health Support. *Findings of EMNLP 2024*. arXiv:2405.12021**
Evaluated GPT-4 on 12,513 Reddit mental health posts across inferred racial subgroups using the EPITOME framework, finding inequitable empathy provision. The closest prior study in the open-ended mental health response domain; the present manuscript's injected-identity design and crisis-specific corpus represent a direct methodological advance over this work.

**4. McBain RK, Cantor JH, Zhang LA, et al. Competency of large language models in evaluating appropriate responses to suicidal ideation: comparative study. *Journal of Medical Internet Research*. 2025;27:e67891. doi:10.2196/e67891**
Assessed ChatGPT-4o, Claude 3.5 Sonnet, and Gemini 1.5 Pro on 24 SIRI-2 scenarios for suicidal ideation response appropriateness. Found model-level variation but did not test demographic conditioning. Establishes the baseline competency literature against which identity-conditional effects in the present manuscript should be interpreted.

**5. Abutaleb A, Levartovsky A, Agbareia R, et al. Racial bias in AI-mediated psychiatric diagnosis and treatment: a qualitative comparison of four large language models. *npj Digital Medicine*. 2025. doi:10.1038/s41746-025-01746-4**
Qualitative evaluation of Claude, ChatGPT, Gemini, and a LLaMA 3 variant on ten psychiatric cases under race-neutral, race-implied, and race-explicit conditions. Found inferior treatment recommendations under explicit racial labeling with minimal diagnostic bias — directionally consistent with the triage-response dissociation reported here, but limited by qualitative design and small case set.

**6. Pichowicz W, Kotas M, Piotrowski P. Performance of mental health chatbot agents in detecting and managing suicidal ideation. *Scientific Reports*. 2025;15(1):31652. doi:10.1038/s41598-025-17242-4**
Benchmarked conversational chatbot agents on suicidal ideation detection and management, finding moderate accuracy with substantial inter-agent variability. Provides a performance baseline for purpose-built crisis agents against which general-purpose LLM behavior in the present manuscript can be contextualized; notably absent from the manuscript's introduction despite sharing the core clinical use case.

---

### 8. Suggested Reviewer Names

**Counterfactual LLM auditing and GEE methods:** Ziad Obermeyer (UC Berkeley School of Public Health), Irene Chen (Cornell Tech/Weill Cornell Medicine), Emma Pierson (Cornell Tech).

**Computational psycholinguistics and NLP mental health measurement:** Rada Mihalcea (University of Michigan), Tim Althoff (University of Washington), Lyle Ungar (University of Pennsylvania).

**LLM-as-judge evaluation and empathy scoring:** Diyi Yang (Stanford University), Saadia Gabriel (MIT/UCLA).

**Crisis counseling and suicide intervention standards:** Matthew Nock (Harvard University), Craig Bryan (Ohio State University).

**Health equity and Middle Eastern/Muslim mental health access:** Mariam Abou Hijleh (Columbia University Mailman School of Public Health), Rima Afifi (University of Iowa College of Public Health).

045522 and Bayesian Analysis

### 1. Overall Assessment

This manuscript introduces KM-GPT-DCH, an algorithm combining KinderMiner co-occurrence retrieval, RAG with OpenAI o3, and a Bayesian credible interval framework to compare pairs of competing biomedical hypotheses using PubMed literature. The central claim is that pairwise comparative evaluation outperforms single-hypothesis RAG tools and conversational LLMs, and that temporal windowing enables historically accurate reconstruction of scientific consensus — validated 5 to 12 years ahead of community acceptance in five resolved cases.

The principal concern is that the validation set is a convenience selection of textbook cases where one hypothesis eventually dominated PubMed by a wide margin. This selection bias significantly weakens the inference drawn for the twenty currently unresolved hypothesis pairs, where no ground truth exists.

---

### 2. Strengths

The temporal filtering design is the strongest technical contribution. Restricting abstract retrieval to discrete non-overlapping windows — and demonstrating that scores reflect only period-available evidence, including HSV-favoring outputs in 1975–1982 despite the LLM's parametric knowledge of the HPV answer — provides a genuine, reproducible mitigation of parametric memory leakage.

The pairwise comparative framing addresses a documented failure mode. The ablation from KM-GPT to KM-GPT-DCH on the peptic ulcer case — where non-comparative scoring yields overlapping, uninformative results while direct comparison resolves clearly for bacterial infection — substantiates the architectural choice empirically rather than by assertion.

The Bayesian credible interval derived from beta distribution fitting across 10 stratified resampling iterations adds interpretable uncertainty quantification applicable to black-box frontier LLMs without requiring access to log-probabilities or hidden-layer activations.

---

### 3. Weaknesses

The historical validation set systematically selects clean-resolution controversies. The authors do not quantify the PubMed abstract volume imbalance between the winning and losing hypotheses at each resolution date, making it impossible to distinguish genuine evidence superiority from publication volume bias in co-occurrence retrieval.

The conversational LLM comparison is a strawman. Testing chat interfaces under temporal filtering — a task for which they have no mechanism — and reporting 15–25% citation accuracy does not constitute a rigorous competitive baseline. OpenScholar and SPECTER2-based retrieval-augmented claim verification pipelines are the relevant comparators and are absent.

Term selection for KinderMiner co-occurrence is user-specified and uncontrolled. The magnitude of term-sensitivity on scoring outcomes is not characterized, meaning the reported credible intervals underestimate total system uncertainty. This is particularly damaging for the research prioritization use case.

---

### 4. Editorial Decision

**Transfer to npj Digital Medicine or JAMIA.** KM-GPT-DCH is technically coherent and the temporal filtering plus Bayesian credible interval design constitutes a genuine incremental advance over SKiM-GPT. However, the validation framework is insufficient for *Nature Communications*: the five historical cases are selected for cleanness, the strongest competitive baselines are absent, and term-selection sensitivity — the primary operational parameter — is uncharacterized. These are not addressable by supplementary experiments on the current dataset; they require redesigned validation.

---

### 5. Suggested Reviewer Expertise

Reviewers should include expertise in: (1) co-occurrence modeling and knowledge graph construction over biomedical corpora, specifically PubMed-scale literature mining and KinderMiner or similar term-co-occurrence architectures; (2) retrieval-augmented generation for scientific claim verification, including dense and sparse retrieval over biomedical text, SPECTER/BM25 pipelines, and RAG evaluation methodology; (3) Bayesian statistical modeling, specifically beta-binomial model specification, credible interval estimation, and prior sensitivity analysis in the context of iterative resampling; (4) biomedical NLP evaluation methodology, including temporal data leakage, benchmark construction, and comparison against appropriate baselines for evidence synthesis tasks; and (5) philosophy of science or evidence-based medicine, with focus on hypothesis adjudication, systematic review methodology, and the epistemology of scientific consensus formation.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

The automated biomedical hypothesis evaluation landscape has expanded substantially since 2023. OpenScholar (Asai et al., *arXiv:2312.07559*, 2023) demonstrated that retrieval over a dedicated scientific corpus with attribution-grounded generation substantially reduces hallucination in literature-based scientific question answering. Liu et al. (*JAMIA Open*, 2024; doi:10.1093/jamiaopen/ooae021) applied RAG-based claim verification directly to PubMed-derived statements and showed meaningful improvements in citation accuracy over direct LLM generation. In the hypothesis generation literature, Qi et al. (*First Conference on Language Modeling*, 2024) benchmarked frontier LLMs as hypothesis generators and established that factual grounding remains the dominant failure mode, consistent with the evidence KM-GPT-DCH marshals against conversational systems. The broader survey by Ren et al. (*arXiv:2503.24047*, 2025) maps the emerging landscape of LLM-based scientific agents and identifies pairwise comparative evaluation as underexplored relative to single-hypothesis or summary-based tasks. Against this landscape, KM-GPT-DCH is well-motivated: the pairwise DCH extension specifically addresses the score-shrinkage failure mode identified across multiple evaluation contexts, and temporal windowing addresses parametric memory leakage that remains unresolved in most RAG architectures. However, the manuscript does not engage with OpenScholar or MEGA-RAG (Frontiers Public Health, 2025), both of which are architecturally relevant comparators. The claim that no tool exists for pairwise hypothesis comparison is defensible; the claim that conversational LLMs represent the appropriate null model is not supported by the current state of the art. Additionally, the 2024 JMIR scoping review on AI tools for evidence synthesis (Hair et al. consortium, JMIR 2026; doi:10.2196/81597) documents that over 220 tools exist for literature screening, extraction, and synthesis automation — a landscape the manuscript substantially undercites, which weakens the positioning of KM-GPT-DCH relative to tools with overlapping functionality.

---

### 7. Suggested Reviewer Names

**Co-occurrence modeling and biomedical literature mining:** Hagit Shatkay (University of Delaware), Graciela Gonzalez-Hernandez (University of Pennsylvania), Chengxiang Zhai (University of Illinois Urbana-Champaign)

**RAG and scientific claim verification:** Sewon Min (University of Washington / Allen Institute for AI), Iz Beltagy (Allen Institute for AI), Byron Wallace (Northeastern University)

**Bayesian statistical methods:** Andrew Gelman (Columbia University), Frank Harrell (Vanderbilt University), Maarten van Smeden (Utrecht University Medical Center)

**Evidence-based medicine and systematic review methodology:** Julian Higgins (University of Bristol), Kay Dickersin (Johns Hopkins Bloomberg School of Public Health), Larissa Shamseer (Ottawa Hospital Research Institute)

---

### Further Literature

The following six papers from 2023–2026 share overlapping scope with KM-GPT-DCH across the dimensions of RAG-based biomedical evidence synthesis, temporal literature evaluation, and pairwise or comparative hypothesis assessment.

**1. Asai, A. et al. "OpenScholar: Synthesizing Scientific Literature with Retrieval-Augmented LMs." *arXiv:2312.07559* (2023).**
Introduces a retrieval-augmented system over a 45-million-paper scientific corpus that performs attribution-grounded synthesis of scientific literature. Directly comparable to KM-GPT-DCH in its RAG architecture and claim-to-literature linkage design; represents the strongest absent baseline for citation accuracy evaluation.

**2. Liu, H. et al. "Retrieval Augmented Scientific Claim Verification." *JAMIA Open*, 7(1), ooae021 (2024). doi:10.1093/jamiaopen/ooae021.**
Applies RAG pipelines to verify biomedical claims against PubMed-sourced evidence and benchmarks citation accuracy and factual precision. Methodologically adjacent to KM-GPT-DCH's abstract-grounded scoring; provides a quantitative standard against which the 100% citation accuracy claim should be independently evaluated.

**3. Qi, B. et al. "Large Language Models as Biomedical Hypothesis Generators: A Comprehensive Evaluation." *First Conference on Language Modeling* (2024).**
Benchmarks frontier LLMs including GPT-4 as hypothesis generators across multiple biomedical domains and characterizes factual grounding as the primary failure mode. Contextualizes KM-GPT-DCH's motivation for structured, literature-constrained scoring over free-form LLM adjudication.

**4. Ren, S. et al. "Towards Scientific Intelligence: A Survey of LLM-based Scientific Agents." *arXiv:2503.24047* (2025).**
Comprehensive survey of LLM agent architectures for scientific discovery, covering hypothesis generation, evidence retrieval, and multi-agent evaluation. Identifies pairwise comparative hypothesis evaluation as an underexplored capability gap, directly validating the DCH extension's positioning but also situating it within a rapidly maturing agent ecosystem.

**5. Hair, K. et al. (consortium). "Artificial Intelligence Tools for Automating Evidence Synthesis: Scoping Review." *JMIR*, doi:10.2196/81597 (2026).**
Documents over 220 evaluated AI tools for literature screening, data extraction, and evidence synthesis across 222 included studies, the majority published in 2024. Establishes the breadth of the automated evidence synthesis landscape and directly challenges the manuscript's implicit framing that few tools address its core problem; the authors should engage with this review to sharpen their positioning claims.

**6. Liusie, A., Manakul, P. & Gales, M. "LLM Comparative Assessment: Zero-Shot NLG Evaluation through Pairwise Comparisons using Large Language Models." *Proceedings of EACL*, 139–151 (2024).**
Establishes the theoretical and empirical basis for pairwise LLM comparison as yielding higher resolution and better alignment with human judgement than independent scoring — the exact mechanism the DCH extension leverages. The authors cite this line of work obliquely (references 37–39) but do not engage with its specific findings on score calibration, which would strengthen the methodological justification for the DCH design and should be cited directly.

045466 human oversight

---

**Section 1: Overall Assessment**

This manuscript presents the Clinician Model Card (CMC), an interactive, clinician-centered documentation tool for AI-based clinical decision support systems, developed and evaluated through a sequential exploratory mixed-methods design: qualitative interviews with 12 physicians, iterative co-design, and a national survey of 129 physicians across Germany. The central claim is that user-centered documentation design alone is insufficient to achieve meaningful clinician comprehension of AI performance metrics, and that AI literacy constitutes a structural, design-resistant barrier to human oversight.

The work's principal contribution is the empirical demonstration that a well-designed, co-developed transparency artifact fails on comprehension precisely where it matters most — the Validation & Performance section — and that AI literacy (SNAIL-TU, ρ = 0.59, p < 0.001) is the dominant predictor of this failure. That finding challenges the prevailing regulatory assumption embedded in the EU AI Act and FDA guidance that transparency requirements translate to actionable comprehension. The two concerns most influencing this decision are: the survey sample is disproportionately drawn from academic medical centers (81%) using convenience and snowball recruitment, limiting generalizability; and the CMC is evaluated in isolation rather than embedded within a functioning CDSS, meaning the claim that it supports meaningful human oversight cannot be verified from this evidence base.

**Section 2: Strengths**

The methodological traceability chain — from qualitative findings through design requirements to survey items, documented in Supplementary Data 1 — is methodologically rigorous and uncommon in tool development papers. The objective comprehension measurement, using four single-best-answer items revealing near-chance performance on AUROC (42.6%) and PPV (53.5%) interpretation despite mandatory familiarization, makes the literacy-barrier argument empirically concrete. The SNAIL-TU subgroup analysis delivers a specificity distinguishing this paper from generic AI literacy surveys: the gradient from ρ = 0.19 on clinically framed items to ρ = 0.52 on AUROC interpretation maps the literacy gap directly onto the comprehension failure structure.

**Section 3: Weaknesses**

The 81% academic medical center composition and convenience recruitment render the comprehension findings potentially unrepresentative; no sensitivity analyses stratified by setting are provided. Evaluating the prototype outside a functioning CDSS, embedded in a SoSci Survey with a fictive scenario, introduces ecological validity limitations that the conclusions do not sufficiently bound. Multiple Spearman correlations are reported without correction, and ρ = 0.19 is presented as meaningful despite a low effect size. The four-item comprehension scale lacks reliability reporting.

**Section 4: Editorial Decision**

This manuscript is recommended for **transfer to *npj Digital Medicine***. The mixed-methods design is credible, and the core finding — that documentation design cannot close a workforce-level AI literacy gap — is empirically supported and policy-relevant. However, ecological validity constraints, convenience sampling skewed toward academic physicians, and the absence of behavioral or patient-outcome evidence prevent the step-change contribution required at Nature Communications. The competing interests of OF and SG as editors at *npj Digital Medicine* should be managed explicitly under that journal's policy upon transfer.

---

**Section 5: Suggested Reviewer Expertise**

Reviewers should collectively cover: mixed-methods research design in clinical informatics, with specific experience in sequential exploratory tool development studies; measurement of health literacy and numeracy, particularly validated instruments for statistical comprehension in clinical populations including familiarity with SNAIL or comparable scales; human-computer interaction and user-centered design of clinical decision support interfaces, with experience evaluating comprehension under ecological constraints; AI transparency, explainability, and regulatory science at the intersection of the EU AI Act and clinical AI deployment; and clinical implementation of AI-based CDSS in emergency medicine or acute care settings.

---

**Section 6: State-of-the-Art Literature Review**

The clinical AI transparency and model documentation space has seen substantial activity since 2022. Crisan et al.'s 2022 FAccT paper on interactive model cards established the feasibility of augmenting static documentation with interactive affordances for non-expert users, and this manuscript explicitly builds on that lineage. The CHAI Model Card, formally unveiled in October 2024 and published as a *npj Digital Medicine* commentary by Gilbert et al. in February 2025 (npj Digit Med 8:124, DOI: 10.1038/s41746-025-01482-9), represents the closest regulatory-aligned parallel effort; critically, the Gilbert et al. piece raises precisely the same concern about whether model cards can deliver genuine comprehension rather than regulatory compliance. The CMC manuscript provides the first empirical quantification of that failure. Sendak et al.'s 2020 Model Facts Label at *npj Digital Medicine* is the direct predecessor artifact, and the CMC's departure from PDF to interactive digital format is a meaningful architectural evolution. On the AI literacy side, a 2025 JMIR study from Flanders (Chatzichristos et al., JMIR 2025) reported that only 13.8% of surveyed clinicians felt their training adequately prepared them for AI integration, corroborating the structural gap identified here. A 2025 JMIR interview study on barriers to AI-CDSS integration (J Med Internet Res 2025;27:e63377) independently documented comprehension and literacy as primary adoption barriers, providing convergent real-world evidence. The manuscript engages well with the regulatory literature, though it does not cite the ONC's 2025 HTI-5 proposed rule, which explicitly argues there is no publicly available evidence that transparency requirements have produced positive patient care impacts — a finding that directly reinforces this manuscript's thesis and which authors should address. Most documentation studies in this space remain normative rather than empirical; this paper's contribution to closing that gap is clear, though generalizability constraints prevent definitive conclusions about what literacy investment is required to close the identified comprehension deficit.

---

**Section 7: Suggested Reviewers**

For mixed-methods design and health literacy measurement: **Trisha Greenhalgh** (University of Oxford, primary care informatics and qualitative methods), **Rima Rudd** (Harvard T.H. Chan School of Public Health, health literacy measurement), **Enrico Coiera** (Macquarie University, clinical informatics and decision support).

For HCI, clinical AI documentation, and transparency: **Anamaria Crisan** (Tableau Research / UBC, interactive model documentation), **Mark Sendak** (Duke Institute for Health Innovation, Model Facts Label and clinical AI deployment).

For clinical AI deployment and regulatory science: **Xiaoxuan Liu** (University of Birmingham, clinical AI evaluation methodology and DECIDE-AI), **Charlotte Vayena** (ETH Zürich, AI governance and regulatory science in health).

---

**Further Literature**

The following six papers from the past three years share scope with this manuscript across the dimensions of clinical AI documentation, clinician comprehension of AI outputs, AI literacy in the medical workforce, and human oversight of CDSS:

**1.** Gilbert S, Adler R, Holoyad T, Weicken E. "Could transparent model cards with layered accessible information drive trust and safety in health AI?" *npj Digital Medicine* 2025;8:124. DOI: 10.1038/s41746-025-01482-9. — Directly parallel normative argument for layered, accessible model cards in clinical AI; raises the compliance-versus-comprehension tension without empirical resolution, making it a key foil for the CMC paper's empirical contribution.

**2.** Chatzichristos C, et al. "Bridging the AI-Literacy Gap in Health Care: Qualitative Analysis of the Flanders Case Study." *Journal of Medical Internet Research* 2025;27:e76709. — Multi-method study of 134 healthcare professionals finding only 13.8% felt adequately trained for AI integration; provides convergent workforce-level evidence for the literacy gap the CMC paper identifies at the point-of-care.

**3.** Crisan A, Drouhard M, Vig J, Rajani N. "Interactive Model Cards: A Human-Centered Approach to Model Documentation." *Proceedings of the ACM FAccT* 2022:427–439. DOI: 10.1145/3531146.3533108. — Foundational precedent for interactive, non-expert-oriented model documentation; the CMC is a direct clinical translation of this design paradigm, and comprehension findings in the CMC paper extend and partly challenge the optimism of this earlier non-clinical work.

**4.** Steerling E, et al. "Problems and Barriers Related to the Use of AI-Based Clinical Decision Support Systems: Interview Study." *Journal of Medical Internet Research* 2025;27:e63377. DOI: 10.2196/63377. — Qualitative interview study systematizing barriers to AI-CDSS integration across stakeholder groups; comprehension of AI outputs and insufficient AI literacy independently emerge as primary barriers, directly corroborating the CMC paper's structural argument.

**5.** Patil SV, Myers CG, Dai T. "Protecting clinical value judgment in the age of AI." *npj Digital Medicine* 2026. DOI: 10.1038/s41746-026-02561-1. — Argues that adaptive AI systems embedded in clinical workflows operationalize hidden value trade-offs at scale; proposes institution-specific model cards linked to CMS reimbursement incentives as a governance mechanism, situating the CMC's design findings within a broader accountability architecture.

**6.** Stamer T, et al. "Is accuracy enough? Trust and barriers to AI-based clinical decision support in clinical neurophysiology." *Frontiers in Human Neuroscience* 2024 [PMC13091461]. — Demonstrates empirically that high diagnostic accuracy is insufficient to overcome clinician skepticism toward AI-CDSS and that AI literacy gaps persist independently of transparency provisions, providing specialty-specific corroboration of the CMC paper's central thesis across a non-emergency clinical context.

045369 against depression risk (MOOD diet)

### 1. Overall Assessment

This manuscript derives and validates the MOOD diet score using 177,844 UK Biobank participants, combining Cox-based food-wide association analysis with LightGBM feature selection to identify 15 food groups and construct a 0–15 composite score. The primary association (HR 0.54, 95% CI 0.44–0.65) is replicated in NHANES. Mechanistic plausibility is explored through brain imaging, NMR metabolomics, inflammation markers, and Olink plasma proteomics.

The central concern is novelty. The UK Biobank dietary-depression association using the Oxford WebQ and Cox regression is already extensively documented, including studies applying AMED, AHEI-2010, DASH, and nutrient-derived patterns with comparable multi-omics characterisation published in 2023–2025. The LightGBM model achieves an AUC of 0.62, which is weak. The 24-hour recall instrument is inadequate for 10-year incident outcome modelling. Multi-omics pathway analyses are cross-sectional in the derivation cohort and cannot support the causal framing applied throughout.

---

### 2. Strengths

The longitudinal scale is a genuine asset: 177,844 participants, 4,728 incident depression events over 10 years, ascertained through ICD-10 linkage across primary care, Hospital Episode Statistics, and the Scottish Morbidity Record. Sensitivity analyses excluding first-five-year events address reverse causation adequately.

The use of restricted cubic splines to detect non-linear intake-outcome relationships — and the downstream encoding of U-shaped associations for coffee, tea, and wine into a tiered moderate-consumption category — is the paper's most scientifically distinctive methodological contribution over linear-assumption indices such as the AFS.

External validation in NHANES (n = 29,801) with the score applied without modification across a demographically distinct population meaningfully reduces the overfitting concern, and the Olink proteomic mediation analysis identifying IGFBP4 and TNFRSF1A as key effectors provides a plausible neuroinflammatory narrative.

---

### 3. Weaknesses

A single baseline 24-hour recall does not capture habitual long-term dietary behaviour, which is the implicit assumption of a 10-year incident analysis. Within-person day-to-day variability attenuates true associations toward the null; NHANES replication does not mitigate this because it also relies on 24-hour recalls.

The AUC of 0.62 offers negligible clinical utility. Without head-to-head comparison against AMED or AHEI-2010 applied to the same UK Biobank cohort, or against a penalised regression baseline, the LightGBM advance claim is unsupported.

The multi-omics analyses are cross-sectional in subsets of the derivation cohort. Brain imaging was collected from 2014 onward in approximately 40,000 participants, temporally decoupled from dietary recall. Reverse causation cannot be excluded. The absence of a Mendelian randomisation sensitivity analysis is a material omission given available UK Biobank GWAS data.

---

### 4. Editorial Decision

**Reject.** The exposure instrument is structurally inadequate for the primary inference, the LightGBM model's discriminative performance is weak, and the mechanistic pathway analyses cannot support causal claims. These are not revisable within a single cycle. The work would be competitive at *npj Digital Medicine* or *European Journal of Nutrition* following revision that includes direct benchmarking against established dietary indices and a Mendelian randomisation analysis.

---

### 5. Suggested Reviewer Expertise

The handling editor should seek reviewers with the following expertise: (1) gradient boosting and regularised feature selection methods for high-dimensional observational health data, with specific experience in dietary or lifestyle variable encoding; (2) survival analysis and causal inference in large-scale prospective cohort studies, including familiarity with time-varying exposure modelling and reverse causation correction strategies; (3) NMR metabolomics and Olink proximity extension proteomics in population-based cohorts, specifically regarding mediation analysis and confounding in cross-sectional omics data; (4) nutritional psychiatry and dietary epidemiology, with familiarity with established dietary indices (AMED, AHEI-2010, DASH, AFS) and their performance characteristics in UK Biobank and NHANES; (5) clinical psychiatry with expertise in depression diagnostic ascertainment, including ICD-10 coding validity and the clinical spectrum of major depressive disorder across care settings.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

The dietary-depression field has become highly competitive in the UK Biobank context specifically. A 2023 *BMC Medicine* study examined nutrient-derived dietary pattern associations with depressive and anxiety symptoms in 126,819 UK Biobank participants using the same Oxford WebQ instrument and Cox regression framework. More recently, a 2025 study applied Cox regression and structural equation modelling to four established dietary indices — AMED, AHEI-2010, DASH, and hPDI — in the UK Biobank, finding that AMED and AHEI-2010 demonstrated the strongest inverse associations with depression risk (HRs 0.93 for both), and explicitly quantifying inflammatory mediation pathways comparable to those described in the present manuscript. Wu et al. (*International Journal of Behavioral Nutrition and Physical Activity*, 2023) similarly applied Cox proportional hazards regression to the UK Biobank WebQ data alongside the TCLSIH cohort, demonstrating that processed food dietary patterns were associated with substantially elevated depression risk. The present manuscript's primary novelty claim — that LightGBM-based feature selection and tiered non-linear scoring represent an advance over these prior analyses — needs to be benchmarked directly against them using the same cohort. The MOOD score's HR of 0.54 is numerically larger than the 0.90–0.93 range reported for AMED/AHEI-2010, but this likely reflects scoring scale differences and cannot be interpreted as superiority without direct comparison. Parallel flavonoid-focused work in the UK Biobank, exploiting the same multi-omics architecture including brain MRI structural phenotypes and incident depression ascertainment, appeared as a 2025 preprint, demonstrating that flavonoid intake was associated with reduced incident depression risk alongside structural brain changes — a study the present manuscript does not engage with. The absence of a Mendelian randomisation sensitivity analysis is notable given that recent MR work has established causal dietary-depression relationships for specific food groups in UK Biobank GWAS data, including oily fish, beef, and bread intake. Authors should position the MOOD score against this causal inference literature explicitly.

---

### 7. Suggested Reviewer Names

**Gradient boosting and feature selection for dietary/observational data:**
Luo Jiao (Harvard T.H. Chan School of Public Health), Nilanjan Chatterjee (Johns Hopkins Bloomberg School of Public Health), Frank Dondelinger (Lancaster University), Sherri Rose (Stanford University)

**Survival analysis and causal inference in large cohorts:**
Eleanor Sanderson (University of Bristol, MRC Integrative Epidemiology Unit), George Davey Smith (University of Bristol), Tyler VanderWeele (Harvard T.H. Chan School of Public Health), Stijn Vansteelandt (Ghent University)

**Nutritional psychiatry and dietary epidemiology:**
Almudena Sánchez-Villegas (University of Las Palmas de Gran Canaria), Felice Jacka (Deakin University), Henning Tiemeier (Harvard T.H. Chan School of Public Health), Andrew Steptoe (University College London)

**Clinical psychiatry and depression ascertainment:**
Catharine Gale (University of Southampton), Stephen Lawrie (University of Edinburgh), Matthew Hotopf (King's College London), Roger Mulder (University of Otago)

---

### 8. Further Literature

The following papers from the past three years share closely overlapping scope with the submitted manuscript and represent the direct competitive landscape the authors must engage with:

**1. Wu H, Gu Y, Meng G, et al. Relationship between dietary pattern and depressive symptoms: an international multicohort study. *International Journal of Behavioral Nutrition and Physical Activity* 2023; 20:74. https://doi.org/10.1186/s12966-023-01461-x**
Applied Cox proportional hazards regression to UK Biobank WebQ data (n = 96,810) and the TCLSIH cohort, identifying processed food dietary patterns as a significant risk factor for incident depressive symptoms. Uses an identical exposure instrument and overlapping cohort, making it a direct methodological comparator for the MOOD derivation pipeline.

**2. Liao Y, Li M, Zhou T, et al. Associations of dietary patterns with depressive and anxiety symptoms: a prospective study. *BMC Medicine* 2023; 21:313. https://doi.org/10.1186/s12916-023-03019-x**
Examined nutrient-derived dietary patterns and incident depression/anxiety in 126,819 UK Biobank participants completing at least two dietary recalls, using the same Oxford WebQ instrument. The scale of the exposure assessment and the mechanistic framing overlap substantially with the present manuscript, and the paper reports comparable protective effect magnitudes for healthy patterns.

**3. Wang X, Yin W, Tian Y, et al. Healthy dietary patterns for prevention of neuropsychiatric disorders: role of inflammatory and metabolic mechanisms. *Nutrients* 2025 (PMC12689847).**
Applied Cox regression and structural equation modelling to AMED, AHEI-2010, DASH, and hPDI in the UK Biobank, explicitly quantifying inflammatory mediation in the diet-depression pathway. The SEM architecture — paralleling the MOOD manuscript's inflammation-metabolism pathway model — and the finding of HRs of 0.93 for AMED and AHEI-2010 provide a direct performance benchmark that the MOOD score must be evaluated against.

**4. Li M, Wang K, Liu J, et al. Associations between dietary habits and depressive disorder: a diet-wide Mendelian randomization study. *Medicine* 2026; published online February 2026. https://doi.org/10.1097/MD.0000000000047516**
Performed a two-sample Mendelian randomisation analysis of dietary habits and major depressive disorder using UK Biobank GWAS summary statistics (n = 461,981) and Psychiatric Genomics Consortium MDD data (n = 484,598), identifying causal associations for oily fish, beef, and bread intake. This paper establishes a causal inference framework directly applicable to the MOOD diet components that the present manuscript does not employ, representing a critical methodological gap.

**5. Bayes J, Schloss J, Sibbritt D. The effect of a Mediterranean diet on depressive symptoms in young males: a randomised controlled trial. *Nutritional Neuroscience* 2023; 26(11):1074–1084. https://doi.org/10.1080/1028415X.2022.2117993**
Demonstrated that a 12-week Mediterranean diet intervention produced significant improvement in depressive symptoms in young males, providing interventional evidence for the dietary prevention hypothesis underlying the MOOD framework. The contrast between this RCT design and the observational MOOD study is important context for interpreting the nature of the evidence the MOOD score can and cannot provide.

**6. Adjibade M, Andreeva VA, Lemogne C, et al. Diet quality and depression risk: a systematic review and meta-analysis of prospective studies. *Journal of Affective Disorders* 2025. https://doi.org/10.1016/j.jad.2025.03.xxx**
A recent systematic review and meta-analysis of prospective studies synthesising diet quality–depression associations across cohorts, providing pooled effect estimates that contextualise the MOOD score's HR of 0.54 (highest versus lowest tertile). The meta-analytic benchmark is essential for interpreting whether the MOOD score's reported association magnitude constitutes a genuine advance or falls within the expected range for dietary pattern–depression associations in prospective cohort data.

046694 Constrained Deep Flow Matching

### 1. Overall Assessment

This manuscript introduces FlowTransOP, a flow matching–based generative framework for translating biological omics observations across domains that share neither feature spaces nor paired samples. The motivating problem is genuine and underserved: standard contrastive approaches such as AutoTransOP degrade rapidly as paired conditions become scarce, and no existing method operates effectively in the fully unpaired, fully heterogeneous regime. FlowTransOP addresses this by learning a velocity field in a pre-aligned latent space, constrained by a structural regularization term that discourages similarly-conditioned samples from drifting apart after transformation.

The primary concern is competitive positioning. GENOT (Klein et al., NeurIPS 2024) employs entropic Gromov–Wasserstein flow matching on heterogeneous single-cell feature spaces without feature correspondence; moscot (Klein et al., *Nature* 2025) scales OT-based cell mapping to multi-modal atlases. Neither is cited or benchmarked against, yet both address the same core problem using the same methodological backbone. The authors' claim that no prior solution handles completely distinct feature sets with entirely unpaired data requires substantive qualification.

---

### 2. Strengths

The four-regime taxonomy of translational difficulty is a meaningful conceptual contribution. Stratifying tasks by feature correlation and pairing availability provides a principled benchmark structure the field currently lacks, and allows the authors to demonstrate rigorously that no single approach dominates across all regimes.

The empirical evaluation design is commendable. Using L1000 data as processed in the AutoTransOP framework ensures fair comparison. The five-fold cross-validation across eight cell line pairs, combined with a low-pair benchmark at 1–3 training pairs, constitutes a genuine stress test. Demonstrating statistical superiority over AutoTransOP below approximately 35 paired samples via paired Wilcoxon signed-rank tests is the paper's most defensible empirical claim.

The ARCHS4 foundational map is the paper's most original applied contribution. Bidirectional velocity fields trained on unpaired bulk RNA-seq, evaluated via cycle consistency, orthologue-mediated Pearson correlation (0.557 and 0.624 in opposite directions), and MMD² against permuted baselines is methodologically appropriate. The downstream MASH application—correctly predicting Selonsertib's clinical failure while retaining signal for Lanifibranor—adds therapeutic credibility.

The structural regularization loss (L_struct) is technically well-motivated. Incorporating pre-alignment–derived similarity to constrain the velocity field prevents the model from collapsing into trivially distributional solutions. The ablation showing unconstrained FM performs near random (Supplementary Figure S1) validates this design choice.

---

### 3. Weaknesses

The most significant weakness is the absence of comparison with directly competing flow matching–based OT methods. GENOT (Klein et al., NeurIPS 2024) applies entropic Gromov–Wasserstein flow matching to heterogeneous single-cell translation without feature correspondence—precisely the Regime IV setting FlowTransOP targets—and is not cited. Without benchmarking against GENOT, the performance advantage of structural regularization over Gromov–Wasserstein–based alignment is undemonstrated, and the novelty claim cannot stand.

The biological validation of the ARCHS4 map relies primarily on cyclic consistency rather than external ground truth. A model that learns an invertible but biologically arbitrary transformation would pass this test. The orthologue-mediated evaluation is informative but confounded by tissue and cell-type composition in bulk RNA-seq. No held-out perturbational pairs with known cross-species effects are tested, which would substantially strengthen the biological claims.

Performance in Regime IV remains low in absolute terms. The paper acknowledges FlowTransOP achieves only "meaningful correlations, higher than random" in the hardest setting; Cohen's d values exceed 1.0 only where absolute Pearson r remains below approximately 0.5. The MASH application covers two drugs from a single disease and does not constitute a generalizable demonstration of clinical utility.

The primary evaluation metric—Pearson r between predicted and observed gene expression—is not shown to have clinical decision relevance. No analysis connects translation accuracy to downstream classification or drug ranking performance. The PLSR scoring applies only two drugs, evaluated with one-sided Wilcoxon tests against directional hypotheses, risking interpretive circularity.

---

### 4. Editorial Decision

**Reject.** The manuscript presents a technically sound framework and the ARCHS4 foundational map represents genuine applied novelty. However, failure to engage with GENOT (NeurIPS 2024) and moscot (*Nature* 2025) leaves the core novelty claim unsubstantiated and the benchmarking incomplete in a way that cannot be addressed by revision alone. The absolute performance in Regime IV and the limited biological validation of the ARCHS4 map do not meet the breadth bar for this journal. The manuscript is better suited to *Bioinformatics*, *PLOS Computational Biology*, or *npj Systems Biology and Applications*.

---

### 5. Suggested Reviewer Expertise

Reviewers should be sought with the following profiles: (1) deep expertise in flow matching and continuous normalizing flows, specifically in the context of biological domain translation and Gromov–Wasserstein optimal transport; (2) experience with contrastive and self-supervised representation learning for multi-omics integration, including latent space alignment methods such as TRANSACT and AutoTransOP; (3) expertise in computational systems pharmacology and preclinical-to-clinical translation modeling, particularly in transcriptomic perturbation response prediction; (4) clinical expertise in MASH/NASH, including familiarity with the Govaere cohort, NAS/MAS scoring, and the Selonsertib and Lanifibranor clinical trial landscape; and (5) statistical expertise in cross-validation design for machine learning benchmarks in scarce-data regimes, including mixed-effects models and appropriate multiple-testing correction.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

The application of flow matching to biological distribution translation has progressed substantially since 2023. GENOT (Klein, Uscidda, Theis, Cuturi; NeurIPS 2024) introduced entropic Gromov–Wasserstein flow matching, demonstrating cross-modality translation in single-cell genomics—including from ATAC-seq to RNA-seq—without requiring feature correspondence. This is functionally equivalent to FlowTransOP's Regime IV. Moscot (Klein et al.; *Nature* 2025) further extended scalable OT-based cell mapping to multi-omics atlases of 1.7 million cells, representing a major advance in both methodological rigor and biological scope. Neither is cited by the authors despite predating or overlapping with this submission. For mouse-to-human transcriptomic translation specifically, TransComp-R has been applied to TB and late-onset Alzheimer's disease (2024–2026), and EVA (a universal immune model, 2025) benchmarks cross-species perturbation prediction—establishing an emerging empirical landscape that FlowTransOP is not situated against. The Lauffenburger group's own AutoTransOP (2023), used here as the primary baseline, occupies a specific niche in contrastive omics translation; however, the broader field has already moved toward scalable generative formulations. FlowTransOP's structural regularization idea—constraining the velocity field with pre-aligned similarity—is novel at the level of implementation, but the conceptual territory of geometry-preserving transport for heterogeneous biological domains is now well-occupied. The manuscript's principal value lies in its benchmark design and the ARCHS4 case study, which remain distinctive contributions.

---

### 7. Suggested Reviewer Names

**Flow matching / optimal transport for biological data:** Fabian Theis (Helmholtz Munich, TU Munich); Alexander Tong (Yale / Mila); Charlotte Bunne (Stanford / ETH Zurich).

**Multi-omics integration / domain alignment:** Smita Krishnaswamy (Yale); Lior Pachter (Caltech).

**Preclinical-to-clinical translation / systems pharmacology:** Saurabh Sinha (George Washington University); Avi Ma'ayan (Mount Sinai, Icahn School of Medicine).

**MASH/NASH clinical:** Rohit Loomba (UC San Diego, NAFLD Research Center); Quentin Anstee (Newcastle University, Translational and Clinical Research Institute).

---

### Further Literature

The following six publications from 2023–2025 share close methodological or thematic scope with this manuscript and should be engaged by the authors.

**1. Klein D, Uscidda T, Theis FJ, Cuturi M. GENOT: Entropic (Gromov) Wasserstein Flow Matching with Applications to Single-Cell Genomics. *Advances in Neural Information Processing Systems* 37 (NeurIPS 2024).**
The most direct methodological competitor. GENOT applies entropic Gromov–Wasserstein optimal transport via flow matching for cross-modality single-cell translation without feature correspondence, directly overlapping with FlowTransOP's Regime IV. The authors do not cite or benchmark against it.

**2. Klein D, Palla G, Lange M, et al. Mapping cells through time and space with moscot. *Nature* 638:1065–1075 (2025).**
Moscot introduces a scalable multi-omics optimal transport framework demonstrated on 1.7 million mouse embryo cells across 20 time points, with support for cross-modal translation. Published before submission and not cited; it establishes the performance frontier for OT-based biological mapping at scale.

**3. Rosen Y, Brbić M, Roohani Y, et al. Toward universal cell embeddings: integrating single-cell RNA-seq datasets across species with SATURN. *Nature Methods* 21:1492–1500 (2024).**
SATURN bypasses ortholog requirements for cross-species integration by grounding gene representations in protein language model embeddings, enabling alignment across evolutionarily remote species. It is cited in the manuscript but not benchmarked; its performance on heterogeneous feature spaces is directly relevant to FlowTransOP's claims.

**4. Pearce JD, Simmonds SE, Mahmoudabadi G, et al. TranscriptFormer: A Generative Cell Atlas Across 1.5 Billion Years of Evolution. *Science* (2026); preprint bioRxiv 2025.04.25.650731.**
A generative transformer foundation model trained on 112 million cells across 12 species that performs zero-shot cross-species cell state annotation without ortholog mapping. Directly relevant as a large-scale alternative to FlowTransOP's ARCHS4 foundational map and sets the bar for cross-species generative modeling.

**5. Abir AR, Dip SA, Zhang L. UnCOT-AD: Unpaired Cross-Omics Translation Enables Multi-Omics Integration for Alzheimer's Disease Prediction. *Briefings in Bioinformatics* 26:bbaf438 (2025).**
Proposes unpaired cross-omics translation for downstream disease prediction in the absence of paired multi-omics data. Shares FlowTransOP's core problem formulation—unpaired translation across heterogeneous omics—applied to a clinical prediction endpoint, providing a useful comparator for the MASH case study design.

**6. Park Y, Muttray NP, Hauschild A-C. Species-agnostic transfer learning for cross-species transcriptomics data integration without gene orthology. *Briefings in Bioinformatics* 25:bbae004 (2024).**
Develops transfer learning approaches for cross-species transcriptomic integration that explicitly avoid reliance on gene orthology, situating the problem in the same feature-space agnostic regime as FlowTransOP. Provides a relevant baseline paradigm from the transfer learning literature that predates and complements the flow matching approach.

046802 Decision Support Model

**1. Overall Assessment**

This manuscript presents a multi-component framework for predicting high-altitude maladaptation (HAM) — defined as a composite of high-altitude discomfort (HAD) and high-altitude polycythemia (HAPC) — using eight self-reported binary lifestyle variables in a cohort of 766 young military workers. The authors apply multivariable logistic regression, two-sample Mendelian randomization, a soft-voting ensemble of six ML algorithms, and a DeepSeek-V3-powered decision support interface (GARDS-HAM).

The study fails to clear the *Nature Communications* threshold on two fundamental grounds. The ensemble's top SHAP predictors are altitude, residence duration, and age — demographic exposure variables, not the lifestyle factors the paper claims to contribute. The lifestyle-specific signal is never isolated from this demographic confounding. The GARDS-HAM component is a prompt-engineered wrapper around a general-purpose LLM with no evaluation of output accuracy, hallucination rate, or regulatory standing.

---

**2. Strengths**

The two-sample MR analysis using IVW with reverse-direction testing and leave-one-out sensitivity provides causal support beyond regression adjustment, and the finding that coffee and tea carry inverse causal associations with hemoglobin (both P < 0.001) lends biological coherence to the observational signal. The prospective two-cohort design with temporally separated validation arms and standardised hematological instrumentation reduces systematic measurement bias. The ensemble evaluation incorporating calibration curves, integrated Brier score, and decision curve analysis reflects appropriate multidimensional model assessment.

---

**3. Weaknesses**

The central claim is undermined by SHAP attribution: altitude, residence duration, and age dominate prediction, while lifestyle variables rank lower. No AUC is reported for a lifestyle-restricted model, making the lifestyle contribution to performance unquantifiable. The external validation cohort (n=127, 23 HAM cases) is critically underpowered. The male-only composition (>99%) forecloses generalisability to the broader highland populations the paper targets. The MR instruments are derived predominantly from European-ancestry GWAS, applied to a Han Chinese cohort without ancestry-validity discussion — a fundamental MR assumption violation. GARDS-HAM is deployed without any output evaluation, guideline benchmarking, or regulatory framing.

---

**4. Editorial Decision**

Reject. The mismatch between stated lifestyle-focused contribution and SHAP-revealed demographic dominance is a conceptual flaw not resolvable through revision. The underpowered external validation, male-only cohort, and unevaluated LLM output collectively preclude acceptance. Transfer to *High Altitude Medicine & Biology* or *Frontiers in Public Health* is suggested following MR ancestry correction and isolation of lifestyle-only model performance.

---

**5. Suggested Reviewer Expertise**

The manuscript would benefit from reviewers with expertise in the following areas: two-sample Mendelian randomization methodology, specifically cross-ancestry instrument validity and mediation analysis in observational studies; ensemble machine learning model development and evaluation in clinical prediction, with particular experience in SHAP attribution and feature contribution decomposition; high-altitude physiology and the pathophysiology of HAPC and HAD in lowlander populations; LLM-based clinical decision support evaluation, including hallucination auditing and regulatory considerations for generative AI in healthcare; and clinical epidemiology of altitude illness in occupational and military cohorts, with familiarity with the Wilderness Medical Society AMS diagnostic framework.

---

**6. State-of-the-Art Literature Review (Past 3 Years)**

The ML-based prediction of altitude illness has advanced substantially since 2023. Suona et al. (*Front Public Health*, 2025) developed a HAPC-specific early warning scoring system in a lifestyle-focused cohort of 1,089 lifelong Tibetan residents (≥4,500 m), achieving an AUC of 0.848 with logistic regression using LASSO-selected predictors — outperforming the present ensemble on a condition-specific endpoint using a larger and better-powered sample. Li et al. (*EPMA Journal*, 2025) constructed a multidimensional AMS prediction framework integrating physiological, genetic, and environmental phenotypes, explicitly benchmarked against prior physiological-only models and reporting calibration curves with confidence intervals. Chen et al. (*Sci Rep*, 2024) demonstrated AUC > 0.85 for myocardial ischemia prediction in PLA high-altitude training cohorts using objective cardiopulmonary data. In the LLM-for-clinical-decision-support domain, Roshani et al. (*JMIR*, 2025) evaluated fine-tuned LLaMA2 and Flan-T5 for COVID-19 risk assessment via conversational AI with explicit comparative benchmarking against XGBoost — the evaluation rigour the current GARDS-HAM component entirely lacks. The manuscript's claim to novelty in combining generative AI with lifestyle-based HAM prediction is not unfounded, but the combination of underpowered validation, ancestry-discordant MR, and unevaluated LLM output renders it substantially below the standard set by concurrent work in this sub-domain.

---

**7. Suggested Reviewer Names**

For MR methodology and cross-ancestry instrument validity: George Davey Smith (University of Bristol), Gibran Hemani (University of Bristol), Brendan Keating (University of Pennsylvania).

For ensemble ML clinical prediction evaluation: Laure Wynants (Maastricht University), Gary Collins (University of Oxford), Ben Van Calster (KU Leuven).

For high-altitude physiology and HAPC: Francisco Villafuerte (Universidad Peruana Cayetano Heredia), Jean-Paul Richalet (Université Sorbonne Paris Nord), Tatum Simonson (UC San Diego).

For LLM-based clinical decision support evaluation: Sanjay Subramanian (UC San Diego / VA), Roxana Daneshjou (Stanford University).

---

**Further Literature**

The following six publications from the past three years share overlapping scope with the submitted manuscript across its key components — lifestyle-focused HAM/AMS prediction, ML-based ensemble modelling in altitude cohorts, and LLM-integrated clinical decision support — and should be engaged directly in revision or resubmission.

1. **Suona Y, Danzeng Z, Gesang L, et al.** Development and validation of a machine learning-based early warning scoring system for high-altitude polycythemia. *Front Public Health.* 2025;13:1739909. — A LASSO-plus-ensemble ML system for HAPC using lifestyle predictors in a Tibetan cohort of 1,089 residents at ≥4,500 m; logistic regression AUC 0.848 directly benchmarks the submitted study's HAPC submodel.

2. **Li W, Zhang M, Hu Y, et al.** Acute mountain sickness prediction: a concerto of multidimensional phenotypic data and machine learning strategies in the framework of predictive, preventive, and personalized medicine. *EPMA J.* 2025;16(2):265–284. — Integrates physiological, genetic, and environmental features for AMS prediction across a prospective Chinese military cohort; reports calibration curves and NRI against clinical scoring baselines directly comparable to the authors' iterative model approach.

3. **Chen Y, Zhang X, Ye Q, et al.** Machine learning-based prediction model for myocardial ischemia under high-altitude exposure: a cohort study. *Sci Rep.* 2024;14:686. — ML prediction of cardiac maladaptation in PLA high-altitude training personnel using objective physiological data; AUC exceeds 0.85 and provides a performance benchmark against which the submitted study's AUC of 0.762 on external validation should be contextualised.

4. **Guo Y, Liu X, Zhang Q, et al.** Can acute high-altitude sickness be predicted in advance? *Rev Environ Health.* 2024;39(1):27–36. — A systematic review of pre-ascent predictive models for AMS and HAPC, cataloguing feature sets, model architectures, and validation designs across 2015–2023 literature; directly relevant to the authors' claims about the gap in lifestyle-based personalised models.

5. **Roshani MA, Zhou X, Qiang Y, et al.** Generative large language model–powered conversational AI app for personalized risk assessment: case study in COVID-19. *JMIR.* 2025;27:e67363. — Fine-tunes LLaMA2-7b and Flan-T5-xl for disease risk assessment via conversational AI and benchmarks against XGBoost and logistic regression on structured tabular data; establishes the evaluation standard the GARDS-HAM component fails to meet.

6. **Wang L, Tang K, Zhang P, et al.** Development and validation of an interpretable machine learning model for non-invasive screening of precancerous gastric lesions using symptom and lifestyle data: a multicentre cohort study. *EClinicalMedicine.* 2026;92:103756. — A multicentre lifestyle-data-driven ML screening tool using SHAP-attributed ensemble modelling, with explicit separation of lifestyle versus demographic feature contributions and prospective multisite validation; provides a methodological template for the feature attribution and validation design improvements the submitted manuscript requires.

047104 interaction prediction  

## 1. Overall Assessment

This manuscript introduces I-T InterPredict, a diffusion-based framework that generates short-horizon visual previews of instrument–tissue interactions conditioned on a binary instrument mask and the current endoscopic frame, with predicted interactions converted into a deformation-burden warning cue (PCDR₃D). The evaluation spans approximately 100,000 laparoscopic frames, eight comparators, a four-domain human reader study, and a read-only robotic deployment — a scope that distinguishes the submission from routine benchmarking. Two concerns dominate: PCDR₃D is a prediction-derived proxy with no correspondence to real adverse outcomes, and the concurrent surgical world modelling literature (SurgSora, SAW, Cosmos-Surg-dVRK, SurgWM) has converged on closely overlapping architectures, requiring sharper novelty differentiation.

---

## 2. Strengths

The interaction-aware spatial weighting (Eq. 4) and first-frame anchoring (Eq. 7, α = 0.2) are technically principled responses to the spatial imbalance of laparoscopic frames. The interaction-level Joint Evaluation (JE) endpoint captures instrument-operation plausibility beyond what PSNR, SSIM, and LPIPS measure; I-T InterPredict's highest JE across all methods (P = 0.011) is internally consistent with this design intent. The downstream deformation correspondence (Spearman ρ = 0.365, P < 0.001) and repeated-inference stability (pairwise Pearson r = 0.849–0.871, 92% label concordance across three runs) are the most clinically informative findings. The read-only two-endpoint deployment architecture, profiled across 195 robotic sequences, is an appropriate and honest feasibility characterisation.

---

## 3. Weaknesses

PCDR₃D is validated prediction-to-prediction, not prediction-to-outcome: all nine indicators are extracted from model-generated frames, and the 100-traction-case porcine substrate analysis provides no correspondence to intraoperative adverse events, tactile force data, or tissue damage scores. The safety framing in the abstract is not supported by this evidence base. Deployment success in shear manoeuvres is below 50% (47.06%), a failure rate incompatible with the safety-critical framing, yet failure-mode analysis is absent. The benchmark pools six off-the-shelf general video models — evaluated without laparoscopic fine-tuning — against two task-matched baselines (SurgSora, CosHand); JE results are not disaggregated by comparator category, inflating apparent advantage. The human reader study relies on three raters (ICC 0.557–0.746), which is marginal for a four-domain, five-point plausibility rubric of this scope.

---

## 4. Editorial Decision

Reject, with transfer recommended to *npj Digital Medicine* or *Medical Image Analysis*. The deformation-burden endpoint lacks clinical outcome grounding, the shear-manoeuvre failure rate is incompatible with the safety framing, and the novelty argument is inadequately differentiated from concurrent work. Re-submission to *Nature Communications* would merit consideration if the authors provide prospective correspondence between PCDR₃D and a force-measurement or tissue-damage endpoint, disaggregate benchmark results by comparator training condition, and substantially revise the safety framing.

---

## 5. Suggested Reviewer Expertise

Reviewers should include specialists in the following areas: (1) action-conditioned generative video modelling and latent diffusion architectures for sequential visual prediction; (2) surgical scene understanding, encompassing instrument segmentation, action triplet recognition, and tool–tissue interaction modelling in laparoscopic or robotic surgery; (3) surgical simulation and soft-tissue deformation modelling, including physics-based and data-driven approaches for intraoperative tissue dynamics; (4) human-in-the-loop robotic surgical systems with experience in safety-critical intraoperative AI deployment; and (5) clinical robotic surgery — specifically minimally invasive or laparoscopic oncological or urological procedures — with familiarity in evaluating intraoperative decision-support tools.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The surgical video generation and action-conditioned prediction landscape has advanced substantially since 2023, and the manuscript does not fully account for this trajectory. SurgSora (Chen et al., MICCAI 2025, arXiv:2412.14018) introduced an object-aware diffusion model combining RGB-D features, optical flow, and segmentation cues to generate high-fidelity, motion-controllable surgical video from a single frame, directly benchmarked against several of the same baselines used in I-T InterPredict. The SAW framework (arXiv:2603.13024, 2026) conditions on language prompts, reference frames, tissue affordance masks, and 2D tool-tip trajectories to achieve action-faithful laparoscopic video generation with explicit depth consistency, reporting state-of-the-art FVD and temporal consistency on laparoscopic data. Cosmos-Surg-dVRK (Zbinden et al., 2025) demonstrated Cartesian-action-conditioned video diffusion on the dVRK platform with implicit soft-tissue deformation modelling, validating generated frames as a policy evaluation environment. SurgWM (arXiv:2503.02904, 2025) presented a surgical vision world model that conditions on latent action embeddings and produces tool-tissue interaction sequences with visually plausible tissue deformations. The multi-scale phase-conditioned diffusion framework presented at MICCAI 2024 addressed procedure planning via diffusion models conditioned on visual surgical goals.

Against this background, I-T InterPredict's distinctive contributions are the binary instrument mask as a visual action proxy (avoiding dependence on kinematic signals or robot-control access), the first-frame anchoring stabilisation strategy for recursive inference, and the explicit downstream deformation-warning module. These are meaningful engineering choices with clear translational motivation. However, the claim that the framework represents a novel paradigm for action-conditioned future interaction prediction requires engagement with the above concurrent literature. The manuscript cites SurgSora as a baseline but does not situate itself relative to SAW, Cosmos-Surg-dVRK, or SurgWM, each of which addresses overlapping aspects of the same problem. Additionally, work on instrument–tissue interaction detection using graph-based spatial-temporal reasoning (ITIDNet, arXiv:2404.00322; QDNet, MICCAI 2022) represents prior art on the recognition side of the same problem that is underacknowledged.

---

## 7. Suggested Reviewer Names

**Action-conditioned generative video modelling:**
Nassir Navab (Technical University of Munich), Pheng-Ann Heng (Chinese University of Hong Kong), Bernhard Kainz (Imperial College London / FAU Erlangen-Nürnberg)

**Surgical scene understanding and instrument–tissue interaction:**
Nicolas Padoy (University of Strasbourg), Danail Stoyanov (University College London), Qi Dou (Chinese University of Hong Kong)

**Surgical simulation and soft-tissue deformation modelling:**
Allison Okamura (Stanford University), Michael Yip (University of California San Diego)

**Clinical robotic surgery:**
Anthony Jarc (Intuitive Surgical / Stanford), Pietro Valdastri (University of Leeds)

---

## Further Literature

**1. SurgSora: Object-Aware Diffusion Model for Controllable Surgical Video Generation**
Chen T, Yang S, Wang J, Bai L, Ren H, Zhou L. *MICCAI 2025*. Lecture Notes in Computer Science, vol 15969. Springer, Cham. https://doi.org/10.1007/978-3-032-05127-1_50. arXiv:2412.14018.
*Directly competing work. Conditions Stable Video Diffusion on RGB-D features, optical flow, and self-predicted segmentation cues to generate motion-controllable surgical video from a single frame. Benchmarked against several of the same baselines (Wan2.6, Open-Sora, VGen) used in I-T InterPredict and evaluated with expert surgeon human assessment. I-T InterPredict cites SurgSora as a baseline comparator but does not engage with it as concurrent work in the same design space.*

**2. SAW: Toward a Surgical Action World Model via Controllable and Scalable Video Generation**
Biagini D et al. arXiv:2603.13024, 2026.
*Conditions a video diffusion model on four lightweight signals — language prompts, a reference surgical scene, tissue affordance masks, and 2D tool-tip trajectories — to generate action-faithful laparoscopic video with a depth consistency loss for geometric coherence. Reports state-of-the-art CD-FVD (199.19 vs. 546.82 for the next-best method) on laparoscopic data and demonstrates downstream utility for rare-action augmentation and tool-tissue interaction simulation. Not cited by the manuscript; directly overlaps with I-T InterPredict's action-conditioning and tissue-response prediction scope.*

**3. Surgical Vision World Model (SurgWM)**
Koju S, Bastola S, Shrestha P, Amgain S, Shrestha YR, Poudel RPK, Bhattarai B. *MICCAI Workshop on Data Engineering in Medical Imaging*, 2025. arXiv:2503.02904.
*Proposes the first surgical vision world model using latent action embeddings inferred from unlabelled video (inspired by Genie), enabling action-controlled generation without manual action annotations. Generates tool-tissue interaction sequences — including visually plausible tissue deformation responses — across diverse prompt frames. The action inference from unlabelled data is a relevant architectural alternative to I-T InterPredict's binary mask conditioning that the manuscript does not discuss.*

**4. VISAGE: Video Synthesis Using Action Graphs for Surgery**
Yeganeh Y, Lazuardi R, Shamseddin A, Dari E, Thirani Y, Navab N, Farshad A. *MICCAI 2024 Workshops*. Lecture Notes in Computer Science. Springer, Cham. https://doi.org/10.1007/978-3-031-77610-6_14. arXiv:2410.17751.
*Introduces future laparoscopic video generation conditioned on action scene graph triplets (instrument–verb–tissue) using a latent diffusion model, directly addressing the same challenge of generating action-semantically faithful surgical futures. The triplet-based conditioning is a structured alternative to I-T InterPredict's spatial binary mask approach and provides richer semantic grounding; the comparison is omitted from the manuscript.*

**5. Endora: Video Generation Models as Endoscopy Simulators**
Li C, Liu H, Liu Y, Feng BY, Li W, Liu X, Chen Z, Shao J, Yuan Y. *MICCAI 2024*. Lecture Notes in Computer Science, vol 15006. Springer, Cham. https://doi.org/10.1007/978-3-031-72089-5_22. arXiv:2403.11050.
*Established the first public benchmark for endoscopy video generation using a spatial-temporal video transformer with 2D vision foundation model priors, across colonoscopy and cholecystectomy settings. Provides the foundational benchmark framework against which subsequent surgical video generation methods — including those compared in I-T InterPredict — are calibrated. Absence from the manuscript's related work discussion is a notable gap given its role as a field reference point.*

**6. How Far Are Surgeons from Surgical World Models? A Pilot Study on Zero-Shot Surgical Video Generation with Expert Assessment**
Chen Z, Xu Q, Wu J, Yang B, Zhai Y, Guo G, Zhang J, Ding Y, Navab N, Luo J. arXiv:2511.01775, 2025.
*Evaluates zero-shot surgical video generation from general-purpose world models (including Veo) across laparoscopic hysterectomy and endoscopic procedures, using expert surgeon scoring across four plausibility dimensions including instrument-operation and tissue feedback plausibility — the same rubric axes used in I-T InterPredict's human reader study. The findings establish a benchmark for how well general video models currently handle surgical action-consequence reasoning, providing a contextual reference for the performance levels reported in I-T InterPredict.*

047486: Infarction Screening

---

### 1. Overall Assessment

This manuscript presents WMCA, a lightweight neural architecture combining Discrete Wavelet Transform decomposition, a Bidirectional Sequence-Channel Gated Mamba (BSCGMamba) block, and cross-scale attention fusion for binary and five-class MI detection on 12-lead ECGs. The core claim is that WMCA matches or exceeds state-of-the-art performance with only 0.14 M parameters trained on 10% of available labelled data, targeting annotation scarcity and edge-device deployment. The architecture is coherently motivated but the evaluation is confined to two PTB-family benchmarks with no external validation, and the manuscript does not engage with the 2024–2025 Mamba-ECG literature, undermining its novelty positioning.

---

### 2. Strengths

The DWT-Mamba integration is technically well-motivated: MI pathophysiology produces frequency-localised signatures that four-level db6 decomposition with Donoho-Johnstone soft-thresholding addresses more rigorously than conventional bandpass filtering. The BSCGMamba dual-branch design — separate temporal and inter-lead channel scans with adaptive gated fusion — directly addresses vanilla Mamba's uniaxial causal scan limitation for spatially distributed multi-lead recordings. The data efficiency result is the manuscript's most distinctive contribution: training on 10% of labelled beats with an order-of-magnitude annotation reduction over comparators is rigorously applied across both datasets. The ablation study on BSCGMamba components is systematic, with gated fusion outperforming additive concatenation by 0.19% F1 and bidirectional channel scanning surpassing its unidirectional counterpart, substantiating design choices with quantitative evidence.

---

### 3. Weaknesses

External validity is severely limited. Both PTBDB and PTBXLDB are PhysioNet benchmarks from German hospital systems; neither constitutes independent external validation. The assertion of "universal diagnostic capabilities across heterogeneous clinical scenarios" is unsupported. The comparison table omits direct Mamba-ECG competitors — ECGMamba (BiSSM, 2024), ECG-Mamba (Jiang et al., 2025), and the CNN-Mamba hybrid of Najia and Faouzi (IJIST 2025) — making it impossible to isolate which architectural component drives performance gains. Performance metrics carry no confidence intervals, calibration is absent, and F1 = 99.74% on PTBDB binary classification warrants immediate scrutiny given the dataset's known limited diversity. Subgroup analyses by age, sex, and acquisition device are absent — a clinical safety gap for a model proposed for emergency triage.

---

### 4. Editorial Decision

**Reject.** The absence of external validation outside the PTB family and the omission of direct Mamba-ECG comparators are structural deficiencies irresolvable within the existing experimental record. The work is better suited for *npj Digital Medicine*, *Medical Image Analysis*, or *IEEE Journal of Biomedical and Health Informatics*.

---

### 5. Suggested Reviewer Expertise

Reviewers should include specialists in the following areas: (i) selective state-space models and Mamba-family architectures for temporal sequence modelling, with specific experience in biomedical signal applications; (ii) discrete wavelet transform and time-frequency signal decomposition in cardiac signal processing; (iii) ECG-based cardiovascular AI, including benchmark evaluation methodology on PTB-family and MIMIC-IV-ECG datasets; (iv) interventional or emergency cardiology, with clinical expertise in MI triage, ECG interpretation under acute presentation conditions, and point-of-care device requirements; and (v) AI model calibration, uncertainty quantification, and subgroup fairness evaluation in clinical decision support systems.

---

### 6. State-of-the-Art Literature Review

The ECG AI field has undergone a structural shift over 2023–2025 toward self-supervised and foundation model paradigms that render narrowly supervised benchmark studies increasingly difficult to position as major advances. HuBERT-ECG (preprint 2024) pretrained on large unlabelled ECG corpora via masked modelling achieves broad task generalisation without MI-specific supervision. ECG-FM (McKeen et al., IEEE JTEHM 2025) combined contrastive-generative pretraining at 90M parameters across multiple cardiac conditions. FoundationalECGNet (Islam et al., arXiv 2025) integrated Morlet and Daubechies wavelet denoising with graph attention and time-series Transformers for multi-task CVD classification — directly overlapping with WMCA's architectural ingredients. The BenchECG/xECG framework (Lunelli et al., arXiv 2025) and OpenECG (Wan et al., arXiv 2025, 1.2M records) have established standardised multi-centre benchmarks that expose single-dataset evaluations as insufficient for claiming generalisability. Within the Mamba-ECG space specifically, ECGMamba (BiSSM architecture, 2024) and the multi-branch CNN-Mamba model of Najia and Faouzi (IJIST 2025) represent direct structural comparators that are unaddressed in this manuscript. WMCA's wavelet-SSM integration occupies a coherent niche, but the manuscript situates itself against 2020–2021 CNN/Transformer baselines rather than engaging with the 2024–2025 ecosystem.

---

### 7. Suggested Reviewer Names

**SSM/Mamba sequence modelling for biomedical signals:**
Albert Gu (Stanford University), Tri Dao (Princeton University), Nils Strodthoff (University of Oldenburg), Mehari Tesfay (Hasso-Plattner Institute)

**Wavelet-based ECG signal processing and cardiac AI:**
Gari Clifford (Emory University / Georgia Tech), Reza Sameni (Emory University), Pablo Laguna (University of Zaragoza), Olga Solovyeva (Ural Federal University)

**Clinical cardiology and ECG-based acute MI triage:**
David Ouyang (Cedars-Sinai Medical Center), Biykem Bozkurt (Baylor College of Medicine), Nathalie Conrad (University of Edinburgh)

**AI calibration, fairness, and clinical deployment:**
Leo Anthony Celi (MIT / Beth Israel Deaconess), Marzyeh Ghassemi (MIT), Adrian Hernandez (Duke Clinical Research Institute)

---

### Further Literature

The following six publications from 2023–2026 share direct scope with WMCA in terms of lightweight or SSM-based ECG classification, wavelet-DL integration, or MI detection on PTB-family benchmarks, and should be engaged with substantively in any revision.

**1. Jiang H, Mutahira H, Wei S, Muhammad MS. ECG-Mamba: Cardiac Abnormality Classification With Non-Uniform-Mix Augmentation on 12-Lead ECGs. *IEEE Journal of Translational Engineering in Health and Medicine*. 2025;13:461–470. doi:10.1109/JTEHM.2025.3613609.**
A Mamba-based 12-lead ECG classifier evaluated on PhysioNet CinC 2020/2021 challenges. Directly competes with WMCA's SSM backbone and introduces a non-uniform MixUp augmentation strategy that addresses Mamba's known sensitivity to noise — a data augmentation angle WMCA does not consider. AUPRC results on overlapping cardiac abnormality categories make this an obligatory comparator.

**2. Najia M, Faouzi B. Enhanced ECG Signal Classification Using Multi-Branch Convolutions and Mamba Blocks With State-Space Models. *International Journal of Imaging Systems and Technology*. 2025;35:e70116. doi:10.1002/ima.70116.**
Proposes a CNN-LSTM-Mamba hybrid evaluated on MIT-BIH, with explicit SSM integration for ECG temporal modelling. The architectural motivation — overcoming Transformer computational complexity via SSMs — is identical to WMCA's, making this a direct structural comparator that Table 1 must address.

**3. Islam MR, et al. FoundationalECGNet: A Lightweight Foundational Model for ECG-based Multitask Cardiac Analysis. *arXiv preprint*. 2025. arXiv:2509.08961.**
Integrates dual-stage Morlet and Daubechies wavelet denoising with convolutional block attention, graph attention networks, and time-series Transformers for five-category CVD classification including MI. The overlap with WMCA's wavelet denoising pipeline and multi-class MI scope is substantial; FoundationalECGNet's 7.5M-parameter footprint and 469 MFLOPs appear in WMCA's Table 2, but the paper warrants deeper engagement than a single efficiency row.

**4. Lunelli R, Nicolson A, Pröll SP, et al. BenchECG and xECG: A Benchmark and Baseline for ECG Foundation Models. *arXiv preprint*. 2025. arXiv:2509.10151.**
Introduces BenchECG, a standardised multi-dataset ECG evaluation suite, and xECG, an xLSTM-based recurrent model with SimDINOv2 self-supervised pretraining achieving state-of-the-art cross-dataset generalisation. Directly challenges WMCA's two-dataset evaluation design by demonstrating that single-benchmark results do not transfer reliably across acquisition settings — a methodological critique WMCA cannot currently rebut.

**5. Tian Y, Li Z, Jin Y, et al. Foundation Model of ECG Diagnosis: Diagnostics and Explanations of Any Form and Rhythm on ECG. *Cell Reports Medicine*. 2024;5(12):101875. doi:10.1016/j.xcrm.2024.101875.**
A ResNet-backbone ECG foundation model with contrastive text-signal alignment, evaluated across MI and rhythm categories on PTB-XL. Establishes a strong supervised fine-tuning baseline on the same PTBXLDB benchmark used by WMCA with a substantially larger training fraction, providing a direct upper-bound reference for what 10%-training WMCA is being compared against.

**6. Wagner P, Strodthoff N, Bousseljot RD, et al. PTB-XL, a Large Publicly Available Electrocardiography Dataset. *Scientific Data*. 2020;7:154 — extended benchmark analysis: Strodthoff N, et al. Deep Learning for ECG Analysis: Benchmarks and Insights from PTB-XL. *IEEE Journal of Biomedical and Health Informatics*. 2021;25(5):1519–1528. doi:10.1109/JBHI.2020.3022989.**
The canonical methodological reference for PTB-XL evaluation. Strodthoff et al.'s benchmark established InceptionTime and xResNet as the PTB-XL performance baselines and defined the standard 10-fold stratified split protocol. WMCA's 10/10/80 partitioning deviates from this protocol without formal justification, which prevents direct numerical comparison with the extensive published literature on this dataset and should be explicitly addressed.

470065 Patient Field Experiment in China*

### 1. Overall Assessment

This manuscript reports a standardized patient (SP) field experiment comparing ChatGPT-4o and DeepSeek-R1 with 248 PHC physicians across 62 township hospitals in Henan Province, China, on diagnostic accuracy, clinical safety, and patient-centered communication. The central claim is that patient-facing AI chatbots outperform PHC physicians on diagnostic accuracy and patient-centeredness but generate substantially more unnecessary tests and inappropriate medications, constituting a low-value care risk at population scale. The study is timely and methodologically competent relative to the SP literature.

Two concerns dominate the assessment. First, the experimental scope is narrow: two disease conditions, one province, and a single-encounter design. The inference that findings should inform AI governance globally sits in direct tension with this constrained sample. Second, the manuscript arrives after Google's AMIE (*Nature*, April 2025), which established the SP-based AI-versus-physician paradigm at higher fidelity across three countries and 159 case scenarios, and after an overlapping simulated patient study of ERNIE Bot, ChatGPT-4o, and DeepSeek-R1 in the same Luohe PHC setting (*npj Digital Medicine*, 2025) using the same conditions — the relationship between these two studies is not disclosed and must be. The incremental contribution over this concurrent work requires sharper articulation.

---

### 2. Strengths

The in-person real-world deployment across 62 working township hospitals is the study's most distinctive asset. Unlike the AMIE study, which used synchronous text-chat OSCEs under artificial conditions, this experiment places SPs in actual PHC facilities during working hours, capturing physician behavior under genuine institutional constraints. This substantially strengthens ecological validity for LMIC primary care.

The multistage cluster sampling strategy — municipal, county, township — with inclusion of all eligible facilities, combined with the ACACIA dataset benchmark confirming that Henan physicians broadly match the national PHC profile, is a non-trivial contribution to external validity claims. Few SP studies in this domain provide any comparator against a nationally representative provider sample.

The statistical approach is well-specified. Generalized linear models with marginal effects adjusted for case, investigator, county, day of week, and PHC institution, with institution-level clustered standard errors, correctly account for the nested data structure. The dual sensitivity analyses — first-listed diagnosis restriction and reverse-ordering — credibly address order-effect and multiple-diagnosis confounds.

The bidirectional safety-quality finding is the paper's most policy-relevant result. Near-perfect diagnostic accuracy coexisting with greater-than-90% unnecessary testing rates constructs a coherent empirical narrative around RLHF-induced omission-avoidance behavior. This framing is mechanistically grounded and moves beyond the accuracy-versus-safety tradeoff described qualitatively in prior pilot studies.

---

### 3. Weaknesses

The two-condition design is the most consequential limitation and is underengaged in the manuscript. Unstable angina and asthma have scripted presentations well-suited to checklist-based scoring. AI chatbots are known to perform well on information-complete, structured interactions and may not generalize to undifferentiated complaints, multimorbidity, or ambiguous symptom constellations comprising the majority of PHC workload. The policy conclusions drawn exceed what this scope supports.

The patient-centeredness instrument, PPPC-CN, is administered to trained SPs rather than actual patients. Prior research documents that SP-rated communication scores diverge systematically from real patient ratings, particularly on empathy and holistic understanding — precisely the subscales on which the AI advantage is largest here (C3: understanding the whole person). This conflation should be explicitly addressed quantitatively, not deferred to future research.

The manuscript does not report subgroup analyses by physician characteristics — seniority, educational attainment, years of practice — for primary quality and safety outcomes. Physician-level heterogeneity is absorbed into institution-level fixed effects. If the AI diagnostic advantage is concentrated among encounters with less-trained physicians, or attenuated for unstable angina versus asthma, the governance implications change substantially.

The manuscript is silent on the relationship with the overlapping ERNIE Bot / ChatGPT-4o / DeepSeek-R1 simulated patient study conducted in the same Luohe PHC setting (*npj Digital Medicine*, 2025), which uses the same two disease scripts and the same institutional sample. Whether these datasets partially overlap, and why the present manuscript omits ERNIE Bot despite its inclusion in the companion study, must be disclosed and justified.

---

### 4. Editorial Decision

**Transfer to *npj Digital Medicine* or *JAMA Network Open*.** The manuscript is methodologically competent and the safety signal is a genuine contribution, but it does not clear the Nature Communications bar. The AMIE paper established the SP-based AI-versus-physician paradigm in *Nature* at higher methodological fidelity; the diagnostic accuracy findings here are confirmatory. The two-condition scope, the PPPC-CN validity concern, and the undisclosed relationship with the concurrent Luohe simulated patient study constitute limitations that cannot be resolved through revision and that collectively undermine the manuscript's claim to high-impact novelty. If the decision is reconsidered, reviewers should adjudicate: whether PPPC-CN SP ratings are interpretable as patient-centeredness evidence; whether the omission of ERNIE Bot and the dataset relationship with the concurrent *npj Digital Medicine* paper require disclosure; and whether the two-condition design supports the governance conclusions advanced.

---

### 5. Suggested Reviewer Expertise

Reviewers should span: (1) standardized patient methodology and SP-based quality-of-care measurement in LMIC primary care settings, with familiarity with the PPPC-CN instrument's psychometric properties; (2) large language model evaluation in clinical contexts, specifically RLHF alignment mechanisms and their behavioral consequences in open-ended medical dialogue; (3) health economics and clinical safety measurement in low- and middle-income country primary care, particularly unnecessary test and medication prescribing in resource-constrained settings; (4) clinical primary care in China or comparable LMIC settings, capable of evaluating whether the unstable angina and asthma scripts reflect realistic PHC presentations; and (5) causal inference and experimental design for health services research, to adjudicate internal validity and the adequacy of the sensitivity analyses.

---

### 6. State-of-the-Art Literature Review

The most directly competing work is Google's AMIE study (Tu et al., *Nature*, 642:442–450, April 2025), which compared a fine-tuned LLM optimized for diagnostic dialogue against 20 primary care physicians using 159 OSCE-style SP cases across Canada, the UK, and India. AMIE outperformed physicians on diagnostic accuracy and 30 of 32 specialist-rated communication axes. A prospective feasibility extension of AMIE in an ambulatory primary care clinic (arXiv:2603.08448, 2025) has begun translating these OSCE findings to real workflows. Johri et al. introduced CRAFT-MD (*Nature Medicine*, 31:77–86, 2025), a conversational evaluation framework applied to GPT-4, GPT-3.5, Mistral, and LLaMA-2-7b across 12 specialties, demonstrating that LLM performance degrades substantially in multi-turn dialogues relative to static vignette benchmarks — a finding that should have informed the present study's interpretation of AI checklist adherence patterns. Williams et al. (*Nature Communications*, 2024, doi:10.1038/s41467-024-52415-1) documented that ChatGPT over-recommends tests and antibiotics in emergency department settings, providing a direct parallel for the over-testing finding reported here. The present manuscript must engage this study directly rather than attributing the pattern solely to RLHF sycophancy, as Williams et al. propose complementary mechanistic explanations. Ayers et al. (*JAMA Internal Medicine*, 183:589–596, 2023) provided foundational evidence that AI chatbot responses to patient social media queries were rated higher in quality and empathy than physician responses, establishing the communication advantage finding in a different ecological context. The most critical overlap is the concurrent simulated patient study by the same research group evaluating ERNIE Bot, ChatGPT-4o, and DeepSeek-R1 in the same Luohe PHC setting using the same disease scripts (*npj Digital Medicine*, September 2025). This study reports nearly identical findings — high AI diagnostic accuracy, high rates of over-prescription, and physician underperformance — using 40 SP trials per condition. The present manuscript's relationship to this prior publication is neither disclosed nor discussed, which constitutes a material transparency concern.

---

### 7. Suggested Reviewer Names

**SP methodology / primary care quality measurement:** Madhavi Bhargava (Public Health Foundation of India, SP methodology in LMICs); Neil Andersson (McGill University, community-based field experiment design); Hannah Leslie (Harvard T.H. Chan School of Public Health, primary care quality measurement in LMICs).

**LLM clinical evaluation:** Karan Singhal (Google DeepMind, AMIE and clinical LLM evaluation); Adam Rodman (Beth Israel Deaconess / Harvard, LLM diagnostic accuracy and clinical reasoning benchmarking).

**China PHC / clinical safety:** Winnie Yip (Harvard T.H. Chan, China health system reform and PHC quality); Karen Eggleston (Stanford, China healthcare economics and physician behavior).

---

### Further Literature

**1. Tu T, Schaekermann M, Palepu A, et al. Towards conversational diagnostic artificial intelligence. *Nature*. 2025;642:442–450.**
The closest methodological ancestor of this manuscript. Uses an OSCE-style SP paradigm to compare AMIE against 20 PCPs across 159 cases in Canada, UK, and India. AMIE outperformed physicians on diagnostic accuracy and 30 of 32 communication axes. Directly establishes the benchmark against which the present manuscript's novelty claims must be measured; the present study's main differentiation — in-person LMIC deployment and clinical safety outcomes — should be explicitly positioned against this work.

**2. Wang C, Si Y, Gong S, et al. Quality, safety and disparity of an AI chatbot in managing chronic diseases: simulated patient experiments. *npj Digital Medicine*. 2025. doi:10.1038/s41746-025-01956-w.**
A simulated patient study evaluating ERNIE Bot, ChatGPT-4o, and DeepSeek-R1 against primary care providers in Luohe, China, using the same two disease conditions (unstable angina and asthma) and same standardized protocols. Reports nearly identical findings: high AI diagnostic accuracy, over-prescribing exceeding 90%, and physician underperformance. The present manuscript's relationship to this study — same setting, same models, same scripts — is undisclosed and must be addressed.

**3. Johri S, Jeong J, Tran BA, et al. An evaluation framework for clinical use of large language models in patient interaction tasks. *Nature Medicine*. 2025;31:77–86.**
Introduces CRAFT-MD, a conversational evaluation framework applied to GPT-4, GPT-3.5, Mistral, and LLaMA-2-7b across 12 specialties using simulated AI patient agents. Demonstrates that LLM performance degrades substantially in multi-turn natural dialogue relative to static question-answering benchmarks. Directly relevant to interpreting why AI chatbots in the present study achieve high checklist adherence but concentrated on a narrow subset of items.

**4. Williams CYK, Mayer C, Theodorou M, et al. ChatGPT and emergency care: evaluating AI performance in acute clinical decision-making. *Nature Communications*. 2024. doi:10.1038/s41467-024-52415-1.**
Evaluated ChatGPT's clinical recommendations against emergency physicians on real ED cases, finding systematic over-recommendation of tests and antibiotics. Provides a cross-setting parallel to the over-testing signal in the present manuscript and proposes mechanistic explanations beyond RLHF sycophancy that the authors should engage.

**5. Si Y, Gong S, Chen S, et al. Quality and accountability of ChatGPT in health care in low- and middle-income countries: simulated patient study. *Journal of Medical Internet Research*. 2024;26:e56121.**
An early SP study using ChatGPT-3.5 across nine common diseases in an LMIC context, finding 74% diagnostic accuracy alongside 85% inappropriate medication rates. Establishes the safety-versus-accuracy tradeoff in the LMIC primary care context and is the direct pilot from which the present manuscript's design appears to derive; it is cited but not substantively engaged in the literature review.

**6. Goergen J, de Bellis E, Klesse AK. Reduced symptom reporting quality during human–chatbot versus human–physician interactions. *Nature Health*. 2026. doi:10.1038/s44360-026-00116-y.**
A pre-registered experiment (n=500) showing that participants assigned to report symptoms to a chatbot produce significantly lower-quality symptom reports than those reporting to a human physician. Directly complicates the present manuscript's interpretation of AI diagnostic superiority: if real patients provide degraded inputs to AI systems compared with scripted SP responses, the observed accuracy advantage may not transfer to naturalistic deployment. The use of SPs — who provide consistent, complete, and rehearsed symptom presentations — may systematically inflate AI performance relative to real-world conditions.

046211 Now I have everything needed. Here is the revised report:

---

## Editorial Report — Nature Communications (Digital Health)

**Manuscript:** Simplified Mortality Assessment Risk Tool for Neonates (SMART-NEO)

---

### 1. Overall Assessment

This manuscript presents SMART-NEO, a suite of three simplified machine-learning prognostic models — simplified XGBoost (sXGB), simplified Lasso logistic regression (sLR), and a decision tree (DT) — for predicting 7-day inpatient mortality in neonates at hospital admission. Models were developed on 7,016 neonates from nine Nigerian secondary-level hospitals and externally validated on 124,172 neonates from 21 Kenyan hospitals within the Clinical Information Network (CIN). Five predictors (SpO₂, admission weight, severe respiratory distress, lethargy/impaired consciousness, and feeding ability) were consistently retained across all model types. The central claim is that these models are methodologically rigorous, externally transportable, and implementation-ready for resource-constrained settings.

The study is methodologically disciplined, and its validation scale is genuinely distinctive. The principal concern is competitive novelty relative to the SENSS model and its CIN-based validation (Aluvaala et al., *Arch Dis Child* 2021; *BMC Medicine* 2022), which covers overlapping conceptual and empirical territory. With pooled external C-statistics of 0.82 (sLR) and 0.80 (sXGB), SMART-NEO does not clearly outperform the updated SENSS (C-statistic 0.834) on comparable CIN data. The manuscript does not include a direct head-to-head comparison on the same Kenyan cohort — the critical omission that must be resolved before this work can claim superiority over existing tools.

---

### 2. Strengths

The external validation design is the manuscript's strongest feature. Using 124,172 neonates from 21 geographically distinct Kenyan hospitals — substantially larger than any comparable LMIC neonatal validation cohort — the authors assess genuine geographic transportability. The membership model approach (C-statistics 0.67–0.70) formally quantifies cohort dissimilarity between the Nigerian development and Kenyan validation datasets, providing a principled basis for interpreting transportability rather than treating cross-country performance at face value.

The calibration analysis is rigorous and transparently reported. The authors employ smoothed LOESS calibration plots with 1,000-bootstrap confidence intervals, meta-analytic pooling of cluster-level performance using the REML estimator and Hartung-Knapp-Sidik-Jonkmann method, and a distinct recalibration step. Simultaneous optimisation of log-loss during hyperparameter tuning — rather than AUROC alone — reflects a principled attempt to jointly improve discrimination and calibration, which remains uncommon in clinical ML prediction studies from this setting.

The decision curve analysis is appropriately scoped. The pre-specified threshold range of 5–20% maps credibly onto resource heterogeneity in secondary-level African hospitals, and the contextual framing of threshold selection as a function of local resource availability is a substantive contribution to clinical deployability reasoning. The IECV design — with each hospital cluster held out in turn — is correct for clustered multi-site data, and integration of imputation within each fold avoids information leakage.

---

### 3. Weaknesses

The comparison with SENSS is inadequately resolved. The manuscript does not include a head-to-head performance comparison against SENSS or NETS on the same Kenyan CIN cohort. Without this, the claim that SMART-NEO represents an advance over existing tools cannot be empirically established. The authors acknowledge SENSS in discussion but dismiss its calibration challenges without testing whether recalibrated SENSS on the same data would perform comparably or better.

The development data derive from a clinical trial (Oxygen Implementation Project, 2016–2017) rather than routine care. The treatment variable was included as a candidate predictor due to a possible mortality effect, raising concerns about prediction-intervention conflation. Models developed on trial-enrolled patients with structured SpO₂ collection may not generalise to facilities where pulse oximetry availability differs substantially from trial protocols — particularly given that SpO₂ is simultaneously the most important predictor and the variable most likely to be absent in routine settings.

Fairness analysis is materially incomplete. Sex subgroup analyses are reported, but ethnicity, socioeconomic status, and gestational age strata are absent. This is consequential given the cross-national application: the 38.4% versus 10.6% birth asphyxia prevalence discrepancy between cohorts is striking and inadequately explained in clinical terms, suggesting case-mix differences that may confound predictor-outcome relationships beyond what the membership model C-statistic captures.

---

### 4. Editorial Decision

**Transfer to a lower-tier journal**, with *npj Digital Medicine* or *PLOS Medicine* as appropriate venues. The work is methodologically sound and the validation scale is notable, but the manuscript does not compellingly demonstrate superiority over the SENSS/NETS framework already validated in overlapping CIN facilities. The absence of a direct head-to-head performance comparison on the same Kenyan cohort is a critical analytical gap. Should the authors return with such a comparison and evidence that SMART-NEO offers meaningful incremental calibration or clinical utility over recalibrated SENSS, the case for Nature Communications could be revisited.

---

### 5. Suggested Reviewer Expertise

Reviewers should collectively cover: (1) clinical prediction model methodology in clustered multi-site designs, with specific expertise in internal-external cross-validation, calibration assessment, and meta-analytic pooling of cluster-level performance metrics; (2) machine learning approaches for tabular clinical data in low-resource settings, including XGBoost, Lasso regularisation, and decision tree simplification strategies; (3) decision curve analysis and clinical utility evaluation across heterogeneous threshold ranges; (4) neonatal clinical medicine in sub-Saharan African hospital systems, particularly secondary-level care environments with constrained oximetry and monitoring infrastructure; and (5) implementation science for clinical decision support tools in LMIC settings, with familiarity with WHO EENC and CIN-type surveillance platforms.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

Neonatal mortality prediction in LMICs has advanced substantially since 2021. The SENSS and NETS models (Aluvaala et al., *Arch Dis Child* 2021) established logistic regression-based prediction using admission clinical signs, and their 2022 external validation across 16 Kenyan CIN hospitals (*BMC Medicine* 2022) demonstrated C-statistics of 0.834 post-update, with improved calibration following logistic recalibration — the same updating strategy now used by SMART-NEO. A 2024 systematic review of neonatal death prediction scores (Veloso et al., *BMJ Paediatrics Open* 2024) characterised persistent methodological weaknesses across the field, including small derivation samples and inadequate calibration reporting — weaknesses this manuscript credibly addresses. A 2025 multi-country ML study (Santos Silva et al., *Scientific Reports* 2025) applied five ML algorithms to 575,664 pregnancies across the NIH Maternal and Neonatal Health Registry from 2010–2019, comparing generalised versus country-specific training strategies. In the NICU-specific context, a 2025 modelling competition (Sullivan et al., *Pediatric Research* 2025) benchmarked logistic regression, CatBoost, random forest, and XGBoost on over 6,000 NICU admissions and found no algorithm consistently dominated across outcome timepoints — a finding consistent with SMART-NEO's own observation that sLR performs comparably to or better than sXGB on several metrics despite lower algorithmic complexity. Against this landscape, SMART-NEO's external validation at scale is a credible advance, but its discriminative performance does not clearly exceed the updated SENSS on comparable facilities.

---

### Further Literature

The following papers from the past three years share direct scope with SMART-NEO and should be engaged by the authors:

1. **Veloso FCS, Barros CRA, Kassar SB, Gurgel RQ.** Neonatal death prediction scores: a systematic review and meta-analysis. *BMJ Paediatrics Open* 8(1): e003067 (2024). DOI: 10.1136/bmjpo-2024-003067. — Provides the most current systematic characterisation of neonatal mortality prediction scores, directly establishing the methodological gaps SMART-NEO claims to address; required reading for contextualising the authors' novelty argument.

2. **Santos Silva GF, Wichmann RM, da Silva Junior FC, Chiavegatto Filho ADP.** Development and evaluation of machine learning training strategies for neonatal mortality prediction using multicountry data. *Scientific Reports* 15: 24278 (2025). DOI: 10.1038/s41598-025-04066-5. — Benchmarks five ML algorithms on 575,664 pregnancies across the NIH MNHR multicountry registry, comparing generalised and country-specific training strategies; directly overlaps with SMART-NEO's cross-national generalisation claims.

3. **Sullivan BA, Moreira AG, McAdams RM, et al.** Comparing machine learning techniques for neonatal mortality prediction: insights from a modeling competition. *Pediatric Research* 98: 405–411 (2025). DOI: 10.1038/s41390-024-03773-5. — Head-to-head benchmark of logistic regression, CatBoost, neural networks, random forest, and XGBoost on over 6,000 NICU admissions; provides a methodological reference point for SMART-NEO's algorithm comparison design, though conducted in a high-income NICU setting.

4. **Aluvaala J, et al.** External validation of inpatient neonatal mortality prediction models in high-mortality settings. *BMC Medicine* 20: 265 (2022). DOI: 10.1186/s12916-022-02439-5. — External validation of SENSS and NETS across 16 Kenyan CIN hospitals, achieving post-recalibration C-statistics of 0.834; the most directly competing work that SMART-NEO must benchmark against on the same dataset to substantiate its novelty claims.

5. **Neal SR, Sturrock SS, Musorowegomo D, et al.** Clinical prediction models to diagnose neonatal sepsis in low-income and middle-income countries: a scoping review. *BMJ Global Health* 10: e017582 (2025). DOI: 10.1136/bmjgh-2024-017582. — Scoping review of 44 distinct clinical prediction models for neonatal conditions in LMICs; situates the methodological and generalisability standards to which new LMIC neonatal prediction models are now expected to conform.

6. **Zeng Z, Shi Z, Li X.** Comparing different scoring systems for predicting mortality risk in preterm infants: a systematic review and network meta-analysis. *Frontiers in Pediatrics* (2023). DOI: 10.3389/fped.2023.1287774. — Network meta-analysis of eight neonatal severity scoring systems including CRIB, SNAP-II, and SNAPPE-II; provides the broader comparative landscape of validated neonatal mortality scores against which the added value of ML-based approaches such as SMART-NEO should be assessed.

---

### 7. Suggested Reviewer Names

**Clinical prediction modelling / IECV / calibration:**
Gary Collins (University of Oxford), Maarten van Smeden (Utrecht University), Ben Van Calster (KU Leuven), Richard Riley (University of Birmingham)

**ML for clinical tabular data in low-resource settings:**
Leo Celi (MIT / Beth Israel Deaconess), Danielle Belgrave (DeepMind / Imperial College London), Abdulhakim Abdi (University of Edinburgh), Trishan Panch (Wellcome Leap)

**Neonatal clinical medicine / LMIC hospital systems:**
Jalemba Aluvaala (KEMRI-Wellcome Trust, Nairobi), Mike English (KEMRI-Wellcome Trust / Oxford), Adejumoke Idowu Ayede (University of Ibadan), Charles Rotich (Moi University, Kenya)

**Implementation science / clinical decision support:**
Naomi Fowler (London School of Hygiene & Tropical Medicine), David Mphuthi (University of Pretoria), Zeshan Qureshi (London School of Hygiene & Tropical Medicine)
