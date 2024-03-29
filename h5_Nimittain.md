
# Kotitehtäväraportti h5  

Tässä raportissa tiivistin alkuun kaksi Tero Karvisen artikkelia. Tiivistelmistä ei jälleen tullut kovin tiiviitä, koska ne toimivat myös muistiinpanoina itselleni tulevaa tehtävää ajatellen. Tämän jälkeen lähdin vuokraamaan virtuaalipalvelimelleni domain nimeä ja analysoimaan uuden domain nimeni tietoja `host` ja `dig` -komennoilla sekä pistämään virtuaalipalvelimelleni pystyyn kotisivuja name based virtual hosting periaatteella tiivistämiäni artikkeleita hyödyntäen.  

## x) Artikkelien tiivistäminen  

### [New Default Website with Apache2 – Show your homepage at top of example.com, no tilde](https://terokarvinen.com/2016/02/16/new-default-website-with-apache2-show-your-homepage-at-top-of-example-com-no-tilde/ "Ensimmäinen artikkeli")  

  - _Alla olevissa tiivistelmän esimerkeissä on Teron omat esimerkkinimet ja kotikansiot. Korvaa tarvittaessa omilla._

  - Asenna apache2  
    - `sudo apt-get update`  
    - `sudo apt-get -y install apache2`  
  - Apachen VirtualHostien muokkauksesta:
    - Apachen saatavilla olevat virtual hostit se löytää hakemistosta /etc/apache2/sites-available/ . Yksittäinen tekstitiedosto per sivu.
    - Päälle laitetut sivut löytyvät hakemistosta /etc/apache2/sites-enabled/  
    - Hakemistoihin ei tarvitse manuaalisesti luoda uusia tiedostoja vaan se onnistuu apachen komennoilla: `sudo a2ensite tero.conf` . Jos tämän haluaa poistaa käytöstä: `sudo a2dismod tero.conf`   
    - Uuden VirtualHostin luominen: Yksinkertainen nimi ilman erikoismerkkejä esim `sudoedit /etc/apache2/sites-available/tero.conf`  
    - Esimerkki ylempää editointikomentoa varten:        
     `## /etc/apache2/sites-enabled/tero.conf`  
      `<VirtualHost *:80>`  
      `DocumentRoot /home/tero/public_html/`  
      `<Directory /home/tero/public_html/>`  
      `Require all granted`  
      `</Directory>`  
      `</VirtualHost>`  
  - Oletussivun poisto käytöstä ja oman käyttöönotto:  
    `a2ensite tero.conf`  
    `a2dissite 000-default.conf`  
  - Käynnistä apache uudelleen `service apache2 restart`
  - Luo se itse sivu, jonka juuri mahdollistit edellämainituilla ohjeilla.
  - Jos yritit päästä localhostilla jo sivulle, jota et ollut vielä luonut voit tutkia lokeista mikä oikeastaan meni pieleen (ei sivuja, ei index.html tiedostoa, väärä kotikansion polku).
  - Tee ensin pelkkä plain text kotisivu, jotta näet toimiiko homma. HTML5 on paljon varaa virheisiin, jotka vaikeuttavat vian etsimistä.
  - Muista validoida sivusi jos teet HTML5.  

### [Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ "Toinen artikkeli")  

  - Asenna apache ja vaihde oletussivu.  
  - Luo uusi VirtualHost apachen saataville hyödyntäen esimerkiksi aiemman artikkelin ohjeita.  
  - Luo itse sivu.
  - Testaa toimivuus:  
    `curl -H 'Host: pyora.example.com' localhost`
    `curl localhost`  
  - Ja useampien nimien asettaminen samalle ip:lle:  
    `sudoedit /etc/hosts`  
    `cat /etc/hosts`   
    `127.0.0.1 localhost`   
    `127.0.1.1 xubuntu`   
    `127.0.0.1 pyora.example.com`   
    `# ...`

### [Name-based Virtual Host Support](https://httpd.apache.org/docs/2.4/vhosts/name-based.html "Kolmas artikkeli") _Tämä lisätty vasta palauttamisen jälkeen kun huomasin sen muita töitä arvioidessani. Hiukan unohtui.._  

