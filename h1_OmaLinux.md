# Kotitehtäväraportti

Tätä kotitehtävää tehdessäni tutustuin Gitiin, GitHubiin, Laksuun ja siihen kuinka luon virtuaalikoneen ja asennan siihen Linux Debian käyttöjärjestelmän.
Tämän lisäksi kirjoitin pienen tiivistelmän ranskalaisilla viivoilla aiheista raportin kirjoittaminen ja FSF Free Software Definition.

  ## Ohjeistus raportin kirjoittamisesta ja katsaus ilmaiseen softaan ja lisensseihin

   ### Raportin ohjeistus    
  -Toistettava, täsmällinen, helppolukuinen, viittaa lähteisiin, vakiotekstejä ja pahoja mokia; sisällysluettelolla se tulikin tiivistettyä.
  
  -Raportin tulee olla tarpeeksi tarkka, että siinä kuvaillut asiat voi toistaa. Näin ongelmanratkaisu on helpompaa ja säästyy aikaa.
  
  -Pidä teksti helppolukuisena ja selkeänä. Säästät tällä paitsi omaa aikaasi kun myöhemmin luet näitä raapustuksia niin mahdollisesti myös jonkun muun aikaa, joka näitä joutuu lukemaan.
  
  -Kunnia sinne minne kunnia kuuluu ja muiden tekemät virheet ovat myös muiden tekemiä vaikka sinä niitä toistaisit eli muista lähdeviittaukset!
  
  -Pitäisi kuulua ihan kaikkien perusarvoihin, mutta älä valehtele tuottamassasi sisällössä.

  Tämä tiivistelmä perustuu Tero Karvisen ohjeisiin raportin kirjoittamisesta (https://terokarvinen.com/2006/raportin-kirjoittaminen-4/).    
    
   ### Ilmainen softa a la Free Software Foundation
  - Paremmin käännettynä ehkäpä vapaa kuin ilmainen softa. Free softwarella voi tehdä rahaa.
  - Perustuu ideologiaan, että käyttäjillä on oikeus suorittaa, kopioida, jakaa ja muokata softaa ilman erillistä lupaa ja ilmaiseksi.
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

  Kun siirryin ohjeissa kohtaan "Insert Debian ISO Image as a Virtual CDROM" oli koneessa jo ilmeisesti valmiina tehty kyseinen vaihe.
  
  ![Vcd1](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/Virtuaalisen%20cdn%20m%C3%A4%C3%A4ritys%201.JPG)
  ![Vcd2](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/Virtuaalisen%20cdn%20m%C3%A4%C3%A4ritys%202.JPG)

  Kun jatkoin ohjeita eteenpäin ja yritin käynnistää virtuaalikoneeni DebianAliRomarCom, Bootloaderi ei käynnistynyt odotusten mukaisesti vaan tuotti seuraavanlaisen virheen:

  ![AMD-V disabled in BIOS](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/8d7a1f98-7159-4355-bbf2-e49526c5239e)

  Tästä virheestä päättelin, että oli poissa päältä BIOSssa/UEFIssa. Tutkin asiaa erinäisiltä sivuilta internetistä (https://support.bluestacks.com/hc/en-us/articles/360058102252-How-to-enable-Virtualization-VT-on-Windows-10-for-BlueStacks-5, Q2. How can I check if Virtualization is enabled/disabled on my desktop/laptop?) ja päädyin tarkistamaan tehtävienhallinnasta onko minulla virtualisointi ylipäätänsä mahdollistettu. Ei ollut.
    
  ![Tehtävienhallinta Virtualisointi.JPG](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/Teht%C3%A4vienhallinta%20Virtualisointi.JPG)
  ![Tarkennus Virtualisoinnista](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/Virtualisointi%20Task%20Manager.JPG)

  Selvitin internetin ihmemaailmasta (https://www.msi.com/faq/nb-1627) mikä asetus piti laittaa päälle BIOSISTA/UEFISTA (AMD SVM) ja toteutin korjauksen.
  Palasin ohjeissa kohtaan "Boot to Desktop - Choose to Live" ja käynnistin virtuaalikoneeni kaksoisklikkauksella. Kone lähti käyntiin, mutta ohjeiden kaltaista bootloaderia ei minulle ilmestynyt joten klikkasin VirtualBox Managerissa Show-nappulaa ja seuraava ruutu avautui minulle.

  ![Debian bootsrappiko](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/DEBIAN%2012%20Bootstrappiko.JPG)

  Valitsin vaihtoehdon Live System (amd64) ja lopulta Linux aukeni minulle.

 [Linux auki](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/Linux%20auki.JPG)

  Jatkoin ohjeiden seuraamista ja kokeilin nettiselaimen avulla hiiren, näppäimistön, netin ja näytön toimivuudet. Tämän jälkeen siirryin asentamaan debiania, ohjeita noudattaen tietysti ~~ja asennus sujui ongelmitta~~. Heti alkuun tuli viestiä untrusted application launcherista, mutta klikkasin vain Launch anyway ja homma jatkui.

![untrusted](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/Untrusted%20application%20launcher.JPG)
  
  Taustalla pyöri mahdollisesti jotain error viestejä (löytyy seuraavasta kuvankaappauksesta), mutta lopulta kone boottasi itsensä login ruutuun ja pääsin kirjautumaan sisään. Ohjeiden avulla sain päivitettyä kaiken ja asennettua ja käynnistettyä palomuurin. Ohjeita seuraamalla asensin myös Guest Additionit, jotka mahdollistivat suuremmat resoluutiot sekä leikepöydän käytön hostin ja virtuaalikoneen välillä. Yhden uudelleenkäynnistyksen yhteydessä sain napattua kuvan aiemminkin pyörineestä error viestistä:

![Ihme errori](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/Ohi%20menev%C3%A4%20Error.JPG)
  
  Olipa seikkailu näin Linux aloittelijalle! Seuraavassa raportissa voisikin perehtyä tämän tiedoston muotoiluun hieman enemmän, jos aika riittää.
