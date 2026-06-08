# Trackrad202512456
043785 Historical and Current Knee Radiographs for Incident and Progressive Knee Osteoarthritis Risk Prediction

### 1. Overall Assessment
This manuscript presents a transformer-based patch multiple-instance learning (MIL) framework trained on the Multicenter Osteoarthritis Study (MOST) cohort to generate image-derived risk scores for incident and progressive radiographic knee osteoarthritis. The central claim is that dual-timepoint, dual-view radiographic inputs improve risk stratification beyond matched Kellgren-Lawrence (KL) grade and patellofemoral OA (PFOA) features, with the greatest gains for incident OA. The study is methodologically coherent and addresses a clinically motivated question regarding the marginal value of individual radiographic views and timepoints.

The work, however, is confined entirely to MOST. All train, validation, and test partitions are drawn from a single cohort under uniform imaging protocols, making the reported performance figures uninterpretable as evidence of generalisability. The modest and inconsistent AUC gains for progression — best fusion AUC 0.744 versus KL benchmark 0.686 — and the absence of model calibration compound this concern. These limitations substantially undermine the manuscript's suitability for *Nature Communications*.

### 2. Strengths
The experimental design correctly separates two clinically distinct populations — preclinical or early-stage knees (KL < 2) for the incidence task and established-OA knees (KL 2–3) for the progression task. This bifurcation is epidemiologically sound and avoids outcome heterogeneity that weakens many prior OA prediction studies.

The evaluation framework is statistically rigorous. Participant-level bootstrap resampling with 1,000 iterations preserves within-participant knee correlation, and paired comparisons against clinically matched benchmarks directly test the primary hypothesis. Reporting both ROC-AUC and PR-AUC is appropriate given the differential event rates across tasks.

The late-fusion architecture is technically sensible for a moderate-sized dataset. Training single-view transformers with shared encoder weights and task-specific heads, then combining probability scores via logistic regression, limits overfitting while enabling systematic ablation of each radiographic input's contribution. The finding that PA-history fusion is most informative for incidence while current PA plus lateral is most informative for progression is a meaningful empirical result with plausible anatomical interpretation.

### 3. Weaknesses
The absence of external validation is fatal to the manuscript's central clinical claim. All partitions derive from MOST, a predominantly White US cohort. There is no validation against OAI, the CHECK cohort, or any non-US dataset. The reported performance figures cannot be taken as evidence of generalisability. This cannot be resolved without additional data.

Model calibration is not reported. The fusion models produce probability risk scores underlying the clinical stratification claims, yet no calibration curve, Brier score, or reliability diagram is presented. For the progression task with a 68% event rate, a poorly calibrated model can achieve respectable AUC while generating clinically misleading absolute risk estimates. This is a material deficiency.

No subgroup performance is reported across race, sex, or BMI strata despite the cohort including over 11% Black or African American participants. Whether model performance is equitable across demographic groups is unaddressed, a known axis of failure in radiographic AI.

The clinical comparison baseline is underpowered. The all-metrics comparator omits longitudinal clinical variables routinely available in MOST — pain trajectories, WOMAC scores, and BMI trajectories — meaning the apparent imaging advantage may partly reflect the weakness of the chosen comparator rather than the strength of the model.

### 4. Editorial Decision
**Reject.** The entire experimental pipeline — training, tuning, and testing — is conducted within a single cohort under uniform acquisition protocols, and no amount of revision within the current data perimeter can satisfy the external validation requirement. The additional absence of calibration and subgroup analyses compounds the concern. The work would be more appropriately considered at *Osteoarthritis and Cartilage* or *Scientific Reports*, where internally validated deep learning studies in musculoskeletal radiology remain within scope.

### 5. Suggested Reviewer Expertise
Reviewers should include: (1) a specialist in patch-based or multiple-instance learning architectures applied to medical image analysis, with specific experience in longitudinal radiographic modelling; (2) a researcher with expertise in prognostic model evaluation for musculoskeletal disease, including calibration and discrimination methodology consistent with TRIPOD standards; (3) a musculoskeletal radiologist with experience in knee OA imaging assessment within large cohort studies, particularly MOST or OAI; (4) an epidemiologist or biostatistician with experience in clinical prediction model development and external validation; and (5) a clinical rheumatologist or orthopaedic specialist with expertise in knee OA risk stratification and clinical decision-making for incident and progressive disease.

### 6. State-of-the-Art Literature Review
The field of deep learning for knee OA prognosis has advanced substantially since the Tiulpin et al. (Scientific Reports, 2019) multimodal CNN benchmark. The present manuscript does not adequately engage with this landscape. Nguyen et al. (IEEE Transactions on Medical Imaging, 2024) introduced CLIMATv2, a dual-transformer architecture modelling OA as a one-to-many trajectory forecasting problem, with explicit calibration reporting and OAI validation — directly raising the methodological bar for both architecture design and calibration transparency that this manuscript does not meet. Panfilov et al. (IEEE Journal of Biomedical and Health Informatics, 2025) developed an end-to-end multimodal transformer fusing knee radiographs and structural MRI across 2–8 year prediction horizons on OAI, showing that structural MRI alone achieves ROC-AUC 0.70–0.76 and that modality contribution varies substantially with prediction horizon — a finding directly relevant to the view-ablation logic of the present work. Yin et al. (Osteoarthritis and Cartilage, 2024) introduced BikNet, which incorporates contralateral knee information from bilateral PA radiographs and achieves AUC 0.761 for incident OA on OAI with cross-site internal validation, providing a directly competitive result that the authors do not cite. Bayramoglu et al. (Osteoarthritis and Cartilage, 2024–2025) applied a CNN to MOST lateral radiographs with clinical covariates for PFOA-specific progression prediction and achieved AUC 0.86 — exceeding the present manuscript's best progression figure — using a compartment-specific design. Lin et al. (Diagnostics, 2025) trained a vision transformer with external hospital validation on 274 cases, reporting AUROC degradation from 0.808 to 0.709 under distribution shift, quantifying precisely the generalisability cost that the present all-MOST design cannot assess.

### Further Literature (Past 3 Years — Similar Scope)
**1. Nguyen HH, Blaschko MB, Saarakkala S, Tiulpin A. Clinically-Inspired Multi-Agent Transformers for Disease Trajectory Forecasting from Multimodal Data. *IEEE Transactions on Medical Imaging*. 2024;43(1):529–541.**
Develops CLIMATv2, a dual-transformer framework formulating KOA prognosis as a one-to-many trajectory forecasting problem using radiographs and clinical covariates from OAI. Directly comparable in its use of transformer-based architectures for longitudinal OA risk prediction, and sets a higher bar by reporting both discrimination and calibration metrics.

