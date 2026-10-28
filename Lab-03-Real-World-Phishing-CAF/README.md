# Lab 03 - Analyse d'une attaque réelle de Phishing (Typosquatting & Bypass DMARC)

##  Contexte
Analyse d'un e-mail malveillant réel ciblant les usagers de la CAF (Caisse d'Allocations Familiales) prétextant un faux remboursement de **949,16 €**. 
L'objectif de ce laboratoire est de décortiquer les en-têtes bruts (*raw headers*) pour comprendre comment l'attaquant a contourné les filtres de sécurité.

---

##  Données Techniques Extraites (Headers & IOCs)

* **Emetteur affiché :** `Report_CAF <portail@espacecaf.com>`
* **Adresse IP source (IOC) :** `148.113.250.31` (`mail.espacecaf.com`)
* **Domaine frauduleux :** `espacecaf.com` (Domaine légitime de la CAF : `caf.fr`)
* **Outil d'attaque :** `PHPMailer 7.1.1`
* **Niveau de Spam attribué :** `X-lpn-spamrating : 69` (Low)

```text
Received: from mail.espacecaf.com (mail.espacecaf.com [148.113.250.31])
Authentication-Results: laposte.net;
   spf=pass smtp.mailfrom=portail@espacecaf.com;
   dkim=pass reason="good signature" header.d=espacecaf.com;
   dmarc=pass reason="SPF is aligned, DKIM is aligned";

⚙️ Diagnostic SOC & Mécanisme de l'Attaque
Technique : Typosquatting / Domain Squatting. L'attaquant n'a pas usurpé le vrai domaine caf.fr, il a acheté un nom de domaine très proche (espacecaf.com).

Contournement DMARC (dmarc=pass) : Comme le domaine appartient à l'attaquant, il a configuré ses propres clés SPF et DKIM sur son serveur. Les contrôles de sécurité valident donc le mail sur la forme, mais le domaine est malveillant sur le fond.

Ingénierie Sociale : Usurpation d'organisme public, promesse de gain financier et lien de redirection piégé (FluentCRM).

🛡️ Remédiation & Actions SOC
Blocage d'IOC : Blocage immédiat de l'adresse IP 148.113.250.31 et du domaine espacecaf.com sur le proxy et le pare-feu.

Signalement : Signalement du domaine malveillant sur la plateforme Phishing Initiative et Signal-Spam.
Purger la messagerie : Suppression globale des e-mails provenant de @espacecaf.com dans l'ensemble des boîtes de l'organisation.
