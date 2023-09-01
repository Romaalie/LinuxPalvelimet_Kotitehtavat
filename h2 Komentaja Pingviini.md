![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/4b2a4e7c-1182-4ff2-b623-7b3e80b93c56)# Kotitehtäväraportti

Tätä raporttia tehdessäni tutustuin komentorivin peruskomentoihin, kirjoitin niistä pienen tiivistelmän ja tutkin miten komentorivi käytännössä toimii suorittamalla kotitehtävissä annettuja tehtäviä.

## Tiivistelmä Command Line Basics Revisited - artikkelista by Tero Karvinen

  -Komennot pwd ja ls kertovat sinulle missä olet ja mitä siellä on.
  
  -Komento cd liikuttaa sinua hakemistopuussa; "cd .." pääset taaksepäin ja cd "X" pääset eteenpäin (tässä tapauksessa hakemistoon X, jos sellainen on saatavilla).
  
  -Artikkelissa listataan myös erinäisiä perus komentoja tiedostojen ja hakemistojen käsittelyyn, etäyhteyden muodostamiseen, manuaalien käyttöön, syötehistorian tutkimiseen sekä tulevan syötteen "arvaamiseen".
  
  -Lopuksi muistutetaan vielä tärkeistä hakemistoista ja käyttöoikeuksien tärkeydestä sekä näytetään miten nethack asennetaan ja poistetaan.

## Käytännön tehtävät

  a)
    Käynnistin virtuaalikoneeni ja aloitin työskentelyn syöttämällä komennot "pwd" ja "ls"; yritin muodostaa tästä tapaa. Syötin myös alkuun komennon "sudo apt-get update" päivittääkseni asioita.
    Tämän jälkeen muistelin, että olin jo asentanut tehtävässä vaaditun micro ohjelman, joten päätin aloittaa poistamalla sen:
    KUVANKAAPPAUS 1
    Linux ilmoitti minulle ystävällisesti, että kun poistat micron niin jälkeen jää tarpeeton paketti xclip, jonka voi poistaa komennolla "sudo apt autoremove". Totta kai halusin kokeilla kyseistä komentoa.
    KUVANKAAPPAUS 2
    Hyvin meni. Sitten asentamaan microa uudelleen. Mikäs se komento olikaan..
    KUVANKAAPPAUS 3
    
  b)
    Lähdin ohjeistuksen mukaan testaamaan "sudo lshw -short -sanitize" komentoa.
    KUVANKAAPPAUS 4
    Tämän jälkeen toimi paremmin:
    KUVANKAAPPAUS 5
    Komento ilmeisesti listaa virtuaalikoneessa olevat laitteet ja erittelee niiden luokan ja antaa kuvauksen. H/W pylvästä en täysin ymmärtänyt. Oletan, että se kertoo virtuaalisen osan "sijainnin".
    Virtuaalikone kuitenkin lukee suoraan oman käyttöjärjestelmäni prosessorin mallin, vaikka siitä on vain osa virtuaalikoneen käytössä.
    Virtuaalikone myös simuloi hauskasti esimerkiksi fyysistä virtanappia.    

  c)
    Tehtävänäni oli asentaa kolme minulle uutta komentoriviohjelmaa ja kokeilla niitä. Helppoa tästä teki sen, että en tiennyt juurikaan komentoriviohjelmia. Mutta koska, asentamiseen tarvitaan ohjelman nimi...
    Olisiko tehtävänannossa tai muualla samalla sivulla ollut minulle valmiina kolme uutta.
    Löysin git, TUI ja CLI. Mietin tarkoitettiinko kahdella viimeisellä ihan vain terminaalia, mutta eri nimillä vai onko tässä jotain ohjelmia kyseessä. No ei kun kokeilemaan:
    KUVANKAAPPAUS 6
    Joo eli ilmeisesti kyseessä oli vain eri nimiä terminaalille tai komento oli väärin kirjoitettu. Sitten kokeilemaan mikä tämä git on, jonka juuri asensin:
    KUVANKAAPAUS 7
    Tämä ei vielä kauheasti paljastanut minulle, joten siirryin nettiin tutkimaan (https://allthings.how/how-to-use-git-in-linux/).
    No niin eli jos oikein ymmärsin niin gitin avulla voin siirtyä tekemään esimerkiksi tätä kotitehtävääni, jota nyt kirjoitan selaimella githubiin, vaikka virtuaalikoneellani microlla. Loin testitiedoston ja kokeilin sillä toiminnallisuutta.
    KUVANKAAPPAUS 8
    Yritin ensin kloonata vain yksittäisen tiedoston kunnes ymmärsin, että tällä komennolla kloonataan kokonaisia projekteja.
    KUVANKAAPPAUS 9
    KUVANKAAPPAUS 10
    Success! Ja sitten siirryin etsimään niitä kahta muuta ohjelmaa internetistä (https://www.makeuseof.com/best-linux-terminal/, https://www.omgubuntu.co.uk/2021/11/best-command-line-tools-ubuntu-linux).
    Päädyin vaihtoehtoihin cool-retro-term ja ddrg. Ohjelmat asentuivat näppärästi yhdellä komennolla:
    KUVANKAAPPAUS 11
    cool-retro-term on vaihtoehtoinen ulkoasu terminaalille. 
    KUVANKAAPPAUS 12
    ddrg antaa terminaaliin duckduckgo hakukoneen toiminnallisuuden. Muutaman kerran typottuani sain homman toimimaan.
    KUVANKAAPPAUS 13
    
  d)
    Tässä tehtävässä tutkin Karvisen artikkelin (https://terokarvinen.com/2020/command-line-basics-revisited/) important directories hakemistoja.
    Aloitin juuresta eli /. Juuri on tietojärjestelmän alkupiste ja sieltä pystyy navigoimaan mihin tahansa.
    KUVANKAAPPAUS 14
    Menin seuraavaksi katsomaan /home/ hakemistoa, josta löytyy jokaisen käyttäjän omat hakemistot.
    KUVANKAAPPAUS 15
    Tällä virtuaalikoneella oli vain minun tekemäni käyttäjä, joten oli loogista mennä seuraavaksi tutkimaan sen hakemistoa.
    KUVANKAAPPAUS 16
    Tämä hakemisto sisälsi kaikki käyttäjän alir tiedostot ja jos alir olisi koneen normikäyttäjä, tämä olisi ainoa paikka johon hän voisi tallentaa asioita.
    Seuraavaksi siirryimme takaisin juuren kautta sijaintiin /etc/. Tämä hakemisto sisälsi Teron kertoman mukaan kaikki järjestelmän asetustiedostot ja paljon siellä ainakin oli tavaraa.
    KUVANKAAPPAUS 17
    Päätin lukea ensimmäisen tiedoston käyttämällä komentoa less adduser.conf
    KUVANKAAPPAUS 18
    Tämä oli erittäin kiinnostavaa ja ajankohtaista eli siirryin mitä pikimmiten juuren kautta /media/ hakemistoon, jossa Teron kertoman mukaan piti sijaita irrotettava media. En tosin löytänyt täältä mitään muuta kuin oman käyttäjäni hakemiston.
    KUVANKAAPPAUS 19
    Seuraavaksi edessä oli sijainti /var/log/, jonka piti sisältää koko järjestelmän lokitiedot.
    
    
    
    
    
    

            
