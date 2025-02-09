---
title: "Kablosuz İletişim Temelleri: İletim Temelleri"
date: 2025-02-17T12:17:30-04:00
categories:
  - blog yazıları
tags:
  - kablosuz iletişim temelleri
---

## iletim temelleri
### iletim karakteristikleri

3 tip iletim karakteristiğinden bahsedilebilir:
1. **path loss - yol kaybı**. bu deterministik (belirlenimci?) bir kayıptır. gönderici ve alıcı arasındaki mesafeden kaynaklanır.
2. **shadowing - gölgelenme** bu rasgeledir, log-normaldir. gönderici ile alıcı arasındaki engellerden kaynaklanır.
3. **multi path fading - çoklu yol sönümlenmesi** bu tamamen rasgeledir. sinyalin göndericiden çıktıktan sonra bir yerden yansıması, bir engelde sönümlenmesi, birden fazla farklı kuvvetlerdeki kopyalarının farklı vakitlerde alıcıya varmasından kaynaklanır.

### ortogonal frekans bölümlü çoğullama

temeli bir bit akışını birden çok sinyalin gönderimi için bölüştürmektir.
bir kanalı tek bir iletime ayırmaktansa darbantlı birden çok iletim oluşturmak. 

güzel bir analoji kurulmuş: 
![Ortogonallik](/assets/images/wireless-communication/ofdm.png){: .center }


peki buradaki sorun ne olabilir?
inter symbol interference - semboller arası girişim?
çünkü her bir alt taşıyıcıyı ayrı ayrı çözersin.

### hücresel ağ

veri trafiği kapasitesi formülü aşağıdaki gibi:

**kapasite = hücre yoğunluğu x spektrum verimliliği x ulaşılabilir spektrum**

bunu birimlerle mühendisleştirelim:
**kapasite** -> birim, bir birim... yani birim alan başına düşen trafik kapasitesi **bit sayısı/s (km^2 başına)**
**hücre yoğunluğu** -> birim alan başına düşen hücre sayısı **hücre sayısı / km^2**
**spektrum verimliliği** -> bir hücrede kullanılan spektrumda birim zamanda sahip olunabilen veri trafiği **bits / s x hertz x hücre **
**ulaşılabilir spektrum** -> [hertz](https://tr.wikipedia.org/wiki/Hertz#:~:text=Hertz%20birimi%2C%20ad%C4%B1n%C4%B1%20Heinrich%20Hertz,her%20saniye%2010%20kez%20tekrarlan%C4%B1r.) sıklık birimi malûmunuz. alman fizikçi hertz'den gelme. güzide dilimize özel isimlerin anlamsal transplantını yapamıyoruz. o yüzden hertz.

e peki bu g'lerin başındaki sayı arttıkça ne yapıyoruz?
aslında yukarıdaki soru tam olarak aşağıda vereceğim yanıtın sorusu değil. (eğer soruyu yukarıdaki gibi bırakırsam ...sonrasında - post[^1] hoc safsatasına kurban gitmiş olurum. kronolojik ya da aynı temel-nedenlere farklı yollardan bağlı olma durumları var bu soruların. ama doğrudan aynı yanıtın sorusu değiller.)
soruyu şöyle güncelleyeyim: peki biz bu trafik kapasitesini nasıl artırıyoruz?
- belirli bir coğrafi alandaki hücre sayısını artırabiliyoruz, ki bu da daha fazla baz istasyonu dikmek oraya buraya.
- spektrum kullanabilme verimliliğimizi artırabiliyoruz. ki bu da aynı hücre içine daha çok verici/anten yerleştirmek oluyor. tebrikler mimo sistemleri keşfettiniz.
- ulaşılabilir spektrumu artırıyoruz. bu da iletimi daha yüksek frekanslara taşımak demek. işte g'ler arttıkça temelde artan bu.

e tabiî bu artırımların da farklı farklı maliyetleri var. mesela kafana göre anten sayısını artırdığında çok daha fazla güç kullanman gerekebilir bir sinyali göndermen için. 

ya da frekansı daha yüksek taşıyıcı sinyaller kullanabilirsin ama bu sefer gönderdiğin sinyaller yağmurla ve su molekülleri ile falan etkileşebilir (yani bunlar tarafından dağıtılabilir veya absorbe edilebilir). gibi gibi.

[^1]: ...sonrasında - post hoc safsatası: kronolojik olarak art arda gerçekleşen iki olay arasında veri, delil ya da mantığa başvurmadan, sırf gerçekleşme sırasından kaynaklanan bir nedensellik bağı kurmaktan ileri gelir.

- #korelasyon biri bağımsız diğeri bağımlı iki değişken arasındaki ilişki.
- birbirleri ardındaki mekaznizmanın net olarak açıklanabilmesi önemli korelasyonda. yazın dondurma tüketimi artar... yazın evlilik sayısı da artar... o hâlde dondurmanın evliliğe neden olduğundan söz edebilir miyiz? elbette hayır.
- uğursuzlukla ilgili inançların birçoğu kaynağını buradan alır.
(safsatalar - tevfik uyar)