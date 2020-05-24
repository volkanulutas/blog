---
author:
  name: "Volkan Ulutaş"
date: 2020-05-02
linktitle: Maven Kurulumu (MacOS)
type:
- post
- posts
title: Maven Kurulumu (MacOS)
weight: 10
tags:
- Maven
- MacOS
categories:
- İpuçları
series:
- Kurulumlar
draft: false
---

Maven'ı MacOS işletim sistemine sahip bilgisayarınıza yüklemek için aşağıdaki adımları takip edebilirsiniz.

# Maven Kurulumu Kontrol Etme
Maven bazı MacOS versiyonlarında önyüklü olarak gelmektedir, kontrol etmek için aşağıdaki komutu terminalde çalıştırınız.
```sh
$mvn -version
```

Sonuç olarak:

```sh
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /Users/volkanulutas/apache-maven-3.6.3
Java version: 1.8.0_231, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home/jre
Default locale: tr_TR, platform encoding: UTF-8
OS name: "mac os x", version: "10.15.4", arch: "x86_64", family: "mac"
```
## Maven Kurulum Dizini
```sh
$ whereis mvn
/usr/bin/mvn
 ```
 
```sh
$ cd /usr/bin
$$ ls -ls | grep mvn
 8 lrwxr-xr-x   1 root   wheel        24 May 23 15:57 mvn -> /usr/share/maven/bin/mvn
 ```
Varsayılan olarak Maven /usr/share/maven dizinine ön tanımlı olarak yüklenmiştir, bir konfigürasyon değişikliği yapmanıza gerek bulunmuyor.

# Maven Manuel Olarak Kurulumu
Mac OS X Mavericks ve sonrasında Maven ön yüklü olarak gelmemektedir. Aşağıdaki adımlarla kurulumu yapalım:

## Maven İndir
Maven'ı [buradan](https://maven.apache.org/install.html) indirebilirsiniz. (Örneğin; apache-maven-3.6.3-bin.tar.gz)

Aşağıdaki komutla sıkıştırılmış indirme dosyasını açıyoruz. Bu işlemi yaparken eğer indirilen dosya /Users/volkanulutas/ dizinine taşımalısınız:
 ```sh
$cp /User/volkanulutas/Downloads/apache-maven-3.6.3-bin.tar.gz /Users/volkanulutas
 ```
 
```sh
$tar -xvf apache-maven-3.6.3-bin.tar.gz
 
$pwd
/Users/volkanulutas/apache-maven-3.6.3
 ```
### Maven'i Ortam Değişkeni Olarak Ayarlama

Bunu ayarlama ile terminal hangi dizinde olursa olsun "mvn" komutlarını çalıştırabileceğiz.

Aşağıdaki komutla eğer bash_profile yoksa yaratacaktır.
 ```sh
~/. bash_profile
 ```

Aşağıda nano ile ~/.bash_profile dosyasını açıyoruz. "export" satırlarını ekledikten sonra kaydetmek için cntrl + O (^ O) ve çıkmak için cntrl + X (^ X) kullanılabilir. (nano yerine vim komutunu da kullanabilirsiniz.)

 ```sh
$ nano ~/.bash_profile
~/.bash_profile
export M2_HOME=/Users/volkanulutas/apache-maven-3.6.3
export PATH=$PATH:$M2_HOME/bin
```

Kurulumun doğru yapılıp yapılmadığını kontrol etemk için: 

```sh
$mvn -version

Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /Users/volkanulutas/apache-maven-3.6.3
Java version: 1.8.0_231, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home/jre
Default locale: tr_TR, platform encoding: UTF-8
OS name: "mac os x", version: "10.15.4", arch: "x86_64", family: "mac"
```

Bu şekilde kurulumumu tamamlanmış olduk. Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.
