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

Lähdin kokeilemaan, miten patterns toimii FoxyProxyssa seuraavaksi. Laitan patterneihin portswiggerin sivuston ja kokeilen mennä saman aikaisesti muutamalle muulle sivulle. 











       
