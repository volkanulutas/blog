---
author:
  name: "Volkan Ulutaş"
date: 2021-12-05
linktitle: Mikroservis Mimarisinde Karşılaşılan Performans Sorunları ve Çözümleri
type:
- post
- posts
title: Mikroservis Mimarisinde Karşılaşılan Performans Sorunları ve Çözümleri
weight: 10
tags:
- Spring, Mikroservis, Performans, Mikroservis Performans
categories: 
  - Mikroservis
series:
  - Mikroservis Performans
draft: false
---

<img src="/images/performance/1.jpeg" height="600" width="800">

Merhabalar, bu yazı serimizde mikroservis mimarisinde yaygın olarak karşılaşılan 9 performans sorununu ve çözümlerini inceleyeceğiz. Bu ilk yazımızda kısaca sorunları kısaca açıklayıp daha sonra detaylı olarak inceleyeceğiz. Bu çözümlemelerimizi yaparken genellikle Java/Spring teknolojilerini kullanacağız. Şimdi bu 9 problemi listeyelim:

- N+1 Problemi
- Asenkron İsteklerin Kullanımı
- Antipattern Kullanımı
- Aşırı Etkin Mikroservisleri Kısıtlama
- 3.Taraf İsteklerin Yönetimi
- Uygulama Ceiling'den Kaçınma
- Uygun Veri Tabanı Seçimi
- Veritabanı İsteklerinin Cache'lenmesi
- Veritabanı Bağlantı Pool'ları 

