##Pendahuluan
Dalam merancang sebuah sistem atau jaringan yang aman, pemilik melakukan berbagai usaha untuk menjamin sistem atau jaringan tersebut benar benar aman. Salah satu cara untuk menjamin keamanan tersebut adalah dengan menyerang sistem atau jaringan itu sendiri, dengan mengetahui cara menyerang sistem atau jaringan tersebut diharapkan pengembang sistem dapat melakukan pencegahan agar sistem tidak bisa diserang dengan cara yang sama.

Kali ini, penulis akan mengulas tentang bagaimana sebuah sistem dapat diserang dengan brute force attack, dimana kemudian akan dilakukan usaha penganalisaan penyerangan tersebut dengan membuat suatu sistem palsu yang disebut honeypot.

Sistem yang menjadi bahan percobaan kali ini adalah Ubuntu Server yang telah terinstall Kippo Honeypot. Penulis menggunakan Kali Linux untuk menyerang Ubuntu Server tersebut.

Pada tulisan kali ini, akan dijelaskan secara bertahap dimulai dari penjelasan tahap persiapan, dimulai dari instalasi Ubuntu Server, instalasi OS Kali Linux untuk penetrasi, instalasi Kippo Honeypot beserta konfigurasi, hingga uji penetrasi dengan SSH brute force tools. Pada akhir tulisan ini akan terdapat kesimpulan dan saran.

##Dasar Teori
###Ubuntu Server
Ubuntu Server adalah salah satu varian dari distro linux Ubuntu yang didesain untuk diinstall di server. Ubuntu Server tidak menyediakan GUI, yang ada hanya CLI (Comand Line Interface). Ubuntu Server digunakan untuk menangani memori sampai puluhan Giga ataupun menangani Multicore CPU.

###Kali Linux
Kali Linux adalah penerus distro BackTrack. Sama seperti BackTrack, distro ini dilengkapi dengan berbagai tools Linux untuk melakukan penetration testing. Dengan Kali Linux, pengguna yang melakukan pengujian keamanan tidak perlu repot men-install atau membuat kode program/script baru. Efek sampingnya: distro Linux seperti ini juga kerap disalahgunakan oleh script kiddie. Istilah script kiddie adalah sebutan untuk orang yang menjalankan tool dan mengikuti panduan tanpa memahami apa yang dilakukan oleh dirinya. Hal ini berbeda dari hacker yang memahami setiap aksi yang dilakukannya dan mampu membuat tool/script-nya sendiri.

###Brute Force Attack
Brute Force Attack adalah metode untuk meretas password (password cracking) dengan cara mencoba semua kemungkinan kombinasi yang ada pada “wordlist“. Metode ini dijamin akan berhasil menemukan password yang ingin diretas. Namun, proses untuk meretas password dengan menggunakan metode ini akan memakan banyak waktu.

###Kippo Honeypot
Honeypot adalah suatu sistem palsu yang sengaja dibuat untuk menjebak attacker menyerang sistem yang aslinya. Apabila attacker berhasil masuk ke honeypot, sistem yang aslinya tetap aman tak terpengaruh sedikit pun. 

