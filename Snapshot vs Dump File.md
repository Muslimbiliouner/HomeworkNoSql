# 📄 Snapshot vs Dump File: Panduan Lengkap

Dalam dunia manajemen basis data, **Snapshot** dan **Dump File** adalah dua metode utama untuk mencadangkan dan memulihkan data. Keduanya memiliki tujuan yang sama, yaitu melindungi data, tetapi berbeda dalam cara kerja, kecepatan, dan aplikasi. Dokumentasi ini menjelaskan secara mendalam perbedaan, kelebihan, kekurangan, dan kapan masing-masing metode digunakan.

---

## **1. Snapshot**

### 📌 **Definisi**
Snapshot adalah salinan seluruh sistem basis data pada titik waktu tertentu. Snapshot ini biasanya diambil di tingkat sistem file atau penyimpanan dan mencerminkan kondisi data saat snapshot dibuat (**point-in-time**).

### ⚙️ **Cara Kerja**
- Snapshot dibuat menggunakan teknologi penyimpanan, seperti:
  - **LVM (Logical Volume Manager)**.
  - **VMware Snapshots**.
- **Teknologi Copy-on-Write** sering digunakan, di mana hanya perubahan setelah snapshot yang disimpan.

### ✅ **Kelebihan**
1. **Kecepatan**: Snapshot dibuat sangat cepat karena tidak perlu menyalin seluruh data.
2. **Minimal Downtime**: Basis data tetap berjalan selama proses snapshot.
3. **Efisiensi Penyimpanan**: Hanya data yang berubah disimpan (copy-on-write).

### ❌ **Kekurangan**
1. **Ketergantungan Teknologi**: Bergantung pada perangkat keras atau perangkat lunak penyimpanan tertentu.
2. **Bukan Salinan Independen**: Tidak mudah dipindahkan ke lokasi lain.

### 🛠️ **Kapan Menggunakan?**
- **Backup Cepat**: Ketika waktu menjadi faktor penting.
- **Pemulihan Lokal**: Untuk rollback cepat pada sistem yang sama.

---

## **2. Dump File**

### 📌 **Definisi**
Dump file adalah salinan data basis data yang diekspor dalam format yang dapat dibaca dan dipulihkan, seperti **SQL script** atau **file biner**. Dump mencakup data dan struktur basis data untuk rekonstruksi di sistem lain.

### ⚙️ **Cara Kerja**
- Basis data menggunakan alat bawaan seperti:
  - `pg_dump` untuk PostgreSQL.
  - `mysqldump` untuk MySQL.
- Data diekspor dalam format SQL (teks) atau biner.

### ✅ **Kelebihan**
1. **Portabilitas**: Mudah dipindahkan antar server atau sistem.
2. **Independen**: Tidak terikat pada perangkat keras atau perangkat lunak tertentu.
3. **Granularitas**: Bisa mencadangkan seluruh basis data, tabel tertentu, atau subset data.

### ❌ **Kekurangan**
1. **Lambat**: Proses ekspor bisa memakan waktu, terutama untuk basis data besar.
2. **Downtime**: Bisa memerlukan penghentian sementara untuk menghindari inkonsistensi.

### 🛠️ **Kapan Menggunakan?**
- **Migrasi Basis Data**: Ideal untuk memindahkan basis data antar server atau platform.
- **Cadangan Jangka Panjang**: Cocok untuk arsip yang membutuhkan format portabel.

---

## **3. Perbandingan Snapshot dan Dump File**

| **Aspek**                | **Snapshot**                             | **Dump File**                            |
|--------------------------|------------------------------------------|------------------------------------------|
| **Tingkat Operasi**      | Sistem file atau penyimpanan blok.       | Basis data langsung.                     |
| **Kecepatan**            | Sangat cepat.                            | Relatif lambat, tergantung ukuran data.  |
| **Ketergantungan**       | Bergantung pada teknologi penyimpanan.   | Independen dari perangkat keras/software.|
| **Format**               | Format internal penyimpanan blok.        | Format SQL atau biner.                   |
| **Portabilitas**         | Rendah (sulit dipindahkan).              | Tinggi (mudah dipindahkan).              |
| **Konsistensi**          | Tergantung pada teknologi snapshot.      | Konsisten jika diatur dengan benar.      |
| **Penggunaan Umum**      | Pemulihan cepat pada sistem yang sama.   | Migrasi atau backup arsip.               |

---

## **4. Kesimpulan**

**Snapshot** dan **Dump File** memiliki aplikasi yang berbeda sesuai dengan kebutuhan MegaShop atau skenario backup:

1. **Snapshot**:
   - Cocok untuk **backup cepat** dan **pemulihan lokal**.
   - Ideal untuk rollback dalam sistem yang sama.

2. **Dump File**:
   - Cocok untuk **migrasi basis data** atau **cadangan jangka panjang**.
   - Formatnya portabel dan dapat digunakan di platform yang berbeda.

MegaShop dapat memanfaatkan kedua metode ini secara bersamaan:
- Gunakan **snapshot** untuk pemulihan cepat dan backup harian.
- Gunakan **dump file** untuk migrasi data ke sistem baru, termasuk ke NoSQL.

Dengan memilih metode yang sesuai, MegaShop dapat melindungi data mereka sekaligus mendukung transisi ke arsitektur basis data modern.
