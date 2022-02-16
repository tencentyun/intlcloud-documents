Dokumen ini menjelaskan cara menggunakan alat klien tcaplus_client untuk mengakses data.

Semua pernyataan DML harus menggunakan klausa `WHERE` yang harus berisi setidaknya bidang kunci primer. Jika ada beberapa kunci primer, pisahkan dengan `and`.

## Mengakses TcaplusDB Melalui Alat Klien
tcaplus_client adalah alat klien yang digunakan untuk mengakses tabel TcaplusDB dan dapat diperoleh di alamat unduhan pada tabel di bawah.

Paket rilis TcaplusServiceAPI untuk Linux x86_64 berisi alat tcaplus_client untuk Linux 64-bit.

| Versi          | Tanggal Rilis   | OS     | Alamat Unduhan Paket                                                     |
| ------------- | ---------- | ------------ | ------------------------------------------------------------ |
| 3.46.0.199033 | 2020/12/28 | Linux x86_64 | [Download](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/release/3-46/TcaplusPbApi3.46.0.199033.x86_64_release_20201210.tar.gz) |

>?
>- Operasi berikut harus dilakukan pada instans CVM di VPC dan subnet yang sama di bawah akun Tencent Cloud Anda sebagai kluster TcaplusDB Anda.
>- Anda dapat mengunduh TcaplusServiceAPI v3.36.0.192960 [di sini](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz).

