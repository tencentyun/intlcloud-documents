## Ikhtisar
Dokumen ini menjelaskan cara menyiapkan citra untuk sistem operasi Windows Server 2012. Anda juga dapat merujuk ke dokumen ini untuk versi Windows Server lainnya.

## Petunjuk

### Persiapan

Sebelum menyiapkan dan mengekspor citra disk sistem, selesaikan pemeriksaan berikut.
>? Jika Anda perlu menyiapkan dan mengekspor citra disk data, lewati operasi ini.
>

#### Memeriksa mode partisi dan memulai OS

1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> untuk membuka jendela **Windows PowerShell** (Windows PowerShell).
2. Di jendela **Windows PowerShell** (Windows PowerShell), masukkan **diskmgmt.msc** (diskmgmt.msc), lalu klik **Enter** (Enter) untuk membuka jendela **Disk Management** (Pengelolaan Disk).
3. Klik kanan disk yang akan diperiksa, klik **Properties** (Properti), lalu pilih tab **Volume** (Volume) untuk memeriksa mode partisi disk.
4. Periksa apakah mode partisi disk adalah GPT.
 - Jika ya, [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) karena migrasi layanan saat ini tidak mendukung partisi GPT.
 - Jika tidak, lanjutkan ke langkah selanjutnya.
5. Mulai CMD sebagai pengguna admin dan jalankan perintah berikut untuk memeriksa apakah sistem operasi dimulai dalam mode EFI:
```
bcdedit /enum {current}
```
Hasil yang mirip dengan berikut ini akan ditampilkan:
```
Windows boot loader
ID                  {current}
device                  partition=C:
path                    \WINDOWS\system32\winload.exe
description             Windows 10
locale                  zh-CN
inherit                 {bootloadersettings}
recoverysequence        {f9dbeba1-1935-11e8-88dd-ff37cca2625c}
displaymessageoverride  Recovery
recoveryenabled         Yes
flightsigning           Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \WINDOWS
resumeobject            {1bcd0c6f-1935-11e8-8d3e-3464a915af28}
nx                      OptIn
bootmenupolicy          Standard
```
 - Jika `path` berisi "efi", sistem operasi akan memulai dalam mode EFI. Dalam hal ini, [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).
 - Jika `path` tidak berisi "efi", lanjutkan ke langkah selanjutnya.

#### Menghapus penginstalan perangkat lunak

Hapus penginstalan driver dan perangkat lunak yang saling bertentangan (termasuk alat VMware, alat Xen, Virtualbox GuestAdditions, dan perangkat lunak lain yang disertakan dengan driver yang mendasarinya).

#### Menginstal cloud-base

