# Zero-shot 與 Few-normal-shot Anomaly Detection

## Overview

WinCLIP 將 Visual Anomaly Detection 的 low-shot setting 明確分成 **zero-shot** 與 **few-normal-shot**。Zero-shot anomaly classification / segmentation 不使用 task-specific normal images；few-normal-shot 則只提供少量 normal reference images。WinCLIP 論文聚焦 K = 1–4 的 few-normal-shot setting，並在文中說明 few-shot 與 few-normal-shot 在該工作中交替使用。[Source: `raw/05_winclip.pdf`, pp.1-3]

SubspaceAD 則聚焦 practical few-shot regime：每個 category 只提供少量正常影像，並以 k ∈ {1, 2, 4} 的設定建立 normal subspace。它另外評估 batched 0-shot，但作者明確指出這與 prompt-based zero-shot 或一般 few-shot setting 不同，因為 batched 0-shot 會利用整批 test tokens 建立統計模型。[Source: `raw/06_subspacead.pdf`, pp.1, 5-7]

## Zero-shot in WinCLIP

WinCLIP 的 zero-shot setting 使用預訓練 CLIP，不需要額外 task-specific tuning。方法透過 normal / anomalous 的 compositional prompt ensemble，以及 window / patch / image-level features，進行 anomaly classification 與 segmentation。[Source: `raw/05_winclip.pdf`, pp.2-5]

## Few-normal-shot in WinCLIP+

WinCLIP+ 在 WinCLIP 的 language-guided zero-shot prediction 上，再加入少量 normal reference images。方法從不同尺度建立 normal reference memories，將 reference-based anomaly maps 與 language-guided scores 結合，用於 few-normal-shot anomaly classification / segmentation。[Source: `raw/05_winclip.pdf`, pp.5-6]

## Few-shot in SubspaceAD

SubspaceAD 不使用 prompt tuning 或 memory bank，而是從少量 normal images 抽取 frozen DINOv2-G patch features，再以 PCA 建立 normal variation subspace。Test patch 與 normal subspace 的 reconstruction residual 被用作 anomaly score。[Source: `raw/06_subspacead.pdf`, pp.1, 3-5]

## Important Distinction

本 Wiki 不將 WinCLIP 的 zero-shot、WinCLIP+ 的 few-normal-shot、SubspaceAD 的 few-shot，以及 SubspaceAD 的 batched 0-shot 視為同一種 setting。它們使用的可用資訊與推論方式不同，進行方法比較時必須保留各自 protocol。[Source: `raw/05_winclip.pdf`, pp.1-3, 6-7] [Source: `raw/06_subspacead.pdf`, pp.5-7]

## References

1. Jongheon Jeong, Yang Zou, Taewan Kim, Dongqing Zhang, Avinash Ravichandran, Onkar Dabeer. *WinCLIP: Zero-/Few-Shot Anomaly Classification and Segmentation*. CVPR 2023. Source file: `raw/05_winclip.pdf`.
2. Camile Lendering, Erkut Akdag, Egor Bondarev. *SubspaceAD: Training-Free Few-Shot Anomaly Detection via Subspace Modeling*. CVPR 2026. Source file: `raw/06_subspacead.pdf`.
