## Ikhtisar
Disk cloud adalah perangkat penyimpanan yang dapat diperluas di cloud.Setelah disk cloud dibuat, Anda dapat memperluas kapasitasnya kapan saja untuk meningkatkan kapasitas penyimpanannya tanpa kehilangan data apa pun di dalamnya.
Setelah disk cloud diperluas, Anda perlu menetapkan kapasitas yang diperluas ke partisi yang ada, atau memformatnya menjadi partisi baru yang terpisah.Untuk informasi selengkapnya, lihat [Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) atau [Menentukan Metode Perluasan](https://intl.cloud.tencent.com/document/product/362/39995).
>!Partisi MBR mendukung disk dengan kapasitas maksimum 2 TB.Saat Anda mempartisi disk dengan kapasitas lebih besar dari 2 TB, sebaiknya Anda membuat dan melampirkan disk data baru dan menggunakan format partisi GPT untuk menyalin data.

### Memperluas Disk Data
Jika disk cloud adalah disk data, Anda dapat memperluasnya menggunakan tiga metode berikut.
>!Jika beberapa disk cloud dengan kapasitas dan jenis yang sama terlampir ke CVM, Anda dapat mengidentifikasinya menggunakan metode yang ditunjukkan di [Membedakan disk data](#distinguish).Pilih disk data dan perluas kapasitasnya seperti yang diinstruksikan di bawah ini.
>

<dx-tabs>
:::Memperluas\sdisk\sdata\smelalui\skonsol\sCVM\s(direkomendasikan) [](id:useCVMConsole)
1.Masuk ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2.Temukan CVM tempat Anda ingin memperluas disk data, dan pilih **More** > **Resource Adjustment** > **Expand Data Disk** (Selengkapnya > Penyesuaian Sumber Daya > Perluas Disk Data) di kolom **Operation** (Operasi).
3.Pilih disk data yang akan diperluas di jendela pop-up, dan klik **Next** (Selanjutnya).
4.Pilih kapasitas baru (harus lebih besar atau sama dengan kapasitas saat ini) dan klik **Next** (Selanjutnya).
5.Baca catatan dan klik **Adjust Now** (Sesuaikan Sekarang).
6.Tetapkan kapasitasnya yang diperluas ke partisi yang ada, atau format menjadi partisi baru yang terpisah.Tergantung pada sistem operasi CVM, lihat [Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) atau [Menentukan Metode Perluasan](https://intl.cloud.tencent.com/document/product/362/39995).
:::
:::Memperluas\sdisk\sdata\smelalui\skonsol\sCBS [](id:useCBSConsole)
1.Masuk ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2.Temukan disk cloud yang akan diperluas, dan pilih **More** > **Expand** (Selengkapnya > Perluas) di kolom **Operation** (Operasi).
3.Pilih kapasitas baru.Ini harus lebih besar dari atau sama dengan kapasitas saat ini.
4.Selesaikan pembayaran.
5.Tetapkan kapasitasnya yang diperluas ke partisi yang ada, atau format menjadi partisi baru yang terpisah.Tergantung pada sistem operasi CVM, lihat [Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) atau [Menentukan Metode Perluasan](https://intl.cloud.tencent.com/document/product/362/39995).
:::
:::Memperluas\sdisk\sdata\smelalui\sAPI [](id:useAPI)
Anda dapat menggunakan API `ResizeDisk` untuk memperluas disk cloud yang ditentukan.Untuk informasi selengkapnya, lihat [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310).
:::
</dx-tabs>



## Memperluas disk sistem[](id:useCVMconsole)
1.Masuk ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).Temukan CVM tempat Anda ingin memperluas disk sistem, dan pilih **More** > **Resource Adjustment** > **Expand System Disk** (Selengkapnya > Penyesuaian Sumber Daya > Perluas Disk Sistem) di kolom **Operation** (Operasi).
2.Pilih disk sistem yang akan diperluas di jendela pop-up, dan klik **Next** (Selanjutnya).
3.Pilih kapasitas baru (harus lebih besar atau sama dengan kapasitas saat ini.) dan klik **Next** (Selanjutnya).
4.Baca catatannya, pilih **Agree to a force shutdown** (Setuju untuk melakukan pematian paksa), dan klik **Adjust Now** (Sesuaikan Sekarang).
5.Setelah perluasan selesai di konsol, periksa konfigurasi cloudinit untuk [instance Linux](#confirmLinuxConfig) atau [instance Windows](#confirmwindowsConfig) sesuai dengan sistem operasi CVM.Kemudian perluas partisi dan sistem file sesuai kebutuhan.



## Operasi
### Membedakan disk data[](id:distinguish)
Periksa disk cloud sesuai dengan sistem operasi CVM.
<dx-tabs>
::: Linux
1.[Masuk ke instance Linux](https://intl.cloud.tencent.com/document/product/213/5436)
2.Jalankan perintah berikut untuk melihat hubungan antara disk cloud elastis dan nama perangkat.
```
ls -l /dev/disk/by-id
``` Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
Perhatikan bahwa `disk-xxxx` adalah ID dari disk cloud.Anda dapat menggunakannya untuk melihat detail disk cloud di [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
:::
::: Windows
1.- [Masuk ke instance Windows](https://intl.cloud.tencent.com/document/product/213/5435).
2.Klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px">, dan pilih **Run** (Jalankan).
3.Masukkan `cmd` di jendela pop-up dan tekan **Enter**.
4.Jalankan perintah berikut untuk melihat hubungan antara disk cloud elastis dan nama perangkat.
```
wmic diskdrive get caption,deviceid,serialnumber
```Anda juga dapat menjalankan perintah berikut.

```
wmic path win32_physicalmedia get SerialNumber,Tag
``` Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)
Perhatikan bahwa `disk-xxxx` adalah ID dari disk cloud.Anda dapat menggunakannya untuk melihat detail disk cloud di [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
:::
</dx-tabs>

### Memeriksa konfigurasi cloudinit
Periksa disk cloud sesuai dengan sistem operasi CVM.
<dx-tabs>
:::Memeriksa\skonfigurasi\scloudinit\suntuk\sinstance\sLinux [](id:confirmLinuxConfig)
Setelah disk sistem diperluas, [masuk ke instance Linux](https://intl.cloud.tencent.com/document/product/213/5436) dan periksa apakah file `/etc/cloud/cloud.cfg` berisi item konfigurasi `growpart` dan `resizefs`.
- Jika ya, abaikan operasi lainnya.
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
- **growpart**: memperluas partisi ke ukuran disk.
- **resizefs**: memperluas atau menyesuaikan sistem file di partisi `/` ke ukuran partisi.
- Jika tidak, secara manual [memperluas partisi dan sistem file (Linux)](https://intl.cloud.tencent.com/document/product/362/39995) sesuai dengan sistem operasi, dan menetapkan kapasitas yang diperluas ke partisi yang sudah ada, atau memformatnya menjadi partisi baru yang terpisah.
:::
:::Memeriksa\skonfigurasi\scloudinit\suntuk\sinstance\sWindows [](id:confirmwindowsConfig)
Setelah disk sistem diperluas, [masuk ke instance Windows](https://intl.cloud.tencent.com/document/product/213/5435) dan periksa apakah item konfigurasi `ExtendVolumesPlugin` ada di bawah `plugin` di `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf`.
- Jika ya, abaikan operasi lainnya.
- Jika tidak, secara manual [memperluas partisi dan sistem file (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) sesuai dengan sistem operasi, dan tetapkan kapasitas yang diperluas ke partisi yang sudah ada, atau memformatnya menjadi partisi baru yang terpisah.
:::
</dx-tabs>
