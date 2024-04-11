## x) Lue/katso ja tiivistä.

*Lyon 2009: Nmap Network Scanning: Chapter 15. Nmap Reference Guide:*
- Port Scanning Basics (opettele, mitä tarkoittavat: open, closed, filtered; muuten vain silmäily)
- Port Scanning Techniques (opettele, mitä ovat: -sS -sT -sU; muuten vain silmäily)

  Nmap on tehokas verkkoskanneri, yleisempänä tehtävän on skannata eri portteja. Portit jaetaan kuuten eri tilaan:

   - **Open** Tässä tilassa aktiivisesti vastaanottaa tietoja.
   - **Closed** Suljettu, mutta vastaanottaa ja vastaa Nmap kyselyihin, mutta palvelua ei ole kuuntelemassa.
   - **Filtered** Ei pysty määrittämään portin tilaa, koska pakettisuodatus estää sen kyselyt.
   - **Unfiltered** Portti on saatavilla, mutta tilaa ei voi määrittää muilla kuin ACK-skannilla.
   - **Open|filtered** Nmap käyttää tätä tilaa, kun se ei voi varmasti sanoa, onko portti avoin vai suodatettu.
   - **Closed|filtered** Käytetään vain IP ID -tunnistuksessa.
 
  Tietynlainen ymmärrys ja valinta oikeasta skannaustekniikasta ovat avainasemassa porttiskannauksessa. Nmap tarjoaa useita skannaustyyppejä eri tilanteisiin, mutta osa niistä vaatii erityisoikeuksia.
  Kokonaisuudessaan Nmap tarjoaa monipuolisen valikoiman työkaluja porttiskannaukseen, mikä mahdollistaa käyttäjän sovittaa lähestymistapansa tehtävän ja järjestelmän kykyjen mukaan.

    - **-sS** (TCP SYN skannaus) Nopea ja suhteellisen huomaamaton skannaus, joka tunnistaa avoimet, suljetut ja suodatetut portit lähettämällä SYN-paketteja ja tarkkailemalla vastauksia.
    - **-sT** (TCP yhteys skannaus) Oletusskannaus, kun SYN-skannaus ei ole mahdollinen. Se käyttää korkean tason yhteydenmuodostuskutsuja, mikä tekee siitä hitaamman ja helpommin havaittavan kuin SYN-skannaus.
    - **-sU** (UDP skannaus): Tunnistaa UDP-portit, mikä on haasteellisempaa ja hidasta kuin TCP-skannaus. Lähettää UDP-paketteja jokaiseen kohdeporttiin ja tarkkailee vastauksia. Taistelee usein aikarajoitusten kanssa, jotka hidastavat skannausta.
 

### a) Asenna Kali virtuaalikoneeseen

Kalin olin jos asentanut aikaisemmassa kotitehtävässä ja se on raportoituna siellä.


### b) Asenna Metasploitable 2 virtuaalikoneeseen

Aloitin Metasploitable 2:n asennuksen jo tunnilla, latasin asennustiedoston *https://sourceforge.net/projects/metasploitable/files/Metasploitable2/* sivustolta.

Tiedosto oli zippi tiedostona, joten aloitin purkamalla kyseisen tiedoston. Tämän jälkeen aloin luomaan uutta virtuaalikonetta virtuaaliboxiin.

![image](https://github.com/Ferresette/tunku/assets/148973799/0c505feb-c3d4-4108-9443-ea429e84f339)

Lisättiin perus asetukset kuten nimi, tyyppi, versio ja säädettiin muistit kuntoon. Seuraavaksi hyödynnettiin jo valmiina olevaa Kali Linuxia existing virtual hard disk filenä.

![image](https://github.com/Ferresette/tunku/assets/148973799/53e328fe-b477-4eee-b3a9-d143ea4d3f34)

Etsittiin ladattu Metaspoitable 2 tiedosto jo lisättiin se Kali linuxiin.

![image](https://github.com/Ferresette/tunku/assets/148973799/dc297a0f-2c6c-4c80-8ad4-d2ebc8c589a2)

![image](https://github.com/Ferresette/tunku/assets/148973799/300b443e-2ec0-41e6-b847-0007f8804d8f)

![image](https://github.com/Ferresette/tunku/assets/148973799/48b9aaa5-51d9-4be7-bd66-4c279513cb3f)

Hyödynsin ohjesivuston kuvia kuvastamaan asennusvaihetta, koska olin koulussa kerennyt asentamaan ohjelman enkä tajunnut ottaa talteen kyseisiä vaiheita.





  
  


  
