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









