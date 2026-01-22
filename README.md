# Cisco NAT Laboratory – Packet Tracer  
### PAT, NAT statique et NAT dynamique 

---

## 📌 Présentation du projet

Ce projet présente une **implémentation complète et comparative du Network Address Translation (NAT)** dans un environnement simulé à l’aide de **Cisco Packet Tracer**.

Il couvre :
- le **NAT Overload (PAT)**,
- le **NAT statique** pour la publication de services,
- le **NAT dynamique** avec pool d’adresses publiques,
- des mécanismes de **réalisme réseau** (routage ISP, filtrage des IP privées).

Le projet est conçu dans une optique **académique (niveau Master)** et peut également servir de **portfolio technique**.

---

## 🎯 Objectifs pédagogiques

- Comprendre le rôle et la nécessité du NAT dans les réseaux IPv4
- Implémenter et comparer les trois principaux types de NAT
- Observer les limites opérationnelles du NAT dynamique
- Mettre en œuvre des bonnes pratiques proches d’un environnement réel
- Savoir valider et documenter une configuration réseau

---

## 🧱 Topologie du laboratoire

### Éléments
- 1 routeur Entreprise (**R1**)
- 1 routeur Fournisseur d’accès (**R2 – ISP**)
- 1 switch LAN
- 3 hôtes internes
- 1 serveur Web interne
- 1 réseau Internet simulé

📷 Voir : `screenshots/topology.png`

---

## 🌐 Plan d’adressage

### LAN interne
- Réseau : `192.168.10.0/24`
- Passerelle : `192.168.10.1`

### WAN (R1–R2)
- Réseau : `203.0.113.0/30`

### Internet simulé
- Réseau : `198.51.100.0/24`

### IP publiques routées
- NAT statique : `203.0.113.100`
- Pool NAT dynamique : `203.0.113.200 – 203.0.113.202`

---

## 🔁 Types de NAT implémentés

### 1️⃣ NAT Overload (PAT)
- Partage d’une seule IP publique
- Traduction basée sur les ports
- Utilisation d’une ACL dédiée (`ACL_PAT`)

📷 Capture : `screenshots/nat_pat.png`

---

### 2️⃣ NAT statique
- Publication du serveur interne `192.168.10.100`
- Correspondance permanente avec `203.0.113.100`
- IP publique représentée par une **interface loopback**
- Routage /32 côté ISP

📷 Capture : `screenshots/nat_static.png`

---

### 3️⃣ NAT dynamique
- Attribution dynamique depuis un pool d’IP publiques
- Une IP publique par hôte interne
- Illustration de l’épuisement du pool

📷 Capture : `screenshots/nat_dynamic.png`

---

## 🔐 Sécurité et réalisme

Afin de reproduire un comportement Internet réaliste :
- une **ACL côté ISP** bloque les adresses privées sur le WAN,
- le NAT devient indispensable pour toute connectivité externe,
- les IP publiques ne sont pas directement attachées aux interfaces.

📷 Capture : `screenshots/acl_matches.png`

---

## 📁 Structure du dépôt

```
packet-tracer-nat-lab/
├── README.md
├── topology/
│   └── nat_topology.pkt
├── configs/
│   ├── R1_config.txt
│   └── R2_config.txt
├── screenshots/
│   ├── topology.png
│   ├── nat_pat.png
│   ├── nat_static.png
│   ├── nat_dynamic.png
│   └── acl_matches.png
└── docs/
    └── nat_explanation_master.md
```

---

## 🧪 Méthodes de validation

- `show ip nat translations`
- `show ip nat statistics`
- `show access-lists`
- Tests ICMP et HTTP depuis les réseaux interne et externe

Les captures fournies permettent de valider le fonctionnement **sans exécuter Packet Tracer**.

---

## 🛠️ Outils et technologies

- Cisco Packet Tracer
- Cisco IOS
- IPv4
- NAT / ACL / Routage statique

---

## 📚 Références conceptuelles

- RFC 1918 – Address Allocation for Private Internets
- RFC 3022 – Traditional NAT
- Documentation Cisco IOS NAT

---

## 👤 Auteur

**Eric Stephane**  
Master Réseaux / Cybersécurité / IA 

---

## 📄 Licence

Projet académique – usage pédagogique.
