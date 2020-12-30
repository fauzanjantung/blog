---
title: Desktop Test Automation Menggunakan SeeShell
description: >-
  Hai teman-teman. Di artikel kali ini saya akan membahas suatu software untuk
  desktop automation. Software ini sebenarnya masih belum…
date: '2020-04-17T03:01:54.572Z'
categories: []
keywords: []
---

Hai teman-teman. Di artikel kali ini saya akan membahas suatu software untuk desktop automation. Software ini sebenarnya masih belum dewasa tetapi punya **potensi.**

Nama softwarenya **SeeShell**, nama ini konon terinspirasi dari indahnya **Seashells** yang artinya kerang laut, dan dari hebatnya **Shell Script**. Seeshell ini menerapkan image-driven scripting untuk automation aplikasi desktop di Windows.

Dengan Seeshell API, kita bisa mengkombinasikan SeeShell dengan bahasa pemrograman dan bahasa scripting lain semacam PowerShell, C#, Java, Visual Basic atau VBA. Semua bahasa scripting yang bisa jalan di Windows bisa diotomasikan, bahkan task Robotic Process Automation (RPA) yang paling kompleks juga bisa. Ini yang menjadikan SeeShell potensial dan pasti akan berkembang di masa mendatang.

Salah dua kelebihan SeeShell :

*   Akurasi desktop automation mencapai 100%. Ini bukan kata saya, mereka yang bilang dengan penuh kepercayaan diri. Semoga saja benar.
*   SeeShell bukan cuma bisa otomasi aplikasi desktop tapi juga bisa dengan yang ada di dalam virtual machines, seperti Linux, Mac , VMware, VBox, dan juga remote connection seperti RDP, TeamViewer, SSH Console, AWS AppStream bahkan Android simulator.

Sekarang saya akan membagikan tutorial desktop automation menggunakan SeeShell. Pergi ke link ini [https://ui.vision/download](https://ui.vision/download), dan pilih opsi SeeShell for desktop automation.

Sesudah di download, install seperti biasa. Tidak akan saya paparkan langkah-langkah cara menginstallnya karena kawan-kawan pasti sudah berapa-puluh bahkan ada yang sampai berapa-ratus kali sudah menginstall software.

Saya akan mencontohkan otomasi aplikasi visual studio code menggunakan SeeShell desktop test automation. Pertama, buka dulu aplikasi SeeShellnya.

![](/img/0__W8HDUIQ4eaPlyakR.png)

Lalu klik icon kaset yang seperti bola mata untuk memulai recording.

![](/img/0__M6t8hEd__Otu1QC__x.png)

Nanti akan muncul sebuah kotak untuk menyeleksi area dan ditengahnya ada tanda silang. Nah tanda silang itulah yang digunakan untuk memilih objek. Karena SeeShell menerapkan Image-driven scripting.

Kalian bisa mengubah ukuran dan posisi kotak tersebut menyesuaikan objek yang ingin kalian pilih. Lebih kecil kotak lebih baik. Lalu disitu ada action-action yang bisa dipilih, contohnya klik biasa dan double click. Di video tadi saya mencontohkan keduanya. Kalian juga bisa menyimpan record tersebut dan kalian replay.

![](/img/0__iPGfyS7nk30oUFCk.png)![](/img/0__ocDBvkBFYYGS6iJ4.png)

Di atas adalah step-step saya dalam membuat file tes.php yang isinya html di Visual Studio Code. Di atas ada type (^n) yang berarti ketikkan (Ctrl + n). Kalian juga bisa tap ENTER atau UP dengan menggunakan tanda {}, contoh {ENTER}. Mari kita coba run test.

RunTest.mp4 1.52 MB [View full-size](https://storage.3.basecamp.com/3096040/blobs/6d6982a0-6d89-11ea-93d7-a0369f740dfa/download/RunTest.mp4) [Download](https://storage.3.basecamp.com/3096040/blobs/6d6982a0-6d89-11ea-93d7-a0369f740dfa/download/RunTest.mp4?attachment=true)

Di atas adalah hasil run test dari SeeShell. Gimana hasilnya menurut kalian? Kalian juga bisa mengedit recordnya jika ingin ada yang ditambah maupun dikurang, dengan cara klik kanan -> edit di record yang dipilih.

Oh iya si SeeShell ini kadang rewel, jadi kalian mungkin akan mengalami SeeShell tidak bisa run test, record dll. Mungkin di build selanjutnya akan di fix. Tapi ada cara untuk mengakalinya, yaitu dengan cara end task si SeeShell nya.

Buka notepad -> lalu paste “taskkill /IM seeshell.exe /f “ dan save sebagai batch file (.bat) Sehingga menjadi seperti dibawah ini.

![](/img/0__Rx60o4JkNjqRdbrO.png)

Maka, jika kalian mengalami hal-hal aneh di SeeShell, tinggal double click file batch tersebut lalu buka lagi SeeShellnya.

Mungkin cukup sekian dulu untuk perkenalan dan gambaran SeeShellnya. Nanti di artikel selanjutnya saya akan bahas SeeShell dengan lebih mendetail.

Sekian dan terima kasih.