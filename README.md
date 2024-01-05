# **Tagihan Kesehatan**
### _Mengeksplorasi Variabilitas dan Analisis Komprehensif tentang Faktor-faktor yang Mempengaruhi_


## Introduction
Dalam era kesehatan modern, pemahaman mendalam terhadap faktor-faktor yang mempengaruhi tagihan kesehatan menjadi krusial. Analisis ini tidak hanya mencakup berbagai faktor seperti kebiasaan merokok, indeks massa tubuh (BMI), dan jumlah tanggungan anak, tetapi juga mengeksplorasi variabilitas yang ada dalam tagihan kesehatan. Dalam penelitian ini, kita akan memperdalam wawasan tentang bagaimana keputusan sehari-hari, seperti kebiasaan merokok, berhubungan dengan tagihan kesehatan. Selain itu, proyek ini bertujuan untuk memberikan pemahaman yang komprehensif tentang sejauh mana faktor-faktor ini berkontribusi terhadap perbedaan dalam tagihan kesehatan. Melalui analisis yang mendalam, kita berusaha menjawab pertanyaan kritis terkait variabilitas dan pengaruh faktor-faktor tertentu dalam konteks tagihan kesehatan.

> *Sumber [dataset](https://www.google.com/url?q=https://drive.google.com/uc?export%3Ddownload%26id%3D11cQ8CxIhBmajxVOlGCPH98x4sAIwKIeJ&sa=D&source=apps-viewer-frontend&ust=1704510678622707&usg=AOvVaw2ir3M7D6SYiMpzE1JrpZ2F&hl=en)*

## Research Question
### 1. Analisa Descriptive Statistic

1. Berapa rata rata umur pada dataset
2. Berapa rata rata nilai BMI dari yang merokok
3. Apakah variansi dari tagihan kesehatan perokok dan non perokok sama
4. Apakah rata rata umur perempuan dan laki-laki yang merokok sama
5. Mana yang lebih tinggi, rata rata tagihan kesehatan perokok atau non merokok
6. Mana yang lebih tinggi, rata rata tagihan kesehatan perokok yang BMI nya diatas 25 atau non perokok yang BMI nya diatas 25 (overweight)
7. BMI mana yang lebih tinggi, seseorang perokok atau non perokok

### 2. Analisa Variabel Diskrit

1. Gender mana yang memiliki tagihan paling tinggi
2. Distribusi peluang tagihan di tiap-tiap region
3. Apakah setiap region memiliki proporsi data banyak orang yang sama
4. Mana yang lebih tinggi proporsi perokok atau non perokok
5. Berapa peluang seseorang tersebut adalah perempuan diketahui dia adalah perokok
6. Berapa peluang seseorang tersebut adalah laki-laki diketahui dia adalah perokok
7. Bagaimana bentuk distribusi peluang besar tagihan dari tiap-tiap region

### 3. Analisa Variabel Kontinu

1. Mana yang lebih mungkin terjadi:

    - Seseorang dengan BMI diatas 25 mendapatkan tagihan kesehatan diatas 16.7k, atau
    - Seseorang dengan BMI dibawah 25 mendapatkan tagihan kesehatan diatas 16.7k

2. Mana yang lebih mungkin terjadi:

    - Seseorang perokok dengan BMI diatas 25 mendapatkan tagihan kesehatan diatas 16.7k, atau
    - Seseorang non perokok dengan BMI diatas 25 mendapatkan tagihan kesehatan diatas 16.7k

### 4. Analisa Korelasi Variabel
1. Korelasi tagihan kesehatan dengan BMI
2. Korelasi tagihan kesehatan dengan tanggungan anak

### 5. Pengujian Hipotesis

1. Tagihan kesehatan perokok lebih tinggi daripada tagihan kesehatan non perokok
2. Variansi tagihan kesehatan perokok dan non perokok sama
3. Tagihan kesehatan dengan BMI diatas 25 lebih tinggi daripada tagihan kesehatan dengan BMI dibawah 25

## Alur Pengerjaan Project 
1. Dataset
    - Accessing dataset
    - Load dataset
    - Create dataframe
2. Exploration and Processing
    - NaN identification
    - Outlier identification
    - Identify inconsistent format
    - Identify duplicate data
    - Other checks required
3. Explorating Data and Analysis

## _*Mari kita mulai pengerjaan projectnya*_

## 1. Dataset
  - Akses, Load dan Create Dataframe
  
        # Import library yang dibutuhkan
        import pandas as pd  # Library untuk manipulasi data menggunakan DataFrame
        import matplotlib.pyplot as plt  # Library untuk visualisasi data
        import numpy as np  # Library untuk operasi numerik
        import seaborn as sns  # Library untuk visualisasi data statistik
        
        import warnings
        warnings.filterwarnings("ignore")  # Mematikan peringatan agar tidak muncul pada output

        # Deklarasi variable df untuk membaca file insurance.csv
        df = pd.read_csv('insurance.csv')

        # Overview dataframe
        df.head()  # Menampilkan 5 baris pertama dari dataframe untuk mendapatkan gambaran awal

    tampilkan img overview df

        # Overview info dataframe
        # Untuk melihat lebih jauh tipe-tipe data pada setiap kolom
        df.info()  # Menampilkan informasi singkat tentang struktur dataframe, termasuk tipe data dan jumlah nilai non-null

    tampilkan df.info

## 2. Exploration and Processing
  - Identifikasi Nilai NaN (missing value)

        # Cek nilai NaN pada dataframe
        df.isna().sum()  # Menampilkan jumlah nilai NaN (missing values) untuk setiap kolom
    Tampilkan df.info
    Terlihat tidak ada nilai kosong (NaN) pada dataframe

  - Identifikasi Nilai Duplikat

        # Cek nilai duplikat pada dataframe
        df[df.duplicated(keep=False)]  # Menampilkan baris yang merupakan duplikat, dengan menandai semua entri duplikat

      tampilkan nilai duplikat
      - Terlihat ada 2 baris data dengan nilai yang sama, kita asumsikan hal ini adalah nilai duplikat
      - Maka kita hapus baris terakhir pada baris tersebut

            # Hapus nilai duplikat
            # Dengan pengecualian nilai awal
            df = df.drop_duplicates(keep='first').reset_index(drop=True)  # Menghapus duplikat dan mengatur ulang indeks

  ## 3. Explorating Data Analyst
  
  ### 3.1 Analisa Descriptive Statistic
  
  - Berapa rata rata umur pada dataframe
  
        # Hitung rata-rata umur pada dataframe
        avg_umur = df['age'].mean()
        print(f'Rata-rata umur: {avg_umur:.2f} tahun')

        # Visualisasi rata-rata umur menggunakan boxplot
        sns.set_theme()
        plt.figure(figsize=(10, 6))
        sns.boxplot(x=df['age'])
        plt.axvline(avg_umur, color='red', linestyle='dashed', linewidth=2, label=f'Rata-rata umur: {avg_umur:.2f}')
        plt.title('Distribusi Rata-rata Umur')
        plt.xlabel('Umur (tahun)')
        plt.legend()
        plt.show()

    ![viz](img/avg_umur.png)
    
    Terlihat rata-rata umur pada dataframe adalah: 39.22 tahun

  - Berapa rata rata nilai BMI dari yang merokok

        # Hitung nilai rata-rata BMI yang perokok
        avg_bmi_smoker = df[df['smoker'] == 'yes']['bmi'].mean()
        
        print(f'Rata-rata BMI yang perokok: {avg_bmi_smoker:.2f}')

        # Visualisasi BMI Perokok menggunakan boxplot
        plt.figure(figsize=(10, 6))
        sns.boxplot(x=df['bmi'])
        plt.axvline(avg_bmi_smoker, color='red', linestyle='dashed',
                    linewidth=2,
                    label=f'Rata-rata BMI Perokok: {avg_bmi_smoker:.2f}')
        plt.title('Distribusi Rata-rata BMI Perokok')
        plt.xlabel('BMI')
        plt.legend()
        plt.show()

    ![viz](img/avg_bmi_perokok.png)

    Terlihat rata-rata BMI yang merokok adalah: 30.71

  - Apakah variansi dari tagihan kesehatan perokok dan non perokok sama?

        # Hitung variansi tagihan kesehatan yang perokok
        variansi_tagihan_smoker = df[df['smoker'] == 'yes']['charges'].var()
        
        # Hitung variansi tagihan kesehatan yang non perokok
        variansi_tagihan_non_smoker = df[df['smoker'] == 'no']['charges'].var()

        # Visualisasi Variansi tagihan kesehatan perokok dan non perokok
        plt.figure(figsize=(10, 6))
        plot = sns.barplot(x=['Perokok', 'Non Perokok'], y=[variansi_tagihan_smoker, variansi_tagihan_non_smoker], palette=['grey', 'green'])
        
        for i, value in enumerate([variansi_tagihan_smoker, variansi_tagihan_non_smoker]):
            plot.text(i, value + 0.2, f'{value:.2f}', ha='center', va='bottom', color='black', fontsize=10)
        
        plt.title('Variansi Tagihan Kesehatan Perokok & Non Perokok')
        plt.ylabel('Variansi')
        plt.show()
        
        # Print variansi tagihan kesehatan perokok dan non perokok
        print(f'Variansi tagihan untuk perokok       : {variansi_tagihan_smoker:.2f}') # dibulatkan 2 angka dibelakang koma
        print(f'Variansi tagihan untuk non perokok   : {variansi_tagihan_non_smoker:.2f}') # dibulatkan 2 angka dibelakang koma

    ![viz](img/var_charges_smoker_nonsmoker.png)

    Terlihat rata-rata Variansi tagihan perokok lebih besar dibanding non perokok yaitu 133207311.21 berbanding 35925420.50
    
