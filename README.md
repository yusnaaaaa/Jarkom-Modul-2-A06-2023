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

#### Hasil 

<img width="580" alt="no1 yudhis" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/83b76a66-508f-4b80-bb52-ccbd9e3e5314">

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

# atau

ping www.arjuna.A06.com -c 5
```
#### Hasil 

<img width="418" alt="2 nakula" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/2dfd5f8c-fe9a-4e3f-b7a4-c7f7a935b4ed"><br />

<img width="418" alt="2 sadewa" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/94fab883-a7f4-4829-8831-cbbaf1956660">


## Soal 3
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

### Penyelesaian soal 3
Untuk menyelesaikan soal no 3, caranya sama seperti no 2 namun hanya berbeda domainnya saja. 

```
apt-get update
apt-get install bind9 -y
```

Kemudian, untuk membuat website utama kita harus membuat zone DNS pada file `named.conf.local` dan mengatur konfirgurasi pada `/etc/bind/jarkom/abimanyu.A02.com` seperti dibawah ini :

```
zone "abimanyu.A06.com" {
        type master;
        file "/etc/bind/jarkom/abimanyu.A06.com";
};

cp /etc/bind/db.local /etc/bind/jarkom/abimanyu.A06.com

$TTL    604800
@       IN      SOA     abimanyu.A06.com. root.abimanyu.A06.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.A06.com.
@       IN      A       10.2.3.3 ; IP Abimanyu
www     IN      CNAME   abimanyu.A06.com.

service bind9 restart

```
Lalu, melakukan setting nameserver pada client (Nakula dan Sadewa) :
```
nano /etc/resolv.conf
nameserver 10.2.2.3 ; IP Yudhistira

ping abimanyu.A06.com -c 5

# atau

ping www.abimanyu.A06.com -c 5
```

#### Hasil 

<img width="420" alt="3 nakula" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/2683a38e-d1f4-4cd1-9d2c-ad00d5e80f7f"><br />

<img width="414" alt="3 sadewa" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/79fd701b-fb3c-40b3-b662-250b6a20a401">

## Soal 4
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

### Penyelesaian soal 4
Untuk membuat subdomain parikesit.abimanyu.yyy.com kita hanya perlu menambahkan subdomain kedalam file `/etc/bind/jarkom/abimanyu.A06.com` seperti berikut ini :
```
$TTL    604800
@       IN      SOA     abimanyu.A06.com. root.abimanyu.A06.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       	IN      NS      abimanyu.A06.com.
@       	IN      A       10.2.3.3 ; IP Abimanyu
www     	IN      CNAME   abimanyu.A06.com.
parikesit 	IN	A	10.2.3.3 ; IP Abimanyu

service bind9 restart
```

Kemudian untuk membuktikan apakah pembuatan subdomain berhasil maka dapat command `ping parikesit.abimanyu.A06.com` pada client (Nakula dan Sadewa)

#### Hasil

<img width="440" alt="no4" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/96b0ced6-9472-406a-94cb-00d5d7896b26">

## Soal 5
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)

### Penyelesaian soal 5
Untuk membuat reverse domain, maka dibutuhkan pendefinisian zone baru dalam `/etc/bin/named.conf.local`. dan membuat konfigurasi ke dalam `/etc/bind/jarkom/3.2.10.in-addr.arpa`seperti dibawah ini : 

```
nano /etc/bind/named.conf.local

zone "3.2.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/3.2.10.in-addr.arpa";
};

cp /etc/bind/db.local /etc/bind/jarkom/3.2.10.in-addr.arpa

nano /etc/bind/jarkom/3.2.10.in-addr.arpa

$TTL    604800
@       IN      SOA     abimanyu.A06.com. root.abimanyu.A06.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.2.10.in-addr.arpa.       	IN      NS      abimanyu.A06.com.
3			       	IN      PTR     abimanyu.A06.com.

service bind9 restart

```

Kemudian untuk mengecek hasilnya pada client bisa menggunakan cara seperti dibawah ini :
```
echo 'nameserver 192.168.122.1 > /etc/resolv.conf'

apt-get update
apt-get install dnsutils

