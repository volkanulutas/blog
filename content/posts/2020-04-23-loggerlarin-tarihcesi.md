---
author:
  name: "Volkan Ulutaş"
date: 2020-04-23
linktitle: Logger'ların Tarihçesi
type:
- post
- posts
title: Logger'ların Tarihçesi
weight: 10
tags:
- Log4j
- Apache Commons
- java.util.logging
- Slf4j
- Logback
categories: 
  - Yazılım Tarihçeleri
series:
  - Yazılım Tarihçeleri
draft: false
---

![alt text](/images/loggerlarin-tarihesi/dolmabahce.jpg "Dolmabahçe Sarayı, İstanbul (Fotoğraf: @colorartistanbul Unsplash ve Instagram)")


Log kelimesini Türkçeye "günlük kaydı" veya "olay kaydı" olarak Türkçe'ye çevirmek mümkündür. Log bilgileri bir yazılım projesi geliştirirken, geliştiricilerin hem test hem de canlı çalışma ortamlarında büyük avantajlar sağlamaktadır. Örneğin geliştirme ortamında debug (hata ayıklayıcısı) yöntemini kullanabilen yazılımcılar, canlı (prod) veye test ortamlarında böyle bir imkana sahip olamazlar. Özellikle canlı ortamda, potansiyel hataları yakalamak için loglama ihtiyacı bulunur. Bunun yanı sıra bazen bu log bilgileri gereksinimler düzeyinde de istenilmektedir. Örneğin; "Belirli rol yetkisine sahip kullanıcının hangi servise veya alana ne zaman giriş yaptığı" gibi bilgiler yine log kütüphaneleri yardımıyla kolaylıkla elde edilebilir. Kısacası log tanımını aşağıdaki gibi yapmak uygun olacaktır:

> "Belirli bir sistemle ilgili olayların otomatik olarak ve zaman damgalı belgelendirilmesidir."

Java’da, çok uzun bir süre önce, loglamanın bir yolu yoktu. İlkel yöntemlerle loglama yapılıyordu:

- System.out
- System.err
- Exception.printStackTrace()

Bu yapıların bir dezavantajı bulunmaktaydı. Bu log kayıtları sadece konsola yazılmaktaydı ve konsol kapatıldığında bu kayıtlara erişim sağlanamıyordu.  Şimdi bu işlemleri "File" yönetimiyle log'ları oraya kaydedebilirdik diye düşünebilirsiniz; ancak bu işlemlerdeki maliyet çok yüksek olabilmektedir ve hataya açıktır.

Günümüzün bilinirliği en yüksek loglama kütüphaneleri ise:
- log4j
- logback
- slf4j
- commons-logging
- java.util.logging

**Log4j**

1996 yılında E.U. SEMPER projesi kendi loglama altyapısını oluşturmaya karar verdi. 1999 yıllarında, Log4j kütüphanesi doğmaya başladı. API’nin, Java için popüler loglama paketi haline gelmesi için pek çok çalışmalar yapıldı. Sonrasında,  bir açık kaynak lisansı olan Apache Yazılım Lisansı kapsamında dağıtımına başlanmıştır.

**JUL - java.util.logging**

Log4J projelerde sıklıkla kullanılmaya başlanmıştı. O zamanlar, Java Sun şirketine aitti ve Java içinde bir loglama özelliğine ihtiyaç duyduğunu hissetti, ancak doğrudan Log4j kullanmak yerine, Log4j'den esinlenerek, 2002 yılının başlarında JDK 1.4 içerisinde java.util.logging (JUL) paketini oluşturdu; ancak kısa bir süre sonra ortak bir loglama arayüzüne ihtiyaç olduğu anlaşıldı. Bir arayüz tanımı ardından herkes istediği loglama altyapısını kullanabilecek ve tüm bu loglama altyapılarının ayarları sistem tarafından kolaylıkla tek bir merkezden yönetilebilekti, kullanılan her altyapı için ayrı ayrı ayar yapmak zorunda olunmayacaktı. Ayar yaparken bile tek bir standardın öğrenilmesi yetecekti. 

**Apache Commons (JCL) - Ortak Bir Loglama Altyapına Doğru**