### Menginstal klien
Setelah mengunduh paket penginstalan TcaplusServiceAPI, Anda dapat [menggunakan alat unggah](https://intl.cloud.tencent.com/document/product/213/34821) untuk mengunggahnya ke instans CVM di VPC dan subnet yang sama dengan kluster TcaplusDB.

1. Selepas mengunggah, jalankan perintah berikut untuk mendekompresi paket penginstalan:
```
tar -xf TcaplusPbApi3.46.0.199033.x86_64_release_20201210.tar.gz -C tcaplus
```
2. Setelah dekompresi, masukkan direktori `bin` di `tcaplus` dan berikan izin yang dapat dieksekusi alat ini:
```
cd tcaplus/release/x86_64/bin
chmod +x tcaplus_client
```
3. Jalankan perintah `./tcaplus_client`, dan sistem akan meminta Anda memasukkan informasi parameter yang diperlukan untuk koneksi database. Anda dapat memasukkannya berdasarkan informasi kluster Anda.
>!Dalam contoh di bawah, `app_id` menunjukkan ID akses kluster, `App` menunjukkan kluster, dan `zone` menunjukkan grup tabel.


```
## ./tcaplus_client
--------------------------------------------------------------------------------
  parameter tidak valid, harap mulai klien sebagai berikut:

    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]

    parameter di [] bersifat opsional, dan urutannya tidak penting.

    -a(--ap_id)    ID Aplikasi

    -z(--zone_id)    ID ZONA

    -s(--signature)    KATA SANDI

    -d(--dir)    dir server addr

    -t(--table)    tabel untuk ditambahkan

    -l(--log)   nama file log yang harus berupa client_log.xml, dan nama kelas log menjadi klien

    -T(--tdr)    nama file tdr 

    -e(--execute) Perintah SQL harus dijalankan, konten harus dalam tanda kutip.

    Misalnya, ./tcaplus_client -a 2 -z 3 -s "FE6533875C8385C3" -d 172.25.40.181:9999 -T table_test.tdr -e "pilih a, b dari tabel dengan key = 1;" 
--------------------------------------------------------------------------------
```

### Menghubungkan ke TcaplusDB (skenario default)
Jalankan perintah yang sesuai untuk terhubung ke TcaplusDB. Informasi titik akses dalam contoh di bawah ini adalah sebagai berikut, dan tabel `tb_online` telah dibuat di grup tabel yang ID-nya 1:
- ID akses kluster: 2
- Kata sandi koneksi: test@Password1
- Alamat pribadi: port pribadi: 10.125.32.21:9999
- ID grup tabel: 1

```
./tcaplus_client -a 2 -z 1 -s "test@Password1" -d 10.125.32.21:9999
+------------------------------------------------------------------------------+
|    tcaplus_client x86_64  dibangun pada Rabu 18 Jan 22.08.38 CST 2017              |
|                                                                              |
|    Selamat datang!                                                                  |
+------------------------------------------------------------------------------+

tcaplus>
```

Masukkan `help` setelah perintah, dan Anda dapat melihat informasi bantuan mendetail. Masukkan `> help` untuk melihat cara menggunakan perintah terkait.
```
tcaplus>help
--------------------------------------------------------------------------------
      help: tampilkan penggunaan perintah, contoh: "help select;".
      show: mendapatkan informasi terkait status server. menjalankan "help show;" untuk detailnya.
      exit/quit: keluar dari klien.
     count: mencetak nomor catatan dalam database.
 
      desc: cetak nama dan jenis bidang tabel.
    select: catatan kueri dari database.
    insert: menyisipkan catatan baru ke dalam database.
   replace: mengganti catatan ke dalam database.
    update: memperbarui catatan dalam database.
    delete: menghapus catatan dari database.
 
      dump: membuang catatan dari database.
      load: memuat catatan ke dalam database.
--------------------------------------------------------------------------------
```

### Deskripsi parameter
| Parameter | Deskripsi                                          | Diperlukan |
| ---- | --------------------------------------------- | -------- |
| -a   | ID Akses                                       | Ya       |
| -z   | ID grup tabel                                     | Ya       |
| -s   | Kata sandi kluster                                      | Ya       |
| -d   | Port dan IP kluster                            | Ya       |
| -t   | Nama tabel                                        | Tidak       |
| -l   | Pengaturan output dari file log. Nama file harus berupa "client_log.xml". | Tidak       |
| -T   | Jalur file TDR                                  | Tidak       |
| -e   | Pernyataan SQL yang akan dieksekusi                           | Tidak       |
| -v   | Versi yang akan dikueri                                      | Tidak       |
| <    | Mengalihkan pernyataan SQL ke klien yang akan dieksekusi.                 | Tidak       |

### Menghubungkan ke TcaplusDB (menggunakan TDR)
Untuk terhubung ke TcaplusDB melalui TDR, Anda harus menggunakan parameter peluncuran klien untuk menentukan jalur file TDR. Anda dapat menggunakan [alat TDR](#tdrgj) untuk mengonversi beberapa database XML menjadi format biner. Jika ada dependensi antara beberapa file XML, file XML dependen harus ditempatkan di depan daftar parameter.

Sampel:
```
[root@test-PC0 /opt]# ./tcaplus_client -a 2 -z 3 -s C12901752D0D3347 -d 8.x.x.8:9999 -T /mnt/e/tdr/2.3.table_list.tdr
 
====== Selamat menggunakan tcaplus_client, gunakan "help" untuk menampilkan penggunaan ======
tcaplus > keluar

[root@test-PC0 /opt]# ./tcaplus_client -a 2 -z 3 -s C12901752D0D3347 -d 8.x.x.8:9999 -T /mnt/e/tdr/2.3.table_list.tdr -e "show tables;"
-------------------------------------------
| Nama Tabel                    Jenis      |
-------------------------------------------
| MTownRoleInfo                 GENERIC   |
| table_generic                 GENERIC   |
| table_generic_xiahuaxian      GENERIC   |
| table_list LIST |
| test_table GENERIC |
-------------------------------------------
```

<span id = "tdrgj"></span>

#### Alat TDR
Anda perlu menggunakan alat TDR untuk menghasilkan file TDR, yang terutama dihasilkan oleh file definisi data (struktur TDR dalam format XML). Unduh alat [di sini](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/tdr).

Sampel:
```
tdr -B -o ov_res.tdr ov_res.xml
        # Konversi basis metadata XML ke database biner TDR.
tdr -C -o ov_res.c --old_xml_tagset  ov_res.xml
        # Konversi metadatabase dalam format XML lama (menggunakan kumpulan tag lama) ke file .c.
tdr -H -O "include" --add_custom_prefix="m_" --no_type_prefix
        # Konversi metadata XML ke file .h yang disimpan di direktori "include".
        # Tambahkan awalan "m_" ke nama anggota struct/union, tetapi jangan tambahkan awalan tipe.
tdr -G -m Pkg -x ATTR -o Pkg.xml net_protocol.xml
        # Buat file konfigurasi dalam format XML melalui paket (paket struktur data yang disesuaikan oleh pengguna).
tdr -T -u prefixfile
        # Ekspor tabel awalan dari anggota data yang digunakan saat membuat file .h ke file "prefixfile".
tdr -A --indent-size=8 net_protocol.xml
        # Buat file kelas ActionScript3 sesuai dengan protokol yang dijelaskan dalam "net_protocol.xml". File kelas yang dihasilkan semuanya menjorok dengan 8 spasi.
tdr -P --indent-size=8 net_protocol.xml
        # Buat file kelas C++ sesuai dengan protokol yang dijelaskan dalam "net_protocol.xml". File kelas yang dihasilkan semuanya menjorok dengan 8 spasi.
tdr -S --indent-size=8 net_protocol.xml
        # Hasilkan file kelas C# sesuai dengan protokol yang dijelaskan dalam "net_protocol.xml". File kelas yang dihasilkan semuanya menjorok dengan 8 spasi.
tdr -E 0x83010404
        # Minta informasi kesalahan kode kesalahan 0x83010404.
```

#### Alat tdr2xml
Alat tdr2xml dapat mendekompilasi file metadata biner ke file metadata XML. Unduh alat [di sini](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/tdr2xml).

Sintaksis:
```
tdr2xml   [-o --out_file=FILE] [-h --help] [-v --version] DRFILE
Deskripsi setiap parameter adalah sebagai berikut:
-o, --out_file=FILE: tentukan nama file output. Nilai default: a.xml.
-h, --help: bantuan output.
-v, --version: menampilkan informasi versi.
```

Sampel:
```
tdr2xml –o net_cs.xml  net_cs.tdr
```
Konversikan file deskripsi metadata dalam format kustom biner yang disimpan dalam file "net_cs.tdr" menjadi file deskripsi dalam format XML.
