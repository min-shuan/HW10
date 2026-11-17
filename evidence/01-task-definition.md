# Evidence Card 01 — Task Definition

## Teaching Topic
Visual Anomaly Detection 是什麼？

## Claim
Visual Anomaly Detection 的任務是在影像中辨識與正常資料不同的異常樣本，並在需要時定位異常區域；工業場景中常見 normal-only / defect-scarce 設定。

## Explanation
MVTec AD 將工業檢測建構成 defect-free training data 搭配 normal / defective test data 的 unsupervised anomaly detection benchmark；VisA 也將 anomaly classification 與 segmentation 作為核心任務。

## Wiki Entry
- `wiki/concepts/visual-anomaly-detection.md`
- `wiki/datasets/mvtec-ad.md`
- `wiki/datasets/visa.md`

## Original Source
- `raw/01_mvtec-ad.pdf`
- `raw/02_visa.pdf`

## Important Numbers
無必要數字。

## Allowed Usage
可用於簡報開頭定義任務、說明 image-level detection 與 pixel-level localization。

## Do Not Claim
不要在沒有額外來源時延伸成「Visual Anomaly Detection 與一般 image classification 的完整理論差異」。
