# Kotitehtäväraportti h6  

_Tässä raportissa jne_  

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
    - `cd _projektinimesi_`, `./manage.py runserver`, selaimella: http://127.0.0.1:8000/  
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
    - `./manage.py runserver` Tarkista toimenpiteiden onnistuminen: "Log into http://127.0.0.1:8000/admin/"
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
   

## a) Asenna Django-kehitysympäristö niin, että näet './manage.py runserver' esimerkkisivun.  


  


## **Lähteet**  
Karvinen 2023, Python Web - Idea to Production - 2023, Python weppipalvelu - ideasta tuotantoon ICT8TN034-3003  
Luettavissa: https://terokarvinen.com/2023/python-web-idea-to-production/#osaamistavoitteet  
Luettu 02.10.2023  

Karvinen 2022, Django 4 Instant Customer Database Tutorial  
Luettavissa: https://terokarvinen.com/2022/django-instant-crm-tutorial/  
Luettu 02.10.2023  

Karvinen 2023, Deploy Django 4 - Production Install  
Luettavissa: https://terokarvinen.com/2022/deploy-django/  
Luettu 02.10.2023  




