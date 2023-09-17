
# Kotitehtäväraportti h4

Tässä raportissa tutustuin ensin Tero Karvisen artikkeliin yksityisen virtuaalisen palvelimen pystyyn laittamisesta, tiivistin artikkelin ja lähdin sen pohjalta toteuttamaan kotitehtäviä eli oman palvelimen pystyyn laittamista. Lopuksi yritin vielä etsiä lokeista merkkejä siitä, että palvelimelleni olisi yritetty saada luvaton yhteys tmv.

## x) Tiivistelmä Tero Karvisen artikkelista [First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ "Karvisen näppärä artikkeli")

Tärkein pointti koko artikkelissa oli hyvät salasanat. Käytä aina pelkästään hyviä salasanoja.  
Käytännössä artikkeli käsitteli oman serverin pystyyn laittamista vuokraamalla pilvipalvelusta virtuaalikone. Aihe oli minulle sen verran ajankohtainen ja halusin selventää sitä itselleni, joten tiivistelmästä ei tullut kovin tiivis.

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

Aloitin tehtävän käynnistämällä oman virtuaalikoneeni ja suorittamalla komennon `sudo apt-get update`. Jätin koneen sen jälkeen pause tilaan suorittaessani muita tehtävän askeleita.

Googletin tunnillakin muistaakseni käytettyä palvelun tarjoajaa Linodea ja löysin saman tarjouksen, jonka muistin tunnilla nähneeni.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/8f147dc5-1c23-4bd2-bd8b-88a1dd5fae43)

Valitsin tilin luomisen vaihtoehdoista email. Pienten ongelmien jälkeen sain tilin luotua.  
Pääsin luomaan uutta virtuaalikonetta Linodeen.  
Valitsin käyttöjärjestelmäksi Linux Debian 12, alueeksi Frankfurt, DE (eu-central), Linode planiksi "Shared CPU" ja sieltä Nanode 1 GB.  
Nimesin koneen "KuuleekoMaailma" ja asetin root käyttäjälle hyvän salasanan.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/51e9236a-53a3-4a08-bac7-3ff8fcbdc9e2)

Hyväksyin yhteenvedon ja Linode alkoi luomaan konetta. Kun kone oli luotu sain sen IP-osoitteen selville koneen linode sivulta.
Tämän jälkeen siirryin pausetetun virtuaalikoneeni terminaaliin ja otin yhteyttä koneeseen komennolla `ssh root@172.104.XXX.XX`.
Minulta varmisteltiin koneen luotettavuutta ja salausavaimia. Vastasin kyllä kyllä ja homma jatkui.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/e0d02361-3943-465a-8455-cbae6bd17e45)

Tämän jälkeen minua varoitettiin, että kyseinen ip-osoite oli lisätty tunnettujen hostien listalle ja linode koneeni sulki yhteyden. Otin uudelleen yhteyttä komennolla `ssh root@172.104.XXX.XX`. Ja linode kone kysyi rootin salasanaa. Syötin salasanan ja olin etäkäyttötilassa.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/b0e87503-fd87-4221-8900-7c282f568ab8)

## b) Alkutoimet

Karvisen alussa tiivistämää artikkelia noudattaen aloin valmistelemaan juuri luomaani konetta. Ensin tarkoituksenani oli tehdä aukko palomuuriin ssh etäkäyttöyhteyttäni varten ja sitten laittaa palomuuri päälle. Aloitin komennolla `sudo ufw allow 22/tcp`. Tämä ei luonnollisestikaan toiminut, koska ufw ei ollut asennettuna. Varmistin, että vikaa ei ollut terminaalissani ja olin varmasti linode koneen hakemistoissa komennoilla `pwd` ja `ls`. Tämän jälkeen yritin asentaa ufw:n muistelemallani komennolla `sudo apt install ufw`. Aluksi näytti lupaavalta, mutta ei.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/4d67f077-5bfe-498e-b139-3b45680008ca)

Tämän jälkeen yritin komennolla `sudo apt-get install ufw`. Jälleen sama ongelma.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/465e5a9f-7cb4-4ad2-b98e-84a8efae697f)

Yritin seuraavaksi päivitellä tiedostojani komennolla `sudo apt-get update`.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/77b519b4-af91-4766-b946-d88f45d220bb)

