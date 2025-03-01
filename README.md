# Automated-ICD-9-Code-Prediction-from-Clinical-Notes-in-MIMIC-III-Using-Deep-Learning

Introduction

This project focuses on predicting medical billing codes (ICD-9) from clinical notes in the revenue cycle. I approached this task using multi-label classification, hierarchical classification, and information retrieval techniques. Specifically, I implement five deep learning models:

1. Hierarchical Self-Attention Network

2. Self-Attention Long Short-Term Memory (SLSTM)
   
3. Codes-Attentive Long Short-Term Memory (CLSTM)

4. Hierarchical Attention Network (HAN)
  
5. Fine-Tuning on Pretrained Clinical BERT

This study explores two types of attention mechanisms across different model architectures. All models are evaluated on the publicly available MIMIC-III dataset using macro-F1, micro-F1, and precision@N metrics.

Data

I trained and evaluated this approach using MIMIC-III (Medical Information Mart for Intensive Care), an open-access dataset containing de-identified medical records from Beth Israel Deaconess Medical Center spanning 2001 to 2012. The dataset includes information from 58,976 hospital admissions across 46,520 patients. Each record documents diagnoses and procedures during a patient’s stay, encompassing structured data, free-text clinical notes, and human-tagged ICD-9 codes.

For this project, it focuses on the following tables from the MIMIC-III dataset:

![Schema](https://github.com/user-attachments/assets/84caff9d-5048-4553-9326-9148d2a28319)
