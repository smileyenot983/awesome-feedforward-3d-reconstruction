# Awesome Feed-Forward 3D Reconstruction

A curated paper list of feed-forward 3D reconstruction methods, with concise key-idea summaries for each paper.
The goal is not to be fully comprehensive, but to make it easier to understand how the field evolved from DUSt3R-style pairwise reconstruction to multi-view, streaming, prior-guided, non-pinhole, dynamic, and 3DGS-based methods.

This list is **not exhaustive**. It focuses on papers that are useful for understanding the recent DUSt3R-style feed-forward 3D reconstruction family.

_Last checked: 2026-07-02._

## Contents

- [Base methods](#base-methods)
- [Online / streaming-based multi-view methods](#online--streaming-based-multi-view-methods)
- [Global multi-view methods](#global-multi-view-methods)
- [Methods using priors](#methods-using-priors)
- [Non-pinhole / camera-agnostic methods](#non-pinhole--camera-agnostic-methods)
- [Dynamic / 4D reconstruction](#dynamic--4d-reconstruction)
- [Feed-forward 3D Gaussian Splatting](#feed-forward-3d-gaussian-splatting)
- [Contributing](#contributing)

## Base methods

| Model | Date | Key idea | Paper / Project | Code |
|---|---:|---|---|---|
| **DUSt3R: Geometric 3D Vision Made Easy** | 2023-12 | Directly regresses 3D pointmaps from unposed, uncalibrated image pairs. For multiple images, it aligns pairwise predictions into a common 3D space, replacing much of the fragile feature matching / triangulation / SfM pipeline. | [arXiv](https://arxiv.org/abs/2312.14132) | [GitHub](https://github.com/naver/dust3r) |
| **MASt3R: Grounding Image Matching in 3D** | 2024-06 | Extends DUSt3R with a dense local-feature head for image matching and a fast reciprocal matching scheme, improving matching while preserving robust 3D reasoning. | [arXiv](https://arxiv.org/abs/2406.09756) / [Project](https://europe.naverlabs.com/blog/mast3r-matching-and-stereo-3d-reconstruction/) | [GitHub](https://github.com/naver/mast3r) |

## Online / streaming-based multi-view methods

| Model | Date | Key idea | Paper / Project | Code |
|---|---:|---|---|---|
| **Spann3R: 3D Reconstruction with Spatial Memory** | 2024-08 | Adds an external spatial memory so images can be processed incrementally while predicting pointmaps in a common global coordinate system, avoiding per-scene optimization-based global alignment. | [arXiv](https://arxiv.org/abs/2408.16061) / [Project](https://hengyiwang.github.io/projects/spanner) | [GitHub](https://github.com/HengyiWang/spann3r) |
| **CUT3R: Continuous 3D Perception Model with Persistent State** | 2025-01 | Uses a recurrent persistent state that updates as new observations arrive and outputs metric-scale pointmaps in a common coordinate system for online reconstruction. | [arXiv](https://arxiv.org/abs/2501.12387) / [Project](https://cut3r.github.io/) | [GitHub](https://github.com/CUT3R/CUT3R) |
| **MUSt3R: Multi-view Network for Stereo 3D Reconstruction** | 2025-03 | Extends DUSt3R from image pairs to multi-view prediction with a memory mechanism, enabling offline and online reconstruction without global alignment. | [arXiv](https://arxiv.org/abs/2503.01661) | [GitHub](https://github.com/naver/must3r) |

## Global multi-view methods

| Model | Date | Key idea | Paper / Project | Code |
|---|---:|---|---|---|
| **Fast3R: Towards 3D Reconstruction of 1000+ Images in One Forward Pass** | 2025-01 | Processes many views jointly in a single Transformer forward pass, bypassing iterative pairwise alignment and scaling to very large image collections. | [arXiv](https://arxiv.org/abs/2501.13928) / [Project](https://fast3r-3d.github.io/) | [GitHub](https://github.com/facebookresearch/fast3r) |
| **FLARE: Feed-forward Geometry, Appearance and Camera Estimation from Uncalibrated Sparse Views** | 2025-02 | Uses a cascaded pipeline: first estimate camera poses, then condition geometry and appearance prediction on those poses. Also targets sparse-view reconstruction and novel-view synthesis. | [arXiv](https://arxiv.org/abs/2502.12138) / [Project](https://zhanghe3z.github.io/FLARE/) | [GitHub](https://github.com/ant-research/FLARE) |
| **VGGT: Visual Geometry Grounded Transformer** | 2025-03 | A unified feed-forward model that predicts camera parameters, point maps, depth maps, and 3D point tracks from one, few, or many views. | [arXiv](https://arxiv.org/abs/2503.11651) | [GitHub](https://github.com/facebookresearch/vggt) |
| **Dens3R: A Foundation Model for 3D Geometry Prediction** | 2025-07 | Jointly predicts multiple geometric quantities, such as pointmaps, depth, and surface normals. Uses position-interpolated RoPE to improve robustness to unseen resolutions. | [arXiv](https://arxiv.org/abs/2507.16290) / [Project](https://g-1nonly.github.io/Dens3R/) | [GitHub](https://github.com/G-1nOnly/Dens3R) |
| **π³: Permutation-Equivariant Visual Geometry Learning** | 2025-07 | Removes dependence on a fixed reference view by predicting local pointmaps and relative / affine-invariant camera poses in a permutation-equivariant way. | [arXiv](https://arxiv.org/abs/2507.13347) / [Project](https://yyfz.github.io/pi3/) | [GitHub](https://github.com/yyfz/Pi3) |
| **Depth Anything 3: Recovering the Visual Space from Any Views** | 2025-11 | A minimal feed-forward geometry model using a plain Transformer backbone and a depth-ray representation, optionally using known camera poses. | [arXiv](https://arxiv.org/abs/2511.10647) / [Project](https://depth-anything-3.github.io/) | [GitHub](https://github.com/ByteDance-Seed/depth-anything-3) |

## Methods using priors

These methods accept extra geometric information, such as camera intrinsics, poses, sparse/dense depth, or partial reconstructions.

| Model | Date | Key idea | Paper / Project | Code |
|---|---:|---|---|---|
| **Pow3R: Empowering Unconstrained 3D Reconstruction with Camera and Scene Priors** | 2025-03 | Extends the DUSt3R-style paradigm with optional priors such as intrinsics, relative pose, dense depth, or sparse depth. | [arXiv](https://arxiv.org/abs/2503.17316) / [Project](https://europe.naverlabs.com/pow3r) | [GitHub](https://github.com/naver/pow3r) |
| **G-CUT3R: Guided 3D Reconstruction with Camera and Depth Prior Integration** | 2025-08 | Adds modality-specific encoders and zero-convolution fusion to CUT3R so it can use camera intrinsics, poses, and depth priors during inference. | [arXiv](https://arxiv.org/abs/2508.11379) | Not open |
| **MapAnything: Universal Feed-Forward Metric 3D Reconstruction** | 2025-09 | A unified feed-forward model for metric 3D reconstruction that can ingest images plus optional intrinsics, poses, depth, or partial reconstruction inputs. | [arXiv](https://arxiv.org/abs/2509.13414) / [Project](https://map-anything.github.io/) | [GitHub](https://github.com/facebookresearch/map-anything) |

## Non-pinhole / camera-agnostic methods

| Model | Date | Key idea | Paper / Project | Code |
|---|---:|---|---|---|
| **UniK3D: Universal Camera Monocular 3D Estimation** | 2025-03 | Predicts metric 3D from a single image under arbitrary camera models using a spherical representation and learned ray directions. | [arXiv](https://arxiv.org/abs/2503.16591) / [Project](https://lpiccinelli-eth.github.io/pub/unik3d/) | [GitHub](https://github.com/lpiccinelli-eth/unik3d) |
| **Wid3R: Wide Field-of-View 3D Reconstruction via Camera Model Conditioning** | 2026-02 | Multi-view feed-forward 3D reconstruction for fisheye / panoramic / wide-FOV imagery using ray representations and a learned camera-model token. | [arXiv](https://arxiv.org/abs/2602.05321) | Not open |
| **CAM3R: Camera-Agnostic Model for 3D Reconstruction** | 2026-03 | Two-view camera-agnostic reconstruction that decouples ray-direction estimation from cross-view geometry and pose prediction for wide-angle cameras. | [arXiv](https://arxiv.org/abs/2603.22631) | Not open |

## Dynamic / 4D reconstruction

| Model | Date | Key idea | Paper / Project | Code |
|---|---:|---|---|---|
| **MonST3R: A Simple Approach for Estimating Geometry in the Presence of Motion** | 2024-10 | Adapts DUSt3R-style pointmap prediction to dynamic scenes and adds video-specific optimization terms such as trajectory smoothness and flow alignment. | [arXiv](https://arxiv.org/abs/2410.03825) / [Project](https://monst3r-project.github.io/) | [GitHub](https://github.com/Junyi42/monst3r) |
| **D4RT: Efficiently Reconstructing Dynamic Scenes One D4RT at a Time** | 2025-12 | Encodes a full video once and uses a query-based decoder to recover depth, correspondence, camera parameters, and 3D point positions across space-time. | [arXiv](https://arxiv.org/abs/2512.08924) / [Project](https://d4rt-paper.github.io/) | [Community code](https://github.com/Lijiaxin0111/Open-d4rt) |

## Feed-forward 3D Gaussian Splatting

| Model | Date | Key idea | Paper / Project | Code |
|---|---:|---|---|---|
| **Splatt3R: Zero-shot Gaussian Splatting from Uncalibrated Image Pairs** | 2024-08 | Extends MASt3R with Gaussian attributes to predict 3D Gaussian Splats from uncalibrated stereo pairs. | [arXiv](https://arxiv.org/abs/2408.13912) / [Project](https://splatt3r.active.vision/) | [GitHub](https://github.com/btsmart/splatt3r) |
| **NoPoSplat: No Pose, No Problem — Surprisingly Simple 3D Gaussian Splats from Sparse Unposed Images** | 2024-10 | Predicts 3D Gaussians from sparse unposed images in a canonical coordinate system, trained with photometric loss rather than ground-truth point clouds. | [arXiv](https://arxiv.org/abs/2410.24207) / [Project](https://noposplat.github.io/) | [GitHub](https://github.com/cvg/NoPoSplat) |

## Contributing

Contributions are welcome. Good additions usually include:

- Paper title
- Month/year
- One-sentence core idea
- Paper/project link
- Code link, if available
- Category suggestion

Please open an issue or pull request if a paper is missing, a link is broken, or a summary is inaccurate.

## Related lists

- [Awesome Feed-Forward 3D](https://github.com/ziplab/Awesome-Feed-Forward-3D)
- [Awesome DUSt3R Resources](https://github.com/ruili3/awesome-dust3r)
- [End-to-End 3D Reconstruction Paper List](https://github.com/chicleee/End-to-End-3D-Reconstruction-Paper-List)

