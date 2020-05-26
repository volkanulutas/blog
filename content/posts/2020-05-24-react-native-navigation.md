---
author:
  name: "Volkan Ulutaş"
date: 2020-05-24
linktitle: React Native - Navigation V5 (StackNavigation ve TabNavigation)
type:
- post
- posts
title: React Native Navigation (StackNavigation ve TabNavigation)
weight: 10
tags:
- react-native
- react-native-navigation
- stack navigation
- tab navigation
categories: 
  - React Native
series:
  - Makale
draft: false
---

<img src="/images/react-native-navigation/react-native.png" height="300" width="600">

Merhabalar, bu yazımızda React-Native menü ve sayfalar arası geçişleri inceleyeceğiz. 



## 1.) React Natıve Kurulumu 

React-Native'ın kurulumu ile ilgili çok güzel anlatımlar mevcut bunların linkine aşağıdan ulaşabilirsiniz, daha sonra bu kurulumlarla ilgili ben de bu blog'da paylaşımda bulunacağım. 

>> Kurulum Bağlantıları: 
*[Windows](https://medium.com/mol42/windows-%C3%BCzerinde-react-native-kurulumu-4de15e0e33b9)* , *[MacOS](https://medium.com/mol42/macos-%C3%BCzerinde-react-native-kurulumu-71d4f96c282e)*, *[Linux](https://medium.com/mol42/linux-%C3%BCzerinde-react-native-kurulumu-a61b54927941)*

## 1.1.) Editor Seçimi ve Kurulum

React-Native geliştirmesi için bir editör kullanmamız işimizi çok kolaylaştıracaktır. Benim tercihimi Visual Studio Code'dan yana kullandım, *[buradan](https://code.visualstudio.com/download)* indirme işlemini yapabilirsiniz.

>> [Visual Studio Code İndirme Bağlantısı](https://code.visualstudio.com/download)

## 2.) React-Natıve Projesinin Başlatılması:
Kurumları bu adıma geldiğimizde tamamlamış olduğunuzu varsayıyorum. Şimdi yeni bir React-Native uygulamasını aşağıdaki komut ile başlatalım: 
```sh
react-native init ReactNativeNavigationSample 
```

React-Native uygulamarını varsayılan olarak JavaScript kullanarak geliştirmek mümkün; ancak Typescript gibi bir dilinde avantajlarından yararlanabilmek için aşağıdaki komut ile projeyi başlatmak daha uygun olacaktır. Typescript şablonu seçilerek başlatılmayan bir projeyi daha sonradan Typescript ile yazacak hala getirebiliriz; ancak bu süreç zor olduğu için başlanğıçta aktifleştirmek daha doğru olacaktır.

```sh
react-native init ReactNativeNavigationSample --template typescript 
```

Kurulumu doğrulamak için projeyi çalıştıralım:

```sh
cd ReactNativeNavigationSample

react-native run-ios
react-native run-android
```

Kurulum doğru olarak yapılandırılmış ise, emulator veya bağlı olan cihazda aşağıdaki ekran görüntüsü oluşmaktadır.


<img src="/images/react-native-navigation/2.png" height="600" width="600">

>> Bu aşamada aşağıdaki ekran görüntüsünde gibi bir hata alırsanız, proje ana dizininde /template/package.json dosyasını siliniz.

>> ![metin](/images/react-native-navigation/1.png)


<img src="/images/react-native-navigation/github.jpg" height="150" width="300" /> 

Bu aşamaya kadar kodumuzu ***[buradan](https://github.com/volkanulutas/blog-tutorials/tree/ebfec43487241bac1314de81ea3121f2a6c43f9e)*** inceleyebilirsiniz.


## 3.) react-natıve-navıgatıon Kütüphanesinin Kurulumu:

Ana dizine gidelim.
```sh
cd ReactNativeNavigationSample
```

Daha sonra "navigation" için gerekli kütüphanelerin kurulumuna başlayalım. Kurulum için "npm" veya "yarn" paket yöneticilerini kullanabilirsiniz.

**3.1.)** Navigation kütüphanesinin ve bağlılıklarının (dependency) kurulumunu yapalım.

```sh
yarn add @react-navigation/native
yarn add @react-navigation/stack
yarn add @react-navigation/bottom-tabs
```
veya
```sh
npm install @react-navigation/native
npm install @react-navigation/stack
npm install @react-navigation/bottom-tabs
```

**3.2.)** Navigation için gerekli bağımlılıkları kuralım:

```sh
yarn add react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view
```
veya
```sh
npm install react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

**3.3.)** Gesture Handler kütüphanesini kuralım:

```sh
yarn add react-native-gesture-handler
```
veya
```sh
npm install react-native-gesture-handler
```
**3.4.)** Daha sonra IOS için gerekli olan "pod" kurulumunu yapalım. Bu işlemi yeni bir kütüphane kurulumunun ardından tekrarlamanızı öneririm.

```sh
cd ios
pod install
cd ..
react-native link
```
**3.5.)** Navigation için gerekli bağımlılıkları kurduk. Şimdi tasarıma başlamadan önce projeyi emulator veya telefonda çalıştıralım:

```sh
react-native run-ios
react-native run-android
```

## 4.) react-native-navigation Kütüphanesinin Kullanımı:
Kurulum tamamlandıktan sonra ana dizinde "src" adında bir klasör oluşturalım. "src" klasörünün altında "containers" ve "navigation" isimlerinde klasörler oluşturalım. "container" klasörünün altında yapacağımız ekranları konumlandıracağız. "navigation" klasöründe ise "stack" ve "tab" navigation kullanımlarını inceleyeceğiz.

## 4.1.) Ekranların Tasarlanması:

Uygulamamızda 4 adet ana ekran (Mesajlar, Bildirimler, Profil ve Ayarlar) bulunmaktadır ve bunları "tab navigation" içerisinde tasarlayıp geçiş sağlayacağız. Somutlaştırmak amacıyla ekranın amaçlarını da inceleyelim:

- Mesajlar Ekranı: Bu ekran aracılığıyla kullanıcı, diğer kullanıcılarla mesajlaşabilmektedir.

- Profil Ekranı: Kullanıcının profil bilgilerini görüntüleyip, değiştirebileceği ekrandır.

- Bildirimler Ekranı: Uygulama içinde verilen bilgilendirme mesajlarının görüntülendiği ekrandır.

- Ayarlar Ekranı: Kullanıcının uygulama ile ilgili tercihlerini gözlemleyip, değiştirebileceği ekrandır.

Bu ekranları fonksiyonel olarak kodlamayacağız, amacımız "navigation" yapısını incelemek olacaktır. 

>> **Projenin Visual Studio Code İle Açılması:**
Visual Studio Code açılır. Daha sonra "File/Open" menüsünden projeyi oluşturduğumuz ana dizin seçilir. 

## 4.1.1.) Ana Dosya Dizinlerinin Oluşturulması:

Yaygın yaklaşım olarak kodlarımızı "src" isminde ana bir dizinin altında konumlandırıyoruz. "src" klasörünün altında;

- container: Ekranlarımızı konumlandıracağız. 
- navigation: tab ve stack navigation yapılarımızı "component" olarak oluşturup kullanacağız. 

"container" klasörünün altında "message", "notification", "profile" ve "setting" isimlerinde klasörler oluşturalım ve ekranlarımızı bu klasörler üzerinden yönetelim.

## 4.1.2.) Mesaj Ekranı (MessageScreen.tsx)

Daha sonra tüm bu ekranların altında aşağıdaki .tsx (.js de olabilir) dosyalarını oluşturalım. Örneğin aşağıdaki "MessageScreen.tsx" dosyasını "src/container/message" klasörünü Visual Studio Code üzerinden seçerek "New File" diyelim ve "MessageScreen.tsx" ismini verelim. Boş olarak oluşmuş dosyanın içerisine aşağıdaki kod parçacığını yapıştıralım.

```js
import * as React from 'react';
import { View, Text, Button} from 'react-native';

function MessageScreen({ navigation }) {
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Message Screen</Text>
        <Button
          title="Go to Details"
          onPress={() => navigation.navigate('Details')}
        />
      </View>
    );
  }

