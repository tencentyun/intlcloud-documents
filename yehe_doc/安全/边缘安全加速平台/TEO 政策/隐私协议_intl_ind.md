## 1\. PENGANTAR
Modul ini berlaku jika Anda menggunakan TencentCloud EdgeOne (“Fitur”). Modul ini tergabung dalam kebijakan privasi yang terdapat di [Kebijakan Privasi](https://intl.cloud.tencent.com/document/product/301/17345). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang ditentukan dalam Kebijakan Privasi. Jika terdapat perbedaan antara Kebijakan Privasi dan Modul ini, Modul inilah yang akan berlaku apabila terjadi inkonsistensi.
## 2\. PENGONTROLAN
Pengontrol informasi pribadi yang dijelaskan dalam Modul ini adalah sebagaimana yang ditentukan dalam Kebijakan Privasi.
## 3\. KETERSEDIAAN
Fitur ini tersedia untuk pengguna secara global.
## 4\. CARA KAMI MENGGUNAKAN INFORMASI PRIBADI
Kami akan menggunakan informasi dengan cara berikut dan sesuai dengan dasar hukum berikut:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      | **Dasar Hukum**                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Log Akses Node Edge:** Stempel waktu akses, alamat IP klien, alamat IP publik server node, host, port, URL, header HTTP yang diakses (permintaan HTTP dari pengguna akhir, seperti agen pengguna, referer, cookie), badan data POST (10 KB pertama), apakah ada serangan berbahaya, aturan keamanan yang dipicu | Kami menggunakan informasi ini untuk tujuan menyediakan Fitur kepada Anda, termasuk:<li>untuk pertanyaan pengguna tentang lalu lintas bisnis dan status akses teratas dengan berbagai dimensi (seperti URL, UA);<li>menganalisis risiko lalu lintas dan mengidentifikasi karakteristik berbahaya; dan<li>memecahkan masalah.<br/>Harap perhatikan bahwa data ini terintegrasi dengan fitur ClickHouse kami untuk tujuan penyimpanan dan pra-agregasi, serta disimpan juga dalam fitur Cloud Virtual Machine (CVM), Cloud Object Storage (COS), dan ClickHouse kami. | Kami memproses informasi ini karena merupakan hal yang penting bagi kami guna melaksanakan kontrak kami dengan Anda untuk menyediakan Fitur. |
| **Data Lalu Lintas:** Data lalu lintas akses dari setiap host pada IP server tunggal (lalu lintas masuk, lalu lintas keluar, jumlah permintaan) | Kami menggunakan informasi ini guna menghitung jumlah kunjungan pengguna untuk tujuan penagihan. <br/>Harap perhatikan bahwa data ini terintegrasi dengan fitur ClickHouse kami untuk tujuan penyimpanan dan pra-agregasi, serta disimpan dan dicadangkan juga dalam fitur TencentDB for MySQL kami. | Kami memproses informasi ini karena merupakan hal yang penting bagi kami guna melaksanakan kontrak kami dengan Anda untuk menyediakan Fitur. |
| **Data Konfigurasi Sistem:** Data konfigurasi node (IP, ISP, alamat), data konfigurasi kluster server, data konfigurasi API, alamat dan kunci DB | Kami menggunakan informasi ini untuk tujuan menyediakan Fitur kepada Anda, termasuk memastikan bahwa content delivery network (CDN) berfungsi dengan benar. <br/>Harap perhatikan bahwa data ini disimpan dan dicadangkan dalam fitur TencentDB for MySQL kami. | Kami memproses informasi ini karena merupakan hal yang penting bagi kami guna melaksanakan kontrak kami dengan Anda untuk menyediakan Fitur. |
| **Data Log Akses API:** Stempel waktu akses, alamat IP klien, alamat IP intranet server API, URL, badan permintaan (termasuk data konfigurasi Anda), badan respons (termasuk data konfigurasi Anda) | Kami menggunakan informasi ini untuk tujuan pemecahan masalah. <br/>Harap perhatikan bahwa data ini terintegrasi dengan fitur Cloud Audit kami untuk menyediakan autentikasi CAM dan log audit, serta disimpan dalam fitur Cloud Log Service kami. | Kami memproses informasi ini karena merupakan hal yang penting bagi kami guna melaksanakan kontrak kami dengan Anda untuk menyediakan Fitur. |

## 5\. CARA KAMI MEMBAGIKAN DAN MENYIMPAN INFORMASI PRIBADI
Sebagaimana ditentukan dalam Kebijakan Privasi. 
Selain itu, APPID dan UIN disimpan dalam fitur TencentDB for MySQL kami.
## 6\. RETENSI DATA
Kami akan menyimpan informasi pribadi sesuai dengan hal-hal berikut:

| **Informasi Pribadi**          | **Kebijakan Retensi** |
| -------------------------           | -------------------- |
| Data Log Akses Node Edge        | Disimpan selama 30 hari.  |
| Data Lalu Lintas        | Disimpan selama 30 hari. Setelah itu, data tersebut dianonimkan. |
| Data Konfigurasi Sistem            | Kami menyimpan data tersebut selama Anda menggunakan Fitur. Apabila penggunaan Fitur Anda berakhir, kami akan menghapus data ini setelah 30 hari. |
| Data Log Akses API         | Disimpan selama 180 hari. |