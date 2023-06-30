### Aturan Pencocokan

Instans cadangan (RI) yang dibeli secara otomatis dicocokan dengan instans prabayar selama jangka waktu RI. Untuk saat ini, hanya instans Windows、Linux yang didukung. Jika tidak memiliki instans yang sesuai dengan spesifikasi RI, RI akan tidak aktif tetapi tetap dikenakan biaya. Saat membeli instans dengan spesifikasi yang sesuai, RI akan langsung mencocokkannya dan manfaat berlaku.  

- RI secara otomatis dicocokan dengan instans bayar sesuai pemakaian tanpa intervensi manual.
- Manfaat penagihan RI dapat berlaku hingga maksimum 3.600 detik (satu jam) penggunaan instans per jam. Anda dapat menjalankan beberapa instans secara bersamaan, tetapi hanya dapat menerima manfaat diskon RI untuk total 3.600 detik per jam; penggunaan instans yang melebihi 3.600 detik dalam satu jam dibebankan dengan tarif bayar sesuai pemakaian. 

Misalnya, jika Anda membeli satu S3.16xlarge256 RI di Silicon Valley Zona 1, dan menjalankan tiga instans S3.16xlarge256 bayar sesuai pemakaian dari atribut yang sama secara bersamaan di zona ketersediaan yang sama selama satu jam, satu instans dikenakan biaya satu jam penggunaan RI dan dua instans lainnya dikenakan biaya dua jam penggunaan bayar sesuai pemakaian. 

Namun, jika Anda membeli satu S3.16xlarge256 RI di Silicon Valley Zone 1 dan menjalankan tiga instans bayar sesuai pemakaian (A, B, dan C) dari atribut yang sama di zona ketersediaan yang sama masing-masing selama 20 menit dalam jam, total waktu berjalan untuk instans adalah satu jam, yang menghasilkan satu jam penggunaan RI dan 0 jam penggunaan bayar sesuai penggunaan, seperti yang ditunjukkan di bawah ini.

![1558602502993](https://main.qcloudimg.com/raw/a812f74455b8b9d8ebbc84e90e26bc04.png)

Jika tiga instans yang memenuhi syarat berjalan secara bersamaan, manfaat penagihan RI diterapkan ke semua instans pada waktu yang sama hingga maksimum 3.600 detik dalam satu jam; setelah itu, harga bayar sesuai pemakaian berlaku.

![1558602155668](https://main.qcloudimg.com/raw/24926b2c2675e2d6959adcf62054f5b1.png)

#### Waktu efektif

RI ditagih setiap jam. RI ini berlaku pada jam sebelumnya dari waktu pembuatan dan kedaluwarsa pada jam berikutnya dari waktu kedaluwarsa. 

Contoh 1: misal Anda membeli CVM R1 berjangka 1 tahun pada 25 Mei 2019 11:15:24, RI akan berlaku sejak 25 Mei 2019 11:00:00 hingga 25 Mei 2020 11:59:59.

Contoh 2: misal Anda membeli CVM R1 berjangka 1 tahun pada 25 Mei 2019 11:00:00, RI akan berlaku sejak 25 Mei 2019 11:00:00 hingga 25 Mei 2020 11:59:59.
