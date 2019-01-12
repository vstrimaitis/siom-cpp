---
layout:     lesson
title:      Patarimai olimpiadoms
date:       2019-01-11 19:55:00
author:     Vytautas Strimaitis
summary:    Šiame skyriuje pateikiami keli patarimai olimpiadoms
categories: teorija
permalink: /:title/
thumbnail:  info
iconclass:  fas fa-info-circle
published: true
---
**Pastaba.** Čia sudėti tik mano nuomone svarbiausi C++ "triukai" ir pavyzdžiai.
Daugiau galima paskaityti [čia](https://codeforces.com/blog/entry/15643) arba
paieškojus Google :). Šiame puslapyje bus aptariama:

- [\#define](#define)
- [typedef](#typedef)
- [cin ir cout pagreitinimas](#cin-ir-cout-pagreitinimas)
- [endl prieš "\n"](#endl-prieš-n)
- [Viena biblioteka visoms gyvenimo reikmėms](#viena-biblioteka-visoms-gyvenimo-reikmėms)
- [Naudingi C++11 dalykai](#naudingi-c11-dalykai)
  - [C++11 įjungimas per Code::Blocks](#c11-įjungimas-per-codeblocks)
  - [Raktažodis auto](#raktažodis-auto)
  - [Naujas for ciklas](#naujas-for-ciklas)
- ["algorithm" biblioteka](#algorithm-biblioteka)
  - [max ir min](#max-ir-min)
  - [swap](#swap)
  - [sort](#sort)
  - [reverse](#reverse)
  - [fill](#fill)
  - [next_permutation](#next_permutation)
- [Standartinės duomenų struktūros](#standartinės-duomenų-struktūros)
  - [pair](#pair)
  - [vector](#vector)
  - [set](#set)
  - [map](#map)
  - [queue](#queue)
  - [stack](#stack)
  - [deque](#deque)
  - [priority_queue](#priority_queue)
- [Dvejetainė paieška](#dvejetainė-paieška)
  - [Paieška vektoriuje](#paieška-vektoriuje)
  - [Paieška aibėje bei asociatyviame masyve](#paieška-aibėje-bei-asociatyviame-masyve)

# \#define
`#define` - C++ preprocesoriaus komanda, leidžianti pakeisti vienas kodo
dalis kitomis. Sintaksė:

{% highlight c++ %}
#define A B
{% endhighlight %}

Paprastai tariant, parašius šią eilutę savo programoje, C++ kompiliavimo metu
suras visas kodo vietas, kur yra parašyta `A`, ir vietoj jų įrašys `B`. Galimas panaudojimo pavyzdys:

{% highlight c++ %}
#include <iostream>
#define pb push_back
using namespace std;

int main() {
    vector<int> v;
    v.pb(5); // bus pakeista į v.push_back(5)
}
{% endhighlight %}

Taip pat naudojant `#define` galima aprašyti tam tikras pagalbines funkcijas.
Pavyzdžiui:

{% highlight c++ %}
#include <iostream>
#include <iomanip>
#define precise(x) fixed << setprecision(x)
#define sgn(x) ((a) > 0 ? 1 : (a) < 0 ? -1 : 0)
#define FOR(i, begin, end) for(int i = (begin); i < (end); i++)
using namespace std;

int main() {
    vector<int> v;
    v.pb(5);                            // bus pakeista į v.push_back(5)
    v.pb(0);                            // bus pakeista į v.push_back(0)
    v.pb(-1);                           // bus pakeista į v.push_back(-1)
    FOR(i, 0, 3) {                      // bus pakeista į for(int i = 0; i < 3; i++)
        cout << sgn(v[i]) << endl;      // bus pakeista į ((v[i]) > 0 ? 1 : (v[i]) < 0 ? -1 : 0)
    }
    double pi = 3.14159265;
    cout << precise(2) << pi << endl;   // bus pakeista į cout << fixed << setprecision(2) << pi << endl;
}
{% endhighlight %}

Dažniausiai olimpiadose `#define` naudojamas būtent sutrumpinti dažnai pasitaikančius kodo gabalus, kad sprendimą būtų galima parašyti gerokai greičiau.


# typedef
Komanda `typedef` naudojama apibrėžti naujiems tipams. Olimpiadose tai dažniausiai tiesiog būdas trumpinti kodą, tačiau, skirtingai nuo `#define`, šis būdas naudojamas **tik naujų tipų įvedimui**. Sintaksė:

{% highlight c++ %}
typedef senas_tipas naujas_tipas;
{% endhighlight %}

Naudingi pavyzdžiai:

{% highlight c++ %}
#include <iostream>
using namespace std;
typedef long long ll;
typedef long double ld;
typedef pair<int, int> pii;
typedef pair<ll, ll> pll;

int main() {
    ll a = 10000000000LL;   // vietoj long long a = ...
    ld b = 1.05;            // vietoj long double b = ...
    pii c = {1, 2};         // vietoj pair<int, int> c = ...
    map<pii, set<pll>> d;   // vietoj map<pair<int, int>, set<pair<long long, long long>>> d
}
{% endhighlight %}

# cin ir cout pagreitinimas
C++ įprastos funkcijos `cin` ir `cout` yra patogios darbui su konsole, tačiau
turi tam tikrų problemų. Jei įvesties ir/ar išvesties kiekis yra didelis, šios
funkcijos gali būti gana lėtos. Tačiau tai gali būti pataisyta `main` funkcijos pradžioje prirašant šias eilutes:

{% highlight c++ %}
ios_base::sync_with_stdio(false);
cin.tie(nullptr); // veiks tik tada, jei esate įsijungę C++11 režimą
// kitu atveju naudoti: cin.tie(NULL);
{% endhighlight %}

Taip pat galima ir išnaudoti jau aptartą `#define` raktažodį:

{% highlight c++ %}
#include <iostream>
using namespace std;
#define FAST_IO ios_base::sync_with_stdio(false); cin.tie(nullptr)

int main() {
    FAST_IO;
    // kodas...
}
{% endhighlight %}

# endl prieš "\n"
Išvedant duomenis į konsolę su `cout` yra įprasta naudoti `endl` raktažodį, kai
norima padėti eilutės pabaigos simbolį. C++, kaip ir daugelyje programavimo
kalbų, išvedimas į konsolę vyksta maždaug taip: duomenys po truputį yra kaupiami
atmintyje (taip vadinamame buferyje) ir kartas nuo karto išvedami į konsolę
vienu ypu (ši operacija vadinama *flush*). Tai padeda paspartinti programos
veikimą, nes išvedimas į konsolę yra gerokai brangesnė operacija, negu duomenų
įrašymas į atmintį. Deja, `endl` naudojimas ne tik spausdina naują eilutę,
tačiau ir iškart įvykdo *flush* operaciją, todėl programos veikimas gali
sulėtėti. Taigi, kuomet duomenų gali tekti išvesti daug, vietoj `endl` verta
naudoti `"\n"`, nes šiuo atveju kiekvienąkart nebus vykdoma *flush* operacija.
Vadinasi, `cout << "Labas" << endl;` keisime į `cout << "Labas" << "\n";`.

# Viena biblioteka visoms gyvenimo reikmėms
Galbūt jau teko pastebėti, kad sprendžiant uždavinius, kuriems reikia daug
įvairiausių bibliotekų, programos `#include` sąrašas gana greitai išsipučia.
Laimei, yra viena biblioteka, kurios viduje yra visos kitos, kokių tik gali
prireikti olimpiadose. Norint ją naudoti užtenka visus turimus `#include`
sakinius pakeisti į vieną:

{% highlight c++ %}
#include <bits/stdc++.h>
using namespace std;

int main() {
    // ...
}
{% endhighlight %}

Tiesa, ši biblioteka neveikia visose aplinkose, nes jai reikia būtent GCC
kompiliatoriaus, tačiau Code::Blocks šį kompiliatorių naudoja kaip numatytąjį.

# Naudingi C++11 dalykai
Nuo C++ 11 versijos kalboje atsirado nemažai naudingų dalykų, paspartinančių
kodo rašymą bei palengvinančių skaitomumą. Čia aptarsime keletą iš jų.

## C++11 įjungimas per Code::Blocks
1. Viršutiniame meniu rinkitės `Settings -> Compiler`.
2. Atsidariusiame lange pasirinkite skiltį `Compiler settings`, o joje - `Compiler Flags`.
3. Spustelėkite dešinį pelės mygtuką ant bet kurios eilutės, pasirinkite `New flag...`
4. Atsidariusiame lange užpildykite tokią informaciją:
   1. Name: `Enable C++11 flag`
   2. Compiler flags: `-std=c++11`
   3. Category: `Warnings`
   4. Supersedes: `-std=c++98 -std=c++0x`
5. Spustelėkite `OK`
6. Įsitikinkite, kad prie naujai pridėtos eilutės (su pavadinimu `Enable C++11 flag [-std=c++11]`) yra pažymėta varnelė.
7. Pasirinkite skiltį `Toolchain executables`.
8. Čia įsitikinkite, kad yra pasirinktas būtent Code::Blocks pateikiamas
   kompiliatorius (`Compiler's installation directory` rodo į, pavyzdžiui, `C:\Codeblocks\MinGW`).

## Raktažodis auto
Senesnėse C++ versijose šalia kintamojo visada buvo privaloma rašyti ir jo tipą.
Nuo C++11 versijos atsirado naujas raktažodis `auto`, kuri galima naudoti vietoj
kintamojo tipo, kuomet tipą gali nustatyti pats kompiliatorius automatiškai.
Pavyzdys:

{% highlight c++ %}
vector<string> v = {"a", "b", "c"};
string s1 = v[0];    // senas būdas
auto s2 = v[0];      // naujas būdas - kompiliatorius pats žino, kad s1 tipas yra string, tad mums nebūtina jo nurodyti
{% endhighlight %}

Dar vienas pavyzdys, kuriame akivaizdžiai atsispindi `auto` nauda:

{% highlight c++ %}
set<pair<int, pair<int, int>>> funkcija() {
    // ... kažką daro ir grąžina reikšmę
}

int main() {
    set<pair<int, pair<int, int>>> rez1 = funkcija();   // senas būdas
    auto rez2 = funkcija();                             // naujas būdas
}
{% endhighlight %}

## Naujas for ciklas
C++11 versijoje atsirado naujas būdas rašyti `for` ciklus. Jo sintaksė tokia:

{% highlight c++ %}
for(tipas elementas : kolekcija)
{% endhighlight %}

Čia `kolekcija` gali būti bet koks **iteruojamas** objektas (masyvas, `vector`,
`set`, `map` ir t.t.). Konkretus pavyzdys:

{% highlight c++ %}
vector<int> v;
// užpildome reikšmėmis
for(int x : v) {
    cout << x << endl;
}
{% endhighlight %}

Taip pat čia galime panaudoti ir jau aptartą `auto` raktažodį:

{% highlight c++ %}
vector<pii> v;
// užpildome reikšmėmis
for(auto x : v) {
    // x tipas yra pair<int, int>
    cout << x.first << " " << x.second << endl;
}
{% endhighlight %}

# "algorithm" biblioteka
Viena itin naudinga C++ pateikiama standartinė biblioteka - `<algorithm>`. Joje
galima rasti nemažai naudingų funkcijų, kurias galima panaudoti, kad nereiktų
rašytis patiems ir gaišti laiko bei rizikuoti padaryti klaidų. Toliau aptarsime
kelis pavyzdžiui.

## max ir min
Šios funkcijos priima du parametrus ir grąžina didesnį (arba mažesnį) iš jų.
Pavyzdys:

{% highlight c++ %}
int a = 5;
int b = 9;
int mx = max(a, b); // mx = 9
int mn = min(a, b); // mn = 5
{% endhighlight %}

## swap
Ši funkcija priima du parametrus ir sukeičia jų reikšmes vietomis. Pavyzdys:

{% highlight c++ %}
string a = "Laba";
string b = "Diena";
swap(a, b);
cout << a << " " << b << endl; // Diena Laba
{% endhighlight %}

## sort
Ši funkcija išrikiuoja nurodytą intervalą duomenų. Sintaksė: `sort(begin, end,
cmp)`, čia `begin` - nuoroda į rikiuojamų duomenų pradžią, `end` - nuorodą į
rikiuojamų duomenų pabaigą, `cmp` - funkcija, nusakanti rikiavimo tvarką (jei ši
funkcija nenurodyta, tai numatytas rikiavimo būdas yra didėjimo tvarka).
Pavyzdys:

{% highlight c++ %}
bool mazejimoTvarka(char a, char b) {
    return a > b;
}
// ...

vector<int> v = {1, 5, 3};
sort(v.begin(), v.end()); // v = {1, 3, 5}

char mas[] = {'c', 'a', 'b'};
sort(mas, mas+3); // mas = {'a', 'b', 'c'}

string s = "raides";
sort(s.begin(), s.end(), mazejimoTvarka); // s = "srieda"
{% endhighlight %}

**Pastaba.** Standartinių duomenų struktūrų pradžios ir pabaigos nuorodos gali
būti pasiekiamos naudojant `.begin()` ir `.end()` funkcijas, o masyvų: `mas` ir
`mas+n`, kur `mas` - masyvo pavadinimas, o `n` - jo dydis.

## reverse
Ši funkcija apsuka duomenis pagal duotas pradžios iš pabaigos nuorodas.
Sintaksė: `reverse(begin, end)`. Pavyzdys:

{% highlight c++ %}
vector<int> v ={1, 5, 6, 3};
reverse(v.begin(), v.end());
//v = {3, 6, 5, 1}
{% endhighlight %}

## fill
Ši funkcija užpildo nurodytą duomenų intervalą viena reikšme. Sintaksė:
`fill(begin, end, val)`. Pavyzdys:

{% highlight c++ %}
int mas[100];
fill(mas, mas+100, 5);
// mas = {5, 5, 5, ..., 5}
{% endhighlight %}

## next_permutation
Ši funkcija priima nuorodas į duomenų rinkinį (pvz. masyvą) ir pakeičia jį taip,
kad būtų gautas kitas (pagal leksikografinę tvarką) išdėstymas. Pavyzdžiui,
sąrašo `[1, 2, 3]` kitas galimas išdestymas yra `[1, 3, 2]`, o dar kitas - 
`[2, 1, 3]`. Funkcija grąžina `true`, jei gautas išdestymas dar nėra paskutinis
galimas, ir `false` kitu atveju. Dažniausiai ši funkcija naudojama norint
sugeneruoti duomenų rinkinio visas įmanomas *permutacijas* (t.y. išdėstymus).
Pavyzdys:

{% highlight c++ %}
vector<int> v = {1, 2, 3};
do {
    for(auto x : v) cout << x << " ";
    cout << endl;
} while(next_permutation(v.begin(), v.end()));
/*
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
*/
{% endhighlight %}

**Pastaba.** Prieš vykdant tokio tipo ciklą įsitikinkite, kad duomenys
**išrikiuoti didėjimo tvarka**, nes kitaip `next_permutation` nesugeneruos visų
galimų išdėstymų (čia grėblys, ant kurio labai skaudžiai teko užlipti pačiam :) ).

# Standartinės duomenų struktūros
Duomenų struktūros - vienas kertinių akmenų daugelio uždavinių sprendime. Geras
jų išmanymas dažnai uždavinio sprendimą gali sutrumpinti kelis (jei ne
keliasdešimt) kartų, o kai kurių uždavinių be jų išspręsti išvis neįmanoma. C++
standartinė biblioteka pateikia gausybę įvairių duomenų struktūrų, kurių geras
įvaldymas kai kurių uždavinių sprendimo laiką gali sutrumpinti nuo valandos iki
vos kelių minučių.

Kelių svarbiausių standartinių duomenų struktūrų pagrindai yra aptariami
[čia]({{ site.baseurl }}{% post_url 2018-05-05-standartines-duomenu-strukturos
%}). Šiame skyriuje pažvelgsime į jau aptartas duomenų struktūras kiek įdėmiau,
taip pat aptarsime ir dar daugiau naudingų duomenų struktūrų.

## pair
Tai - ne visai tokios pat rūšies duomenų struktūra kaip kitos, aptariamos šiame
skyriuje, tačiau `pair` dažnai būna naudojama kartu su kitomis struktūromis, tad
verta aptarti jos panaudojimą. Tipo aprašas: `pair<T1, T2>`. Iš esmės `pair`
leidžia saugoti dvi reikšmes viename kintamajame (pirmosios tipas `T1`,
antrosios - `T2`). Pavyzdžiui, jei sprendžiame uždavinį, kuriame reikia dirbti
su taškų koordinatėmis, turime du sprendimo būdus. Pirmas būtų susikurti savo
struktūrą. Sprendimas atrodytų taip:

{% highlight c++ %}
struct Point {
    int x, y;
};

int main() {
    int n; cin >> n;
    vector<Point> points(n); // sukuria n dydžio vektorių
    for(int i = 0; i < n; i++) {
        cin >> points[i].x >> points[i].y;
    }
    // kažką darom su nuskaitytais taškais...
}
{% endhighlight %}

Kitas būdas yra išnaudoti `pair`:

{% highlight c++ %}
int main() {
    int n; cin >> n;
    vector<pair<int, int>> points(n); // sukuria n dydžio vektorių
    for(int i = 0; i < n; i++) {
        cin >> points[i].first >> points[i].second;
    }
    // kažką darom su nuskaitytais taškais...
}
{% endhighlight %}

Pirmasis būdas yra skaitomesnis, tačiau antrasis aprašomas trumpiau ir greičiau.
Kadangi olimpiadose greitis yra itin svarbu, tai įprastai antras būdas būtų
laikomas geresniu. Žinoma, jei skaitomų duomenų struktūra yra sudėtingesnė, o ne
tik dvi reikšmės, tuomet verta mąstyti apie `struct` naudojimą, tačiau šiuo
atveju tai neapsimoka.

Įdomumo dėlei, štai kaip galėtų atrodyti tas pats kodo pavyzdys išnaudojant jau
aptartus "triukus":

{% highlight c++ %}
typedef pair<int, int> pii;

int main() {
    int n; cin >> n;
    vector<pii> v(n);   // sukuria n dydžio vektorių
    for(auto& x : v) {  // & reiškia, kad iteravimo metu galime keisti x reikšmę
        cin >> x.first >> x.second;
    }
}
{% endhighlight %}

## vector
`vector` yra gana paprasta ir dažnai naudojama duomenų struktūra. Tai iš esmės
yra tas pats, kaip ir paprastas masyvas, tik yra vienas esminis skirtumas -
`vector` dydžio iš anksto nebūtina apibrėžti, jis gali kisti laikui bėgant.
Pagrindinės `vector` palaikomos funkcijos:

* `.push_back(x)` - pridėti reikšmę `x` į vektoriaus galą;
* `.pop_back()` - išimti paskutinę reikšmę iš vektoriaus;
* `.front()` - grąžina vektoriaus priekyje esančią reikšmę;
* `.back()` - grąžina vektoriaus gale esančią reikšmę;
* `.assign(n, val)` - pakeičia vektoriaus dydį į `n` ir visą jį užpildo reikšmę `val`;
* `.resize(n)` - pakeičia vektoriaus dydį į `n`.

Taip pat `vector` palaiko funkcijas, kurias palaiko beveik visos kitos
standartinės duomenų struktūros (toliau jos bus vadinamos standartinėmis
funkcijomis):

* `.size()` - grąžina vektoriuje esančių elementų kiekį;
* `.empty()` - `true`, jei vektorius tuščias, `false` kitu atveju;
* `.clear()` - išvalo vektorių (t.y. ištrina visus elementus).

Pagrindinės operacijos `push_back` ir `pop_back` abi veikia per `O(1)` laiko.
Taigi, elementų pridėjimas į galą bei išėmimas iš galo vektoriuje yra itin
greita operacija. Taip pat, vektorių galima indeksuoti taip pat, kaip ir masyvą
(t.y. galima rašyti `v[1]` norint gauti antrąjį elementą). Indeksavimo
sudėtingumas taip pat yra `O(1)`.

## set
`set` (liet. *aibė*) yra duomenų struktūra, kurioje duomenys visada yra
išrikiuoti ir nėra pasikartojančių elementų. Pagrindinės funkcijos:

* `.insert(x)` - įdeda reikšmę `x` į aibę. Jei tokia reikšmė jau yra, nieko neįvyksta;
* `.erase(x)` - ištrina reikšmę `x` iš aibės. Jei tokiosreikšms nėra, nieko neįvyksta;
* `.find(x)` - grąžina *iteratorių*, rodantį į aibės elementą, lygų `x`. Jei `x`
  aibje nėra, grąžinamas pabaigos iteratorius `end()`;
* `.lower_bound(x)` - grąžina nuorodą į pirma elementą aibje, kuris yra
  **nemažesnis** už `x`;
* `.upper_bound(x)` - grąžina nuorodą į pirma elementą aibėje, kuris yra
  **didesnis** už `x`;
* Standartinės funkcijos.

Visų šių funkcijų sudėtingumas yra `O(log(N))`. Kodo pavyzdys:

{% highlight c++ %}
set<int> S = {1, 5, 6};
S.insert(9); // {1, 5, 6, 9}
S.insert(1); // {1, 5, 6, 9}
S.erase(5);  // {1, 6, 9}
S.erase(7);  // {1, 6, 9}
if(S.find(1) == S.end()) { // jei elemento nėra aibėje, find grąžina end()
    cout << "neradau";
} else {
    cout << "radau";
}
{% endhighlight %}

Vienas svarbus pastebėjimas yra tas, kad su aibėmis, skirtingai nei su
vektoriais, negalima naudoti indeksavimo. Vadinais, gauti elemento pagal indeksą
ar pan. aibėje neįmanoma (indekso sąvoka aibėje išvis nelabai yra apibrėžta).
Todėl aibės dažniausiai naudojamos surinkti elementus be pasikartojimų ar
patikrinti, ar koks nors elementas jau yra aibėje (pvz. į aibę galima dėti grafe
aplankytų viršūnių numerius ir taip gana greitai patikrinti, ar konkreti viršūnė
jau buvo aplankyta, ar ne).

## map
`map` (dar vadinamas asociatyviu masyvu) yra galinga duomenų struktūra, kiek
primenanti vektorius ar masyvus. Skirtingai nei jau aptartos duomenų strukūros,
`map` turi du tipo parametrus. Aprašas `map<TK, TV>` reiškia asociatyvų masyvą,
kurio **raktų** tipas yra `TK`, o **rekšmių** tipas yra `TV`. Paprastai tariant,
raktas yra tai, kas naudojama indeksuojant duomenų struktūra (t.y. tai, ką
rašome tarp laužtinių skliaustų), o reikšmė - tai, ką gauname panaudoję
indeksavimą. Pavyzdžiui, masyvų ar vektorių atvejų indeksavimui visada naudojame
sveikuosius skaičius, tačiau `map` atveju galime naudoti ką tik norime.

Pagrindinės `map` funkcijos yra šios:

* `.erase(x)` - ištrina elementą su raktu `x`. Jei tokio rakto nėra, nieko nenutinka;
* `.find(x)` - grąžina iteratorių, rodantį į elementą, kurio raktas yra `x`. Jei
  rakto `x` nėra, grąžinamas pabaigos iteratorius `end()`;
* `.lower_bound(x)` - grąžina nuorodą į pirma elementą, kurio raktas yra
  **nemažesnis** už `x`;
* `.upper_bound(x)` - grąžina nuorodą į pirma elementą, kurio raktas yra
  **didesnis** už `x`;
* Standartinės funkcijos.

`map` veikia labai panašiai į `set`, nes čia raktai taip pat visada būna
išrikiuoti didėjimo tvarka bei nebūna pasikartojančių reikšmių. Vienintelis
skirtumas lyginant su `set` yra tas, kad kiekvienas raktas turi susijusią
reikšmę. Operacijų sudetingumai, kaip ir `set`, yra `O(log(N))` (**įskaitant ir indeksavimo su laužtiniais skliaustais!**).

Panagrinėkime pavyzdį. Tarkime, kad programos įvestis - `n` taškų. Mūsų tikslas -
suskaičiuoti, kiek kartų kiekvienas taškas buvo įvestas. Tam susikursime
asociatyvų masyvą `map<pii, int> cnt`, kuriame raktai bus patys taškai, o
reikšmės - kiek kartų konkretus taškas pasikartoja įvestyje. Kodas gali
atrodyti maždaug taip:

{% highlight c++ %}
map<pii, int> cnt;
int n; cin >> n;
for(int i = 0; i < n; i++) {
    pii p;
    cin >> p.first >> p.second; // nuskaitome tašką
    cnt[p]++; // padidiname šio taško pasikartojimų skaičių vienetu
}

for(auto e : cnt) {
    // e tipas yra pair<pii, int>
    // e.first yra raktas
    // e.second yra reikšmė
    int x = e.first.first;
    int y = e.first.second;
    int times = e.second;
    cout << "(" << x << ", " << y << "): " << times << endl;
}
{% endhighlight %}

## queue
`queue` (liet. *eilė*) - tai ganėtinai paprasta duomenų struktūra. Kaip gali
išduoti pavadinimas, jos veikimo principas panašus į įprastas gyvenime
sutinkamas eiles, pavyzdžiui, žmonių eilę parduotuvės kasoje - naujai atėję
žmonės stoja į eilės galą, o aptarnavimas vyksta nuo eilės priekio. Tokio tipo
duomenų struktūros paprastai vadinamos **FIFO** (angl. *First In First Out*).
Pagrindinės eilės palaikomos funkcijos:
* `.push(x)` - įdeda reikšmę `x` į eilės galą;
* `.front()` - grąžina reikšmę, esančią eils priekyje (bet jos neišima);
* `.pop()` - išima eilės priekyje esančią reikšmę;
* Standartinės funkcijos.

Mažas eilės veikimo pavyzdys:

{% highlight c++ %}
queue<int> Q;
Q.push(1);
Q.push(2);
Q.push(3);
while(!Q.empty()) {
    cout << Q.front() << endl;
    Q.pop();
}
/* Spausdina:
1
2
3
*/
{% endhighlight %}

Keli svarbūs niuansai: eilė nėra indeksuojama, per ją negalima iteruoti (t.y. su
`for(auto x : Q)` ciklus per eilės reikšmes perbėgti neįmanoma, reikia rašyti
tokį `while` ciklą, koks pateiktas pavyzdyje). Taip pat: visų eilės funkcijų
sudėtingumas yra `O(1)`.

## stack
`stack` - duomenų struktūra, priešinga eilei. Jei eilėje anksčiau įdeti
elementai anksčiau yra ir išimami, tai steke - atvirkščiai - paskutiniai įdėti
elementai yra išimami pirma. Tokio tipo duomenų struktūros vadinamos *LIFO*
(angl. *Last In First Out*). Steką lengviausia įsivaizduojant pasitelkiant
lėkščių krūvos analogiją: lėkštės yra dedamos ant krūvos viršaus, o nuimamos
taip pat nuo krūvos viršaus. Taip darant išeina, kad paskutinės padėtos lėkštės yra
nuimamoms pirmosios. Pagrindinėės steko funkcijos:
* `.push(x)` - įdeda reikšmę `x` į steko viršų;
* `.top()` - grąžina reikšmę, esančia steko viršuje (bet jos neišima);
* `.pop()` - išima steko viršuje esančią funkciją;
* Standartinės funkcijos.

Mažas steko veikimo pavyzdys:

{% highlight c++ %}
stack<int> S;
S.push(1);
S.push(2);
S.push(3);
while(!S.empty()) {
    cout << S.top() << endl;
    S.pop();
}
/* Spausdina:
3
2
1
*/
{% endhighlight %}

Stekas, kaip ir eilė, nėra indeksuojamas ir per jį negalima iteruoti. Steko
funkcijų sudėtingumas taip pat yra `O(1)`.

## deque
`deque` (angl. *double-ended queue*, liet. *dekas*) yra duomenų struktūra, analogiška eilei.
Vienintelis skirtumas - į deką reikšmes galima dėti tiek iš priekio, tiek iš
galo. Taip ir ir išimti reikšmes galima iš abiejų galų. Pagrindinės deko
funkcijos:
* `.push_front(x)` - įdeda reikšmę `x` į deko priekį;
* `.push_back(x)` - įdeda reikšmę `x` į deko galą;
* `.front()` - grąžina deko priekyje esančią reikšmę (bet jos neišima);
* `.back()` - grąžina deko gale esančią reikšmę (bet jos neišima);
* `.pop_front()` - išima deko priekyje esančią reikšmę;
* `.pop_back()` - išima deko gale esančią reikšmę;
* Standartinės funkcijos.

Mažas deko veikimo pavyzdys:

{% highlight c++ %}
deque<int> D;
D.push_front(1);                // [1]
D.push_back(2);                 // [1, 2]
D.push_back(3);                 // [1, 2, 3]
D.push_front(4);                // [4, 1, 2, 3]
cout << D.front() << endl;      // 4
cout << D.back() << endl;       // 3
D.pop_front();                  // [1, 2, 3]
cout << D.front() << endl;      // 1
D.pop_front();                  // [2, 3]
cout << D.front() << endl;      // 2
D.pop_back();                   // [2]
cout << D.back() << endl;       // 2
{% endhighlight %}

Dekas, skirtingai nei eilė ar stekas, yra indeksuojamas ir iteruojamas. Visų
operacijų sudėtingumas yra `O(1)`.

## priority_queue
`priority_queue` (liet. *prioritetinė eilė*) veikia iš dalies panašiai kaip ir
eilė, tačiau turi vieną esminį, labai svarbų ir naudingą skirtumą - joje į
priekį visada "nustumiami" didžiausi elementai (tiesa, šia tvarką galima
keisti). Prioritetinės eilės operacijos:
* `.push(x)` - įdeda reikšmę `x` į eilę;
* `.top()` - grąžina eilės priekyje esančią reikšmę (bet jos neišima);
* `.pop()` - išima eilės priekyje esančią reikšmę;
* Standartinės funkcijos.

Prioritetinės eilės naudojimo pavyzdys:

{% highlight c++ %}
priority_queue<int> Q;
Q.push(2);
cout << Q.top() << endl; // 2
Q.push(1);
cout << Q.top() << endl; // 2
Q.push(3);
cout << Q.top() << endl; // 3
while(!Q.empty()) {
    cout << Q.top() << endl;
    Q.pop();
}
/* Ciklas spausdina:
3
2
1
*/
{% endhighlight %}

Verta pastebėti, kad, skirtingai nei paprastoje eilėje, prioritetinės eilės
`push` ir `pop` funkcijų sudėtingumas yra ne `O(1)`, o `O(log(N))`.

Kitas svarbus aspektas kalbant apie prioritetines eiles yra rikiavimo tvarkos
nustatymas. Kaip matėme, numatytuoju atveju prioritetinė eilė į priekį "stumia"
didžiausius elementus. Norint tą pakeisti, eilės tipo aprašą reikia pakeisti
tokiu: `priority_queue<T, vector<T>, greater<T>>`. Šis užrašas garantuoja, kad į
eilės priekį bus "stumiami" maži elementai. Žemiau pateiktas tas pats pavyzdys,
kaip ir ką tik buvęs, tik su eile, "stumiančia" į priekį mažus elementus:

{% highlight c++ %}
priority_queue<int, vector<int>, greater<int>> Q;
Q.push(2);
cout << Q.top() << endl; // 2
Q.push(1);
cout << Q.top() << endl; // 1
Q.push(3);
cout << Q.top() << endl; // 1
while(!Q.empty()) {
    cout << Q.top() << endl;
    Q.pop();
}
/* Ciklas spausdina:
1
2
3
*/
{% endhighlight %}

# Dvejetainė paieška
C++ standartinė biblioteka taip pat turi dvi patogias funkcijas, gebančias
atlikti dvejetainę paiešką kokioje nors kolekcijoje. Šios funkcijos yra
`lower_bound` ir `upper_bound`.

`lower_bound(x)` - tai funkcija, kuri išrikiuotoje sekoje randa pirmą elementą,
kuris yra **nemažesnis** už `x`. Panašiai `upper_bound` yra funkcija, kuri
išrikiuotoje sekoje randa pirmą elementą, kuris yra **griežtai didesnis** už
`x`. Šios funkcijos naudojamos kiek skirtingai, priklausomai nuo to, kokioje
duomenų struktūroje vykdoma paieška.

## Paieška vektoriuje
Visų pirma panagrinėkime dvejetainės paieškos vektoriuje atvejį. Būtina sąlyga
prieš vykdant paiešką - vektorius **privalo** būti išrikiuotas. Tada pati
paieška vykdoma pasitelkiant funkcijas `lower_bound(begin, end, val)` bei
`upper_bound(begin, end, val)`. Štai pavyzdys:

{% highlight c++ %}
vector<int> v = {1, 5, 6, 2, 9, 10};
sort(v.begin(), v.end());       // išrikiuojame prieš vykdant paiešką!

auto it1 = lower_bound(v.begin(), v.end(), 6);
cout << *it1 << endl;                           // 6
auto it2 = upper_bound(v.begin(), v.end(), 6);
cout << *it2 << endl;                           // 9
{% endhighlight %}

Verta pastebėti gana neįprastą rašymo būdą: `*it1`. Taip rašoma todėl, kad
`lower_bound` ir `upper_bound` funkcijos grąžina *iteratorių*, rodantį į tam
tikrą vektoriaus elementą. Apie iteratorius čia daugiau nebus prasiplečiama
(galima paieškoti papildomos literatūros internete), tačiau esmė tokia, kad,
norint išgauti reikšmę, į kurią rodo iteratorius, naudojama šiame pavyzdyje
matyta sintaksė su žvaigždute. Tiesa, su tokiais užrašais reikia elgtis
atsargiai, nes, jei reikiama reikšmė nebūtų rasta (t.y. funkcija grąžintų
`v.end()`), tai rašymas `*it` "nulaužtų" programą.

Vektoriaus atveju taip pat galima gauti rasto elemento indeksą:

{% highlight c++ %}
auto it = lower_bound(v.begin(), v.end(), 10);
if(it != v.end()) {
    int i = it - v.begin();
    cout << "Rasto skaičiaus indeksas: " << i << endl;
} else {
    cout << "Nerasta" << endl;
}

it = upper_bound(v.begin(), v.end(), 10);
if(it != v.end()) {
    int i = it - v.begin();
    cout << "Rasto skaičiaus indeksas: " << i << endl;
} else {
    cout << "Nerasta" << endl;
}
/* Spausdina:
Rasto skaičiaus indeksas: 5
Nerasta
*/
{% endhighlight %}

## Paieška aibėje bei asociatyviame masyve
Paieška aibėje (`set`) bei asociatyviame masyve (`map`) yra kiek paprastesnė nei
vektoriaus atveju. Šiuo atveju nereikia nuorodų į pradžią ir pabaigą, kadangi
`lower_bound` bei `upper_bound` funkcijos yra "įsiųtos" į pačias duomenų
struktūras. Štai kodo pavyzdys:

{% highlight c++ %}
set<int> S = {1, 5, 6, 2, 9, 10};
// Rikiuoti nereikia, nes aibėje elementai automatiškai išrikiuoti
auto it1 = S.lower_bound(6);
cout << *it1 << endl;                               // 6
auto it2 = S.upper_bound(6);
cout << *it2 << endl;                               // 9

map<int, int> M = { {1, 10}, {5, 9}, {6, 3}, {2, 5}, {9, 2}, {10, 8} };
auto it3 = M.lower_bound(6);
cout << it3->first << " " << it3->second << endl;   // 6 3
auto it4 = M.upper_bound(6);
cout << it4->first << " " << it4->second << endl;   // 9 2
{% endhighlight %}

Čia vėlgi verta pabrėžti naujai atsiradusią sintaksę `it->first` bei
`it->second`. Kaip jau buvo aptarta anksčiau, `it` yra iteratorius, rodantis į
rastą rezultatą. Kadangi `map` duomenų struktūroje kiekvienas įrašas yra `pair`
tipo (t.y. pora iš rakto ir reikšmės), tai, norėdami pasiekti konkrečią rastą
rakto reikšmę, galėtume rašyti `(*it).first`, ir analogiškai su reikšme. C++
būtent šiai sintaksei turi santrumpą: `it->first`. Tai ir buvo panaudota
pavyzdyje.

Vienas esminis skirtumas nuo paieškos vektoriuje yra tas, kad vykdant paiešką su
`set` ir `map` neįmanoma gauti rasto elemento indekso, nes indeksai šiose
duomenų struktūrose tiesiog nėra apibrėžti.

Patikrinti, ar elementas buvo rastas, galima taip pat, kaip ir vektoriaus
atveju: tereikia gautą iteratorių palyginti su `S.end()` (ar `M.end()` `map`
atveju).

{% highlight c++ %}
{% endhighlight %}