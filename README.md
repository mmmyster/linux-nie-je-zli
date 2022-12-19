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

##### 2.1: Pomocou jedného príkazu (vrátane vhodných prepínačov) vytvorte niekoľko adresárov v štruktúre /home/{Váš domovský adresár}/ZLI/domov/uloha.

```
mkdir -p ~/ZLI/domov/uloha
```

##### 2.2

###### a) z domovského adresára pomocou relatívnej cesty zobrazte obsah adresára `/etc/apt/`

```
ls ../../etc/apt
```

###### b) z domovského adresára pomocou absolútnej cesty zobrazte obsah adresára `/etc/apt/`

```
ls /etc/apt
```

###### c) vysvetlite na vyššie uvedených úlohách rozdiel medzi relatívnou a absolútnou cestou

Relatívna cesta je vizaná na pwd, čiže na miesto, kde sa práve nachádzame. Na druhej strane absolútna cesta sa viaže na koreňový adresár.

##### 2.3: Vypíšte mená užívateľov (prvý stĺpec v súbore `/etc/passwd`) usporiadaný v abecednom poradí.

```
cut /etc/passwd -d : -f 1 | sort
```

###### a) zobrazte 3.,5. a 7. stĺpec súboru /etc/passwd

```
cut /etc/passwd -d : -f 3,5,7
```

###### b) zobrazte 15. až 30. riadok a súčasne 3.,5. a 7. stĺpec súboru /etc/passwd

```
cut /etc/passwd -d : -f 3,5,7 | head -n 30 | tail -n 16
```

###### c) spočítajte počet znakov a slov vo výbere riadkov a stĺpcov podľa bodu b) (Hint: wc má prepínače na slová a znaky, pozrite manuálové stránky)

```
cut /etc/passwd -d : -f 3,5,7 | head -n 30 | tail -n 16 | wc -m -w
```

##### 2.4: Vymyslite zadanie, pri ktorom bude nutné použiť pipe (rúru) a minimálne nástroje sort, uniq, grep (zadanie sa nesmie zhodovať s úlohou na hodine).

Každý rok sa zverejňujú štatistiky o najpopulárnejších menách pre bábätká. V rokoch 2002/2003 patrili na prvé miesta mená martin, michal, matej, michaela. Určite ste si všimli, že majú niečo spoločné. presne tak. Všetky začínajú písmenom m. Vypíšte teda z adresára /etc/passwd na študentskom serveri prvých desať najpoužívanejších mien s počiatočným písmenom m, ku každému menu vypíšte počet jeho výskytov a zoraďte od mena s najvyšším počtom.

```
cut /etc/passwd -d _ -f 1 | grep ^m | sort | uniq -c | sort -n -r | head
```

##### 2.5

###### a) nájdite na študentskom serveri (s.ics.upjs.sk) všetky súbory, ktorých názov obsahuje slovné spojenie conf, ich veľkosť je maximálne 20 MB

```
find / -name "*conf*" -size -20M 2>/dev/null/
```

###### b) doplňte riešenie v bode a) tak, aby ste o každom nájdenom súbore vypísali informácie o súbore (HIND: nástroj ls má prepínač pre podrobné informácie o súboroch a adresároch, použite manuálové stránky), akú veľkosť majú tieto súbory?

```
find / -name "*conf*" -size -20M 2>/dev/null -exec ls -lh {} \; | cut -d " " -f 5
```

###### c) upravte riešenie v bode b) tak, aby ste zobrazili prvých 5 riadkov každého súboru

```
find / -name "*conf*" -size -20M 2>/dev/null -exec head -n 5 {} \;
```

##### Bonus

###### a) vysvetlite, čo je jadro (kernel) operačného systému Linux

Kernel je jadro každého operčného systému. Linux kernel je vlastne to, čo zjednodušene voláme Linux.

###### b) zistite distribúciu a verziu jadra operačného systému Linux, ktorý ste si nainštalovali na domácom zariadení (uveďte príkaz, ako ste to zistili)

```
cat /etc/os-release
```

---

### DOMÁCA ÚLOHA Č. 3

##### 3.1

###### a) nájdite na študentskom serveri (s.ics.upjs.sk) všetky súbory, ktoré majú oprávnenia v777 v oktálovom tvare

