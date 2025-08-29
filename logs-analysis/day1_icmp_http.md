# Mission Day 1 – Analyse réseau avec Wireshark

## 🧭 Objectif
Capturer et analyser une requête **ICMP (ping)** et une **requête HTTP GET** à l'aide de Wireshark.

---

## 🔹 Étape 1 – Résolution DNS

### Requête pour `google.com`
- **Source IP** : 10.0.X.X *(anonymisée)*
- **Destination DNS** : 10.0.X.X
- **Type** : `A` et `AAAA`
- **Résultat** : `google.com` → `142.250.75.238`

### Requête pour `example.com`
- **Résultat** : `example.com` → Plusieurs adresses, dont `23.220.75.232`

*Observation : Les résolutions DNS ont bien fonctionné pour les deux domaines.*

---

## 🔹 Étape 2 – ICMP (ping vers google.com)

| Élément        | Détail                    |
|----------------|---------------------------|
| Type           | Echo Request / Echo Reply |
| IP destination | `142.250.75.238` (Google) |
| TTL (aller)    | 64                        |
| TTL (retour)   | 255                       |
| Résultat       | 4 paquets reçus, 0% perte |

*Observation : Ping fonctionnel, latence stable. Les échanges ICMP ont été capturés avec succès via le filtre `icmp`.*

---

## 🔹 Étape 3 – Requête HTTP (curl http://example.com)

### Connexion TCP
- **3-Way Handshake** visible :
  - SYN → SYN-ACK → ACK
- **Port destination** : 80 (HTTP)

### Requête HTTP GET
- **Méthode** : `GET / HTTP/1.1`
- **Host** : `example.com`
- **User-Agent** : `curl/7.X.X`
- **Réponse** : `HTTP/1.1 200 OK`
- **Contenu** : HTML (visible dans Wireshark)

*Observation : Requête HTTP non chiffrée capturée intégralement. Headers visibles. Filtrée avec `http`.*

---

## 🔒 Informations sensibles filtrées

- IP locales anonymisées (ex : `10.0.X.X`)
- Aucune adresse MAC incluse
- Aucun identifiant personnel
- Tous les domaines utilisés sont publics (aucune donnée privée)

---

## 🧠 Leçons retenues

- Savoir identifier les différentes étapes d’un échange réseau : DNS → ICMP → TCP → HTTP
- Utilisation des filtres Wireshark (`icmp`, `http`, `dns`)
- Importance de l’anonymisation dans les rapports professionnels
- Visualisation d’un 3-way handshake + d’une requête GET complète

---

✅ Rapport rédigé dans le cadre d’un entraînement Blue Team (SOC Analyste Niveau 1)

