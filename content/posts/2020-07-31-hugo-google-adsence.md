---
author:
  name: "Volkan Ulutaş"
date: 2020-07-31
linktitle: Hugo'ya GoogleAdSense Reklam Alanı Ekleme (Tema Bağımsız)
type:
- post
- posts
title: Hugo'ya GoogleAdSense Reklam Alanı Ekleme (Tema Bağımsız)
weight: 10
tags:
- Hugo
categories:
  - Hugo

series:
  - Teknolojiler
draft: false
---

<style>
body {
    margin: 0px;
    padding: 0px;
}
table {
    margin-right: auto;
    margin-left: auto;
}
.image {

}
.caption p {
    margin-top: 0px;
}

</style>

<table>
  <tr>
    <td class="image"><img height="150" width= ="100" src="/images/hugo-adsense/hugo.jpg" </td>
    <td class="image"><img height="150" width= ="100" src="/images/hugo-adsense/adsense.jpg" </td>
  </tr>
</table>



Merhabalar, bu yazımızda Hugo blogunuza tema özelliklerinde olmasa bile Google Adsense reklam alanı eklemeyi inceleyeceğiz.

## 1.) Reklamın Gösterileceği Alanı Oluşturma:


**[HUGO_HOME]/themes/[THEME_NAME]/layouts/partials/adsense-inarticle.html**
dizinde aşağıdaki kod parçacığını içeren içeriği oluşturunuz.

>> [HUGO_HOME] hugo blogunuzun kurulumunun yapıldığı dizindir.
>> [THEME_NAME] aktif olarak kullandığınız temanın bulunduğu dizindir.

```html
<!-- in-article ad -->
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<ins class="adsbygoogle"
     style="display:block; text-align:center;"
     data-ad-layout="in-article"
     data-ad-format="fluid"
     data-ad-client="{{.Site.Params.Adsense.client}}"
     data-ad-slot="{{.Site.Params.Adsense.inArticleSlot}}"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>
```

## 2.) Google Adsense Hesabınızı Hugo'ya Bağlama:

Google Adsense hesabınızın bilgilerini (clientId ve SlodId) **config.toml** genel ayar dosyanıza ekleyiniz.

```js
[params.adsense]
client = "ca-pub-12345"
inArticleSlot = "12345"
```

## 3.) Yazılarınıza Google Adsense'ı Ekleme:

Blog yazılarınız içerisinde **<!--adsense-->** ifadesini kullanarak Google Adsense reklamlarını yazınıza dahil edebilirsiniz.

```md
Bu ilk paragraftır.

Bu ikinci paragraftır.

<!--adsense-->

Bu üçüncü paragraftır.
```

## 4.) <!--adsense--> Etiketinin Render Edilmesi:

Eklediğimiz reklam etiketinin (<!--adsense-->) işletilmesi için **[HUGO_HOME]/themes/[THEME_NAME]/layouts/_default/single.html** sayfasını açıp **{{ .Content }}** etiketini aratınız. Bu alanı aşağıdaki kod parçacığı ile değiştiriniz.


```md
{{ replace .Content "<!--adsense-->" (partial "adsense-inarticle.html" .) | safeHTML }}
```

Bu şekilde blog yazılarımızın içerisine Google Adsense reklamlarımızı eklemiş olduk.


Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.
