---
title: "MATLAB Sayı Tabanı Dönüşümleri (Taban Aritmetiği)"
date: 2021-01-19 14:51 +0300
categories: "matlab-ornek-uygulamalar"
tags:  
    - "taban dönüşüm"
    - "matlab"
---

Bu yazımızda, MATLAB kullanarak taban aritmetiği yapan programdan oluşturacağız. Biz günlük hayatta onlu(decimal) sayı sistemini kullanırız. Bilgisayarlar ikili(binary) sayı sistemini kullanır. Bu yazımızda, bir başka sayı tabanındaki sayıyı onlu sayı tabanına ve onlu sayı tabanındaki sayıyı bir başka sayı tabanına çeviren programlar yazacağız. Yazacağımız programlar pozitif ve ondalıksız sayılar için olacak. Lafı daha fazla uzatmadan kodlamaya geçelim.

<h1>Başka Bir Sayı Tabanından Onlu Sayı Tabanına Dönüşüm Yapan MATLAB Programı</h1>

Başka bir sayı tabanından onlu sayı tabanına dönüşüm yaparken; sayının basamaklarındaki ifadeler(rakam veya harf olabilir), üssü olan taban ile çarpılır ve bu çarpımların toplamıyla onlu sayı sistemindeki karşılığı bulunur. Örnek olarak, üçlü sayı tabanında verilen 21 sayısını onlu sayı tabanına dönüşümü:

$$
(21)_3 = 2 \times 3^1 + 1 \times 3^0, \quad (21)_3 = 7 \text{ şeklindedir.}
$$

Tabanın üssü; son basamaktan itibaren, 0’dan başlayarak birer birer artmaktadır. Ayrıca dikkat edilmesi gereken bir başka kısım ise, sayının basamağındaki rakamlar tabandan büyük olamaz. Kodumuzu bu konulara dikkat ederek oluşturacağız. Kodlamaya geçelim:

```matlab
%kodlamaogreniyorum.com,2021
function onlutabanacevir(sayi, taban)
taban = abs(fix(taban)); %hataya karşı pozitif, tam sayı taban
sayi=abs(fix(sayi)); %pozitif,ondalıksız sayılar
sayi=num2str(sayi); %str çevirme   
    if ~any(str2num(sayi(:))>=taban) && (taban>1) && (taban<10) %taban kontrol
        cevrilmis_sayi=0;
        us = 0;
        for i=flip(sayi)
            cevrilmis_sayi=cevrilmis_sayi+str2num(i)*(taban^us);
            us = us + 1;
        end
        fprintf('(%s)_%d = %d\n',sayi,taban,cevrilmis_sayi);
    else
        fprintf('Girdiğiniz sayı ile taban uyumsuz!\n');
    end
end
```

3.ve 4. satırda yazdığımız ifadeler ile kullanıcının hatalı taban veya sayı girmesini önlemiş olduk. `“~any(str2num(sayi(:))>=taban)”` ifadesi ile basamaklardaki rakamların tabandan büyük olup olmadığını kontrol ettik. `“for i=flip(sayi)”` döngüsündeki “i”, sayının son basamağından başlayarak, her basamaktaki rakamları ifade etmektedir.

> Onlu tabana dönüşüm yapan MATLAB Fonksiyonu: base2dec()

![](/assets/img/matlab/matlab78.webp){: style="width: 125%; height: auto;" }

<h1>Onlu Sayı Tabanından Bir Başka Sayı Tabanına Dönüşüm Yapan MATLAB Programı</h1>

Onlu sayı tabanından bir başka sayı tabanına dönüşüm yapmak için; sayı, tabandan küçük kalıncaya kadar sürekli olarak tabana bölünür. Bu işlem sonrasında, ilk olarak bölüm ve sondan başa olacak sırayla tüm kalanlar soldan sağa doğru yazılarak yeni sayı bulunur. Örnek olarak, 137 sayının altılı sayı tabanına dönüşümü:

$$
137 = (x)_6
$$

$$
\frac{137}{6} = 22 \quad \text{Kalan: } \textcolor{orange}{5}
$$

$$
\frac{22}{6} = \textcolor{blue}{3} \quad \text{Kalan: } \textcolor{orange}{4}
$$

$$
137 = (345)_6 \text{ şeklindedir.}
$$

Kodlamaya geçelim:

```matlab
%kodlamaogreniyorum.com,2021
function tabandegistir(sayi, taban)
if (taban>1) && (taban<10)
    taban = fix(taban); %hataya ondalıksız taban
    sayi=abs(fix(sayi)); %pozitif,ondalıksız sayılar
    sayi2 = sayi; %fprintf için saklama
    cevrilmis_sayi = [];
    while sayi >= taban
        kalan = mod(sayi,taban);
        sayi = fix(sayi/taban);
        cevrilmis_sayi = [num2str(kalan) num2str(cevrilmis_sayi)];
        if sayi < taban
            cevrilmis_sayi = [num2str(sayi) num2str(cevrilmis_sayi)];
        end
    end
    fprintf('%d = (%s)_%d\n',sayi2,cevrilmis_sayi,taban);
else
    fprintf('Tabanı kontrol edin!\n');
end
end
```

4.ve 5. satırda yazdığımız ifadeler ile hatalı sayı veya taban girilmesini önlemiş olduk. Girilin sayı üzerinden işlem yaptığımız için 6. satırdaki ifade ile girilen sayının kopyasını oluşturduk. `“while sayi >= taban”` ifadesi ile döngünün, sayı tabandan küçük kalıncaya kadar devam etmesini sağladık. `“cevrilmis_sayi = [num2str(kalan) num2str(cevrilmis_sayi)];”` ifadesi ile sondan başa ekleme yapmayı sağladık.

![](/assets/img/matlab/matlab79.webp){: style="width: 125%; height: auto;" }

Bütün **MATLAB kodlarına** Github sayfam aracılığı ile erişebilirsiniz. Github sayfamın linkine aşağıdan ulaşabilirsiniz. Görüşmek üzere!

Github: [Github MATLAB](https://github.com/TunahanBilgic/kodlamaogreniyorum/tree/main/matlab)

Sitemize destek olmak isteyen sponsorlar için link: [Patreon](https://patreon.com/tunahanbilgic)

<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-mml-chtml.js">
</script>