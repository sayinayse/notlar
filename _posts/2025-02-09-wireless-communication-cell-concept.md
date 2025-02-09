---
title: "Kablosuz İletişim Temelleri: Bilgilendirme"
date: 2025-02-09T17:05:30-04:00
categories:
  - blog yazıları
tags:
  - kablosuz iletişim temelleri
---

hücre konsepti temelini belirli bir coğrafi alana dikilmiş bir adet vericinin bulunmasından alır. fikir 1971'de bell lab'tan çıkıyor.

evvelden mobil iletişim bir adet vericinin şifresiz biçimde veriyi genel yayınlaması/broadcast şeklinde gerçekleşiyordu.

ticari anlamda ilk hücre japonlar tarafından inşa ediliyor. [müziğin altın çağ on yılının](https://open.spotify.com/playlist/3vSNHCFKxn3WLjLWHsakDr?si=MktCHzSCR3iis7tuCL_0nA) sonunda, 1979'da.

buradaki fikir üst üste binme olmadan coğrafyanın bütününü kapsamak. altıgenler. 

### avantajlar
- daha düşük güç harcanması, yayın yapılacak alanın kısıtlanmasından mütevellit.
- sistem kapasitesini artırmaya olanak tanıması, komşu hücrelerde aynı frekans ile yayın yapılmasa da komşu olmayan hücrelerde aynı frekans ile yayın yapılabilir. -> frequency reusing / frekans yeniden kullanımı konsepti.

### dezavantajlar
- hücreleri oluşturmanın bir maliyeti var elbette.
- hücresel devir
- kullanıcıları takip etmeyi gerektirir, arama ya da mesajları yönlendirmek için.
- komşu hücreler arasında girişim olabilir.

### yozgat'a mobil iletişim altyapısı götürelim
evet ne yapıyorduk [[kablosuz ortamın nitelikleri]]'nden başlayarak. yozgat'ta mobil iletişim altyapısı kuruyorduk. kanala dair özelliklerden ve nelerle karşılaşabileceğimizden bahsettik ilgili kısımlarda. şimdi bir altıgen mimaride hücresel bir mobil altyapı dizayn edelim:

dizayn parametrelerimizi sıralayalım önce:
- bir hücredeki band genişliği 20 mhz olsun.
- kullanıcı başına 100 khz band genişliği tahsis edelim.
- basitleştirilmiş bir [[sinyal iletiminde kayıp etkisi#boş uzay - görüş hattı - free space - los modeli]] hesabı/analizi yaptık ve burada yol kaybı katsayısı g'yi 2 bulduk diyelim.
- yozgat'ta yaşayan vatandaşlarımıza sunduğumuz bu hizmete bir kalite taahhütünde bulunmamız şart tabiî. gsm altyapısında makûl bir sesli komünikasyon hizmeti alt sınırının sahip olabileceği sir (signal-to-interference-ratio) 9 db'dir. biz de yozgat'ımıza 10db'lik bir sir sözü vermiş olalım.
- her bir hücrenin yarıçapı da 200 metre olsun (baz istasyonu dikmek konusunda epey cömertiz çünkü yozgat'a karşı)

şimdi hesaba geri dönelim.
1. frekans yeniden kullanım oranımız ne olmalı?
2. kullanıcı kapasitemiz ne olur bu dizaynda?
3. sistem kapasitemiz ne olur peki?

elle yaptığım çözümleri obsidian notlarına aktarmak bir sonraki adım olsun.

### girişim belası
iki tip girişimle karşılaşırız böyle bir hücresel mobil iletişim altyapısında:
1. **co-channel interference - eş kanal girişimi** aynı frekansı kullanan kanallar arası
2. **adjacent channel interference - komşu kanallar girişimi** mükemmel filtrelerimiz yok, diğer frekanslardan gelen sinyalleri de geçirebiliyor alıcılarımız.
