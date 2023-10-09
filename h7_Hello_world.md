# Kotitehtäväraportti h7

_Tähän se kaikki sitten kulminoituu. Tässä kotitehtäväraportissa..._  

## x) Läksyjen linkit
[h1_OmaLinux](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/h1_OmaLinux.md "Alin eka repo ja rapsa")  
[h2 Komentaja Pingviini](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/h2%20Komentaja%20Pingviini.md "Nimeämiskäytännöt voisi yhtenäistää...")  
[h3_HelloWebServer](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/h3_HelloWebServer.md "Tässähän on nimeäminen jo kohdallaan")  
[h4 Maailma kuulee](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/h4%20Maailma%20kuulee.md "Vaan eipä ole enää...")  
[h5_Nimittain](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/h5_Nimittain.md "Nyt ne nimeämiset nimittäin kuntoon! Eiku nyt on taas hyvä.")  
[h6_DJ_Ango](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/h6_DJ_Ango.md "Ja taas joku vähän erilainen..")  
[h7_Hello_world](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/blob/main/h7_Hello_world.md "Pikku metajekku tähän")  



 
## y) [Artikkelin](https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/ "Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04 -- Karvinen 2018") tiivistäminen

  Vielä viimeinen tiivistettävä artikkeli tälle kurssille ja se käsitteli eri ohjelmointikielien suorittamista Linuxissa. Kerrankin sain tiivistelmästäni tiiviin!  
  
  - Kun testaat koodia tee ensin "Hello World" -ohjelma eli yksinkertainen ohjelma, joka tuottaa syötteen "Hello World". Näin testaat, että koodi ylipäätään toimii käyttöympäristössäsi.  
  - Valmiit "Hello World" koodipätkät suosituille kielille: Python 3, Bash, C, C++, Go, Lua, Ruby and Java.




## a) Hei maailma

Tuttuun tapaan aloitin päivittämällä paketinhallinnan listat `sudo apt-get update` ja lataamalla päivityksiä `sudo apt-get upgrade` ja... hei nyt tuli ladattua jotain odottamatonta. Päivitys grub-pc bootloaderiin vaati huomiotani:

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/1fba956a-b283-4e12-9363-4a883d4e0033)

