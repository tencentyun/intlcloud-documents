Dokumen ini menjelaskan cara melihat pesan alarm pengecualian dari DBbrain di konsol TencentDB for MySQL.

Layanan pemberitahuan [alarm pengecualian](https://intl.cloud.tencent.com/document/product/1035/37177) DBbrain mendorong pesan alarm pengecualian instans MySQL kepada Anda secara real-time, memungkinkan Anda menemukan masalah diagnosis pengecualian database dengan mudah dan secepatnya.
Semua pesan alarm pengecualian yang didorong ditampilkan dalam daftar pesan historis, sehingga Anda dapat melihat dan menemukan masalah diagnosis pengecualian yang didorong sebelumnya dengan cepat.

## Melihat Alarm
### Opsi 1
Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Jika masalah diagnosis pengecualian terjadi pada instans saat Anda berada di konsol, akan muncul sebuah jendela di sudut kanan atas konsol secara real-time untuk mendorong pemberitahuan pesan alarm pengecualian, yang berisi informasi instans database seperti instans ID, nama instans, item diagnosis, dan waktu mulai, sehingga Anda dapat mengetahui status instans database yang sedang berjalan dengan cepat dan mudah.
- Anda dapat mengklik **View Exception Diagnosis Details** (Lihat Detail Diagnosis Pengecualian) di pemberitahuan pesan untuk melihat detail diagnosis spesifik dan saran pengoptimalan untuk instans.
- Jika Anda mencentang **No alarm again today** (Tidak ada alarm lagi hari ini) di pemberitahuan pesan, ketika masalah diagnosis pengecualian terjadi pada instans database di bawah akun Anda, tidak terkecuali pesan alarm akan dikirimkan kepada Anda di jendela pop-up.

![](https://main.qcloudimg.com/raw/22f1e14880499e6d18ff38f019b74d2d.png)

### Opsi 2
Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), pilih **Instance List** (Daftar Instans), **Task List** (Daftar Tugas), **Parameter Template** (Templat Parameter), **Recycle Bin** (Keranjang Sampah) atau **Placement Group** (Grup Penempatan) pada bilah sisi kiri, dan klik **Exception Alarm** (Alarm Pengecualian) di sudut kanan atas untuk memperluas daftar pesan alarm pengecualian historis. Jumlah alarm yang dihasilkan dalam kasus di bawah akun Anda ditampilkan di sebelah tombol.
![](https://main.qcloudimg.com/raw/18bda2b422ce5c221001f885bd8279a4.png)

Dalam daftar pesan alarm pengecualian historis yang diperluas, Anda dapat melihat semua pesan alarm pengecualian yang didorong. Anda dapat melihatnya berdasarkan wilayah dan mengklik pesan untuk melihat detail diagnosis dari peristiwa alarm pengecualian.
![](https://main.qcloudimg.com/raw/b2fcff416f3db287aa8b44b536bd33bd.png)
