---
title: "TryHackMe: OhSINT!"
date: 2025-01-04T15:34:30-04:00
categories:
  - tryhackme
tags:
  - osint
  - exiftool
  - MAC
  - BSSID, SSID
---

![OhSINT](/assets/images/tryhackme-ohsint/ohsint.png)

**[OhSINT](https://tryhackme.com/r/room/ohsint)** *açık kaynak istihbaratı* ve becerilerini kullanarak yer alan soruları yanıtlayabileyeceğiniz bir odadır. Açık kaynak istihbaratı, genelde, herkese açık kaynaklardan toplanan bilgilerin analiz edilip kullanılmasıdır. Bu bilgi içeriği görünmeyen ya da aktifliğini yitirmiş bilgileri de kapsar: web uygulamalarının eski sürümleri, yönetim panelleri, portallar, personellerin kullanmasına yönelik sayfalar vb. 

Şimdi odadaki görevlere başlayabiliriz.


## 1. Görselin Üst Verisini İnceleme

![Windows XP](/assets/images/tryhackme-ohsint/image.jpg)

Odada bize sunulan yukarıda gördüğünüz jpg dosyasından ibaret. 

Öncelikle, [exiftool](https://exiftool.org/) kullanarak bu görsele ait *üst veri*lere erişeceğiz. Üst veri, dosyaların içine gömülü olan ve dosyaya dair yan verileri içerir.  

![ohsint1.png](/assets/images/tryhackme-ohsint/ohsint1.png)

Exiftool ile jpg dosyasının üst verilerine baktığımızda fotoğrafın telif hakkının `OWoodflint`e ait olduğunu görüyoruz. Şimdi ilk sorumuza geçelim.

### Soru 1: What is this user's avatar of?

Kullanıcı adını arama motorunuzda aratmanız sonucunda aşağıdaki Twitter (X?) hesabına ve cevaba erişebilirsiniz: **cat**
![ohsint2.png](/assets/images/tryhackme-ohsint/ohsint2.png)

### Soru 2: What city is this person in? 

Sorunun ipuçlarında `bssid + wigle.net` var.

[Bssid](https://www.atera.com/blog/computer-terms-unwrapped-what-is-bssid/) *kablosuz internet ağı* erişim noktasının *medya erişim kontrolü* (MAC) adresidir. MAC (kısaltmalardan kaçınmak ya da kullanışlı Türkçe karşılıklarını yaratmak zorlu bir görev, şimdilik [yola devam](https://www.youtube.com/watch?v=MIBaT3prsNs)). MAC, on altılık gösterimle ifade edilen, 12 karakterli, 48 bitlik bir sayıdır. Örneğin: 

`a3:c4:f2:45:ca:6f`

Bu sayı cihazların üretim aşamalarında atanan tekil bir sayıdır (ağa bağlanabilen bütün cihazların anakartlarında ağa bağlandındığı bir ağ arayüzü olmalı, işte bu tekil sayı oraya atanır).

[wigle.net](wigle.net) ise kablosuz ağ erişiminde bulunan cihazları haritalandıran bir veri tabanıdır denilebilir.

`owoodflint` kullanıcı adlı twitter, pardon x, hesabında yer alan ikinci girdide kullanıcının bssid'sini paylaştığını görebilirsiiz. ilgili bssid'yi wigle.net'te aratmanız durumunda cevaba erişeceksiniz: **London**. 

<div align="center">
<img src="/assets/images/tryhackme-ohsint/ohsint3.png" width="400" height="200">
</div>

![Wigle](/assets/images/tryhackme-ohsint/ohsint3.png){: style="width:400px; height:200px; display:block; margin:auto;"}

Ayrıca kullanıcının [github hesabını](https://github.com/OWoodfl1nt/people_finder) incelerseniz orada da Londra'da yaşadığını belirttiğini görebilirsiniz.

### Soru 3: What is the SSID of the WAP he connected to?

SSID *kablosuz internet ağı*na bağlanmanızı sağlayan cihazı tanıyabilmeniz ve seçebilmeniz içindir (alfanumerik karakterler atayıp isimlendirdiğiniz ağ ismi kısaca). Bir nevi insansal DNS servisi. Neyse, yanıt: **UnileverWiFi**

### Soru 4 ve 5: What is his personal email address? What site did you find his email address on?

İlgili kişinin [github hesabını](https://github.com/OWoodfl1nt/people_finder) incelemeniz durumunda iki sorunun da yanıtına erişeceksiniz:  OWoodflint@gmail.com ve **github**.

### Soru 6: Where has he gone on holiday?

Yine kullanıcının github hesabında paylaştığı [blog sitesine](https://oliverwoodflint.wordpress.com/) giderseniz: **New York**
![Blog sitesi](/assets/images/tryhackme-ohsint/ohsint4.png)

### Soru 7: What is the person's password?

Kaynak kodu görünüz:
![Kaynak kod](/assets/images/tryhackme-ohsint/ohsint5.png){: .center }
