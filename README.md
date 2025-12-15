
# Klasifikasi Gambar Sayuran Menggunakan CNN

Proyek ini membangun model **Convolutional Neural Network (CNN)** untuk mengklasifikasikan gambar sayuran menggunakan dataset *Vegetable Image Dataset*. Dataset diproses secara manual dengan pembagian **70% Train**, **15% Validation**, dan **15% Test**.

Model dikembangkan menggunakan **TensorFlow dan Keras** di Google Colab, kemudian diekspor dalam tiga format berbeda:
- **SavedModel** → untuk deployment backend/server
- **TensorFlow Lite (TFLite)** → untuk aplikasi mobile
- **TensorFlow.js (TFJS)** → untuk digunakan di browser

---

## Langkah Utama Proyek

### 1. Import Dataset dan Split Manual 70/15/15
- Dataset diambil melalui `kagglehub`.
- Semua gambar di-scan dan label diambil dari nama folder.
- Data dibagi menggunakan `train_test_split` dengan stratifikasi.
- Hasil split disalin otomatis ke:
  - `split_data/train/`
  - `split_data/validation/`
  - `split_data/test/`

### 2. Data Generator
Menggunakan `ImageDataGenerator`:
- **train_gen** → augmentasi + normalisasi
- **val_gen** dan **test_gen** → hanya normalisasi (`rescale=1./255`)

Kelas otomatis terdeteksi berdasarkan struktur folder.

### 3. Pembangunan Model CNN
Model menggunakan arsitektur `Sequential` dengan layer:
- `Conv2D`
- `BatchNormalization`
- `MaxPooling2D`
- `Dropout`
- `Flatten`
- `Dense`

Konfigurasi training:
- Optimizer: `Adam(1e-3)`
- Loss: `categorical_crossentropy`
- Metric: `accuracy`

### 4. Training Model
Menggunakan callback:
- **EarlyStopping**
- **ReduceLROnPlateau**
- **ModelCheckpoint** → menyimpan model terbaik ke `exports/best_model.keras`
- **CSVLogger**

Visualisasi:
- Plot akurasi (train vs validation)
- Plot loss (train vs validation)

### 5. Evaluasi Model
Evaluasi dilakukan pada:
- **Train**
- **Validation**
- **Test**

Menghasilkan:
- Accuracy
- Loss
- Classification Report
- Confusion Matrix

### 6. Export Model
Model disimpan dalam tiga format:
- `exports/saved_model/` → SavedModel
- `exports/tflite/model.tflite` → TFLite
- `exports/tfjs_model/` → TensorFlow.js

Selain itu dibuat file:
- `label.txt` → daftar label kelas

### 7. Inferensi
Inferensi dilakukan pada beberapa gambar acak dari folder:
- `split_data/test/`

Model menampilkan:
- Predicted label
- Confidence score
- Visualisasi gambar hasil prediksi

---

## Tools & Library
- TensorFlow
- Keras
- Matplotlib
- NumPy
- Pillow
- scikit-learn
- KaggleHub
- TensorFlow.js converter

---

## Output Utama
- `exports/best_model.keras`
- `exports/saved_model/` → Model untuk server/cloud
- `exports/tflite/model.tflite` → Model untuk mobile (Android/iOS)
- `exports/tfjs_model/` → Model untuk web
- `training_log.csv`
- Grafik akurasi & loss
- Hasil prediksi gambar acak

---

## Lisensi
Dataset berasal dari Kaggle: *Vegetable Image Dataset*.

