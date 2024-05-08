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
- **nmap -sS scanme.nmap.org** # Lähettää SYN paketteja ja analysoi vastauksen. SYN/ACK saatuaan on tieto, että portti on auki ja mahdollisuus avata TCP yhteys. Voi olla aika hidas skannausmetodi.
- **nmap -sV scanme.nmap.org** # Listaa skannattujen palveluiden versiot
- **nmap -A scanme.nmap.org** # Aggressiivinen skannaus, antaa yleisesti parempaa tietoa, mutta helpommin havaittavissa.
- **nmap -p 80** 192.164.0.1 # Mahdollisuus myös skannata tietty portti
- **nmap -v scanme.nmap.org** # Antaa kätevää lisätietoa skannista, kun se on käynnissä.


Lähde: https://www.freecodecamp.org/news/what-is-nmap-and-how-to-use-it-a-tutorial-for-the-greatest-scanning-tool-of-all-time/
    
