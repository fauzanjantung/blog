---
title: Tutorial Penggunaan Katalon Studio untuk project Web Api
description: Apa itu Web API?
date: '2020-05-07T11:45:32.066Z'
categories: []
keywords: []
---

### Apa itu Web API?

Kepanjangan dari API adalah Application Programming Interface, API berfungsi sebagai perantara [Software (Perangkat Lunak)](https://rifqimulyawan.com/pengertian-software.html) yang memungkinkan 2 (Dua) [_Application_ (Aplikasi)](https://rifqimulyawan.com/apa-itu-application.html) untuk saling berkomunikasi.

### Kenapa harus melakukan API Testing?

Jika API yang kita buat tidak stabil atau mengembalikan data yang salah, maka di aplikasi kita juga pasti akan menampilkan data yang salah. Jika API yang kita buat tidak berfungsi dengan baik, maka aplikasi kita juga akan tidak berfungsi dengan baik.

Kita harus melakukan API Testing saat mengembangkan sebuah aplikasi. Jika tidak, saat nanti muncul bug di aplikasi kita maka kita juga harus menginvestigasi bug tersebut di level API. Jika yang bermasalah adalah API, ada kemungkinan berubahnya struktur API, yang mana mempengaruhi kode aplikasi kita juga. Untuk menghindari hal seperti ini, lebih baik kita lebih memprioritaskan API Testing.

Di tutorial ini saya akan mendemonstrasikan penggunaan Katalon Studio untuk melakukan API Automation Testing.

### Membuat project baru dan melakukan API Automation Testing

Step 1: Membuat Project Baru  
Untuk membuat project, kita bisa ke menu File -> New -> Project, lalu masukkan nama project dan pilih type API/Web Service, serta pilih juga lokasi project akan disimpan. Kita juga bisa memilih opsi blank project atau project yang sudah terdapat sample di dalamnya.

![](/img/1__Jnj5lAwEW0apyG4CJe18lQ.png)

Step 2 : Set variable Base URL dan Token di Profile  
Agar lebih memudahkan kedepannya, sebaiknya Base URL dan Token disimpan sebagai Global Variable di profile.

![](/img/1__9dDpAOmAUbzrbOb1w4pTuw.png)

Step 3 : Buat Endpoint REST API di Object Repository  
Caranya dengan masuk ke Object Repository -> New -> Web Service Request.

![](/img/1__4i0jcaGRykNd9lToBhgnKA.png)

Saat membuat Endpoint baru, kita bisa memilih Request Type Restful atau SOAP. Klik OK, maka Endpoint akan terbuat. Katalon Studio menyimpan Endpoint ini di Object Repository, sama halnya dengan Test Object di UI Test.

Kita juga bisa mengimport Endpoint dari Swagger / WSDL. Dengan cara import di Object Repository -> Import -> From Swagger / From WSDL lalu masukkan URL nya.

![](/img/1__PZUeH8twF9EWqoevqoTCMg.png)

Maka semua Endpoint akan terimport.

![](/img/1__BwWwXdz3nIbwYaHx4fQGiw.png)

Step 4 : Input detail Endpoint  
Kita bisa menambah Authorization di HTTP Header jika API tersebut memang membutuhkan Authorization.

![](/img/1__AuhSB34hkzzxQK74908HLw.png)![](/img/1__pGTbHLXUARto__TCiKKeZVQ.png)

Setelah menginputkan header dan atau parameter lain, cobalah untuk Test Request tersebut dengan cara klik button icon play. Jika sudah muncul response, maka sekarang saatnya membuat API Test Case di Katalon Studio.

Step 5 : Membuat Test Case  
Meskipun request di Object Repository berguna untuk testing cepat, kita dapat menambahkan verifikasi request/assertions di test case untuk pengelolaan dan pelaporan yang lebih baik.

Di Test Case, kita bisa menambahkan beberapa keyword seperti send request, verify response dan lain-lain. Berikut adalah script untuk mengecek apakah response status nya 200, mengecek apakah value description nya delivered, dan mengecek value transporter dan counterName sesuai parameter.

import static com.kms.katalon.core.checkpoint.CheckpointFactory.findCheckpoint  
import static com.kms.katalon.core.testcase.TestCaseFactory.findTestCase  
import static com.kms.katalon.core.testdata.TestDataFactory.findTestData  
import static com.kms.katalon.core.testobject.ObjectRepository.findTestObject  
import static com.kms.katalon.core.testobject.ObjectRepository.findWindowsObject  
import com.kms.katalon.core.checkpoint.Checkpoint as Checkpoint  
import com.kms.katalon.core.cucumber.keyword.CucumberBuiltinKeywords as CucumberKW  
import com.kms.katalon.core.mobile.keyword.MobileBuiltInKeywords as Mobile  
import com.kms.katalon.core.model.FailureHandling as FailureHandling  
import com.kms.katalon.core.testcase.TestCase as TestCase  
import com.kms.katalon.core.testdata.TestData as TestData  
import com.kms.katalon.core.testobject.TestObject as TestObject  
import com.kms.katalon.core.webservice.keyword.WSBuiltInKeywords as WS  
import com.kms.katalon.core.webui.keyword.WebUiBuiltInKeywords as WebUI  
import com.kms.katalon.core.windows.keyword.WindowsBuiltinKeywords as Windows  
import internal.GlobalVariable as GlobalVariable

response = WS.sendRequest(findTestObject('GET Order Tracking Detail', \[('orderId') : '200XXXXXX'\]))  
WS.verifyResponseStatusCode(response, 200)  
WS.verifyElementPropertyValue(response, 'data.description', "DELIVERED")  
WS.verifyElementPropertyValue(response, 'data.transporter', "XXXXXXXX")  
WS.verifyElementPropertyValue(response, 'data.counterName', "SELESAI")

Test case dapat dieksekusi seperti test case biasa di Katalon Studio. Setiap langkah verifikasi dapat dilihat di log.

### Langkah Selanjutnya

Setelah membuat test case API Testing menggunakan langkah-langkah di atas, Kamu dapat memodifikasi test case sesuai kebutuhan project.

Katalon Studio memungkinkan kamu untuk:

*   Implementasi pendekatan Data-driven
*   Membuat Custom Keyword dan Packages.
*   Reuse script yang sudah ada.
*   Menambahkan error handling.
*   Melihat laporan testing setelah test di execute.