Instal cloud-base seperti yang diinstruksikan di [Menginstal Cloudbase-Init di Windows](https://intl.cloud.tencent.com/document/product/213/32364).

#### Memeriksa atau menginstal driver Virtio

1. Klik **Control Panel** (Panel Kontrol) > **Programs and Features** (Program dan Fitur), dan masukkan "Virtio" di kotak pencarian.
 - Jika hasil seperti pada citra berikut ditampilkan, berarti driver Virtio sudah terinstal.
![](https://main.qcloudimg.com/raw/ff1dffb01a7f77d515061bce184e033b.png)
 - Jika driver Virtio tidak diinstal, Anda perlu menginstalnya secara manual.
    - Untuk Microsoft Windows Server 2008 R2 (Edisi Standar, Edisi Datacenter, dan Edisi Enterprise), Microsoft Windows Server 2012 R2 (Edisi Standar), Microsoft Windows Server 2016 (Edisi Datacenter), dan Microsoft Windows Server 2019 (Edisi Datacenter), unduh Virtio untuk Tencent Cloud di:
      - Alamat unduhan jaringan publik: `http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe`
      - Alamat unduhan jaringan pribadi: `http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe`
    - Untuk versi sistem lainnya, unduh [Virtio for Community Edition](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers).

#### Memeriksa konfigurasi perangkat keras lainnya

Setelah migrasi ke cloud, perubahan perangkat keras termasuk namun tidak terbatas pada:
 - Kartu grafis diubah menjadi Cirrus VGA.
 - Disk diubah menjadi Virtio Disk.
 - ENI diubah menjadi Virtio Nic, dan Area Koneksi Lokal digunakan secara default.

### Mengekspor citra
Anda dapat menggunakan berbagai alat untuk mengekspor citra sesuai dengan kebutuhan Anda.
<dx-tabs>
::: Using\sa\splatform\stool\sto\sexport\san\simage[](id:Useplatform)
Untuk informasi selengkapnya tentang cara menggunakan alat ekspor citra dari platform virtualisasi, seperti VMWare vCenter Convert dan Citrix XenConvert, lihat dokumen untuk masing-masing platform.
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>Catatan</p><p>Migrasi layanan Tencent Cloud mendukung citra dalam format qcow2, vhd, raw, dan vmdk.</p>
</blockquote>
:::
::: Using\sdisk2vhd\sto\sexport\san\simage[](id:Usedisk2vhd)
Jika Anda perlu mengekspor sistem pada mesin fisik atau jika Anda tidak ingin menggunakan alat platform untuk mengekspor citra, gunakan disk2vhd sebagai gantinya.
1. Instal dan mulai alat Disk2vhd.
[Klik di sini untuk mengunduh disk2vhd >>](https://download.sysinternals.com/files/Disk2vhd.zip).
2. Pilih jalur penyimpanan citra yang akan diekspor, pilih volume yang akan disalin, dan klik **Create** (Buat), seperti yang ditunjukkan pada gambar berikut.
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>Catatan</p><ul><li><p>Disk2vhd hanya dapat dimulai setelah Volume Shadow Copy Service (VSS) diinstal di sistem Windows. Untuk informasi selengkapnya tentang fitur VSS, lihat <a href="https://docs.microsoft.com/zh-cn/windows/win32/vss/volume-shadow-copy-service-portal?redirectedfrom=MSDN">Volume Shadow Copy Service</a>.</p></li><li><p>Jangan pilih "Use Vhdx" (Gunakan Vhdx) karena sistem saat ini tidak mendukung citra VHDX.</p></li><li><p>Sebaiknya pilih "Use volume Shadow Copy" (Gunakan Volume Shadow Copy) untuk memastikan integritas data dengan lebih baik.</p></li></ul>
</blockquote>

![citra](https://main.qcloudimg.com/raw/68d9c4e5e7db49c4cefdd3785ce9b68d.jpg)
:::
</dx-tabs>


### Memeriksa citra

>? Sistem file citra yang Anda siapkan mungkin rusak karena Anda menyiapkan citra tanpa menghentikan layanan atau karena alasan lain. Dengan demikian, sebaiknya periksa citra setelah menyiapkannya.
>
Jika format citra didukung oleh platform saat ini, Anda dapat langsung membuka citra untuk memeriksa sistem file. Misalnya, platform Windows mendukung citra dalam format vhd; platform Linux memungkinkan Anda menggunakan qemu-nbd untuk membuka citra dalam format qcow2; dan platform Xen memungkinkan Anda untuk langsung membuka file dalam format vhd.

Dokumen ini menjelaskan cara memeriksa citra VHD melalui **Attach VHD** (Lampirkan VHD) di **Disk Management** (Pengelolaan Disk) di server Windows.
1. Di desktop, klik kanan <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-4px 0px">, dan pilih **Computer Management** (Pengelolaan Komputer) di menu pop-up.
2. Pilih **Storage** (Penyimpanan) > **Disk Management** (Pengelolaan Disk) untuk masuk ke antarmuka pengelolaan disk.
3. Pilih **Action** (Tindakan) > **Attach VHD** (Lampirkan VHD) di bagian atas jendela.
![](https://main.qcloudimg.com/raw/90a6ce24b78ca128ade5018833011708.png)
Jika muncul hasil mirip dengan gambar berikut, citra telah dibuat.
![](https://main.qcloudimg.com/raw/41eac48fe77d3773dcf1ac9121b251ce.png)
