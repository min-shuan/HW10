# Evidence Card 02 — Datasets

## Teaching Topic
MVTec AD 與 VisA

## Claim
MVTec AD 與 VisA 都支援 industrial anomaly detection / segmentation，但資料規模與場景複雜度不同。

## Explanation
MVTec AD 包含 5,354 張影像、15 個 categories、73 種 defect types，異常影像提供 pixel-precise ground truth。VisA 包含 10,821 張影像、12 個 objects、3 個 domains，並提供 image-level 與 pixel-level annotations；VisA 論文強調其 complex structures、multiple instances 與 location variation。

## Wiki Entry
- `wiki/datasets/mvtec-ad.md`
- `wiki/datasets/visa.md`

## Original Source
- `raw/01_mvtec-ad.pdf`
- `raw/02_visa.pdf`

## Important Numbers
- MVTec AD: 5,354 images, 15 categories, 73 defect types
- VisA: 10,821 images, 12 objects, 3 domains

## Allowed Usage
可做 dataset comparison 與 benchmark introduction。

## Do Not Claim
MVTec AD 與 VisA 的「難度高低」不可直接下結論；只能引用 VisA 論文對結構複雜度與場景差異的描述。
