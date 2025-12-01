# Linux-course
Homework reports for Linux course ICI001AS3A-3012 taught by Tero Karvinen


# Miniprojekti: Web-palvelin – Nginx + HTML-sivu | Fanny Harju & Satu Harjula

Tämän projektin tarkoituksena on asentaa Nginx-webpalvelin ja julkaisa oma HTML-sivu automaattisesti Salin avulla yhdellä komennolla.

## Projekttin toiminta

Projektissa yksi Salt sate tekee kaiken tarvittavan:

- Asentaa Nginx-palvelien (pkg.installed)
- Käynnistää palvelun (service.running)
- Kopioi oman index.html -sivun (file.managed) hakemistoon /var/www.html.index.html
- Lopputulos näkyy selaimessa osoitteessa http://localhost

## Lopputulos