export default MessageScreen;
```
Şimdi ekranımızı kod parçaları halinde inceleyelim:

```js
import * as React from 'react';
import { View, Text, Button} from 'react-native';
```
Burada kütüphanelerimizi ilgili ekranımıza ekliyoruz. React kütüphanesini ekranımızı dahil ettik ve "react-native" kütüphanesinden "View", "Text" ve "Button" elemanlarını kullanacağımızı belirtmiş oluk.

```js
function MessageScreen({ navigation }) {
    return ();
};
```
"React" kütüphanesini kullanacağımızı belirtmiştik, her React sınıfında "return" adında bir fonksiyonla dönüş yaparız. Burada tasarımımızı tanımlar ve dönüşünü sağlarız.

```js
<View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
```

Bu kod parçacığında View tanımlıyoruz. View aslında bir container gibi elemanlarımızı derli toplu tutmamıza ve ortak stiller vermemizi sağlar. View'a stil veriyoruz ve "flex:1" diyerek tüm ekranı kapsamasını belirtiyoruz. "alignItems: 'center', justifyContent: 'center'" diyerek içerikleri ortalamış olduk. Bundan sonra View'ın altında yer alan herhangi bir eleman için bu stil kuralları geçerli olacaktır. 

```js
 <Button title="Go to Details"
         onPress={() => navigation.navigate('Details')} />
