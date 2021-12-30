Anda dapat melihat semua detail HAVIP di wilayah tertentu di konsol HAVIP.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/).
2. Pilih **IP and Interface** (IP dan Antarmuka) > **HAVIP** di bilah sisi kiri untuk masuk ke halaman pengelolaan HAVIP.
3. Pilih wilayah target untuk melihat detail semua HAVIP yang telah diajukan.
	Deskripsi bidang adalah sebagai berikut:
	+ ID/Nama: ID mengacu pada ID HAVIP yang dibuat secara otomatis setelah dibuat. Anda dapat mengekliknya untuk melihat informasi dasar HAVIP. Nama ditentukan oleh pengguna saat HAVIP dibuat.
	+ Status: menunjukkan apakah HAVIP ditetapkan sebagai alamat IP floating di file konfigurasi perangkat lunak HA di CVM. HAVIP yang berhasil dikonfigurasi akan berstatus **Bound with CVM** (Terikat dengan CVM), atau berstatus **Not bound with CVM yet** (Belum terikat dengan CVM).
	+ Alamat: alamat HAVIP.
	+ Backend ENI: mengacu pada ID ENI dari CVM terikat. Jika HAVIP belum terikat dengan CVM, bidang ini akan ditampilkan sebagai **-**.
	+ Server: mengacu pada ID CVM terikat. Jika HAVIP belum terikat dengan CVM, bidang ini akan ditampilkan sebagai **-**.
	+ EIP: mengacu pada EIP terikat. Jika HAVIP belum terikat dengan EIP, bidang ini akan ditampilkan sebagai **-**.
	+ Virtual Private Cloud: mengacu pada VPC dari HAVIP.
	+ Subnet: mengacu pada subnet HAVIP.
	+ Waktu Aplikasi: mengacu pada waktu saat HAVIP ini diterapkan.
	+ Operasi: mengacu pada operasi yang didukung, termasuk **Bind** (Ikatkan), **Unbind** (Putuskan Ikatan), dan **Release** (Rilis).
	   + Ikatkan: mengikat EIP
	   + Putuskan ikatan: memutuskan ikatan EIP
	   + Rilis: merilis HAVIP
3. Masukkan ID, nama atau alamat di kotak pencarian di sebelah kanan untuk mencari HAVIP dengan cepat.
4. Klik ikon di sebelah kotak pencarian untuk memuat ulang halaman.
