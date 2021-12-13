## Skenario Operasi
Dokumen ini menjelaskan cara mengedit tag sumber daya.

## Batasan Penggunaan

Ada beberapa batasan dalam mengedit tag:
- Kuantitas: setiap sumber daya dapat memiliki paling banyak 50 tag.
- Pembatasan kunci tag:
  - Anda tidak dapat membuat kunci tag yang dimulai dengan `qcloud`, `tencent`, dan `project` karena dicadangkan untuk sistem.
  - Kunci tag hanya boleh berisi `angka`, `karakter alfabet`, `+=.@-`, dan harus kurang dari 255 karakter.
- Nilai tag: nilai tag hanya boleh berisi `string atau angka kosong`, `karakter alfabet`, `+=.@-`, dan harus kurang dari 127 karakter.


## Prasyarat
Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm).

## Petunjuk
### Mengedit tag dari satu instans
1. Pada halaman pengelolaan Instans, pilih instans yang tagnya perlu diedit dan klik **More** (Lainnya) > **Instance Settings** (Pengaturan Instans) > **Edit Tags** (Edit Tag), seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/29ad45e372fc78e28ab0ed69e73ec997.png)
2. Tambahkan, modifikasi, atau hapus tag di jendela pop-up “1 sumber daya cloud yang dipilih” berdasarkan kebutuhan Anda.

### Mengedit tag beberapa instans
> Anda dapat mengedit tag hingga 20 sumber sekaligus.
>
1. Pada halaman pengelolaan Instans, pilih instans yang tagnya perlu diedit dan klik **More Actions** (Tindakan Lainnya) > **Instance Settings** (Pengaturan Instans) > **Edit Tags** (Edit Tag) di bagian atas, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/d0e1965a2e256cae7b4dbdb7881ca9de.png)
2. Tambahkan, modifikasi, dan hapus tag di jendela pop-up “n sumber daya cloud yang dipilih” berdasarkan kebutuhan Anda.

## Contoh Operasi

Untuk informasi tentang cara menggunakan tag, harap lihat [Panduan Pengguna tentang Tag](https://intl.cloud.tencent.com/document/product/213/19548).
