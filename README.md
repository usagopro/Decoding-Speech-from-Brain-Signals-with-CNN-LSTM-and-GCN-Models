# EEG-based Envelope Reconstruction  

This repository contains code and experiments for reconstructing the **speech envelope** from EEG signals using the **SparrKULee EEG dataset**. Multiple deep learning models, including CNNs, LSTMs, Transformers, and GCN-based architectures, have been implemented and compared.  

---

# Dataset Description  

We use the **SparrKULee EEG dataset**:  
- Subjects: 85 participants  
- Trials: 668 total (each ~15 minutes long)  
- Stimuli: Audiobooks and podcasts  
- EEG: 64 channels recorded while subjects listened to audio  
- Sampling: Downsampled to 64 Hz

**Preprocessing steps:**  
- EEG + envelope downsampled to 64 Hz  
- Data augmented into 5-second samples (with and without overlap)  
- Both normalized and non-normalized data tested  
- Split: 80% train, 10% validation, 10% test  

---

# Data Analysis  

- Pearson correlation between EEG channels and the speech envelope was computed across different frequency bands:  
  - Delta [0.5–4 Hz]  
  - Theta [4–8 Hz]  
  - Alpha [8–14 Hz]  
  - Beta [14–30 Hz]  
  - Broadband [0.5–32 Hz]  

**Observations:**  
- Correlations were near 0 across all bands  
- No significant difference between raw and artefact-removed EEG  
- Correlation did not depend on audio type (audiobooks vs. podcasts)  

---

# Models Implemented  

## Pretrained Models  
- VLAAI model → Pearson ≈ 0.10  
- Linear backward model → Pearson ≈ 0.15 (Delta band)  
- Dilated CNN → Match-mismatch task, accuracy > 90% (20s window)  

## Custom Models  
- Feedforward NN → Pearson ≈ 0.006  
- EEG Transformers → Pearson ≈ 0.095  
- Hybrid 4-block model → Multi-loss training  
- Clustered + CNN/LSTM → No significant improvement  
- TGCN (Graph-based) → Pearson ≈ 0.064, CosSim ≈ 0.79  
- GCN + LSTM + CNN → Pearson ≈ 0.098  
- CNN + LSTM (2x2 blocks) → Pearson ≈ 0.11  
- CNN + LSTM + Transformers → Pearson ≈ 0.07  

---

# Key Observations  

- Individual EEG channels show very weak correlation with the speech envelope (between -0.10 and +0.10)  
- Models achieve high cosine similarity (~0.77–0.80) but low Pearson correlation (~0.0–0.1)  
- Pretrained and hybrid models outperform simple networks, but still fail to capture strong correlation  
- Future work: focus on Graph Convolutional Networks (GCNs), as suggested by recent literature in EEG decoding  

---

# Getting Started  

Clone the repository:  
```bash
git clone https://github.com/usagopro/Research.git