**2. Panfilov E, Saarakkala S, Nieminen MT, Tiulpin A. End-to-End Prediction of Knee Osteoarthritis Progression with Multimodal Transformers. *IEEE Journal of Biomedical and Health Informatics*. 2025. DOI: 10.1109/JBHI.2025.3536170.**
An end-to-end multimodal transformer fusing knee X-ray and structural/compositional MRI from OAI across 1–8 year prediction horizons. Directly addresses the view-contribution question using a more powerful imaging modality, and its finding that modality value varies by prediction horizon mirrors the task-specific view findings in the present manuscript.

**3. Yin R, Chen H, Tao T, et al. Expanding from Unilateral to Bilateral: A Robust Deep Learning-Based Approach for Predicting Radiographic Osteoarthritis Progression. *Osteoarthritis and Cartilage*. 2024;32(3):338–347.**
Introduces BikNet, which uses contralateral knee PA radiographs as auxiliary input and achieves AUC 0.761 for incident OA on OAI with cross-site validation. Shares the manuscript's radiograph-only, PA-view design philosophy while extending it to bilateral information — a dimension the present work does not explore.

**4. Lin C-H, et al. Simplifying Knee OA Prognosis: A Deep Learning Approach Using Radiographs and Minimal Clinical Inputs. *Diagnostics*. 2025;15(19):2543.**
Trains a vision transformer on OAI with external validation on 274 cases from a Taiwanese hospital, reporting AUROC degradation from 0.808 to 0.709 under cohort shift. Most directly relevant to the external validity concern raised here, as it quantifies the performance cost of applying a model trained on one OA cohort to an independent clinical population.

**5. Wang T, Liu H, Zhao W, et al. Predicting Knee Osteoarthritis Progression Using Neural Network with Longitudinal MRI Radiomics and Biochemical Biomarkers. *PLOS Medicine*. 2025;22(8):e1004665.**
Uses longitudinal MRI radiomics and biochemical biomarkers from OAI to predict structural KOA progression, achieving robust discrimination with calibrated outputs. Shares the longitudinal feature extraction philosophy of the present manuscript and highlights the gains available from incorporating biochemical and symptomatic variables that the present radiograph-only design forgoes.

**6. Bayramoglu N, et al. Deep Learning for Patellofemoral OA Progression Prediction from Lateral Knee Radiographs. *Osteoarthritis and Cartilage*. 2024–2025.**
Applies a deep CNN to MOST lateral radiographs with clinical features (age, sex, BMI, WOMAC, TF KL grade) to predict 7-year PFOA progression, achieving AUC 0.86. Directly overlaps with the present manuscript's use of MOST lateral views and PFOA endpoint, offering a stronger compartment-specific benchmark that Jiang et al. do not engage with.

045098 Online healthcare platforms reshape disease-specific access and triage pathways in China

### 1. Overall Assessment

This manuscript uses 48,861 matched patient-doctor consultation records from the Haodf Doctor Recommendation Dataset to examine how physician-attention concentration and digital triage outcomes vary across six disease groups on a Chinese online consultation platform. The central claim is that online medical platforms do not uniformly expand access but reorganise care through disease-specific concentration, reputation sorting, and triage-oriented decision-making. The framing — that digital health inequality operates within platforms, not only at the access threshold — is conceptually valuable and underdeveloped in the existing literature.

The work combines concentration metrics (Gini coefficient, HHI, effective physician number), multivariable logistic regression, and hyperparameter-tuned XGBoost with SHAP attribution. Two concerns are decisive. First, the manuscript is entirely confined to a pre-constructed six-disease secondary dataset not designed for this research question; the absence of socioeconomic metadata, geographic tier, and longitudinal follow-up prevents any direct connection between within-platform patterns and population-level inequity, yet the equity narrative throughout the discussion implies such a connection. Second, the XGBoost models achieve AUROC of only 0.608 (top-ten flow doctor matching) and 0.658 (offline referral), which limits confidence in the SHAP-derived mechanistic interpretations that form a substantial portion of the contribution.

---

### 2. Strengths

The disease-stratified physician-attention concentration analysis is the manuscript's most technically distinctive contribution. Simultaneous triangulation across top-share measures, Gini, and HHI-derived effective physician number reveals that concentration is not a platform-level constant but a disease-specific property — cold (top-ten share 55.3%, Gini 0.779, effective physicians 21.3) versus depression (22.3%, Gini 0.687, effective physicians 106.7) — a finding not previously demonstrated in the Chinese online consultation literature.

The adjusted logistic regression design cleanly separates physician-attention concentration from triage burden as distinct analytical outcomes. The finding that cold and diabetes have higher odds of top-ten flow doctor matching relative to CHD (OR 2.12 and 1.66 respectively) but lower odds of offline referral (OR 0.58 and 0.69) demonstrates that these are non-redundant processes, preventing conflation that prior work has not explicitly avoided.

The two-model XGBoost architecture with SHAP domain-level attribution adds interpretive value beyond regression. The identification that disease group dominates the concentration model (46% domain contribution) while physician reputation index dominates the referral model (29%) is coherent and actionable for platform governance, even at modest discriminatory performance.

---

### 3. Weaknesses

The dataset is a pre-packaged secondary resource designed for doctor recommendation research, not platform equity analysis. The six disease categories are fixed, non-random, and non-representative of the full Haodf consultation universe. The absence of socioeconomic status, geographic tier, insurance status, and income prevents any direct inference about who is disadvantaged by disease-specific concentration patterns. The equity framing throughout the discussion is stronger than the evidence supports.

The rule-based triage classification underpins every downstream analysis, yet no inter-rater reliability statistic — Cohen's kappa or percent agreement — is reported for any of the eight triage categories. Labels were checked for face validity via stratified sample review, which is insufficient for a high-tier journal when triage outcomes feed directly into logistic regression and XGBoost models as primary outcomes.

The gender coding procedure — inferring coding direction from the near-exclusive presence of pregnancy-related fields in one group — is methodologically informal and unvalidated. Sex is retained as a covariate across all models without sensitivity analysis, despite its clinical relevance to multiple disease groups including depression and diabetes.

The physician reputation index conflates platform visibility with clinical quality. Without physician-side capacity variables such as total active consultations, response times, or pricing, residual confounding by physician volume in the offline referral model cannot be excluded. This is not acknowledged adequately.

---

### 4. Editorial Decision

**Send for Review.** The disease-stratified concentration analysis and the analytical separation of concentration from triage burden represent genuine contributions to the digital health equity literature. Reviewers should adjudicate: (i) whether the equity framing is defensible given the absence of socioeconomic linkage; (ii) whether rule-based triage classification without formal inter-rater reliability satisfies evidentiary standards; and (iii) whether the SHAP attribution at AUROC 0.608–0.658 supports the mechanistic claims advanced in the discussion.

---

### 5. Suggested Reviewer Expertise

