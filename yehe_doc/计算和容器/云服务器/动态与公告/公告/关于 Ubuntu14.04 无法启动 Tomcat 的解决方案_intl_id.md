Kami telah terdeteksi bahwa ketika Tomcat atau Hadoop diinstal melalui perintah apt-get pada CVM Ubuntu14.04 yang dibeli dari Tencent Cloud, perangkat lunak ini dapat terhubung dengan port tetapi tidak dapat menanggapi permintaan. Kini, solusinya tersedia. Anda sebaiknya mengikuti petunjuk di bawah ini jika mengalami masalah ini. 

### Penyebab
Masalah ini disebabkan oleh [masalah Java Runtime Environment yang diketahui](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6202721).

### Analisis
Tomcat dan Hadoop dikembangkan menggunakan Java `java.security.SecureRandom` API.
API ini menggunakan `/dev/random` sebagai pembuat angka acak secara default di beberapa JRE. `/dev/random` mengakses derau lingkungan yang dikumpulkan dari perangkat seperti suhu CPU atau pengaturan waktu keyboard untuk menghasilkan entropi. Namun, lingkungan virtual CVM membuatnya sulit mengakses derau tersebut dan menghasilkan entropi, menyebabkan `cat /dev/random` untuk memblokir pemulaan Tomcat dan Hadoop.

### Solusi
#### Memodifikasi konfigurasi JRE
Harap ubah `securerandom.source=file:/dev/urandom` di `/etc/java-7-openjdk/security/java.security` asli (gunakan URL aktual) menjadi `securerandom.source=file:/dev/. /urandom` untuk mengatasi masalah ini.




