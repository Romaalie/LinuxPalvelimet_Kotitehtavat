# Kotitehtäväraportti h3

Tässä raportissa tutustuin Tero Karvisen [artikkeliin](https://terokarvinen.com/2008/05/02/install-apache-web-server-on-ubuntu-4/) Apache 2 web serverin asentamisesta ja tiivistin kyseisen artikkelin, jonka jälkeen lähdin sen pohjalta tekemään omia kotisivuja virtuaalikoneellani.

## x) [Artikkelin](https://terokarvinen.com/2008/05/02/install-apache-web-server-on-ubuntu-4/) tiivistäminen

Artikkelissa opastettiin askel askeleelta kuinka apache 2 web serveri asennetaan Ubuntu 6.06 LTS Dapperille, mutta mainitaan, että ohjeet toimivat todennäköisesti kaikissa Ubuntu pohjaisissa distroissa.

Artikkelin pääkohdat olivat:
- Apachen asentaminen sudo oikeuksin
  - asennuksen onnistumisen testaaminen localhost osoitteen avulla
  - ip osoitteesi selvittäminen
- Käyttäjän kotisivujen mahdollistaminen
  - a2enmod moduulin käyttöönotto
  - apachen uudelleenkäynnistys asetuksien muutosten voimaan tulemiseksi
- Kotisivujen testaus
  - public_html kansion luonti käyttäjän kotihakemistoon
  - oman käyttäjänimen varmistus "whoami" komennolla
  - nettiselaimella siirtyminen localhost + käyttäjänimesi
 
## a) Apache-weppipalvelimen asennus ja testaus

Käynnistin virtuaalikoneeni kuten aiempina viikkoina ja ajoin terminaalissa alkuun komennon "sudo apt-get update". Tämän jälkeen seuraten tehtävässä x) tiivistämääni Karvisen artikkelia aloin asentamaan apache 2 web serveriä. Huomasin kuitenkin jo asentaneeni apache2 aiemmin. Oletin sen siis olevan myös päällä enkä syöttänyt komentoa "sudo systemctl start apache2".

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/5783592e-32ec-42f0-aa88-0afd3083854b)

Syötin terminaaliin komennon "firefox 'http:<area>//localhost' " ja virtuaalikone avasi firefox selaimen ja sieltä apache 2 debian default pagen. Apache 2 web serveri oli siis toiminnassa.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/69d337a0-1d71-4772-806e-1e32b0dfced1)

Siirryin takaisin terminaaliin jatkamaan tehtävän suorittamista, mutta terminaalissa minua odotti ilmoitus puuttuvista asioista:

"Missing chrome or resource URL: resource://gre/modules/UpdateListener.jsm

Missing chrome or resource URL: resource://gre/modules/UpdateListener.sys.mjs"

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/488c1bbc-4416-4cd3-a7a3-fb0e4c54584f)

Kiireisenä opiskelijana minulla ei ollut aikaa tutkia tätä virheilmoitusta sen tarkemmin.

## b) Apache lokin tutkiminen

Suuntasin komentorivin avulla sijaintiin /var/log, josta löysinkin hakemiston /apache2/. Yritin siirtyä hakemistoon komennolla "cd apache2", mutta minulta evättiin pääsy. Myöskään komennolla "sudo cd apache2" en päässyt sisään, koska cd komentoa ei voinut jostain syystä suorittaa sudo oikeuksin.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/eaaf59f5-3c8b-42cb-b0bc-2004dafad3f0)

Tämän jälkeen yritin katsoa hakemistoon apache2 komennolla "sudo ls /var/log/apache2" ja se onnistui. Täältä löysin access.login, jota pääsin lukemaan komennolla "sudo less /var/log/apache2/access.log". Ja löysinkin kohdan lokista, joka käsitteääkseni syntyi kun siirryin firefoxilla omaan ip osoitteeseeni.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/84318b16-8497-4c74-8da4-13471cacd6fb)

Lokissa kerrottiin mihin ip osoitteeseen oli otettu yhteyttä, päivämäärä ja kellonaika sekä aikavyöhyke ilmeisesti GMT aikavyöhykkeiden mukaan. Tämän jälkeen loki ymmärtääkseni kertoi mikä sivu oli avattu sekä millä selaimella ja käyttöliittymällä oli otettu yhteyttä.

## c) Apachen esimerkkisivun vaihtaminen

Tätä tehtävää tehdessäni tutustuin tarkemmin "[tee](https://linuxize.com/post/linux-tee-command/)" komennon käyttöön. Tämän jälkeen syötin Karvisen vinkeissä ilmoitetun komennon hieman muokattuna "echo BarFuu|sudo tee /var/www/html/index.html" ja tarkistin sen toimivuuden siirtymällä "kotisivulleni".

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/5202195b-6cec-4391-96ef-45db5e1c3137)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/50017c81-9ea0-41ea-b5d7-2374e30ebdde)

