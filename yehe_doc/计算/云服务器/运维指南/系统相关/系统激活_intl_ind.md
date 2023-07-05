CVM menggunakan KMS untuk mengizinkan server Windows.
>! 
> - Dokumen ini ditujukan hanya untuk citra publik Windows Server yang disediakan oleh Tencent Cloud. Dokumen ini tidak berlaku untuk citra kustom atau citra yang diimpor dari sumber eksternal.
> - Berikan izin kepada Windows Server 2008 dan Windows Server 2012 untuk menggunakan metode ini. Alamat KMS default (kms.tencentyun.com:1668) yang dikonfigurasi untuk citra publik Windows Server 2016 dan Windows Server 2019 sudah benar dan tidak perlu diubah.


## Catatan
1. Layanan Pemberitahuan SPP di **Windows Server 2008** (Windows Server 2008) digunakan untuk aktivasi. Pastikan layanan tersebut berjalan dengan baik, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. Beberapa perangkat lunak pengoptimalan dapat menonaktifkan modifikasi izin eksekusi program layanan. Misalnya, mengubah izin eksekusi dari sppsvc.exe mungkin menghasilkan pengecualian, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c1ad23337b0f1b6e186d0c6e50c9e1b5.png)
Sebelum Anda mengaktifkan CVM Windows, pastikan layanan dan fitur lain pada CVM Windows berjalan normal.
 
## Aktivasi Otomatis
Tencent Cloud merangkum skrip untuk mengaktifkan server Windows, yang menyederhanakan aktivasi otomatis. Untuk menggunakan skrip aktivasi, ikuti langkah-langkah di bawah ini:
1. Login ke CVM Windows.
2. Unduh dan jalankan [skrip](https://iso-1251783334.cos.ap-guangzhou.myqcloud.com/scripts/activate-win.bat) untuk menyelesaikan aktivasi otomatis.


## Aktivasi Manual

### Catatan
Jam sistem yang tidak akurat akan memicu kesalahan selama aktivasi manual untuk beberapa sistem. Dalam hal ini, sinkronkan jam sistem terlebih dahulu dengan mengikuti langkah-langkah di bawah ini:
> Jika jam sistem pada CVM Windows berfungsi normal, lanjut ke langkah [Aktivasi](#ActivationStep).
>
1. Login ke CVM Windows.
2. Di desktop, pilih **Start** (Mulai) > **Run** (Jalankan). Masukkan `cmd.exe` di kotak dialog "Run" (Jalankan) untuk membuka jendela konsol.
3. Di jendela konsol, jalankan perintah berikut secara berurutan untuk menyinkronkan jam sistem:
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### Aktivasi

1. Login ke CVM Windows.
2. Di desktop, pilih **Start** (Mulai) > **Run** (Jalankan). Masukkan `cmd.exe` di kotak dialog "Run" (Jalankan) untuk membuka jendela konsol.
3. Di jendela konsol, jalankan perintah berikut secara berurutan untuk menyelesaikan aktivasi manual.
 - Jalankan perintah berikut secara berurutan untuk Windows Server 2008, Windows Server 2012, dan Windows Server 2019:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Jalankan perintah berikut secara berurutan untuk server Windows Server 2016:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