Ehkä tämän takia meitä ei erikseen käsketty lataamaan näitä päivityksiä `sudo apt-get upgrade`lla, pelkästään päivittämään paketinhallinnan listat `sudo apt-get update`lla.  
En jaksanut sen enempää tutkia asiaa ([aina pitää vähän vilkaista](https://github.com/hashicorp/vagrant/issues/289 "Keskustelua aiheesta")) vaan valitisin molemmat vaihtoehdot ja annoin asentaa. Tämän jälkeen käynnistin virtuaalikoneen uudelleen.  
Kone käynnistyi ilman sen kummempia ongelmia tai ilmoituksia.  
  
Seuraavaksi ajattelin asentaa vinkeissä mainitut asiat `sudo apt-get install openjdk-17-jdk ipython3`.  
Nopeat sormet, joten vasta kun asennukset pyörivät kävin katsomassa olisiko openjdk:sta ollut uudempiakin versioita ([olisi](https://openjdk.org/projects/jdk-updates/ "Open JDK.org - jdk-updates")).  
Ehkä tähän tarkoitukseen soveltuu myös asentamani versio.  

Loin kotihakemistooni uuden kansion, jossa aloin työskentelemään `mkdir koodit`, /home/alir/koodit .  
Kokeilin ensimmäiseksi mitä tapahtuu jos vain kopioin aiemmin tiivistämäni artikkelin sivuilta komennot.  
`cat helloalir.py` ei luonnollisestikaan tehnyt mitään, kuten `man cat` minulle ystävällisesti muistutti.  
En muistanut millä komennoilla ja putkilla sai tehtyä näitä tiedostoja komentoriviltä, joten vilkaisin netistä hauskannäköisen [bash komennon](https://www.cyberciti.biz/faq/create-a-file-in-linux-using-the-bash-shell-terminal/) ja kokeilin sitä `echo "Hello world > helloalir.py`.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/ac7211b7-2742-4739-9822-c0d42a95d768)

Tiedosto helloalir.py oli luotu ja tarkistin microlla, `micro helloalir.py`, että siellä tosiaan luki teksti "Hello world". Kyllä luki.  
Muokkasin samalla tiedostoon tekstin `print("Heissulivei muailma")` ja tarkistin, että tämä oli tallentunut käyttämällä `cat helloalir.py`.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/13d3f708-e4a0-4347-b27b-0c378523d406)

Sitten olikin aika testata toimiiko python koodin suorittaminen eli `python3 helloalir.py`. Ja sieltä tulostui haluamani teksti "Heissulivei muailma".

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/7c21b94b-758d-4dfb-82f8-d0e501e75a50)

Seuraavaksi lähdin yrittämään C kieltä. Loin helloalir.c tiedoston microlla `micro helloalir.c`.  
Kopioin artikkelista koodin.  

      #include <stdio.h>
      int main()
      {
       printf("Hello Tero\n");
      }

  ![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/8ed4d2b3-eb48-4a78-9983-eb05c9d549c3)

Varmistin vielä ennen suorittamista mikä on komento `gcc`. En löytänyt sille manuaalimerkintää, joten sitä ei ehkä ollut asennettu. Katsoin asiaa vielä [netistä](https://gcc.gnu.org/ "gcc.gnu.org") ja [toisaalta netistä](https://www.geeksforgeeks.org/gcc-command-in-linux-with-examples/).  

Sitten kokeilemaan komentoja.  
`gcc helloalir.c -o helloalirc` käski gnu compiler collectionia kääntämään tiedoston helloalir.c ja nimeämään tämän uuden käännetyn tiedoston nimellä "helloalirc".  
`./helloalirc` yksinkertaisesti suoritti nykyisestä hakemistosta tuon tiedoston.  
Näytti onnistuneen, mutta unohdin vaihtaa esimerkkitekstin, joten terve vaan Terolle tällä kertaa.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/fda61480-e697-4394-94f2-b6e2c49dd8f7)

Seuraavaksi esiintyi java. Eli `mirco HelloAlir.java` uuden tiedoston luonti microlla.  
Tiedostoon kopioitu (ja muokattu) teksti artikkelista.  

      public class HelloAlir
      {
       public static void main(String[] args)
       {
       System.out.println("Tere t.java");
       }
      }

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/bd1fcde1-ae80-4d04-a878-65fec8038b81)

`javac HelloAlir.java` tekstitiedoston kääntäminen javalle (oletus perustuen aiempaan C kielen kääntämiseen).  
Kurkkasin tässä välissä mitä oli luotu: HelloAlir.class eli luokka, jota java voi suorittaa.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/1a26e1cd-e413-49fb-baab-dffd3806eb8a)

`java HelloAlir` ja tiedoston suorittaminen.  
Tulostui tiedostoon printattavaksi laittamani teksti eli toimi.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/2b4fc255-e690-44e8-ad6b-f11c402d4654)




## b) 3+1 vai... Lisää kieliä käännettäväksi

Sitten piti kääntää jotain muutakin kieltä kuin Python, java tai C. En ollut varma lasketaanko bash käännettäviin ohjelmointikielii ja tästä taisi olla jotain keskustelua tunnillakin, sekä [netissä](https://stackoverflow.com/questions/28693737/is-bash-a-programming-language "StackOverflow. Is bash a programming language?"), mutta päätin käyttää sitä tässä.  

Jostain mieleeni putkahti komento `tee`, joten tarkistettuani sen oikeellisuuden `man tee` päätin palata kurssin alkuun ja pistää komentoja putkeen.  
`echo "Hei putkimestari"|tee hellopiperali.sh`. Tämä toimi niinkuin halusinkin eli loin uuden tiedoston hellopiperali.sh, johon kirjoitettiin "Hei putkimestari".  
Tarkistin nämä vielä `ls` --> hellopiperali.sh ja micro hellopiperali.sh --> "Hei putkimestari".  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/54f70e75-c361-4754-9df5-559c92315738)

Sitten tulostamaan `bash hellopiperali.sh` jaaa...  
"hellopiperali.sh: line 1: Hei: command not found"  
Olisiko tässä nyt unohtunut yhdet lainausmerkit. Kokeillaanpa uudelleen..
`echo ""Hei putkimestari""|tee hellopiperali.sh`. `ls` oikean niminen tiedosto on ja `micro hellopiperali.sh`.. Tiedostossa luki vain "Hei putkimestari", ilman lainausmerkkejä. En tiennyt mikä oli vialla, mutta lisäsin lainausmerkit manuaalisesti ja kokeilin uudestaan bash komentoa `bash hellopiperali.sh`.. Eikä vieläkään. "hellopiperali.sh: line 1: Hei putkimestari: command not found"  
No niin nyt taisin ymmärtää. "Kolmas kerta toden sanoo", totesin ja lähdin suorittamaan:
`echo "echo Hei putkimestari"|tee hellopiperali.sh`, `bash hellopiperali.sh` jaaa... sain tulosteen "Hei putkimestari" eli homma toimii.   

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/30accdbd-002b-4dc1-88f5-96f64198cf50)

