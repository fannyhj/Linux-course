# Web-palvelin – Nginx + HTML-sivu | Fanny Harju & Satu Harjula

Projektissamme yksi Salt state asentaa Nginxin ja laittaa oman index.html -tiedoston paikoilleen. Projekti siis asentaa Nginx-palvelimen ja julkaisee esimerkkisivun automaattisesti. Nginx on avoimen lähdekoodin ohjelmisto, jota käytetään pääasiassa verkkopalvelimena, mutta voidaan käyttää myös välityspalvelimena (reverse proxy), kuormantasaajana (load balancer) ja välimuistina (caching). (Nginx.org, 2025)

Aloitimme projektin tekemällä uuden virtuaalikoneen. Ajattelimme, että toinen ottaisi SSH-yhteyden toisen koneeseen ja tekisimme yhdessä projektia samalle koneelle. Oli kuitenkin SSH-yhteyden muodostamiesssa useita ongelmia, joten päätimme tehdä projektia omilla koneillamme.

Teimme projektin vanhalle virtuaalikoneelle, koska emme saaneet uutta toimimaan. Koneelle oli jo asenettuna Salt, mutta tarkistin sen vielä komennolla "Sudo salt-call --local test.ping" ja sain tulostuksena 'True'. 

Loimme ensimmäiseksi rakenteen komennolla "sudo mkdir -p /srv/salt/web/files" ja siirryimme hakemistoon cd:llä. 

Määritimme sitten mitä stateja ajetaan top.sls-tiedostossa komennolla "sudo nano /srv/salt/top.sls" ja kirjoitmme sinne seuraavan:

base:

  '*':
  
    - web

Tämän jälkeen avasimme init.sls-tiedoston komennolla "sudo nano /srv/salt/web/init.sls". Tiedostoon sisällytimme ohjeet Nginxin asentamiseen ja HTML-sivun paikoilleen laittamisen. (Salt Project, 2025) Kuvassa näkyy tiedoston sisältö:


<img width="837" height="466" alt="image" src="https://github.com/user-attachments/assets/6f6db70e-d73d-4536-a664-4573facba161" />




Seuraavaksi kirjoitimme HTML-koodin, joka lopulta näkyy selaimessa. Teimme tämän index.html:ssä komennolla "sudo nano /srv/salt/web/files/index.html". Kuva alla.


<img width="728" height="249" alt="image" src="https://github.com/user-attachments/assets/91bce59f-dfad-44a7-a146-788143644a1f" />




Yritin sitten kokeilla, että kaikki on okei ennen virallista ajamista. Tein tämän komennolla "sudo salt-call --local state.apply test=TRUE".


<img width="1102" height="158" alt="image" src="https://github.com/user-attachments/assets/7fd52694-05e6-421b-83ec-e9419415bab8" />


Kuvassa näkyy, ettei tämä toiminut joten katselin init.sls-tiedostoani ja huomasin, että unohdin viivan viimeisen rivin edestä. Korjasin tämän ja alkoi toimimaan.


<img width="1080" height="480" alt="image" src="https://github.com/user-attachments/assets/ce7cdcf7-023a-4df9-97c9-afd0b28ea7c7" />


Tulostuksessa näkyi 1=failed. Tämä oli koska Apache2 takia, joten poistin sen seuraavilla komennoilla:

- sudo systemctl stop apache2

- sudo systemctl disable apache2

- sudo apt-get remove -y apache2


Sitten varmistin, että Nginx-palvelin on käynnissä komennoilla:


- sudo systemctl start nginx

- sudo systemctl status nginx
 

Tämän jälkeen alkoi toimimaan. Kokeilin sitten lopullisen tuloksen komennolla "sudo salt-call --local state.apply".

<img width="949" height="502" alt="image" src="https://github.com/user-attachments/assets/7aa8a70a-46b0-453e-aae3-05fc44e66a73" />


Tarkisimme viimeisenä, että teksti näkyy http://localhostissa verkkoselaimella.

<img width="592" height="288" alt="image" src="https://github.com/user-attachments/assets/4a4f59c7-5231-46e3-840a-4d15af8753dd" />

Kaikki toimii, joten projekti sai päätöksen!


## Lähteet:

Nginx - https://nginx.org/

Tero Karvinen, 2025. Palvelinen hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/#laksyt

Salt Project, 2025. The Top File. Luettavissa: https://docs.saltproject.io/en/3006/ref/states/top.html

Salt Project, 2025. Salt.States.Pkg. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.pkg

Salt Project, 2025. Salt.States.File. Luettavissa: https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file

ChatGPT:tä hyödynnetty aiheen keksimiseen ja virheiden korjaukseen.