Tämä artikkeli sisälsi paljon teknistä tietoa, jota en ihan täysin sisäistänyt. Pitänee pistää kirjanmerkkeihin ja perehtyä myöhemmin.

  - Nimeen vs ip osoitteeseen pohjautuvien virtual hostien erot
    - Name-based yleensä yksinkertaisempaa kaikin puolin ja sitä suositellaan aina kun mahdollista.  
  - Serverin valintaperiaatteista nimipohjaisessa virtual hostingissa
    - Tämä meni kyllä vähän yli osaamistasoni..
  - Name-based Virtual Hostien käytöstä
    - VirtualHostille pitää antaa aina tietyt tiedot joiden mukaan asiakas voidaan ohjata haluttuun paikkaan.
    - Tekniikka vaatii myös tiettyjen asetusten säätämistä DNS palvelimen osalta.


## a) Domain nimen vuokraaminen ja osoittaminen virtuaalipalvelimelleni  

Päätin käyttää tunnillakin mainittua [NameCheap](https://www.namecheap.com/ "NameCheap etusivu") palveluntarjoajaa. Heiltä pystyi kätevästi etsimään nimiehdotuksella eri päätteisiä sivuja ja niiden hintoja. Minulla oli suuria vaikeuksia löytää tunnilla bongattuja yhden euron/vuosi hintaisia sivuja:  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/8a96aa8f-4da8-41de-be04-c273a95553a3)

Lopulta alistiuin ja päädyin nimeen vararikko.xyz, joka minulle tarjoiltiin hintaan 2,05€ (todellisuudessa 2,18€...). En muistanut tarkkaan tunnilta enkä jaksanut selvittää mitä Domain Privacy asetus tekee, joten jätin sen päälle. Tarkistin useampaan kertaan, että Auto-Renew ei ollut missään minulla päällä.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/a25c86fd-4867-47c9-b06c-b0d2dfe9c705)

Ai niin, tänne piti luoda tilikin. Ja jälleen kerran uusi salasana...  
Kun tili oli tehty ja tuote tilattu, NameCheap ehdottikin minulle, että nyt olisi hyvä aika laittaa DNS asetukset kuntoon.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/dfe0f8d5-2024-4442-a0ab-a671bf4adbb1)

No itse linkkihän vei vain help sivulle, missä opastettiin DNS asetusten laittamiseen.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/af4bbd64-ed3d-4df9-98bb-e81518072136)

Haluamaani paikkaan pääsin yläreunan Account pudotusvalikosta valitsemalla domain list. Tämän jälkeen valitsin ruudun oikeasta reunasta "manage" oikean (ainoan) domainin kohdalta.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/763bde83-84e3-4abf-a734-afa8ffdc84d8)

Täältä ylävalikosta tuli valita Advanced DNS ja pääsin lopulliseen sijaintiini, josta pystyin muuttamaan mihin ip-osoitteeseen nimestä vararikko.xyz ohjataan.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/f47e277b-591b-4c9b-b9d2-31378c921a15)

Yritin muistella mitä tänne tunnilla tehtiin. Tämän lisäksi yritin etsiä lisätietoja internetistä ilman selkeää vastausta. Katsoin jopa useamman NameCheapin pikselimössöisen ohjevideon, joissa oli vanhentunut GUI, enkä silti ollut täysin varma mitä tietoja minun piti seuraavaksi syöttää tähän kenttään.  
Päädyin seuraaviin vaihtoehtoihin:  
"A Record, @, 172.104.145.15" (virtuaalipalvelimeni ip). Tämän oletin nyt ohjaavan liikenteen vararikko.xyz nimestä kyseiseen ip-osoiteeseen.  
"A Record, www, vararikko.xyz" Tämän oletin ohjaavan www,vararikko.xyz aiemmin mainitsemaani ip-osoitteeseen.  
Vaihdoin TimeToLive asetuksiin 20min. Tämä ymmärtääkseni määritti sen, että asetukset tulevat julkisesti voimaan tämän ajan kuluttua.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/b00c0bf8-065d-4e13-90f0-aa3a8b57ae64)

NameCheap poisti automaattisesti luomansa roskatiedot samalla kun tallensin omat uudet tietoni. Käyttöliittymä ei antanut minun tallentaa "A Record, www, vararikko.xyz" valintaa, joten muutin sen muotoon "CNAME Record, www, vararikko.xyz".  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/4589f873-e95a-42aa-be8b-7beb71428899)  

