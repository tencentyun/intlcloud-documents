## Ikhtisar
Dokumen ini menjelaskan cara mengosongkan ruang disk pada Tencent Cloud CVM berbasis Windows Server 2012 R2 saat ruang disk tidak mencukupi. Dokumen ini juga menjelaskan cara melakukan pemeliharaan disk secara rutin.

## Petunjuk

### Mengosongkan ruang disk
Anda dapat menghapus [file besar](#deleteLargerFiles) atau [file yang tidak terpakai](#deleteObsoleteFiles) untuk mengosongkan ruang disk. Jika ruang disk masih tidak mencukupi setelah menghapus file besar dan yang tidak terpakai, Anda dapat memperluas ruang disk. Untuk melakukannya, harap lihat [Skenario Perluasan Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31600).
<span id="deleteLargerFiles"></span>
#### Menghapus file besar
1. Login ke instans Windows menggunakan [file RDP (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5435) atau [desktop jarak jauh](https://intl.cloud.tencent.com/document/product/213/32498).
2. Klik <img src="https://main.qcloudimg.com/raw/dcdf8e1ebc35bd6db1edaceff6784db2.png" style="margin:-5px 0px"> di bilah alat bawah dan buka jendela “This PC” (PC Ini).
3. Pilih disk tempat Anda ingin mengosongkan ruang, dan tekan **Crtl + F** (Crtl + F) untuk membuka alat pencarian.
4. Pilih **Search** (Pencarian) -> **Size** (Ukuran) dan filter file menurut opsi ukuran yang ditentukan sistem, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/48a1033c6b978dfe6de1b2dc6d8bcdd3.png)
>?Anda juga dapat memasukkan ukuran di kotak pencarian di sudut kanan atas jendela **This PC** (PC Ini). Sebagai contoh:
>- Masukkan “Size: > 500 MB” (Ukuran: > 500 MB) untuk mencari disk untuk file yang lebih besar dari 500 MB.
>- Masukkan “Size: > 100 MB < 500 MB” (Size: > 100 MB < 500 MB) untuk mencari disk untuk file yang lebih besar dari 100 MB tetapi kurang dari 500 MB.
>

<span id="deleteObsoleteFiles"></span>
#### Menghapus file yang tidak terpakai
1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-5px 0px"> untuk membuka **Server Manager** (Pengelola Server).
2. Klik **Add Roles and Features** (Tambahkan Peran dan Fitur) pada bagian **Manage** (Kelola).
3. Di jendela pop-up, klik **Next** (Selanjutnya).
4. Pilih **Role-based or feature-based installation** (Penginstalan berbasis peran atau berbasis fitur) dan klik **Next** (Selanjutnya) dua kali, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/d25dc913281f8cb5c688dd9cc62b8d73.png)
5. Pada halaman **Select features** (Pilih fitur), centang **Ink and Handwriting Services** (Layanan Tinta dan Tulisan Tangan) dan **Desktop Experience** (Pengalaman Desktop), seperti yang ditunjukkan di bawah ini. Klik **OK** (OKE) di kotak dialog pop-up.
![](https://main.qcloudimg.com/raw/f1bf18c4598597ef86428bd4bbd77c15.png)
6. Klik **Next** (Selanjutnya), lalu **Install** (Instal). Tunggu hingga penginstalan selesai, dan mulai ulang CVM saat diminta.
7. Pilih <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px"> dan klik <img src="https://main.qcloudimg.com/raw/4851c97390178d2d8ae2e6385756eb3b.png" style="margin:-5px 0px"> di sudut kanan atas. Masukkan dan cari **Disk Management** (Pengelolaan Disk).
8. Di jendela pop-up **Disk Cleanup** (Pembersihan Disk), pilih disk target dan mulai pembersihan, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/69e2c653c6304a450463cdf07bf5a3ef.png)

### Pemeliharaan disk secara rutin
#### Menghapus program secara teratur
Pilih **Control Panel** (Panel Kontrol) -> **Programs and Features** (Program dan Fitur) -> **Uninstall or change a program** (Hapus penginstalan atau ubah program) untuk menghapus program yang tidak terpakai secara berkala, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/b9294f1e79429dbdb8a7800cfdb6d6b4.png)


#### Melihat penggunaan disk di konsol
Fitur Cloud Monitor diaktifkan secara otomatis setelah instans CVM dibuat. Anda dapat melihat penggunaan disk dengan mengikuti langkah-langkah di bawah ini:
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/instance/index) dan akses halaman **Instances** (Instans).
2. Pilih ID/Nama instans target untuk mengakses halaman detail.
3. Pilih tab **Monitoring** (Pemantauan) untuk melihat penggunaan disk instans, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/19f00a883ed73ba1c636830f06d3f00d.png)
