# Kotitehtäväraportti h6  

Tässä raportissa tiivistin tuttuun tapaan muutaman artikkelin ja perehdyin Django 4 frameworkin hyödyntämiseen luotaessa weppisivuja. 

## x) Artikkelien tiivistäminen  

Tiivistelmistä ei jälleen tullut kovin tiiviitä, koska ne toimivat myös muistiinpanoina ja opetusmateriaalina itselleni tulevia tehtäviä ajatellen.

### [Karvinen 2023: Python Web - Idea to Production - 2023, Python weppipalvelu - ideasta tuotantoon ICT8TN034-3003](https://terokarvinen.com/2023/python-web-idea-to-production/#osaamistavoitteet "Python Web kurssin osaamistavoitteet")

  - Tämä "artikkeli" oli Tero Karvisen opettaman Python Web kurssin kurssisivu, josta tuli tiivistää vain osaamistavoitteet osio  
  - Weppipalvelu Pythonilla julkisella palvelimella toimii millä tahansa käyttöjärjestelmällä, jossa toimii selain  
  - Kerää automaattisesti tietoja palvelun käytöstä  
  - Samanaikainen tietojen muokkaus usealta käyttäjältä
  - Käyttäjän ei tarvitse asentaa mitään
  - Ohjelman/ohjelmiston päivitys tapahtuu palvelinpuolella, käyttäjällä aina uusin versio

### [Karvinen 2022: Django 4 Instant Customer Database Tutorial](https://terokarvinen.com/2022/django-instant-crm-tutorial/ "Asiakastietokannan rakentaminen Django 4:lla helposti - Tutorial")  

  - Tutorialin sisältö:  
    - Asiakastietokannan rakentaminen  
    - Weppipohjainen käyttöliittymä  
    - Samanaikainen asiakastietokannan käyttö usealta eri käyttäjältä  
    - Alkeita Django 4 weppiframeworkista
  
  - Testattu Debian 11-Bullseyella
  
  - Kehitysympäristön asentaminen  
    - `sudo apt-get -y install virtualenv` Asenna virtualenv työkalu, jolla voi luoda erillisiä python virtuaaliympäristöjä.  
    - `virtualenv --system-site-packages -p python3 env/` Luo uusi hakemisto env/, joka sisältää viimeisimmät paketit hakemistossa /lib/site-packages käyttäen Python 3 versiota.  
    - `source env/bin/activate` Aktivoi luotu ympäristö.  
    - `which pip` --> /home/_käyttäjäsi_/env/bin/pip  
       Varmista, että käytät pip:ä oikeassa ympäristössä! (pip = pythonin pakettiasennus järjestelmä. Ei samalla tavalla luotettava kuin linuxin oma paketinhallinta. EI SUDO OIKEUKSILLA)  
    - Luo requirements.txt johon kirjoitetaan "django".
      `pip install -r requirements.txt` Käske pip:ä asentamaan requirements.txt tiedostossa mainitut paketit.   
      `django-admin --version` Varmista, että Djangosta asentui uusin versio: 4.0.2.  
    - `django-admin startproject _projektinimesi_` Käynnistä projekti.  
    - `cd _projektinimesi_`, `./manage.py runserver`, selaimella: `http://127.0.0.1:8000/`  
  - Admin käyttöliittymä  
    - `./manage.py makemigrations`, `./manage.py migrate` Päivitä tietokanta.  
    - `./manage.py createsuperuser` Lisää admin. (`sudo apt-get install pwgen`, `pwgen -s 20 1` jos kaipaat salasanaa)
  - Asiakastietokannan luonti  
    - `micro _projektinimesi_/settings.py` Muokkaa projektisi settings.py tiedostoa ja lisää sinne rivi `'crm'`  
    - `micro crm/models.py` Lisää lomakepohja malleja hyödyntäen muokkaamalla models.py tiedostoa seuraavasti:
        
          from django.db import models
      
          class Customer(models.Model):  
          name = models.CharField(max_length=300)  
    - `./manage.py makemigrations`, `./manage.py migrate` Päivitä muutokset tietokantaan.
    - `micro crm/admin.py` Muokkaa admin.py tiedostoa ja lisää sinne seuraavat rivit:
      
          from django.contrib import admin  
          from . import models  
    
          admin.site.register(models.Customer)  
    - `./manage.py runserver` Tarkista toimenpiteiden onnistuminen: `"Log into http://127.0.0.1:8000/admin/"`  
   - Listanäkymän muokkaaminen
      - `micro crm/models.py` Lisää models.py tiedoston loppuun seuraavat rivit:
        
            def __str__(self):  
            return self.name
          
