## Ikhtisar Tabel
Seperti di database lain, tabel di TcaplusDB adalah kumpulan data sebagai kombinasi data bisnis yang disimpan berdasarkan definisi tabel.
Dari perspektif bisnis game, sebuah tabel dapat mengelola sekumpulan data terkait modul bisnis seperti tabel pengguna dan tabel item.

Misalnya, tabel pemain di bawah ini dapat menyimpan informasi semua pemain dalam game seperti nama karakter game, jenis kelamin, ras, level, kekuatan, senjata, tunggangan, dan item.
```
{
player_id:11474,
player_name: "Test account 2",
gender:0,
ethnicity:"Elf",
FightingPower:10,
equipment:
	{
		helmet:0,
		Warframe:0,
		gloves:0,
		necklace:0,
		pants:0,
		Shoes:0
	},
horse:"0"
}，
{
player_id:11475,
player_name: "Test account 1",
gender:1,
ethnicity:"Orc",
FightingPower:1477,
equipment:
	{
		helmet:1478,
		Warframe:21,
		gloves:554,
		necklace:12,
		pants:64,
		Shoes:122
	},
horse:"3"
}
```


### Catatan
Catatan adalah sekumpulan nilai bidang dari objek yang sama. Dalam contoh tabel karakter pemain di atas, semua informasi karakter pemain terdiri dari beberapa nilai bidang atribut yang secara bersama-sama merepresentasikan kumpulan informasi karakter pemain dalam game. Sebuah catatan dapat berisi hingga 1 MB data.

## Bidang
Bidang menjelaskan atribut dari objek tertentu. Dalam contoh tabel karakter pemain di atas, atribut independen dari karakter pemain disebut bidang, seperti `player_name` dan `ethnicity`.

#### Bidang kunci utama
Seperti yang dapat ditemukan dari tabel contoh di atas, setiap catatan memiliki bidang yang menandai keunikannya. Bidang ini disebut bidang kunci utama. Pada tabel karakter pemain di atas, bidang kunci utama adalah `player_id` dan `player_name`. TcaplusDB mendukung hingga 4 bidang kunci utama.

#### Bidang umum
Selain bidang yang menandai keunikan catatan, setiap catatan juga memiliki atribut lain yang disebut bidang umum. Dalam contoh tabel karakter pemain di atas, bidang umum mencakup `equipment` dan `FightingPower`. TcaplusDB mendukung hingga 128 bidang umum.

#### Bidang sharding
TcaplusDB adalah sistem database terdistribusi yang dapat memberikan kemampuan permintaan bersamaan yang lebih tinggi untuk tabel. Jika Anda mengatur bidang sharding, TcaplusDB akan menghitung nilai hash-nya untuk menyesuaikan pecahan tabel secara otomatis berdasarkan kondisi akses tabel saat ini; jika tidak, sistem akan menggunakan bidang kunci utama sebagai bidang sharding.

Pengaturan bidang sharding sesuai dengan distribusi data backend. Anda perlu mengevaluasi apakah nilai bidang yang digunakan sebagai bidang sharding bersifat terpisah. Anda sebaiknya tidak mengatur bidang dengan nilai terbatas seperti jenis kelamin dan hari kerja sebagai bidang sharding; sebagai gantinya, Anda sebaiknya menggunakan bidang seperti ID dan nama.

#### Jenis bidang
TcaplusDB mendukung beberapa jenis data seperti yang dijelaskan di bawah ini:

| Jenis Bidang | Deskripsi |
|----------|--------------|
| int32 | Integer bertanda panjang variabel yang dapat merepresentasikan nilai antara \-2^31 dan \+2^31. Ini relatif tidak efisien untuk merepresentasikan bilangan negatif. |
| int64 | Integer bertanda panjang variabel yang dapat merepresentasikan nilai antara \-2^63 dan \+2^63. |
| uint32 | Integer tanpa tanda panjang variabel yang dapat merepresentasikan nilai antara 0 dan 2^32. |
| uint64 | Integer tanpa tanda dengan panjang variabel yang dapat merepresentasikan nilai antara 0 dan 2^64. |
| sint32 | Nilai `int` bertanda panjang variabel yang lebih efisien untuk merepresentasikan angka negatif dibanding `int32` biasa. |
| sint64 | Nilai `int` bertanda panjang variabel yang lebih efisien untuk merepresentasikan angka negatif dibanding `int64` biasa. |
| bool | Nilai Boolean yang merepresentasikan `True` atau `False`. |
| fixed32 | Jenis numerik dengan panjang tetap yang selalu mengambil 4 byte. Ini lebih efisien dari `uint32` jika nilainya umumnya di atas 2^28. |
| fixed64 | Tipe numerik dengan panjang tetap yang selalu mengambil 8 byte. Ini lebih efisien dari `uint64` jika nilainya umumnya di atas 2^56. |
| fixed32 | Jenis numerik dengan panjang tetap yang selalu mengambil 4 byte. |
| fixed64 | Tipe numerik dengan panjang tetap yang selalu mengambil 8 byte. |
| float | Titik floating biner 32-bit yang mengambil 4 byte. |
| double | Titik floating presisi ganda biner 64-bit yang mengambil 8 byte. |
| strings | String yang dikodekan dengan UTF\-8 atau ASCII 7-bit yang panjangnya tidak boleh melebihi 2^32. |
| byte | Urutan byte dengan panjang di bawah 2^32. |
| message | Jenis nested. Mendukung hingga 128 tingkat nested berturut-turut. Jumlah level nesting yang tinggi akan memengaruhi kinerja. |

### Format definisi tabel
TcaplusDB mendukung Protocol Buffers yang merupakan format penyimpanan data terstruktur yang ringan dan efisien dan utamanya digunakan untuk menyimpan data terstruktur secara berurutan.
Untuk informasi selengkapnya tentang format tabel, lihat [Bahasa Deskripsi Tabel](https://intl.cloud.tencent.com/document/product/1016/36559).
