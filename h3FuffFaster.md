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

  Analysoi kyseisen hashin




