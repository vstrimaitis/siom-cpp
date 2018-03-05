---
layout:     lesson
title:      Sąlyginiai sakiniai
date:       2018-01-21 22:42:00
author:     Vytautas Strimaitis
summary:    Šis skyrius skirtas susipažinimui su sąlyginiais sakiniais ir kaip juos užrašyti C++ kalboje.
categories: teorija
permalink: /:title/
thumbnail:  if
---
# Sąlyginiai sakiniai
Šis skyrius skirtas susipažinimui su sąlyginiais sakiniais ir kaip juos užrašyti C++ kalboje.

## Kas yra sąlyginis sakinys?
Šnekamojoje kalboje dažnai sakome "Jei bus X, tai darysiu Y". Pavyzdžiui, "Jei šiandien lis, tai būsiu namie, o kitu atveju eisiu žaisti į lauką". Lygiai tokias pačias sąlygas dažnai prisireikia nurodyti ir programuojant kompiuteriui ir tam naudojami **sąlyginiai sakiniai**. Sąlyginis sakinys - tai kodo dalis, nurodanti, kokioms sąlygoms esant reiktų vykdyti (ar nevykdyti) tam tikrą kodą.

## Kaip tai užsirašo C++ kalboje?
Norint parašyti sąlyginį sakinį C++ kalboje (kaip ir daugelyje kitų programavimo kalbų), naudojamas raktinis žodelis `if` (angl. jeigu). Pats sąlyginio sakinio užrašas atrodo taip:

{% highlight c++ %}
if (sąlyga) {
    // Kodas, kurį vykdysime, jei sąlyga teisinga
}
{% endhighlight %}

Šis konkretus kodas tinka tik tais atvejais, kai norime kažką daryti tik tada, kai sąlyga yra teisinga. O ką daryti, jei norime daryti viena, kai sąlyga teisinga, ir kita, kai sąlyga neteisinga?  Čia mums gali pagelbėti kitas svarbus C++ raktinis žodelis - `else` (angl. kitu atveju). Jis visada naudojamas kartu su `if` ir skirtas nurodyti kodą, kurį reiktų vykdyti, jei šalia `if` esanti sąlyga yra klaidinga. Ši struktūra užrašoma taip:

{% highlight c++ %}
if (sąlyga) {
    // Kodas, kurį vykdysime, jei sąlyga teisinga
}
else {
    // Kodas, kurį vykdysime, jei sąlyga neteisinga
}
{% endhighlight %}

Liko tik dar vienas atvejis - kaip parašyti kodą, kuris elgtųsi skirtingai esant kelioms sąlygoms? Šiuo atveju reikia naudoti žodelių `if` ir `else` kombinaciją, kuri atrodo taip:

{% highlight c++ %}
if (sąlyga1) {
    // Kodas, kurį norime vykdyti, jei teisinga pirmoji sąlyga
}
else if (sąlyga2) {
    // Kodas, kurį norime vykdyti, jei klaidinga pirmoji, bet teisinga antroji sąlyga
}
else if (sąlyga3) {
    // Kodas, kurį norime vykdyti, jei klaidingos pirmoji ir antroji, bet teisinga trečioji sąlyga
}
else {
    // Kodas, kurį norime vykdyti, kai visos anksčiau nurodytos sąlygos klaidingos
}
{% endhighlight %}

Tokių `else if` dalių galima įrašyti kiek tik nori, o `else` dalis taip pat nebūtina - viskas priklauso nuo situacijos. Šiuo atveju sąlygos tikrinamos viena po kitos iš viršaus į apačią. Radus sąlygą, kuri yra teisinga, vykdomas su ta sąlyga susijęs kodo blokas, o visi likę šio sąlyginio sakinio blogai praleidžiami.

## Pavyzdžiai
Pastaba: visuose šiuose pavyzdžiuose tarsime, kad turime kintamąjį `int pazymys`, aprašytą kažkur anksčiau.

### Vienas `if` sakinys
Tarkim norime parašyti kodą, pasveikinantį naudotoją, jei `pazymys` yra lygus dešimtukui. Toks kodas atrodytų taip:

{% highlight c++ %}
if (pazymys == 10) {
    cout << "Sveikinu!";
}
{% endhighlight %}

