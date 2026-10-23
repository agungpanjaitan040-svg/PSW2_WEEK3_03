NAMA  :Agung Kristian PPanjaitan                      
NIM   : 41426012                       
KELAS : 41TRPL 1


## 1. Tujuan Praktikum
1. Menyusun kontrol dan label formulir secara tepat serta terstruktur sesuai standar semantik HTML.
2. Menerapkan validasi native HTML5 (required, min, max, step, pattern).
3. Menghubungkan petunjuk format ke kontrol input menggunakan atribut aksesibilitas (aria-describedby).
4. Mengatur dan menguji navigasi keyboard serta indikator fokus (:focus-visible).
5. Menguji perilaku formulir secara terarah melalui matriks uji kasus normal, batas, dan tidak valid.

---

## 2. Cara Menjalankan Proyek
1. Buka folder proyek pswi-week-03/sesi-03/ menggunakan *Visual Studio Code*.
2. Pastikan ekstensi *Live Server* telah terpasang di VS Code.
3. Klik kanan pada berkas index.html lalu pilih *Open with Live Server* (atau akses melalui URL lokal browser, misalnya http://127.0.0.1:5500/pswi-week-03/sesi-03/index.html).
4. Pastikan halaman dibuka melalui URL server lokal, bukan sekadar membuka file path file:///....

---

## 3. Matriks Hasil Pengujian

| Kasus Uji | Input yang Diuji | Harapan | Hasil Nyata (Browser) | Status (Lulus/Gagal) |
| :--- | :--- | :--- | :--- | :--- |
| *Email kosong* | "" | Ditolak karena required | Muncul tooltip validasi native wajib isi | Lulus |
| *Email abc* | abc | Ditolak karena bentuk email | Muncul peringatan native format email tidak valid (harus menyertakan tanda @) | Lulus |
| *Email contoh valid* | user@example.com | Diterima jika lainnya valid | Input valid dan formulir dapat diproses jika field lain sesuai | Lulus |
| *Jumlah 0 / 6* | 0 atau 6 | Ditolak | Ditolak oleh batasan min="1" / max="5" | Lulus |
| *Jumlah 1 / 5* | 1 atau 5 | Diterima | Diterima (berada dalam batas valid) | Lulus |
| *Jumlah 1.5* | 1.5 | Ditolak bila step=1 | Ditolak dengan pesan nilai harus kelipatan bilangan bulat (step="1") | Lulus |
| *Kode 12345* | 12345 | Ditolak | Ditolak oleh validasi pattern [0-9]{6} karena kurang dari 6 digit | Lulus |
| *Kode 001234* | 001234 | Diterima | Diterima, nilai nol di awal tetap dipertahankan | Lulus |
| *Keyboard Navigasi* | Tombol Tab, Shift+Tab, Space, Panah | Semua kontrol dapat dicapai secara logis tanpa mouse | Fokus berpindah secara berurutan, outline fokus terlihat jelas, dan tidak ada perangkap fokus | Lulus |

---

## 4. Jawaban Analisis dan Pertanyaan Modul

### 4.1. Perbedaan inputmode="numeric" dengan Validasi (pattern / type="number")
- inputmode="numeric" berfungsi sebagai instruksi bagi peramban (terutama pada keyboard virtual perangkat layar sentuh/mobile) untuk menampilkan keypad numerik saat elemen difokuskan. Atribut ini *tidak melakukan validasi data*, sehingga pengguna tetap dapat mengetik karakter non-angka melalui keyboard fisik.
- Validasi seperti pattern="[0-9]{6}" atau type="number" merupakan aturan validasi native browser yang secara aktif memverifikasi nilai input dan membatalkan pengiriman formulir (submit) jika formatnya tidak memenuhi kriteria.

### 4.2. Mengapa Server Tetap Perlu Memvalidasi (Eksperimen Penghapusan required)
Validasi di sisi klien (client-side validation) seperti atribut required atau pattern berjalan di peramban pengguna dan dapat dengan mudah dinonaktifkan, dihapus lewat DevTools (Inspect Element), atau dilewati sepenuhnya menggunakan alat seperti cURL atau Postman. Oleh sebab itu, server wajib melakukan validasi ulang (server-side validation) untuk memastikan integritas data, konsistensi sistem, serta mencegah potensi ancaman keamanan.

### 4.3. Catatan Audit Aksesibilitas
- *Label & Kontrol:* Seluruh kontrol formulir memiliki tag <label> yang terhubung secara eksplisit via atribut for ke id kontrol masing-masing.
- *Petunjuk Format:* Petunjuk format input terhubung langsung ke elemen kontrol melalui atribut aria-describedby="kode-help".
- *Indikator Fokus:* Menggunakan selector CSS :focus-visible dengan outline 3px solid #175cd3 dan outline-offset: 3px, serta tidak menggunakan nilai tabindex positif agar urutan tab tetap alami.
- *Aksesibilitas Gambar:* Gambar dilengkapi atribut alt yang informatif dan dikelompokkan menggunakan tag semantik <figure> dan <figcaption>.
- *Validasi HTML:* Dokumen diperiksa menggunakan Nu HTML Checker untuk memastikan struktur bebas dari duplikasi ID atau galat sintaksis.

---

## 5. Pernyataan Penggunaan AI (AI Use Statement)
- *Alat yang Digunakan:* Gemini
- *Tujuan Penggunaan:* Membantu menyusun dokumentasi pengujian, merapikan struktur Markdown, serta menyusun penjelasan konsep teknis perbedaan validasi native vs atribut inputmode.
- *Bagian yang Dibantu:* Format tabel matriks pengujian dan perumusan jawaban analisis modul.
- *Verifikasi Mandiri:* Seluruh instruksi, pengujian keyboard, atribut semantik, dan kode telah diverifikasi serta dijalankan secara manual pada browser lokal dan divalidasi dengan Nu HTML Checker.