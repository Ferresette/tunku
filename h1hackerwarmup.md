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


### a) Ratkaise Over The Wire: Bandit kolme ensimmäistä tasoa (0-2).

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

### b) Asenna WebGoat ja kokeile, että pääset kirjautumaan sisään.

Aloitin tutustumalla https://terokarvinen.com/2024/eettinen-hakkerointi-2024/#h1-hacker-warmup WebGoatin asennukseen, sivuilla neuvottiin asentamaan java ympäristö. Tarkistin asian java -version komennolla ja minulta näkyi löytyvän se jo niin siirryin eteenpäin. 

![image](https://github.com/Ferresette/tunku/assets/148973799/ee35155b-ffdc-4cab-bd91-a321dd9b41e3)

Lähdin tarkistamaan palomuuri asetuksia ja selvisi ettei palomuuria ollut joten asensin sen ja laitoin päälle.

![image](https://github.com/Ferresette/tunku/assets/148973799/44135029-7396-416d-a006-06940131abc2)

![image](https://github.com/Ferresette/tunku/assets/148973799/6a07e5c9-947e-40b1-91dd-a05f3c745880)

Vaihdoin myös Shared clipboard sekä Drag and dropin bidirectionaliksi, joten minun on helpompi kopioida asioita Kali Linuxiin. Seuraavaksi hyödynsin teron sivuilla olevaa linkkiä WebGoatin asennukseen.

    $ wget https://terokarvinen.com/2020/install-webgoat-web-pentest-practice-target/webgoat-server-8.0.0.M26.jar
    $ java -jar webgoat-server-8.0.0.M26.jar

Asennuksien jälkeen aloitin rekistöröitymisen WebGoat sivustolle, jotta pääsen käsiksi harjoituksiin.

![image](https://github.com/Ferresette/tunku/assets/148973799/14b65911-e09f-44c4-bcac-7d6329e88be7)

Rekistöröityminen onnistunut, seuraavaksi tehtävien pariin.

![image](https://github.com/Ferresette/tunku/assets/148973799/87594d2c-7c99-4605-a1f7-27ef53acc947)

### c) Ratkaise WebGoatista tehtävät "HTTP Basics" ja "Developer tools". Katso vinkit alta.


**HTTP BASICS**

Kyseisen tehtävän suorittaminen oli aika yksinkertainen, ensimmäisessä osassa piti vaan kirjoittaa nimi minkä jälkeen se näkyi käänteisenä. Toisessa tehtävässä piti selvittää onko kyseessä POST vai GET
komento. Sain sen selvillä tutkimalla elementtejä ja sieltä siirtymällä networkiin. Sieltä näkyy kaikki tehdyt pyynnöt sivulla, mistä sain selville että kyseessä oli POST komento. Tämän jälkeen aloin tutkia parametrejä selvittääkseni vastaukseksi vaaditun magic numberin, mikä löytyi parametri pyynnöistä aika nopeasti.

![image](https://github.com/Ferresette/tunku/assets/148973799/e13a6341-c48a-4cb8-bf33-e4a1845c05df)

**DEVELOPER TOOLS**

Tässä tehtävässä piti käyttää developer toolsin consolea, saadakseen oikean vastauksen. Kirjoitin konsoliin annentun koodin ja se tulosti sieltä vastauksen, mistä sain numerosarjan tehtävän ratkaisemiseksi.

![image](https://github.com/Ferresette/tunku/assets/148973799/8158962a-1a0b-4335-8308-1249e8f259ce)

Seuraava tehtävä tässä osiossa toimi hyvin samalla tavalla kun HTTP Basiceissa, eli lähetettiin pyyntö, mikä etsittiin ja sen parametreistä saatiin tarvittava numero vastaukseksi.

![image](https://github.com/Ferresette/tunku/assets/148973799/5866a57c-8348-4d7b-9e06-48aec5292ac0)

### d) Ratkaise ja selitä PortSwigger Labs: Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data.

Lähdin suorittamaan tehtävää ensiksi rekistöröitymällä sivustolle. SQL Injectio ei ollut lähtökohtaisesti itselle hirveän tuttua, tiesin jotenkin miten SQL koodia kirjoitetaan.
Löysin https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data sivustolta hyvän ohje videon, missä selitettiin kyseinen tehtävä aika perinpohjaisesti ja siitä sai vähän selkeyttä.
Tämän jälkeen sain tehtävän suoritettua onnistuneesti. Tarkoituksena tehtävässä oli löytää haavoittuvaisuuksia ja muokkaamalla osoitekenttää saatiin esille piilotettua dataa aika helposti.

![image](https://github.com/Ferresette/tunku/assets/148973799/910d7a01-85b6-4145-8f23-dfb35c71d65e)

### f) Porttiskannaa 1000 tavallisinta tcp-porttia omasta koneestasi (localhost). Analysoi tulokset.

Suoritin tehtävän samassa ympäristössä missä aikaisemmat eli Kali Linuxin terminaalissa. Käytin komentoa:

        nmap 127.0.0.1

![image](https://github.com/Ferresette/tunku/assets/148973799/3c52ed16-9964-4184-96d9-52e63fe4cdac)

- Ensimmäinen rivi kertoo sivuston mistä voi ladata nmapin, ajan millon se on käynnistetty sekä versionumeron.
- Toinen rivi kertoo tavoiteltun ip-osoitteen ja myös dns:än jos sellainen löytyisi.
- Kolmannella rivillä kerrotaan että Host on up ja sen vasteajan
- Neljännellä rivillä selviää, että kaikki 1000 porttia on tilassa ignored
- Viidennellä rivillä kerrotaan, että kaikki 1000 porttia löytyy mutta ne on suljettuna
- Viimeinen rivi viestii siitä, että nmap komento on suoritettu ja missä ajassa


### g) Porttiskannaa kaikki koneesi (localhost) tcp-portit. Analysoi tulokset.

Kaikki portit sain skannattua komennolla:

        sudo nmap -p- 127.0.0.1

Muuten näkyi aikalailla samat tulokset, paitsi nyt näkyvillä oli kaikki mahdolliset portit.

![image](https://github.com/Ferresette/tunku/assets/148973799/34e39170-9462-4793-ad72-a1f3994c2358)

### h) Tee laaja porttiskanaus (nmap -A) omalle koneellesi (localhost), kaikki portit. Selitä, mitä -A tekee. Analysoi tulokset.

Käytin komentoa:

        sudo nmap -A -p- 127.0.0.1

Kyseinen nmap -A komento tekee aggressiivisen porttiskannauksen kaikille porteille koneella. Tällä saa lisätietoa käyttöjärjestelmästä, palveluista, auki olevista porteista ja haavoittuvaisuuksista.
Tehtävässä oisin saanut varmaan laajemmat tulokset, jos en olisi käyttänyt virtuaalikonetta, mutta löysin muutamalta nettisivulta hyvät esimerkit minkälaista informaatiota tulisi näkyviin.

### i) Asenna demoni tai pari (esim Apache ja SSH). Vertaile, miten localhost:n laajan porttiskannauksen tulos eroaa.

Aloitin asentamalla Apache HTTP serverin ja SSH palvelun Kali Linuxiin.

        sudo apt update
        sudo apt install apache2
        sudo systemctl start apache2

        sudo apt update
        sudo apt install openssh-server
        sudo systemctl start ssh

![image](https://github.com/Ferresette/tunku/assets/148973799/826dbbc3-5acb-4d6e-8cf5-cf0f4b4f5e71)

Yllä olevassa näkyy nyt kun laaja porttiskannaus on suoritettu sen jälkeen kun Apache serveri ja palvelin on ladattu.
Erovaisuutena nyt näen avoimena olevia portteja, mitä kyseiset serverit ja palvelimet käyttävät. Myös erilaiset salausmenetelmät tulivat näkyviin.

### j) Kokeile ja esittele jokin avointen lähteiden tiedusteluun sopiva weppisivu tai työkalu.

Etsin https://inteltechniques.com/tools/index.html sivustolta itseäni kiinnostavan työkalun, ja käytin IP Lookup työkalua.

Syötin Googlen ip-osoitteen 8.8.8.8 ja sen jälkeen sain seuraavat tiedot näkyyvin.

![image](https://github.com/Ferresette/tunku/assets/148973799/a023ac2f-9681-4c65-a492-86e8f7485e22)



## References

https://terokarvinen.com/2024/eettinen-hakkerointi-2024/#h1-hacker-warmup
https://nmap.org/book/port-scanning-tutorial.html
https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data
https://www.iplocation.net/ip-lookup
https://overthewire.org/wargames/bandit/bandit1.html
https://phoenixnap.com/kb/how-to-install-kali-linux-on-virtualbox
https://chat.openai.com
























