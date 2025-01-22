---
title: "TryHackMe: Blue"
date: 2025-01-05T17:08:30-04:00
categories:
  - tryhackme
tags:
  - metasploit
  - buffer overflow
---

![Blue](/assets/images/tryhackme-blue/blue.gif)

Merhaba, [bu odada](https://tryhackme.com/r/room/blue) EternalBlue [MS17-010](https://learn.microsoft.com/tr-tr/security-updates/securitybulletins/2017/ms17-010) ya da CVE-2017-0144 güvnelik açığını anlayıp istismar ederek soruları yanıtlamamız bekleniyor. Bu açık *bellek taşması*

Bu oda giriş seviyesinde bir oda ve de bir video ile odadaki soruların yanıtları sağlanmış. Lakin benim niyetim bu basit odayı kullarak temel konseptleri ve kavramları yazmak, mümkünse Türkçeleştirmek ve daha ileri görevler istenen odalar için bir literatür oluşturmak.

EternalBlue Microsoft'un SMBv1 protokülnde yer alan bir güvenlk açığını hedefliyor ve WannaCry gibi meşhur fidye yazılımlarda da bu açıklıktan faydalanılmış. 

SMB protokolü, *istemci-sunucu* modeline dayanan ve ağ üzerinden dosya, cihaz ve paylaşılan klasörlere erişim için kullanılan bir protokol.

![SMB](/assets/images/tryhackme-blue/smb.webp)

Neyse, biz odadaki görevlere başlayalım, konsept ve kavramlara yeri geldikçe değinebiliriz.

### Keşfetme ve bilgi toplama


### Erişim kazanma


