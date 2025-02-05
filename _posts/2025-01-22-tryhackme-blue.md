---
title: "TryHackMe: Blue"
date: 2025-01-05T17:08:30-04:00
categories:
  - tryhackme
tags:
  - metasploit
  - buffer overflow
  - nmap
---

![Blue](/assets/images/tryhackme-blue/blue.gif){: .center }

Merhaba, [bu odada](https://tryhackme.com/r/room/blue) EternalBlue [MS17-010](https://learn.microsoft.com/tr-tr/security-updates/securitybulletins/2017/ms17-010) ya da CVE-2017-0144 güvnelik açığını anlayıp istismar ederek soruları yanıtlamamız bekleniyor. Bu açık *bellek taşması*

Bu oda giriş seviyesinde bir oda ve de bir video ile odadaki soruların yanıtları sağlanmış. Lakin benim niyetim bu basit odayı kullarak temel konseptleri ve kavramları yazmak, mümkünse Türkçeleştirmek ve daha ileri görevler istenen odalar için bir literatür oluşturmak.

EternalBlue Microsoft'un SMBv1 protokülnde yer alan bir güvenlk açığını hedefliyor ve WannaCry gibi meşhur fidye yazılımlarda da bu açıklıktan faydalanılmış. 

SMB protokolü, *istemci-sunucu* modeline dayanan ve ağ üzerinden dosya, cihaz ve paylaşılan klasörlere erişim için kullanılan bir protokol.

![SMB](/assets/images/tryhackme-blue/smb.webp){: style="width:400px; height:400px; display:block; margin:auto;"}

Neyse, biz odadaki görevlere başlayalım, konsept ve kavramlara yeri geldikçe değinebiliriz.

## Keşfetme ve bilgi toplama
`nmap -sV -sC --script vuln -oN blue.nmap HEDEF_IP`

Nmap (network mapper) bir ağdaki cihazları, açık portları ve çalışan servisleri tespit etmek için kullanılan bir ağ tarama aracıdır. Böylece yukarıdaki komut yordamıyla belirttiğiniz makinede güvenlik zafiyeti taraması yapabilirsiniz. 

Parametreleri kısaca açıklayacak isek:

* **-sV** açıok olan protlarda sunulan servislerin versiyonları
* **-sC** [betik](https://www.nisanyansozluk.com/kelime/betik)[^1] kodlarını çalıştırmak için
* **--script vuln** güvenlik açıklarını tespit etmek için yazılı
* **-oN blue.nmap** sonucu nmap formatında blue.nmap dosyasına kaydetmek için

Böylece hedef makinedeki açık portları ve bu portlarda çalışan servisleri tespit edebilirsiniz. Ardından bu servislerin versiyon bilgileri ile olası güvenlik zafiyetlerini tarayıp raporluyorsunuz.
![alt text](/assets/images/tryhackme-blue/nmap.png){: .center}

### Soru 1: How many ports are open with a port number under 1000?

Yukarıdaki görselde nmap komutunun çıktısını görebilirsiniz. 135, 139 ve 445 portları açık. **3**


### Soru 2: What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)
Uzaktan kod çalıştırma zafiyeti olduğunu görebilirsiniz **ms17-010** (yıl 2017, yayınlanan 10. bülten) kodlu.


## Erişim kazanma


[^1] Script zamanında betik olarak Türkçeleştirilmiş. TDK'da betik şeklinde geçiyor, tatlıya süçüg demediğimiz gibi *komut dizini dosyası?* gibi bir şeye de betik dememek daha hoş olacak sanki.