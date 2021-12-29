## Versi Umum
### Struktur Data dan Deskripsi Fungsi
- **class ToaFetcher**
Kelas subjek yang digunakan untuk mengelola akuisisi dan pelepasan TOA.
- **InitUpToaFetcher**
 1. Deskripsi Fungsi 
Fungsi ini digunakan untuk menginisialisasi TOA fetcher.
```
bool InitUpToaFetcher(char *ncard_ip_str, char *svr_ip_str, u_short svr_port[], u_short svr_port_num, u_short cache_secs=TIMER_CACHE_SECS)
```
 2. Deskripsi Parameter Input
    - ncard_ip_str: Ini digunakan untuk mengidentifikasi string alamat IP dari antarmuka jaringan, misalnya, 10.75.132.39. Ini adalah NIC yang berkomunikasi dengan NIC klien.
- svr_ip_str: Ini adalah string alamat IP server, misalnya, 10.75.132.39. Ini digunakan untuk memfilter aliran TCP.
    - svr_port: Ini adalah daftar port server. Ini digunakan untuk memfilter aliran TCP. Maksimal dapat menambahkan tiga port. `svr_port` ataupun `port_range_ptr` harus dikonfigurasi.
    - svr_port_num: Jumlah port server.
    - port_range_ptr: Pointer array rentang port server, dengan elemen pointer yang menunjuk ke string. Format string rentang port adalah 10001 - 10005; maksimal dapat menambahkan 3 rentang. Ini digunakan dalam memfilter aliran TCP. `svr_port` ataupun `port_range_ptr` harus dikonfigurasi.
    - port_range_num: Jumlah rentang port server.
    - cache_secs: Panjang cache dalam hitungan detik. 15 detik secara default. Untuk detailnya, lihat `toa_fetcher.h: TIMER_CACHE_SECS`. TOA tidak akan disimpan lagi setelah cache kedaluwarsa.
 3. Nilai Pengembalian
    - TRUE: Berhasil membuat utas tambahan untuk mendapatkan TOA
    - FALSE: Gagal membuat utas tambahan untuk mendapatkan TOA
- **FetchToaValue**
 1. Deskripsi Fungsi
Fungsi ini digunakan untuk mendapatkan nilai TOA. Jika paket tcp-syn telah berinteraksi, TOA dapat diperoleh setelah menunggu hingga 1 milidetik. Biasanya, handshake tiga arah membutuhkan waktu lebih dari 1 milidetik.
```
bool FetchToaValue(u_long fake_client_ip_addr, u_short fake_client_port, u_long &real_client_ip_addr, u_short &real_client_port)
```
 2. Deskripsi Parameter Input
    - fake_client_ip_addr: Alamat IP palsu klien disimpan dalam urutan byte jaringan dan dapat diperoleh dari alamat pasangan yang dikembalikan oleh fungsi `accept` dari server.
    - fake_client_port: Nomor port palsu klien disimpan dalam urutan byte jaringan dan dapat diperoleh dari alamat pasangan yang dikembalikan oleh fungsi `accept` dari server.
    - real_client_ip_addr: Alamat IP klien yang nyata disimpan dalam urutan byte jaringan dan dapat diperoleh dari TOA.
    - real_client_port: Nomor port klien yang nyata disimpan dalam urutan byte jaringan dan dapat diperoleh dari TOA.
 3. Nilai Pengembalian
    - TRUE: TOA berhasil diperoleh.
    - FALSE: Gagal memperoleh TOA. Alasan umum mungkin karena TOA dihapus karena waktu cache terlampaui.
- **StopToaFetcher**
 1. Deskripsi Fungsi
Fungsi ini digunakan untuk menghentikan TOA fetcher.
```
void StopToaFetcher()
```
 2. Deskripsi Parameter Input
Tidak ada
 3. Nilai Pengembalian
Tidak ada].
- **GetFetcherStatus**
 1. Deskripsi Fungsi
Fungsi ini digunakan untuk mendapatkan status Fetcher.
```
int GetFetcherStatus()
```
 2. Deskripsi Parameter Input
