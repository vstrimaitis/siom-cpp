---
layout:     lesson
title:      Palyginimo operatoriai
date:       2018-01-21 23:50:00
author:     Vytautas Strimaitis
summary:    Šiame skyriuje apžvelgsime palyginimo operatorius, kuriuos palaiko C++ programavimo kalba.
categories: teorija
thumbnail:  comparison
---
# Palyginimo operatoriai
Palyginimo operatoriai naudojami palyginti dvi reikšmes tarpusavyje. Šiame skyriuje apžvelgsime palyginimo operatorius, kuriuos palaiko C++ programavimo kalba.

Palyginimo operatoriai C++ kalboje gali dirbti su įvairaus tipo reikšmėmis, tačiau jų rezultatas - visada loginio tipo reikšmė. C++ palaiko šiuo palyginimo operatorius:
* **Lygu** (žym. `==`). Grąžina `true` tada ir tik tada, kai lyginamos reikšmės yra visiškai lygios (pvz.: `2 == 2` grąžina `true`, o `2 == 1` grąžina `false`). Svarbu šio operatoriaus nepainioti su priskyrimo operatoriumi (žym. `=`), nes tai gali sukelti netikėtų klaidų kodo veikimo metu.
* **Nelygu** (žym. `!=`). Grąžina `true` tada ir tik tada, kai lyginamos reikšmės yra nelygios (pvz.: `2 != 2` grąžina `false`, o `2 != 1` grąžina `true`).
* **Daugiau** (žym. `>`). Grąžina `true` tada ir tik tada, kai pirmoji reikšmė yra griežtai **didesnė** už antrąją (pvz.: `2 > 1` grąžina `true`, o `2 > 2` grąžina `false`).
* **Mažiau** (žym. `<`). Grąžina `true` tada ir tik tada, kai pirmoji reikšmė yra griežtai **mažesnė** už antrąją (pvz.: `1 < 2` grąžina `true`, o `2 < 2` grąžina `false`).
* **Daugiau arba lygu** (žym. `>=`). Grąžina `true` tada ir tik tada, kai pirmoji reikšmė yra **didesnė arba lygi** už antrąją (pvz.: `2 >= 1` bei `2 >= 2` grąžina `true`, o `1 >= 2` grąžina `false`).
* **Mažiau arba lygu** (žym. `<=`). Grąžina `true` tada ir tik tada, kai pirmoji reikšmė yra **mažesnė arba lygi** už antrąją (pvz.: `1 <= 2` bei `2 <= 2` grąžina `true`, o `2 <= 1` grąžina `false`).

## Kur naudojami palyginimo operatoriai?
Playginimo operatorius galima naudoti įvairiose vietose, tačiau dažniausiai juos sutiksite aprašydami įvairias sąlygas, pavyzdžiui, sąlyginiuose sakiniuose. Tarkime, jei norite išspausdinti tekstą "Valio" tada ir tik tada, kai kintamojo `x` reikšmė didesnė už 10, tai rašytumėte tokį kodą:

{% highlight c++ %}
if (x > 10) {
    cout << "Valio";
}
{% endhighlight %}
