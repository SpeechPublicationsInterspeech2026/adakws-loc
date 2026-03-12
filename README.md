# adakws-loc

# IV and OOV Trials Preparation

This repository provides a notebook for preparing **In-Vocabulary (IV)** and **Out-of-Vocabulary (OOV)** keyword spotting training, validation and evaluation trials used in AdaKWS-LOC experiments.

The notebook processes transcription and ctm files and generates **keyword–audio trial pairs** that can be used for training,validation and evaluating **keyword detection and localization**.

Notebook:

---

# Overview

The notebook performs the following steps:

1. Load ** metadata** and **transcriptions**
2. Extract candidate **keywords from transcripts**
3. Split keywords into:
   - **In-Vocabulary (IV)** keywords — seen during training
   - **Out-of-Vocabulary (OOV)** keywords — unseen during training
4. Sample keywords of different **lengths from 4 to 12 characters**
5. For each keyword length, **IV and OOV keywords are sampled based on their frequency of occurrence**
6. Generate training, validation, and evaluation trial files for keyword spotting experiments

This procedure ensures that the evaluation set contains keywords with **diverse lengths and realistic frequency distributions**.

---

# Keyword Length Sampling

Keywords are sampled for lengths:
For each keyword length:

- IV keywords are sampled based on **frequency of occurrence in transcripts**
- OOV keywords are sampled similarly to maintain a balanced distribution
- This prevents bias toward very frequent or very short keywords

---

# Data Formats

The notebook generates different file formats for **training/validation** and **evaluation**.

## Training and Validation Format

Training and validation files contain the following fields:


where:

- `utt_id` : utterance name  
- `keyword` : target keyword  
- `start_time` : start timestamp of keyword in the utterance  
- `end_time` : end timestamp of keyword in the utterance  

Example:
---
utt_001 robot 2.31 2.78
utt_002 door 1.05 1.40

## Evaluation Format

Evaluation files include additional fields length and label:
where:

- `utt_id` : utterance name  
- `keyword` : query keyword  
- `start_time` : keyword start timestamp  
- `end_time` : keyword end timestamp  
- `label` :  
  - `1` → keyword present  
  - `0` → keyword absent  
- `length` : keyword length


# Requirements

Install dependencies:
`pip install pandas numpy tqdm`


---

# Running the Notebook

Open the notebook using **Jupyter Notebook** or **Google Colab**:


Run all cells sequentially.

The notebook will generate:

- IV keywords
- OOV keywords
- Training and validation trials
- Evaluation trials
