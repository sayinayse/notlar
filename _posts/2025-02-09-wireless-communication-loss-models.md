---
title: "Kablosuz İletişim Temelleri: Sinyal İletiminde Kayıp Etkisi"
date: 2025-02-09T17:06:30-04:00
categories:
  - blog yazıları
tags:
  - kablosuz iletişim temelleri
---

### boş uzay - görüş hattı - free space - los modeli
sinyal/elektromanyetik dalga enerjisinin uzayda iletimi sırasında kaybettiği enerjiyi matematiksel olarak modelleyeceğiz/hesaplayacağız?

bu kayıp modelinde boş uzayda doğrudan görüş hattında/line-of-sight ilerleyen bir dalganın kaybedeceği güçtne bahsedeceğiz. bu güç kaybı nelere bağlıdır?
- sinyalin gücüne
- kullanılan sinyalin frekansına *frekansa sıklık dememe lüzum yok*
- iletim hedefine uzaklık

şimdi yukarıdaki sözel ifadelerin matematiksel karşılığını paylaşalım:

![yol-kaybi](/assets/images/wireless-communication/path-loss.png){: .center }

birimlerle uğraşmak önemli. burada desibel kullanımı lineer ölçekten logaritmik ölçeğe geçmek içindir. böylece lineer ölçekte çarpma bölme fonksiyonlarıyla eylediklerini logaritmik ölçekte toplama çıkarma ile eyleyebilir ve kayıp-kazanç analizi yapabilirsin.

tabiî gönderdiğimiz sinyalleri genelde boş uzay ortamında iletmediğimizden başka kayıp modelleri de vardır.

### genel ışın izleme - general ray tracing
bu modelde 
- yansımalar
- dağılmalar
- kırınımlar/yön değiştirim? diffracttion
hesaba katılır.

hâlâ maxwell denkleriyle uğraşmaktan daha kolay. farklı boyutlarda ışın izleme modelleri olabilir.

mesela
1. *2-bileşenli ışın izleme*'de doğrudan görüş hattından gelen sinyal ile yerden sekip gelen sinyali hesaba katarsın.
2. diyelim ki *10-bileşenli izleme* yaptık. doğrudan görüş hattından gelen, yerden seken, yerden sekip başka bir yere çarpıp oradan seken... gibi gibi bileşenler de hesaba katılır.


### gerçek hayat (seni rehin alacak, kendinden uzaklaştıracak)
ama bu modeller hâlâ bir kablosuz iletişim sistemini modellemeğe yeterli değil. bu sebeptendir ki ne boş uzay sinyal kaybı hesabı ne de ışın izleme bir başına bu hesaplarda kullanılmaz.

peki neler kullanılır?

deneysel olarak belirlenmiş katsayı ve modellerle yürütülür. 

*okumura modeli*, *hata modeli*
şehir ya da kırsal alanlarda belirli frekans aralıklarına sahip sinyallerin kayıplarını modelleyip bir cheatsheet/kopya kağıdı olarak sunulur. bu hesaplar deney tabanlı metriklerin belirlenmesi ve bunlar üzerine analitik yaklaşım/hesapların yapılmasıyla sürdürülür.

örnek olarak, iç mekanda 1200 hz sinyal duvara tosladığında 5-20 dbm güç kaybeder, pencereden geçtiğinde 3 kilo güç kaybına uğrar gibi. 

### kayıp modelleri genel değerlendirme

- *maxwell denklemleri* fazla karmaşık ve pratik değil
- *doğrudan görüş hattı kaybı modeli* fazla basit
- *ışın izleme modeli* çevreye yönelik fazla spesifik bilgiye sahip olmayı gerektiriyor: şehir, kırsal, iç, dış
- *deneysel modeller* bütün çevreleri kapsayacak şekilde genelleştirilemezler
- *basitleştirilmiş güç kaybı modelleri* yükseklerden sisteme bakarken genel bir içgörü vermek açısından iyi, derinleşme gerektirebilir

### kayıplar: kapsam alanı vs. bant genişliği al-veri
bir kere yüksek frekanslarda iletimi sağlamak için gerekli donanımsal altyapı genelde hem üretim hem de kullanım açısından daha maliyetli. ama daha fazla bilgi iletimi de yapmana olanak sağlıyor. 

1g dolaylarında kullanılan 800 mhzlik sinyali iletmek için 3.5 ghzlik sinyali iletmeye kıyasla 20 kat daha az güç harcıyorsun.

neyse biz devam edelim. detaylarına girmeden bazı kavramları sıralayacağım. ihtiyaç zühur ettiğinde bakılır.

### gölgelenme - shadowing
bu model engellerle sönümlenen ve yoluna devam eden sinyali modellemek için kullanılır. pratikte ise yine basitleştirilmiş hesabı kullanılır.

### doppler kayması
alıcının göndericeye referansla (ya da tam tersi) hareket ettiği durumlarda.

### çoklu yol sönümlenmesi - multi path fading

### gecikme yayılımı - delay spread
yansıyan yüzeeylerden alıcıya ulaşan yan sinyallerden kaynaklanır.

bu sebeple iletim (sıklığı) oranı düşük tutulmak zorunda kalınabilir.

### uyumlu bant genişliği - coherent bandwidth
tabiî sinyaller farklı yolak ve zamanlarda alıcıya ulaşabilrdiği için, alıcı tarafında sinyali işleyebilmek için sinyalin tutarlı kaldığı bir band genişliği/zaman aralığı üzerine hesaplar da yapılmalı.

bu kavramdan bahsettikten sonra [[kanal modelleri]] üzerine konuşmak/düşünmek iyi olur.
