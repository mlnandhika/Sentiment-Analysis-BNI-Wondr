# Analisis Sentimen Ulasan Aplikasi Wondr by BNI (Google Play Store)

Proyek ini bertujuan untuk melakukan scraping data ulasan, pemrosesan teks (text preprocessing), dan analisis sentimen berbasis leksikon (Lexicon-based Sentiment Analysis) terhadap ulasan pengguna aplikasi mobile banking Wondr by BNI di Google Play Store.

---

## Fitur Dan Alur Kerja Proyek

1. **Data Scraping**: Mengambil ulasan terbaru pengguna aplikasi Wondr by BNI (`id.bni.wondr`) menggunakan library `google-play-scraper`.
2. **Data Cleaning**: Menghapus kolom yang tidak relevan serta membersihkan baris data yang terduplikasi.
3. **Text Preprocessing**:
   - **Text Cleaning**: Menghapus mention, hashtag, URL, angka, dan tanda baca.
   - **Case Folding**: Mengubah seluruh teks menjadi huruf kecil (*lowercase*).
   - **Slang Normalization**: Mengganti kata-kata tidak baku/gaul menggunakan Kamus Alay Lexicon (`nasalsabila/kamus-alay`).
   - **Tokenizing**: Memecah kalimat menjadi kumpulan kata menggunakan `NLTK`.
   - **Stopword Removal**: Menghapus kata hubung/kata umum dalam Bahasa Indonesia & Inggris serta stopwords khusus.
   - **Stemming**: Mengubah kata ke bentuk dasarnya menggunakan `Sastrawi`.
4. **Lexicon-Based Sentiment Labeling**: Menghitung skor polaritas sentimen berdasarkan kamus leksikon kata positif dan negatif untuk mengklasifikasikan ulasan menjadi:
   - `positive`
   - `neutral`
   - `negative`
5. **Data Exploration & Visualization**: Visualisasi distribusi sentimen ulasan dan sebaran panjang kata ulasan menggunakan `Seaborn` dan `Matplotlib`.

---

## Struktur Dataset

File dataset yang dihasilkan (`wondr_bni_reviews.csv`) memiliki kolom sebagai berikut:

| Nama Kolom | Deskripsi |
| :--- | :--- |
| `content` | Teks ulasan asli dari pengguna |
| `score` | Rating bintang (1 - 5) yang diberikan pengguna |
| `text_clean` | Teks ulasan setelah pembersihan karakter khusus |
| `text_casefoldingText` | Teks ulasan yang sudah diubah ke huruf kecil |
| `text_slangwords` | Teks ulasan setelah normalisasi kata gaul/singkatan |
| `text_tokenizingText` | Hasil tokenisasi kata dalam bentuk list |
| `text_stopword` | List kata setelah pembuangan stopword |
| `text_stemming` | Teks ulasan akhir yang sudah distem (*akar kata*) |
| `polarity_score` | Skor numerik hasil perhitungan leksikon positif/negatif |
| `polarity` | Label sentimen (`positive`, `neutral`, `negative`) |

---

##  Instalasi 

### 1. Prasyarat
Pastikan Anda telah menginstal **Python 3.11+**.

### 2. Cloning / Download Repositori
```bash
git clone https://github.com/username/wondr-bni-sentiment-analysis.git
cd wondr-bni-sentiment-analysis
```

### 3. Membuat Virtual Environment (Opsional tetapi Disarankan)
```bash
# macOS/Linux
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate
```

### 4. Menginstal Dependensi
Instal seluruh library yang dibutuhkan dengan perintah berikut:
```bash
pip install -r requirements.txt
```

### 5. Mengunduh Resource NLTK
Saat pertama kali menjalankan notebook atau skrip Python, pastikan modul NLTK diunduh:
```python
import nltk
nltk.download('punkt')
nltk.download('punkt_tab')
nltk.download('stopwords')
nltk.download('wordnet')
```

---

## Cara Menjalankan

Proyek ini terbagi menjadi dua tahap utama (dapat dijalankan melalui Jupyter Notebook atau Google Colab / Kaggle):

1. **Scraping Data (`Notebook 1: Scraping`)**:
   - Jalankan notebook scraping untuk mengambil ulasan terbaru dari Google Play Store.
   - Hasil scraping akan disimpan secara otomatis ke file `wondr_bni_reviews.csv`.

2. **Sentiment Analysis (`Notebook 2: Preprocessing & Sentiment Analysis`)**:
   - Muat file `wondr_bni_reviews.csv`.
   - Jalankan seluruh sel untuk melakukan preprocessing teks, pelabelan leksikon, serta menampilkan grafik distribusi sentimen.

