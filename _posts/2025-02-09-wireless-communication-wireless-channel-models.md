---
title: "Kablosuz İletişim Temelleri: Kanal Modelleri"
date: 2025-02-09T17:07:30-04:00
categories:
  - blog yazıları
tags:
  - kablosuz iletişim temelleri
---

kablosuz iletişimde kanal modelleri. ortamdan eklenen gürültüye göre, kanalın yarattığı sönümleme şekline göre değişiklik gösterebilir.

### additive white gaussian noise channel - awgn - toplamalı beyaz gauss gürültü kanalı
şimdi sönümlenme olmadan bir iletim olduğunu düşünelim -> ki bu da verici ve alıcının aynı lokasyonda olduğu anlamına gelir. 

toplamalı çünkü sinyale bir gürültü *eklenir*
beyaz gaussian gürültü çünkü sinyale bütün *frekanslara eşit etki eden* bir gürültü eklenir.

şimdi verici ve alıcı arasına bir mesafe soktuğumuz durumlara bakalım aşağıdaki alt bölümlerde.
### slow varying frequency flat fading channel - yavaş değişen düz sönümlü kanal
girişim kaybı, gölgelenme [[sinyal iletiminde kayıp etkisi#gölgelenme - shadowing]] kaybı var alıcı ve verici arasında. bu sebeple bir kayıp mevcut.

### slow varying frequency selective fading channel - yavaş değişen frekans seçimli sönümlü kanal
hem yansımanın, hem saçılmanın , hem doğrudan görüş hattından gelen sinyalin olduğu kanallar. çoklu yollardan gelen sinyal alıcıya ulaşıyor yani. alıcının yerindeki değişim yapıcı ya da yıkıcı sinyal değişimlerine sebep olabilir çünkü yansıyan da geliyor saçılan da.

bu sebeptendir ki bu kanal = 
**geniş ölçekte sönümleme/large scale fading** -> yol kaybı/path loss, gölgelenme/shadowing, girişim kayıpları kayıpları. göreceli olarak uzun mesafelerde etki eden faktörler olarak değerlendirilebilir, ismin alameti farikası...
   \+ 
**dar ölçekte sönümleme**leri hesaba katar. -> çoklu yol/multipath loss, nesneler yer değişimi gibi daha küçük ölçekli 

slow varying since the channel does not changing much over time
frequency selective since the channel varies with respect to frequency (vericiden gönderilen sinyalin frekansı değişince ortamda maruz kalacağı muamele de değişebillir)

### fast varying frequency selective fading channel - hızlı değişen frekans seçimli sönümlü kanal

bir önceki senaryoda vericinin, alıcının, ortamdaki nesnelerin birinin ya da birden fazlasının hareketli olduğu durumlarda karşılaştığımız iletim ortamına bu ismi vermişler. çünkü kanal *zamanla değişiyor.*


özet: 
![channel-models](/assets/images/wireless-communication/channel-models.png){: .center }

burada bir alt not düşmek isterim. diyelim kanalımız frekans seçimli fakat bizim sinyalimizin bant genişliği bu seçimli frekans aralığından daha dar. o zaman gönderdiğimiz sinyal için (bu kullanım senaryosunda, *nefret ediyorum bu kelime öbeğinden, beyaz yaka diliyle use case, dirac fonksiyonu şeklinde bir can sıkıntısı yaşadım şu an.*) ilgili yardımcı görsel: 
![[frekans seçimli-seçimsiz.png]]
![channel-models1](/assets/images/wireless-communication/channel-models1.png){: .center }