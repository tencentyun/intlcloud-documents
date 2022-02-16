TencentDB for TcaplusDB mendukung dua bahasa definisi tabel: Protocol Buffer (Protobuf) dan Tencent Data Representation (TDR).
Protobuf adalah metode serialisasi data terstruktur yang dikembangkan oleh Google yang menekankan kemudahan dan kinerja.
TDR adalah bahasa deskripsi data netral platform yang dikembangkan oleh Tencent, yang menggabungkan keunggulan XML, bahasa biner, dan pemetaan relasional objek (ORM), dan banyak digunakan dalam skenario serialisasi data game Tencent.
Kedua bahasa itu sama-sama sangat berguna. Gunakan salah satunya berdasarkan kebiasaan penggunaan Anda.
Dokumen ini menjelaskan cara mendefinisikan tabel di TDR.

## Definisi Tabel di TDR

TDR mendukung tabel GENERIC dan tabel LIST. Tabel GENERIC merepresentasikan atribut elemen dalam bentuk tabel, seperti siswa, pemberi kerja, dan pemain game. Tabel LIST adalah daftar catatan, seperti papan peringkat game dan email dalam game (biasanya 100 email terakhir).

Anda dapat membuat berbagai jenis tabel dalam satu file XML.

## Definisi Tabel
- Elemen `metalib` adalah elemen root dari file XML.
- Atribut `tagsetversion` harus satu.
- Elemen `struct` dengan atribut `primarykey` perlu didefinisikan sebagai tabel, atau hanya sebuah struktur.
- Setiap kali struktur tabel diubah, atribut versi harus bertambah 1. Nilai awal dari atribut versi selalu 1.
- Atribut `primarykey` digunakan untuk menentukan bidang kunci utama. Tabel GENERIC mendukung hingga empat bidang kunci utama dan tabel LIST mendukung hingga tiga.
- Atribut `splittablekey` berfungsi sebagai shardkey untuk membagi tabel TcaplusDB menjadi beberapa pecahan dan menyimpannya di beberapa node. `splittablekey` harus merupakan salah satu bidang kunci utama. Karena `splittablekey` yang sangat terpisah memiliki kinerja yang lebih baik dan rentang nilai yang luas, kami merekomendasikan `splittablekey` STRING.
- Atribut `desc` menjelaskan elemen.
- Elemen `entry` mendefinisikan bidang. Nilai yang valid: int32, string, char, int64, double, short.
- Elemen `index` mendefinisikan indeks yang harus berisi `splittablekey`. Karena kunci utama dapat digunakan untuk mengkueri tabel, indeks harus memiliki atribut yang berbeda dari kunci utama.

## Contoh Kode untuk File Deskripsi Tabel di TDR

```
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
 
<metalib name="tcaplus_tb" tagsetversion="1" version="1">
 
  <!-- generic_table `users`, store the user' information -->
  <!-- an user may has many roles -->
  <struct name="users" version="1" primarykey="user_id,username,role_id" splittablekey="user_id" desc="user table">
    <entry name="user_id" type="uint64" desc="user id"/>
    <entry name="username" type="string" size="64" desc="login username"/>
    <entry name="role_id" type="int32" desc="a user can have multiple roles"/>
 
    <entry name="level" type="int32" defaultvalue="1" desc="role's level"/>
    <entry name="role_name" type="string" size="1024" desc="role's name"/>
    <entry name="last_login_time" type="string" size="64" defaultvalue="" desc="user login timestamp"/>
    <entry name="last_logout_time" type="string" size="64" defaultvalue="" desc="user logout timestamp"/>
 
    <index name="index1" column="user_id"/>
  </struct>
 
  <!-- list_table `mails`, store the role's mails -->
  <struct name="mails" version="1" primarykey="user_id,role_id" desc="mail table">
    <entry name="user_id" type="uint64" desc="user id"/>
    <entry name="role_id" type="int32" desc="a user may has many roles"/>
 
    <entry name="text" type="string" size="2048" desc="mail text"/>
    <entry name="send_time" type="string" size="64" defaultvalue="" desc="timestamp of the mail sent"/>
    <entry name="read_time" type="string" size="64" defaultvalue="" desc="timestamp of the mall read"/>
  </struct>
 
</metalib>
```
Selain itu, Anda dapat menggunakan `union` untuk membuat data jenis nested.

Elemen `union` mendefinisikan jenis sederhana sebagai kumpulan (himpunan) nilai dari jenis data sederhana yang ditentukan, seperti INT dan STRING. Anda dapat menggunakan `union` sebagai jenis data kustom.
Tag `Macro` digunakan untuk mendefinisikan konstanta.

```
<macro name="DB_MAX_USER_MSG_LEN" value="301" desc="Max length of the message that user can define"/>
 <union name="DBPlayerMsg" version="1" desc="DB Player message">
   <entry name="SysMsgID"     type="uint8"         desc="Message ID" />
   <entry name="UsrMsg"       type="string"        size="DB_MAX_USER_MSG_LEN"   desc="player created message" />
 </union>
```