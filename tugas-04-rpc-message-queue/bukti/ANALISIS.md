# Analisis 
## Mengapa RPC cocok dengan skenario yang kalian pilih di kasus ini?
RPC (Remote Procedure Call) cocok untuk kasus FoodGo karena memungkinkan modul Pembayaran dan modul Pesanan berkomunikasi dan memanggil fungsi satu sama lain melalui jaringan. RPC memungkinkan modul Pesanan memanggil fungsi pada modul Pembayaran dan menunggu hasilnya.

- Memeriksa saldo pengguna.
- Memvalidasi status pembayaran.
- Memastikan pembayaran berhasil sebelum pesanan diproses lebih lanjut.

