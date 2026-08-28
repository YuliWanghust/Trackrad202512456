# Trackrad202512456

070064
# Editorial Report: Trauma-TCNFormer

## Editorial Integrity Alert — Handling Editor Only

The code URL currently returns 404 and should be resolved before review. References 12 and 16 duplicate the same 2022 systematic review; this appears to be a bibliography-quality issue rather than evidence of fabrication.

## 1. Overall Assessment

Trauma-TCNFormer combines temporal convolution, a two-layer four-head Transformer and attention pooling to predict rolling 28-day mortality from 30 variables in 3,644 MIMIC-IV trauma ICU stays, expanded to 19,940 ICU-day records. Test AUROC is 0.7867. Learned embeddings are clustered into four states and linked into patient trajectories.

The trajectory framework and transcriptomic contextualization are interesting, but the study does not establish a sufficiently robust advance. The decisive concerns are endpoint construction, absent external clinical validation, and incomplete benchmarking against prior dynamic trauma models.

## 2. Strengths

The 70/15/15 split is performed by base hospital admission, preventing repeated ICU-day records from crossing splits. Training-only standardization, explicit time intervals, missingness masks and padding are appropriate safeguards for irregular EHR data.

The architecture is coherent, and ablation identifies perfusion/blood-gas and renal/metabolic modules as major contributors. Four K-means states show graded mortality across splits and yield interpretable recovery, deterioration and persistent high-risk trajectories.

GSE36809 provides independent biological context, linking persistent molecular perturbation to innate inflammatory/complement activation and adaptive immune suppression.

## 3. Weaknesses

The 28-day label is problematic. ICU days are retained as positive only when within 28 days before death; earlier days from eventual decedents are discarded, whereas all survivor days are retained. This alters the risk set and makes the main AUROC a record-level rather than clean patient-level 28-day estimate. A landmark or time-to-event design with explicit censoring is needed.

All clinical validation remains within MIMIC-IV from one academic center. No external cohort or subgroup performance by age, sex, race/ethnicity, injury mechanism or severity is reported. Test precision is 0.3784 and F1 is 0.4549, with no decision-curve analysis.

Benchmarking omits LSTM/GRU, stronger Transformer baselines, and direct ISS/NISS/RTS/TRISS comparisons. Prior dynamic MIMIC-III trauma work reported AUROC 0.929, so the manuscript overstates the field’s reliance on static prediction.

The latent-state biology is partly circular because K-means is applied to embeddings optimized for mortality. Cluster stability and alternative K values are not shown. GSE36809 contains different patients and therefore provides biological plausibility, not validation of the four EHR states.

## 4. Editorial Decision

Reject. The outcome-sampling design, single-center validation and incomplete prior-art comparison materially limit validity and novelty. A redesigned study with survival/landmark evaluation, multicenter validation and stronger baselines may be more appropriate for *Communications Medicine*.

## 5. Suggested Reviewer Expertise

Relevant expertise is longitudinal EHR Transformers; dynamic survival modeling; latent-state phenotyping and cluster stability; trauma/surgical critical care; and trauma immunogenomics.

## 6. State-of-the-Art Literature Review — Past 3 Years

Recent work sets a higher validation bar. Park et al. reported prospective use of the hourly Parkland Trauma Index of Mortality in 2024. Rong et al. introduced the Transformer-based TECO model in 2025 with external disease-cohort evaluation. Oh et al. reported a 2026 trauma model trained on 204,189 patients and externally validated across South Korean and Australian centers, with AUROC 0.895 in Australia. A 2026 cross-database trauma preprint by Kudrot et al. achieved AUROC 0.825 in 13,747 MIMIC-IV stays. Trauma-TCNFormer adds richer trajectory interpretation, but its single-database test AUROC of 0.7867 does not exceed this standard. Tsiklidis, Sinno and Diamond’s 2022 dynamic MIMIC-III trauma study is older than three years but remains directly relevant prior art.

## 7. Suggested Reviewer Names

For longitudinal EHR modeling: Ruichen Rong, Jinseok Lee and Bobak Mortazavi. For trauma AI: Caroline Park, Zongyang Mou and Na-Eun Oh. For dynamic trauma-risk validation: Evan J. Tsiklidis, Maryam Pishgar and Nausin Kudrot. For trauma molecular endotyping: Matthew R. Thau, Eric D. Morrell and Pavan K. Bhatraju. Author identities are not visible in the supplied manuscript, so all names require standard conflict checks.

069953
# Editorial Report — Manuscript 069953

## 1. Overall Assessment

PROMISE introduces a “Store Low, View High” archival framework in which low-resolution WSI pyramid levels are retained and high-resolution regions are reconstructed on demand using MorphoDiff, a deterministic single-step diffusion model. The manuscript claims 93.5% storage reduction while preserving morphology, downstream computational performance, and pathologist interpretation.

Unlike a conventional super-resolution benchmark, the study evaluates 14 AI tasks, out-of-distribution cohorts, retrospective multi-centre reader studies, and a prospective 200-patient breast cohort. The main editorial questions are whether the evidence supports equivalence rather than concordance and whether the storage strategy remains sufficiently distinctive relative to recent WSI compression methods.

## 2. Strengths

MorphoDiff combines CONCH-based morphological-consistency loss, scale-aware conditioning, adversarial optimization, online negative prompting, and single-step diffusion. Validation spans diagnosis, prognosis, molecular prediction, segmentation, treatment-response prediction, and OOD organs. Human evaluation is substantive: three pathologists assessed 320 retrospective cases, followed by the prospective breast cohort, where HR-SR concordance reached Cohen’s κ=0.922 for invasive-carcinoma classification and QWK=0.938 for grading.

## 3. Weaknesses

The statistical framework does not formally establish non-inferiority. Across 14 tasks, the pooled LMM detects an SR-HR difference (p=0.042), while external cohorts (p=0.020) and OOD organs (p=0.037) also retain significant differences; p=0.053 after modality-specific retraining is not evidence of equivalence. A prespecified non-inferiority margin is needed.

The storage comparison is incomplete. The approximately 15-fold reduction largely follows from retaining a fourfold-downsampled pyramid level, without matched-storage comparisons against systems such as AdaSlide or PathoLIC. Generalizability is further limited by predominantly TCGA-derived pretraining, H&E-only evaluation, a single-centre prospective cohort, and absent demographic subgroup analyses.

## 4. Editorial Decision

**Send for Review.** The combination of morphology-constrained reconstruction, downstream testing, OOD evaluation, reader studies, and prospective validation is sufficiently distinctive for external assessment. Reviewers should adjudicate the non-inferiority claim and whether PROMISE provides a genuine infrastructural advance over modern pathology compression systems.

## 5. Suggested Reviewer Expertise

Reviewers should include expertise in diffusion-based histopathology super-resolution and generative image restoration; learned and content-adaptive WSI compression; computational pathology foundation-model feature spaces and morphology-preserving metrics; statistical design of diagnostic non-inferiority and reader studies; and clinical digital pathology, particularly WSI archiving, grading, scanner variability, and diagnostic workflow implementation.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Recent work has moved WSI compression evaluation beyond PSNR and visual appearance. Fischer et al. showed that neural compression can introduce dataset-dependent biases and proposed feature-similarity measures linked to downstream performance. AdaSlide subsequently combined reinforcement-learning-based region selection with a foundational image enhancer and preserved performance across 13 downstream tasks while reducing storage to 10–35% of the original size. PathoLIC introduced content-aware variable-rate learned compression and reported more than eightfold compression beyond standard SVS while maintaining several downstream tasks. In parallel, SuperDiff established diffusion-based pathology SR with histology-specific evaluation.

PROMISE advances this landscape through unusually extensive human and downstream clinical validation and explicit morphology-constrained reconstruction. However, the conceptual “low-resolution archive plus on-demand SR” paradigm is no longer unique. Yang et al. independently described a fallback-safe WSI archival system with approximately 93% space reduction and on-demand reference-based super-resolution in 2026. This directly competing work should be discussed, and comparison with AdaSlide and PathoLIC is needed to establish the incremental contribution of PROMISE as a compression strategy.

## 7. Suggested Reviewer Names

Prateek Prasanna, Stony Brook University, would be appropriate for diffusion-based digital pathology and is senior author of the recent SuperDiff work. Maximilian Fischer, German Cancer Research Center, is directly relevant through recent studies benchmarking diagnostic fidelity and learned WSI compression. Peter Neher, DKFZ, is also suitable for pathology-specific compression methodology and feature-based fidelity assessment. Sangjeong Ahn, Korea University, provides the desired clinical-digital-pathology perspective and co-developed AdaSlide, the most direct recent Nature Communications comparator.

## Further Literature: 10 Closely Related Papers from the Past 3 Years

The following papers were selected for close methodological overlap with PROMISE in WSI compression, low-resolution archival, super-resolution reconstruction, generative pathology restoration, or diagnostic-fidelity assessment. Citation status was checked against the manuscript reference list.

1. **Lee, J., Takemaru, L., Bappy, D.M., et al. Adaptive compression framework for giga-pixel whole slide images. Nature Communications 17, 207 (2026). DOI: 10.1038/s41467-025-66889-0.** Peer-reviewed journal article. **Cited by manuscript: Yes, Ref. 9.** **Author independence: Yes; no submitting-author overlap identified.** AdaSlide is one of the most important direct competitors because its Compression Decision Agent adaptively downscales WSI regions and its Foundational Image Enhancer reconstructs image fidelity, while evaluating 13 downstream tasks and pathologist perception. Its 10–35% retained-storage regime provides an essential matched-purpose comparator for PROMISE.

2. **Li, W., Li, Y., Chen, H., et al. A content-aware variable-rate framework for pathology learned image compression (PathoLIC). Medical Image Analysis 111, 104018 (2026). DOI: 10.1016/j.media.2026.104018.** Peer-reviewed journal article. **Cited by manuscript: Yes, Ref. 11.** **Author independence: Yes.** PathoLIC assigns pathology-content scores to WSI patches, applies adaptive variable-rate learned compression, exploits spatial redundancy through attention, and evaluates downstream WSI-, patch-, and cell-level tasks. It directly challenges PROMISE's claim that low-resolution storage plus reconstruction is the preferred route to scalable pathology archiving.

3. **Yang, W., Shin, S., Zhu, R.Y., Wang, Z. Whole-Slide Image Compression and On-Demand Viewing using Reference-Based Super-Resolution. Journal of Computational Vision and Imaging Systems 11(1), 91–95 (2026). DOI: 10.15353/jcvis.v11i1.10017.** Peer-reviewed journal/proceedings article. **Cited by manuscript: No.** **Author independence: Yes.** This is arguably the closest conceptual competitor. It stores a reduced WSI representation, reports approximately 93% space reduction, retains a fallback-safe conventional image, and reconstructs additional detail on demand through reference-based super-resolution. The journal explicitly states that submissions undergo peer review.

4. **Xu, X., Kapse, S., Prasanna, P. SuperDiff: A diffusion super-resolution method for digital pathology with comprehensive quality assessment. Medical Image Analysis 107, 103808 (2026). DOI: 10.1016/j.media.2025.103808.** Peer-reviewed journal article. **Cited by manuscript: Yes, Ref. 15.** **Author independence: Yes.** SuperDiff is the strongest recent pathology-specific diffusion-SR comparator. It combines histopathological priors with controllable diffusion and emphasizes pathology-specific quality assessment rather than natural-image metrics alone. PROMISE advances beyond it mainly through storage framing, whole-slide downstream evaluation, and reader validation.

5. **Fischer, M., Neher, P., Schüffler, P., et al. Unlocking the potential of digital pathology: Novel baselines for compression. Journal of Pathology Informatics 17, 100421 (2025). DOI: 10.1016/j.jpi.2025.100421.** Peer-reviewed journal article. **Cited by manuscript: No.** **Author independence: Yes.** This study jointly evaluates perceptual fidelity and downstream performance across four histopathology datasets and demonstrates that learned compression may inherit compression-artifact biases. Its feature-similarity metric correlates with downstream performance. This paper is particularly relevant to PROMISE's reliance on morphology-aware feature-space evaluation.

