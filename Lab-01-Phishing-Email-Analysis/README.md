# Lab 01 - Analyse d'un e-mail de Phishing & Authentification (SPF, DKIM, DMARC)

##  Contexte
Un utilisateur a signalé un e-mail suspect prétendant provenir de sa banque (`banque-securite.com`). 
En tant qu'analyste SOC, j'ai extrait et analysé les en-têtes du message pour déterminer sa légitimité et appliquer les mesures de remédiation.

---

##  Données d'Analyse (Headers)

```text
Received: from mail.serveur-inconnu-pirate.ru (IP: 198.51.100.99)
From: service-client@banque-securite.com
Authentication-Results:
   spf=fail (sender IP 198.51.100.99 is not in SPF record for banque-securite.com)
   dkim=fail (header signature invalid)
   dmarc=fail (action=quarantine)
____________________________________________
     ⚙️ Diagnostic Technique
Vecteur d'attaque : Phishing par Domain Spoofing (usurpation d'identité de domaine).

Analyse SPF (Sender Policy Framework) : ÉCHEC (fail). L'adresse IP émettrice (198.51.100.99) n'est pas répertoriée dans l'enregistrement SPF du domaine légitime banque-securite.com.

Analyse DKIM (DomainKeys Identified Mail) : ÉCHEC (fail). La signature cryptographique de l'en-tête est invalide, indiquant une altération du contenu ou de l'émetteur.

Analyse DMARC : ÉCHEC (fail). La politique définie par le domaine émetteur demande la mise en quarantaine (action=quarantine).

🛡️ Mesures de Remédiation (SOC Response)
Isolation de l'IOC : L'adresse IP 198.51.100.99 est identifiée comme un Indicateur de Compromission (IOC) et a été immédiatement bloquée sur le pare-feu périmétrique / proxy.
Confinement Messagerie : Purge et mise en quarantaine automatique du message sur le serveur de messagerie pour empêcher d'autres collaborateurs d'interagir avec le lien malveillant.
Notification & Sensibilisation : Alerte transmise à l'équipe Sécurité et mise à jour de la base de connaissances d'incidents.