Tässähän meni pidempään kuin ajattelin, mutta päätin ottaa harjoituksen vuoksi vielä yhden kun kerrankin oli aikaa (eli välttelin tylsiä englannin tehtäviä).  
Karvisen artikkelissa Ruby näytti melko helpolta tähän tehtävään, melkein sama kuin Python, joten lueskelin ensin hiukan [Rubysta](https://www.ruby-lang.org/en/about/ "ruby-lang.org – Ruby ohjelmointikielestä") ja sitten aloin suorittamaan:  
`echo "print ("Hei taas putkimestari\n")|tee hellopiperali.rb` joka tuotti pettymyksen, koska se tulosti "print (Hei taas putkimestarin)".  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/6bfb0eee-a020-47e0-a726-1808a7cdbf0a)

Ilmeisesti tämä tapa ei taipunut ihan kaikkeen, joten vaihdoin suoraan editointiin microlla `micro hellopiperali.rb` -->  

      print ("Hello Linebreak\n")
      print ("Hello no Linebreak")

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/b3caf3a2-6ac3-4ef3-9a3d-0ab357bbdc9c)

Ja eikun kokeilemaan `ruby hellopiperali.rb` ja kuten oli hiukan aavistellut niin paketteja puuttui: "bash: ruby: command not found".
Nopea vilkaisu aiemmin linkkaamaltani rubyn kotisivulta ja löysin paketinhallintakomennon `sudo apt-get install ruby-full`. Suoritin tämän ja kokeilin uudestaan `ruby hellopiperali.rb` paremmalla menestyksellä. Komento tulosti kirjoittamani rivit ja pääsinkin ihailemaan rivinvaihdon tärkeyttä tässä kielessä.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/f11a8f0b-fa38-4944-9224-6d5fc90da2d6)




## c) python laskimena! Joo voisi tällä tehdä paljon muutakin..

Olin jo aiemmin tässä kotitehtävässä asentanut ipython3 paketin (`sudo apt-get install openjdk-17-jdk ipython3`), joten pääsin heti käyttämään sitä: `python3` (heittämällä oikein).  
Seuraavaksi suoritin niinkin vaikeita laskutoimituksia kuin 2+2 --> 4 ja 2*3 --> 6.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/6f01018d-4640-4091-8bc4-9813d0f2d853)

Pois pääsi komennolla `exit()`, jota ohjelma itse ehdotti kun olin yrittänyt ensin `exit`.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/96d1370d-a3ff-46b6-b77f-b046eff302d4)




## d) Shell script

Niiiin, se keskustelu siitä onko bash ohjelmointikieli. No, tein jo tämän kohdan mielestäni edellisessä tehtävässä. Seuraavaa tehtävää ajatellen yritin kuitenkin keksiä jonkun hyödyllisemmän/monipuolisemman toiminnon. Muistelin, että tunnilla luotiin jotain joka kertoi mm. päivämäärän tmv, joten lähdin tästä pohtimaan jotain tervehdystä+tietoa kun käynnistän koneen.  
Loin uuden tiedoston `micro hailcom.sh` ja muokkasin sinne testitekstiä:

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/4386993c-96ff-4147-87a2-16210fa3c3c1)

Lähdin kokeilemaan miltä tämä näyttää ja sain haluamani näköisen tulosteen `bash hailcom.sh`:

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/6a0e829f-e89d-4b10-863f-4b6de1ac80ef)

Tässä välissä tutkin rehellisesti sanottuna vaikka ja mitä sekä kokeilin eri komentojen toiminnallisuuksia ym. eli opettelin, enkä jaksa sitä prosessia tähän kuvata.  
hailcom.sh tiedostoni sisältö päätyi näyttämään seuraavalta:

    os=$(uname)
    now=$(date)
    kayttaja=$(whoami)
    
    echo 
    echo Avē Imperātor $kayttaja, $os systema tē salūtant!
    echo  
    echo It is now: $now
    echo 
    echo I await your command.

Kun suoritin tiedoston bashilla `bash hailcom.sh` sain seuraavan tuloksen:  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/ac61d72c-0d10-4aea-a5e6-a5284ac1d7f5)

Tämä oli haluamani lopputulos, joten siirryin seuraavaan tehtävään, jossa tultaisiin toteamaan tämän skriptin toimivuus muillakin käyttäjillä.  