Tidak ada].
 3. Nilai Pengembalian
    - 0: Menunjukkan status awal. Instans akan berada dalam status ini setelah diluncurkan. Dalam inisialisasi Fetcher, status awal tetap tidak berubah. Ketika terjadi kesalahan, -1 ditampilkan, dan ketika berhasil dijalankan, 1 ditampilkan.
    - -1: Menunjukkan pengecualian.
    - 1: Menunjukkan operasi normal.
- **FetchThreadHandler**
 1. Deskripsi Fungsi
Fungsi ini digunakan untuk mendapatkan pengendali utas tambahan TOA.
```
HANDLE FetchThreadHandler()
```
 2. Deskripsi Parameter Input
Tidak ada].
 3. Nilai Pengembalian
Pengendali utas tambahan TOA. Saat instans ToaFetcher dihentikan, pengendali akan ditutup.
- **FetchErrorInfo**
 1. Deskripsi Fungsi
Fungsi ini digunakan untuk mendapatkan kode kesalahan.
```
bool FetchErrorInfo(int* err_code_ptr, char* err_msg_ptr)
```
 2. Deskripsi Parameter Input
    - err_code_ptr: Pointer integer yang menunjuk ke kode kesalahan dan digunakan untuk menampilkan kode kesalahan.
    - err_msg_ptr: Pointer karakter yang menunjuk ke buffer string. Setidaknya 50 byte, dan digunakan untuk menampilkan pesan kesalahan.
 3. Nilai Pengembalian
    - TRUE: Berhasil diperoleh.
    - FALSE: Gagal diperoleh.

### Kode Kesalahan

| Kode | Pesan | Deskripsi |
|---------|---------|---------|
| 0	       | Ok	| Normal |
| -1001|Melebihi nomor port server maks |Jumlah maksimum port terlampaui. Periksa `InitUpToaFetcher: svr_port_num`. |
| -1002 | Alamat IP tidak valid	| Alamat IPv4 tidak valid. |
| -1003| Tidak ada antarmuka jaringan yang cocok| Tidak ditemukan antarmuka jaringan yang cocok |
| -1004| Kesalahan Sistem: menemukan kesalahan dev| Kesalahan sistem: `dev` tidak ditemukan. Hubungi developer lib. |
| -1005	| Kesalahan Sistem: kesalahan penghitung waktu mulai	|Kesalahan sistem: Kesalahan startup penghitung waktu. Hubungi developer lib. |
| -1006| Kesalahan Sistem: mengumpulkan kesalahan filter| Kesalahan sistem: Kesalahan pengumpulan aturan filter. Hubungi developer lib. |
| -1007	| Kesalahan Sistem: mengatur kesalahan filter	| Kesalahan sistem: Kesalahan konfigurasi aturan filter. Hubungi developer lib. |
| -1008	| Kesalahan Sistem: membuka kesalahan pcap |	Kesalahan sistem: kesalahan pengaktifan 'dev'. Hubungi developer lib. |
| -1009	| Kesalahan Sistem: memulai kesalahan pcap	|Kesalahan sistem: Kesalahan pengaktifan pendengaran. Hubungi developer lib. |
| -1010	| Kesalahan Sistem: memulai kesalahan utas	| Kesalahan sistem: Kesalahan pengaktifan utas. Hubungi developer lib. |
| -1999	| Kesalahan tidak diketahui	| Kesalahan yang tidak diketahui. Hubungi developer lib. |

