## Ikhtisar
Disk cloud adalah perangkat penyimpanan yang dapat diperluas di cloud. Setelah disk cloud dibuat, Anda dapat memperluas kapasitasnya kapan saja untuk meningkatkan kapasitas penyimpanannya tanpa kehilangan data apa pun di dalamnya.
Setelah disk cloud diperluas, Anda perlu menetapkan kapasitas yang diperluas ke partisi yang ada, atau memformatnya menjadi partisi baru yang independen. Untuk informasi selengkapnya, lihat [Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) atau [Memperluas Partisi dan Sistem File (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).
>! Partisi MBR mendukung disk dengan kapasitas maksimum 2 TB. Saat Anda mempartisi disk dengan kapasitas lebih besar dari 2 TB, kami sarankan Anda membuat dan memasang disk data baru dan menggunakan format partisi GPT untuk menyalin data.

## Memperluas Disk Data
Jika disk cloud adalah disk data, Anda dapat memperluasnya menggunakan tiga metode berikut.
>!Jika beberapa disk cloud dengan kapasitas dan jenis yang sama dipasang ke CVM, Anda dapat membedakannya menurut metode yang ditunjukkan dalam [Membedakan disk data](#distinguish). Pilih disk data dan perluas kapasitasnya dengan cara berikut.


#### Memperluas disk data melalui konsol CVM (direkomendasikan)
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Temukan CVM tempat Anda ingin memperluas disk data, dan pilih **More** (Lainnya) > **Resource Adjustment** (Penyesuaian Sumber Daya) > **Expand Data Disk** (Perluas Disk Data) di kolom **Operation** (Operasi).
3. Pilih disk data yang akan diperluas di jendela pop-up, dan klik **Next** (Selanjutnya).
4. Pilih kapasitas baru (harus lebih besar atau sama dengan kapasitas saat ini.) dan klik **Next** (Selanjutnya).
5. Baca catatan dan klik **Adjust Now** (Sesuaikan Sekarang).
6. Tetapkan kapasitasnya yang diperluas ke partisi yang ada, atau format menjadi partisi baru yang independen. Tergantung pada sistem operasi CVM, lihat [Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) atau [Memperluas Partisi dan Sistem File (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

#### Memperluas disk data melalui konsol CBS
1. Login ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Cari disk cloud yang akan diperluas, dan pilih **More** (Lainnya) > **Expand** (Perluas) di kolom **Operation** (Operasi).
3. Pilih kapasitas baru. Kapasitas harus lebih besar dari atau sama dengan kapasitas saat ini.
4. Selesaikan pembayaran.
5. Tetapkan kapasitasnya yang diperluas ke partisi yang ada, atau format menjadi partisi baru yang independen. Tergantung pada sistem operasi CVM, lihat [Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) atau [Memperluas Partisi dan Sistem File (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

#### Memperluas disk data melalui API
Anda dapat menggunakan `ResizeDisk` API untuk memperluas disk cloud yang ditentukan. Untuk informasi selengkapnya, lihat [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310).




## Memperluas Disk Sistem
Jika disk cloud berfungsi sebagai disk sistem, Anda dapat memperluasnya menggunakan dua metode berikut.

#### Memperluas disk sistem melalui konsol CVM (direkomendasikan)
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index). Temukan CVM tempat Anda ingin memperluas disk sistem, lalu pilih **More** (Lainnya) > **Resource Adjustment** (Penyesuaian Sumber Daya) > **Expand System Disk** (Perluas Disk Sistem) di kolom **Operation** (Operasi).
2. Pilih disk sistem yang akan diperluas di jendela pop-up, lalu klik **Next** (Selanjutnya).
3. Pilih kapasitas baru (harus lebih besar atau sama dengan kapasitas saat ini.) dan klik **Next** (Selanjutnya).
4. Baca catatannya, pilih **Agree to a force shutdown** (Setujui pematian paksa), lalu klik **Adjust Now** (Sesuaikan Sekarang).
5. Setelah perluasan selesai di konsol, periksa konfigurasi cloudinit untuk [instans Linux](#confirmLinuxConfig) atau [instans Windows](#confirmwindowsConfig) sesuai dengan sistem operasi CVM. Kemudian, perluas partisi dan sistem file sesuai kebutuhan.

#### Memperluas disk sistem dengan menginstal ulang sistem
Anda juga dapat memperluas disk sistem dengan [menginstal ulang sistem](https://intl.cloud.tencent.com/document/product/213/4933)



## Operasi
[](id:distinguish)
### Membedakan disk data
Periksa disk cloud sesuai dengan sistem operasi CVM.

#### Linux
1. [Login ke instans Linux](https://intl.cloud.tencent.com/document/product/213/5436)
2. Jalankan perintah berikut untuk melihat hubungan antara disk cloud elastis dan nama perangkat.

```
ls -l /dev/disk/by-id
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
Perhatikan bahwa `disk-xxxx` adalah ID dari disk cloud. Anda dapat menggunakannya untuk melihat detail disk cloud di [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).

#### Windows
1. [Login ke instans Windows](https://intl.cloud.tencent.com/document/product/213/5435).
2. Klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px">, lalu pilih **Run** (Jalankan).
3. Masukkan `cmd` di jendela pop-up, lalu tekan **Enter** (Enter).
4. Jalankan perintah berikut untuk melihat hubungan antara disk cloud elastis dan nama perangkat.

```
wmic diskdrive get caption,deviceid,serialnumber
```
Anda juga dapat menjalankan perintah berikut
```
wmic path win32_physicalmedia get SerialNumber,Tag
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)
Perhatikan bahwa `disk-xxxx` adalah ID dari disk cloud. Anda dapat menggunakannya untuk melihat detail disk cloud di [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).


### Memeriksa konfigurasi cloudinit
Periksa konfigurasi cloudinit sesuai dengan sistem operasi CVM.

[](id:confirmLinuxConfig)
#### Memeriksa konfigurasi cloudinit untuk instans Linux
Setelah disk sistem diperluas, [login ke instans Linux](https://intl.cloud.tencent.com/document/product/213/5436) dan periksa apakah file `/etc/cloud/cloud.cfg` berisi item konfigurasi `growpart` dan `resizefs`.
 - Jika ya, abaikan operasi lainnya.
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart** (growpart): memperluas partisi ke ukuran disk.
    - **resizefs** (resizefs): memperluas atau menyesuaikan sistem file partisi `/` ke ukuran partisi.
 - Jika tidak, secara manual [memperluas partisi dan sistem file (Linux)](https://intl.cloud.tencent.com/document/product/362/31602) sesuai dengan sistem operasi, dan menetapkan kapasitas yang diperluas ke partisi yang ada, atau memformatnya menjadi partisi baru yang independen.

[](id:confirmwindowsConfig)

#### Memeriksa konfigurasi cloudinit untuk instans Windows
Setelah disk sistem diperluas, [login ke instans Windows](https://intl.cloud.tencent.com/document/product/213/5435) dan periksa apakah item konfigurasi `ExtendVolumesPlugin` ada di bawah `plugin` di `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf \cloudbase-init.conf`.
 - Jika ya, abaikan operasi lainnya.
 - Jika tidak, secara manual [perluas partisi dan sistem file (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) sesuai dengan sistem operasi, dan tetapkan kapasitas yang diperluas ke partisi yang ada, atau ubah formatnya menjadi partisi baru yang independen.