Reviewers should include expertise in the following areas: concentration metrics and inequality measurement in digital healthcare markets, with specific experience applying Gini coefficient and HHI to physician-visit distributions in online health communities; gradient-boosted tree modelling with SHAP-based feature attribution, including familiarity with the interpretive limits of low-AUROC models deployed as explanatory rather than predictive instruments; rule-based and NLP-based clinical text classification for triage outcome labelling in Chinese-language medical records, including inter-rater reliability methodology; multivariable logistic regression for health services research outcomes, particularly where physician-level and patient-level covariates are correlated; and clinical expertise in chronic disease management and mental health care delivery in the Chinese outpatient context, including familiarity with the Internet Plus Healthcare policy framework.

---

### 6. State-of-the-Art Literature Review (Past 3 Years)

The concentration of online physician attention in Chinese platforms has been documented since the 2016–2019 era, which established the 80/20 Pareto structure for e-consultation markets. More recent work has shifted toward specific mechanisms. Yang et al. (*BMC Health Services Research*, 2025) analysed 594,695 consultations from 30 Internet hospitals across 11 Chinese provinces, documenting operational status, physician workload dynamics, and the determinants of consultation outcomes at scale — the most directly comparable multi-disease empirical study to the present manuscript. Liu et al. (*JMIR*, 2024) used a quasi-experimental design to examine the impact of internet hospital adoption on outpatient frequency and expenses, finding differential effects for urban and rural patients at a southeastern tertiary hospital, placing offline-referral displacement in a causal rather than descriptive frame. Wang et al. (*JMIR*, 2024) conducted a mixed-methods study of 18,473 patients receiving online follow-up services at a Sun Yat-sen University internet hospital, examining accessibility, cost, and physician-reported quality concerns, including workload implications of chronic disease follow-up online. On the equity and access side, Sun et al. (*JMIR*, 2025) used triangulated provincial and national survey data to characterise internet medical service utilisation disparities among Chinese adult patients post-COVID, identifying age and education as the strongest negative predictors — a necessary complement to any within-platform inequality analysis. The manuscript engages inadequately with the gender discrimination literature on Chinese platforms: recent work has documented that female physicians receive systematically lower consultation volumes and prices than males with equivalent credentials, and that platform ranking algorithms amplify this gap, which is directly relevant to the reputation sorting mechanism the authors propose. The manuscript should also engage with Fan et al. (*Information Systems Research*, 2023), which used a natural experiment to show that opening online consultations displaces offline appointments differentially by disease severity — a structural finding that speaks directly to the offline referral patterns described here.

---

### 7. Suggested Reviewer Names

For **concentration metrics and inequality measurement in online healthcare markets**: Yan Xu (University of Connecticut; *Management Science* 2021, online reviews and physician demand); Wenjing Duan (George Washington University; platform dynamics in healthcare); Zhaohua Deng (Huazhong University; physician effort and reputation on Haodf).

For **gradient-boosted tree modelling and SHAP interpretation**: Scott Lundberg (University of Washington; SHAP framework originator); Carolin Molnar (Ludwig Maximilian University; interpretable machine learning); researchers active in XGBoost-SHAP applications in health services research (e.g., Ponce-Bobadilla group, *Clinical and Translational Science*, 2024).

For **clinical text classification in Chinese-language medical records**: researchers active in the MedDG and IMCS Chinese clinical dialogue datasets; Donghua Chen (clinical NLP, Chinese medical text).

For **chronic disease management and digital health governance in China**: Fang Yang (Capital Medical University; *JMIR* Internet Plus Healthcare policy); Xiaolin Tan (Peking University; Healthy China 2030 digital health policy).

---

### Further Literature

The following five papers from the past three years share substantial thematic or methodological scope with the present manuscript and represent the most relevant concurrent literature.

**1. Yang M, Yan Y, Xu Z, et al. The status and challenges of online consultation service in internet hospitals operated by physical hospitals in China: a large-scale pooled analysis of multicenter data. *BMC Health Services Research* 25, 611 (2025).**
This is the closest comparator in scope: a retrospective analysis of 594,695 online consultations across 30 Internet hospitals in 11 provinces (2020–2021), with a five-category consultation classification, multivariate logistic regression, and workload-response modelling. Unlike the present manuscript, it operates across hospital-based Internet hospitals rather than a third-party commercial platform, providing an important structural contrast. The scale and multi-centre design set a methodological benchmark against which the present six-disease, single-platform analysis should be positioned.

**2. Liu Y, Jin H, Yu Z, Tong Y. Impact of Internet hospital consultations on outpatient visits and expenses: quasi-experimental study. *Journal of Medical Internet Research* 2024; 26:e57609.**
This study uses a quasi-experimental difference-in-differences design to estimate the causal effect of internet hospital adoption on offline outpatient frequency and expenses, stratified by urban and rural patients. The finding of differential displacement effects by patient location speaks directly to the offline referral mechanism examined in the present manuscript. The paper establishes a causal counterfactual framework — absent from the current study — against which the cross-sectional adjusted odds ratios for offline referral should be interpreted.

**3. Wang K, Zou W, Lai Y, et al. Accessibility, cost, and quality of an online regular follow-up visit service at an internet hospital in China: mixed methods study. *Journal of Medical Internet Research* 2024; 26:e54902.**
A mixed-methods study of 18,473 patients at a Sun Yat-sen University internet hospital, covering geographic distribution, chronic disease composition, physician workload burden, and qualitative accounts of quality safeguards. The concentration of usage among geographically proximate, middle-aged, chronic disease patients is directly relevant to the present manuscript's findings on diabetes and CHD consultation pathways, and the physician-reported workload implications of online follow-up parallel the triage burden construct developed here.

**4. Sun Z, Chen X, Qian D. Disparities in internet medical service utilisation among patients in post-COVID-19 China: cross-sectional study of data from provincial field and national online surveys. *Journal of Medical Internet Research* 2025; 27:e60546.**
Using triangulated provincial and national survey data, this study documents persistent disparities in internet medical service utilisation by age, education, and socioeconomic status in post-pandemic China. It provides the population-level access context that the present manuscript's within-platform analysis cannot supply. The finding that adults aged 60 and above and those with lower educational attainment are the least likely to use or prefer internet medical services is a necessary backdrop to any claim about disease-specific concentration among platform users.

**5. Wang P, Huang Y, Li H, Xi X. Public preferences for online medical consultations in China: a discrete choice experiment. *Frontiers in Public Health* 11, 1282387 (2023).**
This discrete choice experiment with 668 respondents quantifies patient willingness-to-pay for physician attributes in online consultation, finding that evaluation score is the most valued attribute (WTP ¥107 for higher-scored physicians) and that preferences vary significantly across patient subgroups. The results ground the reputation-sorting mechanism proposed in the present manuscript in revealed preference data, and the subgroup heterogeneity findings raise the question — not addressed in the current study — of whether disease group differences in concentration partly reflect differential reputation sensitivity among patient populations with different conditions.