Šiame kode visų pirma būtų patikrinta sąlyga `pazymys == 10`. Jei ši sąlyga teisinga, tai būtų vykdomas kodo blokas, einantis po sąlygos (t.y. programa išspausdintų "Sveikinu!). Kitu atveju, visas šis kodo blokas būtų praleidžiamas ir programa tęstų darbą už jo.

### Struktūra `if` - `else`
Tarkim norime parašyti kodo gabaliuką, kuris pasveikina naudotoją, jei jis gavo dešimtuką, ir padrąsina pasistengti kitu atveju. Šis kodas atrodytų taip:

{% highlight c++ %}
if (pazymys == 10) {
    cout << "Sveikinu!";
}
else {
    cout << "Viskas gerai, nenusimink!";
}
// Likęs kodas
{% endhighlight %}

Šiuo atveju visų pirma būtų patikrinta sąlyga `pazymys == 10`. Jei sąlyga teisinga, bus spausdinamas tekstas "Sveikinu!" ir tada vykdomas likęs kodas (pažymėtas komentaru). Kitu atveju bus spausdinamas tekstas "Viskas gerai, nenusimink!" ir tada vykdomas likęs kodas.

### Struktūra `if` - `else if`
Tarkim norime parašyti kodą, kuris pasveikina naudotoją, gavusį dešimtuką, o gavus dvejetą liepia pasistengti, galėtume parašyti taip:

{% highlight c++ %}
if (pazymys == 10) {
    cout << "Sveikinu!";
}
else if (pazymys == 2) {
    cout << "Reiktų pasistengti...";
}
{% endhighlight %}

Šiuo atveju programa spausdintų tekstą "Sveikinu!", jei naudotojas gavo dešimtuką, ir "Reiktų pasistengti...", jei gavo dvejetą. Kitu atveju nieko nebūtų spausdinama. Kaip matote šį kartą išvis neįrašėme `else {...}` dalies - įrodymas, kad ji nebūtina.

### Struktūra `if` - `else if` - `else`
Tarkim turime tokį kodą:

{% highlight c++ %}
if (pazymys == 10) {
    cout << "Sveikinu!";
}
else if (pazymys > 7) {
    cout << "Labai gerai!";
}
else if (pazymys < 5) {
    cout << "Reiktų pasistengti...";
}
else {
    cout << "Viskas gerai";
}
{% endhighlight %}

Šiuo atveju programa spausdins:
* "Sveikinu!", jei `pazymys` bus lygus 10
* "Labai gerai!", jei `pazymys` bus lygus 9 arba 8
* "Reiktų pasistengti...", jei `pazymys` bus mažesnis už 5
* "Viskas gerai" kitais atvejais (t.y. jei `pazymys` bus lygus 5, 6 arba 7)

Verta pastebėti, kad šiuo atveju visos sąlygos yra susijusios - sąlygos bus tikrinamos viena po kitos iš viršaus į apačia ir, kai tik viena iš jų bus teisinga, bus įvykdytas su ta sąlyga susijęs kodo blokas, o visi kiti bus praleisti. 

### Atskiri sąlyginiai sakiniai
Panagrinėkime šiek tiek pakeistą pavyzdį:

{% highlight c++ %}
if (pazymys == 10) {
    cout << "Sveikinu!";
}
if (pazymys > 7) {
    cout << "Labai gerai!";
}
else if (pazymys < 5) {
    cout << "Reiktų pasistengti...";
}
else {
    cout << "Viskas gerai";
}
{% endhighlight %}

Šiuo atveju programa spausdins:
* "Sveikinu!Labai gerai!", jei `pazymys` bus lygus 10
* "Labai gerai!", jei `pazymys` bus lygus 9 arba 8
* "Reiktų pasistengti...", jei `pazymys` bus mažesnis už 5
* "Viskas gerai" kitais atvejais (t.y. jei `pazymys` bus lygus 5, 6 arba 7)

Pastebėkime, kad dabar kode jau yra du atskiri sąlyginiai sakiniai - vienas, turintis sąlygą `pazymys == 10`, ir kitas, turintis visas likusias sąlygas. Būtent dėl šios priežasties programa spausdina labai keistą tekstą ("Sveikinu!Labai gerai!"), kai `pazymys` lygus 10 - visų pirma patenkinama pirmojo sąlyginio sakinio sąlyga ir spausdinamas tekstas "Sveikinu!", o po to patenkinama ir antrojo sąlyginio sakinio pirmoji sąlyga ir spausdinamas tekstas "Labai gerai!".
