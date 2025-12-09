
# Vision Transformer 於腦部 MRI 腫瘤影像之二元分類電腦輔助診斷系統

### A. 數據 (Dataset & DataLoader)

#### 1. 資料來源
[https://drive.google.com/uc?id=18RfTvv5NBKuUgMDJjxXb7BLYz31sT_aH]


#### 2. 資料規模
總資料集：251 張。


訓練集：175 張。


驗證集：76 張

---

### B. 模型 (Model)

#### 1. 使用深度遷移學習 (Deep Transfer Learning)
使用**ViT-B/16**影像分類模型架構，使用預設參數

***這裡使用 ViT 模型是因為病灶（如腫瘤）可能出現在圖像的任何位置，比 CNN 的局部感受野更具優勢，提升了特徵表徵的能力。***


#### 2.凍結部分層（Freeze Layers）
將基礎模型參數凍結，降低小型資料集上的過度擬合風險。

---

### C. 訓練與優化 (Training)

#### 1. 損失函數
`CrossEntropyLoss`

#### 2. 優化器
Adam（預設學習率：`1e-3`）

---

### D. 模型結果與效能評估 (Evaluation)
#### #### 1. Classification Report

| Class | Precision | Recall | F1-score | Support |
|-------|-----------|--------|----------|---------|
| NO    | 1.000     | 0.857  | 0.923    | 35      |
| YES   | 0.891     | 1.000  | 0.943    | 41      |

**Accuracy:** 0.934 (76 samples)

敏感度 (Recall/TPR):1.000 (成功找出所有腫瘤病患，漏診率為 0。)

精確率 (Precision) : 0.891 (預測有腫瘤的結果中有 $89.1\%$ 是正確的，誤報率低。)

#### 2. 混淆矩陣 (Confusion Matrix)
[[30  5]

 [ 0 41]]

*假陰性 (FN) = 0：模型未漏診任何腫瘤病患（敏感度 100%）。*

*假陽性 (FP) = 5：僅有 5 個無腫瘤的病患被誤報為有腫瘤（誤報率低）。*
 
 [confusion_matrix](./image/腫瘤混淆矩陣.png)


#### 3.ROC Curve
[ROC Curve](./image/ROC-cruve.png)

#### 4.AUC :0.9679

#### 5.Youden index: 0.7124 (在驗證集上，同時最大化敏感度 (TPR) 與特異度 (Specificity) 時所找到的最佳分類決策點)

