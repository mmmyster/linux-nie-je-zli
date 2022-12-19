### OBSAH

---

- [**Esej**](#user-information)
- [**Domáca úloha č. 2**](#domáca-úloha-č.-2)
- [**Domáca úloha č. 3**](#user-information)
- [**Domáca úloha č. 4**](#user-information)
- [**Domáca úloha č. 5**](#user-information)
- [**Domáca úloha č. 6**](#user-information)

---

### DOMÁCA ÚLOHA Č. 2

##### 2.1

Pomocou jedného príkazu (vrátane vhodných prepínačov) vytvorte niekoľko adresárov v štruktúre /home/{Váš domovský adresár}/ZLI/domov/uloha 2.2

```
mkdir -p /home/{Váš domovský adresár}/ZLI/domov/uloha
```

##### 2.2

###### a) Z domovského adresára pomocou relatívnej cesty zobrazte obsah adresára `/etc/apt/`

```
ls ../../etc/apt
```

###### b) Z domovského adresára pomocou absolútnej cesty zobrazte obsah adresára `/etc/apt/`

```
ls /etc/apt
```

###### c) Vysvetlite na vyššie uvedených úlohách rozdiel medzi relatívnou a absolútnou cestou

Relatívna cesta je vizaná na pwd, čiže na miesto, kde sa práve nachádzame. Na druhej strane absolútna cesta sa viaže na koreňový adresár.

##### 2.3 Vypíšte mená užívateľov (prvý stĺpec v súbore `/etc/passwd`) usporiadaný v abecednom poradí

```
cut /etc/passwd -d : -f 1 | sort
```

###### a) Zobrazte 3.,5. a 7. stĺpec súboru /etc/passwd

```
cut /etc/passwd -d : -f 3,5,7
```

###### b) Zobrazte 15. až 30. riadok a súčasne 3.,5. a 7. stĺpec súboru /etc/passwd

```
cut /etc/passwd -d : -f 3,5,7 | head -n 30 | tail -n 16
```

###### c) Spočítajte počet znakov a slov vo výbere riadkov a stĺpcov podľa bodu b) (Hint: wc má prepínače na slová a znaky, pozrite manuálové stránky)

```
cut /etc/passwd -d : -f 3,5,7 | head -n 30 | tail -n 16 | wc -m -w
```

##### 2.4 Vymyslite zadanie, pri ktorom bude nutné použiť pipe (rúru) a minimálne nástroje sort, uniq, grep (zadanie sa nesmie zhodovať s úlohou na hodine)

Každý rok sa zverejňujú štatistiky o najpopulárnejších menách pre bábätká.
V rokoch 2002/2003 patrili na prvé miesta mená martin, michal, matej, michaela.
Určite ste si všimli, že majú niečo spoločné. presne tak. Všetky začínajú písmenom m.
Vypíšte teda z adresára /etc/passwd na študentskom serveri prvých desať najpoužívanejších mien s počiatočným písmenom m,
ku každému menu vypíšte počet jeho výskytov a zoraďte od mena s najvyšším počtom.

```
cut /etc/passwd -d _ -f 1 | grep ^m | sort | uniq -c | sort -n -r | head
```

##### 2.5

###### a) Nájdite na študentskom serveri (s.ics.upjs.sk) všetky súbory, ktorých názov obsahuje slovné spojenie conf, ich veľkosť je maximálne 20 MB

```
find / -name "*conf*" -size -20M 2>/dev/null/
```

###### b) Doplňte riešenie v bode a) tak, aby ste o každom nájdenom súbore vypísali informácie o súbore (HIND: nástroj ls má prepínač pre podrobné informácie o súboroch a adresároch, použite manuálové stránky). Akú veľkosť majú tieto súbory?

```
find / -name "*conf*" -size -20M 2>/dev/null -exec ls -lh {} \; | cut -d " " -f 5
```

###### c) Upravte riešenie v bode b) tak, aby ste zobrazili prvých 5 riadkov každého súboru.

```
find / -name "*conf*" -size -20M 2>/dev/null -exec head -n 5 {} \;
```

##### Bonus

###### a) Vysvetlite, čo je jadro (kernel) operačného systému Linux

Kernel je jadro každého operčného systému. Linux kernel je vlastne to, čo zjednodušene voláme Linux.

###### b) Zistite distribúciu a verziu jadra operačného systému Linux, ktorý ste si nainštalovali na domácom zariadení. Uveďte príkaz, ako ste to zistili

```
cat /etc/os-release
```
