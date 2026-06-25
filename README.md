# KGT-Reg: Knowledge-Guided Multimodal Framework for Medical Image Registration

[![Status](https://img.shields.io/badge/Code-Coming%20Soon-yellow.svg)](#code-release)

Official repository for **"KGT-Reg: Knowledge-Guided Multimodal Framework for Medical Image Registration"**.

> 🚧 **Code Release in Progress** — This repository will be updated in future.

---

## Overview

**KGT-Reg** is a unified multimodal framework that integrates **knowledge graph (KG) embeddings** and **textual semantics** into deep registration networks. It fuses visual features from paired medical volumes with semantic embeddings derived from organ-level textual descriptions and graph neural encodings of anatomical knowledge graphs.

<p align="center">
  <em>[ Architecture figure will be shown here ]</em>
</p>

---

## Highlights

- 🧠 **Knowledge-guided registration** — the first framework to incorporate anatomical knowledge graphs into deformable image registration, beyond purely intensity-driven or text-only guidance.
- 🔗 **Unified multi-representation fusion** — jointly leverages image intensity, localized textual semantics, and global relational topology in a single hierarchical fusion architecture.
- 📊 **Extensive validation** — evaluated on four public benchmarks spanning brain MRI and abdominal CT, with consistent improvements.
- 🧩 **Modular & generalizable** — GCFB is portable to other backbones.

---

## Datasets

[OASIS](https://brain-development.org/) (Learn2Reg 2021 Task 3)
[IXI](https://brain-development.org/ixi-dataset/)
[LPBA40](https://www.loni.usc.edu/research/atlases)
[Learn2Reg 2020 Abdomen CT](https://learn2reg.grand-challenge.org/)

---

## Results

Registration performance (Dice Similarity Coefficient, HD95, % negative Jacobian determinant) on all four benchmarks:

| Method | OASIS Dice% | IXI Dice% | LPBA40 Dice% | Abdomen CT Dice% |
|---|---|---|---|---|
| VoxelMorph | 84.7 | 72.6 | 64.2 | 38.8 |
| TransMorph | 86.2 | 74.6 | 63.7 | 40.1 |
| LKU-Net | 88.6 | 75.7 | 68.7 | 50.9 |
| KGT-Reg (ours) | 91.7 | 79.2 | 73.1 | 60.7 |

\* See the paper for full comparisons.

---

## Method Summary

Given a moving image $I_m$ and fixed image $I_f$, KGT-Reg predicts a dense deformation field $\phi$ that warps $I_m$ into alignment with $I_f$. At each decoder level $l$, the image feature map $F_l$ is fused with voxel-wise text and KG embeddings and a global graph vector $g$, via the GCFB.

---

## Citation

*(BibTeX entry will be updated upon publication.)*

---

## Acknowledgments

This work was partly supported by HHP IAF-PP (grant number H25J6a0148).

## License

License information will be added.

