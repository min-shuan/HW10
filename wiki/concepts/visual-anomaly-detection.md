# Visual Anomaly Detection 基本概念

## Overview

Visual Anomaly Detection 的核心任務，是在影像中辨識與正常資料不同的異常樣本，並在需要時定位異常區域。MVTec AD 將工業檢測視為適合的 unsupervised anomaly detection 場景：訓練資料主要由 defect-free 影像構成，而測試資料則包含 defect-free 與 defective 影像。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2]

VisA 將 visual surface anomaly detection 與 segmentation 描述為工業製造中用來辨識與定位缺陷的任務，並指出實務上的幾項困難，包括缺陷樣本稀少、缺陷常只佔很小區域、製造場域對準確度要求高，以及不同產品與檢測任務差異很大。[Source: `raw/02_visa.pdf`, pp.1-2]

## Image-level Detection

Image-level detection 關心的是整張影像是否包含 anomaly。MVTec AD 的設計同時支援 anomaly-free 與 anomalous test images，因此可評估 image-level classification；VisA 也提供 image-level labels，並針對不同 training setup 建立 anomaly classification protocol。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2, 6] [Source: `raw/02_visa.pdf`, pp.8-10]

## Pixel-level Localization / Segmentation

Pixel-level localization / segmentation 關心 anomaly 出現在影像中的哪個位置。MVTec AD 對所有異常提供 pixel-precise ground truth regions，使方法能評估 anomalous region segmentation；VisA 同樣提供 pixel-level annotations。[Source: `raw/01_mvtec-ad.pdf`, pp.1-2] [Source: `raw/02_visa.pdf`, pp.8-9]

## Why Normal-only Training Matters

MVTec AD 指出工業製程通常會盡量降低 defective samples 的數量，因此相較於大量 defect-free samples，實際可取得的 defect images 往往有限。這使只利用正常樣本學習的 unsupervised / one-class setting 具有實際意義。[Source: `raw/01_mvtec-ad.pdf`, p.2]

VisA 也指出 anomalous data 稀少是 surface anomaly detection 的重要挑戰，並說明過去研究因此多集中於只需要 normal images 的 1-class anomaly detection；同時，若成熟製程中已能取得 anomaly samples，也可考慮 2-class setting。[Source: `raw/02_visa.pdf`, pp.1-3]

## References

1. Paul Bergmann, Michael Fauser, David Sattlegger, Carsten Steger. *MVTec AD — A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection*. 2019. Source file: `raw/01_mvtec-ad.pdf`.
2. Yang Zou, Jongheon Jeong, Latha Pemula, Dongqing Zhang, Onkar Dabeer. *SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation*. 2022. Source file: `raw/02_visa.pdf`.
