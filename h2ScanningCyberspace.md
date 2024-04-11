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

Etsittiin ladattu Metaspoitable 2 tiedosto jo lisättiin se Kali linuxiin.

![image](https://github.com/Ferresette/tunku/assets/148973799/53e328fe-b477-4eee-b3a9-d143ea4d3f34)

![image](https://github.com/Ferresette/tunku/assets/148973799/dc297a0f-2c6c-4c80-8ad4-d2ebc8c589a2)

![image](https://github.com/Ferresette/tunku/assets/148973799/300b443e-2ec0-41e6-b847-0007f8804d8f)

![image](https://github.com/Ferresette/tunku/assets/148973799/48b9aaa5-51d9-4be7-bd66-4c279513cb3f)

Hyödynsin ohjesivuston kuvia kuvastamaan asennusvaihetta, koska olin koulussa kerennyt asentamaan ohjelman enkä tajunnut ottaa talteen kyseisiä vaiheita.

Metasploitablen asennus onnistunut.

![image](https://github.com/Ferresette/tunku/assets/148973799/524ce936-0f50-4204-828b-4e31a1f94839)

### c) Tee koneille virtuaaliverkko, jossa

  - Kalin ja Metasploitablen välillä on host-only network, niin että porttiskannatessa ym. koneet on eristetty intenetistä, mutta ne saavat yhteyden toisiinsa

  - Osoita eri komennoilla, että Internet-yhteys katkeaa: 'ping 1.1.1.1', 'ping www.google.com', 'curl www.google.com'

Aloin etsimään tietoa miten koneille luodaan virtuaaliverkko mikä hyödyntää Host-only verkkoa. Pienen tutkiskelun jälkeen selvisi, että tämä voidaan toteuttaa muuttamalla virtuaalikoneiden network settingsejä.

Asetuksista löytyi vaihtoehto Host-only adapter ja sen alapuolelle tuli VirtualBox Host-only Ethernet Adapter. Vaihdoin molempien virtuaalikoneiden asetukset tähän vaihtoehtoon.

![image](https://github.com/Ferresette/tunku/assets/148973799/24ffd071-d33c-45e6-a8fd-d233a09a7a3b)

Lähdin tarkastamaan asian, että koneet käyttävät samaa verkkoa käyttämällä komentoa:

    ip addr

Sieltä löysin Metasploitablen ip osoitteen jota lähdin pingaaman. Pingaus onnistui Kalin kautta Metasploitableen, joten yhteys on kunnossa.
Varmistin myös, että pingaus epäonnistuu annettuun googlen esimerkki osoitteeseen ja tämä meni myös niin kuin piti.

ip addr käyttö.

![image](https://github.com/Ferresette/tunku/assets/148973799/776dd342-9c13-4fd1-a7f8-05aacf9ac1f5)

Pingaus Metasploitablen osoitteeseen.

![image](https://github.com/Ferresette/tunku/assets/148973799/3e621bcc-a1ee-41a4-8d17-1d8181483e7b)

Kokeilin googlen pingauksen kaikilla eri tyylillä ja se antoi hieman eri viestin syötekenttään, mutta voidaan ainakin todeta ettei onnistu.

![image](https://github.com/Ferresette/tunku/assets/148973799/5934e440-d8a7-487f-bc7c-efdc4c826225)









  
  


  
