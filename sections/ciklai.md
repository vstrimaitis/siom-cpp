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
Informacija ruošiama...