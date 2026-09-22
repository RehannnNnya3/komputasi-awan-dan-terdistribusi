# Jurnal Proses — Tugas 1

> Isi jurnal ini selama proses diskusi berlangsung, bukan ditulis ulang rapi di akhir. Tulis dengan gaya bebas — poin diskusi, kebuntuan, perubahan pikiran.

## 21/09/2026
- Peserta: Artha, Rayhan
- Poin diskusi: Menganalisis Pitfall di studi kasus
- Perbedaan pendapat (jika ada): ...

## 22/09/2026
- Peserta: Artha, Rayhan
- Poin diskusi: Memperbaiki hasil analisis Pitfall yang sudah ada
- Perbedaan pendapat (jika ada): ...

## Review Silang
- [Nama] mengomentari analisis [Nama lain]: ...

## Log Penggunaan AI (Level 2)

> Wajib diisi sesuai kebijakan Level 2 di [`../RUBRIK-UMUM.md`](../RUBRIK-UMUM.md). Tulis "Tidak memakai AI" pada baris pertama jika memang tidak dipakai. Hanya untuk brainstorming ide/outline — bukan untuk kode/analisis/teks akhir.

| Tanggal | Tool AI | Prompt yang diberikan | Ringkasan saran/ide AI | Bagaimana diolah jadi tulisan/kode sendiri |
|---|---|---|---|---|
| 21 | Gemini | Di dalam kode awal FoodGo, tertulis komentar # network is always reliable, no need for retry tanpa adanya pembatas waktu (timeout). Asumsi ini sangat berbahaya di dunia nyata. Komunikasi antar-layanan (seperti dari modul pesanan ke modul pembayaran bank) itu lewat kabel internet, bukan di dalam satu komputer. Ketika jam makan siang, jaringan internet luar bisa saja macet atau server bank eksternal sedang lelet. Karena tidak ada timeout, sistem FoodGo akan terus 'bengong' menunggu balasan yang tidak pasti. Akibatnya, memori server penuh oleh antrean pesanan yang menggantung, server macet total (freeze), dan tim IT terpaksa melakukan restart server secara manual | Untuk mengatasi masalah ini, kita harus menghapus asumsi keliru tersebut dari kode FoodGo dan memasang batas waktu tunggu (Timeout), misalnya maksimal 5 detik. Jika dalam waktu 5 detik modul pembayaran bank eksternal tidak memberikan respons, sistem FoodGo harus memutus koneksi secara paksa demi menyelamatkan server agar tidak "bengong". Selain itu, kita perlu menambahkan sistem coba ulang otomatis (Retry Policy) yang pintar menggunakan metode Exponential Backoff. Jadi, jika koneksi gagal, sistem tidak langsung menyerah tetapi mencoba menghubungi kembali dengan memberikan jeda waktu tunggu yang semakin lama (misalnya percobaan pertama menunggu 1 detik, kedua 2 detik, ketiga 4 detik) agar server bank yang sedang sibuk punya waktu untuk bernapas | Dalam sistem terdistribusi nyata,jaringan komputer tidak pernah 100% andal.Data di kirim melewati kabel,router dan internet publik (atau jaringan cloud internal). Selalu ada risiko paket data hilang (packet loss), gangguan koneksi fisik,atau tujuan server (seperti sistem pembayaran pihak ketiga) tiba-tiba down atau kelebihan beban seperti kelebihan beban |
| 22 | Gemini | untuk pitfall monolitik, apakah penyelesaian nya itu harus menggunakan micro service agar semua nya itu tidak berjalan di modul yang sama? mengingat aplikasi foodgo itu aplikasi raksasa yang handle ribuan pesanan, pembayaran, notifikasi kurir | aplikasi berukuran besar seperti FoodGo, solusi utamanya bukan sekadar "pakai Microservices", melainkan: - Menambahkan Horizontal Scaling (Auto-Scaling) di balik Load Balancer.Menggunakan Asynchronous Task Queue / Message Broker untuk tugas-tugas non-blocking (seperti notifikasi kurir). - Menerapkan Timeout, Circuit Breaker, dan Retry Policy pada komunikasi eksternal/antar-layanan. | Untuk aplikasi foodgo yang berskala besar, solusinya tidzak langsung memakai microservices. Lebih utama untuk implementasi Auto-Scalling, Broker Untuk proses latar belakang yang non-blocking.  |
| 22 | Gemini | Untuk pitfall Lack of Self-Healing, apakah penyelesaiannya harus selalu menggunakan teknologi kompleks seperti Kubernetes agar server bisa pulih otomatis saat crash? Mengingat FoodGo adalah aplikasi raksasa yang menghandle ribuan transaksi tetapi tim IT-nya masih berskala startup | Jika server FoodGo crash bukan karena lonjakan pengguna, melainkan karena ada bug fatal pada baris kode atau database utama yang rusak, sistem self-healing akan terjebak. Sistem akan terus-menerus mematikan dan menghidupkan server secara agresif tanpa henti karena setiap kali server hidup, kode yang rusak akan langsung membuatnya mati lagi.Dampak buruknya adalah akar masalah yang sebenarnya akan tersamarkan pada dasbor pemantauan, dan proses hidup-mati server yang terlalu sering di tengah jam sibuk berisiko membuat data transaksi yang sedang ditulis ke database menjadi rusak (corrupt) | Mengandalkan manusia (tim IT) untuk buru-buru buka laptop dan ketik perintah restart saat server mati adalah pola pikir yang kuno di era cloud. Server di cloud itu bisa tumbang kapan saja karena kehabisan RAM atau kodenya macet. Kalau kita cuma mengandalkan cara manual, aplikasi akan kelamaan mati (down) karena kita harus menunggu sampai ada tim IT yang sadar, bangun tengah malam, lalu masuk ke sistem untuk membetulkannya
 |