```
Bu kod parçacığında bir buton tanımladık ve butona tıklandığında ne yapacağını bir fonksiyon olarak vermiş olduk. Burada butona tıklandığında "Details" isminde bir ekranın açılmasını tetiklemiş olacağız.

Şimdi diğer ekranlarımızı tasarlayalım.

## 4.1.3.) Bildirim Ekranı (NotıfıcatıonScreen.tsx)

Diğer ekranlarımızda MessageScreen ekranına benzer şekilde projemize dahil edelim. Visual Studio Code'da "src/container/notification" klasörünü seçerek, "New File" diyelim ve "NotificationScreen.tsx" ismiyle adlandıralım. Daha sonra aşağıdaki kodu bu dosyaya yapıştıralım. 

```js
import * as React from 'react';
import { View, Text, Button} from 'react-native';

function NotificationScreen({ navigation }) {
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Notification Screen</Text>
        <Button
          title="Go to Details"
          onPress={() => navigation.navigate('Details')}
        />
      </View>
    );
  }

export default NotificationScreen;
```

## 4.1.4.) Profil Ekranı (ProfıleScreen.tsx)

Visual Studio Code'da "src/container/profile" klasörünü seçerek, "New File" diyelim ve "ProfileScreen.tsx" ismiyle adlandıralım. Daha sonra aşağıdaki kodu bu dosyaya yapıştıralım. 

```js
import * as React from 'react';
import { View, Text, Button} from 'react-native';

function ProfileScreen({ navigation }) {
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Profile Screen</Text>
        <Button
          title="Go to Details"
          onPress={() => navigation.navigate('Details')}
        />
      </View>
    );
  }
export default ProfileScreen;
```

## 4.1.5.) Ayarlar Ekranı (SettingScreen.tsx)

Visual Studio Code'da "src/container/setting" klasörünü seçerek, "New File" diyelim ve "SettingScreen.tsx" ismiyle adlandıralım. Daha sonra aşağıdaki kodu bu dosyaya yapıştıralım. 

```js
import * as React from 'react';
import { View, Text, Button} from 'react-native';

function SettingScreen({ navigation }) {
    return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Settings Screen</Text>
        <Button
          title="Go to Details"
          onPress={() => navigation.navigate('Details')}
        />
      </View>
    );
  }
export default SettingScreen;
```

## 4.1.6.) Detay Ekranı (Details.tsx)

Detay ekranı, tasarlanan tüm diğer ekranların "buton" elemanının "onClick()" metodunda kullanılmıştır ve "StackNavigation" kullanımını örneklendirmek için kullanılmıştır.

```js
import * as React from 'react';
import { View, Text, Button} from 'react-native';

function Details({ navigation }) {
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Details Screen2</Text>
        <Button title="Go to Home" onPress={() => navigation.navigate('Home')} />
        <Button title="Go back" onPress={() => navigation.goBack()} />
        <Button
          title="Go back to first screen in stack"
          onPress={() => navigation.popToTop()}
        />
      </View>
    );
  }
  
  export default Details;
