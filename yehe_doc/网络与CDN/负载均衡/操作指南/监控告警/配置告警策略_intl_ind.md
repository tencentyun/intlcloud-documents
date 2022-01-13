Anda bisa membuat alarm untuk memicu alarm dan mengirim pesan alarm ke grup pengguna tertentu jika produk Tencent Cloud memenuhi syarat yang dikonfigurasikan.Alarm yang dibuat bisa secara berkala menentukan apakah notifikasi alarm harus dikirimkan berdasarkan perbedaan di antara metrik yang dipantau dan ambang batas yang diberikan.

Pengguna tertentu bisa melakukan tindakan pencegahan atau perbaikan tepat waktu saat alarm terpicu.Oleh karena itu, alarm yang dibuat dengan tepat bisa membantu meningkatkan ketahanan dan keandalan aplikasi Anda.Untuk informasi selengkapnya mengenai alarm, silakan lihat [Membuat Kebijakan Alarm](https://intl.cloud.tencent.com/document/product/248/38908).

Anda bisa membuat kebijakan alarm dengan langkah berikut:
1.Masuk ke [Konsol Monitor Cloud](https://console.cloud.tencent.com/monitor/overview).
2.Klik **Alarm Configuration** (Konfigurasi Alarm) > **Alarm Policy** (Kebijakan Alarm) di bilah sisi kiri untuk masuk ke [halaman konfigurasi kebijakan alarm](https://console.cloud.tencent.com/monitor/policylist).
3.Klik **Add** (Tambahkan) untuk mengonfigurasi kebijakan alarm.
4.Konfigurasikan item dasar seperti yang ditunjukkan di bawah ini:
- Nama Kebijakan: masukkan nama kebijakan.
- Keterangan: tambahkan keterangan pada kebijakan.
- Tipe Kebijakan: pilih metrik pemantauannya.
- Proyek: pilih proyek sesuai kebutuhan.

5.Konfigurasikan objek alarm.
- Jika Anda memilih "semua objek", kebijakan alarm akan diasosiasikan dengan semua instance di bawah akun saat ini.
- Jika Anda memilih "beberapa objek", kebijakan alarm akan diasosiasikan dengan instance terpilih.
- Jika Anda memilih "grup Instance", kebijakan alarm akan diasosiasikan dengan grup instance terpilih.

6.Atur pemicu alarmnya.Anda bisa memilih satu templat syarat pemicu atau mengonfigurasikan syarat-syarat pemicu.
- Templat syarat pemicu
Aktifkan "Templat Syarat Pemicu" dan pilih templat yang dikonfigurasi dari daftar drop-down.Untuk konfigurasi selengkapnya, silakan lihat [Mengonfigurasi Templat Syarat Pemicu](https://intl.cloud.tencent.com/document/product/248/38911).Jika templat yang baru saja dibuat tidak ditampilkan, klik **Refresh** di sebelah kanan.
- Konfigurasikan syarat pemicu
Pemicu alarm adalah syarat semantik yang terdiri dari metrik, periode statistik, hubungan perbandingan, ambang batas, durasi, dan frekuensi notifikasi.
Contohnya, metrik yang ditentukan adalah `paket masuk`, periode statistik `1 menit`, hubungan perbandingannya `>`, ambang batasnya `100 paket/dtk`, durasinya `2 periode`, dan frekuensi notifikasinya `satu kali per hari`, maka jumlah paket masuk akan dikumpulkan satu kali setiap menit, dan alarm akan terpicu satu kali per hari jika jumlah paket masuk pendengar CLB melebihi 100 paket/dtk dua kali berturut-turut.

7.Konfigurasikan saluran alarm.Konfigurasikan grup penerima, periode valid, dan saluran penerima (email dan objek) sesuai kebutuhan.

8.Konfigurasikan callback API opsional sesuai kebutuhan.Masukkan URL yang bisa diakses melalui jaringan publik sebagai alamat API callback (nama domain atau IP[:port][/jalur]), dan Cloud Monitor akan segera mendorong pesan alarm ke alamat ini.

9.Setelah menyelesaikan konfigurasi, klik **Complete** (Selesai).

