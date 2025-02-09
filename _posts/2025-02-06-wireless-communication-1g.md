---
title: "Kablosuz İletişim Temelleri: Pre 1G"
date: 2025-02-06T12:17:51-04:00
categories:
  - blog yazıları
tags:
  - kablosuz iletişim temelleri
---

### 1g
analog fdma (frequency division multiple access - frekans bölümlü çoklu erişim) kullanılıyordu ve yalnızca ses iletimi yapılıyordu. 

analog fdma olması hasebiyle global bir standardı yok idi. amerika'daki cihaz avrupa sınırlarında çalışmaması gayet doğal idi.

en başta american mobile phone service idi ardından advanced mobile phone service denildi ki kısaltmaları gördüğünüz üzere amps şeklinde ve eş.

amps için ufak bir şema:
![amps](/assets/images/wireless-communication/amps.png){: .center }

800 mhz civarlarında.

aşağıda görüldüğü üzere uplink ve downlink için 25 mhzlik iki adet band tahsis edilmiş ve bu bandlar 20 khzlik alt kanallara bölünmüş: 

![amps-cell-bands](/assets/images/wireless-communication/amps-cell-bands.png){: .center }


ters iletişimin (mobilden baz istasyonuna) yapısını da görelim: 
*ekstra bilgi* insan kulağı, 16 Hz-20 khz arasındaki sesleri duyar. erkek sesi frekans değeri  100-8500 hz, kadın ses frekans değeri  150-10000 hz
1g'de de 3 khz civarını filtreden geçirmeyi uygun görmüşler ve bunları 30 khz'lik band genişliğine sahip alt kanallarda analog modülasyon (fm) kullanarak 800 mhz dolaylarına bindirip baz istasyonuna yollamışlar. baz istasyonunda ilgili alt kanal ilgili erişim anında ilgili aboneye tahsis olduğundan vesaire vesaire efendim:

![amps-fdma](/assets/images/wireless-communication/amps-fdma.png){: .center }

bence artık [[2g]]'lik olduk.