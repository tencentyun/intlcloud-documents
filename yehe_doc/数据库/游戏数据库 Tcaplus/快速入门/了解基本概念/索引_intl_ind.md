## Ikhtisar Indeks
Anda dapat membuat indeks untuk tabel dan menggunakannya untuk mendapatkan data yang diinginkan dari database dengan cepat yang memberikan fleksibilitas lebih tinggi dalam kueri data untuk aplikasi Anda.

TcaplusDB mendukung dua jenis indeks:
- Indeks lokal: harus terdiri dari bidang kunci utama dan memungkinkan Anda untuk dengan cepat meminta data menggunakan kunci utama sebagai filter.
- Indeks global: dapat terdiri dari bidang apa pun kecuali bidang dalam jenis `message` dan memungkinkan Anda untuk dengan cepat meminta data menggunakan bidang yang dikonfigurasi dalam indeks global sebagai filter.

TcaplusDB mendukung hingga 1 indeks global dan 6 indeks lokal.

### Indeks lokal
Indeks lokal hanya dapat ditentukan selama pembuatan tabel dan hanya dapat terdiri dari bidang kunci utama. Titik temu semua kumpulan bidang indeks tidak boleh kosong.
Misalnya, tabel `HeroInfo` di bawah ini memiliki 4 bidang kunci utama: `heroId`, `heroName`, `heroFightingType`, dan `heroQuality`.
```
{
	heroId:1,
	heroName:"Arthur",
	heroFightingType:1,
	heroQuality:3
	heroSkill:{
		BasicSkill1:1,
		BasicSkill2:2,
		SpecialSkill:3
	},
	heroLevel:12,
	heroskin:2,
	heroAttackpower:141,
	heroPhysicalDefense: 283,
	heroMagicdefense:124
}
{
	heroId:4,
	heroName:"Shooter",
	heroFightingType:3,
	kualitas pahlawan: 4
	heroSkill:{
		BasicSkill1:1,
		BasicSkill2:2,
		SpecialSkill:3
	},
	heroLevel:11,
	heroskin:1,
	heroAttackpower:225,
	heroPhysicalDefense: 57,
	heroMagicdefense:41
}
```
Untuk tabel di atas, Anda dapat menggunakan kombinasi apa pun dari 4 bidang kunci utama untuk membuat indeks, tetapi titik temu dari semua indeks yang dibuat tidak boleh kosong. Misalnya, jika `heroId` digunakan sebagai bidang titik temu untuk perancangan indeks, indeks berikut dapat dibuat:
- heroId,heroName
- heroId,heroFightingType
- heroId,heroQuality
- heroId,heroName,heroFightingType
- heroId,heroFightingType,heroQuality
- heroId,heroName,heroFightingType,heroQuality
Anda dapat mengkueri data berdasarkan bidang dalam indeks yang dibuat. Buat indeks berdasarkan kebutuhan bisnis aktual; jika tidak, kinerja akan terganggu karena redundansi indeks.

### Indeks global
Dalam tabel `HeroInfo` di atas, Anda dapat mengkueri entri data menggunakan bidang dalam indeks lokal yang dibuat sebagai filter. Misalnya, jika ingin membuat kueri data dengan informasi seperti `heroLevel` dan `heroskin`, Anda dapat menambahkannya ke indeks global dan menggunakan bidang di dalamnya untuk mengkueri data.
Harap perhatikan bahwa indeks global juga tidak mendukung jenis nested seperti bidang `heroSkill` dalam tabel contoh di atas.
