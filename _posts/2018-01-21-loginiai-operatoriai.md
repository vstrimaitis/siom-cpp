---
layout:     lesson
title:      Loginiai operatoriai
date:       2018-01-21 23:32:00
author:     Vytautas Strimaitis
summary:    Šiame skyriuje apžvelgiami C++ loginiai operatoriai.
categories: teorija
permalink: /:title/
thumbnail:  logical
---
# Loginiai operatoriai
Šiame skyriuje apžvelgiami C++ loginiai operatoriai.

Loginis operatorius - tai funkcija, atliekanti logines operacijas su loginėmis reikšmemis. Pagrindinės loginės operacijos yra loginis "ir", loginis "arba" ir loginis neigimas. C++ turi tris operatorius, atliekančius šias logines operacijas. Toliau apžvelgsime visus šiuo operatorius.

## Loginis neigimas
Loginis neigimas "apverčia" loginės reikšmės reikšmę, t.y. `true` paverčia į `false`, o `false` paverčia į `true`. C++ programavimo kalboje loginiam neigimui žymėti naudojamas operatorius `!` (skaitoma "not"). Pavydžiui, jei turime kintamąjį `b`, tai jį paneigti galime parašę `!b`.

Loginio neigimo teisingumo lentelė:

|    a    |    !a   |
|:-------:|:-------:|
| `true`  | `false` |
| `false` | `true`  |

## Loginis "ir"
Loginis "ir" grąžina atsakymą `true` tada ir tik tada, kai abi reikšmės, su kuriomis dirbama, yra `true`. C++ programavimo kalboje loginiam "ir" žymėti naudojamas operatorius `&&` (skaitoma "and"). Pavyzdžiui, jei turime loginius kintamuosius `a` ir `b`, tai jiems pritaikyti loginio "ir" operaciją galime taip: `a && b`.

Loginio "ir" teisingumo lentelė:

|    a    |    b    | a && b  |
|:-------:|:-------:|:-------:|
| `true`  | `true`  | `true`  |
| `true`  | `false` | `false` |
| `false` | `true`  | `false` |
| `false` | `false` | `false` |

## Loginis "arba"
Loginis "arba" grąžina atsakymą `true` tada ir tik tada, kai bent viena iš reikšmių, su kuriomis dirbama, yra `true`. C++ programavimo kalboje loginiam "arba" žymėti naudojamas operatorius `||` (skaitoma "or"). Pavyzdžiui, jei turime loginius kintamuosius `a` ir `b`, tai jiems pritaikyti loginio "arba" operaciją galime taip: `a || b`.

Loginio "arba" teisingumo lentelė:

|    a    |    b    | a \|\| b  |
|:-------:|:-------:|:---------:|
| `true`  | `true`  | `true`    |
| `true`  | `false` | `true`    |
| `false` | `true`  | `true`    |
| `false` | `false` | `false`   |

## Kur naudojami loginiai operatoriai?
Loginius operatorius galima naudoti įvairiose vietose, tačiau dažniausiai juos sutiksite aprašydami įvairias sąlygas, pavyzdžiui, sąlyginiuose sakiniuose. Tarkime, jei norite išspausdinti tekstą "Valio" tada ir tik tada, kai kintamojo `x` reikšmė didesnė už 10, bet neviršija 15 (kitaip tariant, `x` didesnis už 10 **IR** nedidesnis už 15), tai rašytumėte tokį kodą:

{% highlight c++ %}
if (x > 10 && x <= 15) {
    cout << "Valio";
}
{% endhighlight %}