### Contoh
- **Initialize ToaFetcher:** (Inisialisasi ToaFetcher)
```
char ncard_ip_str[] = "1.1.1.1";
char svr_ip_str[] = "1.1.1.1";
char port_range[3][100] = {"10001-10005", "20001-20005", "30001-30005"};
char* port_range_ptr[3] = {port_range[0], port_range[1], port_range[2]};
        u_short svr_port_list[3] = {1111, 2222, 3333};
        ToaFetcher inst = ToaFetcher();
        inst.InitUpToaFetcher((char*)ncard_ip_str, (char*)svr_ip_str, svr_port_list, 3);
```
- **Obtain TOA:** (Dapatkan TOA:)
```
void GetToa(SOCKADDR_IN client_addr, ToaFetcher * toa_fetcher_ptr)
{
	u_long fake_client_ip_addr = 0;
	u_short fake_client_port = 0;
	u_long real_client_ip_addr = 0;
	u_short real_client_port = 0;
	memcpy(&fake_client_ip_addr, &client_addr.sin_addr, 4);
	memcpy(&fake_client_port, &client_addr.sin_port, 2);
	bool ret = toa_fetcher_ptr->FetchToaValue(fake_client_ip_addr, fake_client_port, real_client_ip_addr, real_client_port);
	if(ret == FALSE){
		printf("No toa found\n");
	}else{
    	//fpp: Fungsi cetak khusus
		fpp("real_client_ip_addr", &real_client_ip_addr, 4);	
　　fpp("real_client_port", &real_client_port, 2);
	}
}
```

## Versi Go
Program yang memperoleh TOA mendapatkan alamat IP nyata dari toa_win.exe melalui komunikasi UDP.
### Format Protokol
- ** Request:** (Permintaan:) `| ID（4Bytes）|  FakeIPAddress（4Bytes）| FakePort（2Bytes）|`
 **Kolom dijelaskan sebagai berikut:**
 - ID: 4 byte. ID permintaan yang unik. Ini akan ditampilkan dalam respons apa adanya.
 - FakeIPAddrss: 4 byte. Alamat IP palsu klien disimpan dalam urutan byte jaringan dan dapat diperoleh dari alamat pasangan yang dikembalikan oleh fungsi `accept` dari server.
 - FakePort: 2 byte. Nomor port palsu klien disimpan dalam urutan byte jaringan dan dapat diperoleh dari alamat pasangan yang dikembalikan oleh fungsi `accept` dari server.

- **Response:** (Respons:) `| ID（4Bytes）| Code（1Byte）| RealIPAddress（4Bytes）| RealPort（2Bytes）|`
**Kolom dijelaskan sebagai berikut:**
 - ID: 4 byte. ID permintaan yang unik, sama dengan yang ada di string permintaan.
 - Code: 1 byte. 0: IP dan Port nyata berhasil diperoleh. 1: Gagal diperoleh.
 - RealIPAddress: 4 byte. Urutan byte jaringan. Ketika Code=0, ini menunjukkan alamat IP klien yang nyata.
 - RealPort: 2 byte. Urutan byte jaringan. Ketika Code=0, ini menunjukkan Port klien yang nyata.

### Sampel
Untuk detailnya, lihat demo.go. Anda dapat mengembangkan klien yang memperoleh TOA, atau Anda dapat menggunakan fungsi `queryTOA` di demo.go untuk mendapatkan TOA.
1. **Function Description** (Deskripsi fungsi)
```
func queryToa(serverAddr string, fakeIp string, fakePort uint16)(int32, string, uint16)
```
2. **Input Parameters Description** (Deskripsi Parameter Input)
 - serverAddr: Jenis string, alamat komunikasi layanan toa_win.exe. Format: 127.0.0.1:9999.
 - fakeIp: Jenis string, alamat IP palsu. Format 1.2.3.4.
 - fakePort: tipe uint16, port palsu. Format: 8899.
3. **Return Values** (Nilai Pengembalian)
 - Nilai pengembalian pertama: tipe int32. Digunakan untuk menunjukkan kode kesalahan.
    - 0: Berhasil diperoleh
    - -1: Tidak dapat memperoleh TOA. Ini dapat terjadi jika `fakeIP` dan `fakePort` salah, atau cache kedaluwarsa.
    - -2: Kegagalan pengecualian komunikasi jaringan.
 - Nilai pengembalian kedua: Jenis string. Mengembalikan IP nyata ketika TOA berhasil diperoleh, jika tidak, ini adalah string kosong.
 - Nilai pengembalian ketiga: jenis uint16. Mengembalikan Port nyata ketika TOA berhasil diperoleh. Jika tidak, ini adalah 0.
