## 1\. LATAR BELAKANG

Modul ini berlaku jika Anda menggunakan Cloud Firewall (“**Fitur**”). Modul ini tergabung dalam Perjanjian Keamanan dan Pemrosesan Data yang terdapat di ("[DPSA](https://intl.cloud.tencent.com/document/product/301/17347))". Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, Modul inilah yang akan berlaku apabila terjadi inkonsistensi.

## 2\. PEMROSESAN

Kami akan memproses data berikut sehubungan dengan fitur:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Aset:** informasi tentang aset Tencent Cloud Anda (host, alamat IP publik, layanan web, gateway, VPC, subnet, dan database) yang dilindungi oleh Fitur ini: ID/nama instans aset, alamat IP, jenis aset, wilayah, jaringan pribadi, label sumber daya, tag sumber daya, bandwidth puncak masuk dan keluar, lalu lintas kumulatif masuk dan keluar, serangan siber, port terbuka, kerentanan terbuka, dan keamanan host | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap dicatat bahwa data ini dibagikan dari fitur Tencent Cloud kami yang lain (sesuai dengan konfigurasi dan izin akses Anda), disimpan di fitur TencentDB for MySQL ("**MySQL**") dan Gudang Data Cloud ("**Clickhouse**") kami, dan dicadangkan di fitur Cloud Object Storage ("**COS**") kami. |
| **Data Bisnis CFW:** bandwidth masuk dan keluar, laju aliran kumulatif masuk dan keluar, nama loophole, port terbuka, data konfigurasi firewall (aturan kontrol akses, aturan perlindungan pertahanan intrusi, model perlindungan pertahanan intrusi, daftar larangan, daftar rilis, daftar isolasi, konfigurasi probe honeypot, konfigurasi jaringan honeypot, templat alamat), data konfigurasi firewall lainnya (data on dan off firewall, data konfigurasi instans NATFW) | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap dicatat bahwa data ini disimpan di fitur MySQL dan Clickhouse kami, dan dicadangkan dalam fitur COS. |
| **Data Penyerang:** log data informasi penyerang yang akan diidentifikasi atau dihalang: Alamat IP, lokasi geografis, paket serangan (termasuk payload), jenis serangan, jenis peristiwa serangan, pelacakan serangan, dan informasi penyerang | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap dicatat bahwa data ini disimpan di fitur MySQL dan Clickhouse kami, dan dicadangkan dalam fitur COS. |
| **Data Log:** <br/><li>Log kontrol akses (yang berisi data termasuk arah aturan, waktu hit, sumber akses, port sumber, tujuan akses Anda, port tujuan, perjanjian (perjanjian layanan komunikasi jaringan, TCP, UDP, dan HTTP), kebijakan yang berlaku); <br/><li>Log pencegahan intrusi (yang berisi data termasuk jenis peristiwa serangan, tingkat risiko, sumber akses eksternal, port sumber, tujuan akses Anda, port tujuan, perjanjian (perjanjian layanan komunikasi jaringan, TCP, UDP dan HTTP), waktu kejadian, kebijakan, sumber keputusan); <br/><li>Log lalu lintas (yang berisi data termasuk arah lalu lintas, waktu, sumber akses eksternal, port sumber, tujuan akses Anda, port tujuan, perjanjian (perjanjian layanan komunikasi jaringan, TCP, UDP, dan HTTP), stream byte, wilayah, operator); dan <br/><li>Log operasi (yang berisi data termasuk waktu, pengoperasian akun, jenis operasi, perilaku operasi, detail operasi, tingkat risiko) | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda, termasuk memungkinkan Anda meninjau log yang berkaitan dengan aset dan/atau serangan terhadap aset Anda.<br/>Harap dicatat bahwa data ini disimpan dalam fitur Elasticsearch Service, dan dicadangkan dalam fitur COS kami. |

## 3\. WILAYAH LAYANAN

Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-PROSESOR

Sebagaimana ditentukan dalam DPSA.

## 5\. RETENSI DATA

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut (kecuali diwajibkan lain oleh Undang-Undang Perlindungan Data yang berlaku):

| **Informasi Pribadi** | **Kebijakan Retensi**                                         |
| ------------------------ | ------------------------------------------------------------ |
| Data Aset               | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 14 hari. |
| Data Bisnis CFW        | Secara default, kami menyimpan data tersebut selama 7 hari (kecuali kapasitas penyimpanan melebihi 50GB, di mana data tersebut akan dihapus lebih awal). Jika Anda membeli layanan analisis log dari Fitur ini (yang saling bergantung dengan fitur Message Queue CKafka), kami menyimpan data tersebut selama 6 bulan (untuk batas kapasitas penyimpanan yang Anda tentukan). Jika Anda mencapai batas kapasitas penyimpanan, data akan diganti saat bergulir. |
| Data Penyerang            | Secara default, kami menyimpan data tersebut selama 7 hari (kecuali kapasitas penyimpanan melebihi 50GB, di mana data tersebut akan dihapus lebih awal). Jika Anda membeli layanan analisis log dari Fitur ini (yang saling bergantung dengan fitur Message Queue CKafka), kami menyimpan data tersebut selama 6 bulan (untuk batas kapasitas penyimpanan yang Anda tentukan). Jika Anda mencapai batas kapasitas penyimpanan, data akan diganti saat bergulir. |
| Data Log                 | Secara default, kami menyimpan data tersebut selama 7 hari (kecuali kapasitas penyimpanan melebihi 50GB, di mana data tersebut akan dihapus lebih awal). Jika Anda membeli layanan analisis log dari Fitur ini (yang saling bergantung dengan fitur Message Queue CKafka), kami menyimpan data tersebut selama 6 bulan (untuk batas kapasitas penyimpanan yang Anda tentukan). Jika Anda mencapai batas kapasitas penyimpanan, data akan diganti saat bergulir. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.