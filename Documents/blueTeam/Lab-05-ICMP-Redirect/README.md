

# Lab-05 : ICMP Redirect Attack Analysis

> **Cadre de formation :** TP réalisé dans le cadre du cours **FUN MOOC / Institut Mines-Télécom** (Plateforme Labtainer).


##  Objectif du Laboratoire
Comprendre le fonctionnement des attaques de redirection ICMP (niveau 3) et analyser l'impact sur un protocole non chiffré (Telnet) capturé via Wireshark.

##  Topologie du Réseau
* **Victime** : `192.168.1.1`
* **Attaquant** : `192.168.1.2`
* **Passerelle Légitime** : `192.168.1.10`
* **Serveur (Cible Telnet)** : `192.168.2.1`

##  Points Clés & Concepts Techniques
* **Persistance** : Utilisation de l'option `-l` pour maintenir les redirections ICMP en continu.
* **Paramètre `-G`** : Permet de spécifier la passerelle à usurper de façon à ce que le client accepte l'ICMP redirect.
* **Remarque technique de dépannage** : L'utilisation de `sudo ip route flush cache` permet d'invalider la table de routage en cache sur la victime pour forcer la mise à jour immédiate.


## 📸 Captures d'écran & Preuves d'exécution

### 1. Analyse des options de l'attaque
![Options de l'attaquant](img/Captureattacker.jpg)

### 2. Configuration et exécution de l'attaque
![Lancement de l'attaque](img/Captureattacker2.jpg)

### 3. Manipulation de la victime et test de routage
![Console de la victime](img/Capturevictim.jpg)

### 4. Analyse du trafic réseau (Wireshark)
![Capture Wireshark Telnet](img/CaptureTELNETLab5.jpg)
