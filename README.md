# LIMU-BERT 重現實驗

## 執行環境
- Google Colab
- Tesla T4 GPU
- Python 3.12
- PyTorch

## 論文資訊
### LIMU-BERT: Unleashing the Potential of Unlabeled Data for IMU Sensing Applications

論文連結：  
https://arxiv.org/abs/2106.08265

官方 GitHub：  
https://github.com/dapowan/LIMU-BERT-Public

## 資料集
- UCI HAR Dataset
- Version: 20_120

本專案使用 UCI Human Activity Recognition（HAR）資料集進行論文重現實驗。

## 重現流程

### 1. Clone 專案

    git clone https://github.com/dapowan/LIMU-BERT-Public.git
    cd LIMU-BERT-Public

### 2. 安裝需求套件

    pip install -r requirements.txt

### 3. 確認 GPU

    import torch
    
    print(torch.cuda.is_available())
    print(torch.cuda.get_device_name(0))

預期輸出：

    True
    Tesla T4

## 訓練流程

### Step 1 — 預訓練（Pretraining）

    python pretrain.py v1 uci 20_120 -s limu_v1_fast

此步驟進行 LIMU-BERT 的 self-supervised 預訓練。

### Step 2 — 產生 Embedding

    python embedding.py v1 uci 20_120 -f limu_v1_fast

此步驟利用預訓練模型產生特徵 embedding。

### Step 3 — 訓練分類器

    python classifier.py v2 uci 20_120 -f limu_v1_fast -s limu_gru_v1_fast -l 0

此步驟進行 HAR 下游分類任務訓練。

## 重現結果

### Best Accuracy
- 0.833 / 0.822 / 0.733

### Best F1-score
- 0.796 / 0.782 / 0.715

## 差距分析與討論

本次重現結果低於原論文結果，可能原因如下：

- 預訓練 epoch 數量降低（100 而非原論文 3200）
- GPU 環境不同
- 前處理設定不同
- random seed 差異
- Google Colab 訓練時間限制
- 套件版本差異

此外，原論文中部分超參數設定可能未完整公開，也可能影響最終重現結果。

## 改善方向

未來可嘗試以下方向改善模型表現：

- 增加 pretraining epochs
- 使用更大型資料集進行 self-supervised learning
- 加入 data augmentation
- 調整 learning rate 與 batch size
- 使用更高效能 GPU
- 測試更多 HAR 資料集

## 跨資料集討論

模型在不同 HAR 資料集上的表現可能下降，原因包含：

- 感測器配戴位置不同
- 活動分布不同
- 動作模式差異
- 存在 domain shift 問題

此結果顯示 cross-domain generalization 在 HAR 研究中具有重要性。

## 心得

本次實驗讓我更了解：

- Self-supervised learning
- Transformer 在 IMU sensing 的應用
- HAR 任務中的 representation learning
- 深度學習論文重現流程
- Neural Network 研究中的 reproducibility 重要性

同時也了解到不同訓練設定會明顯影響模型最終結果。

## 檔案說明

- pretrain.py → self-supervised 預訓練
- embedding.py → embedding 產生
- classifier.py → 下游分類器訓練
- training_result.png → 重現結果截圖
- LIMU_BERT_Reproduction.ipynb → Colab Notebook
- 
