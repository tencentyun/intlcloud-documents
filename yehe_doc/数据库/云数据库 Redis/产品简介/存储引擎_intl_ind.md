## Mesin Edisi Memori
Mesin Edisi Memori memberikan pengalaman Redis asli dan mendukung berbagai skenario. Mesin ini mendukung arsitektur deployment standar dan kluster Redis untuk memenuhi persyaratan skenario bisnis yang berbeda.

Edisi yang didukung oleh mesin Edisi Memori meliputi:
 - [Edisi Memori (arsitektur standar)](https://intl.cloud.tencent.com/zh/document/product/239/31959): ketika jumlah replika lebih besar dari 0, data disinkronkan antara node master dan node replika (slave) secara real-time. Ketika node master gagal, failover otomatis akan dilakukan dalam hitungan detik, dan node replika akan mengambil alih bisnis dengan cara yang tidak terlihat. Arsitektur master/slave menjamin ketersediaan layanan sistem yang tinggi dan menyediakan kapasitas penyimpanan 0,25–64 GB.
 - [Edisi Memori (arsitektur kluster)](https://intl.cloud.tencent.com/document/product/239/18336): instans kluster menggunakan arsitektur terdistribusi, yang memungkinkan pemilihan kuantitas pecahann, kapasitas pecahann, dan kuantitas replika yang fleksibel dan memungkinkan penskalaan yang tidak terlihat oleh bisnis. Ini menyediakan kapasitas penyimpanan 2 GB–8 TB dan kinerja puluhan juta QPS.
