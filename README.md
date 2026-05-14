# Trackrad202512456

Here are six papers from the past three years that share the core scope of SkinGPT-X, mapped to its three defining claims: multi-agent collaboration for clinical reasoning, self-evolving/dynamic memory in medical AI, and multimodal dermatological diagnosis at scale.

---

**1. MDAgents: An Adaptive Collaboration of LLMs for Medical Decision-Making**
Kim et al., NeurIPS 2024 (oral)

MDAgents introduces a multi-agent framework that automatically assigns collaboration structures — solo, multi-disciplinary team, or integrated care team — to a group of LLMs based on assessed medical task complexity, emulating real-world clinical decision-making workflows. It achieves best performance in 7 out of 10 medical benchmarks with up to 4.2% improvement over prior methods. This is the closest architectural parallel to SkinGPT-X in the general medical AI literature. The key distinction is that MDAgents uses static LLM collaboration without any persistent or evolving memory, whereas SkinGPT-X's EvoDerma-Mem introduces closed-loop guideline synthesis — a dimension MDAgents does not address.

---

**2. SkinGPT-4: Pre-trained Multimodal Large Language Model Enhances Dermatological Diagnosis**
Zhou et al., *Nature Communications*, July 2024

SkinGPT-4 aligns a pre-trained vision transformer with Llama-2-13b-chat on 52,929 skin disease images, enabling autonomous diagnosis and treatment recommendation evaluated by board-certified dermatologists. This is SkinGPT-X's direct predecessor, sharing corresponding authorship. Its inclusion in this list is not optional — SkinGPT-X must be benchmarked against it directly, and the absence of that comparison in the manuscript is a material gap. SkinGPT-4 represents the monolithic LLM baseline that SkinGPT-X claims to supersede via its multi-agent and memory architecture.

---

**3. PanDerm: A Multimodal Vision Foundation Model for Clinical Dermatology**
Yan et al., *Nature Medicine*, 2025

PanDerm is pretrained through self-supervised learning on over 2 million real-world skin disease images from 11 clinical institutions across 4 imaging modalities, achieving state-of-the-art performance across 28 benchmarks including rare skin condition diagnosis, often outperforming existing models using only 10% of labelled data. Reader studies show PanDerm outperforms clinicians by 10.2% in early-stage melanoma detection and improved non-dermatologist providers' differential diagnosis by 16.5% across 128 conditions. PanDerm is used in SkinGPT-X as the Pre-Diagnosis Agent backbone, but the manuscript does not adequately situate SkinGPT-X's gains relative to PanDerm's standalone capabilities. Reviewers should be asked whether EvoDerma-Mem's contribution is additive to PanDerm's already exceptional few-shot performance.

---

**4. Mind the Rarities: Can Rare Skin Diseases Be Reliably Diagnosed via Diagnostic Reasoning?**
arXiv, March 2026

This work constructs a benchmark of rare skin disease cases with 10,000 chosen-rejected response pairs specifically designed to encourage multimodal reasoning rather than textual heuristics, noting that domain-specific foundation models like PanDerm achieved state-of-the-art results across 28 dermatology benchmarks while DermLIP excelled at zero-shot classification via contrastive learning. This paper directly overlaps with SkinGPT-X's RSDD claim. It constitutes a competing rare skin disease benchmark effort that the authors have not cited, and its methodological approach — preference-based fine-tuning with 10k pairs — offers a substantially more statistically robust training paradigm than RSDD's 564-sample dataset. Its existence weakens the "first benchmark for rare skin disease" claim.

---

**5. Are Multimodal LLMs Ready for Clinical Dermatology? A Real-World Evaluation**
Jiang et al., arXiv, May 2025

This study evaluates four open-weight MLLMs (including SkinGPT-4 and MedGemma-4B-Instruct) and GPT-4.1 across three public datasets and a retrospective multi-site cohort of 5,811 cases with 46,405 clinical images, finding that benchmark performance declined substantially in the real-world clinical cohort. This is the most directly contradicting paper to SkinGPT-X's clinical utility claims. It uses a far larger prospective-style evaluation than anything in SkinGPT-X's experimental design, and its findings — that benchmark-trained models do not transfer to clinical settings — must be engaged with explicitly before this manuscript can be accepted.

---

**6. MDTeamGPT: A Self-Evolving LLM-based Multi-Agent Framework for Multi-Disciplinary Team Medical Consultation**
arXiv, 2025

MDTeamGPT proposes a multi-agent MDT consultation framework using consensus aggregation and residual discussion structures, augmented by a Correct Answer Knowledge Base and Chain-of-Thought Knowledge Base that accumulate consultation experience to enable the framework to evolve and continually improve diagnostic accuracy, achieving 90.1% on MedQA and 83.9% on PubMedQA. This paper shares the self-evolving knowledge base concept most directly with SkinGPT-X's EvoDerma-Mem, but operates in a text-only, non-dermatological setting. The authors must differentiate their visual-multimodal memory evolution from MDTeamGPT's text-only accumulation mechanism and explain why the image embedding-based graph database (Equations 5–7) represents a qualitatively distinct contribution.
