[< Grįžti į turinį](../README.md)
# Ciklai
Šis skyrius skirtas susipažinti su **ciklais** C++ programavimo kalboje.

## Kas yra ciklas?
Kartais rašant programas norisi tam tikrus veiksmus kartoti daug kartų. Pavyzdžiui, galbūt norime nuskaityti dešimt vartotojo konsolėje įvestų skaičių. Vienas būdas tai padaryti būtų rašyti tokį kodą:
```
int a1, a2, a3, a4, a5, a6, a7, a8, a9, a10;
cin >> a1 >> a2 >> a3 >> a4 >> a5 >> a6 >> a7 >> a8 >> a9 >> a10;
```
O kas jei tų skaičių norėtume nuskaityti šimtą? Turbūt akivaizdu, kad tokį kodą rašyti yra labai nepatogu, nors logika juk paprasta - pakartoti tą patį veiksmą dešimt (ar šimtą) kartų. Būtent tokiais atvejais galime panaudoti ciklus.

## Ciklų rūšys
C++ programavimo kalba palaiko trijų rušių ciklus:
* `while`
* `do...while`
* `for`

Apie kiekvieną iš jų pakalbėsime toliau.

## `while` ciklas
Ciklas `while` naudojamas, kuomet norime kartoti tam tikrą kodą tol, kol tenkinama tam tikra sąlyga. Jo sintaksė yra tokia:
```
while (sąlyga) {
    // kodas, kurį norime kartoti
}
```
Pavyzdžiui, tarkime norime sužinoti, kiek kartų skaičius 1024 dalinasi iš dviejų. Tam nustatyti galėtume pabandyti 1024 dalinti iš dviejų iki tol, kol daugiau padalinti be liekanos nebeišeis. Kodas atrodytų taip:
```
int x = 1024;
int kiek = 0;
while (x % 2 == 0) { // kartosime tol, kol x dalinsis iš dviejų be liekanos
    x /= 2; // padaliname x iš dviejų
    kiek++; // padidiname atsakymą vienetu
}
cout << kiek << endl; // atspausdiname atsakymą
```
Šis kodas išvestų skaičių `10`.

### `do...while` ciklas
`do...while` ciklas yra lygiai toks pats, kaip ir `while` ciklas, tik jame esantis kodas garantuotai bus įvykdytas nors vieną kartą, nes sąlyga tikrinama po kodo vykdymo. Sintaksė tokia:
```
do {
    // kodas
} while (sąlyga);
```
Tarkime, kad norime nuskaityti iš konsolės skaičius iki kol bus ivestas nulis, bet bent vieną skaičių nuskaityti tikrai turime. Tada pagelbėtų toks kodas:
```
int a;
do {
    cin >> a;
} while(a != 0);
```

### `for` ciklas
`for` ciklas dažniausiai naudojamas tada, kai iš anksto žinome, kiek kartų norime kartoti tam tikrą kodą. Šio ciklo sintaksė tokia:
```
for(ciklo skaitliuko sukūrimas; sąlyga; ciklo skaitliuko reikšmės keitimas) {
    // kodas
}
```
Šį ciklą geriau paaiškinti konkrečiu pavyzdžiu. Tarkime, kad norime nuskaityti penkis skaičius iš konsolės ir išvesti jų sumą. Tai galima pasiekti tokiu kodu:
```
int suma = 0;
for (int i = 0; i < 5; i++) {
    int a;
    cin >> a;
    suma += a;
}
cout << suma << endl;
```
Panagrinėkime kodą:
* `int i = 0` nustato, kad ciklo kintamasis bus pavadintas `i` ir jo pradinė reikšmė bus lygi nuliui.
* `i < 5` reiškia, kad cikle esantis kodas bus vykdomas tol, kol `i` reikšmė bus mažesnė už 5. Ši sąlyga tikrinama kiekvieną kartą prieš vykdant ciklo kodą.
* `i++` reiškia, kad kiekvieną kartą įvykdžius ciklo kodą, kintamojo `i` reikšmė bus padidinama vienetu.

Taigi, kodas vyks taip:
1. Sukuriamas kintamasis `i` su reikšme `0`
2. Ar `i < 5`? Taip, todėl vykdome kodą.
3. Įvykdomas tarp riestinių skliaustų esantis kodas.
4. Kintamojo `i` reikšmė padidinama vienetu (dabar `i = 1`).
5. Ar `i < 5`? Taip, todėl vykdome kodą.
6. Įvykdomas tarp riestinių skliaustų esantis kodas.
7. Kintamojo `i` reikšmė padidinama vienetu (dabar `i = 2`).
8. ...
9. Kintamojo `i` reikšmė padidinama vienetu (dabar `i = 5`).
10. Ar `i < 5`? Ne, todėl cikle esantis kodas daugiau nebevykdomas.

Taigi iš viso kodas, esantis tarp riestinių skliaustų bus įvykdomas penkis kartus (kai `i = 0`, kai `i = 1`, kai `i = 2`, kai `i = 3` bei kai `i = 4`).