##Pendahuluan
Dalam merancang sebuah sistem atau jaringan yang aman, pemilik melakukan berbagai usaha untuk menjamin sistem atau jaringan tersebut benar benar aman. Salah satu cara untuk menjamin keamanan tersebut adalah dengan menyerang sistem atau jaringan itu sendiri, dengan mengetahui cara menyerang sistem atau jaringan tersebut diharapkan pengembang sistem dapat melakukan pencegahan agar sistem tidak bisa diserang dengan cara yang sama.

Kali ini, penulis akan mengulas tentang bagaimana sebuah sistem dapat diserang dengan brute force attack, dimana kemudian akan dilakukan usaha pencegahan penyerangan tersebut dengan melakukan brute force countermeasures. 

Sistem yang menjadi bahan percobaan kali ini adalah ubuntu server yang telah terinstall SSH server, dimana penulis juga akan melakukan percobaan sebanyak 2 kali penetrasi. Pada penetrasi pertama,dilakukan penyerangan pada sistem ubuntu server melalui SSH server yang telah terinstall dan pada penetrasi kedua akan dilakukan upaya pencegahan (countermeasures) pada ubuntu server. 

Untuk melakukan brute force attack pada ubuntu server, penulis melakukan penyerangan melalui Sistem operasi Kali Linux, dengan software Hydra dan ncrack. Sementara itu, countermeasure dilakukan dengan aplikasi file2ban yang terinstall di ubuntu server.

Pada tulisan kali ini, akan dijelaskan secara bertahap dimulai dari penjelasan tahap uji penetrasi 1, dimulai dari instalasi Ubuntu server,instalasi OS untuk penetrasi,  instalasi SSH server,hingga uji penetrasi dengan SSH brute force tools. Dilanjutkan dengan uji penetrasi 2 dengan tahapan yang dimulai dari konfigurasi fail2ban, konfigurasi SSH server non-default, hingga uji penetrasi dengan SSH brute force tools, yang ditutup dengan kesimpulan dan saran.

##Dasar Teori
Ubuntu Server adalah salah satu varian dari distro linux Ubuntu yang didesain untuk diinstall di server. Ubuntu Server tidak menyediakan GUI, yang ada hanya CLI (Comand Line Interface). Ubuntu Server digunakan untuk menangani memori sampai puluhan Giga ataupun menangani Multicore CPU.

Kali Linux adalah penerus distro BackTrack. Sama seperti BackTrack, distro ini dilengkapi dengan berbagai tools Linux untuk melakukan penetration testing. Dengan Kali Linux, pengguna yang melakukan pengujian keamanan tidak perlu repot men-install atau membuat kode program/script baru. Efek sampingnya: distro Linux seperti ini juga kerap disalahgunakan oleh script kiddie. Istilah script kiddie adalah sebutan untuk orang yang menjalankan tool dan mengikuti panduan tanpa memahami apa yang dilakukan oleh dirinya. Hal ini berbeda dari hacker yang memahami setiap aksi yang dilakukannya dan mampu membuat tool/script-nya sendiri.

SSH merupakan singkatan dari Secure Shell yang merupakan suatu aplikasi pengganti remote login tak jauh berbeda dengan Rsh dan rlogin. SSH merupakan suatu protokol jaringan yang  dengan adanya SSH ini kita dapat menukarkan data melalui saluran yang aman antara dua perangkat jaringan. Protokol jaringan ini sering digunakan pada sistem operasi Linux dan dirancang sebagai pengganti Telnet dan shell remote tak aman lainnya.

THC Hydra

##Uji Penetrasi 1
###Instalasi Ubuntu Server
Memilih bahasa yang digunakan untuk menjalankan sistem operasi
![](images/install_ubuntu_server_1.png?raw=true)
Memilih lokasi
![](images/install_ubuntu_server_2.png?raw=true)
Konfigurasi keyboard
![](images/install_ubuntu_server-3.png?raw=true)
![](images/install_ubuntu_server_4.png?raw=true)
![](images/install_ubuntu_server-5.png?raw=true)
Loading komponen tambahan
![](images/install_ubuntu_server_6.png?raw=true)
Konfigurasi jaringan
![](images/install_ubuntu_server_7.png?raw=true)
Mengatur fullname, username, dan password
![](images/install_ubuntu_server_8.png?raw=true)
INI SALAH SKRINSOT
![](images/install_ubuntu_server_9.png?raw=true)
![](images/install_ubuntu_server_10.png?raw=true)
![](images/install_ubuntu_server_11.png?raw=true)
![](images/install_ubuntu_server-12.png?raw=true)
Mendapatkan waktu berdasarkan server waktu jaringan
![](images/install_ubuntu_server_13.png?raw=true)
![](images/install_ubuntu_server_14.png?raw=true)
Partisi disk
![](images/install_ubuntu_server-15.png?raw=true)
![](images/install_ubuntu_server_16.png?raw=true)
Instalasi sistem operasi
![](images/install_ubuntu_server_17.png?raw=true)
Konfigurasi apt
![](images/install_ubuntu_server_18.png?raw=true)


###Instalasi Kali Linux
Memilih bahasa yang digunakan untuk menjalankan sistem operasi
![](images/install_kali.png?raw=true)
Memilih lokasi
![](images/install_kali_2.png?raw=true)
![](images/install_kali_3.png?raw=true)
![](images/install_kali_4.png?raw=true)
Memilih waktu
![](images/install_kali_5.png?raw=true)
Konfigurasi keyboard
![](images/install_kali_6.png?raw=true)
Loading komponen tambahan
![](images/install_kali_7.png?raw=true)
Konfigurasi jaringan
![](images/install_kali_8.png?raw=true)
![](images/install_kali_9.png?raw=true)
Mengatur fullname, username, dan password
![](images/install_kali_10.png?raw=true)
Mendapatkan waktu berdasarkan server waktu jaringan
![](images/install_kali_11.png?raw=true)
![](images/install_kali_12.png?raw=true)
Partisi disk
![](images/install_kali_13.png?raw=true)
![](images/install_kali_14.png?raw=true)
![](images/install_kali_15.png?raw=true)
![](images/install_kali_16.png?raw=true)
Instalasi sistem
![](images/install_kali_17.png?raw=true)


###Instalsi SSH Server
![](images/install_ssh_server.png?raw=true)


###Instalsi THC Hydra
![](images/install_thc_hydra.png?raw=true)


###Instalsi SSH Server
![](images/install_ssh_server.png?raw=true)


###Langkah Uji Penetrasi dengan SSH Brute Force Tools
![](images/hydra.png?raw=true)


##Uji Penetrasi 2



##Kesimpulan dan Saran


