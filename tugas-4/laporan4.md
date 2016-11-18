##Pendahuluan
Dalam merancang sebuah sistem atau jaringan yang aman, pemilik melakukan berbagai usaha untuk menjamin sistem atau jaringan tersebut benar benar aman. Salah satu cara untuk menjamin keamanan tersebut adalah dengan menyerang sistem atau jaringan itu sendiri, dengan mengetahui cara menyerang sistem atau jaringan tersebut diharapkan pengembang sistem dapat melakukan pencegahan agar sistem tidak bisa diserang dengan cara yang sama.

Kali ini, penulis akan mengulas tentang bagaimana sebuah sistem dapat diserang dengan brute force attack, dimana kemudian akan dilakukan usaha pencegahan penyerangan tersebut dengan membuat suatu sistem palsu yang disebut honeypot.

Sistem yang menjadi bahan percobaan kali ini adalah Ubuntu Server yang telah terinstall Kippo Honeypot. Penulis menggunakan Kali Linux untuk menyerang Ubuntu Server tersebut.

Pada tulisan kali ini, akan dijelaskan secara bertahap dimulai dari penjelasan tahap persiapan, dimulai dari instalasi Ubuntu Server, instalasi OS Kali Linux untuk penetrasi, instalasi Kippo Honeypot beserta konfigurasi, hingga uji penetrasi dengan SSH brute force tools. Pada akhir tulisan ini akan terdapat kesimpulan dan saran.

##Dasar Teori
###Ubuntu Server
Ubuntu Server adalah salah satu varian dari distro linux Ubuntu yang didesain untuk diinstall di server. Ubuntu Server tidak menyediakan GUI, yang ada hanya CLI (Comand Line Interface). Ubuntu Server digunakan untuk menangani memori sampai puluhan Giga ataupun menangani Multicore CPU.

###Kali Linux
Kali Linux adalah penerus distro BackTrack. Sama seperti BackTrack, distro ini dilengkapi dengan berbagai tools Linux untuk melakukan penetration testing. Dengan Kali Linux, pengguna yang melakukan pengujian keamanan tidak perlu repot men-install atau membuat kode program/script baru. Efek sampingnya: distro Linux seperti ini juga kerap disalahgunakan oleh script kiddie. Istilah script kiddie adalah sebutan untuk orang yang menjalankan tool dan mengikuti panduan tanpa memahami apa yang dilakukan oleh dirinya. Hal ini berbeda dari hacker yang memahami setiap aksi yang dilakukannya dan mampu membuat tool/script-nya sendiri.

###Brute Force Attack
Brute Force Attack adalah metode untuk meretas password (password cracking) dengan cara mencoba semua kemungkinan kombinasi yang ada pada “wordlist“. Metode ini dijamin akan berhasil menemukan password yang ingin diretas. Namun, proses untuk meretas password dengan menggunakan metode ini akan memakan banyak waktu.

###Medusa

###Kippo Honeypot
Honeypot adalah suatu sistem palsu yang sengaja dibuat untuk menjebak attacker menyerang sistem yang aslinya. Apabila attacker berhasil masuk ke honeypot, sistem yang aslinya tetap aman tak terpengaruh sedikit pun. 

##Persiapan Uji Penetrasi
###Instalasi Ubuntu Server
Memilih bahasa yang digunakan untuk menjalankan sistem operasi<br/>
![](tugas1/images/install_ubuntu_server_1.png?raw=true)<br/>
Memilih lokasi<br/>
![](tugas1/images/install_ubuntu_server_2.png?raw=true)<br/>
Konfigurasi keyboard<br/>
![](tugas1/images/install_ubuntu_server-3.png?raw=true)<br/>
![](tugas1/images/install_ubuntu_server_4.png?raw=true)<br/>
![](tugas1/images/install_ubuntu_server-5.png?raw=true)<br/>
Loading komponen tambahan<br/>
![](tugas1/images/install_ubuntu_server_6.png?raw=true)<br/>
Konfigurasi jaringan<br/>
![](tugas1/images/install_ubuntu_server_7.png?raw=true)<br/>
Mengatur fullname, username, dan password<br/>
![](tugas1/images/install_ubuntu_server_8.png?raw=true)<br/>
![](tugas1/images/install_ubuntu_server_10.png?raw=true)<br/>
![](tugas1/images/install_ubuntu_server_11.png?raw=true)<br/>
![](tugas1/images/install_ubuntu_server-12.png?raw=true)<br/>
Mendapatkan waktu berdasarkan server waktu jaringan<br/>
![](tugas1/images/install_ubuntu_server_13.png?raw=true)<br/>
![](tugas1/images/install_ubuntu_server_14.png?raw=true)<br/>
Partisi disk<br/>
![](tugas1/images/install_ubuntu_server-15.png?raw=true)<br/>
![](tugas1/images/install_ubuntu_server_16.png?raw=true)<br/>
Instalasi sistem operasi<br/>
![](tugas1/images/install_ubuntu_server_17.png?raw=true)<br/>
Konfigurasi apt<br/>
![](tugas1/images/install_ubuntu_server_18.png?raw=true)<br/>