### [Karvinen 2022: Deploy Django 4 - Production Install](https://terokarvinen.com/2022/deploy-django/ "Tuotantopalvelimen pystyyn laittaminen")

  - Artikkelin sisältö:
    - Esivaatimukset linux komentorivin käyttö, asennettu linux järjestelmä, vuokrattu vps  
    - Micro editorin asennus  
    - Apache2 asennus  
    - Weppi sisällön luominen  
    - Virtual Hostin luominen  
    - VirtualEnvin ja Djangon asentaminen
    - Uuden django projektin luominen
    - Pythonin liittäminen Apacheen käyttäen mod_wsgi:tä
    
  - Keskityin tässä artikkelissa viimeiseen kohtaan, koska muut kohdat on pääosin joko tehty aiemmin kurssilla tai käsitelty tämän kotitehtävän muissa artikkeleissa
      
  - Olennaista on tietää kolme absoluuttista hakemistopolkua seuraaviin kohteisiin:
    - Django projektin päähakemisto (TDIR)  
    - Django projektin wsgi.py tiedoston sijainti (TWSGI)
    - Virtualenv:n sivustopakettien hakemisto (TVENV)
    - `sudoedit /etc/apache2/sites-available/teroco.conf` Sudoeditillä muokataan apacheen sivusto saataville ja lisätään seuraavat muutettuna omilla tiedoilla:
    
    
          Define TDIR /home/tero/publicwsgi/teroco
          Define TWSGI /home/tero/publicwsgi/teroco/teroco/wsgi.py
          Define TUSER tero
          Define TVENV /home/tero/publicwsgi/env/lib/python3.9/site-packages
          # See https://terokarvinen.com/2022/deploy-django/
  
          <VirtualHost *:80>  
                Alias /static/ ${TDIR}/static/  
                <Directory ${TDIR}/static/>  
                        Require all granted  
                </Directory>  
  
                WSGIDaemonProcess ${TUSER} user=${TUSER} group=${TUSER} threads=5  
          python-path="${TDIR}:${TVENV}"  
                WSGIScriptAlias / ${TWSGI}  
                <Directory ${TDIR}>  
                     WSGIProcessGroup ${TUSER}  
                     WSGIApplicationGroup %{GLOBAL}  
                     WSGIScriptReloading On  
                     <Files wsgi.py>  
                        Require all granted  
                     </Files>  
                </Directory>  
     
          </VirtualHost>  
             
          Undefine TDIR   
          Undefine TWSGI   
          Undefine TUSER  
          Undefine TVENV   
     
    - `sudo apt-get -y install libapache2-mod-wsgi-py3` Asennetaan apachen WSGI moduuli.
    - `/sbin/apache2ctl configtest` Tarkistetaan syntaksi.
    - `sudo systemctl restart apache2` Käynnistetään apache, jotta muutokset tulevat voimaan.
    - `curl -s localhost|grep title`  Etsitään localhostilta "title" ja katsotaan mitä palauttaa. Pitäisi tulla "<title>The install worked successfully! Congratulations!</title>"
    - `curl -sI localhost|grep Server` Varmistetaan, että kyseessä on todellakin apachen pyörittämä serveri eikä pelkkä suojaamaton kehitysympäristö. Pitäisi tulla "Server: Apache/2.4.52 (Debian)".         Rippuen omasta apache ja distro versiostasi toki.
    - Tarkista toimivuus nettiselaimessa. Pitäisi näkyä Djangon ilmoitus DEBUG=True jne.  
  - Debug moodin poisto:
    - Muokkaa Django projektisi settings.py tiedostoa (oman projektin nimi tilalle):  
      `cd`  
      `cd publicwsgi/teroco/`  
      `micro teroco/settings.py`  
    - Muuta vain seuraavia rivejä tiedostosta vastaaviksi (Localhost on testausta varten. Oman sivuston nimi "hello.terokarvinen.com" tilalle. Näkyy julkisesti. Se minkä vuokrasit.):
      
           DEBUG = False
           ALLOWED_HOSTS = ["localhost", "hello.terokarvinen.com"]
  
    - `touch teroco/wsgi.py` Kun koodaat jotain uutta sivulle tai muutat asetuksia muista päivittää (OMAN) projektisi wsgi.py tiedoston aikaleimat.
    - `sudo systemctl restart apache2` Suurempia muokkauksia tehtäessä voit joutua käynnistämään apachen uudelleen.
    - `curl -s localhost|grep title` --> "<title>Not Found</title>" Varmista, että sivusto antaa uuden ilmoituksen.
       
  - Staattisten ominaisuuksien käyttöönotto apacheen, esim CSS tyylisivut
    - Muokkaa Django projektisi settings.py tiedostoa (oman projektin nimi tilalle):  
      `cd`  
      `cd publicwsgi/teroco/`  
      `micro teroco/settings.py`  
    - Lisää rivit:  
      `import os`  Tiedoston alkuun muiden importtien joukkoon.  
      `STATIC_ROOT = os.path.join(BASE_DIR, 'static/')`
        
    - `./manage.py collectstatic` --> yes
    - Tyylisivut käytössä nyt myös apachen live versiossa sivuistasi. Jes. Ja sitten kaikki tämä pitäisi osata laittaa käytäntöön. Helppoa, eikö vain. Mitään odottamatonta ei ikinä tapahdu..
   

