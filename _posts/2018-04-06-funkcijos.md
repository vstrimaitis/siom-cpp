---
layout:     lesson
title:      Funkcijos
date:       2018-04-06 00:25:00
author:     Vytautas Strimaitis
summary:    Šis skyrius skirtas susipažinti su funkcijomis C++ programavimo kalboje.
categories: teorija
permalink: /:title/
thumbnail:  function
---
# Funkcijos
Šis skyrius skirtas susipažinti su **funkcijomis** C++ programavimo kalboje.

## Kas yra funkcija programavime?
Dažnai rašant programas (ypač sudėtingesnes) gali prireikti tam tikrą kodą perpanaudoti arba paskaidyti į mažesnes, lengviau suprantamas dalis. Tokiose situacijose praverčia **funkcijos**. Funkcija programavime - tai kodo blokas, atliekantis kažkokį darbą. Pavyzdžiui, C++ standartinėje bibliotekoje turi funkciją `max`, kuri priima du skaičius ir grąžina didesnį iš jų. Panagrinėkime dvi programas, kurios nuskaito du skaičius ir išspausdina didesnį iš jų:

{% highlight c++ %}
int a, b;
cin >> a >> b;
if(a > b) {
    cout << a << endl;
} else {
    cout << b << endl;
}
{% endhighlight %}

{% highlight c++ %}
int a, b;
cin >> a >> b;
cout << max(a, b) << endl;
{% endhighlight %}

Akivaizdu, kad antroji programa yra trumpesnė, ją lengviau parašyti bei suprasti, ką kodas daro. O jei tokį palyginimą reikėtų atlikti daugelyje programos vietų ir nenaudotume funkcijos `max`, tai programos kodas labai greitai taptų nesuvaldomas.

Funkcija `max`, kaip minėta, yra dalis C++ standartinės bibliotekos, tad ją galime tiesiog naudoti programuodami. Tačiau programuojant ne visada patogu naudotis vien standartinėmis funkcijomis. Tokiais atvejais galima susikurti savo funkciją ir ją naudoti lygiai taip pat, kaip standartines.

## Kaip sukurti savo funkciją?
C++ kalboje savo funkciją galima sukurti taip:

{% highlight c++ %}
tipas pavadinimas(tipas parametras1, tipas parametras2, ...){
    // kodas
}
{% endhighlight %}

Kiekviena funkcija privalo turėti šias dalis:
* **Pavadinimas**. Tai vardas, kuriuo naudojantis kviesima funkciją likusiame kode.
* **Parametrai** (arba **argumentai**). Jie nurodomi tarp paprastų skliaustų `(` ir `)`. Kiekvienas iš jų turi turėti tipą ir pavadinimą.
* **Grąžinamas tipas** rašomas prieš funkcijos vardą. Jis nurodo, kokio tipo reikšmę funkcija *grąžins*.

Pavyzdžiui, jau minėta funkcija `max` galėtų būti aprašyta taip:

{% highlight c++ %}
int max(int a, int b) {
    if(a > b) {
        return a;
    } else {
        return b;
    }
}
{% endhighlight %}

Šios funkcijos **vardas** yra `max`, ji priima du **parametrus** - sveikuosius skaičius `a` ir `b`, o **grąžina** taip pat sveikąjį skaičių.

Dar vienas dalykas, kuris liko nepaminėtas, tai raktažodis `return`. Jis naudojamas funkcijos viduje, kuomet norima nurodyti, **ką** funkcija gražina. Šiuo atveju, jei `a > b`, tai funkcija grąžina reikšmę `a`, o kitu atveju - `b`. Raktažodis `return` turi vieną savybę - kodas, esantis funkcijos viduje, ir einantis po `return` **nėra vykdomas**. Pavyzdžiui, šį kodą būtų galima perrašyti taip:

{% highlight c++ %}
int max(int a, int b) {
    if(a > b) {
        return a;
    }
    return b;
}
{% endhighlight %}

Atrodytų, kad kodas `return b;` bus įvykdytas bet kuriuo atveju, tačiau jei `a > b`, tai bus pasiektas kodas `return a`, tad toliau esantis kodas nebebus vykdomas. Šio "triuko" žinojimas dažnai leidžia kodą sutrumpinti, tačiau prie tokio programavimo stiliaus reikia priprasti.

## Procedūros
Tam tikros funkcijos dar būna vadinamos **procedūromis**. Procedūra - tai funkcija, kuri nieko negrąžina. Tokia funkcija turi specialų grąžinamą tipą - `void`. Tarkime norime parašyti funkciją, kuri paprašo vartotojo įvesti vieną sveikąjį skaičių ir išspausdina jį, bet padaugintą iš dviejų. Tokia funkcija galėtų atrodyti taip:

{% highlight c++ %}
void idomiFunkcija() {
    int a;
    cin >> a;
    cout << 2*a << endl;
}
{% endhighlight %}

Kaip matome, ši funkcija nepriima nė vieno parametro, o jos grąžinamas tipas yra `void`. Vadinasi, ši funkcija nieko negrąžina, tad ji dar gali būti vadinama procedūra.