## e) Uusi komento linuxiin. Kaikkien käytettävissä, kiitos

Heti tehtävän alkuun aloin lueskelemaan Mendel Cooperin [Advanced Bash-Scripting Guidea](https://tldp.org/LDP/abs/html/ "Cooper 2014, Advanced Bash-Scripting Guide") ja totesin, että shell skriptini kaipasi vielä hiukan muutoksia, joten siirryin tekemään niitä ja lopuksi hailcom.sh näytti tältä:    

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/4d88ac55-897e-4570-8833-494c6f58474a)

Kokeilin vielä toimivuutta tässä välissä `bash hailcom.sh` ja hyvin näytti toimivan eli sain haluamani tulosteen:

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/5e51ea51-b9c0-44c9-ad78-ad7d1397c9f1)

Yritin seuraavaksi siirtää tiedoston hailcom.sh sijaintiin /bin/bash `mv hailcom.sh /bin/bash`.  
Tästä sain ilmoituksen `mv: replace '/bin/bash', overriding mode 0755 (rwxr-xr-x)?`  
Vastasin tähän "y", jolloin sain toisen ilmoituksen: `mv: cannot move 'hailcom.sh' to '/bin/bash': Permission denied`  
Ymmärtääkseni yritin siirtää tiedostoa paikkaan, johon minulla ei ollut oikeuksia siirtää sitä, jonka lisäksi jos tiedoston siirtäisi haluamaani sijaintiin, tulisi sen oikeudet muuttaa ehdotetuiksi.  
Päätin tässä välissä vielä testata olinko ymmärtänyt `mv` komennon syntaksin oikein. Luin `man mv` ja kokeilin siirtää hailcom.sh yhden pykälän alemmas hakemistopuussa:
`mv hailcom.sh /home/alir/`  
`ls` --> tiedosto oli kadonnut.  
`cd ..` --> `ls` --> tiedosto oli siirtynyt.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/372f27ba-02c3-476e-9972-8fcc5b672d7b)

Tässä välissä lueskelin hiukan lisää Cooperin bash kirjaa ja tajusin ymmärtäneeni asiat hiukan väärin.  `#!/bin/bash` osan hakemistopolku ohjaa ohjelman luo, joka suorittaa kyseisen tiedoston. Se ei ole itse tiedoston polku.  
No, seuraavaksi muutin hailcom.sh oikeudet, jotta kaikki voisivat käyttää sitä `chmod u+rwx,go=rx hailcom.sh`. `ls -l` tarkistin oliko mennyt oikein ja oikeudet olivat nyt mielestäni kunnossa. Nykyisellä käyttäjällä alir oli oikeudet lukea, kirjoittaa ja suorittaa, alir ryhmällä sekä muilla oli oikeudet lukea ja suorittaa.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/8c8a2253-0fc8-49e5-8e17-e394a293e74b)

Sitten piti kyseinen tiedosto siirtää Cooperin kirjan mukaan hakemistoon /usr/local/bin , ja tämä tuli tehdä root oikeuksin. Päätin kokeilla sudoilla: `sudo mv hailcom.sh /usr/local/bin/` .  
Tarkistin `ls` ja kyseinen tiedosto oli kadonnut sijainnista /home/alir .  
`cd /usr/local/bin/`, `ls` ja se oli ilmestynyt haluamaani hakemistoon.  
Kuvan $ ^C on typo joka tuli, koska vaihdan jatkuvasti ikkunasta toiseen.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/cdc95149-ba34-42be-964e-d3beb8fe7743)

Yritin suorittaa juuri luomaani komentoa `hailcom` ja.... `bash: hailcom: command not found`.  
Jossain oli siis virhe.  
Yritin `./ hailcom` --> `bash: ./: Is a directory`. #_Myöhemmin huomasin, että tämä komento on väärin kirjoitettu --> `./hailcom`_  
Kokeilin suorittaa tiedoston `hailcom.sh` ja se toimi kuten pitikin.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/eea20255-06a4-4d1d-a4b2-808cda41be65)

---------------------------------------------------
### **Tästä eteenpäin homma meni vähän väsyneeksi turhaksi oikeuksien selvittelyksi, koska pitkän ruudun täyteisen päivän jälkeen silmät alkavat nähdä mitä sattuu. Tämän osion voi skipata jos ei tahdo erityisesti nähdä "turhaa" ongelmanratkaisua.**
---------------------------------------------------