```

## 5.) Navıgation'ın Ayarlanması:

## 5.1.) StackNavıgatıon.tsx 

Dosya dizininden "src/navigation" klasörünün altına gelip yeni bir .tsx uzantılı (veya .js) "StackNavigation.tsx" isminde bir dosya oluşturunuz. Benzer şekilde Visual Studio code içerisinden "src/navigation" klasörünü seçerek "New File" seçeneğinde "StackNavigation.tsx" yazarak dosyayı oluşturalım. Dosyayı oluşturduktan sonra aşağıdaki kod parçacığını dosyaya yapıştırınız.

```js
import * as React from 'react';

import { createStackNavigator } from '@react-navigation/stack';

import TabNavigation from '../navigation/TabNavigation';
import DetailsScreen from "../container/Details"

const Stack = createStackNavigator();

function StackNavigaiton() {
    return (
        <Stack.Navigator initialRouteName="Home" 
        screenOptions={{
          headerStyle: {
            backgroundColor: '#4CB6ED',
          },
          headerTintColor: '#fff',
          headerTitleStyle: {
            fontWeight: 'bold',
          },
        }} >
          <Stack.Screen name="Home" component={TabNavigation} />
          <Stack.Screen name="Details" component={DetailsScreen} options={{ title: 'Detaylar' }}   />
      </Stack.Navigator>
    );
  }
  export default StackNavigaiton;
```

StackNavigation yapısını, WEB tarayıcınızda olduğu gibi gidilen bir sitedeki "Geri/İleri" butonlarına bahsedebiliriz. Site içerisinde tıkladığınız her bağlantı sonrasında "Geri" butonuyla bir önceki sayfaya gidilebilir. "StackNavigation"de aynı şekilde bir sayfadan diğerine gittiğimizde "Geri" butonuyla bir önceki ekrana geçişimizi sağlar. Genellikle detay ekranlarında kullanılır. Bizim projemizden örnek verecek olursak, "Mesajlar" ekranında arkadaş listenizin gösterildiğini düşünelim, herhangi bir arkdaşınızın ismine tıklandığında açılan "Mesajlaşma" ekranı "detay" ekranı olarak düşünülebilir. Yine "Geri" butonuyla arkadaş listenize gelebileceksiniz.


Burada "import"larımızı yapıyoruz. Detay ekranımızı "stack" yapısında kullacağız. Ana ekranımız  "TabNavigation" olacaktır. Detay ekranımız ise "Details" sınıfı olacaktır ve TabNavigation içerinde yer alan sınıfların (MessageScreen.tsx, ProfileScreen.tsx gibi) onClick metodunda "Details" ekranını açıyoruz. "StackNavigation"a eklediğimiz "Details" sınıfı sayesinde "Geri" kontrolünü oluşturmuş olduk.

```js
import TabNavigation from '../navigation/TabNavigation';
import DetailsScreen from "../container/Details"
```

Burada bir diğer önemli kod parçacığı aşağıdaki gibidir. "Stack.Navigator"a bu şekilde stil vermiş oluyoruz. 

```js
creenOptions={{
          headerStyle: {
            backgroundColor: '#4CB6ED',
          },
          headerTintColor: '#fff',
          headerTitleStyle: {
            fontWeight: 'bold',
          },
        }}
```

## 5.2.) TabNavıgation.tsx

Dosya dizininden "src/navigation" klasörünün altına gelip yeni bir .tsx uzantılı (veya .js) "TabNavigation.tsx" isminde bir dosya oluşturunuz. Benzer şekilde Visual Studio code içerisinden "src/navigation" klasörünü seçerek "New File" seçeneğinde "TabNavigation.tsx" yazarak dosyayı oluşturalım. Dosyayı oluşturduktan sonra aşağıdaki kod parçacığını dosyaya yapıştırınız.

```js
import * as React from 'react';
import { View, Text, Button, Image } from 'react-native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

import MessageScreen from '../container/message/MessageScreen';
import NotificationScreen from '../container/notification/NotificationScreen';
import ProfileScreen from '../container/profile/ProfileScreen';
import SettingScreen from '../container/setting/SettingScreen';

const Tab = createBottomTabNavigator();

