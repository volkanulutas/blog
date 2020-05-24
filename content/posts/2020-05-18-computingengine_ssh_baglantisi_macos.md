---
author:
  name: "Volkan Ulutaş"
date: 2020-05-17
linktitle:  SSH ile Compute Engine'de Oluşturulan Makineye Erişim Sağlamak (MacOS)
type:
- post
- posts
title: SSH ile Compute Engine'de Oluşturulan Makineye Erişim Sağlamak (MacOS)
weight: 10
tags:
- Google Cloud Platform
- Computing Engine
- Cloud
- SSH
categories: 
  - Google Compute Engine
series:
  - Teknolojiler
draft: false
---

Merhabalar, bu yazımda sizlere [Google Cloud Platform (GCP)](https://cloud.google.com/)'un altında yer alan Compute Engine servisinde tanımlamış olduğumuz bir makineye nasıl erişim sağlayabileceğimizi göreceğiz.

1. "Private/Public Key" mimarisine göre öncelikle kendi makinemizde "public" ve "private key" oluşturacağız ve CE'deki makinemize oluşturduğumuz "public key"i ekleyeceğiz. Daha sonra kendi makinemizde yer alan "private key" ile CE'deki makinemize erişeceğiz. Bunun için terminali açalım. (Launchpad açılarak Terminal yazılabilir.) 


2.  Terminalde aşağıdaki komutu kendi kullanıcı adınıza göre değiştirerek çalıştırınız. (Yani volkanulutas yazan yere kendi kullanıcı adınızı yazınız. -C den sonra herhangi bir isim verebilirsiniz; ancak basitlik açısından aynı ismi kullandım.)

```sh
ssh-keygen -t rsa -f /Users/volkanulutas/Desktop/key -C volkanulutas 
```

Bu komutla birlikte sizden şifre oluşturmanızı isteyecektir, iki defa belirlediğiniz bir şifreyi giriniz. Terminal görüntüsü aşağıdaki gibi olacaktır ve masaüstünüzde "key" (private key) ve "key.pub" (public key) isminde iki dosya oluşacaktır. 

![metin](/images/gcp-ce-2/1.png)

3. Bu adımda CE instance'ımıza "public key"i koymak olacaktır. Bunun için [CE Konsol](https://console.cloud.google.com/compute/)'una gidelim. Ad kolonunda yer alan "instance-1" ismine tıklayıp, açılan ekranda "Düzenle"ye tıklayalım. 

![metin](/images/gcp-ce-2/2.png)

4. Daha sonra "SSH Anahtarları" bölümüne gelene kadar sayfada aşağıya ininiz.  "Sahip olduğunuz 0 SSH anahtarı var" metninin altında "ÖĞE EKLE" alanına tıklayınız. Bu alana oluşturduğumuz "public key"imizi metin olarak yapıştıracağız.

![metin](/images/gcp-ce-2/3.png)

5. Bu adımda masaüstünüzde oluşturduğunuz key.pub dosyasının bir editor ile açınız. (TextEdit, SublimeText ile açabilirsiniz.) Buradaki metni kopyalayıp, 4. adımda belirtilen alana yapıştırınız. Daha sonra sayfanın en altında bulunan "Kaydet" butonuna basınız. 

![metin](/images/gcp-ce-2/4.png)

![metin](/images/gcp-ce-2/5.png)

![metin](/images/gcp-ce-2/6.png)

6. Son adım olarak, aşağıdaki komutu terminale yapıştırınız. Burada "public key"i masaüstüne oluşturduğumuz için bu dizini verdik, düzenleme yapmanız gerekmektedir. "volkanulutas@104.197.171.167" alanı için ise 2.adımda kullandığımız en son parametreyi belirtiyor. Adresi ise CE'de instance'ımızın "Harici IP" alanına denk gelmektedir.

```sh
ssh -i /Users/volkanulutas/Desktop/key volkanulutas@104.197.171.167 
```

![metin](/images/gcp-ce-2/7.png)

![metin](/images/gcp-ce-2/8.png)

Bu şekilde GCP CE üzerinde yer alan makinemize erişim sağlamış olduk, kendi uygulamalarımızı bu şekilde gerekli kurulumları yaparak test edebiliriz veya sunabiliriz. 

Bu şekilde kurulumumu tamamlanmış olduk. Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.





