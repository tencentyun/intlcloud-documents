
Dokumen ini menjelaskan cara menggunakan sintaksis petunjuk pada proksi database.

Sintaksis petunjuk dapat digunakan untuk menjalankan permintaan SQL secara paksa pada instans yang ditentukan. Petunjuk memiliki prioritas perutean tertinggi. Misalnya, petunjuk ini tidak tunduk pada konsistensi dan kendala transaksi. Harap evaluasi dengan cermat sebelum menggunakannya, apakah petunjuk diperlukan dalam skenario bisnis Anda.

>!Saat menggunakan alat baris perintah MySQL untuk menghubungkan dan menggunakan pernyataan `HINT`, tambahkan opsi `-c` dalam perintah; jika tidak, petunjuk akan difilter oleh alat.
>
Saat ini, ada tiga jenis petunjuk yang didukung:
- Tetapkan ke instans sumber untuk dijalankan:
```
/* to master */
/*FORCE_MASTER*/   
```  
- Tetapkan ke instans hanya baca untuk dijalankan:
```
/* to slave */
/*FORCE_SLAVE*/  
```  
- Tentukan instans untuk dijalankan:
```
/* to server server_name*/
```
`server_name` dapat berupa ID singkat, seperti `/* to server test_ro_1 */`.

