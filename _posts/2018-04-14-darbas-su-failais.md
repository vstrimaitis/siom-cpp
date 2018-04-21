---
layout:     lesson
title:      Darbas su failais
date:       2018-04-13 16:43:00
author:     Vytautas Strimaitis
summary:    Šiame skyriuje išmoksime dirbti su failais.
categories: teorija
permalink: /:title/
thumbnail:  curly
iconclass:  fas fa-book
published: true
---
# Darbas su failais
Dirbti su duomenimis vien per konsolę ne visada pakanka - dažnai prisireikia duomenis išsaugoti ilgesniam laikui arba nuskaityti jau esamą failą. Čia mums gali pagelbėti C++ biblioteka `fstream`. Šiame skyriuje apsiribosime tik darbu su tekstiniais failais, tačiau galima dirbti su įvairių tipų formatais.

## Pasirengimas darbui su failais
Norint išnaudoti failų skaitymo / rašymo funkcijas, būtinai reikia į savo programą prisidėti biblioteką `fstream`. Tai galima padaryti programos pradžioje įrašius eilutę

{% highlight c++ %}
#include <fstream>
{% endhighlight %}

Tai padarius, programoje galėsime kurti reikiamo tipo kintamuosius. Konkrečiai mus domina du tipai: `ifstream` ir `ofstream`.

## Įvestis ir išvestis su `ifstream` ir `ofstream`
Biblioteka `fstream` pateikia dvi klases, reikalingas darbui su failais - `ifstream` ir `ofstream`. Pirmoji (`ifstream`) naudojama duomenis nuskaitant iš failo, o antroji (`ofstream`) - įrašant į failą. Darbas su failais susideda iš trijų dalių:
* Failo atidarymas
* Darbas su failu
* Failo uždarymas

Tarkime, turime tokį uždavinį: faile `duomenys.txt` yra įrašyti du sveikieji skaičiai. Užduotis - parašyti programą, kuri nuskaito šiuos skaičius ir išveda jų sumą į failą `rezultatai.txt`. Šį uždavinį sprendžianti programa:

{% highlight c++ %}
#include <fstream>

int main() {
    int a, b;
    ifstream fin("duomenys.txt");       // atidarome duomenų failą
    ofstream fout("rezultatai.txt");    // atidarome rezultatų failą
    // Vietoj pavadinimų fin ir fout galima rašyti bet ką. Šiuo atveju
    // fin skirtas nuskaitymui iš failo (t.y. "file input" = "file in" = "fin"),
    // o fout skirtas irašymui į failą (t.y. "file output" = "file out" = "fout").

    fin >> a >> b;                      // nuskaitome skaičius iš duomenų failo
    fout << a+b << endl;                // įrašome sumą į rezultatų failą

    fin.close();                        // uždarome duomenų failą
    fout.close();                       // uždarome rezultatų failą

    return 0;
}
{% endhighlight %}

**PASTABA.** Failai `duomenys.txt` bei `rezultatai.txt` turi būti tame pačiame kataloge, kaip ir jūsų programa.

Kaip galima pastebėti, darbas su failais yra labai panašus į [darbą su konsole]({{ site.baseurl }}{% post_url 2018-02-10-darbas-su-konsole %}) - tereikia vietoj `cin` ir `cout` naudoti savo apsirašytus failų identifikatorius (šiuo atveju - `fin` ir `fout`). Svarbu tik nepamiršti šių dalykų:
1. Nesumaišyti `ifstream` su `ofstream`. `ifstream` skirtas duomenų nuskaitymui (nes `i = input`), o `ofstream` - duomenų išvedimui (nes `o = output`).
1. Nurodyti failą, su kuriuo norime dirbti (t.y. rašant `ifstream fin ("failas.txt");` kai norime skaityti iš failo).
1. Baigus darbą su failu, nepamiršti failo uždaryti (įvykdyti kodą `failoIdentifikatorius.close()`). Neuždarius failo, jis gali likti "užrakintas" ir jo keisti / ištrinti gali nebeleisti operacinė sistema.