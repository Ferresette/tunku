## Johdanto

Tämän viikon tehtävässä on aika valmistautua loppukoitokseen eli CTF. Tarkoituksena minulla on tehdä mahdollisimman hyvä Cheatsheet, mistä olisi itselleni eniten hyötyä kyseisessä harjoituksessa.

Tavoitteeni on kasata tunnilla käytetyistä ohjelmista tarkat ohjeet sekä käytännöllisimmät koodit ja niiden selitykset kasaan. Sen lisäksi aion myös tehdä tiivistyksen vertaisarvioidusta artikkelista.

Viimeisenä aion vielä tarkistaa, että minulta löytyy tarvittavat työkalut lipunryöstöä varten. Näillä näkymin tulen käyttämään KaliLinux virutaalikonetta harjoitukseen. Näiden toteuttamiseen otan rungon https://terokarvinen.com/2024/eettinen-hakkerointi-2024/. Sekä pyrin löytämään netistä mahdollisimman paljon täydentävää tietoa.


### a) Cheatsheet

#### Nmap

Porttiskannaus metodi, millä saa helposti laajan kuvan verkosta ilman vaikeita komentoja ja konfiguraatioita. Esimerkiksi, mitä laitteita verko(i)ssa on yhdistettynä, mitä palveluita on käynnissä tai mitä versiota käytetään.

Suurimmassa osassa komennoista suosittelisin vielä käyttämään ___sudo___ ominaisuutta, jotta ne ajetaan järjestelmänvalvojana.
Komentoja, mitkä koen henkilökohtaisesti hyödylliseksi Nmapissa:

- **nmap -h / man nmap**  # Molemmat komennot antavat laajasti tietoa nmapin komennoista.
- **nmap -sp 192.168.1.1/24** # Tekee Ping scan:in, tekee listan käynnissä olevista aliverkoista
- **nmap scanme.nmap.org** # Skannaa single hostin 1000 yleisintä porttia.
- **nmap -p- 127.0.0.1** # Voit myös skannata halutessasi kaikki portit
- **nmap -sS scanme.nmap.org** # Lähettää SYN paketteja ja analysoi vastauksen. SYN/ACK saatuaan on tieto, että portti on auki ja mahdollisuus avata TCP yhteys. Voi olla aika hidas skannausmetodi.
- **nmap -sV scanme.nmap.org** # Listaa skannattujen palveluiden versiot
- **nmap -A scanme.nmap.org** # Aggressiivinen skannaus, antaa yleisesti parempaa tietoa, mutta helpommin havaittavissa.
- **nmap -p 80** 192.164.0.1 # Mahdollisuus myös skannata tietty portti
- **nmap -v scanme.nmap.org** # Verbose output antaa kätevää lisätietoa skannista, kun se on käynnissä.
- **nmap -oA "tiedostonimi" 127.0.0.1** ## Tallentaa ajetun skannauksen eri tiedostomuotoihin. Voidaan avata tekstieditorilla jälkeenpäin ja nähdä skannaustulos.


Lähde: https://www.freecodecamp.org/news/what-is-nmap-and-how-to-use-it-a-tutorial-for-the-greatest-scanning-tool-of-all-time/


#### Hashcat

Hashcat on avoimen lähdekoodin salasanojen murtamiseen tarkoitettu työkalu. Hyödyntää sanakirjapohjaisia hyökkäyksiä salasanojen paljastamiseen. Kyky purkaa salasanat erilaisista tiivistefunktioista, esim MD5, SHA-1, SHA-256. Hashcat löytyy oletuksena KaliLinuxista.

Komentoja, mitkä koen hyödylliseksi Hashcatin käytössä:

 - **hashcat -h** # Antaa hashcatin help menun
   
         - mkdir hashed # Luo directoryn hashed, käytännössä vain helpompi organisoida työtä.
         - cd hashed # Vaihtaa kyseiseen directoryyn
         - wget https://github.com/danielmiessler/SecLists/raw/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz # Lataa yleisimmän salasanakirjan "rockyou.txt".
         - tar xf rockyou.txt.tar.gz # Purkaa kyseisen tiedoston
         - rm rockyou.txt.tar.gz # Poistaa alkuperäisen pakatun tiedoston, sille ei ole enään tarvettu kun se on purettu.
   
 - **hashid -m "esimerkki hash"** # tämä komento pyrkii selvittämään mitä tiivistefunktiota esimerkki tiiviste käyttää.
 - **hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96' rockyou.txt -o tiedostomihintallennetaan** # Edellisen komennon jäljiltä ollaan saatu erilaisia tiivistefunktioita, joten tässä komennossa "-m 0" tarkoittaa MD5 tiivistettä. Heittomerkeillä pyritään myös tunnistamaan tiivisteet, missä on erikoismerkkejä. Hyödynnetään "rockyou.txt" sanaluetteloa ja tallennetaan nimemämään kansioon.

 Löysin myös mielenkiintoisen kaavion eri tyyleistä suorittaa kyseinen hashid komento, riippuen hieman mitä hyökkäystyyliä käyttää.

 ![image](https://github.com/Ferresette/tunku/assets/148973799/2fb693e1-84e2-4061-9b9d-a7820d86adc4)

 - **cat "tiedostomihintallennettu"** # Näyttää crackatun salasanan hashin perässä jos onnistunut.
 - **hashcat -m 0 "esimerkki hash" rockyou.txt --show** # näyttää suoraan crackatun salasanan command linessa ilman tallentamista.

Lähteet: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/ | https://www.freecodecamp.org/news/hacking-with-hashcat-a-practical-guide/ | https://hashcat.net/wiki/doku.php?id=hashcat

#### John the Ripper




    
