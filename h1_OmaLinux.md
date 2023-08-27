# Kotitehtäväraportti

Tätä kotitehtävää tehdessäni tutustuin Gitiin, GitHubiin, Laksuun ja siihen kuinka luon virtuaalikoneen ja asennan siihen Linux Debian käyttöjärjestelmän.
Tämän lisäksi kirjoitin pienen tiivistelmän ranskalaisilla viivoilla aiheista raportin kirjoittaminen ja FSF Free Software Definition.

  ## Ohjeistus raportin kirjoittamisesta ja katsaus ilmaiseen softaan ja lisensseihin

    ### Raportin ohjeistus
    
      -Toistettava, täsmällinen, helppolukuinen, viittaa lähteisiin, vakiotekstejä ja pahoja mokia; sisällysluettelolla se tulikin tiivistettyä
      -Raportin tulee olla tarpeeksi tarkka, että siinä kuvaillut asiat voi toistaa. Näin ongelmanratkaisu on helpompaa ja säästyy aikaa.
      -Pidä teksti helppolukuisena ja selkeänä. Säästät tällä paitsi omaa aikaasi kun myöhemmin luet näitä raapustuksia niin mahdollisesti myös jonkun muun aikaa, joka näitä joutuu lukemaan.
      -Kunnia sinne minne kunnia kuuluu ja muiden tekemät virheet ovat myös muiden tekemiä vaikka sinä niitä toistaisit eli muista lähdeviittaukset!
      -Pitäisi kuulua ihan kaikkien perusarvoihin, mutta älä valehtele tuottamassasi sisällössä.

      Tämä tiivistelmä perustuu Tero Karvisen ohjeisiin raportin kirjoittamisesta (https://terokarvinen.com/2006/raportin-kirjoittaminen-4/).
    
    
    ### Lorem ipsum dolor sit amet
      - Lorem ipsum dolor sit amet
      - Lorem ipsum dolor sit amet
      - Lorem ipsum dolor sit amet
      - Lorem ipsum dolor sit amet
      


      (https://www.gnu.org/philosophy/free-sw.html)


  ## Linux virtuaalikoneen asentaminen

    Työ aloitettiin sunnuntaina 27. elokuuta 2023, klo 14.08.  Ohessa lista järjestelmätiedoista:
    Käyttöjärjestelmä: Windows 10 Home 64-bit (10.0, koontiversio 19045.3324)
    BIOS: American Megatrends Inc. 2806, 27.10.2022
    Emolevy: ROG STRIX B550-F GAMING (WI-FI)
    Suoritin: AMD Ryzen 5 5600 6-Core Prosessori
    Muisti: 32768MB RAM
    Näytönohjain: AMD Radeon RX 6800 XT 16337MB VRAM, Ohjainversio 31.0.21023.2010
    DirectX-versio: DirextX 12

    Latasin ohjeiden (https://terokarvinen.com/2021/install-debian-on-virtualbox/) mukaisesti Debianin ISO tiedoston (debian-live-12.1.0-amd64-xfce).
    Koneellani oli valmiiksi asennettuna Oracle VM VirtualBox Manager ohjelma (versio 7.0.6 r155176 (Qt5.15.2)).
    Seurasin ohjeita nimeten kuitenkin oman koneeni "DebianAliRomarCom". Valitsin myös RAM määräksi ohjeista poiketen 8192 MB. Prosessorien lukumääräksi valitsin 4.
    Ohjeista poiketen minulla ei ollut valintavaihtoehtoa "Storage on physical hard disk", enkä näin ollen pystynyt valitsemaan "Dynamically allocated".
    Vaihtoehtona oli klikata laatikko, jossa luki "Pre-allocate Full Size". Jätin tämän laatikon klikkaamatta eli tyhjäksi.
    Tämän jälkeen klikkasin Finish ja virtuaalikone ilmestyi VirtualBox Managerin vasempaan reunaan, kuten ohjeissa kuvailtiin.

    Kun siirryin ohjeissa kohtaan "Insert Debian ISO Image as a Virtual CDROM" oli koneessa jo ilmeisesti valmiina tehty kyseinen vaihe (kuvankaappaukset).

    //MUISTA KUVANKAAPPAUKSET 2KPL

     Kun jatkoin ohjeita eteenpäin ja yritin käynnistää virtuaalikoneeni DebianAliRomarCom, Bootloaderi ei käynnistynyt odotusten mukaisesti vaan tuotti seuraavanlaisen virheen:

     //KUVANKAAPPAUS

     
    
    
    