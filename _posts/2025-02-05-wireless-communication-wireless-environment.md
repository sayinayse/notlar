---
title: "Kablosuz İletişim Temelleri: Kablosuz Ortamın Nitelikleri"
date: 2025-02-05T17:08:30-04:00
categories:
  - blog yazıları
tags:
  - kablosuz iletişim temelleri
---

### kablosuz iletim
harika bir fikir ama fazla unsurla al-veri var.

burada kendime anlatmaya çalışacağım şey bu işin ne gibi unsurları olduğu. mesela hangi fiziksel durumlardan etkilenir? bir hücre oluşturduk mühendis olarak yozgat'a baz istasyonu dikip bir iletişim altyapısı kurmamız istendi burada neleri hesap edip planlarız? gibi soruları zihnimden geçirip yanıtlamaya gayret edeceğim.

şimdi ikinci sorudan başlayalım. diyelim ki bu baz istasyonunu dikip sinyal göndermeye başladım. antenin dizaynı, sinyalin işlenip modüle edilmesi gibi adımları geçiyorum konumuz kablosu olmayan bir iletişim unsurları olduğu için.

en temelden başlayıp sinyali gönderelim, bu sinyalin başına neler gelebilir?
1. düz bir yüzeyden yansıyabilir refract olma hâli.
2. bir objenin içinden geçip iletim sürecini sürdürebilir
3. bir yüzey üzerinde saçılabilir
4. bir yüzeyin köşesine çarpıp diffractttt (yön değiştirebilir?) olabilir. 

### matematiksel temsil (hak olan temsiliyet değil, soyut bir modelleme olan temsil)
evet baz istasyonumuzu diktik. antenimiz var. hatta işaretlerimizi kodlayabilmiş (1 ve 0'larla belirli kurallar bütününe göre temsil edebilir) hâldeyiz. artık bu kodlanmış sinyali kablosuz ortamda, havada, iletmek istiyoruz. 

bu uğraşa girebilmek için matematiksel bir temsil yaratmamız şart.

oluşturduğumuz temel bant sinyallerimizi (lowpass temsil, baseband da diyebilirsiniz üstelik böylece güzide dilimizde *temel bant* deyivermenizde bir engel kalmamış olur) bir taşıyıcıya bindireceğiz (bandpass temsil) yani.

şimdi bunun matematiğinden konuşalım. 

*15 dakika sonra gelen not* bu konuşmayı kağıt ve kalemle gerçekledim. düzgüne çekmek ve buraya taşımakla uğraşmak istemediğim için iç konuşma olarak bırakıp karmaşık sayıların sağladığı temsiliyet tiktok'tan video izlemenizi sağlıyor gençler (bu ne işe yarayacak demeyin diye) diyerek geçeceğim.

sinyal iletiminde kayıp etkisinin modellenmesi ve işleyişi için: [bkz](obsidian://open?vault=work&file=%C3%B6ylesine%2Fkablosuz%20ileti%C5%9Fim%20sistemleri%2Fsinyal%20iletiminde%20kay%C4%B1p%20etkisi)
