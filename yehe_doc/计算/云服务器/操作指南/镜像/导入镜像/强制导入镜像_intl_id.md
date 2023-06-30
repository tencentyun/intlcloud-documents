## Skenario
Jika tidak dapat [memasang cloudinit](https://intl.cloud.tencent.com/document/product/213/12587) di citra Linux Anda, gunakan **Forced Image Import** (Impor Citra Secara Paksa) untuk mengimpor citra. Jika Anda menggunakan citra ini untuk impor, yang tidak menginstal cloudinit, Tencent Cloud tidak dapat menginisialisasi CVM Anda. Dalam hal ini, Anda perlu menyiapkan skrip sendiri untuk mengonfigurasi CVM berdasarkan file konfigurasi yang disediakan oleh Tencent Cloud. Dokumen ini menjelaskan cara mengonfigurasi CVM jika citra diimpor secara paksa.

Tencent Cloud memberi pengguna perangkat CDROM yang berisi informasi konfigurasi. Pengguna perlu memasang CDROM dan membaca informasi `mount_point/qcloud_action/os.conf` untuk konfigurasi. Jika data konfigurasi lain atau UserData perlu digunakan, pengguna dapat langsung membaca file di bawah `mount_point/`.

## File Konfigurasi os.conf
Konten os.conf adalah sebagai berikut.
<pre>
hostname=VM_10_20_xxxx
password=GRSgae1fw9frsG.rfrF
eth0&#95;ip&#95;addr=10.104.62.201
eth0&#95;mac&#95;addr=52:54:00:E1:96:EB
eth0&#95;netmask=255.255.192.0
eth0&#95;gateway=10.104.0.1
dns&#95;nameserver="10.138.224.65 10.182.20.26 10.182.24.12"
</pre>
>? Nama parameter di atas adalah untuk referensi, dan nilainya hanya digunakan sebagai contoh.
>
Deskripsi masing-masing parameter dalam file konfigurasi os.conf adalah sebagai berikut:

| Nama Parameter | Deskripsi |
|----------|----------|
| nama host | Nama CVM |
| kata sandi | Kata sandi terenkripsi |
| eth0_ip_addr | IP LAN dari eth0 |
| eth0_mac_addr | Alamat MAC dari eth0 |
| eth0_netmask | Subnet mask dari eth0 |
| eth0_gateway | Gateway eth0 |
| dns_nameserver | Server resolusi DNS |


## Batas
- Citra harus memenuhi batas pada citra Linux sebagaimana diuraikan dalam [Impor Citra](https://intl.cloud.tencent.com/document/product/213/4945), kecuali untuk cloudinit.
- Partisi sistem untuk mengimpor citra tidak lengkap.
- Citra yang diimpor tidak berisi kerentanan yang dapat dieksploitasi dari jarak jauh.
- Sebaiknya ubah kata sandi segera setelah instans berhasil dibuat dengan citra yang diimpor secara paksa.

## Catatan
Perhatikan hal berikut saat mengonfigurasi penguraian skrip:
- Skrip dijalankan secara otomatis saat startup. Harap terapkan persyaratan ini berdasarkan sistem operasi Anda.
- Pasang `/dev/cdrom` dan baca file `os_action/os.conf` di bawah titik pemasangan untuk mendapatkan informasi konfigurasi.
- Kata sandi yang ditempatkan di CDROM oleh Tencent Cloud sudah dienkripsi. Anda dapat mengatur kata sandi baru dengan `chpasswd -e`.
**Note that the encrypted password may contain special characters. We recommend you place it in a file and then set the password with `chpasswd -e < passwd_file`.** (Perhatikan bahwa kata sandi terenkripsi mungkin berisi karakter khusus. Sebaiknya Anda menempatkannya dalam file, lalu atur kata sandi dengan `chpasswd -e < passwd_file`.)
- Saat Anda menggunakan citra yang diimpor secara paksa untuk membuat instans dan kemudian membuat citra, Anda perlu memastikan bahwa skrip akan tetap dijalankan untuk memastikan bahwa instans dikonfigurasi dengan benar. Anda juga dapat menginstal cloudinit dalam instans ini.


## Petunjuk

>! Tencent Cloud menyediakan contoh skrip berdasarkan CentOS. Anda dapat menjadikannya rujukan guna membuat skrip untuk citra Anda. Selama pembuatan, perhatikan bahwa:
> - **The script must be properly placed in the system before image import** (Skrip harus ditempatkan dengan benar di sistem sebelum impor citra).
> - Skrip ini tidak berlaku untuk semua sistem operasi. Anda perlu memodifikasinya sesuai dengan sistem operasi Anda sendiri.
> 


1. Buat skrip `os_config` berdasarkan contoh skrip berikut.
Anda dapat memodifikasi skrip sesuai kebutuhan.

```
#!/bin/bash
### BEGIN INIT INFO
# Provides:          os-config
# Required-Start:    $local_fs $network $named $remote_fs
# Required-Stop:
# Should-Stop:
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: config of os-init job
# Description: run the config phase without cloud-init
### END INIT INFO
###################user settings#####################
cdrom_path=`blkid -L config-2`
load_os_config() {
	mount_path=$(mktemp -d /mnt/tmp.XXXX)
	mount /dev/cdrom $mount_path
	if [[ -f $mount_path/qcloud_action/os.conf ]]; then
		. $mount_path/qcloud_action/os.conf
		if [[ -n $password ]]; then
			passwd_file=$(mktemp /mnt/pass.XXXX)
			passwd_line=$(grep password $mount_path/qcloud_action/os.conf)
			echo root:${passwd_line#*=} > $passwd_file
		fi
		return 0
	else 
		return 1
	fi
}
cleanup() {
	umount /dev/cdrom
	if [[ -f $passwd_file ]]; then
		echo $passwd_file
		rm -f $passwd_file
	fi
	if [[ -d $mount_path ]]; then
		echo $mount_path
		rm -rf $mount_path
	fi
}
config_password() {
	if [[ -f $passwd_file ]]; then
		chpasswd -e < $passwd_file
	fi
}
config_hostname(){
	if [[ -n $hostname ]]; then
		sed -i "/^HOSTNAME=.*/d" /etc/sysconfig/network
		echo "HOSTNAME=$hostname" >> /etc/sysconfig/network
	fi
}
config_dns() {
    if [[ -n $dns_nameserver ]]; then
        dns_conf=/etc/resolv.conf
        sed -i '/^nameserver.*/d' $dns_conf
        for i in $dns_nameserver; do
            echo "nameserver $i" >> $dns_conf
        done
    fi
}
config_network() {
    /etc/init.d/network stop
    cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
IPADDR=$eth0_ip_addr
NETMASK=$eth0_netmask
HWADDR=$eth0_mac_addr
ONBOOT=yes
GATEWAY=$eth0_gateway
BOOTPROTO=static
EOF
    if [[ -n $hostname ]]; then
    	sed -i "/^${eth0_ip_addr}.*/d" /etc/hosts
		echo "${eth0_ip_addr} $hostname" >> /etc/hosts
	fi
    /etc/init.d/network start
}
config_gateway() {
	sed -i "s/^GATEWAY=.*/GATEWAY=$eth0_gateway" /etc/sysconfig/network
}
###################init#####################
start() {
	if load_os_config ; then
		config_password
		config_hostname
		config_dns
		config_network
		cleanup
		exit 0
	else 
		echo "mount ${cdrom_path} failed"
		exit 1
	fi
}
RETVAL=0
case "$1" in
	start)
		start
		RETVAL=$?
	;;
	*)
		echo "Usage: $0 {start}"
		RETVAL=3
	;;
esac
exit $RETVAL
```
2. Tempatkan skrip `os_config` di direktori `/etc/init.d/` dan jalankan perintah berikut.
```
chmod +x /etc/init.d/os_config
chkconfig --add os_config
```
3. Jalankan perintah berikut untuk memeriksa apakah `os_config` telah ditambahkan ke layanan startup.
```
chkconfig --list
```
>? Anda harus memastikan bahwa skrip dijalankan dengan benar. Jika Anda gagal terhubung ke instans melalui SSH atau terjadi pengecualian jaringan setelah impor citra, coba hubungkan ke instans melalui konsol untuk menjalankan skrip lagi. Jika masalah tersebut masih terjadi, hubungi layanan pelanggan.


