### Jarkom_Modul5_Lapres_C11

Kelompok C11
- 05111840000131 Aaron Astonvilla
- 05111840000151 Nikodemus Siahaan

# SoalA
#### Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Bibah seperti dibawah ini :

![image](https://user-images.githubusercontent.com/57977401/103073832-45832180-4603-11eb-9d91-8e34c9dfe803.png)

Jawab : <br>
- Topologi.sh
```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &
uml_switch -unix switch6 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.45 eth1=daemon,,,switch3 eth2=daemon,,,switch2 mem=96M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch2 eth1=daemon,,,switch5 eth2=daemon,,,switch1 mem=96M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch4 eth1=daemon,,,switch6 eth2=daemon,,,switch3 mem=96M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch1 mem=128M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch1 mem=128M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch4 mem=128M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch4 mem=128M &

# Klien
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch5 mem=96M &
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch6 mem=96M &
```
<br><br><br>

# SoalB
#### karena kalian telah mempelajari Subnetting dan Routing, Bibah meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM.

Jawab : <br>
Kami menggunakan metode VLSM, dan berikut adalah gambar pembagian subnet, pohon IP dan table IP nya.

- Pembagian Subnet

![VLSM](https://github.com/nicosiahaan/Jarkom_Modul5_Praktikum_C11/blob/main/Screenshot_221.png)


- Pohon IP

![Praktikum5](https://github.com/nicosiahaan/Jarkom_Modul5_Praktikum_C11/blob/main/Screenshot_222.png)


- Table IP

![Pembagian IP](https://user-images.githubusercontent.com/57977401/103096596-68cbc200-463f-11eb-9499-cf87a32ff23c.png)

<br>

Sehingga didapat IP tiap UML adalah sebagai berikut:
```
Malang	    10.151.77.90
Mojokerto   10.151.77.91
Batu	    192.168.2.2
Sidoarjo    192.168.0.2
Surabaya    10.151.76.46
Kediri	    192.168.2.6
Gresik	    192.168.1.2
Madiun	    192.168.2.10
Probolinggo 192.168.2.11
```

- Interfaces

**UML Surabaya (ROUTER)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.76.46
netmask 255.255.255.252
gateway 10.151.76.45

auto eth1
iface eth1 inet static
address 192.168.2.5
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.2.1
netmask 255.255.255.252
```

**UML Batu (ROUTER)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.2.2
netmask 255.255.255.252

auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 10.151.77.89
netmask 255.255.255.248
```

**UML Kediri (ROUTER)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.2.9
netmask 255.255.255.248

auto eth1
iface eth1 inet static
address 192.168.1.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 192.168.2.6
netmask 255.255.255.252
```

**UML Malang (SERVER)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.90
netmask 255.255.255.248
gateway 10.151.77.89
```

**UML Mojokerto (SERVER)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.77.91
netmask 255.255.255.248
gateway 10.151.77.89
```

**UML Madiun (SERVER)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.2.10
netmask 255.255.255.248
gateway 192.168.2.9
```

**UML Probolinggo (SERVER)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.2.11
netmask 255.255.255.248
gateway 192.168.2.9
```

**UML Sidoarjo (CLIENT)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.0
gateway 192.168.0.1
```

**UML Gresik (CLIENT)**<br>
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.1.2
netmask 255.255.255.0
gateway 192.168.1.1
```
<br><br><br>

# SoalC
#### Kalian juga diharuskan melakukan routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

Jawab : <br>
Routing yang dilakukan adalah sebagai berikut 

- Pada UML Surabaya
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.151.76.46
route add -net 10.151.77.88 netmask 255.255.255.248 gw 192.168.2.2
route add -net 192.168.2.8 netmask 255.255.255.248 gw 192.168.2.6
route add -net 192.168.0.0 netmask 255.255.255.0 gw 192.168.2.2
route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.2.6
```

- Pada UML Batu
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.2.1
```

- Pada UML Kediri
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.2.5
```
<br><br><br>

# SoalD
#### Tugas berikutnya adalah memberikan ip pada subnet SIDOARJO dan GRESIK secara dinamis menggunakan bantuan DHCP SERVER (Selain subnet tersebut menggunakan ip static). Kemudian kalian mengingat bahwa kalian harus setting DHCP RELAY pada router yang menghubungkannya,seperti yang kalian telah pelajari di masa lalu.

Jawab : <br>

- UML MOJOKERTO

1. Lakukan ```apt-get update```
2. Lalu install dhcp dengan perintah ```apt-get install isc-dhcp-server```
3. Buka file ```nano /etc/default/isc-dhcp-server```
4. Masukkan INTERFACES="eth0"
5. Buka file dengan perintah ```nano /etc/dhcp/dhcpd.conf```
6. Masukkan
```
subnet 192.168.0.0 netmask 255.255.255.0 {
    range 192.168.0.2 192.168.0.254;
    option routers 192.168.0.1;
    option broadcast-address 192.168.0.255;
    option domain-name-servers 10.151.77.90;
    default-lease-time 600;
    max-lease-time 7200;
}

subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.2 192.168.1.254;
    option routers 192.168.1.1;
    option broadcast-address 192.168.1.255;
    option domain-name-servers 10.151.77.90, 202.46.129.2;
    default-lease-time 600;
    max-lease-time 7200;
}

subnet 10.151.77.88 netmask 255.255.255.248 {

}
```
7. Lakukan restart dengan ```service isc-dhcp-server restart```<br>
8. Masukkan pada UML GRESIK dan SIDOARJO konfigurasi dibawah
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```
<br><br><br>

# Soal1
#### Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi SURABAYA menggunakan iptables, namun Bibah tidak ingin kalian menggunakan MASQUERADE.

Jawab : <br>
Pada UML Surabaya, ketikkan perintah seperti dibawah
```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to 10.151.76.46
```

Penjelasan : <br>
dengan menggunakan table nat chain POSTROUTING melalui eth0, setiap paket yang menuju keluar akan dirubah sourcenya menjadi 10.151.76.46<br>

- **Testing**
1. ping its.ac.id di seluruh UML
2. Apabila hasilnya adalah sebagai berikut, mana konfigurasi berhasil

![No1](https://user-images.githubusercontent.com/57977401/103078417-cb579a80-460c-11eb-90f8-2228093aecb2.png)
<br><br><br>

# Soal2
#### Kalian diminta untuk mendrop semua akses SSH dari luar Topologi (UML) Kalian pada server yang memiliki ip DMZ (DHCP dan DNS SERVER) pada SURABAYA demi menjaga keamanan.

Jawab : <br>
Pada UML Surabaya, ketikkan perintah seperti dibawah
```
iptables -A FORWARD -p tcp -i eth0 --dport 22 -d 10.151.77.88/29 -j DROP
```

Penjelasan : <br>
pada UML SURABAYA dibuat iptables dengan chain FORWARD, setiap paket dengan protokol tcp, incoming interface eth0 9dari luar), dan port tujuan 22 serta subnet tujuan 10.151.77.89/29 akan didrop

- **Testing**
1. Lakukan ```apt-get update```
2. Install netcat pada seluruh UML dengan perintah ```apt-get install netcat```
3. pada UML SURABAYA, ketikkan ```nc 10.151.77.90 22```
4. Pada UML MALANG dan MOJOKERTO, ketikkan perintah ```nc -l -p 22```
5. Ketikkan sesuatu 
6. Apabila hasilnya seperti dibawah, maka konfigurasi berhasil

![No2](https://user-images.githubusercontent.com/57977401/103155653-b2054880-47dc-11eb-8cea-d2171dfe08cb.png)

<br><br><br>

# Soal3
#### Karena tim kalian maksimal terdiri dari 3 orang, Bibah meminta kalian untuk membatasi DHCP dan DNS server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan yang berasal dari mana saja menggunakan iptables pada masing masing server, selebihnya akan di DROP.

Jawab : <br>
Pada UML MALANG dan MOJOKERTO
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

Penjelasan : <br>
dengan menggunakan chain INPUT setiap paket dengan protokol icmp akan dibatasi untuk membuat koneksi sebanyak 3 ( MAXIMAL 3 UML melakukan koneksi ke DHCP / DNS SERVER ) selebihnya akan didrop.<br>

- **Testing**
1. Lakukan ping ke IP MALANG (10.151.77.90) atau IP MOJOKERTO (10.151.77.91) di 4 UML (Misalkan UML BATU, KEDIRI, MADIUN dan PROBOLINGGO)
2. Apabila hasilnya seperti dibawah, maka konfigurasi berhasil

**Ping ke IP MALANG (10.151.77.90)**

![No3 Malang](https://user-images.githubusercontent.com/57977401/103156056-eb8b8300-47df-11eb-93c7-5d6e67f8efc4.png)

**Ping ke IP MOJOKERTO (10.151.77.91)**

![No3 Mojokerto](https://user-images.githubusercontent.com/57977401/103156058-ec241980-47df-11eb-8691-2db8b41e986d.png)

<br><br><br>

# Soal4_Soal5
### Soal 4
#### Akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat. Selain itu paket akan di REJECT.
#
### Soal 5
#### Akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 hingga pukul 07.00 setiap harinya. Selain itu paket akan di REJECT.
#

Jawab : <br>
Pada UML MALANG
```
#No 4
iptables -A INPUT -s 192.168.0.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s 192.168.0.0/24 -m time --timestart 17:01 --timestop 06:59 -j REJECT
iptables -A INPUT -s 192.168.0.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Sat,Sun -j REJECT
 
#No 5
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 07:01 --timestop 16:59 -j REJECT
```

Penjelasan : <br>
menggunakan chain INPUT, setiap paket yang berasal subnet SIDOARJO hanya boleh diakses pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat, sedangkan akses dari subnet GRESIK akan didrop ketika mengakses pada pukul 07.01 sampai 16.59. Selain itu paket akan diaccept.

- **Testing**
1. Ubah tanggal dan jam hari ini dengan perintah ```date -s '2020-12-13 08:00:00'```
2. Cek tanggal sudah benar atau belum dengan perintah ```date```
3. Lakukan ```ping 10.151.77.90``` pada UML GRESIK dan SIDOARJO
4. Apabila hasilnya seperti dibawah, maka konfigurasi berhasil

![No4 dan 5 Satu](https://user-images.githubusercontent.com/57977401/103093955-f22ac680-4636-11eb-9563-191556467604.png)

![No4 dan 5 Dua](https://user-images.githubusercontent.com/57977401/103093956-f2c35d00-4636-11eb-98d5-066b056a79e5.png)
<br><br><br>

# Soal6
#### Bibah ingin SURABAYA disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada PROBOLINGGO port 80 dan MADIUN port 80.

Jawab : <br>
Pada UML SURABAYA
```
iptables -A PREROUTING -t nat -d 10.151.77.90 -p tcp --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.168.2.10:80
iptables -A PREROUTING -t nat -d 10.151.77.90 -p tcp --dport 80 -j DNAT --to-destination 192.168.2.11:80
```

Penjelasan : <br>
Menggunakan chain PREORUTING dan table nat , setiap paket yang menuju  dns server dengan protocol tcp dan port tujuan 80 akan didistribusikan masing masing ke 192.168.2.10:80 (MADIUN) dan 192.168.2.11:80(PROBOLINGGO)

- **Testing**
1. Lakukan ```apt-get update```
2. Install netcat pada seluruh UML dengan perintah ```apt-get install netcat```
3. pada Putty Yudhistira, ketikkan ```nc 10.151.77.90 22```
4. Pada UML MADIUN dan PROBOLINGGO, ketikkan perintah ```nc -l -p 22```
5. Ketikkan sesuatu 
6. Apabila hasilnya seperti dibawah (gantian antar MADIUN dan PROBOLINGGO), maka konfigurasi berhasil

![No6](https://user-images.githubusercontent.com/57977401/103155651-af0a5800-47dc-11eb-8854-f62884c87941.png)

<br><br><br>

# Soal7
#### Bibah ingin agar semua paket didrop oleh firewall (dalam topologi) tercatat dalam log pada setiap UML yang memiliki aturan drop.

Jawab : <br>
Pada UML SURABAYA
```
iptables -N LOGGING 
iptables -A FORWARD -j LOGGING 
iptables -A LOGGING -m limit --limit 2/min -j LOG --log-prefix "IP Tables Packet Dropped: " --log-level 4 
iptables -A LOGGING -j DROP
```

Pada UML MALANG dan MOJOKERTO
```
iptables -N LOGGING
iptables -A INPUT -j LOGGING
iptables -A OUTPUT -j LOGGING
iptables -A LOGGING -j LOG --log-prefix "IP Tables Packet Dropped: " --log-level 4
iptables -A LOGGING -j DROP
```

Penjelasan : <br>
Membuat sebuah variabel LOGGING. Variabel LOGGING ini bertujuan untuk menambahkan LOG “IPTables Packet Dropped” ketika suatu action dilakukan. Action untuk LOG ini adalah DROP, jadi setiap terjadi droppacket, maa akan ditambahkan LOG tersebut.

- **Testing**
1. Jalankan iptables
2. Apabila hasilnya seperti dibawah, maka konfigurasi berhasil

![No7](https://user-images.githubusercontent.com/57977401/103095562-f0afcd00-463b-11eb-8196-27b0cd55b901.png)

<br><br><br>
