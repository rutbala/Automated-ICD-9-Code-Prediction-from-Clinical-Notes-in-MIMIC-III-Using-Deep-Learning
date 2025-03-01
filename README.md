# Automated-ICD-9-Code-Prediction-from-Clinical-Notes-in-MIMIC-III-Using-Deep-Learning

Introduction

This project focuses on predicting medical billing codes (ICD-9) from clinical notes in the revenue cycle. I approached this task using multi-label classification, hierarchical classification, and information retrieval techniques. Specifically, I implement five deep learning models:

1. Hierarchical Self-Attention Network

2. Self-Attention Long Short-Term Memory (SLSTM)
   
3. Codes-Attentive Long Short-Term Memory (CLSTM)

4. Hierarchical Attention Network (HAN)
  
5. Fine-Tuning on Pretrained Clinical BERT

This study explores two types of attention mechanisms across different model architectures. All models are evaluated on the publicly available MIMIC-III dataset using macro-F1, micro-F1, and precision@N metrics.