echo 'nameserver 10.2.2.3 > /etc/resolv.conf'
host -t PTR 10.2.3.3
```

#### Hasil

<img width="338" alt="5 nakula" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/5c45997a-8b31-40b9-ac58-7d99b84a0937">
<br />

<img width="342" alt="5 sadewa" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/88614b39-f59b-4527-ab8f-725dbe50f950">

## Soal 6
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.

### Penyelesaian soal 6
Pertama-tama yaitu melakukan pengeditan pada zone arjuna dan abimanyu dalam file `/etc/bind/named.conf.local` :
```
nano /etc/bind/named.conf.local

zone "arjuna.A06.com" {
        type master;
        notify yes;
        also-notify { 10.2.2.2; }; 
        allow-transfer { 10.2.2.2; }; 
        file "/etc/bind/jarkom/arjuna.A06.com";
};

zone "abimanyu.A06.com" {
        type master;
        notify yes;
        also-notify { 10.2.2.2; }; 
        allow-transfer { 10.2.2.2; }; 
        file "/etc/bind/jarkom/abimanyu.A06.com";
};

service bind9 restart
```
Kemudian, edit file `/etc/bind/named.conf.local` pada DNS Slave (Werkudara) seperti dibawah ini :
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf

apt-get update
apt-get install bind9 -y

zone "arjuna.A06.com" {
        type slave;
       	masters { 10.2.2.3; }; 
        file "/var/lib/bind/arjuna.A06.com";
};

zone "abimanyu.A06.com" {
        type slave;
       	masters { 10.2.2.3; }; 
         file "/var/lib/bind/abimanyu.A06.com";
};

service bind9 restart

```
Selanjutnya jalankan command `service bind9 stop` pada DNS Master (Yudhistira). Kemudian cek pada client dengan command sebagai berikut :
```
echo 'nameserver 10.2.2.2' > /etc/resolv.conf

ping abimanyu.A06.com -c 5

# atau

ping www.abimanyu.A06.com -c 5
```
Setelah itu jangan lupa untuk melakukan restart kembali pada DNS Master dengan command `service bind9 restart` dan `echo 'nameserver 10.2.2.3' > /etc/resolv.conf` pada kedua client.

#### Hasil 

<img width="419" alt="6 nakula" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/3442a182-aa75-4e65-9c13-aeb20c3d4a91"><br />

<img width="414" alt="6 sadewa" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/851a6b11-f35d-4992-abc1-a316407a3253">

## Soal 7
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.

### Penyelesaian soal 7

Mengedit file `/etc/bind/jarkom/abimanyu.A06.com` dan file `/etc/bind/named.conf.local` pada DNS Master sebagai berikut :

```
echo '
ns1 		IN  	A  	10.2.2.2 ; IP Werkudara
baratayuda 	IN   	NS  	ns1 ' > /etc/bind/jarkom/abimanyu.A06.com

nano /etc/bind/named.conf.options
options {
	directory "/var/cache/bind";

	dnssec-validation auto;

	auth-nxdomain no;
	listen-on { any; };
	allow-query { any; };
};

nano /etc/bind/named.conf.local
zone "abimanyu.A06.com" {
	type master;
	file "/etc/bind/jarkom/abimanyu.A06.com";
	allow-transfer { 10.2.2.2; };
}; 

service bind9 restart
```

Kemudian edit file `/etc/bind/jarkom/abimanyu.A06.com` dan file `/etc/bind/named.conf.local` pada DNS Slave sebagai berikut : 

```
nano /etc/bind/named.conf.options
options {
	directory "/var/cache/bind";

	dnssec-validation auto;

	auth-nxdomain no;
	listen-on { any; };
	allow-query { any; };
};

nano /etc/bind/named.conf.local
zone "baratayuda.abimanyu.A06.com" {
    type master;
    file "/etc/bind/baratayuda/baratayuda.abimanyu.A06.com";
};

mkdir -p /etc/bind/baratayuda

cp /etc/bind/db.local /etc/bind/baratayuda/baratayuda.abimanyu.A06.com

nano /etc/bind/baratayuda/baratayuda.abimanyu.A06.com
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.A06.com. root.baratayuda.abimanyu.A06.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       	IN      NS      baratayuda.abimanyu.A06.com.
@		IN      A	10.2.2.2
www		IN	CNAME	baratayuda.abimanyu.A06.com.

service bind9 restart
```

