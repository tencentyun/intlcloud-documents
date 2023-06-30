Dokumen ini menjelaskan masalah umum yang mungkin Anda temui saat login ke CVM Windows di Mac melalui Microsoft Remote Desktop dan cara mengatasinya.
## Masalah

- Saat login ke CVM Windows melalui Microsoft Remote Desktop, Anda mendapatkan prompt “Sertifikat tidak dapat diverifikasi kembali ke sertifikat root”.

<img src="https://main.qcloudimg.com/raw/070b9c862d6928988768b266461bc816.png" data-nonescope="true" />

- Saat menggunakan Remote Desktop Connection di Mac, Anda mendapatkan prompt “Remote Desktop Connection cannot verify the identity of the computer that you want to connect to” (Koneksi Desktop Jarak Jauh tidak dapat memverifikasi identitas komputer yang ingin Anda hubungkan).


### Pemecahan Masalah
> Operasi berikut menggunakan contoh Windows Server 2016.
>

### Login ke CVM menggunakan VNC

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di halaman manajemen instans, cari CVM yang Anda butuhkan, dan klik **Log In** (Login). Hal ini ditunjukkan pada gambar berikut:
![Login](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Di jendela **Log into Windows instance** (Login ke instans Windows) yang muncul, pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)), lalu klik **Log In Now** (Login Sekarang), untuk login ke CVM.
4. Pada jendela login yang muncul, pilih **Send CtrlAltDel** (Kirim CtrlAltDel) di pojok kiri atas, dan klik **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk masuk ke antarmuka login sistem seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Memodifikasi kebijakan grup lokal dari instans

1. Di antarmuka sistem operasi, klik <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, masukkan **gpedit.msc**, dan tekan **Enter** untuk membuka Local Group Policy Editor (Editor Kebijakan Grup Lokal).
> Anda juga dapat menggunakan pintasan “Win+R” untuk membuka antarmuka Run (Jalankan).
>
2. Di pohon navigasi kiri, pilih **Computer Configuration** (Konfigurasi Komputer) > **Administrative Templates** (Templat Administratif) > **Windows Components** (Komponen Windows) > **Remote Desktop Services** (Layanan Desktop Jarak Jauh) > **Remote Desktop Session Host** (Host Sesi Desktop Jarak Jauh) > **Security** (Keamanan) , klik dua kali **Require use of specific security layer for remote (RDP) connections** (Memerlukan penggunaan lapisan keamanan khusus untuk koneksi jarak jauh (RDP))
3. Di jendela “Require use of specific security layer for remote (RDP) connections” (Memerlukan penggunaan lapisan keamanan khusus untuk koneksi jarak jauh (RDP)), pilih **Enabled** (Diaktifkan), dan atur **Security Layer** (Lapisan Keamanan) ke **RDP** 
4. Klik **OK** (Oke) untuk menyelesaikan konfigurasi.
5. Mulai ulang instans dan coba hubungkan lagi.
Jika koneksi gagal lagi, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
