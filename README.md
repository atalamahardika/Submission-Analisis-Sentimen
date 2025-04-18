# Submission Dicoding "Analisis Sentimen. Studi Kasus: App Mobile Legends"  
## Deskripsi Data  
Dataset ini merupakan hasil scrapping mandiri dengan library dari `google_play_scrapper` dengan total data 15.000 ulasan. Kemudian data tersebut diolah dengan mempertahankan 2 kolom utama yakni `content` sebagai ulasan dan `score` sebagai rating aplikasinya.  

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