**6. Gu H, Cai Y-F, Sun K, Zhao T-F. Equity and spatial accessibility of healthcare resources in online health community network. *Frontiers in Physics* 11, 1336624 (2024).**
This study analyses Good Doctor Online platform consultation data from 2020 to 2023, examining both geographic equity and temporal consultation patterns. The observation that platform usage remains spatially concentrated — with most consultations originating near provider locations — directly challenges the assumption that online platforms dissolve spatial inequality, complementing the present manuscript's finding that physician attention concentration persists and varies by disease. The temporal consultation patterns documented (peaks at lunch and after-hours) have implications for interpreting disease-specific triage decisions made under time-pressure contexts not captured in the present dataset.

044278 A Real-World Agentic Patient Service System with Large-Scale Retrospective Evaluation  

## 1. Overall Assessment
This manuscript describes HEALER, a hierarchical multi-agent LLM framework for post-discharge patient service, evaluated retrospectively across 134 hospitals, 26,772 patients, and 80,858 conversational interactions spanning the 2025 calendar year in China. The central claim is that hierarchical intent resolution and constrained tool execution via the Model Context Protocol can support scalable, safety-oriented patient service workflows superior to RAG-only and workflow-based LLM baselines.

The multi-center deployment scale is genuinely uncommon in the published clinical AI literature. However, the evaluation is observational and retrospective throughout. The longitudinal architecture comparison conflates system maturation, physician learning effects, and patient population drift with system-specific performance gains. Critically, no hard clinical outcome data are reported; the absence of readmission rates, adverse events, or validated patient-reported outcomes renders all clinical benefit claims indirect and unverified.

## 2. Strengths

The deployment scale is the paper's defining strength. With 80,858 real-world interactions across 30 clinical departments spanning 23 Chinese provinces, this represents one of the largest prospectively deployed clinical LLM systems in the published literature, substantially exceeding prior implementation studies that have examined hundreds to low thousands of contacts in single-institution settings.

The independent physician adjudication design is methodologically sound. Five board-certified physicians from three institutions, fully blinded to system identity, evaluated 1,268 stratified samples across four structured Likert dimensions. An ICC of 0.82 (95% CI: 0.78–0.86) confirms high inter-rater reliability and compares favorably to the LLM-as-judge paradigm used in many recent clinical AI papers.

The escalation audit covering 294 consultation events, prospectively categorized into mandatory, discretionary, and autonomous tiers with expert review of all non-escalated cases, provides a structured and transparent safety profile. Reporting only 2/24 mandatory-category non-escalations as clinically unreasonable, rather than aggregate escalation rates, is an appropriate framing of agentic system safety.

The ITS analysis anchored on the February 17 deployment date, restricted to a balanced physician panel, with HAC-robust standard errors and a transition-week sensitivity analysis, is a methodologically defensible quasi-experimental design for an observational deployment context.

## 3. Weaknesses

The absence of hard clinical outcomes is the fundamental limitation. The manuscript does not assess readmission, adverse clinical events, treatment adherence, disease control, or mortality. Text-derived sentiment probability via a locally deployed Chinese StructBERT classifier (Δp = 0.037) is not a validated proxy for patient satisfaction or clinical benefit. A system deployed to 26,772 patients over a full year across 134 hospitals should be able to report at least secondary health outcome signals.

The longitudinal architecture comparison is substantially confounded. The RAG, Workflow-LLM, and HEALER evaluation periods are drawn from non-concurrent temporal windows with different physician cohorts, patient populations, seasonal demand patterns, and system maturity states. Confounding by physician familiarity accumulation and deployment-phase learning effects is unaddressed. The 509/322/437 cross-period samples are neither paired on case mix nor adjusted for patient-level covariates.

The competing interests require material scrutiny. Two authors hold equity in Shanghai Hengfang Health Technology Co., Ltd., the commercial platform through which HEALER is deployed, and the system was evaluated on data generated by that same deployment. No pre-registered protocol, third-party audit, or independent replication dataset is referenced. For a manuscript reporting over 80,000 real patient interactions through a commercially operated system, this conflict is material and must be explicitly managed.

## 4. Editorial Decision

**Send for Review**, with major reservations. The deployment scale and ITS design have genuine merit and place this paper in a thin but important evidence base. Reviewers should adjudicate three specific questions: whether temporal confounders are sufficiently controlled in the architecture comparison; whether the available data support any inference about patient health impact or whether claims must be further scoped; and whether the conflict of interest situation is compatible with Nature Communications editorial standards without additional mitigating conditions.

---

## 5. Suggested Reviewer Expertise

Reviewers should collectively cover: (1) hierarchical multi-agent LLM architectures for clinical workflow automation, specifically tool-grounded execution and intent resolution in healthcare settings; (2) quasi-experimental and interrupted time series methods for health services research, including segmented regression, HAC-robust estimation, and longitudinal confounding in observational deployment studies; (3) clinical safety evaluation of patient-facing AI systems, with expertise in escalation framework design and human oversight mechanisms; (4) post-discharge care coordination and digital patient engagement in high-volume tertiary care systems, preferably in the Asia-Pacific context; and (5) research ethics and conflict of interest governance in commercially deployed clinical AI studies.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The past three years have seen rapid expansion of LLM deployment in patient-facing clinical communication, establishing a competitive landscape against which HEALER must be precisely situated. Wan et al. (*Nature Medicine*, 2024) randomized 2,185 participants to nurse-only versus nurse-LLM collaboration at outpatient reception across two Chinese medical centers, demonstrating higher patient satisfaction (3.91 vs. 3.39, P < 0.001) and more efficient query resolution — providing an RCT benchmark that single-arm retrospective deployments must now justify departing from. Han et al. (*Nature Medicine*, 2026) subsequently tested the PreA LLM chatbot in a 2,069-patient RCT across 24 specialties and 111 clinicians, showing a 28.7% reduction in specialist consultation duration — directly paralleling HEALER's efficiency claims but under a controlled design. These two trials define the methodological ceiling the current manuscript does not reach.

On the draft-reply paradigm, Chen et al. (*Lancet Digital Health*, 2024) and Garcia et al. (*JAMA Network Open*, 2024) both evaluated LLM-generated draft responses to EHR patient portal messages, reporting efficiency gains and physician workload reductions in real-world deployments, but also highlighting performance variability across specialties and limited adoption rates. Tai-Seale et al. (*JAMA Network Open*, 2024) further characterized physician adoption patterns and burden reduction in a prospective quality-improvement study, finding that adoption was moderate and time savings marginal — raising questions about whether HEALER's reported reductions in manual physician responses (5.59 to 2.69 per physician-week) reflect a fundamentally different deployment model or simply higher system autonomy without equivalent evidence of safety. Collectively, this inbox-drafting literature frames HEALER's physician adoption analysis but highlights the absence of a direct comparison to standard EHR-integrated LLM drafting approaches. On agentic system evaluation methodology, Mehandru et al. (*npj Digital Medicine*, 2024) and Johri et al. (*Nature Medicine*, 2025) provide evaluation frameworks for clinical LLM agents that the current manuscript partially implements but does not fully satisfy, particularly with respect to calibration, fairness subgroup reporting, and pre-registered outcome definitions.

