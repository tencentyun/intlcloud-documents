## Ikhtisar
- **Replika data online realtime**
Snapshot adalah salinan disk cloud yang dapat digunakan secara maksimal. Saat terjadi masalah pada disk cloud tempat snapshot telah dibuat, Anda dapat menggunakan snapshot untuk memulihkan disk cloud dengan cepat ke status normal. Sebaiknya Anda untuk membuat snapshot untuk disk cloud sebelum membuat perubahan besar apa pun pada bisnis Anda, sehingga data dapat dengan cepat dipulihkan jika terjadi kegagalan perubahan bisnis.
- **Pencadangan terus-menerus pada tonggak pencapaian penting**
Snapshot dapat digunakan sebagai cadangan data bisnis yang terus-menerus untuk menjaga data bisnis pada tonggak pencapaian.
- **Deployment bisnis yang cepat**
Snapshot memungkinkan Anda mengkloning beberapa disk cloud dengan cepat untuk deplyment server yang cepat.

## Kasus Penggunaan
Snapshot menyediakan layanan perlindungan data yang nyaman dan efisien, yang dapat digunakan dalam skenario bisnis berikut:
- **Pencadangan data harian**
Anda dapat menggunakan snapshot untuk mencadangkan data bisnis penting secara rutin untuk menghindari kehilangan data yang disebabkan oleh kesalahan operasi, serangan, dan virus.
- **Pemulihan data dengan cepat**
Anda dapat membuat snapshot sebelum melakukan operasi besar, seperti mengubah sistem operasi, meningkatkan aplikasi, atau memigrasikan data bisnis. Jika terjadi masalah, Anda dapat menggunakan snapshot untuk memulihkan data bisnis.
- **Aplikasi beberapa replika data produksi**
Anda dapat membuat snapshot untuk data produksi guna menyediakan data yang mendekati realtime untuk aplikasi seperti penambangan data, kueri laporan, dan pengujian pengembangan.
- **Deployment lingkungan yang cepat**
Anda dapat membuat snapshot untuk instans CVM untuk membuat citra kustom, dan menggunakan citra kustom untuk membuat instans CVM untuk deployment batch dengan lingkungan yang sama dan waktu konfigurasi yang lebih sedikit.

## Penagihan
Untuk informasi selengkapnya tentang harga snapshot, lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/362/32415) dan [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).

## Batas Kuota
Untuk informasi selengkapnya tentang batas kuota snapshot, lihat [Batas Penggunaan](https://intl.cloud.tencent.com/document/product/362/32406).

## Jenis Snapshot
- **Snapshot manual**
Anda dapat membuat snapshot untuk disk cloud secara manual pada titik waktu tertentu. Snapshot ini dapat digunakan untuk membuat lebih banyak disk cloud dengan data yang identik, atau untuk memulihkan disk cloud ke titik waktu saat snapshot dibuat. Untuk informasi selengkapnya, lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755).
- **Snapshot terjadwal**
Untuk bisnis yang terus diperbarui, Anda dapat menggunakan snapshot terjadwal untuk menyediakan pencadangan data berkelanjutan. Untuk mencapai pencadangan berkelanjutan data disk cloud selama periode waktu tertentu, Anda hanya perlu mengonfigurasi kebijakan pencadangan dan mengaitkannya dengan disk cloud, yang secara signifikan meningkatkan keamanan data. Untuk informasi selengkapnya, lihat [Snapshot Terjadwal](https://intl.cloud.tencent.com/document/product/362/35238).

>?Selama pembuatan snapshot, data aplikasi yang disimpan dalam memori mungkin tidak disimpan terus-menerus. Dengan demikian, snapshot mungkin tidak menangkap data disk cloud terbaru dan terlengkap. Untuk informasi selengkapnya, lihat [Catatan](https://intl.cloud.tencent.com/document/product/362/5755#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9) untuk memastikan konsistensi data snapshot.


## Tinjauan Kasus
#### Kasus 1: Tidak ada snapshot manual yang dibuat sebelum melakukan operasi berisiko tinggi, yang mengakibatkan hilangnya data
Pelanggan A tidak pernah membuat snapshot untuk disk cloud. Pada Mei 2019, seorang operator melakukan uji fio pada disk cloud. Sistem file rusak. Data rusak dan tidak dapat dipulihkan.
**Analisis**: Jika pelanggan A telah membuat snapshot untuk disk cloud sebelum pengujian, snapshot dapat digunakan untuk memutar kembali data dan melanjutkan bisnis segera setelah kerusakan data.

#### Kasus 2: Tidak ada snapshot terjadwal yang dibuat untuk disk data penting, yang mengakibatkan hilangnya data
Pelanggan B membuat snapshot untuk beberapa disk cloud, kecuali yang dibeli setelah Januari 2019 karena alasan biaya. Pada Juni 2019, disk cloud tanpa perlindungan snapshot mengalami kehilangan data yang tidak dapat dipulihkan karena penghapusan data file lapisan sistem secara tidak sengaja.
**Analisis**: Jika pelanggan B telah membuat snapshot terjadwal untuk disk cloud ini, data dapat dipulihkan ke titik waktu saat snapshot terakhir dibuat, sehingga meminimalkan kerugian. Setelah insiden tersebut, pelanggan B membuat snapshot untuk disk cloud tersebut guna meningkatkan perlindungan data.

#### Kasus 3: Menggunakan snapshot terjadwal untuk memutar kembali data dan memulihkan bisnis setelah operasi yang salah
Pelanggan C membuat snapshot untuk semua disk cloud. Pada Mei 2019, pengecualian startup terjadi karena operasi yang salah.
**Analisis**: Pelanggan C segera memulihkan data menggunakan snapshot terjadwal yang dibuat dua hari lalu, dan bisnis tetap stabil.


Semua kasus ini melibatkan kehilangan data karena operasi yang salah, tetapi hasilnya berbeda. Sebagai perbandingan, kita dapat menemukan bahwa:
- Dalam situasi di mana **snapshot belum dibuat**, data jarang dapat dipulihkan saat pengecualian server atau disk cloud terjadi, yang mengakibatkan kehilangan dalam jumlah besar.
- Dalam situasi di mana **snapshot telah dibuat**, data dapat dipulihkan saat pengecualian server atau disk cloud terjadi, meminimalkan kehilangan.

Sebaiknya Anda membuat snapshot untuk bisnis secara teratur berdasarkan jenis bisnis, meningkatkan keamanan data, dan mencapai pemulihan bencana dengan biaya rendah dan efisiensi tinggi.

## Lainnya
Untuk pertanyaan lain, lihat [Pertanyaan Umum mengenai Snapshot](https://intl.cloud.tencent.com/document/product/362/17820).





