CSS dapat mengambil tangkapan layar streaming langsung dan menyimpannya dalam COS. Penggunaan fitur pengambilan tangkapan layar akan dikenai biaya, yang ditagih **berdasarkan jumlah total tangkapan layar yang diambil selama bulan terkait**.

### Catatan

- Pengambilan tangkapan layar dinonaktifkan secara default dan dapat diaktifkan di konsol atau melalui API cloud.
- Tangkapan layar yang dihasilkan disimpan di COS dan akan dikenai biaya penyimpanan COS. Untuk informasi selengkapnya, silakan pelajari [COS Pricing (Harga COS)](https://intl.cloud.tencent.com/pricing/cos).
- Pengambilan tangkapan layar merupakan fitur berbayar. **Sebanyak 1.000 tangkapan layar pertama setiap bulan tidak dikenai biaya. Biaya akan dikenakan untuk tangkapan layar yang diambil setelahnya**.



### Harga

| Tangkapan layar | Harga (USD/Ribu tangkapan layar) | Catatan |
| -------- | ----------------- | ------------------------ |
| ≤ 1000 |0 | Sebanyak 1.000 tangkapan layar pertama setiap bulan tidak dikenai biaya |
|＞ 1000|0,0176| Jumlah total tangkapan layar akan dibulatkan ke atas hingga 1.000 terdekat |

### Ikhtisar Penagihan

- Item yang dapat dikenai tagihan: jumlah tangkapan layar.
- Mode penagihan: bayar sesuai pemakaian.
- Siklus penagihan: siklus penagihan bulanan. Tagihan bulan berjalan akan dibuat antara tanggal 1 dan 5 bulan berikutnya. Silakan baca laporan penagihan aktual Anda untuk keterangan detail.
- Aturan penagihan: biaya dihitung dengan mengalikan total jumlah tangkapan layar yang diambil dalam suatu bulan dan harga unit.



### Contoh Penagihan

Misalnya, Anda menggunakan layanan pengambilan tangkapan layar dari tanggal 1 Januari hingga 1 Februari 2021, dan total 168.000 tangkapan layar dihasilkan selama bulan tersebut. Jadi, biaya pengambilan tangkapan layar langsung yang harus Anda bayar pada tanggal 2 Februari 2021 adalah sebagai berikut:
Biaya pengambilan tangkapan layar langsung untuk Januari = 0,0176 (USD/Ribu tangkapan layar) × (168 - 1) Ribu tangkapan layar = 2,9392 USD.