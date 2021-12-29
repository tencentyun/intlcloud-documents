Setelah menerima paket ACK handshake tiga arah dari soket pendengaran, kernel Linux memasuki status TCP_ESTABLISHED dari SYN_REVC. Kernel memanggil fungsi tcp_v4_syn_recv_sock.
Fungsi kait tcp_v4_syn_recv_sock_toa memanggil fungsi tcp_v4_syn_recv_sock yang asli terlebih dahulu, lalu mengekstrak OPSI TOA dari OPSI TCP dengan memanggil fungsi get_toa_data, dan menyimpannya di bidang sk_user_data.

Setelah panggilan di atas selesai, kernel memanggil inet_getname_toa hook inet_getname untuk mendapatkan IP sumber dan port. Ini pertama-tama memanggil inet_getname asli, dan memeriksa apakah bidang sk_user_data kosong. Jika IP dan port nyata dapat diekstrak dari bidang ini, nilai inet_getname yang ditampilkan akan diganti dengan dua nilai ini.

Program server memanggil getpeername dalam mode pengguna, dan IP asli dan port klien akan ditampilkan.