Tämän jälkeen yritin uudelleen avata porttia 22 TCP yhteyksille. No eihän se ufw ollut vieläkään asennettuna. Turhautuneena yritin aiemmin laittamiani komentoja kunnes `sudo apt install ufw` toimi ja jostain syystä ufw suostui nyt asentumaan. Ehkä syynä oli aiemmin syöttämäni `sudo apt-get update`. Valitettavasti unohdin ottaa kuvankaappauksen tästä kohdasta. Kun ufw oli asennettuna sain haluamani reiän tehtyä palomuuriin (`sudo ufw allow 22/tcp`).

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/52da8531-7065-4241-8567-263e6a31929d)

Tämän jälkeen kytkin palomuurin päälle komennolla `sudo ufw enable` ja minua varoitettiinkin mahdollisista häiriöistä ssh yhteyksiin.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/f838c530-09fc-4443-8e3a-6a83287ce4a4)

Palomuuri oli päällä ja sitten aloin luomaan uutta käyttäjää ja lisäämään tätä [Karvisen artikkelin](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ "aiemmin tiivistetty artikkeli") mainitsemiin ryhmiin.  
Komennolla `sudo adduser ali` loin koneelle uuden käyttäjän "ali". Muistin käyttää hyvää salasanaa.
Sen jälkeen lisäsin tämän uuden käyttäjän ryhmiin sudo, adm ja admin seuraavilla komennoilla: `sudo adduser ali sudo`, `sudo adduser ali adm`, `sudo adduser ali admin`.  


Komennon `sudo adduser ali admin` kohdalla vastaani tuli virhe, jossa ilmoitettiin, että kyseistä ryhmää ei ole olemassa. Aiemmat kaksi komentoa menivät hyvin läpi.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/a2b1141f-30b8-4525-8123-7d5ce5ba7a86)

En reagoinut tähän ilmoitukseen mitenkään vaan jatkoin työtäni eteenpäin eli avasin uuden terminaalin omalla virtuaalikoneellani, jonka kautta muodostin etäyhteyden linode koneeseeni käyttäen juuri luomaani käyttäjää "ali". Onnistuin kirjautumisessa ja jonkin ajan päästä suljin terminaalin jonka kautta olin root etäyhteydellä kirjautuneena.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/1f4fbcb8-c057-4a37-988e-051b9c5092e8)

Tämän jälkeen tarkoituksenani oli lukita kirjautuminen root tilillä. Käytin tähän komentoa `sudo usermod --lock root`. Kyseinen komento käyttää sudo oikeuksia muokkaamaan käyttäjän tiliä. Tässä tapauksessa sillä lukittiin (--lock tai -L) käyttäjän salasana lisäämällä salakirjoitetun salasanan eteen ! (lähde: man usermod).

Seuraavaksi seurasin [Karvisen artikkelin](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/ "aiemmin tiivistetty artikkeli") ohjeita ja editoin root käyttäjän oikeuksia muodostaa ssh yhteys: `sudoedit /etc/ssh/sshd_config`.
Kyseiseen tiedostoon piti lisätä rivi "PermitRootLogin no". Tai ainakin oletin, että rivi piti lisätä, koska en sellaista sieltä valmiina löytänyt edes pois toiminnasta kommentoituna.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/3a07aff1-e657-4797-84fb-9526a41ac211)

Tallennusvaiheessa minulta kyseltiin vielä varmuuskopiointia. Valitsin vaihtoehdon M-B (eli alt + B).

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/f36fe968-8b67-427a-88e1-21e6c96b2560)

Tallennus ilmeisesti onnistui, koska avasin tiedoston uudestaan ja lisäämäni rivi oli siellä.  

Yritin vielä kirjautua ssh yhteydellä uudestaan sisään rootina eikä se onnistunut. Tästä päättelin muokkausteni tehneen sen mitä pitikin.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/135d507f-1f9c-4818-bbdf-65baca45c845)

