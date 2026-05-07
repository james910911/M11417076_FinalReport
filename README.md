# LIMU-BERT Reproduction

## Environment
- Google Colab
- Tesla T4 GPU
- Python 3.12
- PyTorch

## Paper
### LIMU-BERT: Unleashing the Potential of Unlabeled Data for IMU Sensing Applications

Paper URL: https://arxiv.org/abs/2106.08265

Official GitHub: https://github.com/dapowan/LIMU-BERT-Public

## Dataset
- UCI HAR Dataset
- Version: 20_120

This project uses the UCI Human Activity Recognition (HAR) dataset for reproduction experiments.

## Reproduction Process

### 1. Clone Repository

    git clone https://github.com/dapowan/LIMU-BERT-Public.git
    cd LIMU-BERT-Public

### 2. Install Requirements

    pip install -r requirements.txt

### 3. Check GPU

    import torch
    
    print(torch.cuda.is_available())
    print(torch.cuda.get_device_name(0))

Expected output:

    True
    Tesla T4

## Training Procedure

### Step 1 — Pretraining

    python pretrain.py v1 uci 20_120 -s limu_v1_fast

This step performs self-supervised pretraining for LIMU-BERT.

### Step 2 — Generate Embedding

    python embedding.py v1 uci 20_120 -f limu_v1_fast

This step generates feature embeddings from the pretrained model.

### Step 3 — Train Classifier

    python classifier.py v2 uci 20_120 -f limu_v1_fast -s limu_gru_v1_fast -l 0

This step trains the downstream HAR classifier.

## Reproduced Result

### Best Accuracy
- 0.833 / 0.822 / 0.733

### Best F1-score
- 0.796 / 0.782 / 0.715

## Gap Analysis & Discussion

The reproduced result was lower than the original paper result.

Possible reasons include:

- Reduced pretraining epochs (100 instead of 3200)
- Different GPU environment
- Different preprocessing settings
- Random seed variation
- Limited training time in Google Colab
- Different library or dependency versions

In addition, some hidden hyperparameter settings may not be fully described in the original paper.

## Proposed Improvement

Possible improvements include:

- Increase pretraining epochs
- Use larger datasets for self-supervised learning
- Apply data augmentation
- Tune learning rate and batch size
- Use stronger GPU hardware
- Test on additional HAR datasets

## Cross-Dataset Discussion

The model performance may decrease when evaluated on different HAR datasets because:

- Sensor placement may differ
- Activity distributions are different
- Motion patterns vary across datasets
- Domain shift exists between datasets

This demonstrates the importance of cross-domain generalization in HAR research.

## Reflection

This project helped me understand:

- Self-supervised learning
- Transformer-based IMU sensing
- Representation learning for HAR tasks
- Reproduction workflow in deep learning research
- The importance of reproducibility in neural network research

I also learned how different training settings can significantly affect final performance.

## Files

- pretrain.py → self-supervised pretraining
- embedding.py → embedding generation
- classifier.py → downstream classification
- training_result.png → reproduction result screenshot
- LIMU_BERT_Reproduction.ipynb → Colab notebook
