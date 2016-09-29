##Pendahuluan
Dalam merancang sebuah sistem atau jaringan yang aman, pemilik melakukan berbagai usaha untuk menjamin sistem atau jaringan tersebut benar benar aman. Salah satu cara untuk menjamin keamanan tersebut adalah dengan menyerang sistem atau jaringan itu sendiri, dengan mengetahui cara menyerang sistem atau jaringan tersebut diharapkan pengembang sistem dapat melakukan pencegahan agar sistem tidak bisa diserang dengan cara yang sama.

Kali ini, penulis akan mengulas tentang bagaimana sebuah sistem dapat diserang dengan brute force attack, dimana kemudian akan dilakukan usaha pencegahan penyerangan tersebut dengan melakukan brute force countermeasures. 

Sistem yang menjadi bahan percobaan kali ini adalah ubuntu server yang telah terinstall SSH server, dimana penulis juga akan melakukan percobaan sebanyak 2 kali penetrasi. Pada penetrasi pertama,dilakukan penyerangan pada sistem ubuntu server melalui SSH server yang telah terinstall dan pada penetrasi kedua akan dilakukan upaya pencegahan (countermeasures) pada ubuntu server. 

Untuk melakukan brute force attack pada ubuntu server, penulis melakukan penyerangan melalui Sistem operasi Kali Linux, dengan software Hydra dan ncrack. Sementara itu, countermeasure dilakukan dengan aplikasi file2ban yang terinstall di ubuntu server.

Pada tulisan kali ini, akan dijelaskan secara bertahap dimulai dari penjelasan tahap uji penetrasi 1, dimulai dari instalasi Ubuntu server,instalasi OS untuk penetrasi,  instalasi SSH server,hingga uji penetrasi dengan SSH brute force tools. Dilanjutkan dengan uji penetrasi 2 dengan tahapan yang dimulai dari konfigurasi fail2ban, konfigurasi SSH server non-default, hingga uji penetrasi dengan SSH brute force tools, yang ditutup dengan kesimpulan dan saran.

##Dasar Teori
###Ubuntu Server
Ubuntu Server adalah salah satu varian dari distro linux Ubuntu yang didesain untuk diinstall di server. Ubuntu Server tidak menyediakan GUI, yang ada hanya CLI (Comand Line Interface). Ubuntu Server digunakan untuk menangani memori sampai puluhan Giga ataupun menangani Multicore CPU.

###Kali Linux
Kali Linux adalah penerus distro BackTrack. Sama seperti BackTrack, distro ini dilengkapi dengan berbagai tools Linux untuk melakukan penetration testing. Dengan Kali Linux, pengguna yang melakukan pengujian keamanan tidak perlu repot men-install atau membuat kode program/script baru. Efek sampingnya: distro Linux seperti ini juga kerap disalahgunakan oleh script kiddie. Istilah script kiddie adalah sebutan untuk orang yang menjalankan tool dan mengikuti panduan tanpa memahami apa yang dilakukan oleh dirinya. Hal ini berbeda dari hacker yang memahami setiap aksi yang dilakukannya dan mampu membuat tool/script-nya sendiri.

###SSH
SSH merupakan singkatan dari Secure Shell yang merupakan suatu aplikasi pengganti remote login tak jauh berbeda dengan Rsh dan rlogin. SSH merupakan suatu protokol jaringan yang  dengan adanya SSH ini kita dapat menukarkan data melalui saluran yang aman antara dua perangkat jaringan. Protokol jaringan ini sering digunakan pada sistem operasi Linux dan dirancang sebagai pengganti Telnet dan shell remote tak aman lainnya.

###Brute Force Attack
Brute Force Attack adalah metode untuk meretas password (password cracking) dengan cara mencoba semua kemungkinan kombinasi yang ada pada “wordlist“. Metode ini dijamin akan berhasil menemukan password yang ingin diretas. Namun, proses untuk meretas password dengan menggunakan metode ini akan memakan banyak waktu.

THC Hydra

##Uji Penetrasi 1
###Instalasi Ubuntu Server
Memilih bahasa yang digunakan untuk menjalankan sistem operasi<br/>
![](images/install_ubuntu_server_1.png?raw=true)<br/>
Memilih lokasi<br/>
![](images/install_ubuntu_server_2.png?raw=true)<br/>
Konfigurasi keyboard<br/>
![](images/install_ubuntu_server-3.png?raw=true)<br/>
![](images/install_ubuntu_server_4.png?raw=true)<br/>
![](images/install_ubuntu_server-5.png?raw=true)<br/>
Loading komponen tambahan<br/>
![](images/install_ubuntu_server_6.png?raw=true)<br/>
Konfigurasi jaringan<br/>
![](images/install_ubuntu_server_7.png?raw=true)<br/>
Mengatur fullname, username, dan password<br/>
![](images/install_ubuntu_server_8.png?raw=true)<br/>
![](images/install_ubuntu_server_10.png?raw=true)<br/>
![](images/install_ubuntu_server_11.png?raw=true)<br/>
![](images/install_ubuntu_server-12.png?raw=true)<br/>
Mendapatkan waktu berdasarkan server waktu jaringan<br/>
![](images/install_ubuntu_server_13.png?raw=true)<br/>
![](images/install_ubuntu_server_14.png?raw=true)<br/>
Partisi disk<br/>
![](images/install_ubuntu_server-15.png?raw=true)<br/>
![](images/install_ubuntu_server_16.png?raw=true)<br/>
Instalasi sistem operasi<br/>
![](images/install_ubuntu_server_17.png?raw=true)<br/>
Konfigurasi apt<br/>
![](images/install_ubuntu_server_18.png?raw=true)<br/>


