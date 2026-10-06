# Jurnal Proses — Tugas 3

## Percobaan tanpa Lock
- Hasil `processed_count` yang didapat: 0 (seharusnya 100)
- Kenapa bisa meleset (jelaskan mekanisme race condition dengan kata sendiri): operasi increment seperti processed_count += 1 di Python bukanlah operasi tunggal yang instan (atomic operation), melainkan terdiri dari 3 langkah utama di tingkat mesin/CPU. Ketika ada banyak thread yang berjalan secara bersamaan (concurrently), urutan eksekusi langkah di atas bisa saling bertabrakan. Dampaknya, dua pesanan telah diproses oleh dua thread berbeda, tetapi counter hanya bertambah 1 angka saja (dari 10 menjadi 11, bukan 12). Hasil increment dari Thread A tertimpa oleh Thread B (lost update).

## Percobaan dengan Lock
- Hasil `processed_count` setelah perbaikan: 100 (seharusnya 100)

## Kendala Docker
- Error yang ditemui saat `docker build`/`docker run` dan cara memperbaikinya: pertama, menyalakan Virtual Machine Platform di ternminal Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform. kedua, install Windows subsystem for linux di ternminal wsl --install.

## Log Penggunaan AI (Level 2)

> Wajib diisi sesuai kebijakan Level 2 di [`../RUBRIK-UMUM.md`](../RUBRIK-UMUM.md). Tulis "Tidak memakai AI" pada baris pertama jika memang tidak dipakai. Hanya untuk brainstorming ide/outline — bukan untuk kode/analisis/teks akhir.

| Tanggal | Tool AI | Prompt yang diberikan | Ringkasan saran/ide AI | Bagaimana diolah jadi tulisan/kode sendiri |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |
