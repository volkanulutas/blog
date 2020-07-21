---
author:
  name: "Volkan Ulutaş"
date: 2020-07-21
linktitle: Hugo Blog'unu Github'da Yayınlamak
type:
- post
- posts
title: Hugo Blog'unu Github'da Yayınlamak
weight: 10
tags:
- Hugo
categories: 
  - Hugo
series:
  - Teknolojiler
draft: false
---

Merhabalar, bir önceki yazımızda Hugo'yu kendi bilgisayarımıza tasarlamayı incelemiştik ([Hugo İle Blog Oluşturmak](http://volkanulutas.com/posts/2020-05-18-hugo-ile-blog-olusturmak/)). Şimdi de bunu GithubPages üzerinden herhangi bir hosting'e ihtiyaç duymadan yayınlayacağız. Bunu yapmak için "new-blog" ve "username.github.io" (username alanı sizin github kullanıcı adınızdır) isminde iki depo (repository) aracılığıyla yöneteceğiz. Öncelikle bu depoları yaratmayı göreceğiz daha sonra "new-blog" deposunda Hugo kurulumunu yapacağız. Son adımda Hugo'nun ürettiği statik site yapısını "username.github.io" deposuna aktaracağız ve depoları Github'a "push" edeceğiz. 

## 1.) Gıthub'da Depo (repository) Yaratma:

İlk önce Github üzerinde iki "repository" oluşturalım. Bunu Github WEB sitesi üzerinden yapıyoruz. ("terminal" veya "konsol" üzerinden de yapılabilir.)

Githup hesabınıza gittik sonra yeni bir "repository" yaratmalıyız. Bunu arayüzden yapabileceğimiz gibi "https://github.com/new" adresinden de erişebiliriz. 

Aşağıdaki ekran görüntüsünde gösterildiği gibi, new-blog isminde bir depo yaratıyoruz:
<img src="/images/hugo-githubpages/1.png" height="600" width="800">

Aşağıdaki ekran görüntüsünde gösterildiği gibi, username.github.io isminde bir depo yaratıyoruz:
<img src="/images/hugo-githubpages/2.png" height="600" width="800">

>> Benim Github hesabımda bu depo zaten yaratıldığı için böyle bir hata vermektedir, siz de böyle bir yoksa hata almayacaksınız.


## 2.) Checkout İşlemleri 

**2.1.) GithupPages Deposunu "checkout" Etme:**

>> Checkout'u gerçekleştirdiğimiz dizine yazının devamında [BLOG_HOME] diyeceğiz.

Checkout'u gerçekleştireceğimiz dizine ([BLOG_HOME]) gidelim. 

```sh
https://github.com/username/username.github.io
```

**2.2.) Blog Deposunu "Check-out" Etme** 

[github-username].github.io "repository"sini "clone" komutu ile "check-out" edip, lokal bilgisayarımıza alalım:

```sh
https://github.com/username/new-blog
```

Bu işlemlerden sonra [BLOG_HOME] dizininde "username.github.io" ve "new-blog" isminde iki klasör oluşturmuş olduk.

## 4.) Hugo Kurulumunu Yapalım

[BLOG_HOME]/new-blog dizinine gidip daha önceki blog yazımızda incelediğimiz adımları gerçekleştirlelim. Yazıya *[buradan](http://volkanulutas.com/posts/2020-05-18-hugo-ile-blog-olusturmak/)*ulaşabilirsiniz.

Bu adımları yaptıktan sonra en önemli nokta hugo ile oluşturduğumuz içeriğin GithupPages (username.github.io) deposuna aktarılmasıdır. Bunun için aşağıdaki komutu [BLOG_HOME]/new-blog dizininde çalıştıralım:

**4.1.) Hugo Blog'unu Belli Dizinde OLuşturma:**
```sh
hugo -d ../username.github.io
```
Bu komut ile "-d" parametresiyle GithupPages (username.github.io)için "checkout" ettiğimiz dizini vermiş olduk. Bu yazımızda üst dizinde bulunduğu için "../" komutu kullanılmıştır. 

## 5.) Depoları "Push" Etme:

**5.1.) GithupPages Deposu:**

Öncelikle [BLOG_HOME] dizinine gidelim ve daha sonra aşağıdaki komutları çalıştıralım. 

```sh
cd username.github.io

git add .
git commit -m 'initial'
git push origin master
```

**5.2.) new-blog Deposu:**

```sh
git add . 
git commit -m 'initial'
git push origin master
```

Bu şekilde oluşturmuş olduğumuz blogu "https://username.github.io" adresinde yayınlamış olduk. "[BLOG_HOME]/content/posts" dizininde herhangi bir "md" uzantılı yazı oluşturduğumuzda, bu blogumuzda yer alacaktır. Daha sonra yayına almak için **4.1.)** ve **5.)** adımlarını tekrar etmeliyiz. 

Bir sonraki yazımızda GithubPages ile alanadı bağlamayı inceleyeceğiz ve bu sayede "http://volkanulutas.com" gibi bir alanadı üzerinden blogumuza erişim sağlamış olacağız.

>> Not 1: Blog yazılarınızı "md" dilinde yazabilirsiniz. Çok kolay bir "markup language" olarak sınıflandırabiliriz. Hızlıca öğrenmek için bu "tutorial" [buradan](https://www.markdowntutorial.com/) göz atabilirsiniz. Ek olarak Github'ın "tutorial"ına da [buradan](https://guides.github.com/features/mastering-markdown/) erişebilirsiniz.

>> Not 2: "Repository" kelimesi Türkçeye depo olarak çevirilmiştir. Kullanılan yabancı kelimeler için Türkçe kelime tavsiyelerini bana e-posta üzerinden iletebilirsiniz. 

**Kaynaklar**

[Github Help - Creating a Repo](https://help.github.com/en/github/getting-started-with-github/create-a-repo)

[Githup MD Guide](https://guides.github.com/features/mastering-markdown/)

[markdowntutorial](https://guides.github.com/features/mastering-markdown/)

Bu şekilde kurulumu tamamlanmış olduk. Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.

