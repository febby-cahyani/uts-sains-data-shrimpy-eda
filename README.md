# Tindak Lanjut EDA Citra Udang Vaname — UTS Sains Data

**Febby Cahyani | NRP 1226800016**  
S2 Teknik Informatika dan Komputer, Politeknik Elektronika Negeri Surabaya (PENS)  
Mata kuliah: Sains Data — Semester Gasal 2026/2027

> Repositori pendamping laporan UTS **Tindak Lanjut Exploratory Data Analysis (EDA)**. Penelitian berfokus pada evaluasi kualitas dataset citra udang vaname sebagai persiapan sistem pengukuran panjang non-invasif. Analisis ini **belum** merupakan evaluasi akurasi panjang dalam sentimeter maupun performa YOLO-Seg.

**Laporan dan arsip keluaran lengkap:** [Google Drive] https://drive.google.com/drive/folders/1y4b8VkfKfQbg0u-FkJsgDavAZ0kAZc_7?usp=drive_link  

## 1. Latar belakang dan data

Analisis merupakan kelanjutan dari presentasi EDA sebelumnya. Dataset baseline air jernih **0,5 NTU** mencakup **187.100 frame** dari **240 kombinasi rancangan** (3 kelas ukuran × 8 warna alas × 2 posisi lampu × 5 PWM). Kelas ukuran: Small (4–7 cm), Medium (8–10 cm), dan Large (11–15 cm). Sebanyak **117.613 frame (62,9%)** memiliki label polygon VIA JSON; **69.487 frame (37,1%)** belum berlabel. Jumlah kondisi yang dapat dianalisis untuk setiap hipotesis bisa lebih sedikit karena persyaratan kelengkapan data.

## 2. Pertanyaan dan metode

| Bagian | Analisis | Keluaran utama |
|---|---|---|
| A | Menghubungkan temuan EDA, bukti, keputusan, dan alasan | Laporan UTS |
| B | Audit missing label, outlier, resolusi, autokorelasi, transformasi, split per kondisi | `B_*.csv`, `B_*.png`, `02_*.csv` |
| C/H1 | Perbedaan luas bounding box relatif antar kelas; Kruskal–Wallis dan uji lanjutan | `C_hasil_uji.csv`, `C_H1_median_per_kelas.png` |
| C/H2 | Perbedaan ketajaman citra lampu Bawah vs Atas; Wilcoxon berpasangan | `C_H2_selisih_berpasangan.png` |
| C/H3 | Ekuivalensi luas box relatif antar posisi lampu, margin utama ±10% | `C_H3_ekuivalensi.png` |
| D | Skenario sensitivitas, margin ekuivalensi, pseudoreplikasi | `D_*.csv`, `D_*.png` |

Unit analisis utama adalah **kondisi akuisisi**, bukan setiap frame secara independen, untuk mengurangi risiko pseudoreplikasi akibat frame berurutan.

## 3. Ringkasan hasil pada data penelitian

- **H1:** Kruskal–Wallis pada 188 kondisi, H=152,658; p≈7,09×10⁻³⁴; epsilon-kuadrat≈0,814. Luas box relatif berbeda antarkelas.
- **H2:** 120 pasangan kondisi; median rasio skor ketajaman lampu Bawah/Atas≈3,578 pada skor mentah dan ≈2,176 setelah normalisasi kecerahan.
- **H3:** rasio luas box relatif≈1,024; ekuivalensi terdukung untuk margin **±10%**, tetapi **tidak** untuk margin **±5%**.
- Analisis sensitivitas S0–S6 tidak mengubah kesimpulan utama pada konfigurasi yang diuji.

Hasil tersebut bersifat **statistik karakteristik citra**, bukan bukti bahwa lampu Bawah menghasilkan estimasi panjang udang yang lebih akurat.

## 4. Data, batasan, dan reproduksibilitas

Dataset mentah (citra/video dan anotasi) **tidak disertakan secara publik** dalam repositori ini. Keluaran ringkas dapat dibagikan melalui `outputs/`; CSV berukuran besar, arsip lengkap, dan dokumen pengumpulan dapat diletakkan di [Google Drive] https://drive.google.com/drive/folders/1y4b8VkfKfQbg0u-FkJsgDavAZ0kAZc_7?usp=drive_link , sesuai izin akses dataset. `--demo` hanya memeriksa eksekusi pada data sintetis, tidak memvalidasi angka hasil penelitian.