## a) Django-kehitysympäristön asentaminen esimerkkisivuun asti  

Alkuun kirjauduin paikalliselle virtuaalikoneelleni ja pyörittelin `sudo apt-get update` sekä `sudo apt-get upgrade`, jonka jälkeen otin yhteyden virtuaalikoneeseeni `ssh ali@vararikko.xyz` ja tein samat toimenpiteet siellä.  
  
Tämän jälkeen asensin virtualenvin komennolla `sudo apt-get -y install virtualenv`. Asentamiseen meni muutama minuutti, jonka aikana ehdin hiukan tutkia virtualenviä. Virtualenv on lyhyesti Python Packaging Authorityn kehittämä työkalu, jolla voi luoda "eristettyjä" Python virtuaaliympäristöjä. ([Python Packaging Authority](https://virtualenv.pypa.io/en/latest/index.html))  

Sitten loin uuden virtuaaliympäristön komennolla `virtualenv --system-site-packages -p python3 env/`

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/0458d9e6-38e3-4ac3-a351-3b20305ec30c)  
  
Seuraavaksi otin käyttöön juuri asentamani virtualenvin source komennolla, joka suorittaa lukee/suorittaa annetun tiedoston: `source env/bin/activate`.  
Oletan, että tämä teki mitä halusin, koska käyttäjäni eteen ilmestyi "(env)".  
  
![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/e59d5b6b-aab4-4ec0-a4ee-ee49bdf03495)  
  
Tarkistin ohjeiden mukaisesti `which pip` -komennolla, että `pip`, jonka kohta tulisin suorittamaan suoritettaisiin virtualenvissä. Hakemistopolku vastasi ohjeissa annettua "/home/tero/env/bin/pip" korvattuna omalla käyttäjälläni.  
  
![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/a189a501-f5be-4115-98d4-2f7aceea8083)  
  
Seuraavaksi asensin micro editorin `sudo apt-get install micro`. Tässä välissä katsoin mielenkiinnosta oman hakemistosijaintini koneella (`ls`, `pwd`). Sitten loin sekä muokkasin microlla tiedostoa "requirements.txt";  
lisäsin tiedostoon sanan "django": `micro requirements.txt` --> django crtl-S --> ctrl-Q.   
Varmistin vielä komennolla `cat requirements.txt`, että olin onnistunut. Hyvältä näytti.    
  
![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/4de066f3-aed9-4019-ab6e-8807b06d7db9)
  
Sitten käskin pip:ä asentamaan requirements.txt tiedostoon määritellyt paketit komennolla `pip install -r requirements.txt`. Ja tarkistin komennolla `django-admin --version`, että djangosta oli asentunut oikea versio. Minulla oli versio 4.2.5, ohjeissa oli versio 4.0.2.   
  
![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/0742869d-8ed4-47fd-8391-b12eee0ac188)  
  
`django-admin startproject allikko` -komennolla loin itselleni uuden projektin nimeltään "allikko".  
Navigoin ohjeiden mukaan projektikansioon `cd allikko` ja suoritin siellä komennon `./manage.py runserver`.  
Minulla kerrottiin olevan "18 unapplied migration(s)" ja ne kehotettiin ajamaan läpi tai projekti ei välttämättä toimi halutusti.  
  
![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/2817facc-3162-4c49-b3aa-5274d74e6e48)  

Nyt edessäni oli pienimuotoinen aloittelija ongelma. Terminaalissani pyöri nyt oletettavasti serveri, enkä päässyt pois siitä sulkematta serveriä eli en päässyt testaamaan selaimella tai curlilla oliko serveri oikeasti pystyssä.  
Ratkaisin ongelman ottamalla paikalliselta virtuaalikoneeltani (LinuxNub) uuden ssh yhteyden vps koneeseeni (nodeli). Näin sain uuden terminaalin käyttööni.  
Muistelin, että en ollut saanut selainta vielä toimintaan nodelilla tässä vaiheessa, joten tarkastin devserverin toiminnan komennolla `curl http://127.0.0.1:8000`.  
Aloittelija kun olen, en osannut antaa curlille mitään hienoja lisäkomentoja, joilla olisin saanut tarvitsemani tiedon kompaktisti ja siististi eli eteeni lävähti koko nettisivun koodi.  
Heti alusta löysin kuitenkin haluamani tiedon eli `<title>The install worked successfully! Congratulations!</title>`.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/e8e45196-d495-499d-a047-4509f2fc10a9)  

