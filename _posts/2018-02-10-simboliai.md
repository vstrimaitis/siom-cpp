---
layout:     lesson
title:      Simboliai
date:       2018-02-10 11:59:00
author:     Vytautas Strimaitis
summary:    Šis skyrius skirtas apžvelgti C++ simbolius - kaip jie saugomi atmintyje, kas yra ASCII bei kokių "triukų" galima panaudoti, dirbant su simboliais.
categories: teorija
thumbnail:  char
---
# Simboliai
Šis skyrius skirtas apžvelgti C++ simbolius - kaip jie saugomi atmintyje, kas yra ASCII bei kokių "triukų" galima panaudoti, dirbant su simboliais.

Simboliai C++ kalboje žymimi naudojant viengubas kabutes (pvz `'a'`). Simbolio tipo reikšmėms saugoti naudojamas `char` tipas.

## Kaip simbolius "mato" kompiuteris?
Gali atrodyti keista, tačiau kompiuteris iš tikrųjų su tokiais dalykais kaip "simboliai" atlikti veiksmų nemoka. Jis moka dirbti tik su skaičiais. Dėl šios priežasties, ir simboliai yra koduojami tam tikrais skaičiais. Pavyzdžiui, simbolį `'a'` atitinka skaičius `97`, o simbolį `'3'` - skaičius `51`. Šis kodavimas yra vadinamas **ASCII** (angl. American Standard Code for Information Interchange).

## ASCII lentelė
Žemiau pateikta taip vadinama **ASCII lentelė**:

![ASCII lentelė]({{site.baseurl}}/images/ascii_table.jpg)

**Pastaba:** čia pateikta lentelė nėra pilna. Kaip galima pastebėti, joje trūksta simbolių su kodais nuo 0 iki 31. Šie simboliai yra nespausdinami, todėl kol kas į juos tiesiog nekreipsime dėmesio.

ASCII lentelė parodo, koks skaičius atitinka kurį simbolį. Todėl užmetę čia akį tikrai galime pastebėti, kad simbolio `'a'` atitikmuo yra skaičius `97` ir pan.

## Triukai su C++ simboliais
Remiantis žiniomis apie ASCII kodavimą bei tai, kad kompiuteris simbolius iš tikrųjų saugo kaip skaičius, galime parašyti gan įdomių kodo gabaliukų. Pastebėkime, kad ASCII lentelėje visos mažosios raidės eina viena šalia kitos, t.y. jų kodai yra išsidėstę intervale nuo 97 iki 122. Dėl šios priežasties, galime parašyti tokią programą, kuri nustato, ar įvestas simbolis yra mažoji raidė:

{% highlight c++ %}
char c;
cin >> c; // nuskaitome vieną simbolį iš konsolės
if (c >= 97 && c <= 122) { // jei simbolis pakliūna į nustatytą intervalą
    cout << "Taip" << endl;
}
else {
    cout << "Ne" << endl;
}
{% endhighlight %}

Ši programa spausdins `Taip`, jei bus įvedama mažoji raidė, ir `Ne` kitais atvejais. Žinoma gali atrodyti painu, kad kode naudojami iš pirmo žvilgsnio nieko nereiškiantys skaičiai. Šį kodą galime pagerinti taip:

{% highlight c++ %}
char c;
cin >> c; // nuskaitome vieną simbolį iš konsolės
if (c >= 'a' && c <= 'z') { // jei simbolis pakliūna į nustatytą intervalą
    cout << "Taip" << endl;
}
else {
    cout << "Ne" << endl;
}
{% endhighlight %}

Šiuo atveju simbolį lyginame su simboliu. Tai gali atrodyti keista, tačiau prisiminkime - visi simboliai iš tikrųjų yra skaičiai, tad toks palyginimas yra visiškai teisingas. Be to, šis kodas daug lengviau suprantamas negu pirmasis, nors daro lygiai tą patį.