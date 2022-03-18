Dokumen ini menjelaskan cara mengatasi masalah **network level authentication** (autentikasi tingkat jaringan) saat menghubungkan ke instans Windows menggunakan Desktop Jarak Jauh.

## Masalah
Desktop Jarak Jauh Windows gagal terhubung ke instans Windows Anda dengan pesan kesalahan **The remote computer requires Network Level Authentication, which your computer does not support. For assistance, contact your system administrator or technical support.** (Komputer jarak jauh memerlukan Autentikasi Tingkat Jaringan, yang tidak didukung komputer Anda. Untuk bantuan, hubungi administrator sistem atau dukungan teknis Anda.)
![](https://main.qcloudimg.com/raw/409b3259fa13220e8cde0790aa87488b.jpg)

## Pemecahan Masalah

> Pada langkah-langkah berikut, kami menggunakan Windows Server 2016 sebagai contoh.
>

### Login ke CVM menggunakan VNC
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, cari instans CVM yang diinginkan. Klik **Log In** (Login), seperti yang ditunjukkan pada gambar berikut:
![Halaman indeks CVM](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Di jendela **Log in to Windows instance** (Login ke instans Windows) yang muncul, pilih **Alternative login methods (VNC)** (Metode login alternatif (VNC)). Klik **Log In Now** (Login Sekarang) untuk login ke CVM.
4. Di jendela login yang muncul, pilih **Send Remote Command** (Kirim Perintah Jarak Jauh) di sudut kiri atas. Klik **Ctrl-Alt-Delete** (Ctrl-Alt-Delete) untuk masuk ke antarmuka login sistem seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Memodifikasi registri Windows

1. Pada antarmuka sistem operasi, klik <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>. Masukkan **regedit** ()regedit dan tekan **Enter** (Enter) untuk membuka Registry Editor.
2. Menggunakan pohon navigasi di sisi kiri, arahkan ke **Computer** (Komputer) > **HKEY_LOCAL_MACHINE** (HKEY_LOCAL_MACHINE) > **SYSTEM** (SISTEM) > **CurrentControlSet** (CurrentControlSet) > **Control** (Kontrol) > **Lsa** (Lsa). Di panel sisi kanan, pilih **Security Packages** (Paket Keamanan), seperti yang ditunjukkan pada gambar berikut:
![Paket Keamanan](https://main.qcloudimg.com/raw/db037b5131ff44af72b560fbac4931e1.png)
3. Klik dua kali **Security Packages** (Paket Keamanan) untuk membuka kotak dialog **Edit Multi-String** (Edit Multi-String).
4. Dalam kotak dialog **Edit Multi-String** (Edit Multi-String), tambahkan **tspkg** (tspkg) di bawah **Value Data** (Data Nilai) dan klik **OK** (Oke), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/cca2bce345b48569d45fd391ee65bc51.png)
5. Menggunakan struktur navigasi di sisi kiri, arahkan ke **Computer** (Komputer) > **HKEY_LOCAL_MACHINE** (HKEY_LOCAL_MACHINE) > **SYSTEM**(SISTEM) > **CurrentControlSet** (CurrentControlSet) > **Control** (Kontrol) > **SecurityProviders** (SecurityProviders). Di panel sisi kanan, pilih **SecurityProviders** (SecurityProviders), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/14e84c77ae1d1d3c5bc2ab091543a957.png)
6. Klik dua kali **SecurityProviders** (SecurityProviders) untuk membuka kotak dialog **Edit Multi-String** (Edit Multi-String).
7. Tambahkan `,credssp.dll` ke akhir bidang **Value Data** (Data Nilai) di kotak dialog **Edit Multi-String** (Edit Multi-String). Klik **OK** (Oke) seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/34b98c226c359b070e2f03c2ff1c6e42.png)
8. Tutup editor registri dan mulai ulang instans. Anda sekarang dapat login dari jarak jauh.