## d) Käyttäjän kotisivujen käyttöönotto ja käyttöoikeuksien antaminen normaalille käyttäjälle

Hyödynsin tässä tehtävässä aiemmin kohdassa x) tiivistämääni Karvisen artikkelia käyttäjän kotisivujen käyttöönotosta. Aloitin uuden päivän virtuaalikoneessani terminaalikomennolla "sudo apt-get update", jonka jälkeen syötin komennot "sudo a2enmod userdir" sekä "sudo systemctl restart apache2".

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/17950c83-4669-4631-8b6f-1269ba8c0f45)

Testatakseni toimivatko syöttämäni komennot halutulla tavalla, minun tuli ensin luoda omaan kotihakemistooni (/home/alir) uusi kansio, joka onnistui komennolla "mkdir public_html". Tarkistin "ls" komennolla, että uusi kansio oli ilmestynyt. Tämän jälkeen varmistin komennolla "whoami" käytössä olevan kirjautumistunnukseni (alir). Sitten avasin firefoxilla juuri luomani "kotisivun" komennolla "firefox http:<a>//localhost/~alir".

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/81605b23-186f-4262-933b-cf1b158deb5e)

Toimii.

Varmistin kuitenkin vielä, että käyttäjällä oli tarpeeksi oikeuksia juuri luodussa public_html kansiossa. Syötin komennon "stat public_html" kun olin kotihakemistossani /home/alir, jonne olin kyseisen public_html kansion luonut.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/6af5b951-e8e1-437a-a7ab-7d44a7ecefe6)

Kohdasta "Access: (0755/drwxr-xr-x) minulle selvisi, että käyttäjällä oli kansioon täydet oikeudet, käyttäjän ryhmällä oli oikeudet lukea ja suorittaa, muilla oli oikeudet vain suorittaa.

## e) Validin HTML5 sivun luominen

Yritin ensin siirtää Johdanto Digitaalisiin palveluihin kurssille tekemääni sivustoa virtuaalikoneelle koska kyseinen sivusto oli jo valmiiksi validoitu, mutta jostain syystä en saanut kuvien siirtoa toimimaan virtuaalikoneen ja oman koneeni välillä, joten päädyin käyttämään Karvisen tehtävänannon vinkeissä olevaa lyhyttä [sivua](https://terokarvinen.com/2012/short-html5-page/). Loin aiemmassa tehtävässä tekemääni public_html kansioon microlla tiedoston index.html ja kopioin Karvisen lyhyen koodipätkän tiedostoon. Tallensin ja suljin tiedoston. Avasin firefoxilla localhostin aiempien tehtäväkohtien tyyliin eli testasin ratkaisuni toimivuutta:

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/9ecf6e34-fb82-4ee9-befd-8fb243269809)

Toimi.

Olisin tässä vaiheessa voinut vielä selvittää miten voisin validoida validator.w3.org. sivulla kyseisen sivun, mutta minulla ei ollut aikaa selvittää kuinka saisin tehtyä sen virtuaalikoneessa (julkinen ip jne..), joten jätin sen tekemättä.

## f) Curl komento

Tutustuin curl komentoon kahden eri nettisivun avulla: [1](https://phoenixnap.com/kb/curl-command), [2](https://linuxize.com/post/curl-command-examples/). Ymmärtääkseni siis curlia käytetään datan siirtämiseen eri verkkoprotokollia hyödyntäen. Yksinkertainen tapa käyttää curlia on syöttää "curl _Nettisivu_", jolloin curl palauttaa sivun lähdekoodin.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/e859e9ed-3957-4c94-a395-26cae31e4aa6)

Tehtävänannossa minulle tuotti ongelmia saada selvää oliko seuraavaksi pyydetty komento curl -I vai curl -l. Lopulta päädyin komentoon curl -I, sillä se oli noista kahdesta se komento, joka tuotti erilaisen tuloksen ja sitä oli mielestäni järkevämpi lähteä analysoimaan, joskaan en tehnyt sitä kovin menestyksekkäästi. Aiemmin ilmoittamiltani apusivuilta selvisi, että tämä komento hakee HTTP headerit, mutta tämä ei minulle selventänyt yhtään sen enempää tilannetta kuin eteeni ilmestynyt tekstivirta.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/8bd83535-0666-4ec6-bf9a-b06f058b97f6)

Eli en osannut kertoa tästä listauksesta käytännössä yhtään mitään hyödyllistä. Oletan, että siinä listataan jotain hakemani example.com sivuston tietoja. Yritin lueskella [lisätietoja](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers), mutta tämä ei avannut asiaa minulle juurikaan enempää.
