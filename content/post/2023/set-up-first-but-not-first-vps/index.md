---
title: "Catatan VPS: set up VPS pertama yang bukan pertama"
url: ""
description: "Catatan yang berisikan tentang instalasi, konfigurasi, dan contoh dari Git dan Github"
author: "Faiq Najib"
date: 2023-07-30T20:14:01.039+07:00
lastmod: 2023-07-23T11:58:34.039+07:00
draft: false
toc: false
comments: true
feature_image: /images/let-say-it-is-cloud.webp
# images:
  # - let-say-it-is-cloud.webp
tags:
  - catatan
  - vps
  - linux
---

Keisengan saya yang ingin tahu rasanya punya *server* atau peladen sendiri dan di jaringannya orang lain (alias *cloud*).
<!--more-->
---

*Nganu*, jadi maksudnya adalah beberapa tahun lalu saya pernah iseng *wa* coba membeli layanan [VPS](https://www.hostinger.co.id/tutorial/apa-itu-vps) dari [DigitalOcean](https://www.digitalocean.com/)[^1]. Alasannya ya... nggak ada. Namanya juga iseng, kenapa harus ada alasan hehe~

Singkat cerita, VPS dari DO atau DigitalOcean itu belum sampai sebulan dan sudah saya akhiri. Setelah beberapa purnama dan tersasar ke sana-sini[^2], akhirnya pilihan jatuh kepada [Hetzner](https://www.hetzner.com/)[^1]. Sebuah penyedia *cloud server* yang kata orang-orang cukup sulit untuk melakukan pendaftara. Nyatanya ya, memang! Hahaha.

Singkat cerita, saat itu saya belum tahu apa-apa pun penasaran mengikuti [tutorial ini](https://dev.to/styxlab/ghost-cms-on-hetzner-cloud-1dji). Bermula dari istilah [Jamstack](https://jamstack.org/) yang baru saya ketahui dengan sangat prematur membawa saya ke pertanyaan,

> Bagaimana kalau *static site* bisa direkayasa agar tetap mengonsumsi data yang dinamis?
>
> <cite>penulis yang belajar ilmu *web* secara cabutan[^3]</cite>

Tanpa *fa-fi-fu was-wes-wos*, saya langsung daftar akun dan ~~membeli~~ menyewa VPS *(yang termurah dong)* milik Hetzner. Saya pun mengikuti tutorial itu tadi dengan rajin. Satu demi satu segala halangan *rintangan membentang, tak jadi masalah dan tak kan jadi beban pikiran*&mdash;saya *googling* mencari solusinya semaksimal mungkin.

Hari-hari pun terbagi dengan urusan kerjaan, urusan hati&mdash;*ehem* perut dan urusan server Hetzner tadi. Hingga suatu waktu saya mengikuti bisikan gaib di telinga. Ya, saya *mundung*/*nggondok*/ngambek/merajuk dan tida melanjutkan rasa penasaran tadi hahaha.

VPS Hetzner itu pun akhirnya terbengkalai. Hingga sebuah *email* aneh masuk. Isinya memberitahukan bahwa alamat tagian (*invoices*) saya sudah berganti. *Ja*cok*. Saya baru tahu rasanya kena retas.

{{< figure src="hetzner-account-got-hacked.webp" width="90%" alt="info akun hetzner saya yang diretas melalui email" caption="ancaman kartu debit online hahaha" >}}

Beruntung tim *support* sangat tanggap saat saya mengirim email untuk melaporkan insiden itu. Mereka akhirnya membalas: "*As your account got hacked and you had no products (except the ones ordered by the hacker) we have cancelled your account.*"

Alhamdulillah debit *online* saya masih aman. Ternyata berbagai peringatan tentang kombinasi password yang susah ditebak[^4] memang benar adanya, dan sangat bermanfaat.

OK! Jadi intinya, tulisan saya tadi tidak ada intinya dan tidak nyambung secara langsung dengan postingan ini hehe.

## Pilih dan *set up* VPS

Tahun ini, saya balikan lagi dengan Hetzner hehe. Sebelumnya juga, saya sudah 3x mengulangi untuk mendaftar akun Hetzner baik dengan *email* yang sama, pun *email* yang berbeda tetapi semuanya ditolak. Nah, tapi semuanya teratasi setalah komplain terkait akun lama saya *suspended* karena diretas. Dan, *fualla* akun saya kembali aktif~~

Alhasil, sebuah VPS berjenis [CAX11](https://www.hetzner.com/cloud#pricing) yang ditenagai [Ampere® Altra® processors](https://amperecomputing.com/products/processors) pun berhasil saya sewa. Harganya, yaa murah kok dibandingkan biaya wifi bulanan.

VPS pun aktif dan saya segera mengatur konfigurasinya lalu melakukan *login*.

Jika pada perangkat Windows, akses VPS dapat melalui aplikasi [PuTTY](https://www.putty.org/). *Download* dan lakukan seperti biasa, *next, next,* dan *next* sampe instalasinya selesai.

### *Login* pada VPS

Setelah ter-*install* dengan benar lakukan [langkah](https://www.hostinger.com/tutorials/getting-started-with-vps-hosting#2_Log_Into_Your_VPS_Using_Secure_Shell_SSH) berikut:

1. Buka aplikasi PuTTY.
2. Salin *IP Address* dari Cloud Console, sesuaikan mau pakai ```IPv4```[^5] atau ```IPv6```[^5]. Kemudian biarkan port tetap ```22```.
3. Tempel *IP Address* tadi ke kolom pada PuTTY dan klik tombol ```Open```. Lalu akan muncul *terminal/CMD window*.
4. [Masukkan](https://www.digitalocean.com/community/tutorials/how-to-log-into-a-vps-with-putty-windows-users) *username* dan *password* dari akun ```root``` VPS. Perhatikan bahwa *password* yang diketik tidak muncul pada terminal PuTTY.

Selain itu, bisa juga *login* melalui *terminal/CMD window* dengan [langkah](https://www.domainesia.com/panduan/cara-remote-vps/#Cara_Remote_Cloud_VPS_via_SSH_melalui_Terminal_Linux) berikut:

1. Buka terminal dan ketik ```ssh username@ip_address_nya```.
2. Tunggu sejenak dan tampilan *terminal* akan meminta untuk memasukkan *password* dari *username* yang akan mengakses VPS tersebut.

Jika menggunakan [Ubuntu](https://ubuntu.com/download), maka lakukan *update* dan *upgrade* pada *package* dari VPS dengan perintah:

```bash
sudo apt update
sudo apt upgrade
```

Jika VPS meminta konfirmasi, maka ketik ```-y``` lalu tunggu hingga selesai. Ikuti jika VPS meminta untuk melakukan *reboot*.

### *Set up firewall* VPS

Pada Ubuntu, lakukan langkah berikut:

1. Izinkan UFW agar aktif pada VPS,

   ```bash
   sudo ufw enable
   ```

2. Jika VPS mengembalikan respons bahwa *command* tidak dikenali, maka *install* dahulu,

   ```bash
   sudo apt-get install ufw
   ```

3. Jika sudah ter-*install*, maka lakukan kembali langkah pertama.
4. Cek status *firewall*,

   ```bash
   sudo ufw status
   ```

5. Tambahkan *rule* sesuai [apa yang dibutuhkan](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04).

### *Set up* aplikasi sesuai apa yang dibutuhkan

Karena pada dasarnya VPS ini akan digunakan sebagai tempat *hosting* proyek agar bisa di-*demo*-kan untuk kepentingan portfolio pribadi, maka akan di-*install* beberapa aplikasi atau *package*.

Karena tidak ada panduan pasti dan untuk berjaga-jaga, saya *install* banyak *package* dan aplikasi hahaha.

#### LEMP *stack*

*Stack* yang digunakan di dunia per-kodingan, utamanya *website*, seteau saya (tanpa data yak!) adalah LAMP dan LEMP.

[LAMP](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04#introduction) adalah kepanjangan dari Linux, Apache, MySQL, PHP. Sedangkan [LEMP](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04#introduction) adalah kepanjangan dari Linux, Nginx, MySQL, PHP.

Kebetulan,saya `~~**iseng lagi**~~ memilih *stack* LEMP ini. Oh lupa, ada alasannya *ding*. VPS ini sudah saya rencanakan sebagai subdomain website ini, yaitu [```portfolio.najib.id```](https://portfolio.najib.id) hehehe. *Anyway*, berikut langkah-langkahnya.

##### *Install* NGINX *web server*

*Update* VPS terlebih dahulu dan **bisa** ditambahkan ```-y``` untuk langsung konfirmasi *package* yang akan di-*update*.

```bash
sudo apt update -y
```

Lalu, lanjutkan *install* [NGINX](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04#step-1-installing-the-nginx-web-server).

```bash
sudo apt install nginx -y
```

Setelah instalasi NGINX selesai dan ```ufw``` sudah diizinkan dari langkah sebelumnya, selanjutnya cek aplikasi yang dapat dimasukkan ke *rule* ```ufw```.

```bash
sudo ufw app list
```

Luaran yang ditampilkan oleh VPS, **kurang lebih** seperti berikut,

```bash
Output
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```

Izinkan port ```80``` yang secara *default* sebagai port yang menerima [akses HTTP](https://dewabiz.com/port-yang-digunakan-web-server/).

```bash
sudo ufw allow 'Nginx HTTP'
```

Cek lagi status pada ```ufw```.

```bash
sudo ufw status
```

Luarannya **kurang lebih** akan seperti berikut

```bash {linenos=false,hl_lines=[7,9]}
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
Nginx HTTP                 ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```

Cek hasil konfigurasi NGINX pada peramban (*browser*) dengan memasukkan ```http://ip_address``` atau ```domain_qoeh.com```. Hasilnya adalah tulisan *Welcome to nginx!*.

##### *Install* MariaDB RDBMS

Karena masih dalam waktu yang berdekatan, maka bisa langsung *install package* MariaDB tanpa harus melakukan *update package* terlebih dahulu.

```bash
sudo apt install mariadb-server
```

Pastikan bahwa MariaDB sudah berjalan.

```bash
sudo systemctl start mariadb.service
```

Kemudian, lakukan konfigurasi pada MariaDB.

```bash
sudo mysql_secure_installation
```

Sesuaikan *prompt* dengan [apa yang dibutuhkan](https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-ubuntu-20-04#step-2-configuring-mariadb).

Selanjutnya, saya memilih opsi untuk menambahkan *user* selain *root*.

```bash
sudo mariadb
```

Setelah masuk ke *prompt* ```MariaDB&nbsp;[(none)]>```, buat *user* baru tersebut dan menyetel *privilege*-nya.

```bash
GRANT ALL ON *.* TO 'budi'@'localhost' IDENTIFIED BY 'BudiTanpoHutang619' WITH GRANT OPTION;
```

Lakukan *flush privileges* untuk memastikan konfigurasi *user* baru tersebut.

```bash
FLUSH PRIVILEGES;
```

OK! Keluar dari *prompt* MariaDB

```bash
exit
```

##### *Install* PHP

Lakukan [instalasi PHP](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04#step-3-installing-php) dengan versi sesuai apa yang dibutuhkan.

```bash
sudo apt install php8.1-fpm php-mysql
```

##### Konfigurasi NGINX agar menggunakan PHP

Pertama-tama, buat direktori *root web* dengan domain yang dinginkan, misalnya adalah [```portfolio.najib.id```](https://portfolio.najib.id) sebagai nama *folder*-nya.

```bash
sudo mkdir /var/www/portfolio.najib.id
```

Atur kepemilikan direktori dengan ```$USER```.

```bash
sudo chown -R $USER:$USER /var/www/portfolio.najib.id
```

Lalu, buat konfigurasi NGINX pada direktori ```sites_available``` melalui ```nano```.

```bash
sudo nano /etc/nginx/sites-available/portfolio.najib.id
```

Pada *file* konfigurasi domain yang baru dibuat tersebut, isi dengan konten seperti berikut.

```bash {linenos=false,hl_lines=["3-23"]}
# located at /etc/nginx/sites-available/portfolio.najib.id

server {
    listen 80;
    server_name portfolio.najib.id www.portfolio.najib.id;
    root /var/www/portfolio.najib.id;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
```

Selesai mengubah, keluar dari ```nano``` editor dengan ```CTRL + X``` lalu ```Y``` unguk konfirmasi menyimpan file yang diubah tadi, dan tekan ```ENTER```.

Buat *symbolic link* dari direktori tadi.

```bash
sudo ln -s /etc/nginx/sites-available/portfolio.najib.id /etc/nginx/sites-enabled/
```

Putuskan sambungan *symbolic link* konfigurasi *default*.

```bash
sudo unlink /etc/nginx/sites-enabled/default
```

Lalu cek konfigurasi dengan mengetesnya.

```bash
sudo nginx -t
```

Jika berhasil, akan muncul hasil seperti berikut. Jika belum berhasil, berarti ada port ```80``` dari konfigurasi lainnya yang ikut *'ditarik'* oleh NGINX.

```bash
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

*Restart* NGINX untuk menerapka perubahan konfigurasi.

```bash
sudo systemctl reload nginx
```

Buat alaman awal dari *website* saat *IP Address* atau *domain* diakses.

```bash
nano /var/www/portfolio.najib.id/index.html
```

Isi file ```index.html``` tersebut contohnya seperti ini

```html
<html>
<!-- /var/www/portfolio.najib.id/index.html -->

  <head>
    <title>portfolio.najib.id website</title>
  </head>

  <body>
    <h1>Hello World!</h1>

    <p>This is the landing page of <strong>portfolio.najib.id</strong>.</p>
  </body>

</html>
```

Cek hasilnya pada peramban (*browser*) dengan memasukkan ```http://ip_address``` atau ```domain_qoeh.com```.

#### PostgreSQL Database

*Install package* [PostgreSQL](https://www.digitalocean.com/community/tutorials/how-to-install-postgresql-on-ubuntu-22-04-quickstart) dengan perintah berikut.

```bash
sudo apt install postgresql postgresql-contrib
```

Instalasi tersbut akan membuat *user* dengan nama ```postgres``` dengan *role root* pada PostgreSQL.

Ketika ingin membuat *user* atau *role* yang baru, maka dapat digunakan perintah berikut.

```bash
sudo -u postgres createuser --interactive
```

Dan akan muncul ```prompt``` pada *terminal* yang dapat diisi sesuai kebutuhan.

```bash {linenos=false,hl_lines=[1]}
Output
Enter name of role to add: sammy
Shall the new role be a superuser? (y/n) y
```

#### MongoDB Database

Pertama-tama, masukkan kunci publik ```GPG``` melalui perintah ```curl```.

```bash
curl -fsSL https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
```

Lanjutkan dengan mendaftarkan *package* MongoDB pada ```apt```. Di sini saya hanya menggunakan opsi ```arm64``` yang mana menyesuaikan jenis *processor* yaitu ARM64.

```bash
echo "deb [ arch=arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
```

Perbarui *package* pada ```apt```.

```bash
sudo apt update
```

Baru kemudian *install* MongoDB.

```bash
sudo apt install mongodb-org
```

Jalankan *service* MongoDB.

```bash
sudo systemctl start mongod.service
```

Dan, cek *status* dari MongoDB.

```bash
sudo systemctl status mongod
```

Berikan izin pada MongoDB agar berjalan saat VPS menyala.

```bash
sudo systemctl enable mongod
```

Tes koneksi MongoDB.

```bash
mongosh --eval 'db.runCommand({ connectionStatus: 1 })'
```

Luaran yang didapatkan adalah seperti berikut. Di sini saya menggunakan ```mongosh``` karena perintah ```mongo``` tidak didekteks oleh VPS.

```bash
Current Mongosh Log ID: 64c94ce4a0986579ea215006
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+1.10.2
Using MongoDB:          6.0.8
Using Mongosh:          1.10.2

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

------
   The server generated these startup warnings when booting
   2023-07-31T08:50:33.805+00:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
   2023-07-31T08:50:34.751+00:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
   2023-07-31T08:50:34.751+00:00: vm.max_map_count is too low
------

{
  authInfo: { authenticatedUsers: [], authenticatedUserRoles: [] },
  ok: 1
}
```

## *Troubleshooting*

Untuk kebutuhan koneksi *database* secara *remote* dari perangkat pribadi, maka dapat melakukan pengaturan koneksi melalui ```bind_address=0.0.0.0``` dan menyetel *firewall*. Banyak laah tutorialnya di mbah Google hehehe.

Pada kondisi ini, saya mendapat galat bahwa koneksi *remote* database tidak bisa dilakukan meskipun konfigurasi sudah sesuai dengan apa yang ada di internet. Ternyata solusi yang harus dilakukan adalah mengatur *firewall* pada *console dashboard* Hetzner **juga**. Itu untuk Hetzner, saya tidak tahu bagaimana *provider cloud* lainnya.

Contohnya pada link[https://console.hetzner.cloud/projects/9922305/firewalls/199524/rules](https://console.hetzner.cloud/projects/9922305/firewalls/199524/rules), ini hanya sekedar link contoh.

![Contoh tampilan firewall pada dashboard akun cloud Hetzner](dashboard-firewall-hetzner.webp)

## Pelajaran yang Dapat Diambil

OK! Pembelian atau sewa layanan VPS/*cloud* cukup *tricky* karena bisa jadi *provider* cuma memberikan *gimmick* dan bukan hasil nyata yang dijanjikan. Itu adalah menurut penuturan beberapa *thread* dari forum [LowEndTalk](https://lowendtalk.com/). Temen-temen bisa cari sendiri dari forum tersbut.

Instalasi *package* pada VPS mempunyai perintah yang berbeda-beda. Karena bergantung *flavors* dari OS Linux itu sendiri. Kalau *distro* Ubuntu menggunakan ```apt```, maka mungkin akan berbeda dengan *distro* lainnya.

*Password* root VPS dapat di-*reset* dari *console dashboard* akun *provider* VPS.

Dan, Hetzner sepertinya punya *firewall* bertingkat, mulai dari *console dashboard*-nya dan *firewall* pada VPS-nya itu sendiri. Entah saya yang kurang pengetahuan atau kurang utak-atik VPS sendiri, namun itu adalah impresi saya hehe.

Alasan saya memakai NGINX adalah sekaligus sebagai *reverse proxy* karena *domain* utama saya sudah melalui [Netlify](https://netlify.com) yang meng-*serve website* statis [ini](https://najib.id). Sedangkan NGINX akan berperan untuk me-*route* ketika *subdomain* [portfolio.najib.id](https://portfolio.najib.id) diakses oleh pengguna internet. Itulah rencana saya, setidaknya menurut informasi dan pengetahuan yang saya dapatkan dari Google hehe.

Terima kasih bagi yang sudah tersasar ke *section* catatan ini dan membacanya. Semoga catatan ini bermanfaat bagi Anda.

Sekian. Salam.

[^1]: *Link* tidak mengandung kode *referral* kok.
[^2]: [Situs](https://lowendbox.com/) [forum](https://lowendtalk.com/) unik yang baru saya temui, hingga situs [pembanding](https://www.vpsbenchmarks.com/) VPS.
[^3]: Ilmu cabutan adalah... hmm... sepertinya saat *googling*, tidak ada penjelasan yang pasti. Tapi, saya pernah menemukan sebuah postingan di LinkedIn (maaf lagi, saya lupa menyimpan postingan itu) yang membahas kalau ilmu cabutan itu ilmu-ilmu yang dipelajari dengan tidak berurutan dan diambil dari beragam sumber tanpa tuntunan/panduan guru yang pasti. Kurang lebih seperti itu seingat saya hehe.
[^4]: Kombinasi password yang dianggap *Good* menurut [artikel](https://security.harvard.edu/use-strong-passwords#block-boxes-1574263848) dari Harvard University adalah kombinasi huruf besar, huruf kecil, angka dan simbol. Misalkan, ```budi@TanpoHutang619```.
[^5]: [Perbedaannya](https://www.trivusi.web.id/2022/09/mengenal-ipv4-dan-ipv6.html) [yaitu](https://pandi.id/blog/mengenal-ipv4-dan-ipv6), IPv4 adalah *IP Addrees* versi lama yang biasanya digunakan sampai sekarang bahkan saat postingan ini ditulis. Sedangkan IPv6 adalah jenis *IP Address* yang lebih baru. Perlu diperhatikan bahwa tidak semua penyedia internet/wifi di Indonesia menyediakan IPv6, jadi pilihlah VPS dengan bijak :)