Tarkistin vielä kyseisen tiedoston oikeudet `ls -l` ja.. -rwxr-xr-x. Oikeudet olivat muuttuneet. Vai olivatko.. Tarkistin aiemmista kuvankaappauksistani ja samathan ne olivat siellä. Mitenkäs tälläinen oli mennyt ohi vaikka piti olla katsottu...  

Yritin sitten muokata oikeudet kuntoon:  
`chmod o+r hailcom.sh`, `ls -l` ei muutosta.  
`sudo chmod o+r hailcom.sh`, `ls -l` ei muutosta.  
`chmod 755 hailcom.sh`, `ls -l` ei muutosta.  
Päätin siirtää tiedoston takaisin kotihakemistoni koodit hakemistoon. Ehkäpä jokin ei toiminut, koska olin hassussa hakemistossa, vaikka aiemminkaan chmod käskyt eivät olleet menneet läpi kotihakemistossani... `sudo mv hailcom.sh /home/alir/koodit/` --> `cd /home/alir/koodit/` --> `ls` siellä oli.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/1af5901b-99ea-49bc-933c-b8af9b5dfd7f)


Jonkin aikaa pelleiltyäni ja tutkittuani löydökseni olivat seuraavat:
Kun poistin tiedostolta hailcom.sh suoritusoikeudet kaikilta `chmod -x hailcom.sh` niin esiin tulivat jostain syystä kirjoitusoikeudet ryhmälle muut.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/45ba4d85-86bb-4026-afb3-450c1d2cd86b)

Ja kun lisäsin kaikille...

---------------------------------------------------  
### **Ja nyt huomasin katsoneeni aivan väärin eli palataanpas asiaan.**
---------------------------------------------------  

Eli oikeudet olivat juuri niinkuin pitikin.  
Raportin tarkkuus ja taso tulisi todennäköisesti tästä eteenpäin hiukan laskemaan, koska en jaksanut yksityiskohtaisesti kirjoittaa kaikkea ylös enää tässä vaiheessa. Olisinko voinut lopettaa ja jatkaa toiste virkeämpänä. Ehkä. Oliko minulla aikaa moiseen: ei. Elikkäs.. Yritin tulkita Cooperin kirjan ohjeita suorittamalla seuraavia komentoja: 
Yritin komentoa `bash hailcom` --> ei toiminut.  
`./hailcom` --> ei toiminut.  
`./hailcom.sh` --> toimi.  
`hailcom.sh` --> ei toiminut.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/822c845a-9733-4f7a-9c02-b9bbcb0cce57)

Toivoin, että tämä tarkoitti kaiken olevan kunnossa ja ajattelin yrittää uudestaan siirtoa hakemistoon /usr/local/bin .  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/cf2d8624-cfc9-4c7d-b3eb-41e541dd2597)

Sitten kokeilemaan toimivuutta:  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/db9943d4-973b-495b-a8f5-c981a9e0f821)

Näytti toimivan talossa ja puutarhassa.  
Ei tosin haluamaani tapaan `hailcom`. Kokeilin muuttaa tiedoston nimeä.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/ae320486-68d9-4a35-8e80-a79d76b2f525)

Toimi. Jes. Seuraava. Että tämän tasoinen raportti.  
Tässä välissä laitoin kirjanmerkkeihin Cooperin kirjan.  


_Tässä välissä oli välipäivä, aloin aiemmin suorittamaan f) tehtävää, mutta no, siellä se lukee._  
Siispä luomaan uusi käyttäjä `sudo adduser terppa`, joka luo käyttäjän terppa, sekä uuden ryhmän terppa ja lisää käyttäjän sinne ja kotihakemiston uudelle käyttäjälle. Vielä piti laittaa hyvä salasana ja joitain tietoja. Tarkistin vielä `sudo cat /etc/passwd | grep terppa`, että uusi käyttäjä oli luotu.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/e989fabb-cdfb-4b50-857d-ed703e06966a)

Ja tässä välissä pieni perhekriisi, joten hyvä salasana unohtui muistista ja jouduin luomaan uuden käyttäjän `sudo adduser terppa2`.  
Menin testaamaan sitä `su terppa2`.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/68301099-21f8-420c-a29a-98805be77936)

Ja luomani komennon toimivuutta uudella käyttäjällä `hailcom`. Komento tulosti haluamani syötteen.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/99fb625a-5011-4718-bc3a-c60fb5433a24)






## f) Ratkaise vanha labratehtävä  (Klassisesti aika loppuu kesken, joten tässä vaiheessa olisi paljon lähdeviitteitä ym. mitä voisi parantaa. Aika monta asiaa tuli tutkittua netistä ja komentojen manuaalisivuilta)