Kun yritin löytää tarkempaa kuvausta tiedolle "TTL" laittaakseni sen tähän raporttiin, löysin myös NameCheapilta kohtuullisen [ohjeen Recordien muuttamisesta](https://www.namecheap.com/support/knowledgebase/article.aspx/319/2237/how-can-i-set-up-an-a-address-record-for-my-domain/ "NameCheap - How can I set up an A (address) record for my domain?"). Enkä lopulta jaksanut etsiä sitä kuvausta TTL:stä. Nyt oli aika odotella, että muutokset tulisivat voimaan. Ehkä tehdä pari punnerrusta tai muita kotitehtäviä eteenpäin.  

Tein mm. muita kotitehtävän osioita eteenpäin ja noin tunnin jälkeen palasin tähän vaiheeseen tarkistamaan oliko nimipalvelu käytössä. Syötin virtuaalikoneeni (LinuxNub) komentoriville `firefox vararikko.xyz`. Hetken odottelun jälkeen pääsin aiemmissa tehtävissäni muokkaamalleni linode virtuaalipalvelimen kotisivulle. Avasin firefoxiin kaksi uutta välilehteä ja kokeilin osoitteita. www.vararikko.xyz sekä https://www.vararikko.xyz. https ei toiminut, mutta muut toimivat.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/db2124ad-d755-4ef1-a0d8-b97b7ed79cd1)  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/a2d1ea08-044c-4540-8891-b9fc11a118b5)

Https ei ymmärtääkseni toimi, koska en ole tehnyt domainini asetuksiin recordeja, jotka ohjaisivat oikeaan ip-osoitteeseen https protokollaa käytettäessä.



## b) Oman domain nimen tutkiminen `host` ja `dig` -komennoilla  

Käynnistin oman virtuaalikoneeni (LinuxNub aka ei linode) ja päivitin sen `sudo apt-get update` & `sudo apt-get upgrade`. Tämän jälkeen tutkin sillä otsikon komentojen manuaalisivuja `man host` & `man dig`.  

Manuaalin mukaan host on DNS lookup utility eli työkalu, jolla voidaan mm. katsoa perustietoja ip-osoitteen tai domain nimen takaa, kuten ip-osoite ja domain nimi.
Yrittäessäni lukea `dig` -komennon manuaalia huomasin, että sitä ei ollut olemassa.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/37a96a98-2856-41df-b332-7f18040589fb)  

Ystävällinen ankka auttoi minua löytämään internetistä [sivun](https://phoenixnap.com/kb/linux-dig-command-examples "PhoenixNAP - How to Use Linux dig Command (DNS Lookup)") , joka käsitteli `dig` -komentoa. Heti alkuun artikkeli osoitti minulle, että dig komentoa ei voi käyttää, koska sitä käyttävää työkalua ei ole asennettuna. Onneksi sivulla oli luotettava paketinhallintaa hyödyntävä komento `sudo apt-get install dnsutils`. Tämän ajettuani pääsinkin tutkimaan `dig`:n manuaalia, josta minulle selvisi `dig`:n olevan `host`:n tapaan DNS lookup utility, mutta ilmeisesti hiukan monipuolisempi sellainen.  

Tarkistin tässä välissä tehtävän a) nimipalvelun toimivuuden ja kirjasin tulokset tehtävään a). Syötin sitten komennon `host vararikko.xyz` terminaaliin ja sain vastauksena kyseisen nimen IP-osoitteen sekä 5 riviä, jotka ilmoittivat minulle, että vararikko.xyz mail is handled by 10-20 eforwardX.registrar-servers.com.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/c76e4d3f-92af-4727-8a70-3797e25a9cea)

Yritin löytää tietoa näistä mail is handled riveistä, mutta en nopealla googlettamisella saanut tietoja, joten siirryin testaamaan `dig` komentoa. `dig` antoikin ilman lisäparametreja huomattavasti `host` -komentoa kattavamman kasan tietoa:  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/96d0cf06-b8e9-4e9f-bbb3-ece891f4f222)  

Aiemminkin linkittämäni [PhoenixNAP sivuston](https://phoenixnap.com/kb/linux-dig-command-examples "PhoenixNAP - How to Use Linux dig Command (DNS Lookup)") avulla tutkin edessäni olevia rivejä hiukan tarkemmin.  

- `;  <<>> DiG 9.18.19-1~deb12u1-Debian <<>> vararikko.xyz` kertoo suorittamani `dig` -komennon version, käyttöjärjestelmän sekä etsityn kohteen.
 
- `;; global options: +cmd` rivistä en löytänyt lisätietoja.

- Nämä rivit kertovat minkälaisen vastauksen `dig` -komento sai serveriltä. Näitä en osannut enempää avata.  
 `;; Got answer:`  
 `;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63428`  
 `;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1`  

- Nämä rivit jäivät minulle täysin arvoitukseksi.
  `;; OPT PSEUDOSECTION:`  
  `; EDNS: version: 0, flags:; udp: 512`   

- Seuraavat rivit ilmaisevat `dig` -komennon lähettämä kysymystä ja vastausta hieman selkokielisemmin.  
 `;; QUESTION SECTION:` Kysymys osio.  
  `vararikko.xyz.                  IN    A` Itse kyselytieto "vararikko.xyz.". IN = Internet eli kyselyn tyyppi. A = Address eli mitä recordia kysytään.  
  `;; ANSWER SECTION:` Vastaus osio.  
  `vararikko.xyz.          1200    IN    A        172.104.145.15` Samat kuin kysymyksessä paitsi vastauksessa 1200 kertoo sekunneissa TTL, jonka määrittelinkin 20min kohdan a) asetuksia laittaessani. Ja lopuksi kohteen IP-osoite 172.104.145.15.  

