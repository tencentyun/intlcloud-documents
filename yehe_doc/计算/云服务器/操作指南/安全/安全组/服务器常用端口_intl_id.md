
Dokumen ini menjelaskan port server umum. Untuk informasi selengkapnya tentang port aplikasi layanan untuk Windows, lihat [Ikhtisar Layanan dan Persyaratan Port Jaringan untuk Windows](https://support.microsoft.com/zh-cn/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB).

| Port | Layanan | Deskripsi |
|---------|---------|---------|
| 21 | FTP | Port server FTP terbuka untuk mengunggah dan mengunduh. |
| 22 | SSH | Port SSH untuk koneksi jarak jauh ke server Linux dalam mode CLI. |
| 25 | SMTP | Port server SMTP terbuka untuk mengirim email. |
| 80 | HTTP | Port untuk layanan web, seperti IIS, Apache, dan Nginx, untuk menyediakan akses eksternal. |
| 110 | POP3 | Port untuk layanan POP3 (protokol email 3). |
| 137, 138, 139 | Protokol NetBIOS | Port 137 dan 138 adalah port UDP untuk mentransfer file melalui My Network Places. <br>Port 139: koneksi yang dibuat melalui port 139 mencoba mengakses layanan NetBIOS/SMB. Protokol ini digunakan untuk berbagi file dan printer di Windows dan SAMBA. |
| 143 | IMAP | Port untuk Internet Message Access Protocol (IMAP) v2, yang merupakan protokol untuk menerima email seperti POP3. |
| 443 | HTTPS | Port untuk penjelajahan web. HTTPS adalah varian dari HTTP yang menyediakan enkripsi dan transmisi melalui port aman. |
| 1433 | SQL Server | Port default untuk SQL Server. Layanan SQL Server menggunakan dua port: TCP-1433 dan UDP-1434. Port 1433 digunakan untuk menyediakan layanan eksternal, dan port 1434 digunakan untuk menampilkan respons ke pemohon untuk menunjukkan port TCP/IP yang digunakan oleh SQL Server. |
| 3306 | MySQL | Port default untuk database MySQL, yang digunakan oleh MySQL untuk menyediakan layanan eksternal. |
| 3389 | Layanan Desktop Jarak Jauh Windows Server | Port layanan untuk desktop jarak jauh Windows Server, tempat Anda dapat menyambung ke server jauh menggunakan alat sambungan "Desktop Jarak Jauh". |
| 8080 | Port proksi | Mirip dengan port 80, port 8080 digunakan dalam layanan proksi WWW untuk penjelajahan web. Nomor port ":8080" sering ditambahkan ke URL saat Anda mengunjungi situs web atau menggunakan proksi. Selain itu, setelah server web Apache Tomcat diinstal, port layanan default-nya adalah port 8080. |