function TabNavigation() {
    return (
    <Tab.Navigator>
            <Tab.Screen name="Mesajlar" component={MessageScreen} />
            <Tab.Screen name="Bildirimler" component={NotificationScreen} />
            <Tab.Screen name="Profil" component={ProfileScreen}/>
            <Tab.Screen name="Ayarlar" component={SettingScreen} />
        </Tab.Navigator>
        );
  }
  export default TabNavigation;

```

TabNavigation.tsx sınıfını açıklayalım. Öncelikle kullanacağımız ekranları import ediyoruz. Bulunduğumuz dizinin bir üst dizininde "container" klasörü bulunuyor. Buna erişmek için "../" ibaresini kullanıyoruz. Örneğin "Bildirimler" ekranını aşağıdaki gibi eklemiş olduk: 

```js
import NotificationScreen from '../containers/notification/NotificationScreen';
```

Burada daha önce görmediğimiz "navigation" için gerekli olan bir bağlılığı daha bu sınıfımıza aşağıdaki gibi ekliyoruz:

```js
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
```

Daha sonra global olarak aşağıdaki kod ile TabNavigation'ı yaratıyoruz.

```js
const Tab = createBottomTabNavigator();
```

return fonksiyonu içinde o sınıfta yaptığımız tasarımı döndüğümüzü belirtmiştik, şimdi burada da navigation tasarımızı aşağıdaki gibi tasarlayıp dönüyoruz. Tab.Screen alanının "name" alanında ilgili "tab"ımızın görünen adını vermiş oluyoruz, "component" olarak ise import ettiğimiz ekranlardan hangisinin tıklandığında gidileceğini belirtmiş olduk.

```js
function TabNavigation() {
    return (
    <Tab.Navigator>
            <Tab.Screen name="Mesajlar" component={MessageScreen} />
            ...
```            

## 6.) App.tsx

>> Ana dizinde yani "src" dizininin üzerinde **"App.js"** isminde bir sınıf bulunmaktadır. Bu sınınfın adını **"App.tsx"** olarak değiştirelim. "App.tsx" veya "App.js" uygulamamız ilk açıldığında gösterilecek olan sınıftır. Kod incelemeye buradan başlamak doğru olacaktır, giriş noktasıdır. Kod parçacığını incelediğimizde" "<NavigationContainer />" ile anasayfamızda bir navigation topluluğu kullanabileceğimizi belirtmiş olduk. Daha sonra önceden tasarlamış olduğumuz "<StackNavigatinon>" "component"imizi "container" içinde konumlandırıyoruz. Ek olarak "StackNavigation" sınıfını da import ettik. 

```js
import React from 'react';

import { NavigationContainer } from '@react-navigation/native';
import StackNavigation from './src/navigation/StackNavigation'

const App: () => React$Node = () => {
  return (
    <NavigationContainer>
      <StackNavigation/>
    </NavigationContainer>
  );
};
export default App;
```

Son olarak projemizi tamamladığımızda emülatörlerde aşağıdaki gibi projemizi oluşturmuş olduk. 

<img src="/images/react-native-navigation/3.png" height="600" width="600">

<img src="/images/react-native-navigation/4.png" height="600" width="600">

## 7.1.) Projeye Gıthub Üzerinden Erişim ve Çalıştırma:

<img src="/images/react-native-navigation/github.jpg" height="150" width="300">

Projenin son halini ***[buradan](https://github.com/volkanulutas/blog-tutorials/tree/master/ReactNativeNavigationSample)***inceleyebilirsiniz.


Github üzerinden "fork"layarak veya "clone" ederek eriştiğiniz kodu aşağıdaki komutlar derleyip, çalıştırabilirsiniz. Öncelikle projeyi indirdiğiniz dizine gidiniz.

```sh
npm install
```

Makalemizde anlatılan 2. kısmı tekrarlanıyız, daha sonra aşağıdaki komutları çalıştırınız.

```sh
cd ios
install pods
cd ..
react-native run-android
react-native run-ios
```

Bu şekilde kurulumu tamamlanmış olduk. Soru, görüş ve önerilerinizi bu sayfaya yorum yapabilirsiniz. Bana erişmek için volkanulutas@gmail.com adresini kullanabilirsiniz.

