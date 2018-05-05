---
layout:     lesson
title:      Simbolių eilutės
date:       2018-05-05 11:12:00
author:     Vytautas Strimaitis
summary:    Šiame skyriuje išmoksime, kas yra simbolių eilutės ir kaip su jomis dirbti.
categories: teorija
permalink: /:title/
thumbnail:  quote
iconclass:  fas fa-book
published: true
---
# Simbolių eilutės
Per ankstesnes pamokas jau išmokome apie įvairius duomenų tipus C++ programavimo kalboje (`int`, `bool`, `char` ir kitus). Taip pat išmokome apie masyvus bei kaip galima susikurti savo tipą naudojantis struktūromis. Dabar laikas šių žinių pilnai užtenka norint susikurti savo ganėtinai daug galimybių suteikiančius tipus. Tačiau tai daryti ne visada būtina, nes standartinė C++ biblioteka pateikia nemažai tokių labai naudingų tipų. Šioje pamokoje apžvelgsime vieną iš jų - simbolių eilutes.

# Kas yra simbolių eilutė?
Simbolių eilutė (angl. *string*) yra labai paprastas dalykas - tai tiesiog simbolių (`char`) masyvas. C++ kalboje šis tipas identifikuojamas raktažodžiu `string`, o jo reikšmės rašomos tarp **dvigubų** kabučių (palyginimui: `char` reikšmės rašomos tarp viengubų kabučių). Tiesa, norint naudotis šiuo tipu reikia prisidėti papildomą biblioteką į savo kodą parašant eilutę `#include <string>`. Štai kodo pavyzdys, sukuriantis simbolių eilutę ir išspausdinantis jos reikšmę į konsolę:

{% highlight c++ %}
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "Labas, pasauli!"; // sukuriame simbolių eilutę su reikšmę "Labas, pasauli!"
    cout << s << endl; // išspausdiname jos reikšmę į konsolę
    return 0;
}
{% endhighlight %}

Kaip matote, `string` tipą galima naudoti kaip ir bet kokį kitą mums jau įprastą tipą.

# Kuo `string` geriau už `char` masyvą?
Kaip jau buvo minėta, `string` iš esmės yra tas pats, kaip `char` masyvas. Tuomet natūraliai kyla klausimas - kam reikia to `string`, jei galima susikurti `char` masyvą? Atsakymas labai paprastas - `string` leidžia ne tik saugoti kelis simbolius vienoje vietoje, tačiau pateikia ir naudingų funkcijų. Jas ir apžvelkime.

## Funkcija `length()`
Tipas `string` su savimi atsineša ir funkciją `length()`, kuri grąžina, kiek simbolių turi tame kintamajame įrašytas simbolių eilutė. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "Labas";
    cout << s.length() << endl; // išspausdins 5
    return 0;
}
{% endhighlight %}

## Palyginimo operatoriai
Simbolių eilutes galima tarpusavyje palyginti (panašiai kaip ir skaičius) naudojantis operatoriais `>`, `<`, `>=`, `<=`, `==` bei `!=`. Operatoriai `==` ir `!=` grąžina `true`, jei lyginamos simbolių eilutės visiškai sutampa (nesutampa). Operatoriai `>`, `<`, `>=` ir `<=` lygina simbolių eilutes abėcėlės tvarka, pradedant nuo pirmo simbolio. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <string>
using namespace std;

int main() {
    string a = "abc";
    string b = "abd";
    cout << (a == b) << endl; // false
    cout << (a != b) << endl; // true
    cout << (a > b) << endl;  // false
    cout << (a < b) << endl;  // true
    cout << (a >= b) << endl; // false
    cout << (a <= b) << endl; // true
    return 0;
}
{% endhighlight %}

## Simbolių eilučių apjungimas
Dvi simbolių eilutes galima sujungti į vieną naują simbolių eilutę naudojant operatorių `+`. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <string>
using namespace std;

int main() {
    string a = "abc";
    string b = "abd";
    string c = a + b;
    cout << c << endl; // abcabd
    return 0;
}
{% endhighlight %}

## Indeksavimas
Kadangi simbolių eilutė iš esmės yra simbolių masyvas, galime su ja elgtis kaip su masyvu - gauti simbolį, esantį tam tikroje pozicijoje, pakeisti simbolį ir pan. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <string>
using namespace std;

int main() {
    string a = "abc";
    cout << a[1] << endl; // b
    a[1] = '!';
    cout << a << endl;    // a!c
    return 0;
}
{% endhighlight %}

## Simbolių eilutės dalies gavimas
`string` pateikia dar vieną labai patogią funkciją: `substr` (nuo žodžio *substring*). Ji iš esamos simbolių eilutės grąžina naują, gautą paėmus simbolius, esančius tam tikrame indeksų intervale. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "Labas rytas";
    string ss = s.substr(6, 5); // pradedant nuo 6 indekso, paima 5 simbolius ir grąžina rezultatą
    cout << ss << endl;         // rytas
    return 0;
}
{% endhighlight %}

