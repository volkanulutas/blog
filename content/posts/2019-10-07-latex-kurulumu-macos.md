---
author:
  name: "Volkan Ulutaş"
date: 2019-10-07
linktitle: Latex Kurulumu MacOS (Visual Code, MikTex)
type:
- post
- posts
title: Latex Kurulumu MacOS (Visual Code, MikTex)
weight: 10
tags : 
- "latex"
- "visual code"
- miktex
- macos
categories:
- İpuçları
series:
- Kurulumlar
aliases:
- /blog/Latex-Kurulumu-MacOS-(Visual-Code,-MikTex)
draft: false
---
Merhabalar, bir önceki yazımda Latex kurulumunu Windows üzerinde yapmıştık, ilgili içeriğe buradan erişebilirsiniz. Şimdi kurulumu Mac kullanıcıları için yapacağız.

## 1. Gereksinimler
İlk olarak, aşağıdaki yazılımları indirip, kurulumlarını yapmalısınız.

1.  [Visual Studio Code](https://code.visualstudio.com/download)
2.  [MikTex](https://miktex.org/download)  

## 2. MikTex Kurulumu
1. İndirilmiş olan kurulum dosyasını çift tıklayınız. Daha sonra aşağıdaki gibi izin vermeniz gerekebilir.

![metin](/images/latex-kurulumu-mac/1.png)

3. Aşağıda görülen Mac yükleme ekranındaki gibi MikTex sembolünü "Applications" sembolünün üzerine sürükleyiniz. 

![metin](/images/latex-kurulumu-mac/2.png)

4. Kurulum tamamlanınca aşağıdaki gibi bir ekran (MikTex Console) belirecektir. Burada aşağıda belirtilen iki seçenekten size uygun olanı seçiniz.
-	Burada "Finish Private Setup" seçeceğini seçebilirsiniz. (Bu seçenek sadece ilgili hesap için kurulumu sağlayacaktır. )
-	"Restart as administrator and finish setup" seçeceğini seçerseniz bilgisayarınız "restart" olup tüm hesaplar için bu kurulum aktif olacaktır. 


5. Ekran görüntüsünde belirtildiği aşağıda işlemleri sırasıyla yaptıktan sonra "Update Now" seçeceğini seçiniz.
> Start > MikTex Console > Updates > Check for updates menüsünde geliniz.
![metin](/images/latex-kurulumu-mac/3.png)

![metin](/images/latex-kurulumu-mac/4.png)


## 3. Visual Code Kurulumu ve Latex Ayarı

Eklentiler bölümünden "Latex" veya "Latex Workshop" olarak aratarak ilgili eklentiyi indiriniz.

> Open Extension > search for Latex > Install LaTeX Workshop

![metin](/images/latex-kurulumu/latexWin_3.png)

## 4. Latex Yazma 

".tex" uzantılı bir dosya yaratarak bunu Visual Code ile açıp, değişiklik yapıp derleyebilirsiniz.

![metin](/images/latex-kurulumu/latexWin_4.png)


Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.
