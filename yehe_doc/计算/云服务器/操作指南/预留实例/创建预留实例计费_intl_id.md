## Ikhtisar

Instans Cadangan (RI) memberikan diskon untuk instans bayar sesuai pemakaian. Dokumen ini menjelaskan cara membuat RI melalui konsol.

## Prasyarat
Saat ini, RI hanya ditawarkan kepada pengguna beta. Untuk menggunakannya, buka halaman aplikasi beta RI dan [kirim aplikasi](https://intl.cloud.tencent.com/apply/p/bvrqmrrp5ns) untuk menjadi pengguna beta.

## Petunjuk
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. Klik **Reserved Instance** (Instans Cadangan) di bilah sisi kiri untuk masuk ke halaman pengelolaan.
3. Klik **Create Reserve Instance** (Buat Instans Cadangan) untuk membeli RI.

![image-20200909172355330](https://main.qcloudimg.com/raw/f604c27f8faeded74797d78d66ada9c2.png)

4. Konfigurasi informasi berikut seperti yang diminta oleh halaman:

| Parameter | Wajib/Opsional | Deskripsi |
| ------------------ | --------- | ------------------------------------------------------------ |
| Wilayah/Zona Ketersediaan | Wajib | Wilayah dan zona ketersediaan tempat instans bayar sesuai pemakaian yang cocok berada.           |
| Sistem Operasi | Wajib | Windows、OS Linux.                                    |
| Masa Berlaku | Wajib | Jangka Waktu RI: 1 tahun.                    |
| Instans | Wajib | Jenis instans bayar sesuai pemakaian yang ingin Anda cocokkan dengan RI.</br>Instans bayar sesuai pemakaian ini harus sama persis dengan atribut RI untuk mendapatkan keuntungan dari diskon penagihan selama jangka waktu RI.  |
| Nama RI | Opsional | Ditetapkan pengguna. <li> Nama RI diatur secara default ke “unnamed” (belum diberi nama) jika parameter ini dibiarkan kosong.</li>  <li> Anda dapat memasukkan nama apa pun dalam 60 karakter.</li> |
| Mode Penagihan | Wajib | Pilih opsi penagihan sesuai kebutuhan:</br> <ul><li>**All Upfront** (Semua di Muka): Anda membayar seluruh jangka waktu RI dengan satu pembayaran di muka. Opsi ini memberi Anda diskon terbesar dibandingkan dengan dua opsi lainnya di bawah ini.</li><li>**Partial Upfront** (Sebagian Di Muka): Anda melakukan pembayaran di muka yang rendah dan kemudian membayar biaya instans dengan tarif bulanan atau tarif per jam yang didiskon selama jangka waktu RI. </li> <li>**No Upfront** (Tanpa Uang Muka): Anda tidak melakukan pembayaran di muka, lalu membayar biaya instans dengan tarif bulanan atau tarif per jam yang didiskon selama jangka waktu RI. Untuk informasi selengkapnya tentang harga, lihat [Mode Penagihan Instans Cadangan](https://intl.cloud.tencent.com/document/product/213/37070).</li></ul> |
| Kuantitas | Wajib | Jumlah RI yang ingin Anda beli |


5. Klik **Purchase Now** (Beli Sekarang) dan selesaikan pembayaran. Kemudian, Anda dapat mengunjungi konsol [Instans Cadangan](https://console.cloud.tencent.com/cvm/reservedinstances/) untuk membuat kueri, menelusuri, dan mengelola RI Anda. Di halaman ini, Anda dapat mengklik **Create Instance** (Buat Instans) untuk membuat instans CVM, atau klik **View Bill** (Lihat Tagihan) untuk melihat detail diskon RI.

   ![image-20200909173059650](https://main.qcloudimg.com/raw/86912bb5b8ceabbb071fbb6cfa06cadf.png)
