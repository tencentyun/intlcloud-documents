# Menyimpan Log CDN Secara Teratur

Dokumen ini menguraikan cara menggunakan Tencent Cloud SCF untuk membuat dua fungsi untuk menyimpan log CDN secara teratur ke dalam COS.

# Langkah Utama

Dokumen ini menguraikan cara membuat fungsi "penyimpanan" dan "distribusi tugas", menggunakannya bersama, dan mengonfigurasi pemicu pencatat waktu untuk menyimpan log CDN secara teratur ke dalam COS.

Ada empat langkah utama:

A. Siapkan kunci akses Tencent Cloud API dan informasi COS

B. Buat fungsi penyimpanan (cdn-save-log-into-cos)

C. Buat fungsi tugas (cdn-dispatch-log-jobs)

D. Konfigurasikan pencatat waktu

# Petunjuk

## A. Siapkan sumber daya berikut sebelum membuat fungsi

1.Kunci akses Tencent Cloud API

Masuk ke [halaman pengelolaan kunci akses](https://console.cloud.tencent.com/cam/capi), minta atau buat kunci, dan rekam informasi berikut:

Nama kredensial akses (`SecretId`), seperti `AKIDRVI54XXn10r58oZpmzbBOnwt47xO1LRv`

Kunci kredensial akses (`SecretKey`), seperti `3t0SYPHRIpjmAAUPfKM8b4yXnff4Aq56`

2.Bucket COS

Masuk ke [Konsol COS](https://console.cloud.tencent.com/cos), akses **Bucket List** (Daftar Bucket) untuk mengueri atau membuat bucket, akses bucket untuk melihat **Basic Information** (Informasi Dasar)-nya, dan rekam informasi berikut:

Nama bucket (`Nama Bucket`), seperti `examples-1251002854`

Wilayah bucket (`Wilayah`), seperti `ap-chengdu`

## B. Buat fungsi penyimpanan (cdn-save-log-into-cos)

1.Masuk ke [Konsol SCF](https://console.cloud.tencent.com/scf) dan klik **Function Service** (Layanan Fungsi).

2.Pilih **Create** (Buat) dan masukkan **cdn-save-log-into-cos** sebagai nama fungsi.

3.Pilih **Function Template** (Templat Fungsi), cari dengan kata kunci "CDN", pilih templat "cdn-save-log-into-cos", dan klik "Next" (Selanjutnya) untuk mengakses halaman konfigurasi fungsi:
![](https://main.qcloudimg.com/raw/402a01a22ca748386617afd2fc7255a2.png)

4.Klik **Complete** (Selesai) untuk membuat fungsi.
![](https://main.qcloudimg.com/raw/69f87dc5f7314f0cdb21f45684b403ed.png)

## C. Buat fungsi tugas (cdn-dispatch-log-jobs)

1.Masuk ke [Konsol SCF](https://console.cloud.tencent.com/scf) dan klik **Create** (Buat).

2.Pilih **Function Template** (Templat Fungsi), cari dengan kata kunci "CDN", dan pilih templat "cdn-dispatch-log-jobs".

3.Masukkan **cdn-dispatch-log-jobs** sebagai nama fungsi dan klik "Next" (Selanjutnya).

4.Klik **Complete** (Selesai) untuk membuat fungsi.

![](https://main.qcloudimg.com/raw/b82b157292163ca06b9f43e74bd1a8de.png)

5.Klik tab **Function Code** (Kode Fungsi).Di kotak pengeditan kode, ubah kode Python dengan memasukkan informasi konfigurasi berikut:

Pada variabel `konfig` di baris 143, masukkan informasi konfigurasi yang sesuai:

- Atur bidang, seperti `secret_id`, `secret_key`, `cos_region`, `cos_bucket`, dan `scf_region`.
- Jika Anda mengatur nama fungsi sesuai petunjuk pada langkah B dan tidak ingin mengubahnya, Anda dapat menyimpan nilai asli `scf_function`.
- Nilai default `cdn_host` merupakan suatu array kosong (yaitu, log semua nama domain di bawah akun yang akan disimpan).Jika perlu, Anda dapat memasukkan daftar nama domain tertentu.

![](https://main.qcloudimg.com/raw/8ed596f7843acacc0e3974057922cd0d.png)

6.Klik **Save** (Simpan).

7.Klik **Test** (Uji) untuk menguji apakah kode tersebut berjalan dengan benar.Setelah program pengujian berhenti, Anda dapat mengakses Konsol COS dan memeriksa apakah log yang sesuai tersimpan di COS.

## D. Konfigurasikan pencatat waktu

Setelah Anda membuat dua fungsi di atas, daftar di Konsol SCF akan seperti yang ditunjukkan di bawah ini:

1.Klik **cdn-dispatch-log-jobs** untuk mengakses perinciannya.

![](https://main.qcloudimg.com/raw/55382244ab24832e280b040f284cd09a.png)

2.Klik tab **Trigger Management** (Pengelolaan Pemicu) dan klik **Create a Trigger** (Buat Pemicu).

![](https://main.qcloudimg.com/raw/36949d35a75f77515caacee834427064.png)

3.Pilih **Scheduled triggering** (Pemicuan terjadwal) sebagai metode pemicu, masukkan nama tugas terjadwal khusus, pilih **Every 5 mins** (Setiap 5 menit) sebagai periode pemicu, dan klik **Submit** (Kirim).

![](https://main.qcloudimg.com/raw/fe157cb0c234693920c3efc36ed9c7e3.png)

Setelah Anda menyelesaikan semua langkah di atas, log CDN akan disimpan secara teratur ke COS.