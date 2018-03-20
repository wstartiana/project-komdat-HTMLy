# New Document
<h1 align="center"><img src="https://raw.githubusercontent.com/danpros/htmly/master/system/resources/images/logo-big.png"></h1>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:



# Sekilas Tentang
[`^ kembali ke atas ^`](#)

**HTMLy** adalah *Databaseless Blogging Platform* atau Flat-File Blog yang *open source* dan mengutamakan kesederhanaan serta kecepatan, yang ditulis dalam `PHP`. HTMLy disebut juga sebagai Flat-File CMS yang baik karena dapat mengelola konten dari user.

HTMLy menggunakan algoritme unik untuk menemukan atau mencantumkan konten berdasarkan tanggal, jenis, kategori, tag, atau pengarang, dan kinerjanya akan tetap berjalan dengan cepat meskipun kita memiliki ribuan pos dan ratusan tag.

Sebagai flat-file blog atau flat-file CMS, HTMLy didesain untuk berjalan lancar meski menggunakan spesifikasi server minimal. Dengan RAM 512MB atau bahkan kurang, HTMLy bisa menangani lebih dari 10.000 posting tanpa masalah apapun.




# Instalasi
[`^ kembali ke atas ^`](#)

#### Kebutuhan Sistem :
- Unix, Linux atau Windows.
- PHP versi >= 5.3
- PHP-XML package
- Web Server(Apache2).

#### Virtual private server membutuhkan:
- virtual box
- ubuntu-server.vdi

#### Proses Instalasi :
##### Instalasi Virtual Private Server
A. Setting port-forwarding VM

   **Install Virtual Private Server**
   
   1. Buka virtualbox
   2. masuk 'Settings -> Network -> Advanced -> Port Forwarding' dan tambahkan dua aturan berikut.

Name   | Protocol   | Host IP    | Host Port  | Guest IP   | Guest Port
----   | --------   | -------    | ---------  | --------   | ----------
http   | TCP        |            | 8888       |            | 80
ssh    | TCP        |            | 2222       |            | 22

sehingga jika kita mengakses localhost:8888 di host, maka akan diteruskan ke localhost:80 di guest (VM).

3. kemudian  jalankan VM dengan login username student dan password student.

**Instalasi LAMP (Linux Apache MySQL PHP)**

##### a. Instal SSH
	sudo apt update
	sudo apt install ssh
Setelah terinstal SSH, kita bisa mengakses VM secara remote. Buka terminal di host untuk login remote ke port 2222.
##### b. akses remote dari host
	ssh student@localhost -p 2222

##### c. instal Apache, MySQL, PHP
	sudo apt install apache2
	sudo apt install mysql-server
	sudo apt install php
	sudo apt install libapache2-mod-php
	sudo apt install php-mysql
	sudo apt install php-gd php-mcrypt php-mbstring php-xml php-ssh2
	sudo service apache2 restart
Cek instalasi Apache dengan membuka laman http://localhost:8888.

##### Instalasi HTMLy

1.Ubah status menjadi superuser agar mendapatkan permission yang penuh.

	$ sudo su
    
2.Masuk ke directory /var/www/html pada host.

	$ cd /var/www/html

3.Lakukan cloning repository htmly dari github

	$ git clone "https://github.com/danpros/htmly"
    
4.Masuk ke directory htmly
	
    $ cd htmly
    
5.Kemudian donwload juga file installer.php

	$ wget "https://github.com/danpros/htmly/releases/download/v2.7.4/installer.php"
    
6.Ubah kepemilikan ke user www-data (webserver)

	$ sudo chown -R www-data:www-data /var/www/html/htmly
    
7.Buka halaman http://localhost:8888/htmly/installer.php untuk instalasi lebih lanjut.

-------------
                                                                    
jika pada saat membuka **http://localhost:8888/htmly/installer.php** terdapat **error: no permission to write in the Directory** serta **Warning:Your rewriteRule is not ready to use. Help!** 

lakukan langkah berikut:

Set Up mod_rewrite for Apache

1.Enabling mod_rewrite

	$ sudo a2enmod rewrite
    
2.Lakukan modifikasi pada file .htacces dengan membuka file default apache configuration

	$ sudo nano /etc/apache2/sites-enabled/000-default.conf

3.Didalam file anda akan menemukan blcok <VirtualHost *:80> masukkan block berikut pada line 1, kemudian save.

	...
	<Directory /var/www/html>
    	Options Indexes FollowSymLinks MultiViews
    	AllowOverride All
    	Order allow,deny
    	allow from all
	</Directory>
	...
    
4.Restart apache

	$ sudo service apache2 restart
    
5.coba akses kembali **http://localhost:8888/htmly/installer.php**. seharusnya sudah bisa melakukan instalasi.



# Konfigurasi
[`^ kembali ke atas ^`](#)

- Untuk menentukan konfigurasi umum seperti, site url, timezone, title, tagline, deskripsi blog dan pengaturan lainnya kita dapat membuka menu bar **Config** dan mengisi field yang diinginkan. 
![1](image/konfig.png)

![2](image/isikonfig.png)

    
- Untuk memperindah aplikasi, kita dapat mengganti tema dengan :
	1. Buka laman https://www.htmly.com/download/themes
	2. pilih tema web yang diinginkan. misal tema *ignite*.
	   - ![3](image/tema.PNG)
	3. Download repositorinya
		```bash
		$ git clone https://github.com/danpros/htmly-ignite"
		```
	4. Ganti nama foldernya menjadi ''ignite''
		```bash
		$ mv htmly-ignite ignite
		```
	5. Login kembali.
	   Ganti`config key` dengan value `themes/ignite`, kemudian 'submit'. cek menu 'home' untuk melihat perubahan.
	   - ![4](image/gantitema.png)

# Maintenance
[`^ kembali ke atas ^`](#)

- Hapus *cache* : Kita dapat Menghapus *cache* yang ada pada website. Pada menu Dashboard admin, pilih tab *clear cache* maka secara otomatis akan menghapus isi *cache* aplikasi
- Maintenance Konfigurasi tema, pengaturan jumlah page yang tampil dan sebagainya yang terdapat di HTMLy dapat dilihat/diubah di http://localhost/htmly/admin/config; (localhost dapat berupa alamat web atau localhost).



# Otomatisasi
[`^ kembali ke atas ^`](#)

Jika terasa sulit jika diinstal melalui cara sebelumnya, HTMLy juga dapat diinstal dengan menggunakan web installer dan juga zip archive.

#### Web Installer
1. Download installer.php di https://github.com/danpros/htmly/releases/tag/v2.7.4
2. Masukan ke dalam  folder root web misal /var/www/htmly
3. Kunjungi domainmu www.example.com/installer.php

#### Zip Archive
1. Download versi terakhir, ekstrak, dan kemudian upload file yang telah diekstrak ke server. Pastikan folder instalasi dapat ditulis oleh server

2. Konfigurasi manual
```
1. Ubah config.ini.example didalam folder config, menjadi config.ini (atau bisa membuat file config/config.ini baru.

2. Buat YourUsername.ini didalam folder config/users atau rename file username.ini.example dan tulis passwordmu disana:

	password = YourPassword
    
3. Sebagai tambahan, HTMLy mensupport role user admin, dengan menambah line role = admin ke user yang telah dipilih.
	- User yang mempunyai role admin bisa mengedit/mendelete semua post user.
	- Untuk mengakses panel admin, add/login dapat dengan menambahkannya dalam akhir alamat web contoh  www.yoursite.com/login
```


# Cara Pemakaian
[`^ kembali ke atas ^`](#)

Cara pemakaian **HTMLy** ini sangat mudah, karena aplikasi ini menyediakan *interface* yang sederhana sehingga mudah dimengerti. Berikut untuk lebih jelasnya :
1. Sebelum menggunakan HTMLy, kita wajib mengisi *username* dan *password*, selebihnya seperti deskripsi singkat tentang Blog yang ingin di buat dan link akun bersifat opsional. 

    ![1](image/1.PNG)

2.Setelah mengisi username dan password selanjutnya kita akan masuk ke halaman *Home*. Di halaman *Home* kita bisa langsung membuat 

    ![2](image/3.PNG)
    
    ![3](image/4.PNG)

3.  Berikut ini tampilan setelah kita mencoba membuat post blog di HTMLy


    ![4](image/6.PNG)
    
    ![5](image/7.PNG)
    

4. Pada tampilan HTMLy di bagian atas terdapat berbagai menu yang dapat kita gunakan. Pada menu Post kita bisa melihat daftar post yang pernah kita buat dan kita juga bisa menambah post.

	![6](image/5.PNG)

5. Menu **Add Content** berisi kategori post, kita bisa membuat post sesuai dengan kebutuhan yang kita inginkan. **Regular post** untuk memposting tulisan biasa. **Image post** untuk memposting tulisan yang bisa disisipi gambar. **Video post** untuk memposting tulisan yang bisa disisipi video. **Audio post** untuk memposting tulisan yang bisa disisipi audio. **Link Post** untuk memposting tulisan yang bisa disisipi dengan *featured link*. **Quote post** untuk memposting tulisan yang bisa disisipi dengan *featured Quote*. **Static page** untuk membuat halaman statis.

	![7](image/8.PNG)

	Berikut tampilan Image post
    - ![6](image/9.PNG)
   
    - ![7](image/10.PNG)
    
    Berikut tampilan Video post
    - ![8](image/11.PNG)
    
    - ![9](image/12.PNG)
    Berikut tampilan Audio post
    - ![5](image/13.PNG)
    - ![5](image/14.PNG)
    Berikut tampilan Link post
    - ![5](image/15.PNG)
    - ![5](image/16.PNG)
    Berikut tampilan Quote post
	- ![5](image/17.PNG)
    - ![5](image/18.PNG)


6. Menu **Categories**, kita bisa menambah kategori untuk postingan kita dengan tujuan tulisan bisa di kelompokan sesuai dengan kategori yang diinginkan. 
	- ![5](image/20.PNG)
    - ![5](image/23.PNG)
    - ![5](image/24.PNG)
    

7. Menu **Edit Profile** digunakan untuk mengedit profile. Pada halaman ini tidak ada foto profile user  melainkan hanya ada edit judul blog dan penjelasan tentang blog.

  	- ![5](image/25.PNG)
    - ![5](image/26.PNG)
    - ![5](image/27.PNG)
    

8. Menu **Config** digunakan untuk mengatur tampilan Blog.
	- ![5](image/31.png)
   

9. Menu **Logout** untuk keluar dari akun blog kita. Berikut ini tampilan setelah keluar dari blog.
	- ![5](image/30.PNG)

  


# Pembahasan
[`^ kembali ke atas ^`](#)

HTMLy adalah Databaseless Blogging Platform yang open source dan mengutamakan kesederhanaan dan kecepatan yang ditulis dalam PHP. 
- Kelebihan HTMLy adalah
1. HTMLy menggunakan algoritme unik untuk menemukan atau mencantumkan konten berdasarkan tanggal, jenis, kategori, tag, atau pengarang, dan kinerjanya akan tetap berjalan dengan cepat meskipun HTMLy memiliki ribuan pos dan ratusan tag.
2. Sebagai flat-file blog atau flat-file CMS, HTMLy didesain untuk berjalan lancar meski menggunakan spesifikasi server minimal. Dengan RAM 512MB atau bahkan kurang, seharusnya bisa menangani lebih dari 10000 postingan tanpa masalah apapun.

- Kekurangan HTMLy
1. Tidak ada autosave p
2. ada saat menulis post baru.
3. Tidak memiliki opsi save as a draft.
4. Tidak dapat upload gambar dari editor.

Jika dibandingkan dengan CMS sejenisnya seperti Magento, CMS ini memiliki beberapa 		keunggulan dan kelemahan. Berikut adalah beberapa perbandingan antara kedua CMS ini :

HTMLy   | Magento   
----   | --------  
Resource HTMLy kecil, sehingga HTMLy cepat digunakan   | Resource yang cukup besar, sehingga mengakibatkan magento cenderung lebih berat dan lama untuk melakukan loading     
Semua fitur dalam HTMLy free    | Beberapa fitur dan juga plugin yang berbayar, dan hanya sedikit yang sifatnya gratis
Proses Installasi mudah | Proses installasi lebih rumit dibandingkan HTMLy
Tampilan kurang menarik | Sangat kaya akan fitur yang menarik


# Referensi
[`^ kembali ke atas ^`](#)

1. [About HTMLy](https://www.htmly.com/) - HTMLy
2. [Kelebihan dan kekurangan Magento](https://dosenit.com/kuliah-it/web/kelebihan-dan-kekurangan-magento) - dosenit.com
3. [HTMLy Documentation](https://github.com/danpros/htmly) - HTMLy docs