Ei hele nytkö piti tehdä vielä kokonainen tentti tähän päälle. No, lähdin suorittamaan.  
Tai oikeastaan löydettyäni ja luettuani läpi pari vanhaa labratehtävää:  
[Arvioitava laboratorioharjoitus – Linux palvelimet ict4tn021-4 tiistai – alkusyksy 2017 – 5 op](https://terokarvinen.com/2017/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-4-tiistai-alkusyksy-2017-5-op/)  
[Arvioitava laboratorioharjoitus – Linux palvelimet ict4tn021-5 torstai – alkusyksy 2017 – 5 op](https://terokarvinen.com/2017/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-5-torstai-alkusyksy-2017-5-op/)  
[Arvioitava laboratorioharjoitus – Linux palvelimet ict4tn021-2 (uusi OPS) alkukeväällä 2017 p1](https://terokarvinen.com/2017/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-2-uusi-ops-alkukevaalla-2017-p1/)  
[Arvioitava laboratorioharjoitus – Linux palvelimet ict4tn021-3 (uusi OPS) alkukeväällä 2017 p1](https://terokarvinen.com/2017/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-3-uusi-ops-alkukevaalla-2017-p1/)

Masennuin tehtävien laajuudesta ja haastavuudesta ja päätin lopettaa linux työskentelyn tältä päivältä. Ohjelmointi 1 tentti, joka on myös tiistaina tulee olemaan niin lasten leikkiä tähän verrattuna...  

Jatkoin työskentelyä pidettyäni välipäivän ja tajusin, että en ollut kokeillut edellisen tehtävän komennon toimivuutta toisella käyttäjällä, joten tein sen kohdan tähän väliin ja sitten jatkoin tätä vaihetta.  

Koska vanhan labratehtävän ratkaiseminen JA raportointi vaikutti melko työläältä, päätin alkuun tehdä uuden virtuaalikoneen valmiiksi eli siirryin tehtävään g).  
Tehtyäni tehtävän g), jatkoin tämän suorittamista.  

Valitsin vanhoista labroista seuraavan: [Arvioitava laboratorioharjoitus – Linux palvelimet ict4tn021-3 (uusi OPS) alkukeväällä 2017 p1](https://terokarvinen.com/2017/arvioitava-laboratorioharjoitus-linux-palvelimet-ict4tn021-3-uusi-ops-alkukevaalla-2017-p1/)  
Koska tunneilla käyttämälläni virtuaalikoneella oli jo vaikka mitä kivaa sotkua, päätin tehdä uuden puhtaan asennuksen kohdan g) mukaisesti.  
Tein siis uuden virtuaalikoneen kuten kohdassa g) ja jatkoin siitä.  

~~Koska minun tuli luoda useita käyttäjiä päätin kokeilla password manager ohjelmaa nimeltään pass, josta luin [netistä](https://www.howtogeek.com/devops/how-to-use-pass-a-command-line-password-manager-for-linux-systems/ "pass, pwmanageri").
Latasin pass:n paketinhallinnasta `sudo apt-get install pass`.  
Loin gpg:llä sa..~~

Koska minun tuli luoda useita käyttäjiä päätin kokeilla kpcli nimistä password manager ohjelmaa, josta luin [netistä](https://kpcli.sourceforge.io/).  
Käytettyäni melkoisen määrän aikaa tämän toiminnallisuuden opetteluun, aloin luomaan käyttäjiä.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/3cb4666a-8f43-423c-8126-fdcbd94b6fb4)

Loin käyttäjän Jorma Mähkylä, käyttäjänimi jormamah `sudo adduser jormamah` ja asetin tälle hyvän generoidun salasanan kpclistä.  
Valitettavasti copy pasteilu meni ensimmäisellä kerralla hiukan pieleen, joten jouduin poistamaan Jorman `sudo deluser jormamah --remove-all-files` ja loin hänet uudelleen.  
Tällä kertaa luominen onnistui ja pääsin kirjautumaan Jormalla sisään.  
`su jormamah` --> salasana. Olin ihan Jormana paikalla.  
Menin Jorman kotihakemistoon `cd` ja katsoin missä olen ja mitä siellä on `pwd`, `ls`.  
Olin tosiaan Jorman kotihakemistossa /home/jormamah , eikä siellä ollut mitään, koska Jorma ei ollut tehnyt sinne mitään.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/84946a72-828c-4ad1-8c82-a9c84b8fe4c6)

Koska olin raudanluja aloittelija, loin muutkin käyttäjät (Pekka Hurme, Ronaldo Smith, Håkan Petersson, Einari Mikkonen, Einari Vähäkäähkä, Eija Vähäkäähkä, Maija Virtanen) vastaavasti. Manuaalisesti.  
Maijalle asetin käyttäjätunnuksen "maija".  
Seuraavaksi piti Maijalle antaa sudo oikeudet `sudo visudo`.  
Törmäsin kohteliaaseen ehdotukseen kommenteissa olla muokkaamatta tätä tiedostoa, joten ehkä olisi toinenkin tapa.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/9905fbf7-40c7-4d4a-8fbb-ca9f5bf221ea)