## b) Yksinkertaisen esimerkkitietokannan luominen django-kehitysympäristöön ja tietojen muokkaaminen admin-liittymällä.  

Kotitehtäväkohta vaihtui, mutta ohjeet jatkuivat samasta [artikkelista](https://terokarvinen.com/2022/django-instant-crm-tutorial/ "Toinen tiivistetty artikkeli").  
Oli aika päivittää tietokanta eli tehdä migraatiot, joista minulle aiemmin valiteltiinkin.  
`./manage.py makemigrations`  
`./manage.py migrate`  
Näyttivät menevän läpi ongelmitta.  
   
![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/38d22a60-e940-4457-a8e4-bf4043926e01)

Tässä vaiheessa ajattelin tutkailla miten ohjeissa vinkattu pwgen toimii, joten asensin sen komennolla `sudo apt-get install pwgen`. Tein tämän terminaalissa, jossa minulla pyöri virtualenv. En ollut varma vaikuttiko tämä jotenkin johonkin, joten päätin suorittaa saman komennon vielä terminaalissa, jossa virtualenv ei ollut päällä. Tämän perusteella ei ollut mitään ongelmallista tapahtunut, mutta en ole siitä täysin varma.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/131df576-7024-434d-a5dc-4fd7d5222bca)

Seuraavaksi tutkin pwgenin toiminnallisuutta `man pwgen` ja erityisenä fokuksena ohjeiden komento `pwgen -s 20 1`.  
Ilmeisesti tämä komento käskee pwgeniä luomaan yhden kappaleen täysin satunnaisia (-s), joskin hankalasti muistettavia salasanoja pituudeltaan 20 merkkiä. `pwgen [ OPTION ] [ pw_length ] [ num_pw  ]`  

