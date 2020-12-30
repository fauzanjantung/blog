---
title: Mencari Akun Sosmed Menggunakan Sherlock
description: >-
  Apakah kalian tau apa itu Sherlock? Ya betul, Sherlock adalah tokoh utama dari
  cerita detektif karangan Sir Arthur Conan Doyle. Sherlock…
date: '2019-08-19T02:26:00.043Z'
categories: []
keywords: []
---

Apakah kalian tau apa itu Sherlock? Ya betul, Sherlock adalah tokoh utama dari cerita detektif karangan Sir Arthur Conan Doyle. Sherlock berasal dari Inggris, dan dia sangat jago dalam deduksi. The Science of Deduction. Dia juga bisa tau kehidupan/kepribadian seseorang hanya dengan melihat penampilannya saja.

Nah tapi, yang saya share di artikel ini bukan cerita Sherlock Holmes, namun sebuah tools untuk mencari akun sosial media. Tools ini diprogram dalam bahasa Python. Yaa, barangkali agan-agan ingin mencari akun sosial media gebetan :) bisa pakai tools ini.

Dengan bermodal secuil username atau sebongkah email, Sherlock bisa menemukannya untuk kita, karena dia jago.

### Apa aja Stepnya?

1\. Install Python3 && Python3-pip

Pertama, install python yaa, karena tools ini dibuat pake Python. Disarankan menggunakan Python 3.6 atau yang lebih baru. Juga install Python3-pip.

2\. Clone repository git sherlock

Kalian bisa langsung ngeclone repository nya dengan command ini, pastikan sudah install git yaa.

```
git clone https://github.com/sherlock-project/sherlock.git
```

3\. Masuk ke directory sherlock dan install yang ada di requirements.txt

Agan masuk dulu ke directory sherlock dengan command

```
cd sherlock
```

Lalu, install yang ada di requirements menggunakan pip, dengan command

```
pip3 install -r requirements.txt
```

![](/img/0__2__IlqDsYmfkOrBMu.jpg)

4\. Jalankan Sherlock. The Game is ON!

Kalau sudah, coba ketikkan command dibawah ini untuk mengecek apakah sherlock sudah terinstall dengan benar atau belum

```
python3 sherlock.py -h
```

Nanti akan muncul option-option yang bisa kalian pakai. Thanks, Sherlock.

Mari kita coba mencari akun sosial media seseorang, kita akan mencari akun neilbreen. Ketikkan command dibawah ini, neilbreen adalah nama usernamenya, argumen -r untuk sort media sosial dari yang paling populer, dan — print-found untuk menampilkan website yang ada username tersebut saja.

```
python3 sherlock.py neilbreen -r --print-found
```

Berikut adalah contoh hasil pencarian sherlock

![](/img/0__VMaGILw40dGxo__5n.png)

Sherlock juga menyimpan username akun-akun tersebut di directory sherlock/(username).txt

![](/img/0__tYlZTQ8jpn8Ue8vP.png)

Gimana keren ngga? Bisa dicoba nih untuk nyari akun gebetan :). Silahkan dicoba, The Game is ON!