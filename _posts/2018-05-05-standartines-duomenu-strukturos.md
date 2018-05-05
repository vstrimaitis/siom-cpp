---
layout:     lesson
title:      Standartinės duomenų struktūros
date:       2018-05-05 11:58:00
author:     Vytautas Strimaitis
summary:    Šiame skyriuje susipažinsime su standartinėmis C++ duomenų struktūromis
categories: teorija
permalink: /:title/
thumbnail:  tree
iconclass:  fas fa-book
published: true
---
# Kas yra duomenų struktūra
Kompiuterių moksle **duomenų struktūra** - tai būdas laikyti ar grupuoti duomenis taip, kad darbas su jais būtų kiek įmanoma efektyvesnis. Duomenų struktūrų yra labai įvairių. Vienos iš jų geriau tinka vieniems atvejams, kitos kitiems. Šiame skyriuje susipažinsime su keliomis C++ standartinėje bibliotekoje esančiomis naudingomis duomenų struktūromis.

# C++ standartinės duomenų struktūros
Su viena iš standartinių duomenų jau susipažinome anksčiau. Tai - masyvai. Jie tinka tiem atvejam, kuomet iš anksto žinome, kiek bus elementų ir kai mums su jais nereikės atlikti per daug sudėtingų operacijų. Tačiau masyvų ne visada užtenka - būna uždavinių, kuriuose su paprastais masyvai parašyti efektyvų sprendimą tiesiog per sunku ar net neįmanoma. Tokios situacijose praverčia kitos standartinės duomenų struktūros, kurias dabar ir apžvelgsime.

## Dinaminis masyvas (`vector`)
Viena paprastesnių standartinių duomenų struktūrų - dinaminis masyvas. Jis C++ kalboje aprašomas tipu `vector`. Jis nuo paprasto masyvo skiriasi tik vienu dalyku - jo dydžio nereikia nurodyti iš anksto, o dėti elementų galima kiek tik nori - masyvas auga priklausomai nuo elementų kiekio. Norint naudoti dinaminius masyvus savo programoje, reikia įsidėti biblioteką `vector`.

Dinaminis masyvas aprašomas taip: `vector<tipas> pavadinimas`. Vietoje `tipas` reikia įrašyti tokį tipą, kokio bus masyve laikomi elementai. Pavyzdžiui, jei norime susikurti masyvą sveikųjų skaičių, aprašymas būtų `vector<int> skaiciai`.

Į dinaminį masyvą pridėti elementų leidžia funkcija `push_back`. Ji prideda viena naują elementą į masyvo galą. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;  // []
    v.push_back(1); // [1]
    v.push_back(3); // [1, 3]
    v.push_back(2); // [1, 3, 2]
    return 0;
}
{% endhighlight %}

Kaip matome, dinaminis masyvas `v` iš pradžių buvo tuščias, po to į jį iš eilės pridėjome tris elementus, tad pats masyvas prisitaikė ir išaugo iki trijų elementų dydžio.

Dinaminis masyvas pateikia ir dar vieną labai naudingą funkciją `size`, kuri atsako, kiek elementų dabar yra masyve. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;            // []
    v.push_back(1);           // [1]
    v.push_back(3);           // [1, 3]
    v.push_back(2);           // [1, 3, 2]
    cout << v.size() << endl; // 3
    return 0;
}
{% endhighlight %}

Dinaminis masyvas, kaip ir paprastas, leidžia indeksuoti elementus, t.y. pasiekti elementą pagal tam tikrą indeksą arba pakeisti elemento, esančio tam tikru indeksu, reikšmę. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;        // []
    v.push_back(1);       // [1]
    v.push_back(3);       // [1, 3]
    v.push_back(2);       // [1, 3, 2]
    cout << v[0] << endl; // 1
    v[0] = 5;             // [5, 3, 2]

    for(int i = 0; i < v.size(); i++) {
        cout << v[i] << " "; // 5 3 2
    }
    return 0;
}
{% endhighlight %}