Tähän hienoon työkaluun tutustuttuani loin django projektilleni superuserin `./manage.py createsuperuser`.  
Käyttäjänimeksi jätin oletuksena ali.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/4c0fe9ab-7bac-4ab2-8ae4-8ab30457739a)

Tässä vaiheessa olisi tosiaan se selain pitänyt saada toimintaan nodelilla, joten päätin tutkia asiaa netistä ja päädyin kokeilemaan [w3m nimistä ratkaisua](https://www.wikihow.com/Browse-the-Internet-Using-the-Terminal-in-Linux "wikihow browse internet with terminal").  
Pidin tätä ratkaisua kohtuu luotettavana, koska siinä hyödynnettiin linuxin omaa paketinhallintaa ohjelmien asentamiseen `sudo apt-get install w3m w3m-img`.
Ohjelma asentui hetkessä, mutta valitettavasti en saanut sillä auki haluamaani näkymää. Google tosin toimi. Oletuksena saksan kielisenä.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/31942cc5-3da1-4647-a37f-620c94a2e32b)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/a82e87f1-feca-4b7b-b7e5-3ff50778f418)

Tässä vaiheessa aloin miettimään oliko tehtävä tarkoitus suorittaa paikallisella virtuaalikoneellani. No, meni jo. Kävin kuitenkin katsomassa omalla koneellani vararikko.xyz ja siellä näkyi vielä aiemmissa tehtävissäni laittama testisivu.  
  
Kokeilin vielä `curl http://127.0.0.1:8000/admin/` ja `curl http://127.0.0.1:8000/`. Nämä tuottivat toisessa terminaali ikkunassa (se missä django devserveri pyöri) selvästi jotain, mutta eipä tämä käytännössä minua kauheasti auttanut.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/d325fe2d-7685-401d-b556-b2a8e1dae9b4)

Siispä siirryin etsimään toista ratkaisua. Valitettavasti en löytänyt toista ratkaisua, joten päädyin tekemään yllä mainitut toimenpiteet uudestaan paikallisella virtuaalikoneellani hyödyntäen tätä kirjoittamaani raporttia. Huomasinkin jättäneeni raportin teksistä pois kohdan, jossa luotiin uusi virtuaaliympäristö ja korjasin asian. Nimesin uuden projektini "oja". Kotitehtävän vaihe a) oli nyt suoritettu LinuxNub koneella: 

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/ed7e9962-8589-447c-a206-93bb91d07cab)

Jatkoin samaa mitä olin tehnyt aiemminkin eli loin superuserin (alir) ja nyt pääsin selaimella kirjautumissivullekin.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/40da4f5e-a6d8-4cfc-b5b1-b11acb56602a)

Ja kirjautuminenkin onnistui käyttäjänä alir.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/dffbbe1e-f80d-4be3-931b-faf0d8d6c875)

Loin myös uuden käyttäjän "Pallokala", jolle asetin Staff ja superuser oikeudet.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/74252332-533a-49e8-8005-ae7bb29658e0)

Seuraavaksi aloin luomaan asiakastietokantaa.  
`./manage.py startapp crm` loi uuden hakemiston (crm) tulevalle app:lle.  
`ls` komennolla varmistin tämän. 

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/877d3009-d72e-4129-9336-2a0375d2dbfe)

`micro oja/settings.py` Lisäsin asetustiedostoon tämän uuden app:n.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/a5792b6c-ead5-4ce1-a2bd-9eb9e95c6e94)

`micro crm/models.py` Lisäsin malleja, joista Django voisi automaattisesti luoda tietokannan.  
Lisäsin tiedostoon rivit: 

        class Customer(models.Model):  
        name = models.CharField(max_length=300)

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/80775639-b7ee-4251-83c6-73a0651f673c)

`./manage.py makemigrations`, `./manage.py migrate`. Päivitin tietokannan.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/f3290d25-c220-4e38-ac57-bd0d97f62c9a)

