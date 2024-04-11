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


### d) Etsi Metasploitable porttiskannaamalla (db_nmap -sn). Tarkista selaimella, että löysit oikean IP:n - Metasploitablen weppipalvelimen etusivulla lukee Metasploitable. Katso, ettei skannauspaketteja vuoda Internetiin - kannattaa irrottaa koneet netistä skannatessa. Seuraa liikennettä snifferillä.

Tehtävä tuotti aluksi aika paljon ongelmia. En oikein keksinyt miten db_nmap -sn komennoin saisi toimimaan. Perus nmap komennot toimi Kali linuxin terminaalissa ja myös metaspoitablen ipn kautta nettiosoitteessa tuli oikeat jutut näkyviin. Selvittelin vähän netistä db_nmap -sn komennon virkaa ja selvisi, että sitä pitäisi käyttää Metasploitable frameworkissa. Sielläkään ei aluksi komento toiminut ja antoi kaikennäköistä virhekoodia eteeni.

Yhdestä artikkelista luettuani selvisi, että MSF käyttää PostgreSQL tietokantaa, joten lähdin käynnistämään sitä virutaalikoneellani. Tämän jälkeen aloin alustamaan MSF tietokantaa ja yhdistämään siihen, käytin seuraavia komentoja:

    systemctl start postgresql
    sudo msfdb init

