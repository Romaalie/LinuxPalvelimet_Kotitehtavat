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





