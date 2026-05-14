# Lab 3  Proxy Burp - Interception HTTP/HTTPS sur Android

## Objectif
Configurer un proxy entre un emulateur Android et Burp Suite pour capturer et analyser le trafic reseau.

## Environnement
- PC Hote : Windows
- Emulateur : Genymotion Android 11 API 30
- Proxy : Burp Suite Community Edition

---

## Etapes

### 1. Installation de Burp Suite
Telecharger Burp Suite Community sur https://portswigger.net/burp/communitydownload
Installer et lancer avec un projet temporaire.

### 2. Configuration du Proxy Listener
Dans Burp : Proxy → Proxy settings → Editer le listener 127.0.0.1:8080
Bind to address → All interfaces
Verifier que Running est coche.

<img width="1600" height="787" alt="image" src="https://github.com/user-attachments/assets/b618c43e-3584-4c99-9334-0e1f3684d154" />

---

### 3. IP de la machine hote
Commande : `ipconfig`
IP utilisee : 192.168.56.1

### 4. Configuration du proxy sur l'emulateur
```bash
adb shell settings put global http_proxy 192.168.56.1:8080
Verifier : navigateur emulateur → http://192.168.56.1:8080 → voir page Burp
```

<img width="1067" height="182" alt="image" src="https://github.com/user-attachments/assets/c40604ea-4514-4ec5-85c3-54cbf6eaab0b" />

---

<img width="497" height="995" alt="image" src="https://github.com/user-attachments/assets/2a40e1b3-42fb-4093-90b7-8a5a4964fd5c" />

---

### 5. Capture du trafic HTTP
Burp : Intercept is off
Emulateur : http://neverssl.com
Burp : HTTP history → requete GET / 200 OK

<img width="1600" height="784" alt="image" src="https://github.com/user-attachments/assets/189787f0-e92f-4965-88d1-a1c01cdbabf2" />

---

<img width="1600" height="771" alt="image" src="https://github.com/user-attachments/assets/a744dd28-8a91-47f2-bf63-848a83a25f29" />


### 6. Interception manuelle
Burp : Intercept is on → rafraichir la page → requete bloquee → Forward → Intercept is off

<img width="1470" height="872" alt="image" src="https://github.com/user-attachments/assets/00740495-49cf-4307-9b65-a61edf141f56" />

---

<img width="1600" height="848" alt="image" src="https://github.com/user-attachments/assets/d13e5c8b-1724-44ad-ba6c-b067df7c87eb" />

---

### 7. Certificat HTTPS
Exporter le certificat Burp (DER format)
Transfert : adb push burp_cert.der /sdcard/
Installation :

```bash
adb root
adb remount
adb shell "cat /sdcard/burp_cert.der > /system/etc/security/cacerts/9a5ba575.0"
adb shell chmod 644 /system/etc/security/cacerts/9a5ba575.0
```
Redemarrer l'emulateur.

<img width="1600" height="867" alt="image" src="https://github.com/user-attachments/assets/d98ce9a9-223f-40c8-af6d-04f4fe15b350" />

---

<img width="867" height="107" alt="image" src="https://github.com/user-attachments/assets/d6860720-467c-4980-8efb-c533c3d0c3b6" />

---

<img width="1156" height="82" alt="image" src="https://github.com/user-attachments/assets/f2586de7-e37b-4b1f-97c8-3cf108812062" />

---

<img width="1457" height="417" alt="image" src="https://github.com/user-attachments/assets/82484e69-26cb-4527-8aad-11837830acb5" />


---

### 8. Capture du trafic HTTPS
Emulateur : https://neverssl.com
Burp : HTTP history → requetes HTTPS capturees

<img width="1600" height="846" alt="image" src="https://github.com/user-attachments/assets/8e60002f-db5a-4a47-8f6b-b5ee4946c833" />

---

<img width="1600" height="839" alt="image" src="https://github.com/user-attachments/assets/8a85fbd8-937d-4696-8937-0412d87fd56d" />

---

### 9. Nettoyage
```bash
adb shell settings put global http_proxy :0
```
<img width="802" height="87" alt="image" src="https://github.com/user-attachments/assets/7c6bd914-a069-49a1-b4c7-50a256b997d1" />

---

## Commandes utiles

### Commande	Objectif
```bash
adb shell settings put global http_proxy IP:PORT	Configurer proxy
adb shell settings put global http_proxy :0	Desactiver proxy
adb push fichier.der /sdcard/	Transferer certificat
adb root && adb remount	Mode root
netstat -an | findstr 8080	Verifier Burp
```

## Conclusion
Le lab a permis de configurer Burp comme proxy, capturer du trafic HTTP et HTTPS, et comprendre l'interception des requetes.

## Auteur
**H-oubane**
