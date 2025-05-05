# Submission Dicoding "Analisis Sentimen. Studi Kasus: App Mobile Legends"  
## Abstrak  
Dataset ini merupakan hasil scrapping mandiri dengan library dari `google_play_scrapper` dengan total data 70.000 ulasan. Kemudian data tersebut diolah dengan mempertahankan kolom utama yakni `content` sebagai ulasan. Lalu kita labeling data dengan polarity score dengan 3 kelas (positive, neutral, dan negative). Untuk model yang digunakan yaitu simpleRNN, GRU, dan Custom. Dari ketiga model tersebut yang digunakan untuk inference adalah model GRU karena menunjukkan validation accuracy yang tinggi dan validation loss yang rendah.

## Cara Menjalankan  
1. Clone repository  
```  
git clone https://github.com/atalamahardika/Submission-Analisis-Sentimen.git
```
2. Buat virtual environment  
```
conda create --name sentimen-analisis python=3.13
conda activate base
conda activate sentimen-analisis
pip install -r requirements.txt
```
3. Khusus train model
Terdapat 2 pilihan yakni :  
a. Menggunakan google colab  
b. Menggunakan WSL Ubuntu dengan tensorflow terbaru yang mendukung GPU (lokal)