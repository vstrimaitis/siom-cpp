[< Grįžti į turinį](../README.md)
# Darbas su konsole
Konsolė - tai pirmas ir dažniausiai pradedančiųjų programuotojų naudojamas įrankis bendravimui su naudotoju. Šiame skyriuje apžvelgsime, kaip C++ programavimo kalboje išspausdinti duomenis į konsolę bei nuskaityti naudotojo įvestus duomenis iš konsolės.

Norint naudoti komandas, dirbančias su konsole, reikia į savo programą įsidėti `iostream` biblioteką (tai galima padaryti programos pradžioje parašius `#include <iostream>`).

## Duomenų išvedimas į konsolę
MEDŽIAGA RUOŠIAMA
```
cout << "Labas" << endl; // endl reiškia naują eilutę (tai tarsi "Enter" mygtuko paspaudimas)
int x = 10;
cout << x; // galima ir be endl
int y = 15;
cout << x << " " << y << endl; // išveda 10 ir 15, atskirtus tarpais, užbaigia nauja eilute
```
[//]: # (Apie cout ir endl ir <<)

## Išvesties formatavimas
MEDŽIAGA RUOŠIAMA

Reikalinga `iomanip` biblioteka. Ją įsidėti galima parašius tokį kodą programos pradžioje: `#include <iomanip>`.

Turi daug naudingų funkcijų, tačiau dažniausiai naudojama, kai norima tam tikru tikslumu atspausdinti skaičių su kableliu. Pavyzdžiui, jei norime atspausdinti skaičių 5 ženklų po kablelio tikslumu, rašytume taip:
```
double d = 3.14;
cout << fixed << setprecision(5) << d << endl; // išves 3.14000
```
[//]: # (Paminėt spausdinimą su tam tikru tikslumu ir pan)

## Duomenų nuskaitymas iš konsolės
MEDŽIAGA RUOŠIAMA

Nuskaityti iš konsolės galima naudojantis `cin` komanda. Pavyzdžiui, nuskaityti du sveikuosius skaičius galima taip:
```
int n, m;
cin >> n >> m;
```
Taip galima nuskaityti kiek tik norima daug reikšmių iš konsolės.
[//]: # (Api cin ir >>)