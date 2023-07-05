## Ikhtisar
Jika lupa kata sandi login instans CVM, harap atur ulang kata sandi tersebut di konsol.
>! 
> - Anda dapat langsung mengatur ulang kata sandi login dari instans pematian.
> - Mengatur ulang kata sandi login dari instans yang sedang berjalan akan memaksanya dimatikan. Untuk menghindari kehilangan data, harap rencanakan sebelumnya dan atur ulang kata sandi selama jam tidak sibuk.



## Petunjuk
<dx-tabs>
::: Resetting\sthe\spassword\sof\sa\ssingle\sinstance
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman **Instances** (Instans), cari instans CVM target, lalu klik **More** (Lainnya) > **Password/Key** (Kata Sandi/Kunci) > **Reset Password** (Atur Ulang Kata Sandi) di kolom **Operation** (Operasi), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/bf69799efaca26e824022a82bdb2faa9.png)
3. Pilih **Username** (Nama Pengguna) dan masukkan nama pengguna dari instans yang dipilih. Masukkan **New password** (Kata sandi baru), masukkan kembali kata sandi baru di kolom **Confirm Password** (Konfirmasi Kata Sandi), lalu klik **Next** (Berikutnya).
<dx-alert infotype="notice">**Username** (Nama Pengguna) defaultnya adalah **System default** (Default sistem), dan nama pengguna sistem default digunakan, seperti “Administrator” untuk Windows, “ubuntu” untuk Ubuntu, dan “root” untuk distribusi Linux lainnya. Anda dapat memilih **Specified user name** (Nama pengguna yang ditentukan) dan memasukkan nama pengguna.
</dx-alert>
![](https://main.qcloudimg.com/raw/420c83619601563c1c3c0c64c0bf533d.png)
4. Atur ulang kata sandi sesuai dengan status instans:
 - Untuk mengatur ulang kata sandi instans yang **Running** (Berjalan), pilih **Agree to force shutdown** (Setujui pematian paksa), lalu klik **Reset Password** (Atur Ulang Kata Sandi), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/ff478b4ab58289137c47356e00ad4c9a.png)
 - Untuk mengatur ulang kata sandi instans yang **Shutdown** (Dimatikan), klik **Reset Password** (Atur Ulang Kata Sandi), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/950198759de0f3f937df8c6dc4b2a72d.png)    
:::
::: Resetting\sthe\spasswords\sof\smultiple\sinstances
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman **Instances** (Instans), pilih instans CVM untuk mengatur ulang kata sandi, lalu klik **Reset Password** (Atur Ulang Kata Sandi) di bagian atas daftar instans, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/38b9be9d0b1b6890f9b07852e91c8bd3.png)
3. Pilih **Username** (Nama Pengguna) dan masukkan nama pengguna dari instans yang dipilih. Masukkan **New password** (Kata sandi baru), masukkan kembali kata sandi baru di kolom **Confirm Password** (Konfirmasi Kata Sandi), lalu klik **Next** (Berikutnya).
<dx-alert infotype="notice">**Username** (Nama Pengguna) defaultnya adalah **System default** (Default sistem), dan nama pengguna sistem default digunakan, seperti “Administrator” untuk Windows, “ubuntu” untuk Ubuntu, dan “root” untuk distribusi Linux lainnya. Anda dapat memilih **Specified user name** (Nama pengguna yang ditentukan) dan memasukkan nama pengguna.
</dx-alert>
![](https://main.qcloudimg.com/raw/1abf9af8eb892191acc3998bb5845dea.png)
4. Atur ulang kata sandi sesuai dengan status instans:
 - Untuk mengatur ulang kata sandi instans yang **Running** (Berjalan), pilih **Agree to force shutdown** (Setujui pematian paksa), lalu klik **Reset Password** (Atur Ulang Kata Sandi), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/ff478b4ab58289137c47356e00ad4c9a.png)
 - Untuk mengatur ulang kata sandi instans yang **Shutdown** (Dimatikan), klik **Reset Password** (Atur Ulang Kata Sandi), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/950198759de0f3f937df8c6dc4b2a72d.png)    
:::
</dx-tabs>
