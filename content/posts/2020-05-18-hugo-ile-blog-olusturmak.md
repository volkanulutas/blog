---
author:
  name: "Volkan Ulutaş"
date: 2020-05-18
linktitle:  Hugo İle Blog Oluşturmak
type:
- post
- posts
title:  Hugo İle Blog Oluşturmak
weight: 10
tags:
- Hugo
categories: 
  - Hugo
series:
  - Teknolojiler
draft: false
---

Merhabalar, bu yazımızda Hugo ile blog oluşturma konusuna değineceğiz, üç işletim sistemi içinde çalışan bir kurulum yazmayı hedefledim. Bir sonraki yazımızda da, lokal makinemizde oluşturduğumuz blogumuzu GithubPages üzerinden yayınlayacağız, böylelikle bir barındırma (hosting) gereksinimine de ihtiyaç duymayacağız.

## Hugo Nedir?
Hugo, Go dili ile yazılmış bir statik site oluşturucu çatı olarak tanımlanabilir. Go dili ile yazıldığı için göreceli olarak diğer sistemlere göre hızlı bir çözüm sunmaktadır. HTML ve CSS desteği ile hiç Go dili bilmeden sitenizi değiştirerek oluşturabilir veya birçok tema seçeneğinden biriyle sitenizi yayına alabilirsiniz. Git gibi bir sistem ile aşınaysanız, blog yazımını kolaştıracak ve "md" diliyle (GitHub README dosyalarında olduğu gibi) hızla yazılarınızı oluşturabileceksiniz.

## Ön Yüklemeler 
**MacOS:**

**Brew Kurulumu:**

Homebrew Apple'ın ihtiyaç duymadığı ama size lazım olabilecek paketleri kurmanızı sağlar.

```sh
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**Windows:**
**Chocolatey:**
Chocolatey CMD üzerinden kolaylıkla kurulabiliyor. Bunun için CMD'yi yönetici (administrator) modda başlatmalısınız ve ardından aşağıdaki komutu komut satırına yazarak yükleme işlemi sağlayabilirsiniz.

```sh
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```
**Linux:**
**Homebrew Kurulumu:**

```sh
cd /usr/local
```

```sh
mkdir homebrew && curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew
```
## Hugo Kurulumu

**1. Hugo Kurulumu:**
Hugo'yu kurmak için aşağıdaki komutu çalıştırınız. Bu lokal bilgisayarınıza kurulumu yapacaktır.

**MacOS:**
```sh
brew install hugo
```
**Windows:**
```sh
choco install hugo-extended -confirm
```
**Linux:**
```sh
brew install hugo
```
**2. Kurulumu Doğrulayalım:**
Kurulumun doğru yapıldığını kontrol etmek için aşağıdaki komutu çalıştırınız.

**MacOS / Windows / Linux:**
```sh
hugo version
```

**3. Hugo Sitesi Oluşturma:**
"blog" adında bir site oluşturalım. Komutun çalıştırıldığı dizinde "blog" isminde bir dizin oluşturur.
**MacOS / Windows / Linux:**
```sh
hugo new site blog
```

**4. Tema ekleme:**
Hugo birçok tema sunmaktadır. HTML ve CSS bilginizle kendi temanızı yapabileceğiniz gibi Hugo'nun [Tema](https://themes.gohugo.io/) sayfasından seçebilirsiniz. Örnek olarak, Meme temasını seçmiş olalım. Daha sonra temanın Github sayfasına erişerek, aşağıdaki komutu çalıştıralım. 

```sh
cd blog
git init
git submodule add https://github.com/reuixiy/hugo-theme-meme themes/meme
```

**5. Site Ayarlarını Yapma:**
Site ayarları config.toml dosyası üzerinden yapılmaktadır. Temanızın da ayarlarını da içerir. Bunun en doğru yolu, temanızın örnek içeriğindeki "config.toml" dosyasını değiştirmektir.

**5.1. Config Dosyasına Erişim:**
(https://github.com/reuixiy/hugo-theme-meme/tree/master/exampleSite)[https://github.com/reuixiy/hugo-theme-meme/tree/master/exampleSite] dizinindeki "config.tompl" dosyasını "blog" dizininiz altına koyunuz (Bu dizinde zaten config.toml bulunuyor, yapıştırarak değiştirebilirsiniz.)

**5.2 Config Dosyasını Değiştirme**
Her temanın kendine özgü ayarları bulunmaktadır; ancak biz genel olan her site için gerekli olan ayarlar üzerinde duracağız.

```javascript
baseURL = "https://example.com/"
```

BaseURL ayarı sitenizi nerede hangi alan adında yayınlayacağınıza göre değişmektedir. Eğer bir alan adına sahipseniz, buraya onu yazınınz ("http://volkanulutas.com") gibi. Eğer alan adına sahip değilseniz, GithubPage adresinizi yazmalısınız. Blogumuzu GitHubPages üzerinde yayımlamayı  (TODO: Githubpages yazısı)
Alan adınız bulunuyorsa;
```javascript
baseURL = "https://volkanulutas.github.io/"
```
Alan adınız yoksa;
```javascript
baseURL = "https://volkanulutas.github.io/"
```
Genellikle her temada yer alan menü yapısı aşağıdaki gibi ayarlanır. 
```javascript
[menu]
    ## Menu bar
    # [[menu.main]]
    #     url = "/"
    #     name = "Home"
    #     weight = 1
    #     pre = "internal"
    #     post = "home"
    [[menu.main]]
        url = "/posts/"
        name = "Posts"
        weight = 2
        pre = "internal"
        post = "archive"
    [[menu.main]]
        url = "/categories/"
        name = "Categories"
        weight = 3
        pre = "internal"
        post = "th"
    [[menu.main]]
        url = "/tags/"
        name = "Tags"
        weight = 4
        pre = "internal"
        post = "tags"
    [[menu.main]]
        url = "/about/"
        name = "About"
        weight = 5
        pre = "internal"
        post = "user-circle"
    [[menu.main]]
        weight = 6
        identifier = "theme-switcher"
    [[menu.main]]
        weight = 7
        identifier = "lang-switcher"