Selanjutnya untuk melihat hasilnya dapat menggunakan command seperti dibawah ini pada client :
```
echo 'nameserver 10.2.2.2' > /etc/resolv.conf

ping baratayuda.abimanyu.A06.com -c 5

# atau

ping www.baratayuda.abimanyu.A06.com -c 5
```

#### Hasil

<img width="441" alt="7 nakula" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/728a7fde-98a4-4e34-ba20-e291ae10cb5f"><br />

<img width="439" alt="7 sadewa" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/c530e35c-1c90-4837-8c08-23c4b3cb4acf">

## Soal 8
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.

### Penyelesaian soal 8
Untuk menyelesaikan soal no 8 kita dapat langsung mengedit konfigurasi pada file `/etc/bind/Baratayuda/baratayuda.abimanyu.A06.com` sebagai berikut :

```
echo '
rjp		IN      A	10.2.2.2
www.rjp		IN	A	10.2.2.2
' >> /etc/bind/baratayuda/baratayuda.abimanyu.A06.com

service bind9 restart
```

Selanjutnya untuk melihat hasilnya dapat menggunakan command seperti dibawah ini pada client :
```
echo 'nameserver 10.2.2.2' > /etc/resolv.conf

ping rjp.baratayuda.abimanyu.A06.com -c 5

# atau

ping www.rjp.baratayuda.abimanyu.A06.com -c 5
```

#### Hasil

<img width="461" alt="8 nakula" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/7d529732-5c31-4106-b076-eaf4c1b5a9b9"><br />

<img width="487" alt="8 sadewa" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/f35cd746-2c83-4abb-89a3-a039bd4461aa">

## Soal 9
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.

### Penyelesaian soal 9

Pertama-tama yaitu membuat konfigurasi pada Load Balancer (Arjuna)
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf

apt-get update
apt-get install nginx

service nginx restart
service nginx status

echo ' 
upstream myapp {
	server 10.2.3.2;
	server 10.2.3.3;
	server 10.2.3.4;
}

server {
	listen 80;
	server_name arjuna.A06.com;

	location / {
	proxy_pass http://myapp:8000/;
	}
} ' > /etc/nginx/sites-available/lb-modul2

ln -s /etc/nginx/sites-available/lb-modul2 /etc/nginx/sites-enabled

```

Setelah itu buatlah konfigurasi pada masing-masing node worker sebagai berikut : 
```
apt-get update
apt-get install nginx php php-fpm -y

php -v

mkdir /var/www/modul2

apt-get install git -y

git -c http.sslVerify=false clone https://github.com/yusnaaaaa/arjuna.A06 /var/www/modul2

echo '
server {
	listen 80;
	root /var/www/modul2;

	index index.php index.html index.htm;
	server_name _;

	location / {
		try_files $uri $uri/ /index.php?$query_string;
	}
	
	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
	}

	location ~ /\.ht {
		deny all;
	}

	error_log /var/log/nginx/modul2_error.log;
	access_log /var/log/nginx/modul2_access.log;
} ' > /etc/nginx/sites-available/modul2

ln -s /etc/nginx/sites-available/modul2 /etc/nginx/sites-enabled

rm -f /etc/nginx/sites-enabled/default

service php7.0-fpm start
service nginx reload
service nginx restart

nginx -t
```

Kemudian untuk mengetahuinya kita dapat menggunakan lynx dan deploy index.php pada client.

```
apt-get update
apt-get install lynx

lynx [ip webserver]
```

#### Hasil
- Prabukusuma<br />

<img width="609" alt="9prabukusuma" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/2c2df529-a945-4ce4-a2bf-116be3cda94b"><br />
  
- Abimanyu<br />

<img width="584" alt="9abimanyu" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/8aad101c-58aa-41bf-a924-c15a29fdda6c"><br />

- Wisanggeni<br />

<img width="556" alt="9wisanggeni" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/b8f3eadf-3763-45d5-b91c-ee623139aa2c">

## Soal 10
Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh
    - Prabakusuma:8001
    - Abimanyu:8002
    - Wisanggeni:8003
### Penyelesaian soal 10
Pertama edit konfigurasi pada Load Balancer (Arjuna) seperti dibawah ini :
```
echo '
upstream myapp {
	server 10.2.3.2:8001;
	server 10.2.3.3:8003;
	server 10.2.3.4:8003;
}