-  Lopun neljä riviä sisältävät metadataa eli tietoja itse kyselystä:  
  `;; Query time: 47 msec` Kyselyyn kulunut aika.  
  `;; SERVER: 193.229.0.40#53(193.229.0.40) (UDP)` Kyselyyn vastanneen DNS palvelimen IP-osoite sekä portti (#53) sekä loopback osoite; käsite jota en ymmärtänyt.  
  `;; WHEN: Sun Sep 24 14:19:52 EEST 2023` Kyselyn suorittamisen aika: viikonpäivä, kk, pv, klo, aikavyöhyke, vuosi.  
  `;; MSG SIZE  rcvd: 58` DNS palvelimen vastauksen koko. Oletan sen olevan tavuja.

En kokeillut `host` tai `dig` komentoja millään lisäparametreilla vaan siirryin seuraavaan tehtäväosioon.



## c) Etusivu uusiksi - uudet kotisivut palvelimen etusivuksi  

Tässä tehtävässä tuli tehdä käyttäjän kotisivut käyttäjän kotihakemistoon ja varmistaa, että niiden muokkauksiin ei tarvinnut sudo oikeuksia.  

Otin ssh yhteyden linode virtuaalipalvelimeeni `ssh ali@172.104.145.15`. Päivitin koneen `sudo apt-get update` & `sudo apt-get upgrade`.  
Tässä välissä jouduin pausettamaan virtuaalikoneeni ja palasin 30min päästä takaisin huomatakseni, että ssh yhteys oli katkennut. En tiedä oliko tämä jonkinlainen aikakatkaisu vai oliko se tapahtunut `sudo apt-get upgrade`:n aikana.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/65d0fbe9-8a33-4d12-a2b5-36f817382f5b)

Otin siis uuden ssh yhteyden ja pääsin normaalisti linode koneelleni. Aloin nyt seurailemaan ensimmäisen tiivistämäni artikkelin ohjeita.  

Tarkistin apachen tilan komennolla `sudo systemctl apache2 status`. Näytti pyörivän.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/7eb9809b-f618-4f17-8958-29061dfd0e1f)

Loin uuden VirtualHostin [artikkelin](https://terokarvinen.com/2016/02/16/new-default-website-with-apache2-show-your-homepage-at-top-of-example-com-no-tilde/ "Ensimmäinen artikkeli") ohjeita mukaillen.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/6dea9fa7-5994-4c30-bdb5-83f53eff65b9)

Sudoeditillä muokkaamani tiedosto ali.conf:

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/e1c08819-40a9-4afe-bf18-dedb706728d8)  

Poistin vanhan testisivun käytöstä `sudo a2dissite 000-default.conf`.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/793510cd-2a23-4d61-8bbb-0a14f04bd319)

Käynnistin apachen uudelleen `sudo systemctl restart apache2` ja varmistin että se oli päällä ja käynnistänyt itsensä uudelleen `sudo systemctl status apache2`.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/76aa6175-306d-4562-ad8f-de94e499dfa4)

Kävin katsomassa oikeudet kotihakemistoni public_html hakemistoon.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/acee3b9e-e9ff-4b10-b346-0f97dbce4018)

Yritin käyttää firefoxia virtuaalipalvelimellani, mutta eihän siinä ollut sitä asennettuna. Hetken härväämisen jälkeen syötin komennon `sudo apt-get install gnome-browser-connector` ja kaduin sitä seuraavat 5 minuuttia kun kone asenteli ties mitä. Kun tämä farssi oli ohi jatkoin tehtävän suorittamista. Curlasin localhostin, mutta vastaan tuli 403 forbidden error. Ilmeisesti oikeuteni eivät olleet niin kunnossa kuin luulin.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/6c9aa57f-f56f-4e75-83d3-56b3f129f46f)

