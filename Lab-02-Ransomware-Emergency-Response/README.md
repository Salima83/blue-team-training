# Lab 02 - Réponse d'Urgence Ransomware & Protocole S.I.E.R.A

   ##  Contexte
Alerté par un utilisateur dont les fichiers locaux prenaient l'extension `.locked` avec apparition d'une demande de rançon, j'ai appliqué la procédure de réponse à incident pour circonscrire l'attaque par Ransomware.

---

##  Procédure SOC (Protocole S.I.E.R.A)

1. **S - Stop (Isolation immédiate) :** 
   * Déconnexion réseau du poste (câble RJ45 / Wi-Fi) pour stopper la propagation latérale sur le réseau.
   * **Conservation de la RAM :** La machine **ne doit pas être éteinte** afin de préserver la mémoire vive (RAM) pour l'analyse Forensics (extraction de clés de chiffrement ou artefacts).
2. **I - Investigate (Investigation) :** 
   * Recherche de la commande de suppression des copies d'ombre des fichiers (`vssadmin delete shadows`).
   * Identification du processus malveillant dans le gestionnaire des tâches.
3. **E - Eradicate (Éradication) :** 
   * Arrêt du processus malveillant et suppression de la persistance (clés de registre Run, tâches planifiées).
4. **R - Restore (Restauration) :** 
   * Restauration des données à partir de sauvegardes saines, isolées et hors-ligne (*offline backups*).
5. **A - Analyze (Analyse Post-Incident) :** 
   * Rédaction du rapport d'incident, mise à jour des signatures EDR et renforcement des règles de filtrage.
