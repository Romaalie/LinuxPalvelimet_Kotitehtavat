# Kotitehtäväraportti

Tätä raporttia tehdessäni tutustuin komentorivin peruskomentoihin, kirjoitin niistä pienen tiivistelmän ja tutkin miten komentorivi käytännössä toimii suorittamalla kotitehtävissä annettuja tehtäviä.

## Tiivistelmä Command Line Basics Revisited - artikkelista by Tero Karvinen

  -Komennot pwd ja ls kertovat sinulle missä olet ja mitä siellä on.
  
  -Komento cd liikuttaa sinua hakemistopuussa; "cd .." pääset taaksepäin ja cd "X" pääset eteenpäin (tässä tapauksessa hakemistoon X, jos sellainen on saatavilla).
  
  -Artikkelissa listataan myös erinäisiä perus komentoja tiedostojen ja hakemistojen käsittelyyn, etäyhteyden muodostamiseen, manuaalien käyttöön, syötehistorian tutkimiseen sekä tulevan syötteen "arvaamiseen".
  
  -Lopuksi muistutetaan vielä tärkeistä hakemistoista ja käyttöoikeuksien tärkeydestä sekä näytetään miten nethack asennetaan ja poistetaan.

## Käytännön tehtävät

  a) Micro. Asenna micro-editori
  
   Käynnistin virtuaalikoneeni ja aloitin työskentelyn syöttämällä komennot "pwd" ja "ls"; yritin muodostaa tästä tapaa. Syötin myös alkuun komennon "sudo apt-get update" päivittääkseni asioita.
    Tämän jälkeen muistelin, että olin jo asentanut tehtävässä vaaditun micro ohjelman, joten päätin aloittaa poistamalla sen:
    
   ![Micron poisto](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/1_MicronPoisto.JPG)
    
   Linux ilmoitti minulle ystävällisesti, että kun poistat micron niin jälkeen jää tarpeeton paketti xclip, jonka voi poistaa komennolla "sudo apt autoremove". Totta kai halusin kokeilla kyseistä komentoa.
    
   ![Auto Remove](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/2_AutoRemove.JPG)
    
   Hyvin meni. Sitten asentamaan microa uudelleen. Mikäs se komento olikaan..
    
   ![Micron asennus](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/3_MicroAsennus.JPG)
    
  b) Rauta. Listaa testaamasi koneen rauta (‘sudo lshw -short -sanitize’). Asenna lshw tarvittaessa. Selitä ja analysoi listaus.
  
   Lähdin ohjeistuksen mukaan testaamaan "sudo lshw -short -sanitize" komentoa.
   
   ![LSHW asennus](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/4_LshwAsennus.JPG)
   
   Tämän jälkeen toimi paremmin:
   
   ![LSHW näkymä](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/5_LshwNakyma.JPG)
       
   Komento ilmeisesti listaa virtuaalikoneessa olevat laitteet ja erittelee niiden luokan ja antaa kuvauksen. H/W pylvästä en täysin ymmärtänyt. Oletan, että se kertoo virtuaalisen osan "sijainnin".
    Virtuaalikone kuitenkin lukee suoraan oman käyttöjärjestelmäni prosessorin mallin, vaikka siitä on vain osa virtuaalikoneen käytössä.
    Virtuaalikone myös simuloi hauskasti esimerkiksi fyysistä virtanappia.    

  c) Apt. Asenna kolme itsellesi uutta komentoriviohjelmaa. Kokeile kutakin ohjelmaa sen pääasiallisessa käyttötarkoituksessa. Ota ruutukaappaus. Kaikki terminaaliohjelmat kelpaavat, TUI (text user interface) ja CLI (command line interface). Osaatko tehdä apt-get komennon, joka asentaa nämä kolme ohjelmaa kerralla?
  
   Tehtävänäni oli asentaa kolme minulle uutta komentoriviohjelmaa ja kokeilla niitä. Helppoa tästä teki sen, että en tiennyt juurikaan komentoriviohjelmia. Mutta koska, asentamiseen tarvitaan ohjelman nimi...
    Olisiko tehtävänannossa tai muualla samalla sivulla ollut minulle valmiina kolme uutta.
    Löysin git, TUI ja CLI. Mietin tarkoitettiinko kahdella viimeisellä ihan vain terminaalia, mutta eri nimillä vai onko tässä jotain ohjelmia kyseessä. No ei kun kokeilemaan:
    
   ![TUITUI](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/6_TuiTui.JPG)
   
   Joo eli ilmeisesti kyseessä oli vain eri nimiä terminaalille tai komento oli väärin kirjoitettu. Sitten kokeilemaan mikä tämä git on, jonka juuri asensin:
   
   ![GIT](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/7_WhatIsGit.JPG)
   
   Tämä ei vielä kauheasti paljastanut minulle, joten siirryin nettiin tutkimaan (https://allthings.how/how-to-use-git-in-linux/).
    No niin eli jos oikein ymmärsin niin gitin avulla voin siirtyä tekemään esimerkiksi tätä kotitehtävääni, jota nyt kirjoitan selaimella githubiin, vaikka virtuaalikoneellani microlla. Loin testitiedoston ja kokeilin sillä toiminnallisuutta.
    
   ![Testi](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/8_Testitiedosto.JPG)
   
   Yritin ensin kloonata vain yksittäisen tiedoston kunnes ymmärsin, että tällä komennolla kloonataan kokonaisia projekteja.
   
   ![Toiminta](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/9_GitToiminnallisuus.JPG)

   ![MictoTesti](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/10_TestitiedostoMicrossa.JPG)
    
   Success! Ja sitten siirryin etsimään niitä kahta muuta ohjelmaa internetistä (https://www.makeuseof.com/best-linux-terminal/, https://www.omgubuntu.co.uk/2021/11/best-command-line-tools-ubuntu-linux).
    Päädyin vaihtoehtoihin cool-retro-term ja ddrg. Ohjelmat asentuivat näppärästi yhdellä komennolla:
    
   ![Ohjelmat](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/11_ddgrAndCoolretroterm.JPG)
    
   cool-retro-term on vaihtoehtoinen ulkoasu terminaalille. 
    
   ![RetroTerm](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/12_CoolRetroTerm.JPG)
    
   ddrg antaa terminaaliin duckduckgo hakukoneen toiminnallisuuden. Muutaman kerran typottuani sain homman toimimaan.
    
   ![DDGR](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/13_Ddgr.JPG)
    
  d) FHS. Esittele kansiot, jotka on listattu "Command Line Basics Revisited" kappaleessa "Important directories". Näytä kuvaava esimerkki kunkin tärkeän kansion sisältämästä tiedostosta tai kansiosta. Jos kyseessä on tiedosto, näytä siitä kuvaava esimerkkirivi. Työskentele komentokehotteessa ja näytä komennot, joilla etsit esimerkit.
  
   Tässä tehtävässä tutkin Karvisen artikkelin (https://terokarvinen.com/2020/command-line-basics-revisited/) important directories hakemistoja.
    Aloitin juuresta eli /. Juuri on tietojärjestelmän alkupiste ja sieltä pystyy navigoimaan mihin tahansa.
    
   ![ROOT](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/14_Root.JPG)
   
   Menin seuraavaksi katsomaan /home/ hakemistoa, josta löytyy jokaisen käyttäjän omat hakemistot.
    
   ![HOME](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/15_Home.JPG)
    
   Tällä virtuaalikoneella oli vain minun tekemäni käyttäjä, joten oli loogista mennä seuraavaksi tutkimaan sen hakemistoa.

   ![alir](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/16_Alir.JPG)
    
   Tämä hakemisto sisälsi kaikki käyttäjän alir tiedostot ja jos alir olisi koneen normikäyttäjä, tämä olisi ainoa paikka johon hän voisi tallentaa asioita.
    Seuraavaksi siirryimme takaisin juuren kautta sijaintiin /etc/. Tämä hakemisto sisälsi Teron kertoman mukaan kaikki järjestelmän asetustiedostot ja paljon siellä ainakin oli tavaraa.
    
   ![ETC](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/17_Etc.JPG)
   
   Päätin lukea ensimmäisen tiedoston käyttämällä komentoa less adduser.conf
    
   ![adduser](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/18_lessAdduserconf.JPG)
    
   Tämä oli erittäin kiinnostavaa ja ajankohtaista eli siirryin mitä pikimmiten juuren kautta /media/ hakemistoon, jossa Teron kertoman mukaan piti sijaita irrotettava media. En tosin löytänyt täältä mitään muuta kuin oman käyttäjäni hakemiston.

   ![MEDIA](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/19_Media.JPG)
    
   Seuraavaksi edessä oli sijainti /var/log/, jonka piti sisältää koko järjestelmän lokitiedot.
    Navigoin kyseiseen hakemistoon ja yritin lukea less komennolla faillog, lastlog sekä boot.log. Kaksi ensimmäistä olivat tyhjiä ja boot.log kieltäytyi avautumasta, koska käyttäjäoikeudet puuttuivat.
    Annoin komennon uudestaan sudo oikeuksin, syötin salasanan. Kone ilmoitti tiedoston olevan mahdollisesti binary file, mutta päätin kurkata sitä joka tapauksessa.
    
   ![VARLOG](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/20_varLog.JPG)
    
   ![BOOTLOG](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/21_bootlog.JPG)
    
   Karvisen artikkelissa mainitsemia /var/log/syslog, /var/log/auth.log and /var/log/apache2/error.log en löytänyt.

  e) The Friendly M. Näytä 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. Ohjeita löytyy 'man grep' ja tietysti verkosta. & f) Pipe. Näytä esimerkki putkista (pipes, "|").

  Palasin tässä välissä käyttämään terminaalin oletusulkoasua. Tutkin hiukan "grep" komennon manuaalia komennolla "man grep", mutta en siitä suuremmin viisastunut, joten suuntasin internetiin: https://www.howtogeek.com/496056/how-to-use-the-grep-command-on-linux/
 Lueskeltuani linkittämääni artikkelia siirryin kokeilemaan "grep" komentoa käytännössä:

 ![GrepTest](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/22_grepinTestailua.JPG)

 Sen sijaan, että olisin aiemman esimerkin mukaan etsinyt jotain tiettyä riviä tietystä tiedostosta, lisäämällä "grep" komentoon "-r" ja antamalla poluksi esimerkiksi ".", se etsii nykyisen hakemiston lisäksi myös kaikki alihakemistot ja tiedostot.

 ![GrepRecursive](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/23_grepRecursive.JPG)

 Tämän jälkeen pääsin yhdistin tehtävät e ja f antamalla seuraavat esimerkit putkista ja grep komennosta.

 ![PipeGrep](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/24_pipeGrep.JPG)

 Tässä grep hyödyntää sisäänrakennettua putkea, jonka avulla voi etsiä useampaa sanaa:

 ![GrepPipe](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/25_grepPipe.JPG)

  g) Tukki. Aiheuta lokiin kaksi eri tapahtumaa: yksi esimerkki onnistuneesta ja yksi esimerkki epäonnistuneesta tai kielletystä toimenpiteestä. Analysoi rivit yksityiskohtaisesti.

  Tätä raporttia tehdessäni törmäsin kohdassa d) ongelmaan. En löytänyt esimerkiksi sijaintia /var/log/syslog ja nyt minun piti analysoida järjestelmälokeja joiden piti löytyä kyseisestä sijainnista. No, lukemalla README tiedoston sijainnista /var/log/ minulle selvisi, että virtuaalikoneeni käyttöjärjestelmässäni on system and service manager, joka kerää lokit yhteen paikkaan ja journalctl on komento, jolla lokeja tutkitaan (https://www.howtogeek.com/499623/how-to-use-journalctl-to-read-linux-system-logs/). Tietysti kotitehtävienkin vinkeissä oli lokiin liittyvä komento journalctl -f ja sudo journalctl. Yritin tuottaa lokiin epäonnistuneen salasanan kirjoituksen sudo oikeuksia varmistettaessa.

  ![InstallMaybe](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/26_AsennusYritys.JPG)

  Seuraavasta kuvasta ymmärsin, että lokiin kirjautuu pvm, kellonaika, koneen nimi, käyttäjä jonka tekeminen on jäänyt lokiin ja sen jälkeen mitä on tehty. Tässä tapauksessa ilmeisesti käyttäjä id:llä 1000 eli alir oli epäonnistunut antamaan sudo salasanaa. 12 sekuntia myöhemmin tässä toimenpiteessä on lokien mukaan onnistuttu.

  ![LoginError](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/27_loginError.JPG)
