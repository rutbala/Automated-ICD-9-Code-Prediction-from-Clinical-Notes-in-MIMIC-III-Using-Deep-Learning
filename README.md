# Automated-ICD-9-Code-Prediction-from-Clinical-Notes-in-MIMIC-III-Using-Deep-Learning

Introduction:-

This project focuses on predicting medical billing codes (ICD-9) from clinical notes in the revenue cycle. I approached this task using multi-label classification, hierarchical classification, and information retrieval techniques. Specifically, I implement five deep learning models:

1. Hierarchical Self-Attention Network

2. Self-Attention Long Short-Term Memory (SLSTM)
   
3. Codes-Attentive Long Short-Term Memory (CLSTM)

4. Hierarchical Attention Network (HAN)
  
5. Fine-Tuning on Pretrained Clinical BERT

This study explores two types of attention mechanisms across different model architectures. All models are evaluated on the publicly available MIMIC-III dataset using macro-F1, micro-F1, and precision@N metrics.

Data:-

I trained and evaluated this approach using MIMIC-III (Medical Information Mart for Intensive Care), an open-access dataset containing de-identified medical records from Beth Israel Deaconess Medical Center spanning 2001 to 2012. The dataset includes information from 58,976 hospital admissions across 46,520 patients. Each record documents diagnoses and procedures during a patient’s stay, encompassing structured data, free-text clinical notes, and human-tagged ICD-9 codes.

For this project, it focuses on the following tables from the MIMIC-III dataset:

![Schema](https://github.com/user-attachments/assets/84caff9d-5048-4553-9326-9148d2a28319)

Preprocessing:-

1. The Data Processing file includes methods for extracting, transforming, and loading medical notes and ICD-9 codes from the relevant MIMIC-III tables.

2. The Note Sections file segments clinical notes into different sections and further divides each section into individual sentences. By consulting medical literature and professionals, the preprocessing pipeline discards irrelevant content, converts text to lowercase, removes stopwords and special characters, and applies lemmatization and tokenization.

3. The High-Level Codes file maps low-level ICD-9 codes to higher-level categories, grouping them into broader classifications for better interpretability and hierarchical modeling.

Models:-

1. LSTM (Long Short-Term Memory Networks)

I experimented with Self-Attention Long Short-Term Memory (SLSTM) and Codes-Attentive Long Short-Term Memory (CLSTM) models. Both architectures are relatively shallow, utilizing a core bi-directional LSTM layer for word-level encoding. The attention mechanism is applied to generate a probability distribution over features, enabling the models to assign higher importance to relevant information.

The CLSTM model incorporates an additional title matrix as input, which helps capture contextual relevance between disease names and clinical notes. As a result, it demonstrated superior performance compared to the simpler SLSTM model.

The LSTM file contains the model implementation and evaluation scripts for both SLSTM and CLSTM.

The util file includes code for extracting ICD-9 code titles (disease names) and constructing the text corpus.

![LSTM](https://github.com/user-attachments/assets/214756cf-f005-4e47-a1a4-0fbb9f36e4f9)

2. HAN (Hierarchical Attention Network)

The Hierarchical Attention Network (HAN) applies attention mechanisms at multiple levels of a document, enabling a structured and context-aware representation of clinical notes.

As illustrated in the figure, HAN consists of:

(i) Word-Level Encoding: A sequence encoder processes individual words, followed by an attention layer that assigns importance scores to words.

(ii) Sentence-Level Encoding: Encoded word representations are aggregated into sentence vectors, which are then passed through another attention layer to highlight key sentences.

(iii) Document Representation: The final document vector is obtained by attending to the most relevant sentences.

(iv) Classification Layer: A fully connected layer, along with its activation function, utilizes the document representation for ICD-9 code prediction.

This hierarchical structure allows the model to progressively refine document representations, capturing the importance of different sections and contents more effectively.

![HAN](https://github.com/user-attachments/assets/d7fd6e7b-786f-42d2-aca8-6c7c0c3001cd)

3. BERT (Bidirectional Encoder Representations from Transformers)

The model is fine-tuned on ClinicalBERT, leveraging all MIMIC-III clinical notes. It is based on BioBERT-Base v1.1, trained on:

(i) PubMed 200K abstracts

(ii) PMC 270K full-text articles

Model Configuration:-

(i) Vocabulary size: 28,996

(ii) Embedding dimension: 768

(iii) Hidden state dimension: 768

The pre-trained ClinicalBERT model ends with a BertPooler layer, which is concatenated with a dense layer for multi-label classification.

(i) Sigmoid activation function is applied to convert logits into probabilities for each ICD-9 code.

(ii) Labels with probabilities greater than 0.5 are considered positive predictions.

(iii) Gradient Clipping is applied to prevent overflow issues in the sigmoid function, restricting logits within [-0.14, 0.14] before feeding them into the loss function.

Training Constraints:- 

Due to BERT’s maximum sequence length limitation, we set:

(i) Maximum sequence length: 512 tokens

(ii) Batch size: 8


