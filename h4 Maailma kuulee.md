
# Kotitehtäväraportti h4

Tässä raportissa tutustuin ensin Tero Karvisen artikkeliin yksityisen virtuaalisen palvelimen pystyyn laittamisesta, tiivistin artikkelin ja lähdin sen pohjalta toteuttamaan kotitehtäviä eli oman palvelimen pystyyn laittamista. Lopuksi yritin vielä etsiä lokeista merkkejä siitä, että palvelimelleni olisi yritetty saada luvaton yhteys tmv.

## x) Tiivistelmä Tero Karvisen artikkelista [First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ "Karvisen näppärä artikkeli")

Tärkein pointti koko artikkelissa oli hyvät salasanat. Käytä aina pelkästään hyviä salasanoja.
Artikkeli käsitteli oman serverin pystyyn laittamista vuokraamalla pilvipalvelusta virtuaalikone. Aihe oli minulle sen verran ajankohtainen ja halusin selventää sitä itselleni, joten tiivistelmästä ei tullut kovin tiivis.

- Luo tili jollekin palveluntarjoajalle, tässä voi hyödyntää erilaisia tutustumistarjouksia tai GitHub Education student pakettia.
  - Valitse datakeskuksen sijainti mahdollisten asiakkaidesi mukaan. Ei serveriä japanista jos asiakkaasi ovat euroopassa.
  - Luo virtuaalinen linux (Ubuntu 16.04 LTS artikkelissa) vuokraamallesi koneelle. Tai siis valitse haluamasi käyttöjärjestelmä, palveluntarjoaja luo virtuaalikoneen sinulle.
  - Tarkista uuden koneesi salasana ja IP-osoite.
  - Kirjaudu tälle uudelle virtuaalikoneelle etäyhteyden kautta eli syöttämällä oman koneesi (tai oman toisen virtuaalikoneesi) terminaaliin komento ```ssh root@10.0.0.1.```          Korvaa esimerkin IP-osoite pilvipalvelun virtuaalikoneesi osoitteella. Näin otat root käyttäjänä ssh (secure shell, salattu tietoliikenne protokolla) etäyhteyden uuteen           koneeseen.

- Palomuuri
    - Aluksi on tärkeää ottaa käyttöön palomuuri. Tämä suojaa konettasi epätoivotuilta kaappareilta ja muilta tietojen urkkijoilta. Ennen muurin käyttöönottoa siihen tulee luoda aukko, jotta voit käyttää itse konetta etäyhteydellä.
    - Aukko luodaan komennolla ```sudo ufw allow 22/tcp```; tämä komentoo käskee sudo oikeuksin ohjelmaa uncomplicated firewall sallimaan tcp protokollaa käyttävän liikenteen portissa 22.
    - Kun olet luonut itsellesi aukon voit kytkeä palomuurin päälle komennolla ```sudo ufw enable```.

- Uusi käyttäjä
  - Luodaan koneelle uusi käyttäjä ja lisätään hänet ryhmiin sudo, adm ja admin.
  - Kokeillaan toimenpiteiden onnistumista. Yritetään ottaa ssh yhteys uudesta terminaali ikkunasta tällä uudella käyttäjällä.
  - Jos käyttäjä toimii voi rootin sulkea ja lukita sekä estää rootin käyttö ssh yhteydellä.
 
- Perinteiset päivitykset eli ```sudo apt-get update```, ```sudo apt-get upgrade```. Nämä ovat tosiaan [eri komentoja](https://www.freecodecamp.org/news/sudo-apt-get-update-vs-upgrade-what-is-the-difference/ "freecodecamp opas artikkeli").

- Asennetaan apache2 ja luodaan sille aukko palomuuriin ```sudo ufw allow 80/tcp```.

- Domain nimen hankkiminen on melkolailla olennaista jos aikoo käyttää serveriä lähes mihinkään muuhun kuin omiin harjoitteluihinsa, koska harvempi ihminen kirjoittelee selaimeensa suoraa ip osoitteita saati muistaa niitä. Julkinen DNS nimi eli domain nimi on mahdollista ostaa erillisiltä palveluntarjoajilta kuten NameCheap.

## a) Oman virtuaalipalvelimen vuokraaminen





## **Lähteet**

Tero Karvinen. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ Luettu 17.9.2023

freecodecamp. sudo apt-get update vs upgrade – What is the Difference?. Luettavissa: https://www.freecodecamp.org/news/sudo-apt-get-update-vs-upgrade-what-is-the-difference/ Luettu 17.9.2023