##Persiapan Uji Penetrasi
###Instalasi Ubuntu Server
Memilih bahasa yang digunakan untuk menjalankan sistem operasi<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_1.png?raw=true)<br/>
Memilih lokasi<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_2.png?raw=true)<br/>
Konfigurasi keyboard<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server-3.png?raw=true)<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_4.png?raw=true)<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server-5.png?raw=true)<br/>
Loading komponen tambahan<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_6.png?raw=true)<br/>
Konfigurasi jaringan<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_7.png?raw=true)<br/>
Mengatur fullname, username, dan password<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_8.png?raw=true)<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_10.png?raw=true)<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_11.png?raw=true)<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server-12.png?raw=true)<br/>
Mendapatkan waktu berdasarkan server waktu jaringan<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_13.png?raw=true)<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_14.png?raw=true)<br/>
Partisi disk<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server-15.png?raw=true)<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_16.png?raw=true)<br/>
Instalasi sistem operasi<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_17.png?raw=true)<br/>
Konfigurasi apt<br/>
![](https://github.com/kharismana31/PKSJ/blob/master/tugas1/images/install_ubuntu_server_18.png?raw=true)<br/>


###Instalasi Kippo Honeypot pada Ubuntu Server
Pertama lakukan update pada Ubuntu Server

> apt-get update

Kemudian ganti port (defaultnya port 22) dengan port 2222 pada file sshd_config, caranya ketikkan perintah ini:

> nano /etc/ssh/sshd_config

lalu edit port yang tertera di sana dengan port 2222. Jika sudah lakukan perintah restart

> /etc/init.d/ssh restart

Selanjutnya, download semua kebutuhan untuk Kippo dengan mengetikkan perintah:

> apt-get install python-dev openssl python-openssl python-pyasn1 python-twisted

Sebelum melangkah lebih lanjut, install git pada Ubuntu Server terlebih dahulu

> apt-get install git

Ketikkan perintah ini untuk menjalankan honeypot pada port 22

> apt-get install authbind

Sebelum memulai Kippo, tambahkan user Kippo pada Ubuntu server dengan megetikkan perintah di bawah ini

![](1_tambah_user_kippo.png?raw=true)<br/>

Tambahkan user Kippo pada list user yang dapat mengakses perintah sudo dengan mengetikkan perintah ini

![](2_edit_visudo.png?raw=true)<br/>

Tambahkan satu line ini di bawah "root" user 

![](3_edit_visudo.png?raw=true)<br/>

Untuk menyelesaikan settingan Kippo lakukan perintah di bawah ini

![](4_using_port_22.png?raw=true)<br/>

![](5_using_port_22.png?raw=true)<br/>

![](6_using_port_22.png?raw=true)<br/>

Selanjutnya lakukan perintah ini untuk mendowload Kippo versi terbaru 

![](7_git_clone.png?raw=true)<br/>

Copy dan edit file konfigurasi Kippo dari port 2222 menjadi port 22 

![](8_copy_kippo.png?raw=true)<br/>

![](9_nano_kippo.png?raw=true)<br/>

Kemudian edit file start.sh dengan mengetikkan:

![](10_nano_start.png?raw=true)<br/>

Ubah line ini:

> twistd -y kippo.tac -l log/kippo.log --pidfile kippo.pid

menjadi:

> authbind --deep twistd -y kippo.tac -l log/kippo.log --pidfile kippo.pid

Dan terakhir jalankan honeypot

![](11_run_honeypot.png?raw=true)<br/>

Untuk mengecek status Kippo telah "listening" ketikkan perintah berikut

![](12_cek_kippo.png?raw=true)<br/>

###Hasil Uji Penetrasi dengan SSH Brute Force Tools: Medusa
![](16-52-38_connect_to_ssh.png?raw=true)<br/>
![](16-53-49_pass_gagal.png?raw=true)<br/>
![](16-54-37_login_success_root.png?raw=true)<br/>
![](16-55-48_ls.png?raw=true)<br/>
![](16-56-37_touch_pksj.png?raw=true)<br/>
![](16-57-34_ls_rm.png?raw=true)<br/>
![](16-59-41_exit.png?raw=true)<br/>
![](17-00-18_ls_terakhir.png?raw=true)<br/>

##Kesimpulan dan Saran
####Kesimpulan:
Dari percobaan yang telah dilakukan, dapat disimpulkan bahwa:<br/>
1. Kippo SSH honeypot dapat digunakan untuk mengelabui Attacker dengan memanipulasi port dari SSH dan port dari kippo honeypotnya, yang membuat kippo diakses melalui port default SSH yaitu 22
2. Ditujukan untuk seakan akan sistem dapat dibobol agar dapat melihat aktivitas Attacker saat masuk dalam sistem
3. 

####Saran:
Dalam hal mengelabui Attacker yang pake brute force attack, dan kita pake Kippo SSH Honeypot, pada database password yang bisa diserang brute force attack, 




