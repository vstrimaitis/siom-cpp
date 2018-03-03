[< Grįžti į turinį](../README.md)
# Masyvai
Šis skyrius skirtas susipažinti su **masyvais** C++ programavimo kalboje.

## Kas yra masyvas?
Dažnai rašant programas gali pasidaryti labai nepatogu kiekvienai įvedamai reikšmei rašyti po atskirą kintamąjį - kas, jei tokių kintamųjų yra šimtas ar milijonas? Norint nuskaityti tiek kintamųjų reikšmių reiktų rašyti tokį kodą:
```
int a1, a2, a3, ... a1000000;
cin >> a1 >> a2 >> a3 >> ... >> a1000000;
```
Akivaizdu, kad tai nėra nei patogu, nei greita. Tokiose situacijose mums gali padėti **masyvai**. Masyvas - tai tipas, gebantis savyje laikyti daugiau nei vieną reikšmę. Visos reikšmės, esančios masyvuose, yra **indeksuojamos**, tai yra, turi tam tikrą joms priskirtą numerį. Reikšmės masyvuose indeksuojamos nuo nulio, tad pirmo elemento numeris (arba indeksas) yra lygus 0, antro elemento - 1 ir taip toliau.

## Masyvo sukūrimas
Masyvai visada būna fiksuoto dydžio, tad norint sukurti masyvą, visų pirma reikia žinoti, kiek elementų mes jame norėtume sutalpinti. Šį skaičių kuriant masyvą galima nurodyti ir didesnį, negu iš tikro reikia, tačiau tada bus naudojama daugiau atminties. Masyvą sukurti galima taip:
```
int masyvas[100];
```
Šis kodas sukurs masyvą, kuris galės laikyti iki šimto sveikųjų skaičių.

Masyvo elementams, turintiems tam tikrą indeksą, galima priskirti reikšmes bei jas nuskaityti. Tai daroma taip:
```
int masyvas[100];
masyvas[0] = 10;
masyvas[1] = 20;
masyvas[2] = 60;
cout << masyvas[1] << endl; // spausdina 20
```
Dabar `masyvas` pirmos trys reikšmės bus lygios 10, 20 ir 60 atitinkamai, o visos kitos kol kas neaiškios (jei masyvą parašytume kaip *globalų* kintamąjį, visos kitos reikšmės būtų lygios nuliui).

## Įvesties nuskaitymas į masyvą
Spręsdami uždavinius dažnai susidursite su situacija, kuomet reikės nuskaityti vartotojo įvestus duomenis ir išsaugoti juos masyve. Tai galima padaryti taip:
```
int duomenys[100]; // tarkime, kad vartotojas niekad neįves daugiau nei 100 skaičių
int n; // vartotojo įvedamų duomenų kiekis
cin >> n; // nuskaitome, kiek bus duomenų
for(int i = 0; i < n; i++) {
    cin >> duomenys[i]; // nuskaitome iš konsolės vieną skaičių ir išsaugome jį i-ojoje pozicijoje masyve
}
```

Dabar su šiais duomenimis galima dirbti. Tarkime, norime kiekvieną įvestą skaičių padauginti iš dviejų. Tai būtų galima padaryti taip:
```
for(int i = 0; i < n; i++) {
    duomenys[i] *= 2;
}
```

Po to galime duomenis ir išvesti. Pabandykime išvesti juos atvirkščia tvarka:
```
for(int i = n-1; i >= 0; i--) {
    cout << duomenys[i] << " ";
}
```
Taigi, jei šiai programai įvesime tokius duomenis:
```
3
1 2 3
```
Programa išves:
```
6 4 2
```

## Dvimačiai masyvai
Tai, ką dabar nagrinėjome, yra vadinama vienmačiais masyvais. C++ programavimo kalboje galima kurit ir dvimačius, trimačius, keturmačius ir t.t. masyvus. Šiame poskyryje panagrinėkime, kaip sukurti ir dirbti su dvimačiu masyvu. Toks masyvas kuriamas taip:
```
char dvimatis[100][50];
```
Taip sukursime dvimatį masyvą, kuris laikys simbolius ir bus 100x50 dydžio. Šį masyvą galime įsivaizduoti kaip lentelę, turinčią 100 eilučių ir 50 stulpelių. Pabandykime nuskaityti duomenų į šį masyvą:
```
int n, m; // eilučių ir stulpelių skaičius
cin >> n >> m;
for(int i = 0; i < n; i++) {
    for(int j = 0; j < m; j++) {
        cin >> dvimatis[i][j]; // į i-ąją eilutę ir j-ąjį stulpelį įrašome nuskaitytą reikšmę
    }
}
```

Jei norime išspausdinti reikšmę, esančią 2-oje eilutėje ir 10-ame stulpelyje, rašytume taip:
```
cout << dvimatis[1][9] << endl;
```
Indeksai nėra 2 ir 10, nes juk masyvai numeruojami nuo nulio!

Dar verta pastebėti, kad eilutė su indeksu 0 yra pati viršutinė, su indeksu 1 yra žemiau ir taip toliau.