
Jika Anda sudah mengikuti langkah-langkah di [Best Practice - Live Push (Praktik Terbaik - Push Langsung)](https://intl.cloud.tencent.com/document/product/267/31558), tetapi push tetap tidak berhasil, lakukan pemecahan masalah push umum sesuai dengan instruksi dalam dokumen ini.

### 1. Periksa rekaman CNAME yang mengarah ke alamat Tencent Cloud sudah dikonfigurasikan untuk nama domain Anda atau belum.
Push akan berhasil hanya jika nama domain Anda memiliki rekaman CNAME yang mengarah ke alamat Tencent Cloud. Anda dapat memeriksa apakah nama domain push yang ditambahkan memiliki rekaman CNAME atau tidak di kolom **CNAME** di **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain). Anda akan melihat tanda centang berwarna hijau jika rekaman CNAME telah dikonfigurasikan, seperti ditunjukkan oleh gambar di bawah ini:
![](https://main.qcloudimg.com/raw/ebb055071447bc55c2f17e60ab8d0b75.png)
Jika nama domain tidak memiliki rekaman CNAME, Anda dapat [mengonfigurasikannya](https://intl.cloud.tencent.com/zh/document/product/267/31057).
	

### 2. Pastikan kondisi jaringan normal.
Push RTMP menggunakan port **1935** secara default. Jika port tersebut tidak diaktifkan di firewall jaringan untuk pengujian, Anda tidak akan dapat tersambung ke server. Anda dapat memeriksa mungkin atau tidaknya masalah ini menyebabkan kegagalan push dengan beralih ke jaringan lain (misalnya jaringan 4G).

### 3. Periksa kemungkinan masa berlaku URL push terlalu singkat.
Agar lalu lintas tidak dicuri, beberapa klien mungkin mengatur `txTime` (masa berlaku URL push) ke periode yang sangat singkat, misalnya 5 menit dari waktu saat ini. Cara tersebut tidak perlu dilakukan karena tanda tangan `txSercet` telah menjamin keamanan. Jika masa berlaku terlalu singkat, URL push dapat kedaluwarsa setelah streaming langsung mengalami interupsi karena jaringan terputus sehingga push tidak dapat dilanjutkan.
Sebaiknya atur `txTime` ke 12 atau 24 jam dari waktu saat ini, atau lebih lama dari sesi streaming langsung biasa.

### 4. Pastikan `txSecret` sudah benar.
Untuk memastikan keamanan, Tencent Cloud mengharuskan konfigurasi perlindungan hotlink untuk semua URL push dan **menolak** semua URL perlindungan hotlink yang telah kedaluwarsa atau yang tidak dihitung dengan benar. Jika push ditolak, SDK CSS akan mengirimkan peristiwa **PUSH_WARNING_SERVER_DISCONNECT**.
![](https://main.qcloudimg.com/raw/00c846dda473ee0dd241ffe89554849b.jpg)
Lihat [Best Practice > Live Push (Praktik Terbaik > Push Langsung)](https://intl.cloud.tencent.com/document/product/267/31558) untuk mempelajari cara mendapatkan URL push yang andal.

### 5. Periksa kemungkinan URL push sudah digunakan.
URL push dapat digunakan oleh satu klien saja dalam satu waktu. Klien kedua yang mencoba melakukan push menggunakan URL tersebut akan ditolak oleh Tencent Cloud. Anda dapat login ke konsol CSS dan memeriksa push sudah dilakukan pada streaming tertentu atau belum di **[Stream Management](https://console.cloud.tencent.com/live/streammanage)** > **Live Streams** (Manajemen Streaming > Streaming Langsung). Anda juga dapat memeriksa kemungkinan streaming dinonaktifkan di **Disabled Streams** (Streaming Dinonaktifkan).

 