Ajattelin lisätä siis Maijan sudo ryhmään `sudo usermod -aG sudo maija`.  
Menin testaamaan toimiko tämä. Aluksi vaihdoin Maijan käyttäjälle, mutta sitten löysin komennon `id maija`, joka näytti mm. mihin ryhmiin käyttäjä maija kuuluu. Hän kuului nyt ryhmään 27(sudo).  
Päätin kokeilla jotain sudokomentoa maijana `sudo apt-get update`, mutta en jostain syystä nyt saanut salasanaa toimimaan.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/d3511c06-352c-4c26-a4ee-1b5933e62f2f)

Jotain omaa säätöä siinä vain oli, koska yrittäessäni uudelleen homma toimi.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/1f9da66f-3e0f-4dcc-a7e5-67ab296b0538)

Kokeilin myös `sudo ufw status` --> Status: active.  
Sekä `ufw status` --> bash: ufw: command not found.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/c7483deb-7e29-48d8-a6e1-634485f8fafe)

Jatkoin työskentelyä omalla käyttäjälläni maija: `exit`.  

Sitten piti laittaa kotisivuja kaikille eli `sudo apt-get -y install apache2`.  
`firefox "http://localhost` avasi halutusti apache2 oletussivun.  
`sudo a2enmod userdir` ja `sudo systemctl restart apache2`. Käyttäjien kotisivut toimintaan.  
Kokeilin ensin omallani `cd`, `mkdir public_html`.  
`firefox "http://localhost/~alir/"` avasi halutun oletuskotisivun.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/c603f1ba-81be-4737-ab4a-3624cc10b8da)

Valitettavasti kun yritin luoda sudolla toiselle käyttäjälle vastaavaa kansiota `sudo mkdir -m 755 /home/eijavah/public_html` en saanut sitä omalla käyttäjälläni auki `firefox "http://localhost/~eijavah/"`.  
Vastaan tuli forbidden error. Oletettavasti siis jotain oli luotu, mutta en vain päässyt katsomaan.  
Yritin käydä eijavah käyttäjällä tutkimassa, mutta en saanut hänellä käynnistettyä firefoxia.

No kirjauduin virtuaalikoneeltani pois ja sisään eijavah käyttäjänä ja pääsin avaamaan firefoxin, mutta näytti vieläkin forbiddenia.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/15d824c6-963b-45ec-b297-7c6a2879be98)

Kävin tutkimassa apachen lokia `sudo tail -f /var/log/apache2/error.log` ja tosiaan polun varrelta jostain puuttui oikeuksia niin alir kuin eijavah käyttäjältäkin. Outoa.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/1b8e3097-7787-4d59-84b6-342ae966074a)

Hiukan tutkittuani vika oli varmaankin käyttäjien kotihakemistoissa; niissä ei ollut muita kuin käyttäjien omat oikeudet.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/d8def44a-c054-476a-b301-be6a0eec1717)

`sudo chmod o+r /home/eijavah`  
`sudo ls -l /home`  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/5988411e-c7a3-46ea-a117-4b754207ecf4)

`firefox "http://localhost/~eijavah/"`  
Ei toiminut vieläkään.  
`sudo chmod go+rx /home/eijavah`  
`firefox "http://localhost/~eijavah/"`  
Nyt toimi.
Sama toimenpide muille käyttäjille siis. Tämän ratkaisun tietoturvallisuudesta en ole ollenkaan tietoinen. :)  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/d6445587-6902-409d-ba39-2cd6a14da0f7)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/c60851c9-2c6d-4ee3-81d1-2d5ff97ca01d)

Sitten jokaiselle käyttäjälle public_html kansioon index.html tiedosto johon html5 näkymään heidän käyttäjätunnuksensa.  
Tähän olisi ollut nopeampia tapoja jos osaisi, mutta tein sen käsin. Ehkä opettelen tekemään tämän nopeammin "omalla ajallani".  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/fc133e04-e97e-4122-a8e5-f2a652bcc3f4)

