# SPot-the-Difference (SPD)

## Overview

SPot-the-Difference (SPD) 是 VisA 論文提出的 self-supervised pre-training regularization，目標是讓 representation 對 anomaly detection 所需的 local details 更敏感。作者認為 standard contrastive self-supervised learning 常著重 global semantic differences，而 surface anomaly detection 需要辨識 scratches、cracks 等局部且細微的變化。[Source: `raw/02_visa.pdf`, pp.2-4]

## Core Idea

SPD 以「找出局部差異」作為訓練訊號。它將加入局部 perturbation 的影像當作 SPD negative，而只加入 weak global transformations 的影像作為 SPD positive；訓練目標是拉開 anchor 與 local-changed negative 的 representation，同時維持 anchor 與 weak-global-changed positive 的相似性。[Source: `raw/02_visa.pdf`, pp.3, 6-8]

## Input

輸入為用於 pre-training 的影像。SPD 可以搭配既有的 self-supervised contrastive learning 方法，例如 SimCLR、MoCo 與 SimSiam；論文也描述如何將 SPD 用於 supervised pre-training。[Source: `raw/02_visa.pdf`, pp.1, 7-8]

## Feature Representation

shared encoder `f(·)` 對 anchor、SPD positive 與 SPD negative 提取 representations，再經 projection head `g(·)` 得到用於 SPD loss 的 feature projections。[Source: `raw/02_visa.pdf`, p.7]

## Augmentation

論文提出 **SmoothBlend** 產生局部 perturbation，作為 synthetic spot-the-difference。SPD 同時加入 weak global augmentation，以模擬 lighting、object position 等較小的 global variations。[Source: `raw/02_visa.pdf`, pp.6-7]

## Normality Modeling

本論文沒有將 SPD 本身定義成獨立的 normality modeling algorithm。SPD 的角色是改善 pre-trained representation，再交給 downstream anomaly detection / segmentation method 使用。因此本頁不額外補入 normality modeling 機制。[Source: `raw/02_visa.pdf`, pp.1-3, 7-8]

## Anomaly Scoring

SPD 本身的訓練章節沒有定義一個通用 anomaly score；論文將 SPD pre-trained representation 搭配 downstream anomaly detection methods 進行實驗。因此不在此頁自行推導 anomaly scoring 規則。[Source: `raw/02_visa.pdf`, pp.1-3, 8-14]

## Experimental Setting

論文在 VisA 與 MVTec AD 上測試 SPD 對多種 pre-training baseline 的影響，並使用 1-class、2-class high-shot，以及 5/10-shot 等不同設定。主要評估同時包含 anomaly classification 與 segmentation。[Source: `raw/02_visa.pdf`, pp.9-14]

## Strengths Reported by the Paper

作者報告 SPD 可作為 regularization 加到多種 self-supervised 或 supervised pre-training 方法，並在多個 VisA / MVTec AD downstream experiments 中提升 anomaly detection 或 segmentation 表現。[Source: `raw/02_visa.pdf`, pp.1, 11-14]

## Limitations

原論文未在主要本文中建立獨立的 limitations section。本次 ingest 不額外推論作者未明確提出的限制。

## Related Methods

- SimCLR
- MoCo
- SimSiam
- PaDiM
- PatchCore

以上方法名稱均出現在本論文的背景或實驗中；本批次尚未對它們建立完整 method pages。[Source: `raw/02_visa.pdf`, pp.1-4, 10-14]

## References

1. Yang Zou, Jongheon Jeong, Latha Pemula, Dongqing Zhang, Onkar Dabeer. *SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation*. 2022. Source file: `raw/02_visa.pdf`.
