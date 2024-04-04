### x) Lue/katso ja tiivistä.

**Santos et al: The Art of Hacking (Video Collection): [..] 4.3 Surveying Essential Tools for Active Reconnaissance.**

- Videoissa kartoitetaan aktiivisen tiedustelun työkaluja. Aktiivisessa tiedustelussa hakkeri kerää tietoja tietomurron tekemiseksi.
- Erilaisten työkalujen käsittelyä ja toimintaperiaatteita.

**Hutchins et al 2011: Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains, chapters Abstract, 3.2 Intrusion Kill Chain.**

- Perinteiset verkkopuolustustyökalut, kuten tunkeutumisen havaitsemisjärjestelmät ja virustorjunta, keskittyvät tunnistamaan tiettyjä haavoittuvuuksia, mutta eivät riittävästi suojaamaan monimutkaisempia uhkia, kuten APT-hyökkäyksiä (Advanced Persistent Threat). APT:t ovat erittäin organisoituneita ja kokeneita toimijoita, jotka käyttävät edistynyttä teknologiaa ja taktiikoita saavuttaakseen päämääränsä.

- Tiedustelulähtöinen verkkopuolustus korostaa tarvetta ymmärtää tarkemmin uhkaajien toimintamalleja ja tavoitteita. Kill chain -mallin käyttö mahdollistaa hyökkäyksen eri vaiheiden hahmottamisen, minkä avulla puolustajat voivat kehittää tietotekniikkaan perustuvia puolustusmekanismeja, jotka estävät uusien tunkeutumisyritysten onnistumisen.

- Kill Chain -mallissa hyökkäys jaetaan useisiin vaiheisiin, kuten tiedustelu, aseistus, toimitus, hyväksikäyttö, asennus, komento ja valvonta sekä tavoitteiden toteuttaminen. Ymmärtämällä jokaisen vaiheen puolustajat voivat suunnitella vastatoimia estääkseen tunkeutumisen ennen sen tapahtumista.

- Toimintavaihtoehdot, kuten havaitseminen, kieltäminen, häiritseminen ja huijaaminen, auttavat puolustajia sovittamaan puolustuskykynsä vastaamaan uhkaajien toimintatapoja. Tämä strategia muodostaa jatkuvan syklin, jossa tietoa kerätään, uhkia analysoidaan ja oppeja sovelletaan puolustustoimenpiteisiin. Tämä auttaa parantamaan vastustuskykyä APT-uhkia vastaan, kohdentamaan resursseja tehokkaammin ja parantamaan puolustuksen tehokkuutta.




### e) Asenna Linux virtuaalikoneeseen. Suosittelen joko Kali (viimeisin versio) tai Debian 12-Bookworm.

![image](https://github.com/Ferresette/tunku/assets/148973799/4c8829e6-d0b3-4074-a242-9ab9536072ba)

Aloitin asentamalla ensiksi Kali Linuxin, koska ajattelin että pystyn sillä suorittamaan suurimman osan myös edellä olevista tehtävistä .


## a) Ratkaise Over The Wire: Bandit kolme ensimmäistä tasoa (0-2).

Aloitin suorittamaan ensimmäistä tehtävää, missä oli tarkoitus kirjautua ssh:n kautta kyseisellä sivulle. Se onnistui ja käytin Linux Kali:n terminaalia tässä.

![image](https://github.com/Ferresette/tunku/assets/148973799/e5b4c583-5dcc-46e9-ac50-6b6f0f01460d)

Ensimmäisen tehtävän suoritettuani siirryin seuraavaan, jossa piti readme filestä ottaa salasana. Käytin komentoa "cat readme" ja sain salasanan näkyviin.

![image](https://github.com/Ferresette/tunku/assets/148973799/4a5ea359-ad15-4d26-a4a8-94849557b411)

Käytin kyseistä salasanaa kirjautuakseen bandit1 käyttäjälle, samalla tavalla kun ensimmäisessä osiossa.

![image](https://github.com/Ferresette/tunku/assets/148973799/c7c546ff-f040-488f-9b09-565a395bda85)

Seuraava salasana on piilossa tiedostossa "-" mikä sijaitsee home directoryssa, lähdin selvittämään miten saan sen auki. 
Käytin komentoa "cat ./-" jotta sain auki tiedostosisällön ja sieltä löytyi tarvittava salasana.

![image](https://github.com/Ferresette/tunku/assets/148973799/1378e350-0888-47c7-b648-d6794b77f6ca)

Toimi samalla metodilla kun aikaisemmin, eli kirjauduin nyt bandit2:selle edellä mainitulla salasanalla.

![image](https://github.com/Ferresette/tunku/assets/148973799/3e4f1e49-3b52-431c-bf5e-ddbfa9cf1a38)

Seuraavaksi minun täytyi löytää salasana kansiosta: spaces in this filename. Käytin komentoa cat "spaces in this filename" ja sain salasanan onnistuneesti. Heittomerkkejä käytetään käsittääkseni sen takia jos tiedostossa on välilyöntejä.

![image](https://github.com/Ferresette/tunku/assets/148973799/2b8cb748-e348-4521-8f6c-1f44d6fece6c)








