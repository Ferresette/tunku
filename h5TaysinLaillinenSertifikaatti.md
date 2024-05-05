### x) Lue/katso ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva kustakin artikkelista. Kannattaa lisätä myös jokin oma ajatus, idea, huomio tai kysymys.)

  - OWASP 2021: OWASP Top 10:2021
     - A01:2021 – Broken Access Control (IDOR ja path traversal ovat osa tätä)
       
       Access controllin tarkoitus on estää käyttäjiä toimimaan oikeuksiensa ulkopuolella, välillä näissä on haavoittuvaisuuksia joten syntyy Broken Access Control.
       Muutama esimerkki käytetyistä haavoittuvaisuuksista on:
       - Pääsynvalvonnan tarkistusten ohittaminen, esimerkiksi URL:n muokkaamisen kautta tai hyödyntämällä API-pyynnön muokkausta.
       - API:n käyttö ilman asianmukaista pääsynvalvontaa POST, PUT ja DELETE-toiminnoille.
       - Toisen käyttäjän tilin tarkastelu tai muokkaus antamalla sen yksilöllinen tunniste.
      
         Kulunvalvonta on tehokasta vain luotetussa palvelinpuolen koodissa tai palvelimettomassa API:ssa, jossa hyökkääjä ei voi muokata kulunvalvontatarkistusta tai metatietoja.
         
     - A10:2021 – Server-Side Request Forgery (SSRF)

        - SSRF tapahtuu kun verkkosovellus noutaa etäresurssia vahvistamatta käyttäjän URL-osoitetta.
        - Hyökkääjä voi pakottaa sovelluksen lähettämään muotoilupyyntöjä kohteeseen, vaikka se olisi suojattu palomuurilla.
        - SSRF yleistyy pilvipalveluiden ja arkkitehtuurin monimutkaisuuden takia.

          Esimerkkihyökkäyksiä SSRF:

          - Porttiskannaus sisäisiin palvelimiin
          - Pääsy paikallisiin tiedostoihin tai palveluihin saadakseen herkkää tietoa
          - Pilvipalvelujen metatieto varastot

        **Karvinen 2020: Using New Webgoat 2023.4 to Try Web Hacking**

       - Webgoatilla voidaan suorittaa tunkeutumistestausta
       - Tarvitaan WebGoatia, Javaa sekä tietenkin porttia
       - Suositellaan käyttämään palomuuria tämän aikana

       

### a) Totally Legit Sertificate. Asenna OWASP ZAP, generoi CA-sertifikaatti ja asenna se selaimeesi. Laita ZAP proxyksi selaimeesi. Laita ZAP sieppaamaan myös kuvat, niitä tarvitaan tämän kerran kotitehtävissä. Osoita, että hakupyynnöt ilmestyvät ZAP:n käyttöliittymään. (Ei toimi localhost:lla ilman Foxyproxya)

Aloitin asentamalla OWASP ZAP:in virutaalikoneelleni:

    sudo apt-get update
    sudo apt install zaproxy

