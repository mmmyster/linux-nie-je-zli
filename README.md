### OBSAH

---

- [**Esej**](#user-information)
- [**Domáca úloha č. 2**](#domáca-úloha-č.-2)
- [**Domáca úloha č. 3**](#domáca-úloha-č.-3)
- [**Domáca úloha č. 4**](#domáca-úloha-č.-4)
- [**Domáca úloha č. 5**](#domáca-úloha-č.-5)
- [**Domáca úloha č. 6**](#domáca-úloha-č.-6)

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

Každý rok sa zverejňujú štatistiky o najpopulárnejších menách pre bábätká. V rokoch 2002/2003 patrili na prvé miesta mená martin, michal, matej, michaela. Určite ste si všimli, že majú niečo spoločné. presne tak. Všetky začínajú písmenom m. Vypíšte teda z adresára /etc/passwd na študentskom serveri prvých desať najpoužívanejších mien s počiatočným písmenom m, ku každému menu vypíšte počet jeho výskytov a zoraďte od mena s najvyšším počtom.

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

---

### DOMÁCA ÚLOHA Č. 3

##### 3.1

###### a) Nájdite na študentskom serveri (s.ics.upjs.sk) všetky súbory, ktoré majú oprávnenia v777 v oktálovom tvare

```
ind / -perm 777
```

###### b) Doplňte riešenie v bode a) tak, aby chybové hlásenia boli presmerované do /home/{Váš domovský adresár}/errors

```
find / -perm 777 2>/home/{Váš domovský adresár}/errors
```

###### c) Doplňte riešenie v bode b) tak, aby sa zobrazilo prvé 3 riadky každého súboru

```
find / -perm 777 2>/home/{Váš domovský adresár}/errors -exec head -n 3 {} \;
```

##### 3.2 Spočítajte počet adresárov v adresári /etc v operačnom systéme Linux, ktorý ste si nainštalovali na domáce zariadenie

```
find /etc -type d | wc -l
```

##### 3.3

###### a) Vytvorte súbor `skuska1` a nastavte oprávnenia k tomu súboru tak, aby vlastník a ostatní mohli len čítať. Členovia skupiny nemajú žiadne oprávnenia. Použite sumárny oktalový zápis.

```
touch skuska1 | chmod 404 skuska1
```

###### b) Vytvorte súbor `skuska2` a nastavte oprávnenia k tomu súboru tak, aby vlastník mal všetky oprávnenia. Členovia skupiny a ostatní môžu len čítať. Použite sumárny oktalový zápis.

```
touch skuska2 | chmod 744 skuska2
```

###### c) Vytvorte súbor `skuska3` a nastavte oprávnenia k tomu súboru tak, aby oprávnenia k súboru skuska3 boli presne komplementárne k tým, aké ma vytvorený nový súbor (HINT: ak sčítate oprávnenia nového súboru a Vami nastavených oprávnení pre používateľa, skupinu a ostatných dostanete 7)

```
touch skuska3 | chmod 133 skuska3
```

##### 3.4

###### a) Vytvorte súbor `no-octal` a nastavte oprávnenia k tomu súboru tak, aby vlastník mal všetky oprávnenia. Členovia skupiny a ostatní môžu len čítať. V danej úlohe nesmiete použiť sumárny oktálový zápis.

```
touch no-octal | chmod no-octal u+rwx,g=r,o=r
```

###### b) Zabezpečte svoj domáci adresár (/home/{Vas_domovsky_adresar}) tak, aby v ňom ostatní užívatelia nemali žiadne oprávnenia až na výpis tohto adresára pomocou nástroja ls (nebude možné tam vstúpiť pomocou nástroja cd, ani vytvoriť súbor pomocou nástroja touch)

```
chmod o=r /home/{Vas_domovsky_adresar}
```

##### 3.5

###### a) Vytvorte si svojom domovskom adresári súbor secret. Nastavte k tomuto súboru ľubovoľné oprávnenia.

```
touch secret | chmod a=r secret
```

###### b) Následne nastavte k súboru secret oprávnenia tak, aby všetci okrem Vás na študentskom serveri dostávali pri príkaze cat /home/{Vas_domovsky_adresar}/secret chybové hlásenie "Permission denied". Pri tejto úlohe nesmiete použiť oktálový tvar pre oprávnenia.

```
chmod u=rwx,g=rw,o=rw secret
```

##### Bonus

##### Nástroj touch slúži nielen na vytvorenie súboru, ale aj na zmenu časových pečiatok súborov. Toto využívajú útočníci na oklamanie administrátorov pri bezpečnostných incidentoch.

###### a) vytvorte súbor narodeniny, zapíšte do tohto súboru aktuálny dátum a nastavte časovú pečiatku poslednej modifikácie tohto súboru na 31.12.1999

```
touch narodeniny | date > narodeniny
touch -d "1999-12-31" narodeniny
```

###### b) koľko a akých časových pečiatok máme v operačnom systéme Linux

V linuxe máme tri základné a jednu pridanú časovú pečiatku. sú to modification time ukazujúci na poslednú zmenu obsahu, change time ukazujúci na poslednú zmenu metadát, access time ukazujúci na posledné otvorenie alebo prečítanie súboru a nakoniec birth time zaznamenávajúci vytvorenie súboru v systéme.