server {
	listen 80;
	server_name arjuna.A06.com;

	location / {
		proxy_pass http://myapp/;
	}
}' > /etc/nginx/sites-available/lb-modul2

ln -s /etc/nginx/sites-available/lb-modul2 /etc/nginx/sites-enabled
```
Selanjutnya edit juga konfigurasi pada masing-masing webserver dengan menambahkan port yang telah ditentukan pada soal, dibawah ini merupakan contoh port untuk Prabakusuma : 
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf

echo '
server {
    listen [Port masing-masing worker];
    root /var/www/modul2;

    index index.php index.html index.htm;
    server_name _;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }

    error_log /var/log/nginx/modul2_error.log;
    access_log /var/log/nginx/modul2_access.log;
}' > /etc/nginx/sites-available/modul2

ln -s /etc/nginx/sites-available/modul2 /etc/nginx/sites-enabled

service nginx restart
```

Lalu, untuk mengetahui hasilnya dapat menggunakan command seperti dibawah ini pada client :
`lynx [ip webserver:port]`

#### Hasil
- Prabukusuma<br />

<img width="579" alt="10prabukusuma" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/8aab2064-17ea-4142-a226-4905cbc7123c"><br />

- Abimanyu<br />

<img width="558" alt="10abimanyu" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/4641f6c9-29da-4c34-b3ad-69cdfd39550d"><br />

- Wisanggeni<br />

<img width="584" alt="10wisanggeni" src="https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/57f5975e-fe13-4f02-8d2b-d0b49afdd0df">

## Soal 11
Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.yyy.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy

### Penyelesaian soal 11
Melakukan setting pada node abimanyu seperti dibawah ini :
```
apt-get install apache2 -y

service apache2 start

apt-get install libapache2-mod-php7.0 -y

apt-get install git -y

cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/abimanyu.A06.com.conf

echo '
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName abimanyu.A06.com
    ServerAlias www.abimanyu.A06.com
    DocumentRoot /var/www/abimanyu.A06

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/abimanyu.A06.com.conf

mkdir /var/www/abimanyu.A06

git -c http.sslVerify=false clone https://github.com/yusnaaaaa/jarkom-abimanyu.A06 /var/www/abimanyu.A06

a2ensite abimanyu.A06.com

service apache2 restart
```

Kemudian untuk mengetahui hasilnya dapat menggunakan command `lynx abimanyu.A06.com` pada client

#### Hasil
![no11](https://github.com/yusnaaaaa/Jarkom-Modul-2-A06-2023/assets/91377793/bd259207-e17c-40d9-98b4-eac02cba6a9a)

## Soal 12
Setelah itu ubahlah agar url www.abimanyu.yyy.com/index.php/home menjadi www.abimanyu.yyy.com/home.

### Penyelesaian soal 12
#### Hasil

## Soal 13
Selain itu, pada subdomain www.parikesit.abimanyu.yyy.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.yyy

### Penyelesaian soal 13
#### Hasil

## Soal 14
Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).

### Penyelesaian soal 14
#### Hasil

## Soal 15
Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.

### Penyelesaian soal 15
#### Hasil

## Soal 16
Buatlah suatu konfigurasi virtual host agar file asset www.parikesit.abimanyu.yyy.com/public/js menjadi 
www.parikesit.abimanyu.yyy.com/js 

### Penyelesaian soal 16
#### Hasil

## Soal 17
Agar aman, buatlah konfigurasi agar www.rjp.baratayuda.abimanyu.yyy.com hanya dapat diakses melalui port 14000 dan 14400.

### Penyelesaian soal 17
#### Hasil

## Soal 18
Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudayyy” dengan yyy merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.yyy.

### Penyelesaian soal 18
#### Hasil

## Soal 19
Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.yyy.com (alias)

### Penyelesaian soal 19
#### Hasil

## Soal 20
Karena website www.parikesit.abimanyu.yyy.com semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.

### Penyelesaian soal 20
#### Hasil