Menin katsomaan apachen error lokeja `sudo tail -l /var/log/apache2/error.log` ja ymmärtääkseni siellä kerrottiin, että jossain kohtaa polkua /home/ali/public_html oikeudet loppuivat kesken.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/ba29a623-c1d5-424e-b77f-cddf182caf53)

Yritin käydä koko polun läpi `chmod 744` komennolla. /home oikeuksia en saanut muutettua, joka on todennäköisesti aika hyvä juttu.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/eee39aea-7400-450f-8b47-d5b65b12fe3d)

Löysin `namei` komennon [netin syövereistä](https://cwiki.apache.org/confluence/display/httpd/13PermissionDenied) ja tarkistettuani `namei`:n manuaalista mitä komento tekee, suoritin `namei -m /home/ali/public_html/index.html`. Tämä komento listasi minulle yhteen näkymään koko syöttämäni polun ja käyttäjien oikeudet polun kussakin vaiheessa.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/485bab5a-eb64-4fdc-8a68-a2196d4d05e0)

Ymmärtääkseni tämän hakemistopolun kansioiden ja tiedoston omistajalla (minä?) on oikeus lukea, kirjoittaa ja suorittaa kaikissa polun vaiheissa. Ryhmäläisillä ja muilla käyttäjillä oli oikeus lukea ja suorittaa rootissa sekä /home hakemistossa. ali ja public_html hakemistoissa sekä index.html tiedostossa ryhmällä ja muilla oli vain oikeus lukea.

Tässä vaiheessa päätin hyödyntää puolivalmista raporttiani ja aloin käymään sitä läpi. Huomasin, että poistettuani vanhan testisivun käytöstä en ollut syöttänyt komentoa `systemctl reload apache2`. Niinpä syötin sen ja vastaan tuli uudenlainen tunnistusikkuna. Salasana meni läpi.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/2662ad62-a40f-4446-a070-10be89ece2cd)

Mutta `curl localhost` antoi vieläkin 403 forbiddenia. Eipä ollut apua tästäkään. Kävin vielä varmistamassa, että /home/ali/public_html/index.html oli tehty ja sillä oli sisältöä.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/adf8627c-3465-4b98-8afc-edf56b451ac6)

Tässä vaiheessa mietin, että entä jos lukuoikeudet eivät riitä. No, päätin antaa execute oikeudet koko polulle, yksi kerrallaan.. `chmod 755`..  index.html ei näy kuvassa, mutta sille suoritettiin sama toimenpide.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/61f388d4-96ed-43a1-8246-65c175781642)

Ja sivu toimii... Eli lukuoikeudet eivät riittäneet vaan piti olla oikeudet myös suorittaa.

Kävin vielä muokkaamassa uuden testisivun, josta ilmeni taas ongelmat ääkkösten kanssa virtuaalipalvelimellani.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/67f4c3b3-a4b2-427b-949e-82bf024bb8f4)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/8fdd6b19-c025-4bc4-a018-71f9d8881af9)

Koin tässä vaiheessa suorittaneeni tehtävänannon riittävän hyvin vaikka olisin vielä voinut kokeilla tehdä useampia sivuja saman IP-osoitten alle tällä tekniikalla. Kiitos ja kuittaus.


## **Lähteet**

Tero Karvinen. New Default Website with Apache2 – Show your homepage at top of example.com, no tilde.  
Luettavissa: https://terokarvinen.com/2016/02/16/new-default-website-with-apache2-show-your-homepage-at-top-of-example-com-no-tilde/  
Luettu: 24.9.2023  

Tero Karvinen. Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address.  
Luettavissa: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/  
Luettu: 24.9.2023  

Name-based Virtual Host Support  
Luettavissa: https://httpd.apache.org/docs/2.4/vhosts/name-based.html  
Luettu 24.9.2023

NameCheap. How can I set up an A (address) record for my domain?  
Luettavissa: https://www.namecheap.com/support/knowledgebase/article.aspx/319/2237/how-can-i-set-up-an-a-address-record-for-my-domain/  
Luettu 24.9.2023  

PhoenixNAP. How to Use Linux dig Command (DNS Lookup).
Luettavissa: https://phoenixnap.com/kb/linux-dig-command-examples  
Luettu 24.9.2023  

Cwiki. 13PermissionDenied.  
Luettavissa: https://cwiki.apache.org/confluence/display/httpd/13PermissionDenied  
Luettu 24.9.2023
