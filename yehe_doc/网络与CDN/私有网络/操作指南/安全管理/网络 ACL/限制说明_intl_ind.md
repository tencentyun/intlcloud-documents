### Batasan Penggunaan
- Satu jaringan ACL dapat diikatkan ke beberapa subnet.
- ACL jaringan bersifat stateless. Dengan demikian, Anda perlu menetapkan masing-masing aturan keluar dan aturan masuk.
- ACL jaringan tidak memengaruhi interkomunikasi jaringan pribadi antar instans CVM di subnet terhubung.

### Batasan Kuota
| Sumber Daya | Batas |
| -------------- | ----------------- |
| Jumlah ACL jaringan di setiap VPC | 50 |
| Jumlah aturan per jaringan ACL | Masuk: 20<br/>Keluar: 20 |
| Jumlah ACL jaringan terhubung ke setiap subnet | 1 |

