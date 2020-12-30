---
title: Mendirikan Device Farm Menggunakan OpenSTF
description: >-
  Selamat pagi/siang/sore/malam teman. Semoga kalian sehat dan sukses selalu.
  Saya ucapkan selamat datang.
date: '2019-08-09T02:12:30.057Z'
categories: []
keywords: []
---

Selamat pagi/siang/sore/malam teman. Semoga kalian sehat dan sukses selalu. Saya ucapkan selamat datang. Mungkin beberapa dari kalian sudah tahu apa itu Device Farm, dan mungkin beberapa dari kalian juga belum tahu apa itu Device Farm, jadi mari kita belajar bersama-sama.

Disini saya mengacu ke tulisan di [https://tech.mercari.com](https://tech.mercari.com). Tulisan disana keren-keren. Jika ilmu ibarat ikan, maka [https://tech.mercari.com](https://tech.mercari.com) ibarat sungai. Kita bisa mendapatkan banyak ikan disana.

[**Mercari Engineering Blog**  
_We're the software engineers behind Mercari. Check out our blog to see the tech that powers our marketplace._tech.mercari.com](https://tech.mercari.com "https://tech.mercari.com")[](https://tech.mercari.com)

### Apa itu Device Farm?

Kalau menurut bahasa, Device Farm berarti sebuah tempat/peternakan/perkebunan perangkat. Sama seperti Animal Farm, tetapi isinya adalah perangkat. Jadi bisa anda bayangkan sebuah tempat, yang berfungsi untuk menyimpan dan memelihara device kita.

### Kenapa menggunakan Device Farm?

Membuat aplikasi mobile yang berkualitas tinggi itu sulit, jangan diremehkan. Apalagi di bumi ini terdapat banyak variasi jenis-jenis mobile device dan sistem operasinya. Inilah yang menjadi tantangan untuk para pengembang aplikasi mobile. Salah satu cara untuk menjamin kualitas aplikasi mobile yaitu dengan mengetes aplikasi tersebut di berbagai variasi jenis mobile device. Sebab itu kita harus mempunyai beberapa variasi mobile device. Namun, bagaimana cara kita memelihara mereka semua? Tentu pasti sulit untuk mengelola semua mobile device tersebut. Solusinya adalah kita membuat sebuah sistem yang dimana semua mobile device tersebut terhubung dan bisa kita akses secara remote. Nah, OpenSTF adalah alat satu-satunya tools yang open-source yang bisa membantu kita mendirikan sistem tersebut.

### Pengenalan OpenSTF

**STF** (atau Smartphone Test Farm) adalah sebuah aplikasi web untuk memantau, mengetes dan men-debug mobile device, smartwatch atau gadget lain secara remote, cukup diakses dari browser.

Di STF juga terdapat beberapa fitur yang keren, seperti remote control, menginstal aplikasi, screenshot, logcat, menjalankan perintah shell, dan memiliki akses penuh untuk adb. Singkatnya, apa yang bisa kita lakukan di mobile device berbentuk fisik, bisa juga dilakukan di STF menggunakan browser.

Berikut adalah sedikit contoh dari ke-kerenan openSTF. Silahkan kunjungi [https://openstf.io](https://openstf.io/) untuk info yang lebih mendetail.

*   OS support
*   Android
*   Supports versions 2.3.3 (SDK level 10) to 9.0 (SDK level 28)
*   Supports Wear 5.1 (but not 5.0 due to missing permissions)
*   Supports Fire OS, CyanogenMod, and other heavily Android based distributions
*   `root` is **not** required for any current functionality
*   Remote control any device from your browser
*   Real-time screen view
*   Refresh speed can reach 30–40 FPS depending on specs and Android version. See [minicap](https://github.com/openstf/minicap) for more information.
*   Rotation support
*   Supports typing text from your own keyboard
*   Supports meta keys
*   Copy and paste support (although it can be a bit finicky on older devices, you may need to long-press and select paste manually)
*   May sometimes not work well with non-Latin languages unfortunately.
*   Multitouch support on touch screens via [minitouch](https://github.com/openstf/minitouch), two finger pinch/rotate/zoom gesture support on regular screens by pressing `Alt` while dragging
*   Drag & drop installation and launching of `.apk` files
*   Launches main launcher activity if specified in the manifest
*   Reverse port forwarding via [minirev](https://github.com/openstf/minirev)
*   Access your local server directly from the device, even if it’s not on the same network
*   Open websites easily in any browser
*   Installed browsers are detected in real time and shown as selectable options
*   Default browser is detected automatically if selected by the user
*   Execute shell commands and see real-time output
*   Display and filter device logs
*   Use `adb connect` to connect to a remote device as if it was plugged in to your computer, regardless of [ADB](http://developer.android.com/tools/help/adb.html) mode and whether you're connected to the same network
*   Run any `adb` command locally, including shell access
*   [Android Studio](http://developer.android.com/tools/studio/index.html) and other IDE support, debug your app while watching the device screen on your browser
*   Supports [Chrome remote debug tools](https://developer.chrome.com/devtools/docs/remote-debugging)
*   File Explorer to access device file system
*   Experimental VNC support (work in progress)
*   Manage your device inventory
*   See which devices are connected, offline/unavailable (indicating a weak USB connection), unauthorized or unplugged
*   See who’s using a device
*   Search devices by phone number, IMEI, ICCID, Android version, operator, product name and/or many other attributes with easy but powerful queries
*   Show a bright red screen with identifying information on a device you need to locate physically
*   Track battery level and health
*   Rudimentary Play Store account management
*   List, remove and add new accounts (adding may not work on all devices)
*   Display hardware specs
*   Simple REST [API](https://github.com/openstf/stf/blob/master/doc/API.md)

![](/img/1__R__QAAq5Zer23Fb__Dyl__hcQ.png)
![](/img/1__ifaXDDKCG1JtF4PUJ6um9Q.png)

Berikut juga adalah beberapa penampakan yang gambarnya saya ambil dari [https://tech.mercari.com](https://tech.mercari.com).

![](/img/1__eOMtMuB__LY06kV5r2SQzBg.png)
![](/img/1__pna6p__cY__w0BcnTyKR3XmA.jpeg)

### Arsitektur

Arsitektur STF ini menggunakan microservices. Beberapa services yang independen berkomunikasi dengan satu sama lain lewat [ZeroMQ](http://zeromq.org/) dan [Protocol Buffer](https://github.com/google/protobuf). Tidak seperti web services biasanya yang hanya client side dan server side, STF mempunyai satu bagian lagi yaitu bagian device. Jadi arsitektur STF adalah sebagai berikut:

*   Device Side
*   Server Side
*   Client Side

![](/img/1__LvOckD5LUu2YT4Ry2s3CnQ.png)

### Device Side

Untuk menangkap layar dan men-trigger event touch Android, STF menggunakan [minicap](https://github.com/openstf/minicap) and [minitouch](https://github.com/openstf/minitouch) yang berjalan di dalam device dan open socket. Sekaligus mengirimkan data antara server side dengan device side melalui adb.

STF juga menggunakan [STFService.apk](https://github.com/openstf/STFService.apk) di mobile devicenya yang mana apk tersebut berjalan di background sebagai [Android Service](https://developer.android.com/guide/components/services.html). Service ini menyediakan socket API untuk memantau dan melakukan berbagai aksi di device tersebut. Server side berkomunikasi dengan STFService.apk melalui adb menggunakan Protocol Buffer.

### Server Side

Server side terdiri dari berbagai microservices berbasis [NodeJS](https://nodejs.org/en/). Service-service ini berkomunikasi satu sama lain menggunakan ZeroMQ.

### Client Side

STF client side diimplementasikan menggunakan AngularJS. Kebanyakan komunikasi antara client side dan server side dilakukan melalui websocket.

### Deployment Requirements

*   Physical machines where the devices are connected should have CoreOS or (any Linux based OS)
*   All machines should have static IP
*   Port Range (15000 ~ 25000) for all machines should be open to all users
*   Docker & Systemd are available on each machine

### Cara Install

[**thinkhy/deploy-stf-docker**  
_You can't perform that action at this time. You signed in with another tab or window. You signed out in another tab or…_github.com](https://github.com/thinkhy/deploy-stf-docker "https://github.com/thinkhy/deploy-stf-docker")[](https://github.com/thinkhy/deploy-stf-docker)

Diatas saya lampirkan link untuk menginstal STF dengan menjalankan satu script saja. Didalam script tersebut terdapat command untuk menginstal adb, menginstal docker, pull image STF,RethinkDB, dan Nginx. Jadi STF kita akan berjalan diatas Nginx web server.

Kalian tinggal mengklon saja repositori diatas lalu edit deploy\_stf.sh, ubah IP Address di dalam script menjadi IP Static kalian. Tetapi disini saya akan mencontohkan mendirikan openSTF di jaringan lokal menggunakan OS Debian Buster.

![](/img/1__zbnbIgnzRnQqp2IHpo__L2g.png)
![](/img/1__4NvGq7wj____VgQ67sJ8AGSA.png)

Setelah di save, kita tinggal ketikkan command ./deploy\_stf.sh maka openSTF akan diinstal dan akan langsung bisa digunakan. Jika terjadi kesalahan mohon cek list process status container dockernya. Pastikan semua container dalam status up, kecuali stf-migrate.

![](/img/1____x2Uh1r5s3awu9DGaVpmyQ.png)![](/img/1__vXGtHHxWo8Zwdh__1ni8UuQ.png)

### Notes

*   Jika kalian mengalami device di web kalian terus-terusan dalam mode disconnected, dimohon kalian mencoba mematikan firewall.

#### Menambahkan device Xiaomi

Kalau untuk device Xiaomi, ada beberapa langkah tambahan yang harus dilakukan. Berikut diantaranya:

1.  Mengaktifkan **Developer options**, untuk mengaktifkannya cukup pergi ke **Settings** → **About phone** dan tap bagian **MIUI version** sampai mode developer aktif.
2.  Pergi ke **Settings** → **Mi Account** dan buatlah akun MI, atau login jika sudah punya.
3.  Buka **Settings** → **Additional settings** → **Developer options**. Aktifkan **USB debugging** (untuk akses ADB), **Install via USB** (dibutuhkan untuk instal STFService.apk) dan **USB debugging (Security settings)** (untuk menjalankan minitouch). Kalian harus punya akun MI untuk mengaktifkan _USB debugging (Security settings)_.

*   Note: Ada beberapa versi MIUI yang mengharuskan device untuk memasang SIM card.

4\. Koneksikan device dengan PC. Izinkan ADB key dan pilih “Selalu izinkan.”

5\. Jalankan STF. Akan muncul dialog pop up di device untuk menginstal `STFService`. Kalian harus mengizinkan instalasti tersebut.

6\. Jika STF gagal dijalankan setelah instalasi `STFService.apk`, coba buka **Settings** → **Permissions** → **Autostart** dan aktfikan `STFService`.

7\. Sekarang harusnya device sudah aktif di STF.

Sekian dan terima kasih.