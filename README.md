# Linux-course
Homework reports for Linux course ICI001AS3A-3012 taught by Tero Karvinen


# Miniprojekti: Web-palvelin – Nginx + HTML-sivu | Fanny Harju & Satu Harjula

Tämän projektin tarkoituksena on asentaa Nginx-webpalvelin ja julkaisa oma HTML-sivu automaattisesti Saltin avulla yhdellä komennolla.

## Projekttin toiminta

Projektissa yksi Salt sate tekee kaiken tarvittavan:

- Asentaa Nginx-palvelien (pkg.installed)
- Käynnistää palvelun (service.running)
- Kopioi oman index.html -sivun (file.managed) hakemistoon /var/www.html.index.html
- Lopputulos näkyy selaimessa osoitteessa http://localhost

## Lopputulos

<img width="592" height="288" alt="520519837-4a4f59c7-5231-46e3-840a-4d15af8753dd" src="https://github.com/user-attachments/assets/6754ab37-1b41-4862-b5df-5120101685f5" />


## Lisenssi

Projekti on lisensoitu GPLv3-lisenssillä. Katso tarkemmat tiedot tiedostosta LICENSE.
