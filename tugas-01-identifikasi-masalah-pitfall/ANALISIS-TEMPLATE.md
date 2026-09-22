# Tugas 1 — Analisis Pitfall FoodGo

**Kelompok:** [nama kelompok]

| Nama | NIM | Kontribusi |
|---|---|---|
| Mohammad Rayhan Pakaya | 103072400037 | [pitfall/bagian yang dikerjakan] |
| Putra Paramartha Suratinoyo | 103072400022 | [pitfall/Network is reliable] |
| [nama 3] | [nim] | [pitfall/bagian yang dikerjakan] |

## Pitfall 1: [The Network is Reliable — ditulis oleh [Putra P Suratinoyo]

**Bukti di skenario:** Tim menemukan bahwa kode mereka menulis asumsi seperti # network is always reliable, no need for retry dan tidak ada timeout sama sekali pada pemanggilan antar service (modul pesananan pembayaran dan menunggu tanpa batas waktu ).

**Kenapa ini keliru:** Dalam sistem terdistribusi nyata,jaringan komputer tidak pernah 100% andal.Data di kirim melewati kabel,router dan internet publik (atau jaringan cloud internal). Selalu ada risiko paket data hilang (packet loss), gangguan koneksi fisik,atau server tujuan (seperti sistem pembayaran pihak ketiga) mendadak down atau kelebihan beban seperti overload 

**Dampak ke FoodGo:** ketika jam makan siang traffic melonjak naik akibat pembayaran melambat dan jaringan yang padat.karena modul pesanan tidak memiliki  batasan waktu,
modul akan menggantung dan menungggu jawaban selamanya hal ini,menahan thread dan memori server utama karena lonjakan trafic lonjakan pas jam makan siang terus masuk ke server.akibat nya server kehabisan sumber daya dan akhir nya backend crash total

**Solusi desain awal:** mungkin saya bakalan memakai batas waktu tunggu maksimal pada setiap pemanggilan jaringan.seperti menggunkan metode exponential Backoff dengan jitter
agar koneksi gagal atau lambat,sistem akan mencoba lagi dengan memberikan jeda waktu tunggu yang semakin lama dan acak,agar tidak membebani jaringan dan nge buat backend crash total

**Trade-off:* bakalan mati total dan menjadi senjata makan tuan 
---

## Pitfall 2: [Monolithic Single Point of Failure] — ditulis oleh [Rayhan]

**Bukti di skenario:** satu server yang menangani semua modul (pesanan, pembayaran, notifikasi kurir) kewalahan karena semuanya berjalan di satu proses monolitik yang sama.

**Kenapa ini keliru:** Dikarenakan semua modul harus berbagi CPU, RAM, thread pool, dan network I/O. Saat Traffic tinggi, ada modul yang tidak kebagian sumber daya.

**Dampak ke FoodGo:** hal ini menyebabkan jika ada 1 saja modul yang terjadi crash, maka seluruh aplikasi foodgo akan terjadi crash 

**Solusi desain awal:** Menambah server untuk membuat Server Cluster agar aplikasi terhindar dari 
downtime dan kehilangan data saat server mengalami crash saat High Traffic

**Trade-off:** Biaya untuk Menambah Server 

## Pitfall 3: [nama pitfall] — ditulis oleh [nama]

(ulangi struktur di atas)

---

## Kesimpulan Kelompok

[Ringkasan: jika FoodGo memperbaiki ketiga pitfall ini, apa arsitektur yang disarankan secara garis besar? Kaitkan dengan Tugas 2.]
