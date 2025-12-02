# 🥣 **Cereal Analysis – KNIME Workflow**

Analisis nutrisi, visualisasi data, dan klasifikasi kesehatan sereal

---

## 📌 **Deskripsi Proyek**

Repository ini berisi **workflow KNIME Modern UI** untuk melakukan analisis pada dataset sereal (Cereals.csv).
Tujuan proyek:

1. **Membersihkan & mempersiapkan dataset**
2. **Melakukan exploratory data analysis (EDA)**
3. **Visualisasi nutrisi sereal (scatter plot, bar chart, histogram, pie chart)**
4. **Membuat klasifikasi sederhana HEALTHY vs UNHEALTHY**
5. **Memberikan insight yang mudah dipahami**

Workflow ini sangat cocok untuk pemula KNIME, karena langkah-langkahnya dibuat **ringkas, modular, dan mudah dipelajari**.

---

## 📁 **Isi Repository**

```
📦 Cereal-Analysis-KNIME
├── cerealworkflow.knwf     → workflow KNIME Modern UI
├── Cereals.csv             → dataset cereal
├── README.md               → dokumentasi proyek
```

---

## 🧠 **Alur Workflow (Ringkasan)**

```
CSV Reader
 → Missing Value
 → Column Filter
 → Math Formula (opsional)
 → Normalizer
 → Rule Engine (Healthy/Unhealthy)
        ↳ Bar Chart (Distribusi Health Status)
        ↳ Pie Chart  (Proporsi Health Status)
 → Scatter Plot (Visualisasi 2 variabel)
 → Histogram (Distribusi numerik)
```

Model klasifikasi **opsional**, sehingga workflow tetap berjalan walau tanpa partitioning maupun machine learning.

---

## 🥼 **1. Data Preparation**

### ✔ Node yang digunakan:

* **CSV Reader**
  Mengimpor dataset Cereals.csv.

* **Missing Value**
  Mengatasi data kosong secara aman:

  * Numerik → *median*
  * Kategori → *most frequent*

* **Column Filter**
  Menghapus kolom tidak penting atau non-numerik.

* **Math Formula**
  Menghitung Heath Score

  ```
  health_score = fiber * 2 - sugars
  ```

---

## ⚙️ **2. Data Processing**

* **Normalizer**
  Menyamakan skala data numerik untuk visualisasi yang lebih jelas.

* **Rule Engine**
  Membuat label kategori kesehatan:

  ```
  calories < 100 => "HEALTHY"
  TRUE => "UNHEALTHY"
  ```

Label ini digunakan untuk bar chart & pie chart.

---

## 📊 **3. Visualisasi**

### 🔹 Scatter Plot

Membandingkan `Sugars` vs `Rating`.
Insight yang muncul:
* Semakin tinggi **gula**, biasanya **rating cenderung turun**.
  Konsumen tidak terlalu menyukai sereal yang terlalu manis.
* HEALTHY (kalori rendah) sering muncul di area gula rendah.

### 🔹 Histogram

Distribusi:
`Sugars`, `Calories`, dll.
* Histogram gula umumnya miring ke kanan → banyak sereal manis.
* Histogram kalori menunjukkan distribusi berat antara HEALTHY dan UNHEALTHY.
* Histogram fiber sering didominasi nilai rendah → banyak sereal rendah serat.

### 🔹 Bar Chart

Total HEALTHY vs UNHEALTHY.

* Biasanya kategori **UNHEALTHY** lebih banyak.
* Menunjukkan bahwa mayoritas sereal memiliki kalori di atas 100 per serving.
* Konsumen harus lebih selektif untuk memilih sereal rendah kalori.

### 🔹 Pie Chart

Proporsi visual kategori kesehatan.
* Pie chart mem visualisasikan persentase HEALTHY dan UNHEALTHY.
* Jika HEALTHY kecil → hanya sebagian kecil produk yang memenuhi standar rendah kalori.

---

## 🧩 **4. Klasifikasi (Rule Engine)**
Workflow menggunakan klasifikasi deterministik sederhana:

```
calories < 100 => "HEALTHY"
TRUE => "UNHEALTHY"
```

Kategori ini membantu memetakan produk sereal menjadi dua kelompok kesehatan.

Workflow ini menggunakan klasifikasi sederhana berbasis **Rule Engine**, bukan machine learning, sehingga:
✔ Tidak membutuhkan Partitioning
✔ Tidak memerlukan Decision Tree
✔ Cocok untuk pemula KNIME
✔ Tetap memenuhi poin “bonus: klasifikasi”

Kategori dibuat berdasarkan batas kesehatan sederhana (kalori).

---

## 📈 **5. Insight Utama**

Beberapa temuan dari analisis:

* Sereal dengan **kalori rendah (<100)** cenderung lebih sehat dan lebih disukai.
* Kadar gula memiliki pengaruh besar terhadap kualitas dan persepsi konsumen.
* Histogram menunjukkan sebagian besar sereal memiliki **kandungan gula cukup tinggi**.
* Scatter plot memperlihatkan hubungan terbalik antara **sugars** dan **rating**.
* Porsi HEALTHY lebih sedikit dibandingkan UNHEALTHY (tergantung dataset yang diunggah).

---

# 🏁 **6. Kesimpulan**

Berdasarkan seluruh analisis dan visualisasi:

**Mayoritas produk sereal di pasaran tidak termasuk kategori HEALTHY**, terutama karena kandungan kalori dan gula yang cukup tinggi.
Namun, masih ada sebagian produk yang lebih sehat—biasanya rendah kalori, rendah gula, dan memiliki sedikit serat tambahan.

Visualisasi scatter plot, histogram, bar chart, dan pie chart memperlihatkan bahwa **nutrisi memiliki pengaruh nyata terhadap persepsi konsumen**, terutama gula dan kalori.
Dengan workflow KNIME ini, pengguna dapat memahami pola nutrisi, mengelompokkan produk berdasarkan kesehatan, dan mendapatkan insight yang mudah untuk dipresentasikan atau digunakan dalam laporan.

---