Lopuksi päätin suorittaa vielä [tehtävänannon vinkeissä](https://terokarvinen.com/2023/linux-palvelimet-2023-alkusyksy/ "Karvinen, h4 Maailma kuulee; vinkit") mainitut komennot

`sudo apt-get update`, `sudo apt-get dist-upgrade` ja `sudo systemctl reboot`. dist-upgrade komennosta luin lisää [täältä](https://itsfoss.com/apt-get-upgrade-vs-dist-upgrade/ "itsfoss artikkeli"). Päivitysten jälkeen reboot komento käynnisti järjestelmän uudestaan ja luonnollisesti sulki ssh yheyteni palvelimeen.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/3eed227c-8285-4483-8ca3-4847c960e86e)

Päätin heti yhteyden suljettua ottaa yhteyttä uudestaan, mutta palvelin ei ilmeisesti ollut ehtinyt käynnistyä uudelleen. Odottelin noin 30 sekuntia kunnes kokeilin syöttää komentoriville komennon `echo $`, joka näytti tyhjää, kokeillakseni oliko virtuaalikoneeni kaatunut. Sitten tappoin yhteydenotto ohjelman painamalla ctrl+C. Kokeilin noin minuutin päästä uudelleen ja sain etäyhteyden muodostettua uudelleen.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/96650f17-fe35-4887-8f77-658cbb9b17bb)


## c) Weppipalvelin ja kaikille avoin sivu

Nyt oli tarkoitus pistää tälle uudelle linode virtuaalikoneelle apache2 weppipalvelin pyörimään, korvata testisivu ja varmistaa, että se näkyy julkisesti. Mieluusti myös eri laitteilla. Aloitin asentamalla apache2: `sudo apt-get install apache2`. Sitten tein apache2:lle reiän palomuuriin: `sudo ufw allow 80/tcp`.  
Tarkistin komennolla `sudo ufw status` palomuurin nykyisen tilan ja säännöt. Palomuuri oli päällä ja siellä oli sallimani reiät ssh yhteydelle ja apache2:lle.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/7f8a9f55-a0c3-4096-9020-0ed682087949)  

Tämän jälkeen seurasin [aiemman kotitehtävän artikkelin ohjeita](https://terokarvinen.com/2008/05/02/install-apache-web-server-on-ubuntu-4/) ja varmistin vielä komennolla `ip addr` linode koneen ip-osoitteen. Kyllä, se oli sama mikä aiemminkin oli tullut ilmi ssh yhteyden muodostamisessa.  
Käynnistin komennolla `sudo a2enmod userdir` apache2:n käyttäjäsivut, joskin sain outoja varoituksia.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/a2eb6ffc-148f-4458-b8c9-95b2dbeb749c)  

Jos ymmärsin oikein niin jostain asetuksista puuttui kielen määrittäminen, joten käyttöön otettiin englanti. Ymmärtääkseni kuitenkin komentoni suoritettiin onnistuneesti.  
Käynnistin tämän jälkeen apache2 demonin uudelleen komennolla `sudo systemctl restart apache2`, kuten ohjetekstissäkin kehotettiin tekemään.  
Loin seuraavaksi käyttäjäni kotikansioon hakemiston public_html ja varmistin, että se oli oikean käyttäjän kotikansiossa. Aikeenani oli tehdä ali käyttäjälle jonkinlaiset omat nettisivut.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/712b4213-31ab-4777-bfed-238c8714bd35)  

Tässä kohtaa kuitenkin väsymys iski ja koin helpoimmaksi vain tehdä nopea muutos apachen testisivulle komennolla `echo TestisivunMuutosHAhaHaHHaahaa|sudo tee /var/www/html/index.html`.  
Kävin kokeilemassa muutoksen toimivuutta virtuaalikoneeni (ei linode) firefox selaimella sekä kännykkäni selaimella. Molemmat toimivat.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/1a258476-3605-4494-8f8d-306093908ae1)  

_Tee tähän vielä omat kotisivut jos jaksat_

## d) Lokien tutkiminen

_Tutki lokeja ja etsi tunkeutujia_


## **Lähteet**

Tero Karvinen. First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS. Luettavissa: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/  
Luettu 17.9.2023

freecodecamp. sudo apt-get update vs upgrade – What is the Difference?. Luettavissa: https://www.freecodecamp.org/news/sudo-apt-get-update-vs-upgrade-what-is-the-difference/  
Luettu 17.9.2023

IT'S FOSS. What's the difference between apt-get upgrade vs dist-upgrade? Luettavissa: https://itsfoss.com/apt-get-upgrade-vs-dist-upgrade/  
Luettu 17.9.2023