```
Menü yapısında gözükecek sayfaların ayarlanması bu bölümde yapılır. Anadizinde (blog dizininde) yer alan "content" dizinine koyacağınız "about.md" dosyası menü dizininde "About" isminde gözükecetir. "posts" dizininde yer alacak, "md" uzantılı dosyalar ise, "categories" ve "posts" olarak gözükecektir. Ayrıca bu temanın özelliği anasayfada "posts" altında yer alan "md" dosyaları gösterilecektir.

**6. Yeni Bir İçerik Ekleme:**

**MacOS / Windows / Linux:**

```sh
hugo new posts/my-first-post.md
```

**7. Yazı Ekleme:**
İçeriği bir editörde açıp, aşağıdaki gibi bir "header" dosyası eklemeliyiz, bu "header" dosyası içerikte gözükmeyecektir; ancak "post"un kategori, etiket (etiket), tarih, yayınlansın mı? gibi özellikleri ayarlanır. 

```javascript
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
```
Örneğin burada etiket (tag), kategori (category), seri (series), tarih (date), yazar (author) gibi özellikler verilir. En önemli diyebileceğimiz özellik "draft: false" olarak verilmesidir, bu şekilde verilerek "post" yayına alınır, eğer bu şekilde verilmezse yazı gözükmeyecektir, "draft" olarak kalacaktır. 

8. **Blogu Localhost'da Yayına Alma:**

**MacOS / Windows / Linux:**
```sh
hugo server -D
```

Bu komut ile birlikte [http://localhost:1313](http://localhost:1313) alanında site yayınlanmaya başlayacaktır (Konsol'da bu port yayınlanmaktadır, bazen farklı bir porttan yayınlanabiliyor bu kısma dikkat ediniz.)

Bir sonraki yazımızda Hugo blogumuzu GithupPage üzerinden yayınlamayı inceleyeceğiz. 

**Kaynaklar:**

1. [Hugo Resmi Sitesi Kurulum Sayfası](https://gohugo.io/getting-started/installing/)

 Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.







