Berikut ini menjelaskan port server umum. Untuk informasi selengkapnya tentang port aplikasi layanan untuk Windows, lihat dokumen resmi Microsoft ([Ikhtisar Layanan Windows dan Persyaratan Port Jaringan](https://support.microsoft.com/zh-cn/help/832017/service-overview-and-network-port-requirements-for-windows?spm=5176.7740724.2.3.omd4DB%3Fspm%3D5176.7740724.2.3.omd4DB)).

| Nomor Port | Layanan | Deskripsi |
|---------|---------|---------|
| 21 | FTP | Port server FTP terbuka untuk mengunggah dan mengunduh. |
| 22 | SSH | Port 22 adalah port SSH. Ini digunakan untuk terhubung dari jarak jauh ke server Linux dalam mode CLI. |
| 25 | SMTP | Port terbuka server SMTP untuk mengirim email. |
| 80 | HTTP | Port ini digunakan untuk layanan web seperti IIS, Apache, dan Nginx untuk menyediakan akses eksternal. |
| 110 | POP3 | Port 110 terbuka untuk layanan POP3 (protokol email 3). |
| 137, 138, 139 | Protokol NetBIOS | Port 137 dan 138 adalah port UDP untuk mentransfer file melalui My Network Places. <br>Port 139: koneksi melalui port 139 mencoba mengakses layanan NetBIOS/SMB. Protokol ini digunakan untuk berbagi file dan printer di Windows dan SAMBA. |
| 143 | IMAP | Port 143 utamanya digunakan untuk Internet Message Access Protocol (IMAP) v2, protokol untuk menerima email yang serupa dengan POP3. |
| 443 | HTTPS | Port penelusuran web. HTTPS adalah jenis HTTP lain yang menyediakan enkripsi dan transmisi melalui port aman. |
| 1433 | SQL Server | Port 1433 adalah port default untuk SQL Server. SQL Server menggunakan dua port: port 1433 untuk TCP dan port 1434 untuk UDP. Port 1433 digunakan untuk SQL Server untuk menyediakan layanan eksternal, sedangkan port 1434 digunakan untuk menanggapi pemohon mengenai port TCP/IP yang digunakan oleh SQL Server. |
| 3306 | MySQL | Port 3306 adalah port default untuk database MySQL dan digunakan untuk menyediakan layanan eksternal. |
| 3389 | Windows Server Remote Desktop Services | Port 3389 adalah port untuk layanan desktop jarak jauh di Windows 2000/2003 Server yang memungkinkan Anda terhubung ke server jauh menggunakan alat sambungan Desktop Jarak Jauh. |
| 8080 | Port proksi | Mirip dengan port 80, port 8080 digunakan untuk layanan proksi WWW untuk penjelajahan web. Ekstensi nomor port ":8080" sering ditambahkan ke URL saat pengguna mengunjungi situs web atau menggunakan server proksi. Selain itu, setelah server web Apache Tomcat diinstal, port layanan defaultnya adalah port 8080. |
