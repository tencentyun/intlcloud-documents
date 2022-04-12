
Dokumen ini menjelaskan tiga kebijakan isolasi sumber daya TencentDB for MySQL: dasar, umum, dan khusus.

>?
>- "Edisi Dasar" sebelumnya telah diganti namanya menjadi "node tunggal dasar", dan "Edisi IO Tinggi node tunggal" sebelumnya telah diubah namanya menjadi "node tunggal umum".
>- Instans dua node dan tiga node mendukung kebijakan umum dan khusus. Kebijakan khusus saat ini dalam versi beta; oleh karena itu, untuk membeli mesin virtual khusus, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

| Kebijakan Isolasi Sumber Daya | Deskripsi                                                         |
| -------- | ------------------------------------------------------------ |
| Dasar | Hanya instans node tunggal yang mendukung kebijakan ini. Instans node tunggal dasar (sebelumnya dikenal sebagai Edisi Dasar) mendukung pemisahan komputasi-penyimpanan dan menggunakan disk cloud sebagai penyimpanan dasar. |
| Umum | <li>Instans umum memiliki penggunaan eksklusif dari memori dan sumber daya disk yang dialokasikan, tetapi berbagi sumber daya CPU dengan instans umum lainnya pada mesin fisik yang sama. <li>Dengan berbagi sumber daya CPU, instans umum menikmati spesifikasi lebih tinggi dengan biaya lebih rendah. <li>Kapasitas disk instans umum tidak bergantung pada spesifikasi CPU dan memorinya. |
| Khusus | <li>Instans khusus memiliki penggunaan eksklusif dari CPU (CPU pinning yang dikonfigurasi), memori, dan sumber daya disk. Ini menawarkan performa stabil jangka panjang dan tidak akan terpengaruh oleh perilaku instans lain pada mesin fisik. <li>Instans khusus dengan konfigurasi tertinggi dapat memonopoli mesin fisik dan semua sumber dayanya. | 


