##Pendahuluan


##Dasar Teori
###Metasploit
Metasploit adalah sebuah framework yang dapat digunakan untuk meretas berbagai jenis aplikasi, sistem operasi, web, dan lain sebagainya. Metasploit memiliki banyak modul, payload, dan exploit yang dapat digunakan untuk melancarkan aksi sang hacker. Banyak sekali hacker yang "suka" dengan aplikasi berbasis framework ini karena dukungan exploit yang selalu bertambah setiap harinya.

###Metasploitable
Metasploitable adalah sebuah virtual machine yang sengaja dibuat sebagai versi lemah dari ubuntu linux. Metasploitable didesain untuk menguji coba security tools dan kelemahan suatu server.

###Exploit
Exploit adalah sebuah kode yang menyerang keamanan_komputer secara spesifik. Exploit banyak digunakan untuk penentrasi baik secara legal ataupun ilegal untuk mencari kelemahan (Vulnerability) pada komputer tujuan. Bisa juga dikatakan sebuah perangkat lunak yang menyerang kerapuhan keamanan (security vulnerability) yang spesifik namun tidak selalu bertujuan untuk melancarkan aksi yang tidak diinginkan. Banyak peneliti keamanan komputer menggunakan exploit untuk mendemonstrasikan bahwa suatu sistem memiliki kerapuhan.

###Instalasi Metasploit
1. Download metasploit: http://www.metasploit.com/download/
2. Setelah di download, buka terminal, lalu pindah kan alamat direktori ke tempat metasploit yang tadi di download
3. Setelah pindah ke direktori tool metasploit berada , ketikkan perintah berikut untuk mulai menginstall
	> sudo chmod +x metasploit-latest-linux-installer.run
	> sudo ./metasploit-latest-linux-installer.run
    > sudo chmod +x metasploit-latest-linux-x64-installer.run
	> sudo ./metasploit-latest-linux-x64-installer.run
4. Setelah berhasil, ketikkan syntax berikut untuk mengetes
	> sudo msfconsole

###Instalasi Metasploitable
1. Download metasploitable: https://sourceforge.net/projects/metasploitable/files/Metasploitable2/
2. Extract file yang sudah di download
3. Nyalakan virtual box
4. Tambahkan mesin virtual versi linux
5. Set RAM paling tidak 512MB, klik next
6. Pilih "use an existing virtual hard drive file". Kemudian pilih file vmdk dari file yang telah di download tadi. klik create.
7. Secara otomatis akan menuju booting metasploitable dengan default username dan password msfadmin

###Uji Penetrasi
![](image/2.png?raw=true)<br/>
![](image/3.png?raw=true)<br/>
Masuk ke console metasploitable dengan mengetikkan sudo msfconsole. Gunakan exploit (dalam tugas ini kami menggunakan postgres_payload) dengan syntax use exploit/linux/postgres/postgres_payload<br/>
![](image/1.png?raw=true)<br/>
Kemudian setting alamat ip atau alamat web server yang ingin diserang. Dalam kasus ini kami menyetting RHOST menjadi ip dari sistem ooperasi metasploitable<br/>
![](image/4.png?raw=true)<br/>
Jalankan dengan mengetikkan run. Kemudian akan membuat session dengan memunculkan meterpreter. Ketika telah berganti menjadi tampilan shell artinya kami sudah dapat masuk ke metasploitable dengan user postgres (belum root)<br/>
![](image/5.png?raw=true)<br/>
Untuk mengetahui passsword dari postgres kami menggunakan syntax use auxiliary/scanner/postgres/postgres_login. Kemudian kami menyetting RHOSTS menjadi ip dari metaspoitable. Jalankan exploit. Terlihat pada gambar bahwa login yang dilakukan berhasil dengan user postgres dan password postgres <br/>
![](image/6.png?raw=true)<br/>
Masuk kembali ke postgres_payload dengan cara yang sama sampai akhirnya masuk ke meterpreter lagi. Ketikkan shell dan ketikkan psql -U postgres dan masukkan password postgres. Untuk melihat database yang ada, ketikkan \l . Pilih database yang sekarang kemudian buatlah sebuah tabel bernama penteslab untuk membackup data yang diinginkan dari server. Copy dari misal sebuah file /etc/passwd untuk mengcopy semua user dari metasploitable. Selanjutnya baca tabel yang sudah dibuat dengan syntax select input from penteslab. Hasilnya akan seperti gambar di bawah ini<br/>
![](image/7.png?raw=true)<br/>

##Kesimpulan dan Saran
####Kesimpulan:
- postgres_payload dapat mengeksploitasi dbms postgres pada server
- postgres_payload dapat melakukan pem-backup-an data dari server ke dbms postgres yang dapat dibaca oleh penyerang

####Saran:
- postgres_payload tidak dapat berjalan sendirian exploit yang lain agar dapat masuk sebagai root dan mengekploitasi dbms postgres pada server


