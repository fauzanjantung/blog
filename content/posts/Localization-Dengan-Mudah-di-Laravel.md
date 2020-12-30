---
title: Localization Dengan Mudah di Laravel
description: Apa itu Localization?
date: '2020-05-07T11:34:18.882Z'
categories: []
keywords: []
---

### Apa itu Localization?

Menurut Wikipedia, **Localization** adalah proses mengadaptasi situs web yang ada dengan bahasa dan budaya lokal di pasar sasaran. Ini adalah proses mengadaptasi situs web ke dalam konteks bahasa dan budaya yang berbeda — yang melibatkan lebih dari sekadar terjemahan teks yang sederhana.

### Kenapa Localization Itu Penting?

Dilansir dari [https://medium.com/@Shakti\_Enterprise](https://medium.com/@Shakti_Enterprise), Ada beberapa alasan kenapa Localization itu penting, diataranya :

*   Jangkauan Global:

Internet tidak terbatas pada area atau wilayah tertentu. Menurut laporan oleh International Telecommunication Union PBB, ada lebih dari 3 miliar pengguna dan lebih dari 85% pengguna berbicara lebih dari 10 bahasa. 55% dari konten online dalam bahasa Inggris. Jadi untuk memberikan kemudahan bahasa maksimum bagi pembaca, layanan terjemahan konten digunakan untuk menerjemahkan konten situs. Ini adalah salah satu cara untuk mencapai pasar global.

*   Lebih Banyak Orang Tetap Memilih Bahasa Asli:

Meskipun orang berbicara bahasa kedua atau ketiga, banyak orang menggunakan bahasa ibu untuk berbicara. Menurut laporan Common Sense Advisory, 72% konsumen menghabiskan waktu mereka di situs web dengan bahasa asli. Dengan demikian, adaptasi budaya situs web menjadi penting.

*   Peningkatan Peringkat SEO Global:

Search Engine membantu situs web untuk mencapai peringkat teratas jika memenuhi persyaratan pengunjung dan mengikuti pedoman. Melakukan proses SEO multibahasa dengan benar, yang biasanya dilakukan oleh layanan terjemahan konten profesional, akan membantu situs mencapai peringkat teratas.

Di tutorial ini kita akan belajar bersama bagaimana membuat pengaturan Localization di Laravel. Kita akan membuat halaman features, yang mana bahasanya bisa berubah-ubah, dan akan menggunakan Bahasa Indonesia dan Bahasa Inggris.

Step 1 : Mempersiapkan kata/kalimat di dalam folder resources/lang.  
Saat pertama kali menginstall Laravel, di folder resources/lang akan terdapat folder default yaitu bahasa Inggris (en). Karena kita ingin membuat 2 (dua) bahasa yaitu Inggris dan Indonesia, maka di folder tersebut kita tambahkan folder lagi yaitu “id” (Kode untuk negara Indonesia).

Nah di dalam folder masing-masing bahasa itu lah mari kita buat sebuah file php yang isinya adalah array yang memiliki key dan value.

**resources/lang/en/features.php**

```
<?php  
return \[  
    'label' => 'Greeting',  
    'title' => 'Hello from Radya Labs!',  
    'description' => 'Hello again from Radya Labs!',  
\];
```

**resources/lang/id/features.php**

```
<?php  
return \[  
    'label' => 'Salam',  
    'title' => 'Halo dari Radya Labs!',  
    'description' => 'Halo lagi dari Radya Labs!',  
\];
```

Step 2 : Install package mcamara/laravel-localization.  
Fitur-fitur dari package ini adalah :

*   Detek bahasa dari browser
*   Smart redirects (Menyimpan locale di session/cookie)
*   Smart routing (Kita hanya mengatur routes sekali saja, tidak peduli mau seberapa banyak bahasa yang dipakai)
*   Translatable Routes
*   Supports caching & testing
*   Opsi untuk menyembunyikan default locale di url

Cara Install :   
Install package dengan composer :

composer require mcamara/laravel-localization

Setelah itu, untuk mengedit konfigurasi default kita harus execute

php artisan vendor:publish --provider="Mcamara\\LaravelLocalization\\LaravelLocalizationServiceProvider"

Maka file **config/laravellocalization.php** akan terbuat.

**Step 3 : Konfigurasi sesuai kebutuhan.**  
Di file itu, ada banyak bahasa yang disupport tetapi dalam posisi ter-comment. Untuk menggunakan bahasa-bahasa tersebut, kita tinggal un-comment bahasa yang diinginkan.

![](/img/1__CYnpyQb1UrnR0z6Ws1H22A.png)


Ada juga konfigurasi untuk :

*   **useAcceptLanguageHeader** Jika di set true, maka akan otomatis mendeteksi bahasa dari browser.
*   **hideDefaultLocaleInURL** Jika true, maka tidak akan menampilkan bahasa default di url.
*   **localesOrder** Untuk urutan bahasa.
*   **localesMapping** Untuk mengubah bahasa di url.
*   **utf8suffix** Mengizinkan untuk mengubah utf8suffix untuk CentOS dll
*   **urlsIgnored** Untuk mengabaikan url.

Step 4 : Daftarkan middleware.  
**Kita harus mendaftarkan middleware di **app/Http/Kernel.php** seperti berikut ini :

```
<?php namespace App\\Http;

use Illuminate\\Foundation\\Http\\Kernel as HttpKernel;

class Kernel extends HttpKernel {  
    /\*\*  
    \* The application's route middleware.  
    \*  
    \* @var array  
    \*/  
    protected $routeMiddleware = \[  
        /\*\*\*\* Middleware lain \*\*\*\*/  
        'localize'                => \\Mcamara\\LaravelLocalization\\Middleware\\LaravelLocalizationRoutes::class,  
        'localizationRedirect'    => \\Mcamara\\LaravelLocalization\\Middleware\\LaravelLocalizationRedirectFilter::class,  
        'localeSessionRedirect'   => \\Mcamara\\LaravelLocalization\\Middleware\\LocaleSessionRedirect::class,  
        'localeCookieRedirect'    => \\Mcamara\\LaravelLocalization\\Middleware\\LocaleCookieRedirect::class,  
        'localeViewPath'          => \\Mcamara\\LaravelLocalization\\Middleware\\LaravelLocalizationViewPath::class  
    \];  
}
```

Step 5 : Mengatur Routes.  
**Ubahlah **routes/web.php** menjadi seperti ini :

```
Route::group(\['prefix' => LaravelLocalization::setLocale(),  
	'middleware' => \[ 'localeSessionRedirect', 'localizationRedirect', 'localeViewPath'\], function()  
{  
	/\*\* Tambahkan semua routes yang harus dilokalisasi disini \*\*/  
	  
        //Features  
        Route::get('/features','FeaturesController@index')->name('frontend.features');

});
```

/\*\* Routes yang tidak perlu dilokalisasi disimpan dibawah ini \*\*/

Setelah route group ini ditambahkan ke file routes/web.php, kita dapat mengakses semua bahasa di url. Misalnya :

// Web berbahasa Inggris  
http://iniurl/en  
http://iniurl/en/features

// Web berbahasa Indonesia  
http://iniurl/id  
http://iniurl/id/features

// Jika bahasa tidak ditemukan, maka akan di set ke default  
http://iniurl  
http://iniurl/features

Step 6 : Memanggil pengaturan bahasa di view  
**Contoh pemanggilan pengaturan bahasa di view adalah seperti ini, dengan cara menggunakan @lang(‘namaFile.key’)**.**

```
<section class="section mb-8">  
  <div class="container">  
    <div class="row gap-y align-items-center">

      <div class="col-md-6 text-center text-md-right">  
        <p class="small-2 text-uppercase text-lightest fw-500 ls-1">@lang('features.label')</p>  
        <h3 class="fw-500">@lang('features.title')</h3>  
        <br>  
        <p>@lang('features.description')</p>  
      </div>

      <div class="col-md-6">  
        <img class="rounded-md ml-md-4" src="{{ asset('img/thumb/17.jpg') }}" alt="...">  
      </div>

    </div>  
  </div>  
</section>
```

Web Multi Bahasa pun sudah berhasil dibuat. Bagaimana? Mudah bukan?

![](/img/1__PRxCCn__GKh1M__2nvu__5Wvg.png)
![](/img/1__4Ueubhv8hmoBBHEeFT1wwQ.png)


Oke, begitulah tutorial kali ini. Kita sudah berhasil melakukan Localization di Laravel. Sekian dan terima kasih.