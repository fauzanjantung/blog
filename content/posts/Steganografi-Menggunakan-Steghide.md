---
title: Steganografi Menggunakan Steghide
description: >-
  Apa itu Steganografi? Menurut mas Wikipedia, Steganografi adalah seni dan ilmu
  menulis pesan tersembunyi atau menyembunyikan pesan dengan…
date: '2019-08-12T07:48:52.831Z'
categories: []
keywords: []
---

Apa itu Steganografi? Menurut mas Wikipedia, **Steganografi** adalah seni dan ilmu menulis [pesan](https://id.wikipedia.org/wiki/Pesan) tersembunyi atau menyembunyikan pesan dengan suatu cara sehingga selain si pengirim dan si penerima, tidak ada seorangpun yang mengetahui atau menyadari bahwa ada suatu pesan rahasia. Sebaliknya, [kriptografi](https://id.wikipedia.org/wiki/Kriptografi) menyamarkan arti dari suatu pesan, tapi tidak menyembunyikan bahwa ada suatu pesan. Kata “steganografi” berasal dari [bahasa Yunani](https://id.wikipedia.org/wiki/Bahasa_Yunani) _steganos_, yang artinya “tersembunyi atau terselubung”, dan _graphein_, “menulis”.

Nah, di tulisan ini kita akan belajar cara untuk menyisipkan sebuah informasi ke dalam sebuah gambar.

Pertama-tama, install dulu tools yang bernama “Steghide”. Untuk anda pengguna Windows bisa didownload disini [http://steghide.sourceforge.net/download.php](http://steghide.sourceforge.net/download.php). Kalau di linux bisa dengan command

sudo apt-get install steghide

![](/img/0__fwzRo6l__Vec8sjS__.png)

Kedua, buat sebuah file yang ingin anda sisipkan. Contohnya saya membuat sebuah pesan dengan ekstensi txt.

![](/img/0__Ej1v7mS3o__zA__W4S.png)

Ketiga masuk dulu ke direktori gambar dan teks, lalu ketikkan command ini

steghide embed -cf 518301.jpg -ef steg.txt

518301.jpg kalian ubah dengan nama gambar kalian, dan steg.txt kalian ubah menjadi nama dari teks kalian. Command diatas adalah untuk menyisipkan pesan tersebut ke dalam gambar.

Keempat, masukkan password agar aman.

![](/img/0__nhngMQe5PXRIPvDf.png)![](/img/0__2__IlqDsYmfkOrBMu.jpg)

Nah ini tadi hasil setelah disusupi gambar, tidak ada yang aneh. Inilah yang dinamakan Steganografi.

#### Gimana kalau mau melihat pesannya?

Pertama, mari kita coba pindahkan gambar ke direktori lain, gambarnya aja ya jangan dengan file text nya. Setelah masuk direktori, ketikkan command berikut

steghide extract -sf 518301.jpg

518301.jpg bisa diubah dengan nama file gambar kalian.

Kedua, masukkan password. Setelah memasukkan password maka anda akan dapat mengakses pesan tersebut.

![](/img/0__fpPasUrVHYolfkXx.png)

Bisa dilihat sebelumnya di direktori Downloads belum ada file bernama steg.txt , setelah saya ekstrak dan memasukkan password, maka akan muncul pesan yang disisipkan pada gambar. Mari kita buka file steg.txt

![](/img/0__sRGrIjqssG5qH7mR.png)

Nah gimana keren ngga? Bisa dipake buat chat sama gebetan tanpa ada orang lain yang tau :)

Sekian dan terima kasih.