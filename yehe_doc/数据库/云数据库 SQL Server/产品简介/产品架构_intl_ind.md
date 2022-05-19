## Edisi Kluster
## Versi yang didukung
SQL Server 2017 Enterprise

### Arsitektur
Edisi Kluster TencentDB for SQL Server mengadopsi arsitektur Always On, termasuk satu primer dan satu replika yang di-deploy di seluruh rak/AZ. Masing-masing sesuai dengan agen pemantau yang memantau database melalui detak jantung secara real-time.
- Kluster manajemen Tencent Cloud: terdiri dari kluster pengambilan keputusan dan penjadwalan yang di-deploy secara independen dan kluster konfigurasi sebagai pusat manajemen dan penjadwalan kluster dan bertanggung jawab untuk mengelola operasi normal grup node database, kluster gateway akses, dan COS.
- COS: menyediakan pemulihan bencana data dan layanan cold backup.
- Akses kluster gateway: menyediakan IP unik secara eksternal, sehingga meskipun node data dialihkan, IP pengguna untuk terhubung ke instans tetap tidak berubah.


>?Proses sinkronisasi dasar Always On:
>Log (komit dan penulisan blok log) dari node utama akan dihapus dari cache log ke disk. Pada saat yang sama, utas Pengambilan Log dari node utama juga akan mengirim log ke semua node replika lainnya, dan utas Penerimaan Log dari node yang sesuai juga akan menghapus log yang diterima dari cache log ke disk. Akhirnya, utas Redo mem-flush log ini ke file data.
>
![](https://main.qcloudimg.com/raw/32fbdee7b03ed0b44aae3b539f0ca78f.png)


## Edisi Ketersediaan Tinggi Server Ganda
## Versi yang didukung
- SQL Server 2008/2012/2014/2016/2017 Enterprise
- SQL Server 2008/2012/2014/2016/2017 Standard

### Arsitektur
Edisi Ketersediaan Tinggi Server Ganda TencentDB for SQL Server terdiri dari satu database utama dan satu database cermin yang di-deploy di seluruh rak/AZ. Masing-masing sesuai dengan agen pemantau yang memantau database melalui detak jantung secara real-time.
- Kluster manajemen Tencent Cloud: terdiri dari kluster pengambilan keputusan dan penjadwalan yang di-deploy secara independen dan kluster konfigurasi sebagai pusat manajemen dan penjadwalan kluster dan bertanggung jawab untuk mengelola operasi normal grup node database, kluster gateway akses, dan COS.
- COS: menyediakan pemulihan bencana data dan layanan cold backup.
- Akses kluster gateway: menyediakan IP unik secara eksternal, sehingga meskipun node data dialihkan, IP pengguna untuk terhubung ke instans tetap tidak berubah.
- Penskalaan instans baca saja diimplementasikan melalui model publikasikan/langganan.

>? Sebuah cermin memiliki salinan data yang lengkap tetapi tidak menyediakan layanan baca/tulis dengan sendirinya; karenanya, ini mengimplementasikan sinkronisasi data dengan menerima log pembaruan dari primer dan memungkinkan pembuatan snapshot untuk pelaporan. Dalam kluster cermin, sinkronisasi data antara primer dan cermin bergantung pada log transaksi. Log transaksi SQL Server berada di tingkat database daripada tingkat instans, dan setiap database memiliki log transaksi terpisah, sehingga pencerminan SQL Server diimplementasikan pada tingkat database.

![](https://main.qcloudimg.com/raw/908fda85784c6d198536e44980715d5a.png)

## Edisi Dasar
## Versi yang didukung
SQL Server 2008/2012/2014/2016/2017 Enterprise

### Arsitektur
Edisi Dasar mengadopsi metode deployment node tunggal dan menawarkan efektivitas biaya yang sangat tinggi. Fitur-fiturnya disorot seperti di bawah ini:
- Mendukung pemisahan komputasi-penyimpanan. Jika node komputasi gagal, pemulihan cepat dapat dicapai dengan beralih ke node lain. Data yang mendasari disimpan dalam tiga salinan pada disk cloud, yang memastikan tingkat keandalan data tertentu dan memungkinkan pemulihan data cepat dari snapshot disk jika terjadi kegagalan disk.
- Menawarkan lebih dari 20 metrik pemantauan seperti koneksi database, akses, dan sumber daya dan mendukung konfigurasi kebijakan alarm sesuai kebutuhan. Dibandingkan dengan database berbasis CVM yang dibuat sendiri, instans Edisi Dasar juga di-deploy pada instans CVM tetapi lebih nyaman dan memberikan performa database yang lebih tinggi dengan biaya lebih rendah.
- Menggunakan disk cloud premium sebagai media penyimpanan dasarnya, sehingga cocok untuk skenario I/O 90% dengan biaya rendah dan performa stabil.
>!
>- Sangat cocok untuk pembelajaran pribadi, perangkat lunak ISV untuk perusahaan kecil dan menengah (seperti pelanggan keuangan, CRM, dan ERP), aplikasi web, dan sistem perusahaan kecil non-inti.
> - Karena mengadopsi arsitektur node tunggal, ketika node gagal, pemulihannya membutuhkan waktu sedikit lebih lama daripada CVM (karena mulai ulang instans dan pemulihan data).
>- Jika bisnis Anda memerlukan ketersediaan tinggi, sebaiknya gunakan Edisi Ketersediaan Tinggi Server Ganda atau Edisi Kluster.

![](https://main.qcloudimg.com/raw/e16d9a236cf2c6f9c6ce174486c1fcce.svg)