6. **Yellapragada, S., Graikos, A., Triaridis, K., et al. Pathology Image Compression with Pre-trained Autoencoders. Medical Image Computing and Computer Assisted Intervention—MICCAI 2025, LNCS 15961, 442–452. DOI: 10.1007/978-3-032-04937-7_42.** Peer-reviewed conference paper. **Cited by manuscript: No.** **Author independence: Yes.** The study repurposes latent-diffusion autoencoders for histopathology compression, fine-tunes reconstruction with pathology foundation-model perceptual features, and evaluates segmentation, patch classification, and multiple-instance learning. It is an important alternative to PROMISE because it compresses into learned latent representations rather than storing standard low-resolution WSI imagery.

7. **Huang, L., Li, Y., Pillar, N., et al. A robust and scalable framework for hallucination detection in virtual tissue staining and digital pathology. Nature Biomedical Engineering 9, 2196–2214 (2025). DOI: 10.1038/s41551-025-01421-9.** Peer-reviewed journal article. **Cited by manuscript: Yes, Ref. 20.** **Author independence: Yes.** Although focused on virtual staining rather than SR, AQuA directly addresses the central safety problem facing PROMISE: generative models can produce realistic histological structures that conventional PSNR-like metrics fail to detect. AQuA achieved 99.8% accuracy for acceptable versus unacceptable generated pathology images and high agreement with pathologists, making it a relevant benchmark for hallucination-control claims.

8. **Barsi, A., Nayak, S.C., Parida, S., et al. A deep learning-based compression and classification technique for whole slide histopathology images. International Journal of Information Technology 16, 4517–4526 (2024). DOI: 10.1007/s41870-024-01945-4.** Peer-reviewed journal article. **Cited by manuscript: No.** **Author independence: Yes.** This work uses supervised compressive autoencoders to retain diagnostically meaningful histopathology representations and evaluates reconstructed data through transfer-learning classifiers. Its clinical validation is much narrower than PROMISE, but it represents relevant prior art linking compression quality to downstream classification rather than purely pixel-level metrics.

9. **Afshari, M., Yasir, S., Keeney, G.L., Jimenez, R.E., Garcia, J.J., Tizhoosh, H.R. Single patch super-resolution of histopathology whole slide images: a comparative study. Journal of Medical Imaging 10(1), 017501 (2023). DOI: 10.1117/1.JMI.10.1.017501.** Peer-reviewed journal article. **Cited by manuscript: Yes, Ref. 14.** **Author independence: Yes.** This comparative study directly evaluates histopathology WSI super-resolution motivated by the storage and acquisition burden of high magnification. It provides an important pre-diffusion baseline showing both the promise and limitations of reconstructing diagnostically useful high-resolution pathology from lower-resolution inputs.

10. **Rong, R., Wang, S., Zhang, X., et al. Enhanced Pathology Image Quality with Restore–Generative Adversarial Network. American Journal of Pathology 193(4), 404–416 (2023). DOI: 10.1016/j.ajpath.2022.12.011.** Peer-reviewed journal article. **Cited by manuscript: No.** **Author independence: Yes.** Restore-GAN addresses low resolution, blur, and staining variation in pathology images and demonstrates that restoration can improve robustness of existing downstream pathology algorithms. It is less directly concerned with archival storage than PROMISE, but closely overlaps with the manuscript's claim that generative reconstruction can restore diagnostically useful morphology rather than merely improve perceptual appearance.

**Editorial implication of the additional literature.** The strongest novelty pressure comes from AdaSlide, PathoLIC, Fischer et al., Yellapragada et al., and especially Yang et al. The Yang paper is conceptually very close to PROMISE because both explicitly combine reduced WSI storage with high-resolution reconstruction on demand and report storage savings near 93%. PROMISE nevertheless appears stronger in clinical validation, particularly its 14 downstream tasks, OOD organ analysis, multi-centre pathologist evaluation, and prospective breast cohort. For peer review, the critical issue is therefore not whether PROMISE works, but whether its morphology-constrained diffusion architecture and depth of clinical validation constitute a sufficiently substantial advance over these rapidly converging compression-and-reconstruction paradigms.

069912
# Editorial Report — Manuscript 069912

## 1. Overall Assessment

This manuscript tests whether independently trained wearable-sensor foundation models contain shared, interpretable physiological structure. Three 256-dimensional models (PPG ViT, PPG EfficientNet, accelerometer ViT), pretrained on about 20 million minutes from the Apple Heart and Movement Study (AHMS), are decomposed with PCA, ICA, NMF and sparse autoencoders, then aligned using bijective matching, CCA or sparse CCA. Evaluation uses a 30,000-subject cohort excluded from pretraining and 23 binary health targets. Cross-modal transfer retains more than 95% of in-domain AUROC for the strongest alignments.

The central concern is whether this reflects modality-independent physiological convergence or shared AHMS-specific covariance. Because all models and evaluation data come from the same study population and device ecosystem, the manuscript cannot cleanly separate physiological invariance from recruitment, device and behavioral structure.

## 2. Strengths

The evaluation design is comparatively rigorous. Symbol operators and downstream classifiers are fitted on an operator split and tested on a frozen evaluation split, reducing direct leakage.

The phenomenon is examined across two modalities, two PPG architectures, multiple extraction methods and several alignment strategies. Blood type serves as a negative control, while age, sex and BMI provide a confounder-only baseline. Transfer is approximately symmetric between modalities, and sparse CCA preserves most alignment while using fewer active weights.

## 3. Weaknesses

External validity is inadequate for the main claim. Independent cohorts, devices or acquisition settings are needed to establish that the recovered structure is genuinely physiological rather than AHMS-specific.

Semantic validation is also limited. Broad self-reported health categories, subject-level averaging and descriptive symbol–target associations do not demonstrate mechanistic interpretability. Ethnicity and socioeconomic subgroup analyses, confidence intervals and calibration are not reported. Methodological novelty is moderate because the framework relies mainly on established PCA, ICA, NMF and CCA variants.

## 4. Editorial Decision

**Reject, with transfer to npj Artificial Intelligence.** The scale, controls and held-out evaluation are strengths, but the same-study design leaves the principal convergence claim insufficiently resolved for Nature Communications.

## 5. Suggested Reviewer Expertise