Dinaminis masyvas naudingas tuomet, kai iš anksto nežinome, kiek elementų mums reikės saugoti, tačiau vis dar tinka visos paprasto masyvo galimybės.

## Aibė (`set`)
Aibė (angl. *set*) - tai duomenų struktūra, leidžianti greitai įterpti elementus ir laikyti juos taip, kad:
1. Elementai būtų išrikiuoti didėjimo tvarka
2. Visi elementai būtų skirtingi

Šios duomenų struktūros aprašymas toks pats, kaip ir dinaminio masyvo atveju: `set<tipas> pavadinimas`. Norint naudoti aibes, reikia į savo programą įsidėti biblioteką `set`. Elemento pridėjimui į aibę naudojama funkciją `insert`, o dydžiui gauti - `size`. Pavyzdys:

{% highlight c++ %}
#include <iostream>
#include <set>
using namespace std;

int main() {
    set<int> aibe;               // {}
    aibe.insert(1);              // {1}
    aibe.insert(2);              // {1, 2}
    aibe.insert(0);              // {0, 1, 2}
    aibe.insert(1);              // {0, 1, 2}

    cout << aibe.size() << endl; // 3

    return 0;
}
{% endhighlight %}

Kaip matome, aibėje visi elementai visada laikomi išrikiuota tvarka, o bandant įdėti jau egzistuojantį elementą aibė tiesiog nepakinta. Šios savybės labai naudingos uždaviniams, kuomet svarbus elementų unikalumas. Tačiau aibės turi ir vieną didelį minusą - jų negalima indeksuoti kaip masyvų. Taigi, kodas `cout << aibe[0] << endl;` sukeltų kompiliavimo klaidą. Tiesa, iteruoti per aibes įmanoma, tačiau to šioje pamokoje nepaliesime.

## Asociatyvus masyvas (`map`)
Dar viena labai naudinga duomenų struktūra - asociatyvus masyvas. Dažnai būna uždavinių, kuomet atrodytų, kad reikia naudoti masyvą, tačiau kaip indeksą reiktų naudoti arba skaičius, bet nebūtinai nuo 0 ir einančius iš eilės, arba išvis ne skaičius. Tokiose situacijose praverčia asociatyvus masyvai, kuriuos C++ kalboje aprašo tipas `map`. Norint jais naudotis, į savo kodą reikia prisidėti biblioteką `map`. Asociatyvaus masyvo aprašas kiek skiriasi nuo iki šiol matytų duomenų struktūrų. Jis yra toks: `map<rakto_tipas, reiksmes_tipas> pavadinimas`. Kaip matome, dabar jau reikia nurodyti du tipus, o ne vieną. Pirmasis tipas (`rakto_tipas`) nurodo, kokio tipo bus šio asociatyvaus masyvo indeksai, o antrasis (`reiksmes_tipas`) - kokio tipo reikšmes laikysime.

Panagrinėkime pavyzdį. Tarkime, kad mums reikia parašyti programą, kuriai bus įvedama kažkiek simbolių, o mes norime atsakyti, kiek kartų matėme simbolį `'a'`. Tokį uždavinį spręstų ši programa:

{% highlight c++ %}
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<char, int> kiek; // raktas bus simbolis, o reikšmė - skaičius, nurodantis, kiek kartų ši simbolį matėme
    char c;
    while(cin >> c) { // skaitome po vieną simbolį iki galo
        kiek[c]++;    // pasižymime, kad šį simbolį matėme dar vieną kartą
    }
    cout << kiek['a'] << endl; // išspausdiname, kiek kartų matėme simbolį 'a'
    return 0;
}
{% endhighlight %}

Asociatyvūs masyvai tikriausiai yra viena iš naudingiausių standartinių duomenų struktūrų. Juos dažniausiai vertėtų naudoti tuomet, kai atrodytų, kad užtektų masyvo, tačiau netinka įprasti indeksai, kurie tiktų masyvams.
