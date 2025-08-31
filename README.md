## Project Overview
Deteksi hoaks Bahasa Indonesia dengan pendekatan hybrid: TF-IDF + Logistic Regression (screening cepat) dan IBM Granite 3.1-3B Instruct (4-bit) untuk kasus “zona ragu”. Output akhir: klasifikasi HOAX/NON-HOAX, insight EDA, dan contoh summarization JSON-only.

## Dataset
- Sumber: (isi nama/daring Kaggle/sumber publik yang dipakai).
- Lisensi: (cantumkan lisensi sumber).
- Pembagian: train/valid/test dengan stratified split.

## Pipeline & Tools
- Baseline: TF-IDF (1–2gram, 30k fitur) + LR (class_weight="balanced") + tuning threshold.
- Hybrid: zona ragu **low=0.42, high=0.58**, kasus ragu → **IBM Granite 3.1-3B (4-bit)** few-shot (prompt **JSON-only**, ensemble header).
- Artefak model & laporan tersimpan di `artifacts/`.

## Cara Reproduksi (Colab + GitHub, tanpa Drive)
1. Buka notebook `notebooks/Capstone_Hoax_ID.ipynb` di Colab.
2. Jalankan sel persiapan data (unduh dataset publik) → split.
3. Jalankan sel baseline LR → Granite → **Finalisasi HYBRID (LOCK)**.
4. Artefak akan muncul di `./artifacts/` (siap commit).

## AI Support
- IBM Granite 3.1-3B Instruct (4-bit) via HuggingFace Transformers untuk **few-shot classification** & **summarization** (JSON-only).
- LR untuk high/low confidence; Granite hanya untuk ~25% “zona ragu” (efisien).

## Insight & Temuan
- Dataset imbalanced (HOAX dominan) → thresholding + hybrid penting agar recall NON-HOAX tidak jatuh.
- HYBRID meningkatkan keseimbangan metrik tanpa mengorbankan akurasi keseluruhan.
- Lihat `artifacts/*report*.json` & CM PNG untuk detail per kelas.

## Rekomendasi
- Perbanyak contoh **NON-HOAX** (kurangi bias).
- Kalibrasi threshold berkala (drift).
- Ekstensi multi-kelas (kategori topik hoaks).


## Notebooks

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Febri-ElectricalEngineering/CapstoneProject/blob/main/notebooks/01_eda.ipynb) 01 – EDA

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Febri-ElectricalEngineering/CapstoneProject/blob/main/notebooks/02_baseline_classification.ipynb) 02 – Baseline TF-IDF Classification