```
ind / -perm 777
```

###### b) doplňte riešenie v bode a) tak, aby chybové hlásenia boli presmerované do /home/{Váš domovský adresár}/errors

```
find / -perm 777 2> ~/errors
```

###### c) doplňte riešenie v bode b) tak, aby sa zobrazilo prvé 3 riadky každého súboru

```
find / -perm 777 2> ~/errors -exec head -n 3 {} \;
```

##### 3.2: Spočítajte počet adresárov v adresári /etc v operačnom systéme Linux, ktorý ste si nainštalovali na domáce zariadenie.

```
find /etc -type d | wc -l
```

##### 3.3

###### a) vytvorte súbor `skuska1` a nastavte oprávnenia k tomu súboru tak, aby vlastník a ostatní mohli len čítať, členovia skupiny nemajú žiadne oprávnenia (použite sumárny oktalový zápis)

```
touch skuska1 | chmod 404 skuska1
```

###### b) vytvorte súbor `skuska2` a nastavte oprávnenia k tomu súboru tak, aby vlastník mal všetky oprávnenia, členovia skupiny a ostatní môžu len čítať (použite sumárny oktalový zápis)

```
touch skuska2 | chmod 744 skuska2
```

###### c) vytvorte súbor `skuska3` a nastavte oprávnenia k tomu súboru tak, aby oprávnenia k súboru skuska3 boli presne komplementárne k tým, aké ma vytvorený nový súbor (HINT: ak sčítate oprávnenia nového súboru a Vami nastavených oprávnení pre používateľa, skupinu a ostatných dostanete 7)

```
touch skuska3 | chmod 133 skuska3
```

##### 3.4 V danej úlohe nesmiete použiť sumárny oktálový zápis.

###### a) vytvorte súbor `no-octal` a nastavte oprávnenia k tomu súboru tak, aby vlastník mal všetky oprávnenia, členovia skupiny a ostatní môžu len čítať

```
touch no-octal
chmod u+rwx,g=r,o=r no-octal
```

###### b) zabezpečte svoj domáci adresár (/home/{Vas_domovsky_adresar}) tak, aby v ňom ostatní užívatelia nemali žiadne oprávnenia až na výpis tohto adresára pomocou nástroja ls (nebude možné tam vstúpiť pomocou nástroja cd, ani vytvoriť súbor pomocou nástroja touch)

```
chmod o=r ~
```

##### 3.5 Pri tejto úlohe nesmiete použiť oktálový tvar pre oprávnenia.

###### a) vytvorte si svojom domovskom adresári súbor secret. Nastavte k tomuto súboru ľubovoľné oprávnenia.

```
touch secret
chmod a=r secret
```

###### b) následne nastavte k súboru secret oprávnenia tak, aby všetci okrem Vás na študentskom serveri dostávali pri príkaze cat /home/{Vas_domovsky_adresar}/secret chybové hlásenie "Permission denied"

```
chmod u=rwx,g=rw,o=rw secret
```

##### Bonus: Nástroj touch slúži nielen na vytvorenie súboru, ale aj na zmenu časových pečiatok súborov. Toto využívajú útočníci na oklamanie administrátorov pri bezpečnostných incidentoch.

###### a) vytvorte súbor narodeniny, zapíšte do tohto súboru aktuálny dátum a nastavte časovú pečiatku poslednej modifikácie tohto súboru na 31.12.1999

```
touch narodeniny
date > narodeniny
touch -d "1999-12-31" narodeniny
```

###### b) koľko a akých časových pečiatok máme v operačnom systéme Linux

V linuxe máme tri základné a jednu pridanú časovú pečiatku. sú to modification time ukazujúci na poslednú zmenu obsahu, change time ukazujúci na poslednú zmenu metadát, access time ukazujúci na posledné otvorenie alebo prečítanie súboru a nakoniec birth time zaznamenávajúci vytvorenie súboru v systéme.

---

### DOMÁCA ÚLOHA Č. 4

##### 4.1: Vypíšte všetky procesy na Vašom virtuálnom stroji:

###### a) spustené pod používateľom root vo formáte: ID rodičovského proces, ID procesu, commandline spusteného príkazu