Tässä vaiheessa oli vajaa 15min aikaa ennen palautusta. Ajattelin katsoa kuinka pitkälle pääsen name based virtual hostingissa.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/ac1287e4-4cd0-4330-ac4f-4e41db806b3b)

---------------------------------------------- AIKA LOPPUI -----------------------------------------------------





## g) Virtuaalikone labraa varten

Tämä tehtävä oli käytännössä ensimmäisen kotitehtävän toisinto, joten käytin samoja työkaluja (Oracle VM VirtualBox Manager) ym. kuin siinäkin.  
debian-live-12.1.0-amd64-xfce.iso oli valmiiksi ladattuna, joten käytin sitä uutta konetta luodessani.  
Nimesin uuden koneen VirtualBoxissa "DebianTenttikone". Ja laitoin tässä vaiheessa loput tiedot/vaiheet pääosin kuvina säästääkseni aikaa.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/95df42c4-8fb8-4d86-be13-9a628d30428d)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/650c8574-3743-4c9b-aa09-1fccb3db2ba6)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/177f4b67-94c3-433f-8cde-37f8df00034a)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/37bfece6-55f3-42c1-9649-095e1c8a22f2)

Valitsin bootissa live version ja kokeilin netin, hiiren ym. toimivuudet ja käynnistin työpöydältä debian installerin.  

Asennuskieli: American English  
Location: Helsinki  
Keyboard: Generic 105-key PC, Finnish Default. Kokeilin ääkkösten toiminnan.  
Erase disk.  
Boot loader: Master Boot Record of..  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/b6e76a17-0fbd-4e4a-bd14-13d23498b541)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/c32852be-f2eb-4e7f-80e8-3a57d8d904ba)

Asennus lähti pyörimään ja kesti jokusen minuutin.  

Pääsin kirjautumaan koneelle.  
Meinasin ensin asentaa guest additionit parempaa resoluutiota varten, mutta en ollut varma onko se vielä sallittua, joten koitan muistaa sen tentin alussa.  
Suoritin terminaalissa `sudo apt-get update` ja `sudo apt-get -y install ufw` sekä tämän jälkeen `sudo ufw enable`, jonka jälkeen suljin terminaalin.  
Kävin vielä testaamassa firefoxin toimivuuden osoitteessa terokarvinen.com ja toimi. Sitten suljin virtuaalikoneen ja palasin kotitehtävän f) osioon.  





# **Lähteet**

Karvinen T. 2018. Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java – Programming Languages on Ubuntu 18.04.  
Luettavissa: https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/  
Luettu 07.10.2023  

Gitbuh. Vagrant. Issues.  What is the grub-pc? #289.  
Luettavissa: https://github.com/hashicorp/vagrant/issues/289  
Luettu 07.10.2023  

Open JDK. JDK Update Releases.  
Luettavissa: https://openjdk.org/projects/jdk-updates/  
Luettu 07.10.2023  

Cyberciti. How to create a file in Linux using the bash terminal.  
Luettavissa: https://www.cyberciti.biz/faq/create-a-file-in-linux-using-the-bash-shell-terminal/  
Luettu 07.10.2023  

GCC, the GNU Compiler Collection  
Luettavissa: https://gcc.gnu.org/  
Luettu 07.10.2023  

geeksforgeeks. gcc command in Linux with examples.  
Luettavissa: https://www.geeksforgeeks.org/gcc-command-in-linux-with-examples/  
Luettu 07.10.2023  

StackOverflow. Is bash a programming language?.
Luettavissa: https://stackoverflow.com/questions/28693737/is-bash-a-programming-language
Luettu 07.10.2023  

ruby-lang.org. About ruby.
Luettavissa: https://www.ruby-lang.org/en/about/
Luettu 07.10.2023  

Cooper M. 2014. Advanced Bash-Scripting Guide. An in-depth exploration of the art of shell scripting.  
Luettavissa: https://tldp.org/LDP/abs/html/  
Luettu 07.10.2023  

HowToGeek. How to Use Pass, a Command-Line Password Manager for Linux Systems.  
Luettavissa: https://www.howtogeek.com/devops/how-to-use-pass-a-command-line-password-manager-for-linux-systems/  
Luettu 09.10.2023  

kpcli - A command line interface to KeePass database files.  
Luettavissa: https://kpcli.sourceforge.io/  
Luettu 09.10.2023  

