# Kotitehtäväraportti

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
    
