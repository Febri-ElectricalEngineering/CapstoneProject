Deteksi Hoaks Berita Indonesia + Ringkasan Netral (IBM Granite)

Project Overview
- **Masalah**: Penyebaran hoaks berdampak pada opini publik.
- **Tujuan**: Klasifikasi `HOAX` vs `NON-HOAX` dan pembuatan ringkasan netral 3–5 kalimat untuk membantu moderasi.
- **Scope**: Teks pendek Bahasa Indonesia (tweet/teks), tanpa metadata pribadi.

Raw Dataset Link
- GitHub: IDNHoaxCorpus (lihat folder `dataset/`).

Analysis Process
1. EDA & pembersihan data (hapus URL, normalisasi sederhana)
2. Baseline: TF‑IDF + Logistic Regression
3. IBM Granite 3.1 3B (few‑shot) untuk klasifikasi (JSON output)
4. IBM Granite 3.1 3B untuk summarization (JSON: `summary`, `key_claims`)
5. Evaluasi: F1/precision/recall; ROUGE (opsional) + inspeksi manual

Insight & Findings (contoh)
- Tema hoaks dominan: politik/kesehatan.
- Ciri leksikal: klik-bait, modalitas tertentu.
- *Error analysis*: kasus ambigu atau satire.

Conclusion & Recommendations
- Daftar kata kunci pemicu & aturan `flagging` awal.
- Workflow moderasi: (1) klasifikasi → (2) prioritas review → (3) ringkasan untuk editor.
- Rencana perawatan model/prompt bulanan.

AI Support Explanation
- **Granite 3.1 3B Instruct**: open, long context (128K), mendukung klasifikasi & summarization.
- Prompt JSON-only untuk stabilitas parsing; suhu rendah untuk konsistensi.

Cara Reproduksi (Colab)
1. Aktifkan GPU di Colab, jalankan sel instalasi.
2. Jalankan seluruh sel berurutan.
3. Commit notebook via *File → Save a copy in GitHub*.


## Notebooks

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Febri-ElectricalEngineering/CapstoneProject/blob/main/notebooks/01_eda.ipynb) 01 – EDA

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Febri-ElectricalEngineering/CapstoneProject/blob/main/notebooks/02_baseline_classification.ipynb) 02 – Baseline TF-IDF Classification