###Instalasi Kali Linux
Memilih bahasa yang digunakan untuk menjalankan sistem operasi<br/>
![](images/install_kali.png?raw=true)<br/>
Memilih lokasi<br/>
![](images/install_kali_2.png?raw=true)<br/>
![](images/install_kali_3.png?raw=true)<br/>
![](images/install_kali_4.png?raw=true)<br/>
Memilih waktu<br/>
![](images/install_kali_5.png?raw=true)<br/>
Konfigurasi keyboard<br/>
![](images/install_kali_6.png?raw=true)<br/>
Loading komponen tambahan<br/>
![](images/install_kali_7.png?raw=true)<br/>
Konfigurasi jaringan<br/>
![](images/install_kali_8.png?raw=true)<br/>
![](images/install_kali_9.png?raw=true)<br/>
Mengatur fullname, username, dan password<br/>
![](images/install_kali_10.png?raw=true)<br/>
Mendapatkan waktu berdasarkan server waktu jaringan<br/>
![](images/install_kali_11.png?raw=true)<br/>
![](images/install_kali_12.png?raw=true)<br/>
Partisi disk<br/>
![](images/install_kali_13.png?raw=true)<br/>
![](images/install_kali_14.png?raw=true)<br/>
![](images/install_kali_15.png?raw=true)<br/>
![](images/install_kali_16.png?raw=true)<br/>
Instalasi sistem<br/>
![](images/install_kali_17.png?raw=true)<br/>


###Instalasi SSH Server
![](images/install_ssh_server.png?raw=true)<br/>


###Langkah Uji Penetrasi dengan SSH Brute Force Tools
####THC Hydra
Tools THC Hydra sudah ada pada OS Kali Linux, sehingga tidak memerlukan instalasi. Begitu juga pada OS Kali Linux, sudah terdapat dictionary password yang sering digunakan dan untuk itu kami tidak perlu mendownload atau mencari dictionary lagi.<br/>
Pada uji penetrasi pertama, kami mecoba untuk mencari password dari user root ubuntu server, namun password tidak ditemukan, padahal password yang kami gunakan ada pada dictionary kali linux. Kemudian kami mendapat referensi, memang by default dari konfigurasi ssh, bahwa kita tidak dapat melakukan ssh pada ubuntu server dengan user root secara langsung.
Kemudian, kami akhirnya mengasumsikan bahwa attacker telah mengetahui username dari server yang akan diserang, sehingga syntax yang kami gunakan adalah :<br/>
> hydra -l ubuntuserver -P /usr/share/wordlists/metasploits/unix_passwords.txt -t 6 ssh://10.151.43.26

Kami mencoba untuk melakukan attempt login dengan username **ubuntuserver** dengan dictionary password pada /usr/share/wordlists/metasploits/unix_passwords.txt, menggunakan 6 thread (**-t 6**) pada ubuntu server dengan ip 10.151.43.26. <br/>
![](images/hydra.png?raw=true)

####Ncrack
Pada percobaan tools Ncrack melalui kali linux gagal dijalankan, dan error yang muncul adalah sebagai berikut <br/>
![](images/ncrack_error_kali.png?raw=true)

Setelah berusaha mendownload library yang dibutuhkan, kemudian me-upgrade OS Kali Linux, hasilnya Ncrack belum bisa dijalankan pada Kali Linux. <br/>
Kami kemudian menggunakan ubuntu desktop (non virtual) untuk mencoba melakukan penetrasi menggunakan Ncrack dan berhasil mendapatkan password dari user **ubuntuserver**
command yang kami jalankan adalah sebagai berikut
> ncrack -p 22 -user ubuntuserver -P 1000_passwords.txt 10.151.43.26

Kami mencoba untuk melakukan attempt login dengan username **ubuntuserver** melalui port 22 (ssh) dengan dictionary password yang telah kami download melalui internet yaitu **1000_passwords.txt** pada server 10.151.43.26<br/>
![](images/ncrack_with_ubuntunonvirtual.png?raw=true)<br/>
##Uji Penetrasi 2



##Kesimpulan dan Saran
####Kesimpulan:
- Sistem keamanan pada suatu Ubuntu server bisa diserang dari perangkat lain dengan cara brute force attack via SSH server, terutama jika password yang digunakan pada ubuntu server adalah password umumnya. Perangkat lain ini melakukan penyerangan dengan menggunakan software ncrack dan hydra pada sistem operasi Kali Linux. Kali linux dipilih sebagai Sistem operasi penyerang karena dapat membantu 2 software penyerang tadi, dengan menyediakan kamus data tentang password yang sering digunakan, sehingga aplikasi tersebut bisa melakukan brute force attack dengan mencoba satu demi satu password tersebut.
- Sistem keamanan pada ubuntu server bisa dijaga dari serangan brute force attack dengan bantuan aplikasi pencegah serangan tersebut, seperti fail2ban. Aplikasi semacam fail2ban ini dapat mencegah aktivitas login berkali kali dari ip address yang sama dengan memblok ip address yang gagal login tersebut. 

####Saran:
- Dengan dilakukannya uji penetrasi menyerang dan pencegahan terhadap serangan ini, telah disimpulkan bahwa brute force attack bisa membahayakan sistem keamanan ubuntu server, terutama jika pengguna ubuntu server menggunakan password yang sudah biasa digunakan dan telah terdaftar pada dictionary password yang biasa digunakan. Oleh karena itu penulis menyarankan kepada pengguna ubuntu server untuk mengkonfigurasi password dengan kombinasi yang unik untuk mengecilkan kemungkinan sistem keamanan diserang dengan brute force attack atau mengimplementasikan penggunaan aplikasi yang mencegah serangan brute force pada linux, seperti fail2ban agar sistem dapat memblok ip address dari login yang gagal berkali kali tersebut.


