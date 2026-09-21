# Tugas 1 — Analisis Pitfall FoodGo

**Kelompok:** [nama kelompok]

| Nama | NIM | Kontribusi |
|---|---|---|
| Mohammad Rayhan Pakaya | 103072400037 | [pitfall/bagian yang dikerjakan] |
| Putra Paramartha Suratinoyo | 103072400022 | [pitfall/bagian yang dikerjakan] |
| [nama 3] | [nim] | [pitfall/bagian yang dikerjakan] |

## Pitfall 1: [The Network is Reliable — ditulis oleh [Putra P Suratinoyo]

**Bukti di skenario:** Tim menemukan bahwa kode mereka menulis asumsi seperti # network is always reliable, no need for retry dan tidak ada timeout sama sekali pada pemanggilan antar service (modul pesananan pembayaran dan menunggu tanpa batas waktu ).

**Kenapa ini keliru:** Dalam sistem terdistribusi nyata,jaringan komputer tidak pernah 100% andal.Data di kirim melewati kabel,router dan internet publik (atau jaringan cloud internal). Selalu ada risiko paket data hilang (packet loss), gangguan koneksi fisik,atau server tujuan (seperti sistem pembayaran pihak ketiga) mendadak down atau kelebihan beban (overloaded)

**Dampak ke FoodGo:** Ketika Traffic melonjak saat jam makan siang,pembayaran melambat akibat jaringan yang padat.karena modul pesananan tidak memiliki batasan waktu,modul pesanana akan mengggantung dan menunggu jawaban selamanya.hal ini menahan thread dan memori server utama.Karena antrean pesanan baru terus masuk,server kehabisan sumber daya komputasi hingga akhir nya backend crash total

**Solusi desain awal:** menerapkan batas waktu tunggu maksimal pada setiap pemanggilan jaringan.selain itu,buat kebijakan percobaan kembali otomatis menggunkan metode exponential Backoff debgan jitter.artinya,jika koneksi gagal atau lambat,sistem akan mencoba lagi dengan memberikan jeda waktu tunggu yang semakin lama dan acak,agar tidak membebani jaringan

**Trade-off:* solusi retry tidak lah gratis.jika modul pembayaran eksternal memang sedang mati total,melakukan retry terus-menerus dari ribuan pesananan yang masuk justru akan menciptakan badai permintaan baru (retry storm)> Hal ini akan memperparah beban jaringan dan memastikan server tujuan semakin sulit untuk pulih (cascadin failure)
---

## Pitfall 2: [nama pitfall] — ditulis oleh [nama]

(ulangi struktur di atas)

---

## Pitfall 3: [nama pitfall] — ditulis oleh [nama]

(ulangi struktur di atas)

---

## Kesimpulan Kelompok

[Ringkasan: jika FoodGo memperbaiki ketiga pitfall ini, apa arsitektur yang disarankan secara garis besar? Kaitkan dengan Tugas 2.]
