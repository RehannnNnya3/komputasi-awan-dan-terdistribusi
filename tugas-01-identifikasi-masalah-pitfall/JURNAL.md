# Jurnal Proses — Tugas 1

> Isi jurnal ini selama proses diskusi berlangsung, bukan ditulis ulang rapi di akhir. Tulis dengan gaya bebas — poin diskusi, kebuntuan, perubahan pikiran.

## 21/09/2026
- Peserta: Artha, Rayhan
- Poin diskusi: Menganalisis Pitfall di studi kasus
- Perbedaan pendapat (jika ada): ...

## [Tanggal diskusi 2]
- Peserta: Artha, Rayhan
- Poin diskusi: Memperbaiki hasil analisis Pitfall yang sudah ada
- Perbedaan pendapat (jika ada): ...

## Review Silang
- [Nama] mengomentari analisis [Nama lain]: ...

## Log Penggunaan AI (Level 2)

> Wajib diisi sesuai kebijakan Level 2 di [`../RUBRIK-UMUM.md`](../RUBRIK-UMUM.md). Tulis "Tidak memakai AI" pada baris pertama jika memang tidak dipakai. Hanya untuk brainstorming ide/outline — bukan untuk kode/analisis/teks akhir.

| Tanggal | Tool AI | Prompt yang diberikan | Ringkasan saran/ide AI | Bagaimana diolah jadi tulisan/kode sendiri |
|---|---|---|---|---|
| 21 | ... | ... | ... | ... |
| 22 | Gemini | untuk pitfall monolitik, apakah penyelesaian nya itu harus menggunakan micro service agar semua nya itu tidak berjalan di modul yang sama? mengingat aplikasi foodgo itu aplikasi raksasa yang handle ribuan pesanan, pembayaran, notifikasi kurir | aplikasi berukuran besar seperti FoodGo, solusi utamanya bukan sekadar "pakai Microservices", melainkan: - Menambahkan Horizontal Scaling (Auto-Scaling) di balik Load Balancer.Menggunakan Asynchronous Task Queue / Message Broker untuk tugas-tugas non-blocking (seperti notifikasi kurir). - Menerapkan Timeout, Circuit Breaker, dan Retry Policy pada komunikasi eksternal/antar-layanan. | Untuk aplikasi foodgo yang berskala besar, solusinya tidak langsung memakai microservices. Lebih utama untuk implementasi Auto-Scalling, Broker Untuk proses latar belakang yang non-blocking.  |
