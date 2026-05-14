# Trackrad202512456

Here are six papers from the past three years that share substantial scope with *Depth-Retina*, organized by proximity of contribution:

---

**1. Zhang J. et al. — "Polar Eyeball Shape Net for 3D Posterior Ocular Shape Representation." MICCAI 2023.**
The most direct technical comparator. PESNet reconstructs complete 3D posterior eye shape from small-FOV OCT using a dual-branch architecture with a Polar Voxelization Block (PVB) for sparse-to-dense conversion and a Radius-wise Fusion Block (RFB). It shares *Depth-Retina*'s goal of full-field 3D PES reconstruction but remains confined to OCT inputs and limited posterior coverage. *Depth-Retina* is distinguished by operating from CFP alone and achieving metric calibration over a 20 × 20 mm field.

**2. Han Y.X. et al. — "Automated Posterior Scleral Topography Assessment for Enhanced Staphyloma Visualization and Quantification with Improved Maculopathy Correlation." *Translational Vision Science & Technology*, 2024.**
Constructs posterior scleral topography automatically from MRI using deep learning surface extraction, computes curvature-distance parameters (C·D_max, D_var), and demonstrates correlation with myopic traction maculopathy grades via the ATN classification. This paper shares *Depth-Retina*'s ambition of deriving quantitative 3D PES descriptors for clinical phenotyping, but relies on MRI rather than fundus photography and is validated in only 102 eyes from a single center — the scalability gap that *Depth-Retina* explicitly addresses.

**3. Zhou Y. et al. — "A Foundation Model for Generalizable Disease Detection from Retinal Images." *Nature*, 2023.**
RETFound, trained by self-supervised masked autoencoding on 1.6 million unlabelled CFPs and OCT B-scans (ViT-L backbone), establishes a new baseline for CFP-based disease detection and prognostication across glaucoma, diabetic retinopathy, AMD, and systemic disease. It is directly relevant because *Depth-Retina* claims to add clinical value for exactly these conditions via a PES intermediary, yet never benchmarks against RETFound-adapted classifiers on the same cohorts. This omission is a material weakness in the downstream validation.

**4. Yii F. et al. — "Can Fundus Features Tell Us Something About 3D Eye Shape?" *Ophthalmic & Physiological Optics*, 2025.**
A UK Biobank study (99 eyes, MRI-derived posterior shape) demonstrating that optic disc orientation, optic disc-fovea angle, and central retinal arteriolar equivalent (CRAE) associate with posterior eye asphericity beyond spherical equivalent. This provides statistical validation for *Depth-Retina*'s core assumption that CFPs encode 3D PES information, but the sample is too small and the approach too indirect to constitute reconstruction. It serves as concurrent conceptual support rather than a competing method.

**5. Wang Y. et al. — "Development of Deep Learning Models to Screen Posterior Staphylomas in Highly Myopic Eyes Using UWF-OCT Images." *Translational Vision Science & Technology*, 2025.**
Trains seven CNN architectures (VGG, ResNet, DenseNet variants) on 1,428 UWF-OCT images to detect posterior staphyloma edges in highly myopic eyes. It shares *Depth-Retina*'s clinical target (high myopia, posterior deformation, UWF imaging) and institutional affiliation (Ohno-Matsui group), but frames the task as binary staphyloma screening rather than continuous 3D surface reconstruction. The performance ceiling of edge-detection approaches compared to full metric PES quantification is a gap this paper does not bridge.

**6. Yang L. et al. — "Depth Anything V2." NeurIPS 2024.**
The strongest general-scene MDE foundation model in the current landscape, trained on synthetic ground truth with a scale-up teacher-student pseudo-labeling framework, achieving substantially finer and more robust relative depth than V1. It is directly relevant because *Depth-Retina* initializes from Depth Anything V1 weights and frames its contribution partly as a domain-specific adaptation beyond general MDE. The paper's failure to include Depth Anything V2 as a fine-tuning baseline (only V1 is used) is a notable gap; the performance delta claimed against fine-tuned ZoeDepth would need to be reproduced against a V2-initialized comparator to fully substantiate the architectural contribution claim.

Based strictly on what the manuscript reports, three things materially differentiate *Depth-Retina* from the prior works listed:

**Modality.** Every comparator that attempts 3D PES reconstruction (PESNet, Han et al., Wang et al.) requires OCT or MRI as input. *Depth-Retina* is the only method that produces metrically calibrated, full-field 3D PES from a CFP alone — a modality available in virtually every eye clinic globally. This is the single most defensible novelty claim.

**Scale calibration.** General MDE foundation models (Depth Anything V2, ZoeDepth) produce relative depth — scale-ambiguous outputs that cannot be compared across patients or time points. *Depth-Retina* outputs physically calibrated depth in micrometers over a 20 × 20 mm posterior pole. That metric fidelity is what enables the downstream clinical comparisons against axial length and refractive error, which are themselves absolute measures. Without it, the clinical validation section collapses entirely.

**Downstream clinical linkage.** Prior works stop at geometric reconstruction or binary disease classification. *Depth-Retina* connects the reconstructed PES to a prospective 10-year clinical outcome (incident PM prediction, AUC 0.90) in a population-based longitudinal cohort. No prior method has demonstrated that fundus-derived posterior shape predicts a hard clinical endpoint at that time horizon.

**The counterargument you should anticipate:** RETFound (Zhou et al., *Nature* 2023), operating directly on CFPs without any geometric intermediary, achieves competitive disease detection across the same conditions *Depth-Retina* targets — and does so without the complexity of a 3D reconstruction pipeline. The manuscript never directly tests whether PES adds discriminative value *over and above* what RETFound extracts from the same CFP. Until that experiment is done, the claim that the geometric representation is doing the clinical work — rather than the fundus appearance features learned during ViT pretraining — remains unproven.
