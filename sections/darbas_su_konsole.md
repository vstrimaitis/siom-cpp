[< Grįžti į turinį](../README.md)
# Darbas su konsole
Konsolė - tai pirmas ir dažniausiai pradedančiųjų programuotojų naudojamas įrankis bendravimui su naudotoju. Šiame skyriuje apžvelgsime, kaip C++ programavimo kalboje išspausdinti duomenis į konsolę bei nuskaityti naudotojo įvestus duomenis iš konsolės.

Šiame skyriuje apžvelgsime, kaip į konsolę išvesti duomenis bei kaip iš konsolės nuskaityti duomenis.

**Pastaba:** Norint naudoti komandas, dirbančias su konsole, reikia į savo programą įsidėti `iostream` biblioteką (tai galima padaryti programos pradžioje parašius `#include <iostream>`).

## Duomenų išvedimas į konsolę
Pirmiausia apžvelkime, kaip C++ kalboje kažką išspausdinti į konsolę. Tam yra naudojama komanda `cout` (kad būtų lengviau įsiminti - `c`, nes C++, `out` - nes *išvedame į išorę*). Pats spausdinimas atliekamas taip:
```
cout << pirmas << antras << trecias << ...;
```
Čia simbolių junginys `<<` atskiria spausdinamus duomenis. Galite įsivaizduoti, kad duomenis `pirmas`, `antras`, `trecias` ir taip toliau tiesiog jungiate į vieną eilutę. Būtent tą ir žymi simboliai `<<`.

Čia paminėti duomenys `pirmas`, `antras`, `trecias` ir taip toliau gali būti:
* Kintamieji
* Tekstas (rašomas apgaubiant dvigubomis kabutėmis)
* `endl` - reiškia eilutės pabaigą. Tai iš esmės tas pats, kaip paspausti mygtuką "Enter" klaviatūroje.
* Formatavimo modifikatoriai (pvz. `fixed`, `setprecision` ar pan., apie juos vėliau).

Štai keli kodo pavyzdžiai:
```
cout << "Labas" << endl; // endl reiškia naują eilutę (tai tarsi "Enter" mygtuko paspaudimas)
int x = 10;
cout << x << "!"; // galima ir be endl
int y = 15;
cout << x << " " << y << endl; // išveda 10 ir 15, atskirtus tarpais, užbaigia nauja eilute
```
Šis kodas išspausdina:
```
Labas
10!10 15

```

## Išvesties formatavimas
Kaip jau buvo užsiminta, išvestį galima formatuoti naudojant tam tikrus modifikatorius. Išvesties formatavimui reikalingos komandos yra `iomanip` bibliotekoje. Ją įsidėti galima parašius tokį kodą programos pradžioje: `#include <iomanip>`.

Tokių išvesties modifikatorių `iomanip` biblioteka turi tikrai nemažai (jei įdomu, galite paskaityti [čia](http://www.cplusplus.com/reference/iomanip/)), tačiau čia apžvelgsime vieną iš jų - `setprecision`.

Modifikatorius `setprecision` naudojamas nurodyti, kokiu tikslumu reikia spausdinti realiuosius skaičius. Pavyzdžiui, jei bespausdindami įterpsime `setprecision(6)`, tai toliau einantys realieji skaičiai bus spausdinami šešių skaitmenų po kablelio tikslumu.

Modifikatorius `setprecision` dažnai naudojamas kartu su modifikatoriumi `fixed`, esančiu jau aptartoje `iostream` bibliotekoje. Modifikatorius `fixed` garantuoja, kad spausdinamas realusis skaičius bus rašomas kaip įprasta dešimtainė trupmena.

Kodo pavyzdys:
```
double pi = 3.14;
int penkiolika = 15;
cout << pi << endl;
cout << fixed << setprecision(5) << pi << endl;
cout << fixed << setprecision(6) << penkiolika << endl;
```
Šis kodas spausdina:
```
3.14
3.14000
15
```
Atkreipkite dėmesį, kad skaičius `15` nebuvo spausdinamas šešių skaitmenų po kablelio tikslumu, nors tai nurodėme naudodami `setprecision`. Taip atsitiko dėl to, kad `penkiolika` yra `int` tipo kintamasis, o sveikieji skaičiai juk neturi trupmeninės dalies. Todėl jų `setprecision` modifikatorius neveikia.

## Duomenų nuskaitymas iš konsolės
Galiausiai pažiūrėkime, kaip galima nuskaityti konsolėje naudotojo įvestus duomenis. Tam yra naudojama komanda `cin` (kad būtų lengviau įsiminti - `c`, nes C++, `in` - nes *imame duomenis "vidun"*). Pats nuskaitymas atliekamas taip:
```
cin >> pirmas >> antras >> trecias >> ...;
```
Šiame pavyzdyje `pirmas`, `antras`, `trecias` ir t.t. turi būti aprašyti kažkur anksčiau kaip kintamieji.

Atkreipkite dėmesį, kad nuskaitant duomenis jau naudojamas simbolių junginys `>>` (spausdinant buvo `<<`).

Naudojant tokį užrašą galima nuskaityti kiek norima daug duomenų iš konsolės. Nuskaitant duomenis yra ignoruojami *whitespace* simboliai (t.y. tarpai, tabuliacijos žymės bei naujos eilutės).

Kodo pavyzdys:
```
int i;
double d;
char c;
cin >> i >> c >> d;
```
Šis kodas iš konsolės nuskaitys vieną sveiką skaičių, vieną simbolį ir vieną realųjį skaičių, o nuskaitytas reikšmes įrašys į kintamuosius `i`, `c` bei `d`. Šie trys dalykai įvestyje gali būti atskiriami tiek tarpais, tiek naujomis eilutėmis - nuskaitymas vis tiek veiks.