```
ps -u root -o "ppid,pid,cmd"
```

###### b) spustené pod používateľom root a usporiadajte ich podľa veľkosti použitej pamäte od najväčšej po najmenšiu

```
ps u -u root --sort -rss
```

##### 4.2: Vypíšte všetky procesy bežiace v operačnom systéme a usporiadajte ich podľa veľkosti použitej pamäte od najväčšej po najmenšiu (HINT: použite manuálové stránky príkazu ps).

```
ps aux --sort -rss
```

##### 4.3: V adresári /etc nájdite všetky súbory s príponou .conf a usporiadajte ich podľa počtu riadkov, ktoré obsahujú.

```
find /etc -name "*.conf" -exec wc -l {} + | sort -rn
```

##### 4.4: Spočítajte počet písmen (HINT: prepínač -m) v časti súboru /etc/passwd, pre ktorý platí:

###### a) riadky neobsahujú slovo bash

```
cat /etc/passwd | grep -v bash | wc -m
```

###### b) riadky obsahujú slovo home, ale neobsahujú slovo nologin a stĺpce obsahujú názov používateľa, domovský adresár a shell

```
cat /etc/passwd | grep home | grep -v nologin |  wc -m
```

###### c) stĺpec popisuje poznámky o používateľoch

##### Bonus: Vysvetlite, čo sú signály. Signály majú svoje čísla. Na konkrétnom príklade vysvetlite rozdiel medzi signálmi 9,15,19.

Signál je špeciálna správa zaslaná procesu. Je asynchrónny, takže ho proces vybaví okamžite, bez čakania na dokončenie aktuálnej funkcie.

`SIGKILL` (9) je na okamžitú, ale nie veľmi čistú termináciu

```
kill -9 pid
```

`SIGTERM` (15) sa zvyčajne odošle keď použijeme `kill`

```
kill pid
```

`SIGSTOP` (19) je na "pozastavenie" procesu s možnosťou nekôr znova spustiť s `SIGCONT` (18)

```
kill -19 pid
```

---

### DOMÁCA ÚLOHA Č. 5

##### 5.1: V rámci svojho operačného systému spočítajte:

###### a) počet nainštalovaných balíčkov

```
apt list --installed | wc -l
```

###### b) počet balíčkov, ktoré je možné aktualizovať (upgradovať)

```
apt list --upgradable | wc -l
```

##### 5.2: Vyhľadajte v celom operačnom systéme súbory a následne vykonajte konkrétnu činnosť:

###### a) vyhľadajte súbory, ktorých veľkosť presahuje 300MB a zmeňte týmto súborom vlastníka a skupinu na root:root

```
find / -size +300M 2> /dev/null -exec chown root:root {} \;
```

###### b) vyhľadajte súbory, ktoré sa končia na príponu conf a zmeňte oprávnenia k týmto súborom na 770

```
find / -name "*.conf" 2> /dev/null -exec chmod 770 {} \;
```

##### 5.3: Jednorázovo naplánujte:

###### a) reštart systému o 3 hodiny od času zadania úlohy

```
echo "reboot" | at now + 3 hours
```

###### b) reštart systému 20.12.2022 o 15:20

```
b) echo "reboot" | at 15:20 122022
```

##### 5.4:

###### a) vytvorte tar archív z adresára `/etc` a uložte ho do domovského adresára pod názvom "zaloha.tar.gz"

```
sudo tar -czvf zaloha.tar.gz /etc
```

###### b) vytvorte zip archív z adresára `/var` a uložte ho do domovského adresára pod názvom "zaloha.zip". (Doinštalujte príslušný balík, ak je potrebný na splnenie tohto zadania)

```
sudo zip -r zaloha.zip /var
```

##### Bonus: Nainštalujte program git (vhodný balík nájdite v repozitáre balíčkov). Nainštalujte program nmap z tohto zdroja: https://github.com/nmap/nmap. Postup inštalácie popíšte. (HINT: Na webovom odkaze vpravo hore klik na zelené Code a v časti Local - Clone nájdete dokaz na repozitár.)

```
sudo apt-get install git
git clone https://github.com/nmap/nmap
cd nmap
./configure
make
make install
```
