---
author:
  name: "Volkan Ulutaş"
date: 2020-05-10
linktitle: GCP - Compute Engine Makine Oluşturma
type:
- post
- posts
title:  GCP - Compute Engine Makine Oluşturma
weight: 10
tags:
- Google Cloud Platform
- Computing Engine
- Cloud
- linux
- devops
categories: 
  - Google Compute Engine
series:
  - DevOps
draft: false
---

Merhabalar, bu yazımda sizlere [Google Cloud Platform (GCP)](https://cloud.google.com/) servisinden bahsedeğim ve Compute Engine sisteminde tanımlamış olduğumuz bir makineye nasıl erişim sağlayabileceğimizi göreceğiz.

## Google Cloud Platform 
GCP, Google'ın tüm bulut tabanlı servislerini içerir. Bulut tabanlı olarak veri depolama ve sunma, veri analizi ve makine öğrenimi gibi hizmetleri sunar. Bu hizmetleri "kullandıkça öde" sistemine göre sağlamaktadır. Yani siz sunmak istediğiniz bir web uygulamasını, hizmet verdiğiniz müşterilerin kullanım oranlarına göre ücretlendirir ve fiziksel olarak sizin sunucu alıp işletme maliyetinden kurtarır. Ek olarak Google GPC ile arama, Gmail ve Youtube gibi hizmetleri içinde GPC altyapısını kullanmaktadır. GPC,  IaaS (infrastructure as a service), PaaS (platform as a service), and sunucusuz mimari (serverless computing environments) yaklaşımlarında hizmet vermektedir.

## Compute Engine
Bu yazımızda Compute Engine (CE) sistemine odaklanacağımızı belirtmiştik. Ulaşılabilirliği çok yüksek olan bir hizmettir ve CE sayesinde kendi sunucunuza erişim sağlar gibi SSH sayesinde erişim sağlayıp istediğiniz teknolojiyi kullandığınız işletim sisteminin desteği doğrultusunda kullanabilirsiniz. Örneğin, Linux tabanlı Ubuntu tercihiniz doğrultusunda SSH kullanarak sisteme bağlanıp isteğiniz teknolojilerin kurulumu ile birlikte kendi uygulamanızı sunabilirsiniz. Spring Boot tabanlı, Mongo veritabanı kullanan bir docker imajı üretip burada Kubernates ile yöneterek ulaşılabilirliği, yedekliliği yüksek sistemlerinizi test edebilir veya son ürün olarak sunabilirsiniz (deploy). Daha sonraki bir yazımızda PaaS özelliğine de değinmeyi planlıyorum, burada hazır bir geliştirme ortamı sunuluyor gibi düşünebiliriz, yani platforma özgü yazılımlar ön yüklü olarak gelmektedir, bu kurulumlarla da uğraşmamaktasınız.

Sistemde temel özellikler ücretsiz olarak sunulmaktadır. Tüm özellikleri denemeniz için ise 300 dolarlık bir kredi tanımlanmaktadır. Dezavantajlı olarak görülebilecek bir özelliği ise kredi kartınızı sisteme tanımlamanız gerekmektedir; ancak Google bu konuda şeffaf davranarak sizin ne yaparsanız ücretli bir işlem yaptığınız hakkında her adımda sizi uyarmaktadır, yani deneme amaçlı veya test amaçlı olarak kullanımlarda, kredi kartınıza herhangi bir ücret yansıtmamaktadır.

>> Compute Engine'nin En temel özelliklerinden biri yazılımcıların oluşturdukları uygulamayı test etmek veya ürün haline getirip bulutta sunmak için kullanabilecekleri bir servis olarak tanımlayabiliriz. 

## Compute Engine'de Ücretsiz Olarak Makine Oluşturma

1. [GCP](https://console.cloud.google.com/compute) adresine giderek Google hesabınızla giriş yapınız. Aşağıdaki resimde görüldüğü gibi bir ekran ile karşılaşacaksınız. 

![metin](/images/gcp-ce-1/1.png)

2. Resimde görülen "ÖRNEK OLUŞTUR" butonuna tıklayalım. Gelen ekran aşağıda gösterilmektedir. Burada sadece "Önyükleme Diski" alanını "Değiştir" butonunu kullanarak "Ubuntu" olarak değiştirelim.

![metin](/images/gcp-ce-1/2.png)

3. Daha sonra sayfanın en altında bulunan "Oluştur" butona basarak tamamlayalım. 


4. Belirli bir süre geçtikten sonra aşağıdaki resimde görüldüğü gibi "intance-1" isminde bir makinemiz oluşmuş olacaktır. Burada önemli bir bilgi "Harici IP" kısmında yer alan adrestir. Bu adresi kullanarak bu makineye SSH kullanarak erişim sağlayacağız.

![metin](/images/gcp-ce-1/3.png)



Bu şekilde makinenin kurulumunu tamamlanmış olduk. Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.





