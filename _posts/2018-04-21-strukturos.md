---
layout:     lesson
title:      Struktūros
date:       2018-04-20 15:13:00
author:     Vytautas Strimaitis
summary:    Šiame skyriuje išmoksime, kas yra struktūros ir kaip jomis naudotis.
categories: teorija
permalink: /:title/
thumbnail:  curly
iconclass:  fas fa-book
published: true
---
# Struktūros
C++ kalboje yra nemažai bazinių, o visoje standartinėje bibliotekoje - ir gana sudėtingų tipų. Tačiau būna atvejų, kuomet jų nepakanka. Tokiose situacijose galima pasinaudoti **struktūromis** - C++ kalbos dalimi, leidžiančia apsirašyti savo duomenų struktūras ir jas naudoti kaip bet kurį kitą tipą.

## Problema
Tarkime, sprendžiame uždavinį, kuriame mums pateikiamas sąrašas iš `N` taškų su tam tikromis koordinatėmis, o mums reikia atrinkti tik tokius taškus, kurių abi koordinatės yra griežtai mažesnės už tam tikrą skaičių `C`. Vienas galimas šio uždavinio sprendimas būtų toks:

{% highlight c++ %}
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n; // nuskaitome taškų kiekį
    int x[n], y[n]; // susikuriame du masyvus - vienas laikys taškų x koordinates, o kitas - y
    for(int i = 0; i < n; i++) { // nuskaitome n taškų
        cin >> x[i] >> y[i];
    }
    int c;
    cin >> c; // nuskaitome sąlygoje paminėtą skaičių C
    for(int i = 0; i < n; i++) {
        if(x[i] < c && y[i] < c) { // jei abi taško koordinatės mažesnės už c, spausdiname šį tašką
            cout << x[i] << " " << y[i] << endl;
        }
    }
    return 0;
}
{% endhighlight %}

Uždavinio sprendimas atrodo gan paprastas, tačiau už akies gali užkliūti viena detalė - taškams laikyti mums prireikė dviejų masyvų. Kadangi taškas yra viena esybė (tik sudaryta iš dviejų skaičių poros), norėtųsi ir masyvą turėti vieną, kur kiekvienas elementas aprašytų vieną tašką. Čia į pagalbą ateina struktūros.

## Kas yra struktūra
C++ kalba leidžia apsirašyti savus duomenų tipus, vadinamus struktūromis. Aprašymo sintaksė yra tokia:

{% highlight c++ %}
struct Pavadinimas {
    tipas narys1;
    tipas narys2;
    ...
    tipas narysN;
}
{% endhighlight %}

Kaip matome, kiekviena struktūra yra sudaryta iš **narių** - kintamųjų arba funkcijų. O pati struktūra - tai tarsi grupė, jungianti tuos narius į vieną esybę. Pavyzdžiui, jau minėtą taško esybę būtų galima aprašyti taip:

{% highlight c++ %}
struct Taskas {
    int x;
    int y;
}
{% endhighlight %}

Iš šio pavyzdžio matome, kad taškas - tai esybė, turinti du **narius** - `x` ir `y` koordinates.

Po to, kai apsirašėme struktūrą, galime ją naudoti kaip bet kokį kitą duomenų tipą. Pavyzdžiui, galime susikurti kintamąjį, kurio tipas yra `Taskas`:

{% highlight c++ %}
Taskas t;
{% endhighlight %}

Struktūros tipo kintamųjų narių reikšmės galima pasiekti naudojant *taško* (`.`) operatorių. Taigi, jei norime nurodyti, kad taško `t` koordinatės yra `(4, 6)`, galime parašyti taip:

{% highlight c++ %}
Taskas t;
t.x = 4;
t.y = 6;
{% endhighlight %}

Lygiai taip pat galime narių reikšmes ir nuskaityti. Pavyzdžiui, jei norėtume šį tašką išvesti į konsolę, galėtume rašyti tokį kodą:

{% highlight c++ %}
cout << t.x << " " << t.y << endl;
{% endhighlight %}

Struktūros nariai gali būti ne tik paprasti kintamieji - ten galima rašyti ir funkcijas. Papildykime savo struktūrą `Taskas` pridėdami funkciją `bool arLygus(Taskas kitas)`, kuri pasakytų, ar šis taškas yra lygus kažkokiam kitam taškui:

{% highlight c++ %}
struct Taskas {
    int x;
    int y;

    bool arLygus(Taskas kitas) {
        return x == kitas.x && y == kitas.y;
    }
}
{% endhighlight %}

Šią funkciją galima panaudoti taip:

{% highlight c++ %}
Taskas a, b, c;
a.x = 4;
a.y = 6;

b.x = 4;
b.y = 7;

c.x = 4;
c.y = 6;

if(a.arLygus(b)) {
    cout << "a ir b lygus" << endl;
}
if(a.arLygus(c)) {
    cout << "a ir c lygus" << endl;
}
{% endhighlight %}

Šis kodo gabaliukas išspausdintų `a ir c lygus`, nes taškų `a` ir `c` koordinatės sutampa.

## Uždavinio sprendimas su struktūromis
Išspręskime skyrelio pradžioje nagrinėtą uždavinį pasinaudodami struktūromis. Sprendimo kodas:

{% highlight c++ %}
#include <iostream>
using namespace std;

// Apsirašome struktūrą, kurią sudaro du sveikieji skaičiai x ir y - taško koordinatės, bei funkcija
// bool arTinkamas(int c), nurodanti, ar šio taško abi koordinatės mažesnės už nurodytą skaičių c.
struct Taskas {
    int x;
    int y;

    bool arTinkamas(int c) {
        return x < c && y < c;
    }
}

int main() {
    int n;
    cin >> n; // nuskaitome taškų kiekį
    Taskas taskai[n]; // dabar jau turėsime tik vieną masyvą laikyti taškams
    for(int i = 0; i < n; i++) { // nuskaitome n taškų
        cin >> taskai[i].x >> taskai[i].y;
    }
    int c;
    cin >> c; // nuskaitome sąlygoje paminėtą skaičių C
    for(int i = 0; i < n; i++) {
        if(taskai[i].arTinkamas(c)) { // jei dabartinis taškas tenkina sąlygą, tai jį spausdiname
            cout << taskai[i].x << " " << taskai[i].y << endl;
        }
    }
    return 0;
}
{% endhighlight %}

## Apibendrinimas
Nors daugelį uždavinių įmanoma išspręsti naudojant vien primityvius duomenų tipus, struktūros dažnai palengvina programuotojo darbą. Šiame uždavinyje, kaip matėme, buvo galima išsiversti be struktūrų gana nesunkiai, tačiau jei uždavinį kiek pakeistume - būtų gerokai sunkiau.

Tarkime, kad dabar vėl gauname sąrašą taškų, tačiau dabar juos norime išrikiuoti pagal `x` koordinatę, o jei `x` koordinatės lygios - pagal `y` koordinatę. Šį uždavinį išspręsti be struktūrų būtų tikrai nemažas galvos skausmas, tačiau naudojantis struktūromis jis beveik nesiskiria nuo jau matyto skaičių rikiavimo.

Sprendimo idėja - apsirašyti struktūrą, laikančią taško koordinates ir turinčią funkciją `bool arMazesnisUz(Taskas kitas)`, kuri atsakytų, ar šis taškas yra mažesnis už tašką `kitas` (palygina pagal `x` koordinates, jei jos nelygios, ir pagal `y`, jei lygios). Tada, turint tokių taškų masyvą galima nesunkiai tarpusavyje palyginti du taškus, o tai leidžia ir turimą masyvą išrikiuoti.