---
title: "TryHackMe: Crack the hash!"
date: 2025-01-05T15:34:30-04:00
categories:
  - tryhackme
tags:
  - hash
  - john the ripper
  - hashcat
---

![Hash cracking](/assets/images/tryhackme-cracking-hashes/cracking-hashes.jpeg)

**[Crach the hash](https://tryhackme.com/r/room/crackthehash)** *öz* değerlerini çeşitli araçları kullanarak kıracağınız ve *öz* değerlerinin karşılık geldiği açık metin değerleri yazarak soruları yanıtlayacağınız bir odadır. *Öz fonksiyonları* ile ilgili detaylı bilgiyi paylaşmayacağım fakat ayırsanmasının önemli olduğunu düşündüğüm 3 terimden bahsetmek istiyorum odadaki görevlere başlamadan evvel. Bu terimler *öz alma*, *kodlama* ve *şifreleme*dir. [Lügat](\2025-01-04-lugat.md) sayfasından ecnebice[^1] karşılıklarına bakabilirsiniz. 

*Öz alma* işlemi *parola*ların (özellikle *şifreleme* kavramı ile *öz alma* işleminin karışmasını *parolaya* şifre denmesinden kaynaklandığını düşünüyorum) tersinir olmayan bir matematiksel fonksiyona girdi olarak verilmesiyle elde edilir.

*Kodlama* işlemi bilgisayarlara bizim için semantik anlamı olan kelime, harfler ve sembollerin anlatılması için kullanılan yöntemlere verilen isimdir (bkz. UTF-8, ASCII).

Öte yandan *şifreleme* ise veri/metinlerin gizliliğini sağlamak için kullanılan tersinir işlemin adıdır. 

Neyse. Odadaki göreve başlayalım.

### Görevler

 Odada yer alan *öz*lerin açık metin hâlini çıkarmaya çalışacağız. Burada "çıkarmak" fillini bilinçli bir seçim ile kullandım çünkü "kırmak" tabirini kullanınca sanki şifrelenmiş (bu sebepten parolaya şifre denmememeli!!!) bir metini deşifre etmekten bahsediyoruz gibi bir ima yaratıyor. Hâlbuki bizi özü alınmış değeri bulmaya çalışıyoruz, ve bu işlem zaten bir şifreleme değil. *Öz alma*nın tersinir bir işlem olmadığından bahsetmiştik, dolayısıyla burada birden çok girdinin özünü alıp karşılaştırmak suretiyle bir kaba kuvvet saldırısı gerçekleyeceğiz.

 Bunun için de çeşitli araç ve yöntemler kullanacağız.

## Bölüm 1
### Soru 1
``` 48bb6e862e54f2a795ffc4e541caed4d ```

Sorunun ipuçlarında öz alma işleminin md5 öz alma fonksiyonuyla yapıldığı belirtilmiş. Bizim de bu *öz-çözme*? işlemini gerçekleyebilmemiz için öz alma işleminin hangi fonksiyonla yapıldığını bilmemiz/bulmamız gerek zaten.

Ben bu soruda John the Ripper denilen aracı kullanacağım. Bu araç ile de hangi öz alma fonksiyonunun kullanıldığını öğrenebilirsiniz. ([Bu site](https://hashes.com/en/decrypt/hash) ya da [bu araç](https://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master) vasıtasıyla da öğrenebilirsin).

Öz alma tipini bildiğiniz bir özü çözmek için aşağıdaki komut yapısını kullanabilirsiniz.

`john --format=[format] --wordlist=[path to wordlist] [path to file]`

* **format** parametresi ile öz değerinin türü belirtilir (bu örnekte md5)
* **wordlist** parametresi ise öz-çözme işlemi için kullanılacak olasılıkların bulunduğu dosyaya ait yolu belirtir (meşhur bir örnek için bkz.rockyou.txt). kısaca bu parametre, denenecek parolaların listesidir. Yanıt aşağıdaki görselde (hash1.txt sorudaki hash değerini içeren bir metin dosyasıdır) göreceğiniz üzere: **easy**.

**NOT:** Bir öz alma fonksiyonunun farklı versioynları bulunabilir. Doğrudan standard versiyonundan bahsediyorsan format parametresinde başına *raw-* eklemen gerekir. 

![Hash1](/assets/images/tryhackme-cracking-hashes/hash1.PNG)


### Soru 2
``` CBFDAC6008F9CAB4083784CBD1874F76618D2A97 ```

Bu sefer örnekte SHA öz alma fonksiyonu kullanıldığı belirtilmiş ama hangi versiyonu olduğu belirtilmemiş. Şimdilik John'u format parametresini vermeden koşturalım. John bizim için çözemezse hangi tip SHA olduğunu bizim bulmamız gerekecek.

![Hash2](/assets/images/tryhackme-cracking-hashes/hash2.PNG)

Ve çözdü: **password123**

### Soru 3
``` 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 ```

Yine örnekte SHA öz alma fonksiyonu kullanıldığı belirtilmiş ama hangi versiyonu olduğu belirtilmemiş. Şimdilik John'u format parametresini vermeden koşturalım. 

![Hash3a](/assets/images/tryhackme-cracking-hashes/hash3-a.PNG)

Bulamadı, ama SHA256 olabileceğini gösterdi. Deneyelim:

![Hash3b](/assets/images/tryhackme-cracking-hashes/hash3-b.PNG)

Ve yanıt: **letmein**

### Soru 4

``` $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom ```

Sorunun ipuçlarında verdiği üzere [hashcat](https://hashcat.net/wiki/doku.php?id=example_hashes) örnekleri üzerinden aratacağız.

![Hash4a](/assets/images/tryhackme-cracking-hashes/hash4-a.PNG)

Böylece öz alma modunun bycrypt olduğunu ve modunun 3200 olduğunu öğrenmiş olduk. Bundan sonrasında hashcat kullanacağım. Soruda şifrenin 4 adet küçük harf içerdiği belirtilmiş, bu sebepten atak modunu 3 (maskelenmiş) olarak ayarlayıp 4 harf ile maskeleyeceğim:

`hashcat -m 3200 -a 3 hash.txt ?l?l?l?l`

Gördüğünüz üzere burada rockyou.txt gibi bir kelime listesi kullanmaya gerek yok. Hâlihazırda nasıl bir parola aradığımızı biliyoruz, yanıt: **bleh**.


### Soru 5
``` 279412f945939ba78ce0758d3fd83daa ```

Soruda bu özün md4 öz alma fonksiyonu ile oluşturulduğu söylenmiş.Burada da hashcat kullanabiliriz. Hashcat örneklerinden md4'un modunun 900 olduğunu görebilirsiniz:

`hashcat -m 900 -a 0 hash.txt /usr/share/wordlist/rockyou.txt`

-D bayrağı ile işlemci modunu da seçebilirsiniz bu arada (1:CPU, 2:GPI, 3:FPGA).

**Eternity22**

## Bölüm 2
Bu bölümde zorluk biraz daha artırılmış fakat rockyou parola listesinin buradaki soruları yanıtlamak için yeterli olacağını belirtmişler.

### Soru 1 

``` F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 ```

Bu soruda öz tipi ile bir ipucu verilmemiş bu sebepten john kullanarak hash tipini çıkarabilirsiniz (aşağıdaki görselde de görebileceğiniz üzere SHA256-opencl).

Ardından ise yapmanız gereken --format, --wordlist parametrelerini ve sordaki özü ve sağlayarak john'u koşturmak, yanıt: **paule**

![2Hash1](/assets/images/tryhackme-cracking-hashes/2hash1.PNG)



[^1]: "Müslümanlar Hrıstiyan'ın iyisine 'makûl kefere', kötüsüne 'gâvur', beterine 'şapkalı gâvur' derdi". Çankaya, Falih Rıfkı Atay. Keyifli okumalar dilerim: [Atatürk’ün İnebolu Şapka Nutku (27 Ağustos 1925)](https://isteataturk.com/g/icerik/Ataturkun-Inebolu-Sapka-Nutku-27081925/1610). 




