---
title: Python Seçerek Sıralama (Selection Sorting) Algoritması
date: 2020-01-08 00:24 +0300
categories: "python-algoritmalar"
tags:  
    - "python algoritmalar"
    - "seçerek sıralama"
    - "selection sorting"
    - "python"
---

Bu yazımızda, bir [Sıralama algoritması](https://www.kodlamaogreniyorum.com/python-algoritmalar/) olan “Seçerek Sıralama” (Selection Sorting) algoritmasına değineceğiz. Seçerek Sıralama algoritmasını diziyi küçükten büyüğe sıralamak için kullanacağız.

Seçerek Sıralama algoritmasının işleyişi; dizideki en küçük elemanı ilk sıraya yerleştirir, kalanlardan en küçük olanı da ikinci sıraya yerleştirir.Bir eleman kalana kadar bu şekilde devam eder.

[Buradaki bağlantıya](https://www.toptal.com/developers/sorting-algorithms) tıklayarak, sıralama algoritmalarının çalışma şekillerine ait animasyona bakabilirsiniz.

!["Kaynak: Vikipedi"](/assets/img/matlab/matlab51.gif){: style="width: 75%; height: auto;" }  Görsel Kaynak:Vikipedi

Örnek olarak, “a” isimli dizinin adım adım küçükten büyüğe sıralanması:

```python
a = [3 4 1 1000 -1 25 35 111]
```

[<span style="background-color: yellow;">3</span>, 4, 1, 1000, <span style="color: red;">-1</span>, 25, 35, 111]

[-1, <span style="background-color: yellow;">4</span>, <span style="color: red;">1</span>, 1000, 3, 25, 35, 111]

[-1, 1, <span style="background-color: yellow;">4</span>, 1000, <span style="color: red;">3</span>, 25, 35, 111]

[-1, 1, 3, <span style="background-color: yellow;">1000</span>, <span style="color: red;">4</span>, 25, 35, 111]

[-1, 1, 3, 4, <span style="background-color: yellow;">1000</span>, <span style="color: red;">25</span>, 35, 111]

[-1, 1, 3, 4, 25, <span style="background-color: yellow;">1000</span>, <span style="color: red;">35</span>, 111]

[-1, 1, 3, 4, 25, 35, <span style="background-color: yellow;">1000</span>, <span style="color: red;">111</span>]

[-1, 1, 3, 4, 25, 35, 111, <span style="background-color: yellow;">1000</span>]


Algoritmanın kodları:

```python
def secerek_sirala(Vektor):
    for i in range(len(Vektor)-1):
        enk = Vektor[i]
        enk_indis = i
        for j in range(i+1, len(Vektor)):
            if Vektor[j] < enk:
                enk = Vektor[j]
                enk_indis = j

        depo = Vektor[i]
        Vektor[i] = Vektor[enk_indis]
        Vektor[enk_indis] = depo
        #print(Vektor) Bu komutu aktif ederek sıralama adımlarını görebilirsiniz.
    print(Vektor)

a = [3, 4, 1, 1000, -1, 25, 35, 111]
secerek_sirala(a)
```

İlk döngü ( i ) en küçük elemanın atanacağı indisi temsil ediyor. İkinci döngüyü ( j ) ise en küçük elemanı bulma amacıyla kullanıyoruz. Dolayısıyla ikinci döngüyü, ilk döngünün bulunduğu yerden bir sonraki sıradan başlatmamız gerekiyor. (for j in range(i+1)) Algoritma son elemanda biteceği ve ikinci döngü, ilk döngüden bir sonraki sıradan başladığı için; ilk döngünün bitiş değeri, “a” dizisinin boyutundan bir eksik olması gerekiyor. Dizinin elemanlarının yerlerini değiştireceğimiz için bir saklama değişkeni(depo) kullanıyoruz. Son iki satırda ise  sıralanmasını istediğimiz diziyi tanımlıyoruz ve fonksiyonumuzu çağırıyoruz. 

Programın ekran görüntüsü:

![](/assets/img/python/python63.png)

> 10. satıra sadece “Vektor[i], Vektor[enk_indis] = Vektor[enk_indis], Vektor[i] yazarak kodlamayı kısaltabiliriz.

> 16. satırda sıralanmasını istediğimiz diziyi tanımlıyoruz, 17. satırda da fonksiyonumuzu çağırıyoruz.

Aldığımız çıktı:

![](/assets/img/python/python64.png)

> Sıralama yapmak için “.sort()” fonksiyonunu kullanabilirsiniz.

Bütün **Python kodlarına** Github sayfam aracılığı ile erişebilirsiniz. Github sayfamın linkine aşağıdan ulaşabilirsiniz. Görüşmek üzere!

Github: [Github Python](https://github.com/TunahanBilgic/kodlamaogreniyorum/tree/main/python)

Sitemize destek olmak isteyen sponsorlar için link: [Patreon](https://patreon.com/tunahanbilgic)

Kaynak: [Carnegie Mellon University, School of Computer Science](http://www.cs.cmu.edu/~adamchik/15-121/lectures/Sorting%20Algorithms/sorting.html)