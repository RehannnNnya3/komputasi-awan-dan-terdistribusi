# Jurnal Proses — Tugas 2

  | Nama | NIM | Kontribusi |
  |---|---|---|
  | Moh Rayhan Pakaya | 103072400037 | Mengisi Jurnal AI dan menganalisis arsitektur yang cocok |
  | Putra Paramartha S | 103072400022 | membuat flow diagram dan  |

## [Tanggal] 28
- Opsi arsitektur yang dipertimbangkan: Kombinasi SOA dan Public-subsribe 
- Kenapa akhirnya pilih SOA/Pub-Sub: Karena kelebihannya diantaranya SOA untuk Pemisahan Jalur Kritis dan Non-Kritis, Pub-sub untuk menghindari matinya salah satu modul tidak akan menyebabkan timeout
- Revisi diagram (versi 1 → versi 2, apa yang berubah dan kenapa): ...

## Log Penggunaan AI (Level 2)

> Wajib diisi sesuai kebijakan Level 2 di [`../RUBRIK-UMUM.md`](../RUBRIK-UMUM.md). Tulis "Tidak memakai AI" pada baris pertama jika memang tidak dipakai. Hanya untuk brainstorming ide/outline — bukan untuk kode/analisis/teks akhir.

| Tanggal | Tool AI | Prompt yang diberikan | Ringkasan saran/ide AI | Bagaimana diolah jadi tulisan/kode sendiri |
|---|---|---|---|---|
| 28 | Gemini | Apakah arsitektur SOA dan public subscribe bisa digunakan bersamaan ? | kombinasi keduanya sangat efektif dan umum digunakan. SOA digunakan untuk jalur kritis yang butuh respon instan (sinkron), seperti validasi menu ke Katalog Resto dan pemotongan saldo. Sedangkan Pub-Sub (via Message Broker) digunakan untuk jalur asinkron, seperti notifikasi koki dan pencarian kurir, sehingga modul-modul ini *decoupled* dan tidak membuat aplikasi *crash* jika salah satunya lambat. | konsep pembagian ini sebagai landasan untuk menggambar diagram arsitektur. Interaksi Modul Pesanan dengan Katalog dan Pembayaran saya buat sinkron (SOA), lalu saya menambahkan Message Broker setelah pembayaran sukses agar Modul Kurir dan Resto bisa bekerja secara asinkron (Pub-Sub). Penjelasan dari AI saya parafrase menggunakan kata-kata sendiri untuk mengisi bagian justifikasi pemilihan kombinasi arsitektur di bagian atas jurnal. |
| ... | Gemini | Apa tugas masing masing kombinasi arsitektur SOA dan Public-subscribe? | - SOA (komunikasi berbasis request-response seperti REST API) digunakan untuk proses yang membutuhkan validasi instan sebelum pengguna bisa lanjut ke tahap selanjutnya setelah pesanan pengguna dipastikan sah dan sudah dibayar. - Public-subscribe digunakan untuk proses yang bisa berjalan di latar belakang tanpa mengharuskan pengguna menunggu di loading screen| SOA berfungsi untuk mevalidasi katalog resto (cek menut dan ketersediaan stok) dan modul pembayaran (memotong saldo pengguna). Sedangkan Public-subscribe digunakan untuk mengirim pesan "Pesanan Berhasil" ke message broker lalu mengirim notifikasi ke driver dan Resto yang dituju pengguna |