## Kaip naudotis funkcijomis?
Kol kas išmokome tik apsirašyti savo funkcijas, tačiau jos mums nenaudingos, kol iš tikro jų nepanaudojame. Funkcijos "panaudojimas" dažniausiai vadinamas **funkcijos kvietimu**. Funkcija kviečiama nurodant jos vardą bei parametrus, nurodomus skliaustuose. Pavyzdžiui, jau matytą funkciją `max` galima iškviesti parašius `int c = max(2, 5);`. Šiuo atveju, funkcijos parametrai yra skaičiai `2` ir `5`, funkcija grąžins reikšmę `5` ir ji bus įrašyta į kintamąjį `c`.

Kviečiant procedūras, kadangi jos nieko negrąžina, negalima bandyti funkcijos reikšmės priskirti kokiam nors kintamajam. Pavyzdžiui, tarkime esame apsirašę jau anksčiau minėtą funkciją `idomiFunkcija`. Ją kviesti galima taip: `idomiFunkcija()`, bet ne taip: `int blogai = idomiFunkcija()` ir ne taip: `idomiFunkcija(5)`. Skliaustuose visada privaloma perduoti būtent tiek parametrų, kiek funkcijas *prašo* (t.y. kaip nurodyta jos apraše), o reikšmę galima priskirti kintamajam tik tada, jei funkcija nėra `void`.

## Kur rašyti funkcijas?
Rašant funkcijas yra vienas "kabliukas" - jas reikia rašyti tokioje programos vietoje, kad visi funkcijos kvietimas būtų **žemiau**. Tarkime turime tokį kodą:

{% highlight c++ %}
int main() {
    idomiFunkcija();
    cout << "Baigiau" << endl;
    return 0;
}

void idomiFunkcija() {
    int a;
    cin >> a;
    cout << 2*a << endl;
}
{% endhighlight %}

Pirmoje `main` eilutėje bandome kviesti funkciją `idomiFunkcija`, tačiau ji kol kas dar nebuvo aprašyta (nes jos aprašas yra žemiau), tad programa nesikompiliuos. Pataisyti šią programą galima taip:

{% highlight c++ %}
void idomiFunkcija() {
    int a;
    cin >> a;
    cout << 2*a << endl;
}

int main() {
    idomiFunkcija();
    cout << "Baigiau" << endl;
    return 0;
}
{% endhighlight %}

Dabar bandant kviesti funkciją `idomiFunkcija`, ji jau yra aprašyta aukščiau, todėl viskas veiks taip, kaip tikimės.

## `main` irgi atrodo kaip funkcija. Ar taip ir yra?
Taip, mūsų jau daugybę kartų matytas `main` taip pat yra funkcija, tik ji yra ypatinga. Tai funkcija, kuri yra kviečiama paleidus programą. Galima pastebėti, kad jos grąžinamas tipas yra `int`, o gale visuomet rašome `return 0;`. Taip daroma ne be reikalo - funkcijos `main` grąžinama reikšmė nurodo, ar programa baigė darbą sėkmingai, ar kažkas "nulūžo". Kodas `0` reiškia, kad programa baigė darbą be jokių trikdžių (todėl ir rašome `return 0`!). Įvykus klaidai, būna grąžinamas kodas, nelygus nuliui.

## Pavyzdžiai
Toliau pateikiami keli programų pavyzdžiai, kad būtų lengviau suprasti funkcijų aprašymo ir naudojimo sintaksę:

### Išspausdinti didžiausią iš trijų skaičiu

{% highlight c++ %}
int max3(int a, int b, int c) {
    return max(a, max(b, c)); // panaudojame standartinę C++ funkciją max
}

int main() {
    int s1, s2, s3;
    cin >> s1 >> s2 >> s3;
    cout << max3(s1, s2, s3) << endl;
    return 0;
}
{% endhighlight %}

### Funkcijų panaudojimas nuskaitymui ir įrašymui

{% highlight c++ %}
int skaityk() {
    int a;
    cin >> a;
    return a;
}

void spausdink(int skaicius) {
    cout << skaicius << endl;
}

int main() {
    int ivestis = skaityk();
    spausdink(ivestis);
    return 0;
}
{% endhighlight %}

### Stačiakampio "piešimas"

{% highlight c++ %}
// Ši funkcija atsakinga už vienos stačiakampio eilutės spausdinimą
void spausdinkEilute(int ilgis) {
    for(int i = 0; i < ilgis; i++) {
        cout << "*";
    }
    cout << endl;
}

// Ši funkcija atsakinga už viso stačiakampio spausdinimą
void spausdinkStaciakampi(int a, int p) {
    for(int i = 0; i < a; i++) {
        spausdinkEilute(p); // a kartų spausdiname eilutę, kurios dydis p
    }
}

int main() {
    int aukstis, plotis;
    cin >> aukstis >> plotis; // iveda du skaičius - stačiakampio plotį ir aukštį
    spausdinkStaciakampi(aukstis, plotis);
    return 0;
}
{% endhighlight %}
