# LAB PROXY BURP - RAPPORT D'ANALYSE

## Perimetre
- Date : 15/05/2026
- Analyste : [votre nom]
- Environnement : Genymotion Android 11 API 30
- Proxy : Burp Suite Community v2026.4.3
- IP Hote : 192.168.56.1
- Port Proxy : 8080
- Cible : neverssl.com (HTTP et HTTPS)

## Configuration
- Proxy Android : manuel 192.168.56.1:8080
- Certificat Burp : installe sur l'emulateur
- Interception : testee puis desactivee

## Trafic capture (HTTP)
URL : http://neverssl.com
Methode : GET
User-Agent : Mozilla/5.0 (Linux; Android 11; Phone Build/RQ1A_210105.003; wv)
Host : neverssl.com
Accept : text/html,application/xhtml+xml...

## Trafic capture (HTTPS)
URL : https://www.google.com/generate_204
Methode : GET
Statut : 204 No Content

## Observations
- Le proxy intercepte correctement le trafic HTTP et HTTPS
- Le certificat Burp permet de decrypter le trafic HTTPS
- L'interception permet de bloquer et analyser les requetes en temps reel

## Nettoyage (a faire)
- Desactiver le proxy sur l'emulateur
- Supprimer le certificat Burp (si necessaire)