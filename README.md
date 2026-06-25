# KGT-Reg: Knowledge-Guided Multimodal Framework for Medical Image Registration

[![MICCAI 2026](https://img.shields.io/badge/MICCAI-2026-blue.svg)](https://conferences.miccai.org/2026/en/)
[![Paper](https://img.shields.io/badge/Paper-PDF-red.svg)](#citation)
[![Status](https://img.shields.io/badge/Code-Coming%20Soon-yellow.svg)](#code-release)

Official repository for **"KGT-Reg: Knowledge-Guided Multimodal Framework for Medical Image Registration"**, accepted at **MICCAI 2026**.

> 🚧 **Code Release in Progress** — We are currently cleaning up and organizing the codebase for public release. This repository will be updated with the full training/inference code, pretrained weights, and configuration files soon. ⭐ Star/Watch this repo to get notified!

---

## Authors

**Yuhe Dai**¹˙²˙³, **Zhiyong Huang**¹˙², **Xiaohong Wang**³, **Weimin Huang**³*

¹ School of Computing, National University of Singapore, Singapore
² NUS Chongqing Research Institute, China
³ Institute of Advanced Intelligence and Computing (IAIC), Agency for Science, Technology and Research (A\*STAR), Singapore

*Corresponding author: wmhuang@a-star.edu.sg

---

## Overview

Deformable medical image registration (DIR) benefits from both pixel-level correspondence modelling and high-level semantic understanding of anatomical structures. However, most learning-based registration methods remain purely data-driven and fail to leverage rich domain knowledge describing anatomical structures and inter-organ relations.

**KGT-Reg** is a unified multimodal framework that integrates **knowledge graph (KG) embeddings** and **textual semantics** into deep registration networks. It fuses visual features from paired medical volumes with semantic embeddings derived from organ-level textual descriptions and graph neural encodings of anatomical knowledge graphs — to our knowledge, the **first attempt to use KG-encoded relational priors to condition deformation-field decoding** in DIR.

<p align="center">
  <em>[ Architecture figure — Fig. 1 of the paper — will be added here ]</em>
</p>

### Key Components

- **LK U-Net backbone** — a large-kernel convolutional encoder–decoder for multi-scale spatial feature extraction.
- **Text encoder** — a frozen CLIP text encoder that produces semantic embeddings for anatomical structures from natural-language prompts (e.g., *"Magnetic Resonance Imaging (MRI) of the [i] region of the brain."*).
- **Knowledge Graph (KG) encoder** — a dataset-level static anatomical KG, built from training-set segmentation masks (organ adjacency + spatial topology), encoded via a 2-layer Graph Attention Network (GAT).
- **Graph-Conditioned Fusion Block (GCFB)** — fuses image, text, and KG features at multiple decoder levels via FiLM-based modulation, allowing semantic and relational cues to dynamically condition the deformation field decoding.

---

## Highlights

- 🧠 **Knowledge-guided registration** — the first framework to incorporate anatomical knowledge graphs into deformable image registration, beyond purely intensity-driven or text-only guidance.
- 🔗 **Unified multi-representation fusion** — jointly leverages image intensity, localized textual semantics, and global relational topology in a single hierarchical fusion architecture.
- 📊 **Extensive validation** — evaluated on **four public benchmarks** spanning brain MRI and abdominal CT, with consistent improvements over classical, CNN-, Transformer-, and text-guided baselines.
- 🧩 **Modular & generalizable** — GCFB is portable to other backbones (validated on DMR), and the framework supports both NCC/MSE similarity objectives.

---

## Datasets

| Dataset | Modality | # Scans | # Structures | Resolution |
|---|---|---|---|---|
| [OASIS](https://brain-development.org/) (Learn2Reg 2021 Task 3) | Brain MRI (T1) | 414 | 35 | 160×192×224 |
| [IXI](https://brain-development.org/ixi-dataset/) | Brain MRI (T1) | 576 | 38 | 160×192×224 |
| [LPBA40](https://www.loni.usc.edu/research/atlases) | Brain MRI (T1) | 40 | 56 | 160×192×160 |
| [Learn2Reg 2020 Abdomen CT](https://learn2reg.grand-challenge.org/) | Abdominal CT | 30 | 13 | 192×160×256 (2mm iso) |

Missing segmentation labels for brain MRI were generated via [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/) and the [Neurite](https://github.com/adalca/neurite) package.

---

## Results

Registration performance (Dice Similarity Coefficient, HD95, % negative Jacobian determinant) on all four benchmarks:

| Method | OASIS Dice% | IXI Dice% | LPBA40 Dice% | Abdomen CT Dice% |
|---|---|---|---|---|
| VoxelMorph | 84.7 | 72.6 | 64.2 | 38.8 |
| TransMorph | 86.2 | 74.6 | 63.7 | 40.1 |
| LKU-Net | 88.6 | 75.7 | 68.7 | 50.9 |
| TextSCF | 90.1 | / | / | 60.8 |
| **KGT-Reg (ours)** | **91.7** | **79.2** | 73.1 | **60.7*** |

\* second-best on Abdomen CT. See the paper for full comparisons (incl. HD95, Jacobian regularity, and ablation studies on text-prompt design, GCFB placement, backbone portability, and the contribution of each component).

---

## Method Summary

Given a moving image $I_m$ and fixed image $I_f$, KGT-Reg predicts a dense deformation field $\phi$ that warps $I_m$ into alignment with $I_f$. At each decoder level $l$, the image feature map $F_l$ is fused with voxel-wise text and KG embeddings (retrieved according to segmentation labels) and a global graph vector $g$, via the GCFB:

$$F_l' = \gamma_l \odot F_l + \beta_l$$

where $(\gamma_l, \beta_l)$ are FiLM modulation parameters predicted from the concatenated text/KG/global conditioning vector. The network is trained with a combination of similarity loss (NCC/MSE), an auxiliary Dice loss on segmentation overlap, and a smoothness regularizer on the deformation field.

---

## Code Release

The codebase is being prepared for public release and will include:

- [ ] Data preprocessing scripts (segmentation, KG construction, text-prompt generation)
- [ ] Model implementation (LK backbone, CLIP text encoder integration, GAT-based KG encoder, GCFB)
- [ ] Training & inference scripts
- [ ] Pretrained checkpoints
- [ ] Evaluation scripts (Dice, HD95, Jacobian determinant)

**ETA:** to be announced — please check back or watch this repository for updates.

---

## Citation

If you find this work useful, please consider citing:

```bibtex
@inproceedings{dai2026kgtreg,
  title     = {KGT-Reg: Knowledge-Guided Multimodal Framework for Medical Image Registration},
  author    = {Dai, Yuhe and Huang, Zhiyong and Wang, Xiaohong and Huang, Weimin},
  booktitle = {Medical Image Computing and Computer Assisted Intervention (MICCAI)},
  year      = {2026}
}
```

*(BibTeX entry will be updated with final volume/page numbers upon publication.)*

---

## Acknowledgments

This work was partly supported by HHP IAF-PP (grant number H25J6a0148).

## License

License information will be added upon code release.

## Contact

For questions about the paper, please contact: **wmhuang@a-star.edu.sg**
