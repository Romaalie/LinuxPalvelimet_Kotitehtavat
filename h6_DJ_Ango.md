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
        
