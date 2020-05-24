---
author:
  name: "Volkan Ulutaş"
date: 2019-10-07
linktitle: Latex Kurulumu Windows (Visual Code, MikTex)
type:
- post
- posts
title: Latex Kurulumu Windows (Visual Code, MikTex)
weight: 10
tags:
- latex
- visual code
- miktex
categories:
- İpuçları
series:
- Kurulumlar
draft: false
---


Merhabalar, Latex tez yazarken size büyük kolaylık sağlayacaktır. Birçok kurulum türü bulunmasına rağmen zamanınızı çok almayacak bir yöntem paylaşmak istiyorum, umarım işinize yarar. 

## 1. Gereksinimler
İlk olarak, aşağıdaki yazılımları indirip, kurulumlarını yapmalısınız.

> Windows mimarisine uygun türü seçmeyi unutmayınız (x86/x64).

1.  [StrawberryPerl](http://strawberryperl.com/)
2.  [Visual Studio Code](https://code.visualstudio.com/download)
3.  [MikTex](https://miktex.org/download)  

## 2. Miktex Kurulumu
İndirilmiş olan kurulum dosyasına çift tıkladıktan sonra, tüm varsayılan ayarları kabul ederek kurulumu tamamlayanız. 

> Start > MikTex Console > Updates > Check for updates menüsünde geliniz. Aşağıdaki resimde belirtilmiştir.

![metin](/images/latex-kurulumu/latexWin_1.png)

**latexmk** kurulumunu aratarak aşağıdaki resimdeki gibi yapınız. 
 
![metin](/images/latex-kurulumu/latexWin_2.png)

## 3. Visual Code Kurulumu ve Latex Ayarı

Eklentiler bölümünden "Latex" veya "Latex Workshop" olarak aratarak ilgili eklentiyi indiriniz.

> Open Extension > search for Latex > Install LaTeX Workshop

![metin](/images/latex-kurulumu/latexWin_3.png)

## 4. Latex Yazma 

".tex" uzantılı bir dosya yaratarak bunu Visual Code ile açıp, değişiklik yapıp derleyebilirsiniz.

![metin](/images/latex-kurulumu/latexWin_4.png)


Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.