`micro crm/admin.py` Lisäsin tiedostoon admin.py seuraavat rivit:  

        from . import models  
        admin.site.register(models.Customer)  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/edc5f785-04c0-47ab-b7cb-06100f9dbb12)

Käynnistin taas serverin ja kirjauduin käyttäjänä Pallokala.  
CRM ja Customerit näkyivät.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/63e6d096-bbff-4bc7-b526-09d1175339ac)

"Asiakkaiden" lisääminen onnistui.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/0c4e5247-df37-4f7c-99b2-ec61a7fe3be9)

Suljin serverin ja muokkasin tiedostoa models.py `micro crm/models.py` lisäämällä rivit:  

      def __str__(self):
      return self.name

Menin takaisin serverille katsomaan oliko näkymä muuttunut ja olihan se:  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/d5f54e6c-99cc-439f-b8a0-eadef4948d74)

## c) Djangon tuotantotyyppinen asennus omalle, paikalliselle virtuaalikoneelle  

45min aikaa ennen palautusta, joten katsotaan kuinka pitkälle päästään. 

`mkdir -p publicwsgi/oja/static/` Loin uuden hakemiston, jonne tein microlla tiedoston index.html, johon kirjoitin "Statically see you at ThePond.com".  
`sudoedit /etc/apache2/sites-available/oja.conf` Loin uuden VirtualHostin.  

    <VirtualHost *:80>
	      Alias /static/ /home/alir/publicwsgi/oja/static/
	      <Directory /home/alir/publicwsgi/oja/static/>
		        Require all granted
	      </Directory>
    </VirtualHost>


![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/25928c13-d02b-4a81-b053-41ee7f3e2fed)

Kävin laittamassa uuden virtualhostin käyttöön.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/8a4b7400-2d75-4310-a04e-eb14f3872d72)

Palasin vielä muokkaamaan hiukan aiemmin luomaani oja.conf tiedostoa, koska halusin hyödyntää name based virtual hostingia.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/b2532240-b72d-44c7-92a7-c1de95818f30)

`sudo a2ensite oja.conf` Otin sivuston käyttöön.  

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/ec8aea4a-b958-4129-a3b7-c000406bbcb9)

`sudo systemctl restart apache2` Ja uudelleenkäynnistin apache2.  
`curl http://localhost/static/` -komennolla en saanut haluamaani sivustoa.

![kuva](https://github.com/Romaalie/LinuxPalvelimet_Kotitehtavat/assets/143311643/a7903521-afe8-44a2-8447-980b609c2dd5)

---------------------------------------- AIKARAJA TULI VASTAAN -------------------------------------------
Keskeytys ajalla 02.10.2023 klo 13.45.

Olin varmaankin sotkenut jotain asetuksia tehdessäni tätä vaihetta kiireellä, eikä minulla nyt ollut ennen palautusta aikaa tutkia tarkemmin mikä oli vialla. Harmi. Ehkäpä voin jatkaa tehtävän tekemistä myöhemmin jos sellainen on sallittua. Katsokoot ihmiset muutoslokista vaikka mitä on tehty missäkin vaiheessa. Jos sitä muut edes näkee.


## **Lähteet**  
Karvinen 2023. Python Web - Idea to Production - 2023, Python weppipalvelu - ideasta tuotantoon ICT8TN034-3003.  
Luettavissa: https://terokarvinen.com/2023/python-web-idea-to-production/#osaamistavoitteet  
Luettu 02.10.2023  

Karvinen 2022. Django 4 Instant Customer Database Tutorial.  
Luettavissa: https://terokarvinen.com/2022/django-instant-crm-tutorial/  
Luettu 02.10.2023  

Karvinen 2023. Deploy Django 4 - Production Install.  
Luettavissa: https://terokarvinen.com/2022/deploy-django/  
Luettu 02.10.2023  

Python Packaging Authority. virtualenv.  
Luettavissa: https://virtualenv.pypa.io/en/latest/index.html  
Luettu 02.10.2023  