---

## 7. Suggested Reviewers

**Multi-agent LLM architectures and clinical NLP:**
- Eric J. Topol (Scripps Research Translational Institute)
- Danielle Bitterman (Harvard Medical School / Dana-Farber Cancer Institute)
- Zhiyong Lu (NIH National Library of Medicine)

**Quasi-experimental design and health services research methods:**
- Atul Butte (University of California San Francisco)
- Isaac Kohane (Harvard Medical School)

**Clinical AI safety, HITL systems, and patient-facing AI governance:**
- Nigam Shah (Stanford University)
- Leo Anthony Celi (MIT / Beth Israel Deaconess Medical Center)

**Post-discharge care and patient service workflows (clinical):**
- David W. Bates (Brigham and Women's Hospital)
- Adam Wright (Vanderbilt University Medical Center)

---

## Further Literature: Papers of Similar Scope (Past 3 Years)

1. **Wan P, Huang Z, Tang W, et al. Outpatient reception via collaboration between nurses and a large language model: a randomized controlled trial. *Nature Medicine*, 30(10):2878–2885, 2024.** This RCT randomized 2,185 outpatients across two Chinese medical centers to nurse-only versus nurse-LLM (SSPEC) collaboration at clinical reception. Patient satisfaction was significantly higher in the collaboration arm, and the LLM resolved a greater proportion of queries within two rounds (68.0% vs. 50.5%, P = 0.009). The study offers the most direct methodological comparator to HEALER: a real-world Chinese tertiary hospital setting with patient-facing LLM integration and measurable clinical workflow outcomes, but with the critical advantage of a randomized controlled design.

2. **Han S, et al. An LLM chatbot to facilitate primary-to-specialist care transitions: a randomized controlled trial. *Nature Medicine*, 2026 (online ahead of print).** The PreA chatbot was evaluated in 2,069 patients across 24 specialties and 111 clinicians in a three-arm RCT (chatbot-only, chatbot-with-staff, no chatbot), demonstrating a 28.7% reduction in specialist consultation duration in the chatbot-only arm (P < 0.001). The study directly addresses patient-physician communication at the care transition interface — identical to HEALER's stated scope — and demonstrates that RCT-level evidence is feasible in this deployment context, making the current manuscript's retrospective observational design a meaningful evidentiary limitation rather than a merely logistical one.

3. **Garcia P, Ma SP, Shah S, et al. Artificial intelligence–generated draft replies to patient inbox messages. *JAMA Network Open*, 7(3):e243201, 2024.** GPT-3.5 Turbo and GPT-4 were evaluated for generating draft responses to patient portal messages in gastroenterology, hepatology, and primary care. Physician-rated quality of AI drafts was comparable to human replies on safety and accuracy, with efficiency gains reported for routine administrative queries. This study establishes the single-physician-speciality, non-agentic draft-reply benchmark — informing interpretation of HEALER's physician adoption rates and semantic similarity analyses, but also highlighting that standard EHR-integrated LLM drafting achieves substantial efficiency gains without the infrastructure complexity of a hierarchical multi-agent architecture.

4. **Tai-Seale M, Baxter SL, Vaida F, et al. AI-generated draft replies integrated into health records and physicians' electronic communication. *JAMA Network Open*, 7(4):e246565, 2024.** A prospective quality-improvement study across family medicine and general internal medicine at a large US academic health system evaluated Epic-integrated GPT-4 drafts for EHR inbox messages. Draft generation took a mean of 55 seconds; adoption was modest (roughly 20%) with significant burden reduction and burnout score improvements. The study provides the most rigorous characterization of real-world adoption dynamics and physician behavior change under AI drafting assistance, directly contextualizing HEALER's claim of reduced manual physician responses (5.59 to 2.69 per physician-week).

5. **Mehandru N, Miao BY, Rodriguez Almaraz E, et al. Evaluating large language models as agents in the clinic. *npj Digital Medicine*, 7(1):84, 2024.** This methodological paper proposes AI-SCE (AI Structured Clinical Examination) frameworks for evaluating LLM agents deployed in clinical settings, drawing analogy to autonomous vehicle safety evaluation paradigms. The authors argue that single-task benchmark performance is insufficient and that agent evaluation must cover multi-step reasoning fidelity, escalation behavior, and real-world edge-case robustness. HEALER's escalation audit partially implements these recommendations, but the paper does not cite this framework and does not report multi-step reasoning fidelity or edge-case coverage in a form that satisfies the AI-SCE criteria.

6. **Johri S, Jeong J, Tran BA, et al. An evaluation framework for clinical use of large language models in patient interaction tasks. *Nature Medicine*, 31(1):77–86, 2025.** This framework paper defines structured evaluation criteria for patient-interaction LLMs spanning factual accuracy, safety, communication quality, and workflow integration, with specific attention to failure modes arising from hallucination and inappropriate escalation decisions. The HEALER evaluation adopts several aligned dimensions (clinical safety, routing logic, operational clarity, empathy) but does not address calibration, does not report subgroup-level performance across patient demographics, and uses a locally deployed sentiment classifier rather than a validated patient satisfaction instrument — gaps that reviewers applying this framework would flag as materially incomplete.

044685 HERA: A Hierarchical-Compensatory Ranking Framework for Paired Benchmarking with Data-Driven Effect-Size Thresholds  

## 1. Overall Assessment

This manuscript introduces HERA, a MATLAB-based non-parametric ranking toolbox for comparing small candidate sets (3–15) across up to three user-defined metrics using paired observations. The framework combines Wilcoxon signed-rank testing with Holm–Bonferroni correction, Cliff's Delta, and a bootstrap-derived Relative Mean Difference (RelDiff) threshold in a conjunctive "win" criterion. A three-stage hierarchical-compensatory sorting algorithm resolves multi-metric trade-offs without subjective weighting. The problem statement — that standard benchmarking conflates statistical significance with practical relevance and fails to integrate magnitude-based thresholds into a unified ranking — is methodologically important.

The work is technically careful and transparently implemented. However, it does not meet the novelty bar for Nature Communications Digital Health. The core statistical components are individually well-established, and the empirical ROPE operationalized here closely parallels Benavoli et al.'s Bayesian signed-rank framework (JMLR, 2017). The validation is conducted entirely on synthetic data, and the neuroimaging use case substitutes Monte Carlo-simulated data for real patient measurements due to "institutional data protection constraints." These two gaps — limited methodological novelty and the absence of any real-data demonstration — are the primary grounds for rejection.

---

## 2. Strengths

The data-driven threshold mechanism is the most technically original contribution. Rather than requiring the user to specify a minimally important difference, HERA derives thresholds empirically from the percentile bootstrap distribution of all pairwise effect sizes, augmented by an SEM-based lower bound inspired by the Smallest Worthwhile Effect concept. This operationalizes an empirical ROPE within a non-parametric framework without Bayesian priors — a practical advance over toolboxes such as pyDecision or RMCDA that rely on user-specified numerical weights.

The validation suite of 19 automated tests is commendable. It covers small-sample exact Wilcoxon computation (n < 16), MCAR data loss up to 60%, cycle detection via Condorcet paradox injection, rank stability under cluster bootstrapping, and a 15-candidate full-logic test. Monte Carlo convergence analysis across 400 simulated datasets demonstrates BCa interval convergence at 100% and ranking convergence at 99.2%. The sensitivity analysis via Borda Count aggregation across all permutations of the metric hierarchy is a principled approach that most MCDM toolboxes do not provide.

The reproducibility infrastructure is strong: full analysis state exported in JSON and CSV, automated PDF reports with win/loss matrices and Sankey diagrams for rank-shift attribution, and a publicly archived codebase with Python interface. These features align with the BIAS reporting framework and Metrics Reloaded standards increasingly required in biomedical image analysis.

---

## 3. Weaknesses

The validation relies entirely on synthetic data. The neuroimaging use case uses Monte Carlo-simulated data calibrated to the distributional characteristics of real MRI image quality metrics, not actual patient measurements. HERA has therefore not been validated on any real cohort. For Nature Communications Digital Health, a real-data demonstration — even with a small, properly consented dataset — is expected.

The novelty positioning is insufficiently substantiated. The conjunctive win criterion (p < α, |d| > θ_d, RelDiff > θ_RelDiff) is conceptually related to Benavoli et al.'s Bayesian signed-rank test with ROPE (JMLR, 2017), cited but not benchmarked against. There is no empirical comparison against the Bayesian hierarchical approach, Demšar's critical-difference diagram procedure, ChallengeR (Wiesenfarth et al., Scientific Reports, 2021), or Soft Condorcet Optimization. The claim of superiority over existing approaches remains asserted rather than demonstrated.

RelDiff is set to zero when mean(X) + mean(Y) = 0, a scenario arising naturally with z-score transformed metrics, accepting a Type II error by design. This failure mode is unacknowledged and untested. For biomedical imaging applications where metrics are routinely standardized prior to multi-metric analysis, this is a material limitation that could silently suppress valid effect detection.

---

## 4. Editorial Decision

**Reject.** Despite technically careful execution, the manuscript does not advance the field sufficiently relative to existing non-parametric and Bayesian ranking frameworks to merit publication in Nature Communications Digital Health. The absence of any real-data validation, the lack of head-to-head empirical comparison against established competitors, and the unaddressed RelDiff failure mode under metric standardization represent fundamental gaps not resolvable by revision of the current study design. The manuscript is better suited to *SoftwareX*, *Journal of Statistical Software*, or *PLOS Computational Biology*, where toolbox descriptions with synthetic validation are standard.

---

## 5. Suggested Reviewer Expertise

Reviewers should be drawn from the following areas: (1) non-parametric statistics for multi-comparison benchmarking, including bootstrap methods for paired data and family-wise error rate control; (2) Multi-Criteria Decision Analysis methodology, specifically outranking and lexicographic approaches with expertise in the ELECTRE, PROMETHEE, and Bayesian signed-rank test literature; (3) biomedical image analysis challenge design and ranking methodology, with familiarity with the BIAS reporting framework and the Metrics Reloaded recommendations (Reinke et al., Nature Methods, 2024); (4) MRI image quality assessment and neuroimaging methodology, including contrast enhancement evaluation and signal-to-noise characterisation in clinical MRI; and (5) open-source scientific software evaluation, including reproducibility standards, computational benchmarking, and toolbox validation methodology.

---

## 6. State-of-the-Art Literature Review

The problem of robust multi-metric ranking under paired observations sits at the intersection of three active literatures. In the statistical comparison of classifiers, Benavoli et al. (JMLR, 2017) and the Bayesian Bradley-Terry model (arXiv, 2022) established that posterior-based inference with explicit regions of practical equivalence avoids the systematic limitations of frequentist post-hoc tests. HERA's empirical ROPE is conceptually aligned with this approach but implemented entirely within a frequentist bootstrap framework; no systematic comparison is provided. In the biomedical image analysis challenge literature, Maier-Hein et al. (Nature Communications, 2018) demonstrated that challenge rankings are highly sensitive to metric choice and aggregation strategy; the subsequent Metrics Reloaded initiative (Reinke et al., Nature Methods, 2024) provides a comprehensive metric selection framework for image analysis tasks. HERA is designed to operate downstream of metric selection, but the relationship to these standards is not articulated. ChallengeR (Wiesenfarth et al., Scientific Reports, 2021) — an open-source R toolkit for bootstrap-based ranking uncertainty analysis with blob plots, Kendall's τ stability quantification, and Holm-corrected pairwise significance testing — is the most directly comparable existing toolbox, yet it is neither cited nor compared against. Zhang et al.'s lexicographic optimization approaches for multi-criteria sorting (Computers & Operations Research, 2025) further extend the methodological landscape in which HERA situates itself, with more principled treatment of non-monotonic criteria. HERA advances the field by combining conjunctive effect-size filtering with a compensatory hierarchical sorting algorithm and providing a complete audit trail, but the positioning as a step-change advance over the existing landscape is overstated given these unengaged contemporaries.

---

## 7. Suggested Reviewer Names

**Non-parametric statistics / bootstrap methods:**  
Janez Demšar (University of Ljubljana), Alessio Benavoli (Trinity College Dublin), Ullrich Köthe (Heidelberg University), Achim Zeileis (University of Innsbruck)

**MCDM methodology:**  
Milosz Kadzinski (Poznan University of Technology), Salvatore Greco (University of Catania), Roman Slowinski (Poznan University of Technology), José Rui Figueira (IST Lisbon)

**Biomedical image analysis benchmarking:**  
Lena Maier-Hein (DKFZ Heidelberg), Annika Reinke (DKFZ Heidelberg), Spyridon Bakas (University of Pennsylvania), Bjoern Menze (University of Zurich)

**MRI image quality / neuroimaging:**  
Ralf Deichmann (Goethe University Frankfurt — note: potential COI, acknowledged in manuscript), Frithjof Kruggel (UC Irvine), Nikolaus Weiskopf (MPI Leipzig)

---

## Further Literature

The following six papers from the past three years share substantive methodological or applied scope with HERA and represent the immediate competitive landscape.

1. **Maier-Hein L, Reinke A, Godau P, et al. Metrics Reloaded: recommendations for image analysis validation. *Nature Methods* 21, 195–212 (2024). doi:10.1038/s41592-023-02151-z**  
A 73-author international consensus framework developed via a multi-stage Delphi process for problem-aware metric selection in biomedical image analysis. It introduces the "problem fingerprint" concept to guide researchers from task definition through metric choice and validation. Directly relevant because HERA is designed to operate as a downstream ranking layer after metric selection; the absence of any articulation of how HERA interacts with or extends the Metrics Reloaded recommendations is a notable gap in positioning.

2. **Zhang Z, Li Z, Yu W. Lexicographic optimization-based approaches to learning a representative model for multi-criteria sorting with non-monotonic criteria. *Computers & Operations Research* 175, 106917 (2025). doi:10.1016/j.cor.2024.106917**  
Proposes threshold-based value-driven sorting procedures with lexicographic optimization to learn representative models from assignment example preference information, explicitly handling non-monotonic criteria through marginal value transformation functions. Closely parallels HERA's hierarchical-compensatory logic and use of lexicographic principles, but derives thresholds from preference disaggregation rather than empirical bootstrapping. Directly competing work that the manuscript does not engage with.

3. **Wiesenfarth M, Reinke A, Landman BA, et al. Methods and open-source toolkit for analyzing and visualizing challenge results. *Scientific Reports* 11, 2369 (2021); actively maintained and widely adopted through 2024–2025.**  
ChallengeR is the closest existing toolbox to HERA in functional scope: it provides bootstrap-based ranking stability quantification (blob plots, violin plots), Holm-corrected pairwise Wilcoxon testing, Kendall's τ uncertainty quantification, and multi-task challenge reporting. Implemented in R with open-source license and adopted as standard practice in numerous biomedical image analysis challenges (crossMoDA, LNQ 2023, MARIO 2025). The absence of any citation or comparative evaluation against ChallengeR is a material omission in the manuscript.

4. **Rodemann T, Dietrich F, et al. Statistical Multicriteria Evaluation of LLM-generated Text. *arXiv* 2506.18082 (2025).**  
Introduces a multi-criteria statistical evaluation framework for LLM outputs using stochastic dominance, simultaneous rank confidence intervals, and MCDM aggregation with pymcdm. Addresses the same convergence of statistical inference and multi-criteria aggregation as HERA but in an NLP benchmarking context. Demonstrates that the problem HERA targets has attracted independent concurrent methodological development, reinforcing the need for explicit comparative benchmarking.

5. **Reinke A, Tizabi MD, Baumgartner M, et al. Common limitations of image processing benchmarks and how to overcome them. *Nature Methods* 20, 1285–1297 (2023). doi:10.1038/s41592-023-01910-0**  
Systematically identifies and categorizes the most prevalent design flaws in biomedical image processing benchmarks — including inappropriate aggregation, failure to account for sampling variability, and insufficient uncertainty quantification — and provides practical recommendations. Provides the empirical motivation for tools like HERA and is directly relevant to the validation gaps identified in this review.

6. **Zhang K, Zhan J, Yao Y. Stability analysis of multi-criteria decision-making techniques: A comprehensive review. *Applied Soft Computing* 153, 111279 (2024). doi:10.1016/j.asoc.2024.111279**  
A comprehensive review of stability and sensitivity analysis methods in MCDM, covering rank reversal phenomena, weight perturbation methods, and Monte Carlo approaches across TOPSIS, VIKOR, PROMETHEE, and ELECTRE. Contextualizes HERA's Borda Count sensitivity analysis within the broader MCDM stability literature and highlights open problems — including rank reversal under small candidate-set changes — that HERA does not address. Relevant for situating HERA's methodological novelty claims.

042329 Generative AI for Forecasting and Digital-Twin Simulation of Glucose Dynamics Integrating Wearable Biosensors

## 1. Overall Assessment

This manuscript presents CAMEO, a context-aware mixture-of-experts (MoE) flow-matching framework for personalised glucose forecasting and *in silico* perturbation in type 1 diabetes (T1D). The central claim is that conditioning a continuous-time normalising flow on multi-modal wearable and metabolic time-series — routed through a context-aware MoE velocity estimator — improves MAE and hypoglycaemia detection over glucose-only baselines and standard sequence architectures. The digital-twin framing, in which guided sampling under perturbed step-count inputs generates counterfactual glucose trajectories, is a secondary contribution.

The technical execution is competent and the paper is clearly written. Two concerns dominate: all experiments are confined to a single demographically homogeneous cohort (T1DEXI; 91.4% Caucasian, adults only, exercise-intervention enriched), and the digital-twin framing rests on observational associations rather than interventional validity. Together these constrain the work to a credible proof-of-concept, insufficient for the *Nature Communications* standard.

---

## 2. Strengths

The conditional flow matching backbone is a principled architectural choice. Unlike autoregressive point predictors, the continuous-time ODE (S = 50 steps) enables full predictive distributions evaluated via CRPS and calibrated 95% PI coverage — a materially stronger evaluation than MAE alone. CAMEO's achievement of nominal PI coverage while LSTM and Autoformer exhibit systematic mis-coverage is a meaningful probabilistic result.

The MoE routing and interpretability analysis are well executed. The post-hoc correspondence between wearable embedding clusters and differential expert activation — Expert 2 specialising in high step-count windows, Expert 0 in rising heart-rate patterns — provides mechanistic insight rarely reported in glucose forecasting work.

The hypoglycaemia detection analysis is clinically grounded. The 30% improvement in Level 2 sensitivity (0.63 → 0.82, p < 0.05) at comparable specificity is the paper's most clinically actionable result, given that Level 2 events demand immediate intervention.

---

## 3. Weaknesses

The absence of any external validation cohort is a fundamental flaw. All results are generated within T1DEXI — a single-site exercise-enriched study that systematically excludes paediatric patients, non-Western populations, and individuals with unstable glycaemia. Without evaluation on, for example, OhioT1DM or comparable multimodal benchmarks, all quantitative claims are cohort-specific.

The digital-twin framing is overclaimed. The heart-rate adjustment applied during step-count perturbation is derived from per-patient regressions fit to training data, creating a circular dependency that undermines counterfactual independence. The paper requires either evaluation against a held-out intervention arm or benchmarking against a mechanistic simulator (e.g., UVA/Padova) to substantiate this framing.

The COI disclosure warrants editorial scrutiny. Corresponding author G.I.A. receives professional fees from GlucoseZone, Labfront, and Calm.com, and holds a provisional patent on a lifestyle medicine digital system — all directly adjacent to this paper's commercial scope. The current disclosure is insufficient for a wearable-guided digital-twin glucose platform.

---

## 4. Editorial Decision

**Decision: Reject.** The absence of external validation and the overclaimed digital-twin framing are not addressable within a revision cycle. Resubmission to *npj Digital Medicine* or *PLOS Computational Biology* would be appropriate after external validation and a rigorous counterfactual analysis are completed. The COI situation should be resolved before resubmission anywhere.

---

## 5. Suggested Reviewer Expertise

Reviewers should collectively cover the following areas: (1) conditional flow matching and normalising flows applied to temporal data, with specific familiarity with CRPS-based evaluation and ODE-based generative models; (2) probabilistic forecasting for physiological time series, particularly CGM-based glucose prediction and uncertainty quantification; (3) mixture-of-experts architectures and context-aware routing in deep learning; (4) T1D clinical management, closed-loop insulin delivery systems, and the clinical interpretation of hypoglycaemia detection metrics; (5) causal inference and counterfactual simulation methodology in observational health data, with experience in distinguishing statistical association from interventional validity.

---

## 6. State-of-the-Art Literature Review (Past 3 Years)

The glucose forecasting landscape has matured substantially since 2022. GluFormer (*Nature*, 2025; Moshkovitz et al.) now defines the high-water mark: a generative transformer trained on 10 million CGM measurements from 10,812 individuals, with cross-cohort transfer validated across 19 external datasets, 8 CGM devices, and diverse pathophysiological states. This is the benchmark that any single-cohort forecasting system must engage with explicitly, and CAMEO does not. On the probabilistic forecasting side, TSFlow (Kollovieh et al., ICLR 2025) applies conditional flow matching with Gaussian process priors to time-series forecasting on eight real-world datasets, demonstrating competitive CRPS performance — a direct methodological precursor to CAMEO whose absence from the manuscript is notable. ProFITi (Yalavarthi et al., 2024) addresses probabilistic forecasting of irregularly sampled time series via conditional normalising flows, further competing in the same methodological space. In the T1D digital-twin domain, ReplayBG (Cappon et al., *IEEE Trans. Biomed. Eng.*, 2023) provides a mechanistic Bayesian framework for identifying personalized glucose-insulin models and simulating counterfactual therapies; a 2025 randomised trial by Kovatchev et al. (*npj Digital Medicine*, 2025) used digital-twin technology for human-machine co-adaptation in automated insulin delivery — both represent work that directly contextualises CAMEO's digital-twin claims and that the authors neither cite nor rebut.

CAMEO's genuine contribution is the integration of real-time wearable context (heart rate, step count) into a flow-based generative model via MoE routing, enabling state-dependent expert specialisation. This is a technically novel integration that no prior glucose forecasting paper has executed in this form. However, the claim that this constitutes a clinically actionable digital-twin system — as opposed to a technically interesting single-cohort demonstration — is not currently supported by the validation evidence presented.

---

## 7. Suggested Reviewer Names

**Conditional flow matching / probabilistic time-series forecasting:**
Marcel Kollovieh (Technical University of Munich), Alexander Amini (MIT), Kashif Rasul (Hugging Face), Vijaya Krishna Yalavarthi (University of Kaiserslautern)

**CGM-based glucose forecasting and wearable integration:**
Giacomo Cappon (University of Padova), Elisa Passini (University of Oxford), Reyna Jenssen (Norwegian University of Science and Technology), Martina Vettoretti (University of Padova)

**T1D clinical management and digital health:**
Boris Kovatchev (University of Virginia), Anne L. Peters (Keck School of Medicine, USC), Tadej Battelino (University Medical Centre Ljubljana)

**Causal inference in observational health data:**
Mihaela van der Schaar (University of Cambridge), Uri Shalit (Technion), Ioana Bica (University of Oxford)

---

## Further Literature

The following six papers published in the past three years share overlapping scope with this manuscript across its three core axes: multimodal wearable-guided glucose forecasting, probabilistic or generative prediction frameworks, and data-driven T1D digital-twin simulation.

**1. Zhu T et al. Multi-horizon glucose prediction across populations with deep domain generalization. *IEEE Journal of Biomedical and Health Informatics*, 2024.**
Directly addresses multi-horizon CGM forecasting (1–4 hours) with cross-population generalisability via domain generalisation — the same prediction horizons and population-transfer challenge that CAMEO targets but does not resolve. Provides a strong methodological comparator that the authors should have benchmarked against.

**2. Sergazinov R, Armandpour M, Gaynanova I. Gluformer: Transformer-based personalised glucose forecasting with uncertainty quantification. *IEEE ICASSP*, 2023.**
Models future glucose trajectories as an infinite mixture of basis distributions conditioned on CGM history, enabling probabilistic forecasting with explicit uncertainty quantification. Shares CAMEO's emphasis on predictive uncertainty and personalisation but uses a transformer backbone without wearable context; provides a direct ablation-style reference point for the value of wearable conditioning.

**3. Cappon G et al. ReplayBG: A digital twin-based methodology to identify a personalised model from type 1 diabetes data and simulate glucose concentrations to assess alternative therapies. *IEEE Transactions on Biomedical Engineering*, 2023.**
Establishes a Bayesian mechanistic digital-twin framework for T1D that identifies patient-specific glucose-insulin models and generates counterfactual therapy simulations. The most directly competing work on the digital-twin claim; unlike CAMEO, it grounds counterfactual predictions in physiologically interpretable ODE parameters, not learned statistical associations.

**4. Roquemen-Echeverri V et al. A physiologically-constrained neural network digital twin framework for replicating glucose dynamics in type 1 diabetes. *Neural Computing and Applications*, 2026 (accepted 2025).**
Uses the same T1DEXI dataset to construct physiologically-constrained neural network digital twins validated against real-world exercise scenarios. The existence of this work on identical data with an explicitly mechanistic approach makes it a critical reference that CAMEO must engage: the two papers represent competing philosophies (data-driven association vs. physiology-constrained simulation) applied to the same cohort.

**5. Lee S-M et al. Generalized multi-task learning framework for glucose forecasting and hypoglycaemia detection using simulation-to-reality. *npj Digital Medicine*, 2025.**
Jointly optimises glucose trajectory prediction and hypoglycaemia detection in a multi-task framework using simulation-to-reality transfer on OhioT1DM — a dataset CAMEO notably avoids. Directly relevant to Section 2.8 of the manuscript (hypoglycaemia detection) and demonstrates that the combined forecasting-plus-detection task has already been formulated and validated externally.

**6. Moshkovitz M et al. GluFormer: A foundation model for continuous glucose monitoring data. *Nature*, 2025.**
Trained on 10 million CGM measurements from 10,812 individuals and validated across 19 external cohorts spanning 8 CGM devices and multiple pathophysiological states. Represents the generalisability ceiling against which any single-cohort forecasting system must be situated. CAMEO's failure to engage with this work is the most consequential omission in its literature review.
