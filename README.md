# Jarkom-Modul-2-A06-2023

## Group Member

| NRP        | Name                        |
| ---------- | --------------------------- |
| 5025211057 | Salsabila Fatma Aripa       |
| 5025211254 | Yusna Millaturrosyidah      |

## Daftar Isi
- [Soal 1](#soal-1)
	- [Penyelesaian soal 1](#penyelesaian-soal-1)
- [Soal 2](#soal-2)
	- [Penyelesaian soal 2](#penyelesaian-soal-2)
- [Soal 3](#soal-3)
	- [Penyelesaian soal 3](#penyelesaian-soal-3)
- [Soal 4](#soal-4)
	- [Penyelesaian soal 4](#penyelesaian-soal-4)
- [Soal 5](#soal-5)
	- [Penyelesaian soal 5](#penyelesaian-soal-5)
- [Soal 6](#soal-6)
	- [Penyelesaian soal 6](#penyelesaian-soal-6)
- [Soal 7](#soal-7)
	- [Penyelesaian soal 7](#penyelesaian-soal-7)
- [Soal 8](#soal-8)
	- [Penyelesaian soal 8](#penyelesaian-soal-8)
- [Soal 9](#soal-9)
	- [Penyelesaian soal 9](#penyelesaian-soal-9)
- [Soal 10](#soal-10)
	- [Penyelesaian soal 10](#penyelesaian-soal-10)
- [Soal 11](#soal-11)
	- [Penyelesaian soal 11](#penyelesaian-soal-11)
- [Soal 12](#soal-12)
	- [Penyelesaian soal 12](#penyelesaian-soal-2)
- [Soal 13](#soal-13)
	- [Penyelesaian soal 13](#penyelesaian-soal-13)
- [Soal 14](#soal-14)
	- [Penyelesaian soal 14](#penyelesaian-soal-14)
- [Soal 15](#soal-15)
	- [Penyelesaian soal 15](#penyelesaian-soal-15)
- [Soal 16](#soal-16)
	- [Penyelesaian soal 16](#penyelesaian-soal-16)
- [Soal 17](#soal-17)
	- [Penyelesaian soal 17](#penyelesaian-soal-17)
- [Soal 18](#soal-18)
	- [Penyelesaian soal 18](#penyelesaian-soal-18)
- [Soal 19](#soal-19)
	- [Penyelesaian soal 19](#penyelesaian-soal-19)
- [Soal 20](#soal-20)
	- [Penyelesaian soal 20](#penyelesaian-soal-20)
- [Kendala](#Kendala)

## Soal 1
Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut

### Penyelesaian soal 1
1. Pertama-tama kita buat Topologi terlebih dahulu, disini kelompok kami mendapatkan Topologi No 7 <br />

<img width="614" alt="topologi" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/7cdd6ebb-6835-4c32-9bae-586fdd0c6627">

2. Membuat konfigurasi pada setiap node yang ada
#### Router
- Router
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.2.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 10.2.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.2.3.1
	netmask 255.255.255.0
```

#### DNS Master
- Yudhistira
```
auto eth0
iface eth0 inet static
	address 10.2.2.3
	netmask 255.255.255.0
	gateway 10.2.2.1
```

#### DNS Slave
- Werkudara
```
auto eth0
iface eth0 inet static
	address 10.2.2.2
	netmask 255.255.255.0
	gateway 10.2.2.1
```

#### Client
- Nakula
```
auto eth0
iface eth0 inet static
	address 10.2.1.2
	netmask 255.255.255.0
	gateway 10.2.1.1
```
- Sadewa
```
auto eth0
iface eth0 inet static
	address 10.2.1.3
	netmask 255.255.255.0
	gateway 10.2.1.1
```

#### Load Balancer
- Arjuna
```
auto eth0
iface eth0 inet static
	address 10.2.1.4
	netmask 255.255.255.0
	gateway 10.2.1.1
```

#### Web Server
- Prabukusuma
```
auto eth0
iface eth0 inet static
	address 10.2.3.2
	netmask 255.255.255.0
	gateway 10.2.3.1
```
- Abimanyu
```
auto eth0
iface eth0 inet static
	address 10.2.3.3
	netmask 255.255.255.0
	gateway 10.2.3.1
```
- Wisanggeni
```
auto eth0
iface eth0 inet static
	address 10.2.3.4
	netmask 255.255.255.0
	gateway 10.2.3.1
```

Menambahkan command yang selalu dijalankan di node tersebut ke file `/root/.bashrc` di bagian paling bawah.
`iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.2.0.0/16`

Untuk memastikan apakah router sudah terhubung ke internet maka dapat membuat file .sh seperti dibawah ini :
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf

ping google.com
```

## Soal 2
Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.

### Penyelesaian soal 2
Pertama-tama yang harus kita lakukan adalah melakukan update dan install bind9 terlebih dahulu dengan command seperti dibawah ini :
```
apt-get update
apt-get install bind9 -y
```

Kemudian, untuk membuat website utama kita harus membuat zone DNS pada file `named.conf.local` dan mengatur konfirgurasi pada `/etc/bind/jarkom/arjuna.A02.com` seperti dibawah ini :

```
zone "arjuna.A06.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.A06.com";
};

mkdir -p /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/arjuna.A06.com

$TTL    604800
@       IN      SOA     arjuna.A06.com. root.arjuna.A06.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.A06.com.
@       IN      A       10.2.1.4
www     IN      CNAME   arjuna.A06.com.

service bind9 restart

```
Lalu, melakukan setting nameserver pada client (Nakula dan Sadewa) :
```
nano /etc/resolv.conf
nameserver 10.2.2.3 ; IP Yudhistira

ping arjuna.A06.com -c 5
ping www.arjuna.A06.com -c 5
```
#### Hasil 


## Soal 3
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

### Penyelesaian soal 3

## Soal 4
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

### Penyelesaian soal 4

## Soal 5
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)

### Penyelesaian soal 5

## Soal 6
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.

### Penyelesaian soal 6

## Soal 7
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.

### Penyelesaian soal 7

## Soal 8
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.

### Penyelesaian soal 8

## Soal 9
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.

### Penyelesaian soal 9

## Soal 10
Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh
    - Prabakusuma:8001
    - Abimanyu:8002
    - Wisanggeni:8003
### Penyelesaian soal 10