![image](https://github.com/Ferresette/tunku/assets/148973799/f3d394ff-d820-4071-b77b-9445d9485d1c)

Käsittääkseni nyt minulta löytyy tarvittavat työkalut MSF käyttämiseen, kokeillaan avaamalla msfconsoli komennolla:

    msfconsole

Päästiin sisään konsoliin.

![image](https://github.com/Ferresette/tunku/assets/148973799/4a412ec2-baa0-4ff6-9b2d-c7dfe611ab68)

Nyt aloin kokeilemaan tehtävänannossa annettuja komentoja, ensiksi:

    db_nmap -sn (Jälkeen päin huomasin, että tässä olin vielä yhteydessä internetiin. En tiedä oliko sillä vaikutusta)

Nyt nmappaus näytti menevän läpi msfconsolessa.

![image](https://github.com/Ferresette/tunku/assets/148973799/c60d42c0-3c1c-473f-bca5-13881295c578)

Seuraavaksi vielä varmistin, että kyseinen ip toimi verkkoselaimella ja antoi metaspoitable tekstin.

![image](https://github.com/Ferresette/tunku/assets/148973799/143d8b96-194e-476f-bf9c-735b9629f8a9)

Irroitin virtuaalikoneet internetistä. 

![image](https://github.com/Ferresette/tunku/assets/148973799/5d464ea6-814c-4445-b37a-05eb699e3658)

Tämän jälkeen lähdin testaamaan wiresharkilla millaista liikennettä näkyy.

![image](https://github.com/Ferresette/tunku/assets/148973799/dcf36aee-a9b5-43d6-9acf-52c8b2af33f7)

Kuvassa näkyy aika paljon tapahtumia, spottasin muutaman rivin, missä oli punaista ja tutkin niitä vähän tarkemmin. Lisätiedoista selviää, että nämä kehykset ovat suspected eli kuvittelisin näiden olevan niitä haitallisia kehyksiä.

![image](https://github.com/Ferresette/tunku/assets/148973799/266ce6a5-471b-4ff4-9620-d37058ae6cf3)

### e) Porttiskannaa Metasploitable huolellisesti (db_nmap -A -p0-). Analysoi tulos. Kerro myös ammatillinen mielipiteesi (uusi, vanha, tavallinen, erikoinen), jos jokin herättää ajatuksia. Seuraa liikennettä snifferillä.

Lähdin nyt kokeilemaan toisenlaista nmappaus komentoa msfconsolessa:

  db_nmap -A -p0- 127.0.0.1 (Tässä en ole yhteydessä internetiin, kuten ip-osoitteesta huomaa että se on erilainen)

![image](https://github.com/Ferresette/tunku/assets/148973799/4bffc46d-a649-40a7-8a1c-02b6cf5c994d)

![image](https://github.com/Ferresette/tunku/assets/148973799/a9991a38-1bb6-4de6-946f-0331b0858bcd)

Tulos oli edellisestä poikkeava. Skannaus on paljon laajempi ja huomioni ainakin herätti, että portti 5432 on auki. Skannauksessa havaittiin myös yksi palvelu jonka tietoja ei tunnistettu, voisin kuvitella, että tämä oli se mitä tässä etsittiin.

Tutkin sen jälkeen wiresharkilla verkkoliikennettä, se näytti mielestäni aika samalta kun sitä katsoin aiemmassa tehtävässä. Nyt en löytänyt toki yhtään punaisia kehyksiä.

![image](https://github.com/Ferresette/tunku/assets/148973799/8d752ea9-959c-468e-97bb-76c6f9e64855)

### f) Tallenna portiskannauksen tulos tiedostoon käyttäen nmap:n omaa tallennusta (nmap -oA foo).

Tallensin porttiskannauksen tulokset kyseisellä komennolla:

  nmap -oA foo 127.0.0.1

![image](https://github.com/Ferresette/tunku/assets/148973799/98cd4cd9-e4f4-4e56-b6c8-cbcc7b0d9440)

Tämän jälkeen tarkistin, että kyseinen tiedosto löytyy käyttämällä ls komentoa. 

![image](https://github.com/Ferresette/tunku/assets/148973799/25ca3bdf-f61d-4595-a309-61d9351d200a)

Kuten kuva näyttää, sieltä löytyy tallenneut tiedostot. Halusin vielä nähdä niiden sisällön, joten avasin teksieditorilla tiedoston. Käytin vim:iä.

![image](https://github.com/Ferresette/tunku/assets/148973799/3ba38358-278b-465d-a523-db15f6b4b6a0)

### g) Tallenna shell-sessio tekstitiedostoon script-työkalulla (script -fa log001.txt)

Lähdin tallentamaan shell-sessiota tekstitiedostoon script-työkalulla. Käytin seuravaa komentoa avatakseen tallennuksen ja tallennuspaikan:

  script -fa log001.txt

Tämän jälkeen tein jotain shellin sisällä ja suoritin exit komennon shell-session päättämiseksi.

![image](https://github.com/Ferresette/tunku/assets/148973799/5e0ed230-20ce-4840-b046-7adebe3d66de)

![image](https://github.com/Ferresette/tunku/assets/148973799/e8a001d4-462f-45c8-aefc-06f9d0e29b02)

Scriptin sisältö näytti tältä tekstieditorilla, käytin siis shellin tallennusaikana ls ja ls -a komentoja.

![image](https://github.com/Ferresette/tunku/assets/148973799/6dd4ea18-8082-4f8b-95df-d07cd786a56d)

### h) Etsi kaikki maininnat jostain osoitteesta, palvelusta tai vastaavasta kaikista tallennetuista tuloksista ja lokeista (grep -ir tero).

Etsin yllämainitulla komennolla maininnat, tämä komento näköjään etsii tietoa hakemistoista ja tiedostoista. Tällä kertaa se haki teroa.

![image](https://github.com/Ferresette/tunku/assets/148973799/52c8c980-9511-4bcd-9f7f-037fb788c7fb)

![image](https://github.com/Ferresette/tunku/assets/148973799/e9ea43ab-7d35-4d54-8981-de39b7f1cc84)

### Anna esimerkit nmap ajonaikaisista toiminnosta. (man nmap: runtime interaction)

Tästä löysin muutamia hyviä esimerkkejä Nmapin runtime interaction komentoihin.

![image](https://github.com/Ferresette/tunku/assets/148973799/36012a25-a05b-46db-9846-5c399eb66798)



### References

https://terokarvinen.com/2024/eettinen-hakkerointi-2024/#h2-scanning-cyberspace

https://www.geeksforgeeks.org/how-to-link-kali-linux-with-metasploitable-2/?ref=ml_lbp

https://medium.com/@nickhandy/kali-linux-metasploit-getting-started-with-pen-testing-89d28944097b

https://gist.github.com/fabionoth/ba46407d9cd03144150225715697c47f

https://nmap.org/book/man-runtime-interaction.html

https://chat.openai.com/

https://sourceforge.net/projects/metasploitable/files/Metasploitable2/





























  
  


  