###Instalasi Kippo Honeypot pada Ubuntu Server

![](1_tambah_user_kippo.png?raw=true)<br/>
![](2_edit_visudo.png?raw=true)<br/>
![](3_edit_visudo.png?raw=true)<br/>
![](4_using_port_22.png?raw=true)<br/>
![](5_using_port_22.png?raw=true)<br/>
![](6_using_port_22.png?raw=true)<br/>
![](7_git_clone.png?raw=true)<br/>
![](8_copy_kippo.png?raw=true)<br/>
![](9_nano_kippo.png?raw=true)<br/>
![](11_run_honeypot.png?raw=true)<br/>
![](12_cek_kippo.png?raw=true)<br/>
![](16:52:38_connect to ssh.png?raw=true)<br/>
![](16:53:49 pass gagal.png?raw=true)<br/>
![](16:54:37 login success root.pngg?raw=true)<br/>
![](16:55:48 ls.png?raw=true)<br/>
![](16:56:37 touch pksj.png?raw=true)<br/>
![](16:57:34 ls & rm.png?raw=true)<br/>
![](16:59:41 exit.png?raw=true)<br/>
![](17:00:18 ls terakhir.png?raw=true)<br/>


###Langkah Uji Penetrasi dengan SSH Brute Force Tools
~~####THC Hydra
Tools THC Hydra sudah ada pada OS Kali Linux, sehingga tidak memerlukan instalasi. Begitu juga pada OS Kali Linux, sudah terdapat dictionary password yang sering digunakan dan untuk itu kami tidak perlu mendownload atau mencari dictionary lagi.<br/>
Pada uji penetrasi pertama, kami mecoba untuk mencari password dari user root ubuntu server, namun password tidak ditemukan, padahal password yang kami gunakan ada pada dictionary kali linux. Kemudian kami mendapat referensi, memang by default dari konfigurasi ssh, bahwa kita tidak dapat melakukan ssh pada ubuntu server dengan user root secara langsung.
Kemudian, kami akhirnya mengasumsikan bahwa attacker telah mengetahui username dari server yang akan diserang, sehingga syntax yang kami gunakan adalah :<br/>
> hydra -l ubuntuserver -P /usr/share/wordlists/metasploits/unix_passwords.txt -t 6 ssh://10.151.43.26

~~Kami mencoba untuk melakukan attempt login dengan username **ubuntuserver** dengan dictionary password pada /usr/share/wordlists/metasploits/unix_passwords.txt, menggunakan 6 thread (**-t 6**) pada ubuntu server dengan ip 10.151.43.26. <br/>
![](images/hydra.png?raw=true)

~~####Ncrack
Pada percobaan tools Ncrack melalui kali linux gagal dijalankan, dan error yang muncul adalah sebagai berikut <br/>
![](images/ncrack_error_kali.png?raw=true)

~~Setelah berusaha mendownload library yang dibutuhkan, kemudian me-upgrade OS Kali Linux, hasilnya Ncrack belum bisa dijalankan pada Kali Linux. <br/>
Kami kemudian menggunakan ubuntu desktop (non virtual) untuk mencoba melakukan penetrasi menggunakan Ncrack dan berhasil mendapatkan password dari user **ubuntuserver**
command yang kami jalankan adalah sebagai berikut
> ncrack -p 22 -user ubuntuserver -P 1000_passwords.txt 10.151.43.26

~~Kami mencoba untuk melakukan attempt login dengan username **ubuntuserver** melalui port 22 (ssh) dengan dictionary password yang telah kami download melalui internet yaitu **1000_passwords.txt** pada server 10.151.43.26<br/>
![](images/ncrack_with_ubuntunonvirtual.png?raw=true)<br/>
##Uji Penetrasi 2
Setelah fail2ban diinstall, lakukan setting iptables di Ubuntu Server<br/>
> sudo iptables -A INPUT -i lo -j ACCEPT <br/>
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT <br/>
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT <br/>
sudo iptables -A INPUT -j DROP <br/>

~~Kemudian restart fail2ban dengan command
>sudo service fail2ban restart


~~Menampilkan iptables yang telah diset<br/>
![](images/showing_iptables_dan_fail2ban.png?raw=true)
Mencoba meng-ssh Ubuntu Server menggunakan fail2ban <br/>
![](images/gagal_ssh_by_fail2ban_iptables.png?raw=true)
Penolakan koneksi ssh dr Ubuntu Server tercatat dalam log file2ban<br/>
![](images/logfile_file2ban.png?raw=true)


##Kesimpulan dan Saran
####Kesimpulan:


####Saran:




