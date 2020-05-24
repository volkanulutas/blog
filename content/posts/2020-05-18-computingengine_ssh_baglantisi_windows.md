---
author:
  name: "Volkan Ulutaş"
date: 2020-05-18
linktitle:  SSH ile Compute Engine'de Oluşturulan Makineye Erişim Sağlamak (Windows)
type:
- post
- posts
title: SSH ile Compute Engine'de Oluşturulan Makineye Erişim Sağlamak (Windows)
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

Merhabalar, [Google Cloud Platform (GCP)](https://cloud.google.com/)'un altında yer alan Compute Engine servisinde tanımlamış olduğumuz bir makineye nasıl erişim sağlayabileceğimizi göreceğiz. ( [önceki yazımızda](http://volkanulutas.com/posts/2020-05-18-computingengine_ssh_baglantisi_macos/) MacOS üzerinden erişimden bahsetmiştik.)

1. "Private/Public Key" mimarisine göre öncelikle kendi makinemizde "public" ve "private key" oluşturacağız ve CE'deki makinemize oluşturduğumuz "public key"i ekleyeceğiz. Daha sonra kendi makinemizde yer alan "private key" ile CE'deki makinemize erişeceğiz. Bunun için (PuTTYgen)[https://www.puttygen.com/] uygulamasını indirelim.


2.  PuTTYgen uygulamasını açıp, "Type of key to generate" alanında "SSH-2 RSA" seçeneğini seçelim ve "Generate" butonuna basalım ve belirli süre sonunda "private" ve "public key"ler oluşturulmuş olacaktır.

3. "Key passphrase" alanına tıklayıp bir şifre belirleyelim, daha sonra aynı şifreyi "Confirm passphrase" alanıyla doğrulayın. 

4. "Save private key" butonu ile "private key"inize bilgisayarınıza kaydetmiş olacaksınız.
5. "Public key for pasting into OpenSSH authorized_keys file" alanına sağ seçim yaparak "Select All"u seçelim. 
6. Son adım olarak sağ seçim ile oluşan metni kopyalıyalım (public key).

![metin](/images/gcp-ce-3/1.png)

7. Bu adımda CE instance'ımıza "public key"i koymak olacaktır. Bunun için [CE Konsol](https://console.cloud.google.com/compute/)'una gidelim. Ad kolonunda yer alan "instance-1" ismine tıklayıp, açılan ekranda "Düzenle"ye tıklayalım. 

![metin](/images/gcp-ce-2/2.png)

8. Daha sonra "SSH Anahtarları" bölümüne gelene kadar sayfada aşağıya ininiz.  "Sahip olduğunuz 0 SSH anahtarı var" metninin altında "ÖĞE EKLE" alanına tıklayınız. Bu alana oluşturduğumuz public key'imizi metin olarak yapıştıracağız.

![metin](/images/gcp-ce-2/3.png)

9. Bu adımda masaüstünüzde oluşturduğunuz key.pub dosyasının bir editor ile açınız. (Notepad++ ile açabilirsiniz.) Buradaki metni kopyalayıp, 8. adımda belirtilen alana yapıştırınız. Daha sonra sayfanın en altında bulunan "Kaydet" butonına basınız. 

![metin](/images/gcp-ce-2/4.png)

![metin](/images/gcp-ce-2/5.png)

![metin](/images/gcp-ce-2/6.png)

10. Son adım olarak, PuTTy uygulamasını indiriyoruz. PuTTy uygulamasını aşağıdaki resimlerdeki gibi konfigüre etmeliyiz. "volkanulutas@104.197.171.167" alanı için ise 2.adımda kullandığımız en son parametreyi belirtiyor. Adresi ise CE'de instance'ımızın "Harici IP" alanına denk gelmektedir. Son olarak "private key"i de bu bağlantıya vermeliyiz.

![metin](/images/gcp-ce-3/2.png)

![metin](/images/gcp-ce-3/3.png)

Bu şekilde GCP CE üzerinde yer alan makinemize erişim sağlamış olduk, kendi uygulamalarımızı bu şekilde gerekli kurulumları yaparak test edebiliriz veya sunabiliriz. 

**Kaynaklar**
[GCP](https://cloud.google.com/compute/docs/instances/connecting-advanced#provide-key)

Bu şekilde kurulumu tamamlanmış olduk. Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.
