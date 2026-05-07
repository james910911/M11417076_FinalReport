# LIMU-BERT Reproduction

## Environment

* Google Colab
* Tesla T4 GPU
* PyTorch
* Python 3.12

---

## Paper

LIMU-BERT: Unleashing the Potential of Unlabeled Data for IMU Sensing Applications

Paper URL:
https://arxiv.org/abs/2106.08265

Official GitHub:
https://github.com/dapowan/LIMU-BERT-Public

---

## Dataset

* UCI HAR Dataset
* Version: 20_120

---

## Reproduction Process

### 1. Pretraining

python pretrain.py v1 uci 20_120 -s limu_v1_fast

### 2. Generate Embedding

python embedding.py v1 uci 20_120 -f limu_v1_fast

### 3. Train Classifier

python classifier.py v2 uci 20_120 -f limu_v1_fast -s limu_gru_v1_fast -l 0

---

## Result

Best Accuracy:
0.833 / 0.822 / 0.733

F1-score:
0.796 / 0.782 / 0.715

---

## Discussion

The reproduced result was lower than the original paper result. Possible reasons include:

* Reduced pretraining epochs (100 instead of 3200)
* Different GPU environment
* Different preprocessing settings
* Random seed variation

---

## Reflection

This project helped me understand the workflow of self-supervised learning and Transformer-based IMU sensing applications.