Relevant expertise includes wearable biosignal foundation models; cross-modal representation alignment and CCA; mechanistic interpretability and sparse latent decomposition; and clinical digital-biomarker validation, including confounding and subgroup robustness.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Recent work has raised the bar for wearable foundation models. Abbaspourazad et al. introduced large-scale PPG/ECG foundation models at ICLR 2024. ([mlanthology.org](https://mlanthology.org/iclr/2024/abbaspourazad2024iclr-largescale/?utm_source=chatgpt.com)) Narayanswamy et al. demonstrated wearable-model scaling laws using up to 40 million hours from more than 165,000 people at ICLR 2025. ([proceedings.iclr.cc](https://proceedings.iclr.cc/paper_files/paper/2025/hash/94b25992757a549470c8f8dfe73d8df6-Abstract-Conference.html?utm_source=chatgpt.com)) PaPaGei provided an open PPG foundation model with out-of-domain evaluation, while NormWear tested multivariate physiological representations across 11 public datasets and 18 applications. ([mlanthology.org](https://mlanthology.org/iclr/2025/pillai2025iclr-papagei/?utm_source=chatgpt.com)) The present work adds post-hoc alignment without joint training, but should engage more directly with these generalization-focused studies and with recent sparse-autoencoder interpretability work that validates medical FM concepts beyond the training domain. ([arxiv.org](https://arxiv.org/abs/2407.10785?utm_source=chatgpt.com))

## 7. Suggested Reviewer Names

Arvind Pillai, based on PaPaGei and open PPG foundation-model evaluation; Girish Narayanswamy, based on *Scaling Wearable Foundation Models*; Yunfei Luo, based on NormWear and physiological representation alignment; and Chanwoo Kim, based on recent concept-level interpretability work for medical foundation-model embeddings, would provide complementary and methodologically relevant expertise. ([mlanthology.org](https://mlanthology.org/iclr/2025/pillai2025iclr-papagei/?utm_source=chatgpt.com))

069900
# Editorial Report — Manuscript 069900

### Editorial Integrity Alert — Handling Editor Only

Reference 19 is explicitly marked as retracted but is cited in the Introduction to support the clinical analogy motivating asymmetric collaboration. The underlying *BioMed Research International* article was retracted following identification of indicators of systematic publication manipulation. This reference should be removed and the argument independently re-supported before review. ([pmc.ncbi.nlm.nih.gov](https://pmc.ncbi.nlm.nih.gov/articles/PMC9371885/?utm_source=chatgpt.com))

## 1. Overall Assessment

The manuscript introduces PFL-AC, which replaces a single global model with client-customised proxy models and learns an asymmetric pairwise contribution matrix; Lay-PFL-AC extends this relation layer-wise. The conceptual contribution is distinctive because collaboration is directed rather than assumed reciprocal. However, the central medical experiment assigns seven MIDOG++ tumour domains to simulated “hospitals,” and performance is summarized using the highest or peak accuracy reached during training. These design choices substantially weaken the clinical and statistical claims.

## 2. Strengths

PFL-AC explicitly estimates directed client-support relationships from gradients and uses them to steer personalised model updates. The layer-wise extension increases the granularity of collaboration modelling.

The empirical comparison is broad, covering Per-FedAvg, FedRep, FedCP, FedAS, FedFomo, FedAMP, FedPHP and FedALA across MIDOG++, four MedMNIST datasets and general benchmarks, including 50- and 100-client simulations. Public datasets and an accessible GitHub implementation also support reproducibility.

## 3. Weaknesses

The medical validation is synthetic rather than genuinely multi-institutional. MIDOG++ domains are remapped to simulated clients, while MedMNIST heterogeneity is generated by Dirichlet partitioning. This does not establish robustness under real institutional differences in governance, prevalence, acquisition workflow, or patient mix.

The evaluation is potentially optimistic because Figures 2 and 3 emphasize the highest or peak training accuracy without a clearly independent model-selection procedure. Only three runs are reported, without confidence intervals, paired statistical tests, calibration, or rigorous uncertainty analysis.

Privacy and scalability claims are also under-supported. Raw-data locality is not a formal privacy guarantee, and the \(K\times K\) or \(K\times K\times L\) relation structures raise scaling concerns beyond the tested 100-client setting.

## 4. Editorial Decision

Reject. The method is technically plausible, but simulated institutional partitions, optimistic model selection, and incomplete statistical validation prevent the medical claims from meeting the Nature Communications threshold. Transfer to *npj Artificial Intelligence* would be more appropriate after genuine multi-site validation and a fixed, statistically rigorous testing protocol.

## 5. Suggested Reviewer Expertise

Relevant expertise includes personalised federated optimisation under non-IID data, asymmetric client collaboration and contribution estimation, federated medical imaging, privacy and security of model-update exchange, and cross-domain computational pathology.

## 6. State-of-the-Art Literature Review — Past 3 Years

Recent work already models client relationships directly. Wu et al. use marginal contributions and coalition game theory for personalised client collaboration in *IEEE Transactions on Mobile Computing* (2024); Liu et al. develop directed asymmetric collaboration in DFedPGP at CVPR 2024; and PFedCS uses classifier similarity for adaptive collaboration at AAAI 2025. ([researchportal.hkust.edu.hk](https://researchportal.hkust.edu.hk/en/publications/rethinking-personalized-client-collaboration-in-federated-learnin/?utm_source=chatgpt.com)) In medical FL, Jiang et al. estimate client contribution in gradient and data space, while Wang et al. demonstrate that personalization does not necessarily improve demographic fairness. ([openaccess.thecvf.com](https://openaccess.thecvf.com/content/CVPR2023/html/Jiang_Fair_Federated_Medical_Image_Segmentation_via_Client_Contribution_Estimation_CVPR_2023_paper.html?utm_source=chatgpt.com))

PFL-AC’s strongest novelty is its continuously learned directed contribution matrix coupled to client-specific proxy models. However, superiority over these newer relationship-aware approaches is not shown under genuine institutional heterogeneity, despite MIDOG++ being explicitly designed around laboratory, scanner, species and tumour-domain shifts. ([nature.com](https://www.nature.com/articles/s41597-023-02327-4?utm_source=chatgpt.com))

## 7. Suggested Reviewer Names

For personalised client collaboration, suitable candidates include Leijie Wu, Yaohong Ding and Yingqi Liu. For contribution-aware medical federated learning, Meirui Jiang, Ziyue Xu and Tongnian Wang are relevant. For MIDOG++ and cross-domain digital pathology, Marc Aubreville, Frauke Wilm and Christof A. Bertram are appropriate candidates. ([researchportal.hkust.edu.hk](https://researchportal.hkust.edu.hk/en/publications/rethinking-personalized-client-collaboration-in-federated-learnin/?utm_source=chatgpt.com))

## 1. Overall Assessment

The manuscript presents Dynomap, an end-to-end framework that converts unordered biomedical tabular data into task-optimized two-dimensional maps through feature gating, trainable spatial coordinates, differentiable Gaussian rendering, and a CNN predictor. It is tested across circulating RNA, platelet RNA, TCGA-BRCA, Parkinson’s voice measurements, Tabula Muris single-cell RNA-seq, and 13 additional tabular datasets.

The contribution is more substantial than a routine benchmark because spatial organization is learned jointly with prediction rather than imposed from fixed feature similarity. The main concerns are validation independence and whether the claimed advance holds against the closest recent tabular-to-image methods.

## 2. Strengths

Dynomap integrates feature selection, spatial arrangement, rendering, and downstream prediction within one differentiable objective. Moran’s I, k-nearest-neighbour spatial coherence, and Integrated Gradients provide explicit analysis of learned structure.

The evaluation is broad. Reported results include 93.0% binary cancer-versus-control accuracy with 4,000 highly variable genes, 92.0% multiclass cancer-subtype accuracy using the 622-gene panel, and 93.7% Parkinson classification accuracy. Comparisons include logistic regression, random forest, XGBoost, SVM, MLP, ModernNCA, TabM and TabPFN.

## 3. Weaknesses

Most biomedical results remain retrospective and internally cross-validated, with no independent external cohort establishing robustness to institution, assay, or batch shifts. The Parkinson dataset contains repeated recordings per participant, yet the manuscript does not clearly document participant-grouped folds; recording-level splitting would create subject leakage. Similar donor-level safeguards should be explicit for single-cell experiments.

The closest tabular-to-image baselines are incomplete. HACNet, MRep-DeepInsight, LM-IGTD, NCTD and recent systematic tabular-to-image benchmarks provide direct tests of whether task-adaptive cartography is genuinely superior. Calibration, confidence intervals and AUROC/PR-AUC are also inconsistently reported.

## 4. Editorial Decision

**Send for Review.** The differentiable, task-adaptive feature cartography is sufficiently distinctive for external assessment. Reviewers should determine whether subject/donor-disjoint validation preserves performance and whether direct comparison with contemporary tabular-to-image methods supports the novelty claim.

## 5. Suggested Reviewer Expertise

Suitable expertise includes deep learning and foundation models for tabular data; differentiable tabular-to-image representation learning and CNN architectures; explainability and spatial-statistical analysis of learned representations; computational genomics and cfRNA liquid biopsy; and machine-learning analysis of Parkinsonian speech biomarkers.

## 6. State-of-the-Art Literature Review — Past 3 Years

The tabular-learning field has advanced rapidly through TabR at ICLR 2024, TabPFN in *Nature* 2025, TabM at ICLR 2025 and TabICL at ICML 2025. These methods establish increasingly strong retrieval, ensemble and foundation-model baselines. Concurrently, NCTD and LM-IGTD have extended tabular-to-image learning, while recent systematic benchmarking questions whether image conversion consistently improves upon strong tabular learners. Dynomap advances this literature by making feature placement task-adaptive and differentiable. Its novelty therefore rests less on tabular-to-image conversion itself than on demonstrating that learned cartography provides reproducible gains over both modern tabular models and the strongest image-conversion alternatives.

## 7. Suggested Reviewer Names

Yury Gorishniy would provide expertise in modern tabular architectures through TabR and TabM. Francisco J. Lara-Abelenda is directly relevant through recent biomedical tabular-to-image and LM-IGTD work. Amir Momen-Roknabadi provides clinically relevant expertise in AI-based cell-free RNA cancer detection with independent-cohort validation. Juan Rafael Orozco-Arroyave is highly relevant to Parkinsonian speech modeling and cross-cohort generalization. A targeted search identified no obvious coauthorship between these candidates and the submitting author group.

## Further Literature — 10 Closely Related Papers Published in the Past 3 Years

1. **Bragilovski M, Kapri Z, Rokach L, Levy-Tzedek S. “TLTD: Transfer Learning for Tabular Data.” *Applied Soft Computing* 147, 110748 (2023). DOI: 10.1016/j.asoc.2023.110748.** Peer-reviewed. **Cited by manuscript:** No, not identified in references 1–98. **Independence:** no submitting-author overlap identified. **Relevance:** converts tabular data to images and combines the representation with transfer learning and knowledge distillation across 25 structured datasets. It is a direct conceptual predecessor for exploiting image-network inductive biases on non-image data.

2. **Medeiros Neto L, Rogerio da Silva Neto S, Endo PT. “A comparative analysis of converters of tabular data into image for the classification of Arboviruses using Convolutional Neural Networks.” *PLOS ONE* 18, e0295598 (2023). DOI: 10.1371/journal.pone.0295598.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** directly compares IGTD and alternative tabular-to-image converters in a biomedical classification setting and therefore provides an important benchmark for Dynomap’s representation claims.

3. **Matsuda T, Uchida K, Saito S, Shirakawa S. “HACNet: End-to-end learning of interpretable table-to-image converter and convolutional neural network.” *Knowledge-Based Systems* 284, 111293 (2024). DOI: 10.1016/j.knosys.2023.111293.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** probably the closest methodological comparator. HACNet jointly trains a hard-attention table-to-image converter and CNN using prediction loss, making the absence of a direct Dynomap-versus-HACNet experiment particularly notable.

4. **Sharma A, López Y, Jia S, Lysenko A, Boroevich KA, Tsunoda T. “Enhanced analysis of tabular data through Multi-representation DeepInsight.” *Scientific Reports* 14, 12851 (2024). DOI: 10.1038/s41598-024-63630-7.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** extends DeepInsight through multiple spatial representations and evaluates single-cell RNA-seq, ATAC-seq and Alzheimer’s molecular data using ResNet-50 and EfficientNet-B6, closely overlapping Dynomap’s high-dimensional biomedical use case.

5. **Lara-Abelenda FJ, Chushig-Muzo D, Peiro-Corbacho P, Gómez-Martínez V, Wägner AM, Granja C, Soguero-Ruiz C. “Transfer learning for a tabular-to-image approach: A case study for cardiovascular disease prediction.” *Journal of Biomedical Informatics* 165, 104821 (2025). DOI: 10.1016/j.jbi.2025.104821.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** applies LM-IGTD to clinical tabular data and explicitly compares CNN-based tabular-to-image learning with TabPFN and conventional models. It is highly relevant to Dynomap’s biomedical generalizability claims.

6. **Alenizy HA, Berri J. “Transforming tabular data into images via enhanced spatial relationships for CNN processing.” *Scientific Reports* 15, 17004 (2025). DOI: 10.1038/s41598-025-01568-0.** Peer-reviewed. **Cited by manuscript:** **Yes, reference 32.** **Independence:** no author overlap identified. **Relevance:** introduces NCTD and benchmarks it against IGTD, DeepInsight, REFINED, TINTO, HACNet and Fotomics on ten datasets. Although cited, it is not included as an experimental comparator and therefore remains directly relevant to the novelty assessment.

7. **Lee J, Kim B. “Zero inflated high dimensional compositional data with DeepInsight.” *PLOS ONE* 20, e0320832 (2025). DOI: 10.1371/journal.pone.0320832.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** adapts tabular-to-image representation learning to zero-inflated high-dimensional biomedical compositional data and validates the approach on paediatric inflammatory bowel disease data, providing another genomics-adjacent comparator.

8. **Selke WD, Sung H, Lee C, Whooley M, Kim W. “Exploring Tabular-to-Image Algorithms for Applying CNNs to Tabular Data.” *IEEE International Conference on Bioinformatics and Biomedicine (BIBM)*, 5066–5073 (2025). DOI: 10.1109/BIBM66473.2025.11356899.** Peer-reviewed conference paper. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** systematically evaluates seven tabular-to-image CNN methods against seven conventional/non-CNN classifiers across 14 datasets, including medical and gene-expression tasks, and finds that tabular-to-image approaches are not uniformly superior. This is a particularly important challenge to Dynomap’s broad performance framing.

9. **Lin Y-R, Wu H-M. “Image generator for tabular data based on non-Euclidean metrics for CNN-based classification.” *PLOS ONE* 21, e0340005 (2026). DOI: 10.1371/journal.pone.0340005.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** extends IGTD using correlation, geodesic, Jensen–Shannon, Wasserstein and tropical distances to encode nonlinear feature relationships. Its genomics experiments make it a direct contemporary alternative to Dynomap’s learned spatial organization.

10. **Mamdouh A, El-Melegy M, Ali S, Kikinis R. “Tab2Visual: Deep learning for limited tabular data via visual representations and augmentation.” *Pattern Recognition* 176, 113173 (2026). DOI: 10.1016/j.patcog.2026.113173.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** transforms heterogeneous tabular data into visual representations and combines them with image augmentation and transfer learning, specifically targeting small datasets common in healthcare. It provides a very recent comparison point for Dynomap’s claims regarding data efficiency and CNN-based tabular representation.

069816
## Editorial Integrity Alert — Handling Editor Only

A 2025 *Circulation* conference abstract reports a highly overlapping UK Biobank analysis using >8,000 Google Satellite/Street View features, cross-validated sparse PLS scores, MACE outcomes, and mediation through BMI, SBP, LDL-C and diabetes. Several reported mediated proportions closely parallel the present manuscript. The same research programme has also published satellite-imagery/MACE analyses in *JACC* and Street View/MACE analyses in the *European Journal of Preventive Cardiology*. Because the submitted authors are blinded, authorship and cohort overlap cannot be established here. The editor should request a transparent statement distinguishing the present work from these publications and confirming whether participant-level overlap exists.

## 1. Overall Assessment

The manuscript develops a composite VISION environmental score from 8,192 ResNet-50-derived Google Satellite and Street View features, reduced by sparse partial least squares to seven satellite and four Street View components. It evaluates MACE associations in UK Biobank (n=255,844), All of Us (n=40,192), and University Hospitals (n=98,475). A 1-SD higher score is associated with MACE in UKB (HR 1.082) and both US cohorts (approximately HR 1.13), while mediation analysis attributes 91.3% of the effect to pathways outside BMI, SBP, LDL-C, and diabetes.

External replication is strong, but exposure chronology and outcome-supervised score derivation weaken the central causal interpretation.

## 2. Strengths

The three-cohort design provides meaningful geographic and health-system replication. The multimodal framework combines satellite and Street View imagery, and Cox models adjust for demographic, clinical, socioeconomic, air-pollution, traffic, and natural-environment covariates.

Sequential mediation, Martingale-residual testing, partial Cox-Snell R² ranking, and attributable-event calculations provide a broader mechanistic assessment than simple association testing.

## 3. Weaknesses

Temporal alignment is the principal concern. UKB recruitment occurred in 2006-2010, whereas satellite imagery was captured in 2022-2024 and Street View imagery spans 2010-2024. Environmental measurements can therefore post-date mediators and MACE events, invalidating strong causal-mediation interpretation.

VISION is outcome-supervised. Sparse PLS uses follow-up time and event status for feature reduction, after which the same UKB cohort supports incremental-risk, residual, attributable-event, and mediation analyses. Component-selection cross-validation does not replace fully nested cross-fitting.

The manuscript also lacks discrimination, calibration, reclassification, decision-curve evaluation, and detailed subgroup performance against contemporary cardiovascular risk models.

## 4. Editorial Decision

Reject. External replication is substantial, but the claim that imagery-derived environmental risk operates predominantly independently of conventional cardiometabolic pathways is not supportable under the current chronology and derivation strategy. A reframed associative study using pre-outcome imagery and nested derivation could be considered for *npj Digital Medicine* or *Communications Medicine*.

## 5. Suggested Reviewer Expertise

Review should combine expertise in geospatial computer vision and remote-sensing exposure modelling; outcome-supervised survival machine learning and nested validation; causal mediation for time-to-event outcomes; spatial/environmental epidemiology with residential exposure assessment; and preventive cardiology with clinical cardiovascular risk prediction.

## 6. State-of-the-Art Literature Review — Past 3 Years

The field has moved rapidly beyond ecological proof-of-concept work. Chen et al. linked satellite-derived deep features to cardiometabolic prevalence in *JAMA Cardiology* in 2024 and subsequently demonstrated satellite-derived MACE associations in 64,230 individuals in *JACC*. Street View features have since been associated with MACE in 49,887 Northeast Ohio participants, while a 2025 national Veterans study evaluated interpretable Street View features in 770,990 patients with ASCVD. Recent prospective work in the Nurses' Health Study has further linked deep-learning-derived street-level greenspace to incident CVD in 88,788 women.

The present manuscript advances this literature through joint satellite/Street View representation, three-cohort validation, and formal decomposition of residual risk. Its novelty is therefore meaningful but narrower than implied. The unresolved advance would be a temporally valid, independently derived environmental risk model demonstrating calibrated improvement over accepted cardiovascular prediction tools, rather than stronger association alone.

## 7. Suggested Reviewer Names

For GeoAI and environmental exposure modelling, suitable candidates include Hari Iyer, Peter James, Esra Suel, and Marcia Pescador Jimenez, whose recent work spans GeoAI epidemiology and deep-learning-derived street-level environmental exposures. For causal mediation and statistical inference, Linda Valeri, Shu Jiang, Judith Abécassis, and Houssam Zenati have directly relevant methodological expertise. For cardiovascular risk prediction, Sadiya Khan and Kunihiro Matsushita are particularly relevant through development of the AHA PREVENT equations. All suggested reviewers require standard conflict-of-interest screening because the manuscript author list is blinded.

## Further Literature — 10 Closely Related Papers From the Past 3 Years

Cited status below was checked against the manuscript reference list on pages 22–23. Because the submission is blinded, author independence cannot be established definitively until unblinding.

1. **Chen Z, et al. “AI-Facilitated Assessment of Built Environment Using Neighborhood Satellite Imagery and Cardiovascular Risk.” *Journal of the American College of Cardiology*. 2024;84:1733–1744. DOI: 10.1016/j.jacc.2024.08.053.** Peer-reviewed. **Not cited in the manuscript.** This is arguably the closest prior study: pretrained deep features from Google Satellite Imagery were linked to MACE in 64,230 individuals using Cox models and a composite environmental risk score. Potential submitting-group overlap should be checked after unblinding.

2. **Moorthy S, et al. “The built environment and adverse cardiovascular events in US veterans with cardiovascular disease.” *Science of the Total Environment*. 2025;980:179596. DOI: 10.1016/j.scitotenv.2025.179596.** Peer-reviewed. **Not cited.** It links 164 million Google Street View images to MACE in 770,990 US Veterans with ASCVD using competing-risk models. This provides substantially larger-scale external evidence for image-derived built-environment cardiovascular associations. Potential author-group overlap requires checking.

3. **Chen Z, et al. “Artificial intelligence–based assessment of built environment from Google Street View and coronary artery disease prevalence.” *European Heart Journal*. 2024;45:1540–1549. DOI: 10.1093/eurheartj/ehae158.** Peer-reviewed. **Not cited.** Deep learning applied to approximately 0.53 million Street View images explained substantial census-tract variation in CHD prevalence across seven US cities. It is direct methodological prior art for the GSV component of VISION.

4. **Chen Z, et al. “Deep learning analysis of Google Street View to assess residential built environment and cardiovascular risk in a Midwestern US retrospective cohort.” *European Journal of Preventive Cardiology*. Published online 2025. DOI: 10.1093/eurjpc/zwaf038.** Peer-reviewed. **Cited.** In 49,887 individuals, deep-learning-derived tree-sky and pavement indices were independently associated with MACE. It directly overlaps the manuscript's residential Street View exposure and time-to-event framework.

5. **Chen Z, et al. “Deep Learning–Based Assessment of Built Environment From Satellite Images and Cardiometabolic Disease Prevalence.” *JAMA Cardiology*. 2024. DOI: 10.1001/jamacardio.2024.0749.** Peer-reviewed. **Cited.** CNN-derived satellite features across seven US cities were associated with CHD, stroke, and CKD prevalence beyond demographic and social-determinant variables. It establishes the satellite-imagery component of this research programme.

6. **Chen Z, et al. “AI-Enhanced Analysis of Built Environment Imagery and Neighborhood Obesity in US Cities.” *JAMA Network Open*. 2025;8:e2534612. DOI: 10.1001/jamanetworkopen.2025.34612.** Peer-reviewed. **Cited.** More than 94,000 satellite and 670,000 Street View images were jointly modelled across 94 US cities. Its multimodal GSI+GSV architecture is particularly relevant to the manuscript's claim that combining the two perspectives captures environmental information beyond conventional measures.

7. **Yi L, et al. “Assessing greenspace and cardiovascular health through deep-learning analysis of street-view imagery in a cohort of US children.” *Environmental Research*. 2025;265:120459. DOI: 10.1016/j.envres.2024.120459.** Peer-reviewed. **Cited.** Deep-learning segmentation of Street View imagery was linked longitudinally to Life's Essential 8 cardiovascular-health measures. The largely null longitudinal findings are important because they temper strong assumptions that visually derived environmental exposures necessarily translate into prospective cardiovascular effects.

8. **James P, et al. “Assessing greenspace and cardiovascular disease risk through deep learning analysis of street-view imagery in the US-based nationwide Nurses’ Health Study.” *Environmental Epidemiology*. 2026;10:e442. DOI: 10.1097/EE9.0000000000000442.** Peer-reviewed. **Not cited.** The study links deep-learning measurements from 350 million Street View images to incident CVD in 88,788 women with residential histories. Its temporally resolved exposure design is directly relevant to the chronology problem in the present manuscript.

9. **Nguyen QC, et al. “Neighborhood built environment, obesity, and diabetes: A Utah siblings study.” *SSM – Population Health*. 2024;26:101670. DOI: 10.1016/j.ssmph.2024.101670.** Peer-reviewed. **Not cited.** CNNs characterized greenness, crosswalks, sidewalks, and building types from 1.4 million Google Street View images linked to 1.9 million adults. It provides strong individual-level evidence for imagery-derived environmental associations with cardiometabolic mediators central to the manuscript's causal model.

10. **Tong J, et al. “Deep-learning analysis of greenspace and metabolic syndrome: A street-view and remote-sensing approach.” *Environmental Research*. 2025;274:121349. DOI: 10.1016/j.envres.2025.121349.** Peer-reviewed. **Not cited.** This study jointly evaluates CNN-derived street-level Green Visibility Index and satellite-derived NDVI in the Wuhan Chronic Disease Cohort and uses counterfactual analyses to estimate potentially avoidable metabolic-syndrome burden. It is closely relevant to the manuscript's multimodal environmental exposure and attributable-disease claims.

The most consequential omissions for novelty assessment are the 2024 *JACC* satellite-imagery MACE study and the 2025 national Veterans MACE study. Both directly test whether AI-derived neighborhood imagery contributes cardiovascular-event information beyond conventional covariates, substantially narrowing the novelty attributable to the VISION–MACE association itself.

069529
### 1. Overall Assessment

The manuscript introduces DiffeoAfford, which retrospectively propagates instrument–tissue interaction targets through deformable laparoscopic video, and AffordView, a SegFormer-B3 model that predicts these tissue-affordance hotspots for anticipatory auto-framing. Evaluation spans Cholec80, AutoLaparo, a prospective 26-case eye-tracking cohort, a 28-surgeon preference survey, and 24 intraoperative paired sessions. The central claim is that action-grounded targets anticipate surgeon intent better than reactive instrument tracking and can reduce cognitive workload. This is a distinctive contribution, but the small clinical evaluation and the gap between digital cropping and physical camera actuation are the principal limitations.

### 2. Strengths

DiffeoAfford combines SAM2 segmentation, point tracking, global transformation, and local diffeomorphic deformation to generate dense affordance labels without per-frame expert annotation. On 141 Cholec80 images, median localization error was 32.38 pixels, outperforming similarity-RANSAC and homography-RANSAC.

Validation is unusually multi-level. On AutoLaparo, predicted hotspots showed 95.16% directional consistency with subsequent camera motion. In the LCET cohort, predictions aligned more closely with surgeon gaze than camera-assistant gaze or image center. The paired intraoperative study further showed concordant reductions in SURG-TLX, EEG theta/alpha ratio, pupillary activity, and verbal camera instructions.

### 3. Weaknesses

The efficacy study includes only 12 matched pairs across five surgeons, with novice camera assistants and alternating rather than randomized condition order. This leaves learning, sequence, and operator effects incompletely controlled. Generalizability is also limited to single-center elective cholecystectomy.

AffordView digitally crops and magnifies an already acquired image. It does not test autonomous camera movement, robotic kinematics, remote-center-of-motion constraints, or safety when relevant anatomy lies outside the original field.

### 4. Editorial Decision

**Send for Review.** The action-grounded supervision strategy, cross-dataset evaluation, prospective gaze validation, and multimodal workload assessment justify external review. Reviewers should scrutinize clinical-study robustness, independence from instrument-motion priors, and whether claims should be restricted to digital auto-framing rather than autonomous camera control.

### 5. Suggested Reviewer Expertise

Relevant expertise includes deformable surgical-video correspondence and segmentation; surgical workflow anticipation and intent modeling; gaze-aware laparoscopic camera control and visual servoing; EEG, pupillometry, eye tracking, and SURG-TLX human-factors methodology; and clinical laparoscopic cholecystectomy and operating-room ergonomics.

### 6. State-of-the-Art Literature Review (Past 3 Years)

Recent work has shifted from reactive tool-centering toward intent-aware assistance. SAVAnet by Gao et al. modeled action-driven visual attention for autonomous endoscope control; GazeScope by Zhang et al. fused gaze, instrument position, and eye–hand consistency for FoV adjustment; Shi et al. developed compliant deep-learning-based autonomous laparoscope manipulation; Li et al. combined gaze weighting with a 6-DOF endoscopic robot; and Wagner et al. demonstrated real-time anticipation of instrument requirements from laparoscopic video.

The manuscript advances this landscape mainly through its supervision strategy: tissue-level affordances are mined retrospectively from action trajectories and then predicted without continuous gaze input. Its prospective gaze and workload validation is stronger than most controller-centric studies, although physical camera actuation and broader procedural validation remain absent.

### 7. Suggested Reviewer Names

Mengtang Li, Sun Yat-sen University, is appropriate for gaze-assisted robotic FoV control; Lars Wagner, Technical University of Munich, for anticipatory surgical AI and surgical robotics; Nathan Lau, Virginia Tech, for eye tracking, cognitive workload, and human–automation interaction; and Jinze Shi, Zhejiang University, for autonomous laparoscope manipulation. Their public affiliations show no apparent institutional overlap with the submitting Wuhan-based group, subject to routine conflict-of-interest checks.

### Further Literature — 10 Closely Related Papers from the Past 3 Years

The following papers were selected for methodological overlap with action-grounded affordance prediction, surgeon-intent modeling, gaze-aware field-of-view control, laparoscopic camera automation, soft-tissue correspondence, or prospective surgical anticipation. “Cited” status refers to the submitted manuscript’s reference list.

1. **Huber, M., Ourselin, S., Bergeles, C. & Vercauteren, T. “Deep Homography Prediction for Endoscopic Camera Motion Imitation Learning.” MICCAI 2023, pp. 217–226. DOI: 10.1007/978-3-031-43996-4_21.** Peer-reviewed conference paper; **cited in the manuscript as Ref. 37**; independent author group. This is one of the closest methodological comparators because it learns future laparoscopic camera motion directly from retrospective videos using homography-based imitation learning and evaluates on Cholec80, HeiChole and AutoLaparo. It therefore provides an important alternative to the manuscript’s affordance-mediated prediction strategy.

2. **Gao, H., Fan, W., Qiu, L., et al. “SAVAnet: Surgical Action-Driven Visual Attention Network for Autonomous Endoscope Control.” IEEE Transactions on Automation Science and Engineering 20(4), 2655–2667 (2023). DOI: 10.1109/TASE.2022.3203631.** Peer-reviewed journal article; **not cited in the manuscript**; independent author group. SAVAnet explicitly connects surgical-action recognition to predicted visual-attention targets and autonomous endoscope control. Its conceptual overlap with action-grounded surgeon-attention prediction makes its omission notable.

3. **Sivananthan, A., Rubio-Solis, A., Darzi, A., Mylonas, G. & Patel, N. “Eye-controlled endoscopy—a benchtop trial of a novel robotic steering platform—iGAZE2.” Journal of Robotic Surgery 18, 266 (2024). DOI: 10.1007/s11701-024-02022-5.** Peer-reviewed journal article; **not cited**; independent Imperial College group. Twelve participants completed simulated endoscopic tasks faster and with substantially lower NASA-TLX workload using gaze control. This is directly relevant to AffordView’s argument that improved visual-control interfaces can reduce cognitive demand.

4. **Gong, S., Long, Y., Chen, K., et al. “Self-Supervised Cyclic Diffeomorphic Mapping for Soft Tissue Deformation Recovery in Robotic Surgery Scenes.” IEEE Transactions on Medical Imaging 43(12), 4356–4367 (2024). DOI: 10.1109/TMI.2024.3439701.** Peer-reviewed journal article; **cited as Ref. 52**; independent author group. This work combines semantics, temporal motion information and diffeomorphic regularization for dense surgical soft-tissue correspondence. It is particularly relevant to the deformation-propagation component of DiffeoAfford and represents an important technical baseline for tissue-level label transport.

5. **Zhang, J., Wang, B., Pan, Z. & Li, M. “GazeScope: A Framework of Gaze Attention-Based Automatic Field-of-View Adjustment for Laparoscopic Robots.” IEEE Robotics and Automation Letters 10(7), 6560–6567 (2025). DOI: 10.1109/LRA.2025.3570158.** Peer-reviewed journal article; **cited as Ref. 60**. It shares a Sun Yat-sen University affiliation with one submitting author, although no author-name overlap is evident. GazeScope integrates surgeon gaze, instrument positions and eye–hand consistency, reducing unnecessary FoV adjustments by at least 66%. It is a direct comparator for the manuscript’s claim that predicted affordances can replace continuous gaze input.

6. **Gao, Y., Li, Z., Zhao, J., Li, J. & Li, J. “A human–AI collaborative framework for surgical field-of-view adjustment: design and experimental validation.” Journal of Robotic Surgery 19, 259 (2025). DOI: 10.1007/s11701-025-02421-2.** Peer-reviewed validation study; **cited as Ref. 20**; independent Tianjin University/Tsinghua group. HIC-FoV uses concise surgeon commands plus scene understanding to produce intent-aligned camera adjustment and reports reduced NASA-TLX physical demand in simulated cholecystectomy. It directly frames the competing design choice between explicit human input and implicit intention prediction.

7. **Shi, J., Zhou, C., Wang, L., et al. “Hands-Free Camera Assistant: Autonomous Laparoscope Manipulation in Robot-Assisted Surgery.” International Journal of Medical Robotics and Computer Assisted Surgery 21(4), e70103 (2025). DOI: 10.1002/rcs.70103.** Peer-reviewed journal article; **not cited**; independent Zhejiang University group. The study combines deep learning, robot kinematics and compliant control for autonomous laparoscope manipulation. Unlike AffordView, it closes the perception-to-actuation loop, making it particularly relevant when judging whether the manuscript’s “auto-framing” claims should extend to robotic camera autonomy.

8. **Li, M., Zhao, S., Wang, S. & Liu, F. “Enhanced flexibility and dexterity in robotic endoscopy via a 6-DOF parallel mechanism and eye-gaze-assisted field-of-view control.” Robotics and Autonomous Systems 198, 105322 (2026). DOI: 10.1016/j.robot.2025.105322.** Peer-reviewed journal article; **not cited**. The authors are based at Sun Yat-sen University, creating institutional overlap with one submitting affiliation, although no author-name overlap was identified. The system dynamically weights multiple tools using gaze-derived surgeon intent and achieves automated FoV regulation with a physical 6-DOF endoscopic robot. This is a strong recent comparator to AffordView’s predicted-intent approach.

9. **Wang, B., Zhang, J., Pan, Z., Zhao, S., Li, M. & Liu, H. “Automatic field-of-view adjustment for multi-surgical tools of a novel continuum laparoscopic robot.” Measurement 257, 118544 (2026). DOI: 10.1016/j.measurement.2025.118544.** Peer-reviewed journal article; **not cited**. The Sun Yat-sen University affiliation again creates institutional overlap with one submitting affiliation. The study integrates a 6-DOF RCM-free continuum laparoscope with multi-tool visual-servo FoV adjustment and reports stable tracking error below 20 pixels. It highlights the hardware and motion-control validation absent from the present manuscript.

10. **Wagner, L., Jourdan, S., Mayer, L., et al. “Robotic scrub nurse to anticipate surgical instruments based on real-time laparoscopic video analysis.” Communications Medicine 4, 156 (2024). DOI: 10.1038/s43856-024-00581-0.** Peer-reviewed journal article; **not cited**; independent Technical University of Munich group. Using 62 laparoscopic cholecystectomies, the system anticipates 71.54% of required instruments through single-frame, temporal multi-frame and informed models. Although the downstream task differs, it is highly relevant to the manuscript’s broader claim that implicit surgical intent can be inferred prospectively from laparoscopic video and used to reduce verbal coordination.

069327
### 1. Overall Assessment

BridgeECG proposes a self-supervised ViT-Base framework transferring 12-lead ECG knowledge into single-lead representations through explicit 12-lead modelling (E12M), teacher-guided feature distillation (TeFD), and adaptive feature aggregation (AFA). It is pretrained on more than 1.3 million ECGs from eight public repositories and evaluated on PTB-XL, CPSC2018, PhysioNet2017, and a 1,473-record hospital cohort.

The work targets the clinically important information gap between wearable single-lead and standard 12-lead ECG. The principal concerns are whether simulated single-lead inputs adequately represent wearable acquisition and whether novelty is sufficiently distinguished from recent reduced-lead reconstruction and multi-to-single-lead transfer methods.

### 2. Strengths

The framework is coherent: E12M uses masked 12-lead reconstruction to encode cross-lead morphology, TeFD distils diagnostic semantics from a frozen 12-lead teacher, and AFA preserves transferred priors during downstream adaptation. Across eight tasks, BridgeECG reports the best mean rank of 1.25 and closes 14.1–66.4% of the supervised single-lead-to-12-lead performance gap.

Evaluation includes multiple public datasets, limited-label experiments, lead/configuration robustness, 1,000 paired bootstrap resamples with Holm-Bonferroni correction, an independent hospital cohort, and blinded cardiologist assessment.

### 3. Weaknesses

Wearable relevance remains indirect because Lead-I/II inputs are extracted from conventional clinical ECGs. Motion artefact, device filtering, electrode placement, ambulatory conditions, and wearable-domain shift are therefore untested. The physician study is spectrum-enriched, so its accuracy does not estimate real screening performance; calibration, PPV, decision-curve analysis, and workload effects are absent.

No substantive subgroup analysis is reported across age, sex, ethnicity, or socioeconomic context. Recent direct competitors in single-lead reconstruction and teacher-student transfer also reduce the apparent conceptual novelty unless stronger head-to-head comparisons establish a clear advantage.

### 4. Editorial Decision

**Send for Review.** The scale, multi-level transfer design, cross-dataset evaluation, and independent clinical cohort justify external assessment. Reviewers should focus on wearable-domain validity, direct baselines, leakage control, calibration, subgroup robustness, and whether BridgeECG meaningfully outperforms reconstruction-based alternatives.

### 5. Suggested Reviewer Expertise

Relevant expertise includes self-supervised ECG representation learning and foundation models; masked autoencoding, cross-lead learning and knowledge distillation for physiological signals; reduced-lead-to-12-lead ECG reconstruction; statistical validation and calibration of clinical AI; and clinical electrophysiology with wearable or ambulatory ECG screening.

### 6. State-of-the-Art Literature Review (Past 3 Years)

Recent work has progressed rapidly toward both ECG foundation models and clinically evaluated reduced-lead reconstruction. Mason et al. reconstructed 12-lead ECG from three leads using more than 600,000 ECGs and performed cardiologist assessment in *npj Digital Medicine* (2024). Chen et al. introduced MCMA and ECGGenEval for arbitrary single-lead reconstruction in *npj Cardiovascular Health* (2024), while Presacan et al. evaluated single- and dual-lead reconstruction in *Communications Medicine* (2025).

Foundation-model development has simultaneously accelerated. ECG-FM used 1.5 million ECGs with hybrid masked-reconstruction and contrastive self-supervision, while ECGFounder scaled to more than 10.7 million ECGs and explicitly evaluated reduced-lead applications. BridgeECG is differentiated by transferring multi-lead priors into a deployable single-lead representation rather than requiring reconstructed waveforms at inference. However, the reconstruction literature constitutes direct competing prior art and warrants stronger head-to-head engagement.

### 7. Suggested Reviewer Names

Federico Mason is directly relevant through the 2024 *npj Digital Medicine* reduced-lead reconstruction study. Kaden McKeen provides expertise in open ECG foundation models through ECG-FM. Oriana Presacan has directly evaluated the feasibility of limited-lead 12-lead reconstruction. Jørgen K. Kanters provides complementary clinical ECG interpretation and reduced-lead validation expertise. These candidates are distinct from the submitting author group in the materials reviewed.

### 8. Further Literature — 10 Closely Related Papers from the Past 3 Years

1. **Qin, Y. et al. “MVKT-ECG: Efficient single-lead ECG classification for multi-label arrhythmia by multi-view knowledge transferring.” *Computers in Biology and Medicine* 168, 107503 (2023).** DOI: 10.1016/j.compbiomed.2023.107503. Peer-reviewed journal article. This is one of the closest methodological precedents because a multi-lead teacher transfers information to a single-lead student using Contrastive Lead-information Transferring and multi-label knowledge distillation. **Cited by manuscript:** Yes, Ref. 48. **Independence:** no apparent author overlap with the submitting author list.

2. **Mason, F. et al. “AI-enhanced reconstruction of the 12-lead electrocardiogram via 3-leads with accurate clinical assessment.” *npj Digital Medicine* 7, 201 (2024).** DOI: 10.1038/s41746-024-01193-7. Peer-reviewed journal article. The model was trained on more than 600,000 ECGs and reconstructed 12-lead ECGs from leads I, II and V3, including cardiologist evaluation for STEMI. It directly tests an alternative route to recovering multilead diagnostic information from reduced-lead acquisition. **Cited by manuscript:** Yes, Ref. 8. **Independence:** no apparent author overlap.

3. **Chen, J., Wu, W., Liu, T. et al. “Multi-channel masked autoencoder and comprehensive evaluations for reconstructing 12-lead ECG from arbitrary single-lead ECG.” *npj Cardiovascular Health* 1, 34 (2024).** DOI: 10.1038/s44325-024-00036-4. Peer-reviewed journal article. MCMA explicitly learns cross-lead information through masked reconstruction and introduces ECGGenEval for signal-, feature-, and diagnostic-level assessment. This is arguably the most important direct reconstruction comparator for BridgeECG. **Cited by manuscript:** No apparent citation in the reference list. **Independence:** no author-name overlap; institutional/collaboration conflicts should be checked separately.

4. **Presacan, O. et al. “Evaluating the feasibility of 12-lead electrocardiogram reconstruction from limited leads using deep learning.” *Communications Medicine* 5, 139 (2025).** DOI: 10.1038/s43856-025-00814-w. Peer-reviewed journal article. Using PTB-XL, the study shows that single- or dual-lead reconstruction can regress toward population-average morphology despite visually plausible outputs. This provides an important counterpoint to claims that missing multilead information can simply be regenerated from limited leads. **Cited by manuscript:** Yes, Ref. 14. **Independence:** no apparent author overlap.

5. **Srivastava, A., Sheet, D. & Patra, A. “L2G-ECG: Learning to Generate Missing Leads in ECG Signals using Adversarial Autoencoder.” *IEEE Journal of Biomedical and Health Informatics* (2025).** DOI: 10.1109/JBHI.2025.3587428. Peer-reviewed journal article. L2G-ECG addresses missing-lead generation through an adversarial autoencoder and therefore provides another direct generative alternative to BridgeECG's representation-transfer strategy. **Cited by manuscript:** Yes, Ref. 13. **Independence:** no apparent author overlap.

6. **Safdar, M.F., Nowak, R.M., Pałka, P. & Al Faresi, A. “An integrated algorithm for single lead electrocardiogram signal analysis using deep learning with 12-lead data.” *Scientific Reports* 15, 34955 (2025).** DOI: 10.1038/s41598-025-18910-1. Peer-reviewed journal article. This study trains on isolated leads from conventional 12-lead datasets and develops a translational architecture for subsequent single-lead classification across PTB-XL, CPSC2018 and PhysioNet2017—the same general deployment problem and several of the same benchmarks as BridgeECG. **Cited by manuscript:** No apparent citation. **Independence:** no apparent author overlap.

7. **Liu, W., Pan, S., Chang, S., Huang, Q. & Jiang, N. “Self-supervised learning for Electrocardiogram classification using Lead Correlation and Decorrelation.” *Applied Soft Computing* 172, 112871 (2025).** DOI: 10.1016/j.asoc.2025.112871. Peer-reviewed journal article. LCD explicitly exploits intra- and inter-lead correlations during self-supervised pretraining and produces an encoder usable for individual ECG leads. It is particularly relevant to BridgeECG's claim that multi-lead structural priors can improve single-lead representations. **Cited by manuscript:** Yes, Ref. 19. **Independence:** no apparent author overlap.

8. **McKeen, K. et al. “ECG-FM: an open electrocardiogram foundation model.” *JAMIA Open* 8, ooaf122 (2025).** DOI: 10.1093/jamiaopen/ooaf122. Peer-reviewed journal article. ECG-FM uses approximately 1.5 million 12-lead ECGs with masked reconstruction plus contrastive learning and evaluates label efficiency, cross-dataset transfer, ECG interpretation and reduced LVEF prediction. It is a major benchmark for the broader claim of transferable ECG representations. **Cited by manuscript:** Yes, Ref. 18, but as the earlier arXiv version rather than the final journal publication. **Independence:** no apparent author overlap.

9. **Li, J. et al. “An Electrocardiogram Foundation Model Built on over 10 Million Recordings.” *NEJM AI* 2 (2025).** DOI: 10.1056/aioa2401033. Peer-reviewed journal article. ECGFounder was built from 10,771,552 ECGs from 1,818,247 individuals and explicitly addresses the performance gap between multilead and single-lead ECG analysis. It sets a substantially larger-scale reference point for claims about general-purpose ECG transfer. **Cited by manuscript:** Yes, Ref. 26. **Independence:** no apparent author-name overlap; institutional and collaboration relationships should be checked because several authors are based at Peking University.

10. **Gu, X. et al. “Cardiac health assessment across scenarios and devices using a multimodal foundation model pretrained on data from 1.7 million individuals.” *Nature Machine Intelligence* 8, 220–233 (2026).** DOI: 10.1038/s42256-026-01180-5. Peer-reviewed journal article. The Cardiac Sensing Foundation Model uses generative masked pretraining across heterogeneous cardiac signals and maintains performance across 12-lead and single-lead ECG configurations. It is particularly relevant to BridgeECG's generalization and device-transfer claims. **Cited by manuscript:** Yes, Ref. 46. **Independence:** no apparent author overlap.

The most consequential literature gap is **Chen et al. 2024 (MCMA/ECGGenEval)**, because it directly addresses arbitrary single-lead-to-12-lead information recovery with masked modelling yet does not appear in the manuscript's reference list. **Safdar et al. 2025** is also uncited and overlaps closely with the use of 12-lead datasets to improve single-lead diagnostic models. These two studies should be considered in the novelty assessment and, ideally, in additional head-to-head experiments.

069291
### 1. Overall Assessment

The manuscript, “Choosing How Medical AI Reasons: Inference Protocols as a Decision Layer in Medical AI,” argues that medical AI should be evaluated as model–protocol pairs rather than models alone. It formalizes inference protocols spanning direct answering, chain reasoning, retrieval, verification, committees, aggregation and clinician gating, with workload-conditioned selection according to clinical loss, latency, cost and human burden.

The framing is coherent, but the work remains conceptual. The main concerns are absence of empirical validation and limited novelty relative to adaptive reasoning and multi-agent medical AI systems.

### 2. Strengths

The formulation \(a=(M,\pi)\) captures an important limitation of model-centric benchmarking. The same model can have materially different risk profiles under direct prompting, retrieval, self-consistency, committee reasoning or clinician verification. The manuscript also appropriately distinguishes sequential depth reasoning from committee-style breadth reasoning and emphasizes correlated harmful errors.

### 3. Weaknesses

The central limitation is the absence of experimental validation. No clinical cohort, benchmark or simulated workflow demonstrates that the proposed criterion selects safer or more efficient protocols. Figure 2 therefore provides workload–strategy recommendations without quantitative validation.

The framework is also operationally underdefined. Clinical-loss functions and weights for latency, cost, clinician burden and aggregation are not estimated or subjected to sensitivity analysis. Rankings under \(R(w,a)\) could therefore depend strongly on arbitrary parameter choices.

Novelty is constrained by Med-PaLM 2, MedAgents and MDAgents, which already alter retrieval, ensemble reasoning or collaboration structures according to task requirements. More recent work further evaluates adaptive collaboration and test-time reasoning in medical LLMs.

### 4. Editorial Decision

**Reject.** The model–protocol perspective is conceptually useful but does not meet the Nature Communications threshold without empirical evidence that workload-conditioned protocol selection improves clinically meaningful safety, accuracy or efficiency over fixed and existing adaptive strategies. A substantially expanded validation study may be more appropriate for *npj Digital Medicine* or *Communications Medicine*.

### 5. Suggested Reviewer Expertise

Appropriate expertise would include adaptive inference and test-time reasoning for large language models; multi-agent and ensemble architectures for clinical AI; uncertainty, calibration and correlated-error analysis in AI systems; clinical workflow evaluation and human–AI teaming; and medical AI safety, deployment and regulatory evaluation.

### 6. State-of-the-Art Literature Review (Past 3 Years)

The relevant literature has moved beyond simply demonstrating that prompting matters. Med-PaLM 2 combined domain adaptation with ensemble refinement and chain of retrieval, reaching 86.5% on MedQA and introducing clinician-centered evaluation of factuality and harm. ([doi.org](https://doi.org/10.1038/s41591-024-03423-7?utm_source=chatgpt.com)) MDAgents subsequently made collaboration structure adaptive to task complexity and achieved the strongest result on seven of ten evaluated benchmarks. ([proceedings.neurips.cc](https://proceedings.neurips.cc/paper_files/paper/2024/hash/90d1fc07f46e31387978b88e7e057a31-Abstract-Conference.html?utm_source=chatgpt.com)) Ensemble reasoning has separately been evaluated against zero-shot CoT with self-consistency on USMLE questions, demonstrating task- and model-dependent gains. ([academic.oup.com](https://academic.oup.com/jamia/article/31/9/1964/7705627?utm_source=chatgpt.com))

The field is now also testing these protocol choices in more clinically structured environments. Chen et al. showed that a multi-agent conversational framework improved diagnosis on 302 rare-disease cases relative to GPT-3.5, GPT-4, CoT, Self-Refine and Self-Consistency. ([nature.com](https://www.nature.com/articles/s41746-025-01550-0?utm_source=chatgpt.com)) Agent evaluation has expanded toward realistic clinical workflows through AI-SCE concepts and MedAgentBench, which contains 300 physician-authored tasks across ten categories in a FHIR-compatible EHR environment. ([nature.com](https://www.nature.com/articles/s41746-024-01083-y?utm_source=chatgpt.com)) Against this literature, the manuscript's main contribution is a unifying risk-based vocabulary. It does not yet establish that its formal selection principle outperforms existing adaptive protocol-selection approaches.

### 7. Suggested Reviewer Names

For adaptive inference and test-time reasoning, suitable reviewers include Yubin Kim, Chanwoo Park, Alex J. Goodell and Simon N. Chu. For multi-agent clinical AI, suitable reviewers include Hae Won Park, Xuhai Xu, Xi Chen and Qicheng Lao. For uncertainty, error dependence and AI safety, suitable reviewers include Roxana Daneshjou, Ziad Obermeyer, Marzyeh Ghassemi and Jonathan H. Chen. For clinical workflow and agent evaluation, suitable reviewers include Yixing Jiang, Kameron C. Black, Dara Rouholiman and Hyeonhoon Lee. Reviewer independence and recent co-authorship conflicts should be checked before invitation.

### 8. Further Literature — 10 Closely Related Papers from the Past 3 Years

**1. Singhal, K. et al. “Toward expert-level medical question answering with large language models.” *Nature Medicine* 31, 943–950 (2025). DOI: 10.1038/s41591-024-03423-7.** Peer-reviewed journal article. Cited by the manuscript: **Yes**. Author independence: **Yes; no evident overlap with the submitting group**. This is a direct comparator because Med-PaLM 2 combines chain-of-thought, self-consistency, ensemble refinement and chain of retrieval, demonstrating that inference-time protocol choice materially changes medical QA performance and safety.

**2. Kim, Y. et al. “MDAgents: An Adaptive Collaboration of LLMs for Medical Decision-Making.” *Advances in Neural Information Processing Systems 37* (NeurIPS 2024). DOI: 10.52202/079017-2522.** Peer-reviewed conference paper; oral presentation at NeurIPS 2024. Cited by the manuscript: **Yes**. Author independence: **Yes; no evident author overlap**. MDAgents directly challenges the manuscript’s novelty because it operationalizes task-conditioned selection between solo and multi-agent collaboration and evaluates accuracy–efficiency trade-offs across ten medical benchmarks.

**3. Tang, X. et al. “MedAgents: Large Language Models as Collaborators for Zero-shot Medical Reasoning.” *Findings of ACL 2024*, 599–621. DOI: 10.18653/v1/2024.findings-acl.33.** Peer-reviewed conference paper. Cited by the manuscript: **Yes**. Author independence: **Yes; no evident overlap**. The framework uses multi-disciplinary role assignment, iterative discussion and consensus formation, directly overlapping with the manuscript’s committee and aggregation protocols.

**4. Chen, X. et al. “Enhancing diagnostic capability with multi-agents conversational large language models.” *npj Digital Medicine* 8, 159 (2025). DOI: 10.1038/s41746-025-01550-0.** Peer-reviewed journal article. Cited by the manuscript: **No apparent citation in the submitted reference list**. Author independence: **Yes; no evident overlap**. The MAC framework evaluates four doctor agents plus a supervisor on 302 rare-disease cases and compares against CoT, Self-Refine and Self-Consistency, making it highly relevant to claims about committee protocols and dissent handling.

**5. Shi, W. et al. “MedAdapter: Efficient Test-Time Adaptation of Large Language Models Towards Medical Reasoning.” *EMNLP 2024*, 22294–22314. DOI: 10.18653/v1/2024.emnlp-main.1244.** Peer-reviewed conference paper. Cited by the manuscript: **No apparent citation**. Author independence: **Yes**. MedAdapter ranks multiple candidate LLM solutions at test time using a lightweight adapter and reports gains across four biomedical tasks and eight datasets. It is directly relevant to protocol-level selection, verification and inference-time adaptation.

**6. Savage, T. et al. “Diagnostic reasoning prompts reveal the potential for large language model interpretability in medicine.” *npj Digital Medicine* 7, 20 (2024). DOI: 10.1038/s41746-024-01010-1.** Peer-reviewed journal article. Cited by the manuscript: **No apparent citation**. Author independence: **Yes**. This study compares traditional CoT with differential-diagnosis, analytical, Bayesian and intuitive reasoning prompts using MedQA and NEJM cases, demonstrating that reasoning protocol effects are workload- and model-dependent rather than universally beneficial.

**7. Sivarajkumar, S. et al. “An Empirical Evaluation of Prompting Strategies for Large Language Models in Zero-Shot Clinical Natural Language Processing.” *JMIR Medical Informatics* 12, e55318 (2024). DOI: 10.2196/55318.** Peer-reviewed journal article. Cited by the manuscript: **Yes**. Author independence: **Yes**. The study compares prefix, cloze, anticipatory, heuristic, chain-of-thought, ensemble and few-shot prompting across five clinical NLP tasks and three LLM families, providing direct empirical evidence for workload-conditioned prompt selection.

**8. Lee, H. et al. “Reasoning with large language models for medical question answering.” *Journal of the American Medical Informatics Association* 31, 1964–1975 (2024).** Peer-reviewed journal article. Cited by the manuscript: **No apparent citation**. Author independence: **Yes**. The paper introduces iterative ensemble reasoning and compares it against zero-shot CoT with self-consistency on USMLE Step 1–3 questions using GPT-3.5 Turbo, GPT-4 Turbo and Med42-70B. It directly addresses the relative value of alternative inference protocols.

**9. Jiang, Y. et al. “MedAgentBench: A Virtual EHR Environment to Benchmark Medical LLM Agents.” *NEJM AI* 2(9) (2025). DOI: 10.1056/AIdbp2500144.** Peer-reviewed journal article. Cited by the manuscript: **No apparent citation**. Author independence: **Yes**. MedAgentBench provides 300 physician-authored tasks across ten categories, 100 realistic patient profiles and more than 700,000 EHR elements in a FHIR-compatible environment. It is particularly relevant to the manuscript’s claim that protocol selection should depend on workflow, verification and human-action context rather than benchmark accuracy alone.

**10. Wu, X. et al. “A Knowledge-driven Adaptive Collaboration of LLMs for Enhancing Medical Decision-making.” *Proceedings of EMNLP 2025*, 33495–33512. DOI: 10.18653/v1/2025.emnlp-main.1699.** Peer-reviewed conference paper. Cited by the manuscript: **No apparent citation**. Author independence: **Yes**. KAMAC dynamically recruits additional expert agents as diagnostic knowledge gaps emerge and therefore provides one of the closest recent implementations of workload- and state-conditioned inference-protocol selection. Its existence further weakens a broad novelty claim for the present framework unless the authors clearly distinguish their formal risk criterion from adaptive multi-agent orchestration.

Taken together, these studies show that the closest competing literature already covers fixed versus adaptive prompting, retrieval, self-consistency, ensemble refinement, test-time candidate ranking, multi-agent committee reasoning, dynamic agent recruitment and workflow-level medical agents. The manuscript’s potentially distinctive contribution is therefore not the proposition that inference strategy matters, but the attempt to formalize these alternatives within a common clinical-risk objective. That distinction would need empirical validation to support publication at the current level.

069040
## 1. Overall Assessment

This manuscript presents COMPASS, a clinician-facing multi-agent LLM framework for clinical research protocol development. COMPASS structures question refinement, evidence retrieval, feasibility assessment, causal and statistical design, protocol portfolio generation, simulated review, ethics checks, and final composition. It was evaluated on 24 clinical questions spanning eight organ-system domains, with blinded expert scoring and a small clinician workflow study.

The framework is methodologically more structured than generic text-generation approaches. However, the central benchmark is vulnerable to contamination because the evaluation questions were reconstructed from already published studies, many from prominent journals. This makes it difficult to distinguish genuine methodological reasoning from memorization, retrieval, or reproduction of known study designs. The limited comparator set and very small clinician experiment further weaken the claim of a substantial, generalizable advance.

## 2. Strengths

COMPASS has a clearly decomposed architecture. Dedicated components address PICO/PECO refinement, evidence retrieval, causal-design selection, statistical planning, feasibility, ethics, protocol construction, and simulated review. Figure 6 shows a substantially more explicit workflow than single-prompt LLM generation.

The evaluation covers 24 questions across eight clinical systems. Five domain experts per system performed blinded assessment using the eight-domain CLEAR framework. COMPASS achieved a mean overall expert score of 4.72 ± 0.21 versus 4.26 ± 0.29 for the ablation condition and 2.71 ± 0.29 for the general-LLM baseline.

The authors also include ablation and workflow experiments. COMPASS-assisted protocol development reduced completion time from approximately 110 to 40 minutes while maintaining similar blinded final-protocol quality.

## 3. Weaknesses

The primary weakness is benchmark contamination. Because the source questions derive from published studies, the model may reproduce study designs encountered during pretraining or retrieval. A convincing evaluation would require prospectively formulated, unpublished, or temporally held-out research questions.

The comparator set is too weak. The manuscript does not test competitive agentic systems, retrieval-augmented structured prompting, or other specialist protocol-generation approaches. Therefore, the contribution of multi-agent decomposition cannot be isolated from retrieval, additional inference, or iterative self-review.

The clinician workflow study is underpowered, with only five participants per arm. This supports preliminary usability, not robust real-world validation. Reproducibility is also incomplete because code release is deferred and key implementation details require fuller specification.

## 4. Editorial Decision

**Reject and encourage transfer to Communications Medicine.** The framework is technically interesting, but the benchmark does not convincingly separate methodological reasoning from contamination or retrieval effects, and the comparator and workflow evaluations are insufficient for the claims made at Nature Communications. Stronger temporally or prospectively held-out evaluation and more competitive baselines would be required.

## 5. Suggested Reviewer Expertise

Appropriate expertise would include multi-agent and agentic LLM architectures for biomedical applications; retrieval-augmented generation and evidence-grounded biomedical NLP; evaluation and contamination auditing of clinical foundation models; clinical-trial methodology including causal estimands, statistical analysis plans, feasibility and protocol design; and human-factors evaluation of AI-supported clinical research workflows.

## 6. State-of-the-Art Literature Review (Past 3 Years)

Recent work has moved rapidly from generic medical text generation toward structured clinical-trial workflows. TrialGPT demonstrated an end-to-end LLM framework for trial retrieval, criterion-level eligibility reasoning and ranking, including a human evaluation showing a 42.6% reduction in screening time. ([nature.com](https://www.nature.com/articles/s41467-024-53081-z?utm_source=chatgpt.com)) Zhang, Bornet, Teodoro and colleagues subsequently used LLM-derived representations to analyse eligibility-criteria clusters for clinical-trial design. ([academic.oup.com](https://academic.oup.com/jamia/article/32/3/447/7933305?utm_source=chatgpt.com)) Markey and colleagues evaluated retrieval-augmented LLM generation of clinical-trial documents, while CPRS combined GPT-4 with a knowledge graph for protocol recommendation. ([journals.sagepub.com](https://journals.sagepub.com/doi/full/10.1177/17407745251320806?utm_source=chatgpt.com))

Particularly relevant is the 2025 JMIR study evaluating GPT-4-Turbo-Preview on 20 RCTs selected partly after its training cutoff. It reported 72% overall design accuracy but substantially weaker performance for eligibility criteria and outcome specification, illustrating why temporal separation from pretraining data is critical in this domain. ([jmir.org](https://www.jmir.org/2025/1/e67469/?utm_source=chatgpt.com)) Shin, Bhat and Ramanathan also evaluated GPT-4o for statistical-analysis-plan and PK-PD protocol assessment against regulatory guidance, showing progress toward methodology-specific rather than purely linguistic evaluation. ([pmc.ncbi.nlm.nih.gov](https://pmc.ncbi.nlm.nih.gov/articles/PMC12816432/?utm_source=chatgpt.com)) COMPASS advances this literature through deeper decomposition of protocol reasoning and explicit multi-agent review, but its novelty is weakened by the absence of a contamination-resistant benchmark and direct comparisons with these increasingly structured alternatives.

## 7. Suggested Reviewer Names

For **agentic LLMs and biomedical NLP**, suitable candidates include Qiao Jin, Zifeng Wang, Alban Bornet, and Douglas Teodoro. Their recent work covers LLM-based clinical-trial matching, eligibility reasoning, and structured trial-design representations. ([nature.com](https://www.nature.com/articles/s41467-024-53081-z?utm_source=chatgpt.com))

For **LLM-based clinical-trial protocol generation and evaluation**, suitable candidates include Nigel Markey, Euibeom Shin, Amruta Gajanan Bhat, and Murali Ramanathan. Their recent studies directly address LLM-generated clinical-trial documents, protocol assessment, statistical analysis plans, or regulatory-methodological evaluation. ([journals.sagepub.com](https://journals.sagepub.com/doi/full/10.1177/17407745251320806?utm_source=chatgpt.com))

For **clinical-trial informatics and methodological AI evaluation**, Alban Bornet, Douglas Teodoro, Qiao Jin, and Zifeng Wang would provide complementary expertise in trial informatics, benchmark construction, human evaluation, and clinically grounded LLM assessment. Reviewer conflicts and recent collaboration with the submitting authors should be checked before invitation.

068260
### 1. Overall Assessment

This manuscript develops an instance-retrieval framework for five-class kidney-transplant rejection classification from H&E whole-slide images. UNI embeddings support retrieval of morphologically similar structural-reference patches and diagnostically labelled patches, which are aggregated into structure-aware patient-level representations for normal, borderline TCMR, active TCMR, ABMR, and mixed rejection.

The retrieval design is interpretable and clinically motivated, but the evidence does not meet the generalizability standard expected at Nature Communications. The study is retrospective and single-centre, while robustness is assessed using simulated Reinhard–Macenko stain shifts rather than genuine external cohorts. Cohort accounting also requires clarification because the Methods describe 490 diagnostic cases whereas the comparative analysis repeatedly refers to 200 patients.

### 2. Strengths

The strongest contribution is the explicit separation of structural and diagnostic retrieval. Structural labels are assigned from a pathologist-annotated reference library using cosine similarity, while diagnostic neighbours provide traceable case-level evidence. This is more clinically interpretable than conventional attention-only MIL.

The evaluation includes five-fold patient-level cross-validation, pooled out-of-fold predictions, paired normalization comparisons, bootstrap confidence intervals, ablations, and labelled-library expansion experiments. The full model achieves a pooled macro-AUC of 0.7349 and remains numerically strongest under simulated cross-normalization.

### 3. Weaknesses

The absence of true external validation is the principal limitation. Stain normalization does not capture differences in fixation, scanners, sectioning, laboratory workflow, patient mix, or biopsy composition. The manuscript also lacks demographic subgroup analyses, calibration, clinically interpretable class-specific sensitivity, and direct comparison with transplant pathologists.

Performance remains moderate, and the manuscript does not demonstrate prospective or workflow-level clinical utility. The discrepancy between the 490 cases described in the Methods and the 200-patient comparison cohort further weakens confidence in the evaluation framework.

### 4. Editorial Decision

**Reject.** The retrieval-based formulation is methodologically interesting, but the central claims of robustness and clinical applicability are not supported by independent multi-institutional validation. The work would be more appropriate for **Communications Medicine** after resolving cohort accounting and strengthening external evaluation.

### 5. Suggested Reviewer Expertise

Appropriate reviewers should cover computational pathology using histopathology foundation models and WSI retrieval; multiple-instance and structure-aware representation learning; domain shift, stain normalization and external validation in digital pathology; statistical evaluation and calibration of multiclass medical-AI systems; and kidney-transplant pathology with specific expertise in Banff rejection classification.

### 6. State-of-the-Art Literature Review (Past 3 Years)

The closest clinical comparator is Ye et al., who reported a two-hospital H&E WSI system for kidney-allograft rejection using multi-instance learning, with 906 WSIs from 302 biopsies and an overall three-category AUC of 0.798; they also compared the system directly with transplant pathologists. ([frontiersin.org](https://www.frontiersin.org/journals/immunology/articles/10.3389/fimmu.2024.1438247/full?utm_source=chatgpt.com)) A second 2024 study used Mask R-CNN to quantify renal structures and inflammatory/fibrotic morphology relevant to Banff assessment. ([sciencedirect.com](https://www.sciencedirect.com/science/article/pii/S2001037024002691?utm_source=chatgpt.com)) Recent reviews consequently place the field beyond simple rejection classification toward automated Banff scoring, quantitative morphometry and multimodal clinicopathologic prediction. ([pmc.ncbi.nlm.nih.gov](https://pmc.ncbi.nlm.nih.gov/articles/PMC12052063/?utm_source=chatgpt.com))

The manuscript is more distinctive on retrieval than on rejection classification itself. Alfasly et al. demonstrated in 2025 that UNI, Virchow and GigaPath embeddings can support zero-shot WSI retrieval across TCGA, establishing foundation-model retrieval as an active computational-pathology paradigm. ([nature.com](https://www.nature.com/articles/s41598-025-88545-9?utm_source=chatgpt.com)) The present paper usefully adapts that paradigm to transplant pathology and introduces structure-conditioned evidence aggregation, but its clinical validation is materially narrower than contemporary rejection studies.

### 7. Suggested Reviewer Names

**Saghir Alfasly** would be appropriate for histopathology foundation-model retrieval because of his 2025 Scientific Reports study benchmarking UNI, Virchow and GigaPath for WSI retrieval. ([mayoclinic.elsevierpure.com](https://mayoclinic.elsevierpure.com/en/publications/validation-of-histopathology-foundation-models-through-whole-slid/?utm_source=chatgpt.com)) **Yongrong Ye** would provide directly relevant expertise in AI-based classification of kidney-allograft rejection and subsequent multimodal rejection modelling. ([frontiersin.org](https://www.frontiersin.org/journals/immunology/articles/10.3389/fimmu.2024.1438247/full?utm_source=chatgpt.com)) **Dimitra van Midden** would provide computational nephropathology expertise, particularly AI-assisted interpretation of kidney-transplant biopsies and rejection. ([computationalpathologygroup.eu](https://www.computationalpathologygroup.eu/publications/farr25/?utm_source=chatgpt.com)) **Saghir Alfasly or Ghazal Alabtah** would additionally be suitable for adjudicating whether the retrieval methodology meaningfully advances current foundation-model retrieval approaches; institutional and co-authorship conflicts should be checked before invitation. ([pmc.ncbi.nlm.nih.gov](https://pmc.ncbi.nlm.nih.gov/articles/PMC11787325/?utm_source=chatgpt.com))

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


## 1. Overall Assessment

The manuscript presents Dynomap, an end-to-end framework that converts unordered biomedical tabular data into task-optimized two-dimensional maps through feature gating, trainable spatial coordinates, differentiable Gaussian rendering, and a CNN predictor. It is tested across circulating RNA, platelet RNA, TCGA-BRCA, Parkinson’s voice measurements, Tabula Muris single-cell RNA-seq, and 13 additional tabular datasets.

The contribution is more substantial than a routine benchmark because spatial organization is learned jointly with prediction rather than imposed from fixed feature similarity. The main concerns are validation independence and whether the claimed advance holds against the closest recent tabular-to-image methods.

## 2. Strengths

Dynomap integrates feature selection, spatial arrangement, rendering, and downstream prediction within one differentiable objective. Moran’s I, k-nearest-neighbour spatial coherence, and Integrated Gradients provide explicit analysis of learned structure.

The evaluation is broad. Reported results include 93.0% binary cancer-versus-control accuracy with 4,000 highly variable genes, 92.0% multiclass cancer-subtype accuracy using the 622-gene panel, and 93.7% Parkinson classification accuracy. Comparisons include logistic regression, random forest, XGBoost, SVM, MLP, ModernNCA, TabM and TabPFN.

## 3. Weaknesses

Most biomedical results remain retrospective and internally cross-validated, with no independent external cohort establishing robustness to institution, assay, or batch shifts. The Parkinson dataset contains repeated recordings per participant, yet the manuscript does not clearly document participant-grouped folds; recording-level splitting would create subject leakage. Similar donor-level safeguards should be explicit for single-cell experiments.

The closest tabular-to-image baselines are incomplete. HACNet, MRep-DeepInsight, LM-IGTD, NCTD and recent systematic tabular-to-image benchmarks provide direct tests of whether task-adaptive cartography is genuinely superior. Calibration, confidence intervals and AUROC/PR-AUC are also inconsistently reported.

## 4. Editorial Decision

**Send for Review.** The differentiable, task-adaptive feature cartography is sufficiently distinctive for external assessment. Reviewers should determine whether subject/donor-disjoint validation preserves performance and whether direct comparison with contemporary tabular-to-image methods supports the novelty claim.

## 5. Suggested Reviewer Expertise

Suitable expertise includes deep learning and foundation models for tabular data; differentiable tabular-to-image representation learning and CNN architectures; explainability and spatial-statistical analysis of learned representations; computational genomics and cfRNA liquid biopsy; and machine-learning analysis of Parkinsonian speech biomarkers.

## 6. State-of-the-Art Literature Review — Past 3 Years

The tabular-learning field has advanced rapidly through TabR at ICLR 2024, TabPFN in *Nature* 2025, TabM at ICLR 2025 and TabICL at ICML 2025. These methods establish increasingly strong retrieval, ensemble and foundation-model baselines. Concurrently, NCTD and LM-IGTD have extended tabular-to-image learning, while recent systematic benchmarking questions whether image conversion consistently improves upon strong tabular learners. Dynomap advances this literature by making feature placement task-adaptive and differentiable. Its novelty therefore rests less on tabular-to-image conversion itself than on demonstrating that learned cartography provides reproducible gains over both modern tabular models and the strongest image-conversion alternatives.

## 7. Suggested Reviewer Names

Yury Gorishniy would provide expertise in modern tabular architectures through TabR and TabM. Francisco J. Lara-Abelenda is directly relevant through recent biomedical tabular-to-image and LM-IGTD work. Amir Momen-Roknabadi provides clinically relevant expertise in AI-based cell-free RNA cancer detection with independent-cohort validation. Juan Rafael Orozco-Arroyave is highly relevant to Parkinsonian speech modeling and cross-cohort generalization. A targeted search identified no obvious coauthorship between these candidates and the submitting author group.

## Further Literature — 10 Closely Related Papers Published in the Past 3 Years

1. **Bragilovski M, Kapri Z, Rokach L, Levy-Tzedek S. “TLTD: Transfer Learning for Tabular Data.” *Applied Soft Computing* 147, 110748 (2023). DOI: 10.1016/j.asoc.2023.110748.** Peer-reviewed. **Cited by manuscript:** No, not identified in references 1–98. **Independence:** no submitting-author overlap identified. **Relevance:** converts tabular data to images and combines the representation with transfer learning and knowledge distillation across 25 structured datasets. It is a direct conceptual predecessor for exploiting image-network inductive biases on non-image data.

2. **Medeiros Neto L, Rogerio da Silva Neto S, Endo PT. “A comparative analysis of converters of tabular data into image for the classification of Arboviruses using Convolutional Neural Networks.” *PLOS ONE* 18, e0295598 (2023). DOI: 10.1371/journal.pone.0295598.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** directly compares IGTD and alternative tabular-to-image converters in a biomedical classification setting and therefore provides an important benchmark for Dynomap’s representation claims.

3. **Matsuda T, Uchida K, Saito S, Shirakawa S. “HACNet: End-to-end learning of interpretable table-to-image converter and convolutional neural network.” *Knowledge-Based Systems* 284, 111293 (2024). DOI: 10.1016/j.knosys.2023.111293.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** probably the closest methodological comparator. HACNet jointly trains a hard-attention table-to-image converter and CNN using prediction loss, making the absence of a direct Dynomap-versus-HACNet experiment particularly notable.

4. **Sharma A, López Y, Jia S, Lysenko A, Boroevich KA, Tsunoda T. “Enhanced analysis of tabular data through Multi-representation DeepInsight.” *Scientific Reports* 14, 12851 (2024). DOI: 10.1038/s41598-024-63630-7.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** extends DeepInsight through multiple spatial representations and evaluates single-cell RNA-seq, ATAC-seq and Alzheimer’s molecular data using ResNet-50 and EfficientNet-B6, closely overlapping Dynomap’s high-dimensional biomedical use case.

5. **Lara-Abelenda FJ, Chushig-Muzo D, Peiro-Corbacho P, Gómez-Martínez V, Wägner AM, Granja C, Soguero-Ruiz C. “Transfer learning for a tabular-to-image approach: A case study for cardiovascular disease prediction.” *Journal of Biomedical Informatics* 165, 104821 (2025). DOI: 10.1016/j.jbi.2025.104821.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** applies LM-IGTD to clinical tabular data and explicitly compares CNN-based tabular-to-image learning with TabPFN and conventional models. It is highly relevant to Dynomap’s biomedical generalizability claims.

6. **Alenizy HA, Berri J. “Transforming tabular data into images via enhanced spatial relationships for CNN processing.” *Scientific Reports* 15, 17004 (2025). DOI: 10.1038/s41598-025-01568-0.** Peer-reviewed. **Cited by manuscript:** **Yes, reference 32.** **Independence:** no author overlap identified. **Relevance:** introduces NCTD and benchmarks it against IGTD, DeepInsight, REFINED, TINTO, HACNet and Fotomics on ten datasets. Although cited, it is not included as an experimental comparator and therefore remains directly relevant to the novelty assessment.

7. **Lee J, Kim B. “Zero inflated high dimensional compositional data with DeepInsight.” *PLOS ONE* 20, e0320832 (2025). DOI: 10.1371/journal.pone.0320832.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** adapts tabular-to-image representation learning to zero-inflated high-dimensional biomedical compositional data and validates the approach on paediatric inflammatory bowel disease data, providing another genomics-adjacent comparator.

8. **Selke WD, Sung H, Lee C, Whooley M, Kim W. “Exploring Tabular-to-Image Algorithms for Applying CNNs to Tabular Data.” *IEEE International Conference on Bioinformatics and Biomedicine (BIBM)*, 5066–5073 (2025). DOI: 10.1109/BIBM66473.2025.11356899.** Peer-reviewed conference paper. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** systematically evaluates seven tabular-to-image CNN methods against seven conventional/non-CNN classifiers across 14 datasets, including medical and gene-expression tasks, and finds that tabular-to-image approaches are not uniformly superior. This is a particularly important challenge to Dynomap’s broad performance framing.

9. **Lin Y-R, Wu H-M. “Image generator for tabular data based on non-Euclidean metrics for CNN-based classification.” *PLOS ONE* 21, e0340005 (2026). DOI: 10.1371/journal.pone.0340005.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** extends IGTD using correlation, geodesic, Jensen–Shannon, Wasserstein and tropical distances to encode nonlinear feature relationships. Its genomics experiments make it a direct contemporary alternative to Dynomap’s learned spatial organization.

10. **Mamdouh A, El-Melegy M, Ali S, Kikinis R. “Tab2Visual: Deep learning for limited tabular data via visual representations and augmentation.” *Pattern Recognition* 176, 113173 (2026). DOI: 10.1016/j.patcog.2026.113173.** Peer-reviewed. **Cited by manuscript:** No. **Independence:** no author overlap identified. **Relevance:** transforms heterogeneous tabular data into visual representations and combines them with image augmentation and transfer learning, specifically targeting small datasets common in healthcare. It provides a very recent comparison point for Dynomap’s claims regarding data efficiency and CNN-based tabular representation.
