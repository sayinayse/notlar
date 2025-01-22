---
title: "Makine Öğrenmesi Modellerine Saldırı"
date: 2025-01-22T12:17:30-04:00
categories:
  - blog yazıları
tags:
  - makine öğrenmesi
  - kod enjeksiyonu
---


Bu yazıda [HiddenLayer](https://hiddenlayer.com/innovation-hub/weaponizing-machine-learning-models-with-ransomware/#Pickle-Internals)'da yer alan önemli bir makine öğrenmesi (MÖ) saldırısını olabildiğince açık şekilde açıklamak istiyorum. Bu saldırıda bir MÖ modelinine bir zaralı yazılım gizlemenin ve bu zararlı yazılımın otomatik olarak başlatılabileceği *ispat niteliğinde konsept* şeklinde gösterilmiş.

### Saldırı düzlemi

MÖ modellerini eğitmek için gerekli veri setlerini oluşturmak, bu verileri depolamak ve ardından işlemek (özellikle büyük MÖ modelleri için) maliyetli olabilir. Sıfırdan model eğitmek için gerekli olabilecek donanim maliyetleri ve uzun eğitim sürelerini azaltmak için önceden eğitilmiş MÖ modelleri kullanılır. Önceden eğitilmiş bu modeller, genel görevler için modele ait ağırlık ve parametleri oluşturup son kullanıcıya sunar. Son kullanıcılar, modele ait ağırlık ve parametreleri kendi verileriyle yeniden eğiterek, modeli kendi spesifik problemlerine uyarlayabilir. (Detaylı bilgi için: [bkz](https://spotintelligence.com/2023/10/13/pre-trained-models/))

İşte yazının başında linkini sağladığım MÖ saldırısı tam olarak burada yani önceden eğitilmiş modellerin paylaşım, dağıtım ve kullanımı işleminde gerçekleniyor. Saldırıyı göstermek niyetiyle araştırmacılar ResNet18 adında önceden eğitilmiş bir ResNet modeli kullanmışlar. Burada ResNet, görüntü tanıma için derin öğrenmeyi destekleyen bir model mimarisi sağlıyor.

Şimdi saldırının nasıl gerçekleştiğine başlamadan evvel burada kullanılan derin öğrenme modelinin bileşenleri nedir, nasıl saklanır ve paylaşılır buna bakalım.

### Nöron yapısı

Burada yapay sinir ağlarına dair bilgilendirme yapmak konuyu dallanıp budaklandıracağından **nöron**un bu yapay sinir ağının bir katmanında yer alan bir düğüm olduğunun bilindiğini varsayacağım.  

Biyolojik karşılığında da olduğu gibi, yapay nöron bir önceki katmanda yer alan nöronlardan bir girdi alırlar ve bu girdiyi belirli bir şekilde işleyerek bir çıktı üretirler (figürde görüldüğü üzere). 

![Neuron](/assets/images/ml-security/neuron.jpg)

Şimdi tek bir nöronu en evrensel lisan olan mateamatik ile tanımlayacak olursak:

$$
Y = \sum (\text{ağırlık} \times \text{girdi}) + \text{kayma değeri}
$$

Kısaca bir nöron; **ağırlıklar**dan, **kayma değerleri**nden ve bu norönün **aktivasyon fonksiyonu**ndan tekevvündür ("oluşur" değil de  "var oluşur" gibi bir şey söylemek gerek sanki, çünkü nöron bu üç unsurla var olan bir temsil aslında, neyse). 


### Nöronların saklanması

Nöronların bu saldırıda bir atak düzlemi ögesi hâline gelişi nöronların *nasıl saklandığı* konusuyla ilintili. 

Peki nasıl saklanıyor bu nöronlar? Yapay sinir ağı dediğimiz yapı içerisinde nöronları bulunduran katmanlardan ve bu katmanlar arasındaki nöronların birbirleriyle yaptığı bağlantı şekillerinden müteşekkil bir şey. Bu sebeptendir ki, bu **model**ler genelde çok boyutlu kayan-sayı dizileri hâlinde saklanır.

* Yani *(i)* bütün katmanları içeren bir dizi, *(ii)* her bir katmanda yer alan nöronları içeren dizi şeklinde düşünülebilir. Fikir vermesi için adi bir gösterimle somutlaştıracağım.


$$
\begin{bmatrix}
\text{(Katman1 için)} & \\
\begin{bmatrix}
\text{Ağırlık1} & \text{Ağırlık2} & \text{Ağırlık3} & \text{Kayma Değeri1} \\
\vdots & \\
\text{AğırlıkX} & \text{AğırlıkY} & \text{AğırlıkZ} & \text{Kayma DeğeriQ}
\end{bmatrix}
& \\
\text{(Katman2 için)} & \\
\vdots & \\
\text{(KatmanN için)} & \\
\end{bmatrix}
$$


Neyse, daha fazla dağılmadan saldırıya geri dönelim. Bu saldırıda kullanılan ResNet18 modelinde ağırlıklar ve kayma değerleri bir zip dosyası içinde *data.pkl* adlı bir dosyada saklanıyor. Bu *data.pkl* dosyası pytorch'a her bir katmanı ve her bir katmanda yer alan tensörü nasıl oluşturacağını söylemekte.

TO BE CONTINUED...

