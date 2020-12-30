---
title: Mobile Test Automation dan Cucumber BDD di Katalon
description: >-
  Halo, selamat pagi/siang/sore/malam kawan-kawan. Semoga kalian sehat dan
  sukses selalu. Di artikel ini saya akan membuat tutorial Test…
date: '2019-09-03T22:59:12.719Z'
categories: []
keywords: []
---

Halo, selamat pagi/siang/sore/malam kawan-kawan. Semoga kalian sehat dan sukses selalu. Di artikel ini saya akan membuat tutorial Test Automation di Katalon menggunakan cucumber BDD. Kalau ada yang belum tau tentang BDD, bisa baca-baca dulu di [https://en.wikipedia.org/wiki/Behavior-driven\_development](https://en.wikipedia.org/wiki/Behavior-driven_development). Kalian sebaiknya mencoba BDD karena sungguh, ini sangat membantu sekali. Banyak raksasa-raksasa IT juga yang sudah menggunakan BDD.

Apalagi sekarang ada Cucumber, tools yang digunakan untuk mendukung BDD. Untuk memahami Cucumber, kalian harus paham dulu tentang syntax Gherkin. Kalian bisa baca semuanya disini [https://cucumber.io/docs/guides/overview/](https://cucumber.io/docs/guides/overview/).

Sekarang mari kita implementasikan Cucumber BDD di Katalon Studio. Silahkan buka Katalon Studio anda.

![](/img/0__QmTOPV__hBG86RbzL.png)

Lalu kalian bikin project baru, disini saya mencontohkan tes aplikasi android.

![](/img/0__EUYEtNkHlqq77RZM.png)

Setelah project selesai dibuat, di Test Explorer akan muncul struktur folder-folder, dan untuk menyimpan file .feature Cucumber, kalian harus menyimpannya di folder Include->features.

Sekarang mari kita coba buat Feature login dengan cara klik kanan di folder features lalu New -> New Feature File, lalu kasih nama dan biarkan “Generate sample Feature template” tetap tercentang karena untuk memudahkan kita.

![](/img/0__JO8jfnSGLZXU7FmV.png)

Maka hasilnya akan seperti ini, Katalon sudah memberikan kita template dan penjelasan dari syntax-syntax Gherkin, terima kasih banyak, Katalon.

![](/img/0__DefrGyuZVfvQFlZN.png)

Mari kita implementasikan BDD kita di katalon, saya akan memberikan contoh feature login dengan 1 skenario saja.

![](/img/0__BlziLUQ5yhvszwQy.png)

Dari contoh diatas saya menggunakan Scenario Outline karena saya menggunakan placeholder dan examples untuk “customerCode” dan “password”. Karena kalau Scenario biasa tidak akan bisa menggunakan examples dan placeholder.

Step-step diatas akan berwarna kuning karena belum didefinisikan, mari kita definisikan. Coba buat package baru di folder Include -> Scripts -> groovy, karena saya menggunakan bahasa Groovy. Lalu di default package klik kanan lalu New->Step definitions. Berikan nama untuk keyword package dan class kalian. Centang juga checkbox “Generate” untuk memudahkan.

![](/img/0__nGumrFNoBImqRsPM.png)

Lalu buka file groovy dan si Katalon sudah membuatkan template untuk kita.

![](/img/0__xFYdAy2pFqLUH__Pt.png)

Sesuaikan steps yang ada di file Groovy dengan yang ada di file Feature, dan definisikan nama function sama dengan steps agar memudahkan kita. Gunakan (.\*) untuk menandakan placeholder dari Feature File. Dan tentu saja kalau menggunakan placeholder maka kita harus menggunakan parameter contohnya “String customerCode”.

Disini saya akan mengetes keserasian file Feature dengan file Groovy, makanya didalam function saya hanya menulis printline saja.

![](/img/0__yHYQzMUqRxl2zZAa.png)

Coba kembali ke file Feature lalu klik kanan di steps yang kuning-kuning tadi, setelah itu klik “Recalculate Steps”. Maka warna kuning di steps akan menghilang, dan itu artinya si Katalon sudah otomatis menghubungkan file Feature dan file Groovy tadi, tanpa kita harus membuat gluecode nya.

![](/img/0__3iplBPmpnO0LUons.png)

Kalian coba liat configuration Cucumber dengan cara klik kanan steps lalu Run As -> Run Configuration lalu di tab New Configuration, Glue kita otomatis terisi karena kelakuan baik Katalon. Terus ada checkbox formatter, yang artinya kita bisa menulis format yang di centang di file Feature. Jadi anda juga bisa menuliskan BDD dalam bentuk JSON dan lain-lain.

![](/img/0__F44gtYXv6DsMjc__w.png)

Mari kita jalankan apakah Feature file dan Groovy file sudah serasi dengan Glue yang di atur Katalon? Silahkan klik Run.

![](/img/0__g4JEjpU7g3YZu4cO.png)

Setelah berhasil di-run, coba lihat tab console. Itu ada warning merah karena SLF4J binding saya ngga kompatibel, tapi ini sebenernya ngga terlalu ngaruh dan aman untuk diabaikan. Pihak katalon juga akan membetulkan ini di release berikutnya.

Terus juga dibawah ditandai bahwa Katalon membuatkan kita report dan disitu juga ada nama direktori tempat katalon menyimpan report tersebut.

Dan disebelah kiri ada line yang kita print dan muncul di Console, yang berarti Cucumber kita sukses.

![](/img/0__Cl2qxkH6Pq9giXHu.png)![](/img/0__MWw1l5p3x8LXj2mv.png)![](/img/0__4sU9LKEOpCqxa__IX.png)

Sekarang mari langsung tes APKnya. Coba kalian buat test case baru dan langsung record. Oh iya, sebelumnya kalian harus menginstall dulu Appium, NodeJS, dan pastikan pengaturan USB Debugging di android kalian aktif.

![](/img/0__AkaDmxWD__FJBL0mU.png)

Nanti akan muncul opsi untuk memilih device, itu terserah kalian mau menggunakan device local atau menggunakan Kobiton, dan kalian harus memilih direktori dimana file apk disimpan. Langsung saja klik start.

![](/img/0__663gOfd36aEFFHls.png)

Nanti kalau ada opsi untuk install via usb di android kalian, tap setuju. Maka nanti aplikasi tersebut akan diinstall di android kalian dan kalian akan langsung masuk ke aplikasi tersebut. Nanti tampilan katalon akan seperti dibawah.

![](/img/0__Cm7YsbsIw0__ZK__wu.jpg)

Tes lah login tersebut sesuai dengan BDD. Contohnya “Given User berada di halaman login”. Saat di halaman login, saya tap logo aplikasi tersebut karena itu hanya ada di halaman login. Jadi itu untuk membuktikan bahwa saya sedang berada di halaman login. Kalau nanti test sedang dijalankan dan Katalon tidak menemukan si logo tersebut, maka saya sedang bukan di halaman login.

Lakukan juga untuk mengisi customer code, password, centang syarat dan ketentuan, dan tap button masuk. Dan tujuan nya adalah user masuk ke halaman home. Jadi di halaman home saya tap bagian yang saya lingkari (android.widget.RelativeLayout0) dan jika nanti saat test dijalankan dan test nya gagal, maka si Katalon tidak berhasil masuk ke halaman home.

![](/img/0__prxwC__g26th9ClSF.jpg)

Jika sudah, klik ok dan simpan object-object tersebut di object repository -> folder baru. Lalu klik ok.

![](/img/0__Zn9iSIkG__jNJWp__N.jpg)

Maka test case kalian akan menjadi seperti ini.

![](/img/0__IX9gU__T3EdRzNlmu.png)

Pindahkan steps tersebut ke dalam function di file Groovy. Sesuai dengan steps BDDnya. Sehingga file Groovy kalian menjadi seperti ini.

![](/img/0__ItTxFw2s8fYyklnE.png)

Lalu buka file Feature kalian lalu klik Run->Android. Tetapi screen Android tidak akan muncul di layar laptop kalian, jadi kalian harus menggunakan software Vysor untuk menampilkan layar android kalian. Berikut adalah tampilan saya di halaman home karena sudah berhasil login.

![](/img/0__IMyxLojjZNbiwwGK.jpg)![](/img/0__JnnFGRRnNlm__LCqT.png)

Sekarang mari kita coba gagalkan test tersebut, di BDD tersebut kan ada kondisi “Given User berada di halaman home” maka kita coba saya di apk tersebut dengan kondisi sudah login, jadi saya berada di halaman home.

![](/img/0__vVkMHTbIMqOdSqiF.png)

Maka test akan gagal dan segera diberhentikan karena object logo aplikasi tersebut tidak ditemukan, yang berarti saya sedang tidak ada di halaman login.

![](/img/0__CMlPmDg0cmuzOgFT.png)

Mungkin segitu dulu untuk artikel ini, nanti akan saya bahas lebih rinci di artikel selanjutnya, sekian dan terima kasih.