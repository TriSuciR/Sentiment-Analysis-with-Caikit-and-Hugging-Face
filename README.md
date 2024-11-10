<h1 align="center">Analisis Sentimen Teks menggunakan Caikit dan Hugging Face
Penulis: Cognitive Class AI

<p align="center"> Selamat datang di proyek Analisis Sentimen yang menggabungkan kekuatan Caikit dan Hugging Face! 
Proyek ini bertujuan untuk menganalisis sentimen teks menggunakan model transformer terbaru dari Hugging Face, dan mengintegrasikannya dengan kerangka kerja Caikit. 
Solusi ini memungkinkan Anda untuk memahami emosi dan opini dalam teks secara lebih efisien dan akurat.</p>



<div align="center">
    <img src="https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white">
    <img src="https://img.shields.io/badge/Hugging%20Face-Transformer-yellow?logo=huggingface&logoColor=white">
    <img src="https://img.shields.io/badge/Caikit-Analisis%20Sentimen-blueviolet">
    <img src="https://img.shields.io/badge/Linux-x86__64-important?logo=linux">
</div>

---

# 🚀 Fitur Utama:
- * Model Sentimen Terbaru: Memanfaatkan model transformer terkini dari Hugging Face untuk menganalisis sentimen dengan tingkat akurasi yang tinggi.
- * Integrasi dengan Caikit: Menggunakan Caikit sebagai framework modular yang memungkinkan pengembangan AI yang lebih fleksibel dan skalabel.
- * Antarmuka Pengguna yang Ramah: Menyediakan antarmuka yang intuitif dan mudah digunakan, sehingga memungkinkan siapa saja untuk mencoba analisis sentimen.
- * Dukungan Multi-Bahasa: Dapat menganalisis sentimen dalam berbagai bahasa utama.
- * Visualisasi Hasil: Menampilkan hasil analisis dengan cara yang mudah dipahami.

## 📦 Instalasi
Ikuti langkah-langkah di bawah untuk menginstal dan menjalankan proyek ini di lingkungan lokal Anda:

## ✨ Teknologi yang Digunakan:
- Python (v3.8+)
- Hugging Face Transformers
- Caikit (v0.9.2)

## 📝 Persyaratan:
1. Linux/MacOS x86_64
2. Caikit v0.9.2
3. Python 3.8+
4. pip (v23.0+)

## Langkah Instalasi:

1. Instalasi virtualenv:  
   Gunakan perintah berikut untuk menginstal `virtualenv`:

   ```bash
   pip install --user virtualenv
   ```

2. Buat Virtual Environment:  
   Buat lingkungan virtual baru dengan perintah:

   ```bash
   virtualenv -p python3 env
   ```

3. Aktifkan Virtualenv:  
   Untuk mengaktifkan lingkungan virtual, gunakan perintah:

   - Di Linux/MacOS:
     ```bash
     source env/bin/activate
     ```

   - Di Windows (PowerShell):
     ```bash
     .\env\Scripts\Activate
     ```

4. Instalasi Paket yang Diperlukan:  
   Instal semua dependensi yang dibutuhkan dari file `requirements.txt`:

   ```bash
   pip install -r requirements.txt
   ```

5. Mulai Runtime:  
   Jalankan runtime untuk memulai model dan layanan analisis sentimen:

   ```bash
   python start_runtime.py
   ```

6. Jalankan Klien:  
   Setelah runtime berjalan, Anda bisa menguji aplikasi klien dengan perintah berikut:

   ```bash
   python client.py
   ```

## Prosedur Konfigurasi:
Ikuti langkah-langkah berikut untuk menyiapkan runtime Caikit dan model AI, kemudian uji menggunakan aplikasi klien:

1. Buat Proyek:  
   Buat direktori dan file yang diperlukan untuk proyek Anda:

   ```bash
   pip install --user virtualenv  
   mkdir -p /home/project/text-sentiment/text_sentiment  
   cd /home/project/text-sentiment/text_sentiment
   ```

2. Buat Spesifikasi Model Data:  
   Tentukan format data yang digunakan oleh modul Caikit:

   ```bash
   mkdir data_model
   cd data_model
   touch classification.py
   ```

3. Buat Pembungkus Model:  
   Buat pembungkus yang mengintegrasikan model AI dengan Caikit:

   ```bash
   mkdir -p models/text_sentiment
   cd models/text_sentiment
   touch config.yml
   mkdir runtime_model
   cd runtime_model
   touch hf_module.py
   touch __init__.py
   cd ../../..  # Kembali ke direktori proyek
   ```

4. Sertakan Modul dan Ketergantungan Paket:  
   Tentukan ketergantungan yang diperlukan dalam file konfigurasi proyek:

   ```bash
   touch requirements.txt
   virtualenv -p python3 env
   source env/bin/activate
   pip install -r requirements.txt
   ```

5. Mulai Runtime Caikit:  
   Jalankan runtime Caikit untuk menyediakan model untuk inferensi:

   ```bash
   touch start_runtime.py
   python start_runtime.py
   ```

6. Uji Analisis Sentimen:  
   Uji model untuk memastikan analisis sentimen berjalan dengan baik melalui aplikasi klien:

   ```bash
   touch client.py
   python client.py
   ```

## **Penggunaan:**
Setelah aplikasi berjalan, Anda bisa memasukkan teks untuk dianalisis sentimennya melalui antarmuka pengguna. Hasil analisis akan menunjukkan apakah sentimen teks tersebut bersifat positif, negatif, atau netral.

## 💻 **Kode Utama**

Berikut adalah kode utama untuk menjalankan analisis sentimen dalam proyek ini:

```python
# Copyright Penulis Caikit
#
# Lisensi Apache, Versi 2.0
#
# Hak Cipta (c) Penulis

import os
import grpc
from caikit.runtime.service_factory import ServicePackageFactory
from text_sentiment.data_model import TextInput

# Siapkan layanan inferensi
inference_service = ServicePackageFactory().get_service_package(
    ServicePackageFactory.ServiceType.INFERENCE,
)

port = 8085

# Mengonfigurasi klien
channel = grpc.insecure_channel(f"localhost:{port}")
client_stub = inference_service.stub_class(channel)

# Menjalankan inferensi untuk dua contoh teks
for text in ["The sunset was beautiful", "yet I felt sad to see it go."]:
    input_text_proto = TextInput(text=text).to_proto()
    request = inference_service.messages.HuggingFaceSentimentTaskRequest(
        text_input=input_text_proto
    )
    response = client_stub.HuggingFaceSentimentTaskPredict(
        request, metadata=[("mm-model-id", "text_sentiment")]
    )
    print("Text:", text)
    print("RESPONSE:", response)
```

## 📊 Contoh Hasil Akhir
Berikut adalah contoh output yang dapat Anda peroleh setelah melakukan analisis sentimen:

```
Text: The sunset was beautiful
RESPONSE: [Positif]

Text: yet I felt sad to see it go.
RESPONSE: [Negatif]
```

---

Dengan proyek ini, Anda bisa dengan mudah menganalisis sentimen teks dalam berbagai bahasa dan mendapatkan wawasan tentang opini atau emosi yang terkandung di dalamnya. Semoga proyek ini bermanfaat!
