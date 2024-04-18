## x) Lue/katso ja tiivistä.

- *Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf*
  
   Fuff on työkalu, jota käytetään piilossa olevien verkkokansioiden etsimiseen. 
  
- *Karvinen 2022: Cracking Passwords with Hashcat*

  Hashcatilla voidaan murtaa salasanoja. Järjestelmät eivät tallenna alkuperäisiä salasanoja, vaan niiden tiivistettä eli hashia.
  Hashaus on yksisuuntainen toiminto, joten salasanaa ei voi palauttaa siitä takaisin.
  
- *Karvinen 2023: Crack File Password With John*

  John the Ripper on avoimen lähdekoodin salasanan murtamistyökalu, sillä voi esimerkiksi murtaa salasanoja, jotka sijaitsevat ZIP tiedostoissa.


  ## a) Asenna Hashcat ja testaa sen toiminta murtamalla esimerkkisalasana.

  Lähdin asentamaan Hashcatia Teron sivuilta olevilla ohjeilla. Käytin seuraavia komentoja:

      sudo apt-get update
  
      sudo apt-get -y install hashid hashcat wget

  ![image](https://github.com/Ferresette/tunku/assets/148973799/65815737-116a-4e86-a1f7-90a88958aa51)

  Hashcat näytti jo löytyvän Kalista valmiiksi.

  Aloin testaamaan Hashcatin toimintaa ja miten sillä voisi murtaa salasanoja. Ensiksi loin kirjaston seuraavilla komennoilla:

      mkdir hashed
      cd hashed

  ![image](https://github.com/Ferresette/tunku/assets/148973799/9d752e55-3428-4b62-bdcd-7fc676ca6aee)

  Löysin Teron sivuilta suositun kirjaston, mitä ajattelin käyttää tehtävän suorittamiseksi. Latasin kirjaston aikaisemmin tehtyyn hakemistoon seuraavilla komennoilla:

      wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz (Lataa kirjaston rockyou.txt.tar.gz)
  
      tar xf rockyou.txt.tar.gz (purkaa kyseisen tiedoston)
  
      rm rockyou.txt.tar.gz (poistaa kyseisen tiedoston)

  ![image](https://github.com/Ferresette/tunku/assets/148973799/49002af3-63f2-47f1-932b-737891d9a284)

  ![image](https://github.com/Ferresette/tunku/assets/148973799/2e8bed9f-dc74-426f-9b69-86768eed9b34)

  Lähdin kokeilemaan salasanan murtamista Terolla oli hyvät ohjeet, joten jatkoin sitä rataa. Seuraavalla komennolla:

      hashid -m 6b1628b016dff46e6fa35684be6acc96

  ![image](https://github.com/Ferresette/tunku/assets/148973799/6e44670a-1ee5-4688-9fc2-e226d6793dd6)

  Analysoi kyseisen hashin sen moden ja hash id:n perusteella.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/f87108af-db45-4bb4-9af8-4fc2c639d4cf)

  Tämä komento käynnistää hashcatin ja aloittaa murtautumaan käyttäen tiivistettä ja sanalistaa rockyou.txt. Tallentaen ne solved kansioon.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/f98a7da6-1f93-4320-b747-80d09e023ce0)

  ![image](https://github.com/Ferresette/tunku/assets/148973799/a064586d-9bba-4733-93d6-02962b4accd6)

  Tässä vielä lopuksi näkyy kun käytän komentoa:

      cat solved~

  ![image](https://github.com/Ferresette/tunku/assets/148973799/ce886065-cde7-4f3c-b04c-c7750ee739f4)

  ## b) Salainen, mutta ei multa. Ratkaise dirfuzt-1 artikkelista Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf

  Aloin suorittamaan tätä tehtävää ohjeessa annetulta sivustolta.

  
  ![image](https://github.com/Ferresette/tunku/assets/148973799/229ee161-4750-4e85-b105-f22cdf59bff4)

  Latasin teron sivuilta hakemiston ja sen jälkeen vaihdoin käyttöoikeudet siten, että käyttäjällä on suoritusoikeudet. Sain ip-osoitteen, mitä kokeilin seuraavaksi selaimella.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/ef2a8e2e-e269-4704-9d67-e8de30ca0ccf)

  Sivustolta tuli esiin haluttu näkymä, jonka jälkeen aloin asentamaan ffuffia.

      $ wget https://github.com/ffuf/ffuf/releases/download/v2.0.0/ffuf_2.0.0_linux_amd64.tar.gz
      $ tar -xf ffuf_2.0.0_linux_amd64.tar.gz
      $ ./ffuf

  ![image](https://github.com/Ferresette/tunku/assets/148973799/60049dac-217d-4cd7-9c54-df0db01a1c37)

  ![image](https://github.com/Ferresette/tunku/assets/148973799/142ee964-5a0a-409c-add8-cf99c4a5331c)

  Seuraavaksi tarvitaan kirjastoa, onneksi teron sivuilta löytyi valmis kirjasto samalta tekijältä mitä hyödynnettiin aikaisemmassa tehtävässä.

      $ wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt

  ![image](https://github.com/Ferresette/tunku/assets/148973799/34a35f34-dc55-44fe-81a9-f66960649299)

  Aloin uudella shellillä kokeilemaan fuzzaamista teron esimerkkisivustoon:

      $ ./ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ

  ![image](https://github.com/Ferresette/tunku/assets/148973799/de53a20e-87cf-49df-a56d-a071afe9648b)

  ![image](https://github.com/Ferresette/tunku/assets/148973799/c13b91a5-2f02-41dc-8e37-ffe8306eab0c)


  Fuzzaaminen onnistui ja löytyi paljon dataa. Sivu mitä fuzzattiin sekä wordlist ja 4727 kohdetta.

  Tämän jälkeen filtteröin 132 bytesiin, jotta tulosten määrä pienentyisi.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/06b5aa3e-3773-41aa-96db-455f271ce74c)

  Kyseinen filtteröinti pienensi huomattavasti tuloksia. Sinne jäi nyt kaksi kohdetta, Admin sekä google.com. Lisäsin teron esimerkkisivuston URLiin adminin perään ja tämä tehtävä onnistui.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/d25e2292-fe19-4cc1-8214-d7af0a8e56cc)

  ### Your turn - Challenge

  Aloitin tekemään haastetta. Suoritin samat toimenpiteet mitä harjoituksissa, mutta vaihdoin vain dirfuzt-0 dirfuzt-1:seksi.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/b402fba3-4d05-485c-9e87-204af8ba1232)

  Kuvassa näkyy suoritetut komennot, sekä nettiselaimen näkymä.

  Avasin uuden shellin ja asensin kirjaston uudelleen.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/cc6feb71-c7b8-4164-b8ca-6a2d703a15aa)

  Tämän jälkeen aloitin taas fuzzaamisen.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/b5928333-65a7-4567-a721-e4910e4609de)

  ![image](https://github.com/Ferresette/tunku/assets/148973799/786b4d67-aa2f-4fad-9540-ba3fea43592b)

  Tulokset olivat aika samanlaisia kuin aiemmassa harjoituksessa, kiinnitin kuitenki huomiota 154 bytesiin, joten päätin filtteröidä sillä.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/d4c35e10-071d-4d06-a490-ea0744afdbce)

  ![image](https://github.com/Ferresette/tunku/assets/148973799/918a8517-e678-48e7-8b64-a474b087caf8)

  Sieltä löytyikin sitten tarvittavia aineksia tehtävän ratkaisemiseksi, kokeillaan wp-adminia URLiin selaimessa.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/b713cf00-102b-4725-8606-efbe3dcb821f)

  Kappas keppanaa.

  ## c) Asenna John the Ripper ja testaa sen toiminta murtamalla jonkin esimerkkitiedoston salasana.

  Lähdin tutkimaan https://terokarvinen.com/2023/crack-file-password-with-john/ sivustolta John the Ripperistä.

  Aloitin asentamalla tarvittavat työkalut johnin käyttöön.

      $ sudo apt-get update
      $ sudo apt-get -y install micro bash-completion git build-essential libssl-dev zlib1g zlib1g-dev zlib-gst libbz2-1.0 libbz2-dev atool zip wget

  ![image](https://github.com/Ferresette/tunku/assets/148973799/935b482e-5c0b-4923-bca0-a9a9ffef13b6)

  Seuraavaksi itse johnin asennus.

      $ git clone --depth=1 https://github.com/openwall/john.git

  ![image](https://github.com/Ferresette/tunku/assets/148973799/24fff7ca-705c-41e9-9e96-3fea9cd3a62b)

  Aloitin johnin konfiguroinnin.

      $ cd john/src/
  
      $ ./configure

  ![image](https://github.com/Ferresette/tunku/assets/148973799/c34bec40-b673-48eb-b44b-080a9229f6e4)

  Asennusskriptin asensin seuraavalla komennolla:

      ./configure && make -s clean && make -sj4

  ![image](https://github.com/Ferresette/tunku/assets/148973799/b56a06ae-c0f4-48a7-a80d-8984ed8ff034)


  Käytin komentoa ls -l, jotta näin vähän mitä tiedosto sisältää.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/e0c8c398-c6f2-4f1d-8306-e515ed7cd4ab)

  Käytin teron sivuilla löytyvää zippi tiedostoa testatakseni ympäristöä.

      $ wget https://TeroKarvinen.com/2023/crack-file-password-with-john/tero.zip

  ![image](https://github.com/Ferresette/tunku/assets/148973799/2aa89e84-cb80-4293-a9fa-08e4cc1ff2ae)

  Koitin avata teron zippi tiedostoa, kuten sivuillakin sanottiin että se olisi turhaa. Ei päästy vielä eteenpäin siis.

  ![image](https://github.com/Ferresette/tunku/assets/148973799/394c797a-e2e2-456d-b567-e999b7ba8ea7)

  Jotta saisin zippi tiedostosta jotain irti, minun täytyi purkaa se uuteen tiedostoon nimeltä tero.zip.hash.

      zip2john tero.zip >tero.zip.hash

  Tämän jälkeen suoritin hyökkäyksen Johnilla kyseiseen tiedostoon.

      john tero.zip.hash

  ![image](https://github.com/Ferresette/tunku/assets/148973799/7a864445-fe3a-41ce-8796-ea0f9c93f2c0)

  Sain nyt talteen salasanan "Butterfly", lähdetään yrittämään purkaa teron zippi tiedostoa tällä salasanalla. Syötettiin salasana, se toimi ja nyt saatiin tiedosto sijainti.

      unzip tero.zip
      cat secretFiles/SECRET.md

  ![image](https://github.com/Ferresette/tunku/assets/148973799/14160961-9b95-40d9-bc8d-5932d2fd2cdd)

  ## d) Fuffme. Asenna Ffufme harjoitusmaali paikallisesti omalle koneellesi. Ratkaise tehtävät (kaikki paitsi ei "Content Discovery - Pipes")

  Aloitin lataamalla tehtävään tarvittavia ympäristöjä.

      $ sudo apt-get update
      $ sudo apt-get install docker.io git ffuf

![image](https://github.com/Ferresette/tunku/assets/148973799/16f1d43a-6189-43c7-9763-c7c08982cd3d)

Tämän jälkeen aloitin rakentamaan harjoituskohdetta Dockeriin.

    $ git clone https://github.com/adamtlangley/ffufme
    $ cd ffufme/
    $ sudo docker build -t ffufme .

![image](https://github.com/Ferresette/tunku/assets/148973799/7bc1d58d-1d06-46b6-b754-93e2a9e8f2ee)

Seuraavaksi lähin käynnistämään dockeria, mikä käytti ffufme kuvaa. Ja ohjaa sen koneen portin 80 isäntäkoneen porttiin 80. Ja testasin yhteyden curlilla.

    $ sudo docker run -d -p 80:80 ffufme
    $ curl localhost

![image](https://github.com/Ferresette/tunku/assets/148973799/64fdef31-9b0f-4911-beea-2feaf112bf94

Latasin vielä kaikki tarvittavat sanalistat, jotta pääsin suorittamaan tehtäviä.

    $ mkdir $HOME/wordlists
    $ cd $HOME/wordlists
    $ wget http://ffuf.me/wordlist/common.txt
    $ wget http://ffuf.me/wordlist/parameters.txt 
    $ wget http://ffuf.me/wordlist/subdomains.txt
    $ cd -

Katkaisin internet yhteyden ja aloin fuzzamaan.

    $ ffuf -w $HOME/wordlists/common.txt -u http://ffuf.me/cd/basic/FUZZ

![image](https://github.com/Ferresette/tunku/assets/148973799/d2095c70-0607-4536-98a6-729f8ba2da9c)


Harjoittelusivulle päästy onnistuneesti, sivu päivittyi kyllä todella hitaasti.

![image](https://github.com/Ferresette/tunku/assets/148973799/86a1e542-0bf3-4f30-9187-1cf526cfe3b4)



**Basic Content Discovery**

Perinteisin fuzzaus menetelmä. Tämä löytää class sekä development.log tiedostot.

![image](https://github.com/Ferresette/tunku/assets/148973799/f34fcfa3-2f88-4e92-a33f-5110d724f896)


**Content Discovery With Recursion**

Samankaltainen kun edellinen fuzzaus. Käyttää rekursiokytkintä. Paljastaa admin, admin/users ja admin/users/96 tiedostot.

![image](https://github.com/Ferresette/tunku/assets/148973799/3f580c5c-04c3-4e51-9d8d-ddbaaa2dcb8b)


**Content Discovery With File Extensions**

Löytää logs/users.log tiedostot.

![image](https://github.com/Ferresette/tunku/assets/148973799/d6ebaa39-01d6-496b-8ef4-4a4498de87cf)


**No 404 Status**

Löytää secretin ja filtteröi sen 669.

![image](https://github.com/Ferresette/tunku/assets/148973799/676355a0-3634-4b84-8a35-278c4e91e987)

**Param Mining**

Etsii URL parametrejä.
Löytää debugin.

![image](https://github.com/Ferresette/tunku/assets/148973799/066f2116-de6b-44b9-bf95-ea7ca43c4e43)


**Rate Limited**

Rate limitedin tarkoituksena on rajoittaa haun pyyntöjen lähetystä, eli kuinka nopeasti se lähettää pyyntöjä. Jotkut verkkopalvelut voivat rajottaa pyyntöjen määrää.


**Subdomains - Virtual Host Enumeration**

Tarkoituksena tunnistaa subdomaineja ja löytää aktiiviset virtuaaliset isännät.

redhat tuli tulokseksi tässä.

![image](https://github.com/Ferresette/tunku/assets/148973799/671faf34-01e5-4152-b162-8905328d1b0d)

### e) Tee msfvenom-työkalulla haittaohjelma, joka soittaa kotiin (reverse shell). Ota yhteys vastaan metasploitin multi/handler -työkalulla.

 - Haittaohjelma ei saa olla automaattisesti leviävä. Msfvenom tekee tunnilla opetelluilla asetuksilla ohjelman, joka avaa reverse shellin, kun sen ajaa, mutta joka ei leviä eikä tee muutenkaan mitään 
   itsestään.
 - Raporttiin riittävät pelkät komennot haitakkeen tekemiseen, itse binääriä ei ole pakko laittaa verkkoon. Mikäli laitat binäärin verkkoon, pakkaa se salakirjoitettuun zip-pakettiin ja laita salasanaksi "infected". Latauslinkin yhteydessä on oltava selkeä varoitus siitä, että binääriä ei tule ajaa oikeilla koneilla. Salasanan voit halutessasi kertoa varoitusten yhteydessä.

Jos oikein ymmärsin, niin tässä pelkät komennot ja selitykset riittivät. Tunnilla jo hieman käytiinkin msfvenomin käyttöä läpi. 



### f) Asenna Windows virtuaalikoneeseen. Voi olla esimerkiksi Metasploitable 3 tai Microsoftin sivuilta saatava ilmainen kokeiluversio.

Aloitin asentamaan windowsia virtuaalikoneeseen. Hain microsoftin sivuilta Windows 10 ja valitsin sieltä latauskohdassa iso tiedoston, jotta se ei asenna sitä omalle koneelleni.
Latauksen jälkeen lähdin tekemään uutta virtuaalikonetta Windows iso imageen. Asetettiin muistit ja haluamani asetukset. Käynnistettiin kone.

![image](https://github.com/Ferresette/tunku/assets/148973799/df7ac4e7-e651-4875-b4d0-3282a7eeefcb)

![image](https://github.com/Ferresette/tunku/assets/148973799/46a77054-6edf-424c-956c-8b9fcb4535ec)












  











  
