Loglama tarafında birbirinden farklı kütüphaneler ortaya çıkmaya başlayınca 2002 yılı ortalarında Jakarta ekibi "commons logging" için JCL (Jakarta Commons Logging diğer bilinen adıyla [Apache Commons Logging Manuel](https://commons.apache.org/proper/commons-logging/)) projesini çıkardılar. Bu sayede eğer bir loglama altyapısı kullanacaksanız, projenize bu altyapı standartlarına uygun loglama altyapısı ekleyebilir hale geldiniz. Yani burada ortak bir standartlaşma ortaya konularak bir log altyapısının ne yapması gerektiği ve nasıl kullanılacağı standartlaştırılmış oldu, projenizde birden fazla loglama kütüphanesi kullanabilir ve bunların hepsi için ortak ve tek bir tane konfigürasyon dosyası ile yönetim sağlayabilir hale gelmiş olduk.

**Slf4j**

Loglama kütüphanelerinde evrimleşme devam ederken, JCL yeterince iyi çözümler sunamıyordu. Kullanıcılar tarafından çözdüğünden daha fazla sorun yarattığını söyleniyordu. Ceki Gülcü (Log4j’nin de mimarı olarak bilinir ve [Complete Log4j Manuel](https://www.amazon.com/Complete-Log4j-Manual-Ceki-Gulcu/dp/2970036908) kitabının da yazarıdır.) kollarını sıvadı ve 2005 yılında yeni bir SLF4J (Simple Logging Facade) projesini çıkardı. Aslında adı Log4jv2 olabilecekken basitlik vurgusuyla bu ismi seçmiş olabilirler, bilinmez; ama Ceki Gülcü’nün amacı daha iyi bir ortak loglama altyapısı ortaya çıkartmaktı. 

Slf4J'nin resmi sitesinde yer alan tanımına bakacak olursak,

>> The Simple Logging Facade for Java or (SLF4J) is intended to serve as a simple facade for various logging APIs allowing to the end-user to plug in the desired implementation at deployment time. SLF4J also allows for a gradual migration path away from Jakarta Commons Logging (JCL).

Türkçesiyle;

>> Java için SLF4J, son kullanıcının(yazılım geliştiricinin) dağıtım zamanında istenen loglama kütüphanesini projesinde kullanmasına izin veren bir altyapıda "facade" tasarım örüntüsü kullanılarak geliştirilmiştir. Ek olarak, Jakarta Commons Logging'den (JCL) aşamalı şekilde göç etmenize de izin verir.

**Logback**
Log4j, 1999 yılından beri sıklıkla kullanılan loglama altyapısı olmasına rağmen yeterince iyi değildi, yine yaratıcısı tarafından (Ceki Gülcü) yeni bir projeyle - logback ile değiştirildi. 2006 yılında logback görücüye çıktı. Logback, Log4j'ye göre daha iyi bir altyapı diyebiliriz çünkü yaratıcısı eski altyapının eksiklerini tespit edip, tecrübelerinin artışıyla birlikte de daha bir altyapı sunmuş oldu. Bu konuda Güclü'nün açıklamalarına [buradan](http://logback.qos.ch/reasonsToSwitch.html) erişebilirsiniz.

**Günümüz**
Günümüze baktığımızda birçok loglama API'sı bulunuyor burada bir kaos ortamı bulunuyor; ancak iki adet ortaklaşma kütüphanesi (commons-logging ve slf4j) sayesinde istediğiniz loglama altyapsını rahatlıkla kullanabiliyoruz diyebiliriz. Projemizi geliştirirken kullandığımız birçok farklı kütüphaneden faydalanıyoruz, hepsinin kullandığı ayrı loglama altyapıları olabiliyor. "Classpath"imizde birbirinde farklı bir sürü loglama altyapısı bulunabiliyor, maven sayesinde doğru versiyonları bulabiliyoruz. 

Peki doğru çözüm nedir? 
En kısa yoldan slf4j ve logback kullanmaktır diyebiliriz. 

**Son olarak,**
Şimdilerde loglama kütüphaneleri sayesinde, ortaklaştırılmasının (ata bir yapıdan türetilmesi) sağlanmasıyla birlikte loglar dosya sisteminde saklanabilir, e-posta ile gönderilebilir, hatta bulut tabanlı sistemler yardımıyla o log'tan (hata veya uyarıdan) sorumlu kişiye telefon araması yapma yeteneğine bile sahiptir. Veritabanlarına kaydedilmiş loglar, veri madenciliği uygulamalarıyla anlamlandırılarak sistemin zayıflıkları, hatanın çok yapıldığı yerler tespit edilerek canlı ortamda bulunan bu sorunlar çözülebilir hale geldi.

**Kaynaklar**

[[javacodegeeks, Bozhidar Bozhanov]](https://www.javacodegeeks.com/2011/09/java-logging-mess.html)

[[Şirket Sitesi, Ceki Gülcü]](http://www.qos.ch/)

[[Blog, Nicolas Fränkel]](https://blog.frankel.ch/thoughts-on-java-logging-and-slf4j/)

Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.
