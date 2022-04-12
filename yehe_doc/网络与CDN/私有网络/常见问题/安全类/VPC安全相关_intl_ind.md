### Bagaimana Cara Memastikan Keamanan CVM di Instans VPC?
VPC sendiri adalah lingkungan jaringan yang terisolasi secara logis, dan lalu lintas dapat dikontrol dengan mengonfigurasi grup keamanan dan ACL jaringan:
- Grup keamanan: menyediakan kontrol lalu lintas jaringan untuk CVM di tingkat instans. Lalu lintas yang tidak diizinkan untuk masuk atau keluar dari instans secara otomatis ditolak.
- [ACL Jaringan](https://intl.cloud.tencent.com/document/product/215/31850): menyediakan kontrol lalu lintas jaringan tingkat subnet.
