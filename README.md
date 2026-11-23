# Bank Account Fraud Detection — MLOps Assignment

Deteksi penipuan pembukaan rekening bank menggunakan dataset **Bank Account Fraud (BAF) Suite** varian Base (NeurIPS 2022).

## 1. Metode
Saya menggunakan **LightGBM Classifier** dengan `class_weight='balanced'`. Alasan memilih:
- LightGBM efisien untuk data tabular dan terbukti menjadi *state-of-the-art* pada dataset BAF.
- Dataset ini *highly imbalanced* (fraud < 2%), sehingga `class_weight='balanced'` sangat penting.
- LightGBM dapat menangani *missing values* dan data kategorikal secara native.

## 2. Cara Membagi Data
Saya menggunakan **Time-Based Split**:
- **Train**: Bulan 0, 1, 2
- **Test (Validasi)**: Bulan 3
**Alasan**: Untuk mensimulasikan kondisi produksi nyata dan menghindari *data leakage*, karena model harus diuji pada data masa depan yang belum pernah dilihat.

## 3. Skor di Data Validasi
- **TPR @ FPR 5%**: **56.61%**
- **Threshold**: **0.8309**

Artinya: Dengan toleransi salah tuduh maksimal 5% nasabah jujur, model berhasil menangkap 56.61% penipu.

## 4. Struktur File
- `notebook.ipynb`: Eksperimen lengkap.
- `models/baf_fraud_model.pkl`: Model yang sudah dilatih.
- `requirements.txt`: Daftar library.