![image](https://github.com/Ferresette/tunku/assets/148973799/2dbc6f9a-5ebf-4771-8840-d7e5af130e72)

Aloin luomaan CA sertifikaattia.

![image](https://github.com/Ferresette/tunku/assets/148973799/9bcdfd89-8a3a-4480-bb11-b79ba86eec6a)

Tämän jälkeen tallensin luodun sertifikaatin desktopille, jotta löydän sen helposti.

![image](https://github.com/Ferresette/tunku/assets/148973799/18f70d04-5fe8-4e97-ad63-56d3303cea52)

Seuraavaksi lähdin asentamaan sertifikaattia selaimeeni. Selaimesta navigoin "Certificate Manager" osioon, mihin minun on tarkoitus importata aiemmin luotu sertifikaatti.

![image](https://github.com/Ferresette/tunku/assets/148973799/72eadb5b-2f6f-4f1c-86e5-85fb0e4e1d3b)

![image](https://github.com/Ferresette/tunku/assets/148973799/3ab91db5-0444-4f5b-8201-c9e4b9cdd7b1)

Ja näin, sertifikaatti on lisätty selaimeen.

![image](https://github.com/Ferresette/tunku/assets/148973799/52a6372b-5831-4463-b303-94acf8e7e5b3)

Seuraavaksi tarkoitus on laittaa ZAP proxyksi selaimeeni ja käytin Firefoxia tässä. Network settingsien kautta ja select manual proxy configuration. Localhost ja portti 8080, koska zap käyttää sitä automaattisesti.

![image](https://github.com/Ferresette/tunku/assets/148973799/e947197e-0184-4eea-b8ba-95e381b5934b)

Tehtävässä haluttiin, että ZAP sieppaisi myös kuvia. Kävin muokkaamassa ZAP:in asetuksista, että kuvat sallitaan. " Process images in HTTP requests/responds ".

![image](https://github.com/Ferresette/tunku/assets/148973799/21e8dfa5-41be-4142-b7a5-7670e11c9d06)

Kuten viimeisenä sanottiin, niin ei toimi localhostilla ilman FoxyProxya, joten siirryin tehtävään B, missä otetaan FoxyProxy käyttöön.

### b) Kettumaista. Asenna FoxyProxy Standard Firefox Addon, ja lisää ZAP proxyksi siihen. Käytä FoxyProxyn "Patterns" -toimintoa, niin että vain valitsemasi weppisivut ohjataan Proxyyn. (Läksyssä ohjataan varmaankin PortSwigger Labs ja localhost.)

FoxyProxy on Firefoxn Addon joka on avoimen lähteen proxyn hallintatyökalu. Kävin lataamassa sen virtuaalikoneeni Firefox selaimella https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/.

![image](https://github.com/Ferresette/tunku/assets/148973799/f016c552-a85f-4f17-b995-7e9a85fe5e84)

Tarkoituksena lisätä uusi proxy FoxyProxyyn, ja tässä tehtävässä haluttiin käyttää ZAP proxya. Eli FoxyProxysta auki Options --> Proxies --> Add. Lisäsin localhost ja ZAPin portin kyseisiin tietoihin.

![image](https://github.com/Ferresette/tunku/assets/148973799/7cf811da-52d6-41b7-a3a7-9fc676336cfb)

Alla olevassa kuvassa nähdään, että liikennettä kaapataan portswiggerin sivuilta.

![image](https://github.com/Ferresette/tunku/assets/148973799/16b5b4ac-1afb-460f-8c53-951f69d387f4)

Myös se, että kuvienkaappaminen näyttäisi onnistuvan.

![image](https://github.com/Ferresette/tunku/assets/148973799/600d30ce-12ed-4353-b743-8dd0a12a4a8b)

Lähdin kokeilemaan, miten patterns toimii FoxyProxyssa seuraavaksi. Laitan patterneihin portswiggerin sivuston ja localhostin. Kokeilen mennä saman aikaisesti muutamalle muulle sivulle.

![image](https://github.com/Ferresette/tunku/assets/148973799/77a665b0-93d7-43d7-ab18-cebe2a3bc8a7)


Tässä huomaa kun menen iltalehden sivulle, zappiin ei ilmesty mitään kun pattern on päällä.

![image](https://github.com/Ferresette/tunku/assets/148973799/97e58ed0-fd7c-4431-a944-0b9d233ab5e7)

Seuraavaksi koitan mennä portswiggerin sivuille, mikä löytyy kyseisestä patternista.

![image](https://github.com/Ferresette/tunku/assets/148973799/347e1bae-bcc3-485a-859c-a4d500f04192)

Kuten näkyy, portswiggerin sivustosta tulee tietoa ZAP:piin joten patternit tuntuisi toimivan oikein.

### PortSwigger Labs. Ratkaise tehtävät. Selitä ratkaisusi: mitä palvelimella tapahtuu, mitä eri osat tekevät, miten hyökkäys löytyi, mistä vika johtuu. Kannattaa käyttää ZAPia, vaikka malliratkaisut käyttävät harjoitusten tekijän maksullista ohjelmaa. Malliratkaisun kopioiminen ZAP:n tai selaimeen ei ole vastaus tehtävään, vaan ratkaisu ja haavoittuvuuden etsiminen on selitettävä ja perusteltava.

  - Insecure Direct Object Reference (IDOR)

### c) Insecure direct object references

Kun lähdin tekemään tehtävää, olin aivan kuistilla. Katsoin hieman suuntaa ohjeista mihin päin pitää lähteä. Tarkoituksena oli siis päästä kirjautumaan Carloksen tilille ja löytää siihen krendentiaalit sivustolta. Ohjeessa käskettiin käyttämään Live Chatia. Aloitin live chatin käymällä satunnaista keskustelua jotta saisin transcriptiä minkä tallentaa. Minulla oli ZAP päällä kokoajan, ja sinne ilmestyi paljon erilaisia pyyntöjä. Jokaisesta keskustelusta, mitä oli livechatissa oli historia Websocketissa. Ihmettelin, että miksi en löydä transciptiä sieltä. Historysta kun etsin tarkemmin siellä oli POST pyyntönä ladattu transcript. Tulostin aika monta transcriptiä, joten minulla se viimeisin näkyi 5.txt, ensimmäinen oli 2.txt. 

![image](https://github.com/Ferresette/tunku/assets/148973799/117c8bbd-cd1b-4bcc-9fb7-6647701700dc)

Nyt kun tätä miettii tarkemmin, jos jokaisesta keskustelusta jää historia ja mikä voidaan tallentaa transcriptiksi. Niin todennäköisesti minun ei ole ainut mikä on joskus tallennettu. Ladatut transcriptit on tallennettu tietyllä tavalla ja muuttamalla numeroa HTTP messageen on mahdollisuus nähdä myös muita scriptejä(jos siis ne tallennetaan tähän tyyliin). Eli tässä vaiheessa lähetin HTTP requestin, missä muokkasin transcripti tiedoston numeroa 5 --> 1. Vastauksena sain transcriptin, mikä oli tallennettanu 1.txt ja täällä näkyi "Carlosin" käymä keskutelu live chatissa.

![image](https://github.com/Ferresette/tunku/assets/148973799/9d7ce30f-60da-466b-987a-206851e3582c)

![image](https://github.com/Ferresette/tunku/assets/148973799/8d5cd2da-de3b-430f-a22b-cd3a9adc6501)

Kuten keskustelusta huomaa, Carlos on livechatissa sanonut unohtaneensa salasanan. Joten poimittiin se ylös ja lähdetään kokeilemaan.

![image](https://github.com/Ferresette/tunku/assets/148973799/14301cbe-3d7a-45f4-9a99-b02564b3ef0b)

Päästiin sisään carloksen tilille. Sanoisin, että ensimmäiseksi ehkä suurin virhe on siinä, että salasanoja ei pitäisi jakaa chat keskusteluissa. Normaalimpi käytäntö on lähettää ne sähköpostiin. Mutta kun kirjauduttiin carloksen tunnukselle, siinä vaaditaan heti päivittämään sähköpostiosoite mikä voisi jokseenkin selittää tätä vuotoa. Resurssit olivat siis ihan vapaassa käytössä, ja päästiin manipuloimaan tietoja eli pääsynhallinnan parantamista ehdottomasti tarvittaisiin.

- Path traversal
### d) File path traversal, simple case

Tarkoituksena tehtävässä oli löytää haavoittuvaisuuksia kuvista, ja muokkaamalla niiden parametrejä. Lähdin kokeilemaan painamalla kuvia ja ZAP:piin alkoikin ilmestyä pyyntöjä. Löysin kuviin liittyviä pyyntöjä hyvin nopeasti niitä klikattuani ja myös kuvien polun, mikä näytti seuraavalta:

    GET https://0a8800750330735d802b1721001300a9.web-security-academy.net/image?filename=22.jpg

Pienen pähkäilyn ja portswiggerin apujen jälkeen, ajattelin muokata kyseistä polkua tehtävässä annetulla esimerkillä requester tabissa. Aluksi kopioin kuvatiedoston tiedot requester tabiin:

![image](https://github.com/Ferresette/tunku/assets/148973799/89ef488a-31ff-46ee-8bca-98e02b0ce148)

Ja sen jälkeen vaihdoin "22.jpg" tilalle ../../../etc/passwd. Eli tarkoitus manipuloida kyseistä tiedostopolukua tässä tehtävässä, jolloin päästään juurihakemistosta arkaluontoisiin tietoihin käsiksi.

![image](https://github.com/Ferresette/tunku/assets/148973799/2410b0a6-9e86-40dc-a072-dc38ec15b2dd)

### e) File path traversal, traversal sequences blocked with absolute path bypass

Hyvin samantyylinen tehtävä kun edellinen, käytettiin vain absoluuttista polkua saadakseen arkaluontoiset tiedot käsiimme. Eli 3.jpg korvattiin /etc/passwd.

![image](https://github.com/Ferresette/tunku/assets/148973799/0761240c-e696-4948-bf6a-02b27ef8c265)

Ja sieltä päästiin käsiksi tietoihin.

![image](https://github.com/Ferresette/tunku/assets/148973799/5f5a636a-186e-4947-bc9f-8f34d6c1a6b4)

![image](https://github.com/Ferresette/tunku/assets/148973799/7b6d4f4c-8d82-4662-bd65-b80f9dab1db1)


### f) File path traversal, traversal sequences stripped non-recursively

Taas mennään samalla linjalla, manipuloidaan tiedostopolkua vain hieman eritavalla. Käsittääkseni, kun lisätään tälläinen tiedostopolku niin merkkijonot poistetaan vain kerran ja ei jatka merkkijonojen poistoja, milloin päästiin taas käsiksi arkaluontoiseen tietoon.

![image](https://github.com/Ferresette/tunku/assets/148973799/0a0baa4a-11de-4886-8968-be4dcbeb26dc)

![image](https://github.com/Ferresette/tunku/assets/148973799/6bd318a1-b966-40df-b84e-e74b88db833d)

![image](https://github.com/Ferresette/tunku/assets/148973799/0b63b390-e106-4283-bcfa-98050f6208d4)


- Server Side Request Forgery (SSRF)

### h) Basic SSRF against the local server

SSRF:ssä tarkoitus manipuloida sovelluksen lähettämiä HTTP pyyntöjä ja saada sitä kautta kyseiset pyynnöt lähetettyä sisäisille tai luotettaville palvelimille. Tässä tarkoituksena saada pyynnöt lähetettyä paikalliselle palvelimelle ja poistaa käyttäjä carlos. Tehtävässä käskettiin tarkastelemaan varastosaldoja, mistä saataisiin mielenkiintoisia GET pyyntöjä. 

![image](https://github.com/Ferresette/tunku/assets/148973799/001f6960-3f69-4619-bdac-63b6a7c6f913)

Varastosaldo pyyntö löydetty ZAP:ista. Seuraavaksi pyyntöä pitäisi muokata requester tabissa, jotta saataisiin pyynnöt kohteeseen /localhost/admin. Minkä kautta päästäisiin adminille tuhoamaan carlos.

![image](https://github.com/Ferresette/tunku/assets/148973799/c5267767-7603-424a-866d-bfad225c6488)

wiineri ja carlos löytyi responsesta!

![image](https://github.com/Ferresette/tunku/assets/148973799/e1a516d7-2897-47ee-9ccd-c5fa2b90318b)

Carlosin vuoro lähteä, sorry buddy.

![image](https://github.com/Ferresette/tunku/assets/148973799/09f95112-6d47-4101-acc1-61790b4a97ce)

![image](https://github.com/Ferresette/tunku/assets/148973799/dca058a8-5963-49f7-97ee-ee4287c2ab17)

- Cross Site Scripting (XSS)


### i) Reflected XSS into HTML context with nothing encoded

Käsitellään käyttäjän haitallista syötettä, tässä käytetään javascript koodia haitallisena koodina, mikä pitäisi sisältyä html-vastaukseen. Eli opetuksena olisi sovelluksen oikea oppinen syötteen validointi ja pyrkiä käyttämään turvallisia koodausmenetelmiä. Kokeilin ensiksi vain kirjottaa jotain, että näkisin miltä tulostus näyttää.

![image](https://github.com/Ferresette/tunku/assets/148973799/276083d6-e6e2-45bd-b211-e9fc0691d939)

Ei tulosta! Kokeillaan tehtävänannossa tarjottua koodin pätkää sen sijaan, minkä jälkeen homma näyttäisi taas pelittävän.

![image](https://github.com/Ferresette/tunku/assets/148973799/7bb0731a-0995-48cd-9d02-49c1640ee3fc)

![image](https://github.com/Ferresette/tunku/assets/148973799/a1b8cb06-dd8c-4767-bc2f-e357e818dc27)


### j) Stored XSS into HTML context with nothing encoded

Samankaltainen kun edellinen, mutta tässä tallennetaan sovelluksen tietokantaan ja toistetaan myöhemmin käyttäjän selaimessa. Eli haitallinen koodi sisällytetään HTML-vastaukseen käsittääkseni.
Täytettiin kommenttikenttään esimerkki koodinpätkä, lisättiin nimi ja sähköposti.

![image](https://github.com/Ferresette/tunku/assets/148973799/d669febe-9a40-497a-a0f8-63dfad63592c)

![image](https://github.com/Ferresette/tunku/assets/148973799/e09b7d02-f978-469f-955c-4d6e1fcec281)
























       