> “The survey found that 33% of Java development professionals consider combined application performance to be the biggest challenge in microservices 
> development. An additional 29% of respondents reported troubleshooting microservice-to-microservice performance as their 
> biggest challenge.”
> [Perforce Survey](https://www.perforce.com/)

Perforce tarafından yayınlanan anket, Java geliştirme uzmanlarının %33'ünün uygulama performansının, mikroservis geliştirmedeki en büyük zorluk olduğunu düşündüğünü ortaya koydu. Katılımcıların ek %29'u en büyük zorluk olarak mikroservislerin performans sorunlarını gidermeyi bildirdi.

Anketinde göstermiş olduğu gibi performans sorunları projelerin belki de en son safhasında göz önüne alındığı için bu sorunlar ortaya çıkabiliyor. Yaygın sorunları projelerin başında ortaya koyup ve yazılımı geliştiren tüm ekiplerde farkındalık yaratılırsa bu sorunlar ortaya çıkmadan çözümlenmiş olur. Performans sorunları oluşturmanın önüne geçen bu farkındalıklar sayesinde yüksek maliyetlerden kaçınmış oluruz çünkü bu sorunları çözmek için projenin son safhalarında büyük mimari ve yapı değişikliklerine gitmemiz gerekebilir.

Şimdi bu problemlere göz atalım: 

## N+1 Problemi

Yazılım tasarımındaki en büyük performans sorunlarından olarak görülen N+1 problemi, veritabanından veri çekerken ortaya çıkar. Nesne yönelimli yaklaşım ile veri tabanlarının ilişkisel dünyası arasındaki paradigma farkından dolayı oluşur. Nesneleri tablolara dönüştürmek ORM (Object Relational Mapping) araçlarını kullanırız. Java/Spring dünyasında ise sıklıkla kullanılan araç Hibernate'dir. Hibernate çok performanslı şekilde çalışmasına rağmen bilindik problemlere sahiptir. Örneğin, nesnelerimiz için bir _List_ veya _Set_ kullanımı yaptığımızda bunu ORM dünyasında ilişki olarak gösteririz. Bu ilikiler _@OneToMany_, _@ManyToMany_ gibi ilişki türlerine karşılık gelir. N+1 problemi de burada karşımıza çıkar, içerisinde liste bulunan bir nesneyi veritanından çekmek istediğimizde 1 istek ile çekebilirken, bu içeride bulunan _List_ türündeki veriyi çekmek için _N_ adet küçük istek yapmamız gerekir ki performans açısından istenmeyen bir durumdur. Yazılım geliştiricinin tek satırda yaptığını düşündüğü bu istek Hibernate tarafından nesnenin boyu kadar yani _N_ yeni istekle karşılanır. Bu sorunun çözümünü, bu serimizin ilerleyen yazılarında ele alacağız. 

## Asenkron İsteklerin Kullanımı

Senkron (eş zamanlı) ve Asenkron (eş zamansız) çağrıların ne zaman kullanılacağının belirlenmesi, uygulama performansı üzerinde büyük bir etkiye sahiptir. Zorunlu kalmadıkça senkron isteklerden kaçınmak gerekmektedir; çünkü bu istekler cevap gelene kadar bekletildiğinden uygulamada dar boğaza neden olabilir. İsteklerin türünün seçimi uygulama domain (uygulamanın alanına) bilgisine göre çok değişkenlik gösterebilse de bu seçimleri örnekleyerek detaylandıracağız.

## Antipattern Kullanımı

Performans anti-kalıpları genellikle yük veya ölçekte birleşen verimsiz sorgular etrafında toplanır. Bu performans anti-kalıpları kullanmak, düşük performansa ve hatta başarısızlığa neden olabilir. Örneğin, N+1 problemi bir anti-kalıp örneğidir. Bu kalıpları kullanmak düşük performansa neden olabileceği gibi bir çok hataya da neden olabilir. Zaman aşımı (time-out) ve yeniden deneme işlemlerinde de anti-pattern kullanımına örnektir. Daha önce belirttiğimiz gibi time-out çözümü sorunu çözmek yerine daha kötü bir hale getirmekteydi. 

## Aşırı Etkin Mikroservisleri Kısıtlama

Bir mikroservisiniz yoğun istekler (yük) aldığı durumda bu isteklerin kısıtlanması veya sabit bağlantı limitlerinin kullanılması, uygulamanın ve diğer servislerin düzgün çalışmasına ve göreceli olarak sistem kaynaklarını adil bir şekilde kullanmasını sağlar. Bu kısıtlamalar uygulamanın genel kullanılabilirliğini sağlarken, aşırı etkin mikroservisin ise yavaşlamasına sebep verir; ancak tüm uygulamanın başarısız olmasını önlemiş oluruz.

## 3.Taraf İsteklerin Yönetimi
Uygulamanız en zayıf veya en yavaş servisiniz kadar hızlıdır diye bir cümle kursam yanlış olmaz. Bu yüzden yapmış olduğunuz 3. taraf isteklerinin hızı veya hatası da uygulamamızın hızına ve performansına etki eder. Eğer kullanılan dış API yavaşsa bizim sistemimizinde yavaşlamasına sebebiyet verir ve bu sorunların ele alınması gerekir. 

## Uygulama Ceiling'den Kaçınma

Düzgün yapılandırılmış ve optimize edilmiş servisler bile performans ceiling'ine sahip olabilir. Bu sorun, otomatik ölçeklendirmeye (auto-scaling) bakılarak çözülebilir ve gerektiğinde konteyner ekleyip çıkararak gelen istek yüküne dinamik olarak uyum sağlayabilir.

##  Uygun Veri Tabanı Seçimi
Mikroservis mimarisi, herbir servis için farklı veritabanı seçme esnekliğini sunar; ancak mikservisler için yanlış veritabanı teknolojisini seçmek büyük performans sorunlarına neden olabilir. Örneğin, milyon seviyseinde kullanıcısı olan bir fotoğraf ve video paylaşım sistemini düşleyin bunun için ilişkisel veritabanı kullanmak veriye ulaşma ve gösterim maliyetlerini (streaming) çok arttıracaktır ve sistemin düzgün çalışmasını engelleyecektir.
Bu yüzden yazılım geliştiricilerin ilgili mikroservis için uygun veritabanını seçmesi çok önemlidir. 

## Veritabanı İsteklerinin Cache'lenmesi
Bir mikroservisin birden çok veritabanına ait bir veri alanını talep ettiğinde, veya tek bir veritabanında uzun süren bir sorgu çağrıldığında performans düşüşleri oluşabilir. Bunun önüne geçmek için ilgili veriya çok sık ulaşıldığı bir durumda varsa ilgili veriyi uygun bir şekilde cache'leyerek her defasında veritabanından istemenin önüne geçilmiş olur. Bu da uygulamamızın performansını arttırır.

## Veritabanı Bağlantı Pool'ları 
Bir mikroservis bir veritabanı sorgusu yapacakken (cache'leme dışında) veritabanı baplantısı kurar ve ilgili sorgu bitince de hızlı bir şekilde bağlantıyı kapatır. Bağlantı kurmak ve bağlantıyı kapamak kısa ömürlü ve sıkça yapılan sorgular için aşırı maliyet getirir ve performansı düşürür. Bu şekilde her sorgu için bir bağlantı açmak yerine bir bağlantı havuzu (connection pool) yapılandırmak etkin bir çözüm sunar. Bağlantı havuzu, hali hazırda açık bulunan bağlantılar oluşturur ve bir mikroservis bağlantı veritabanına bağlanacakken bu havuzda boş olan bir bağlantıyı kullanır böyle bağlantı açılıp kapatılmak yerine tekrar kullanılmış olur. Bu da performansta artışa sebep olur.

Bu yazımızın sonuna geldik, detaylı olarak sorunları ve çözümleri ilerleyen yazılarımızda inceleyeceğiz. Sağlıcakla kalın.

Bu şekilde kurulumu tamamlanmış olduk. Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.