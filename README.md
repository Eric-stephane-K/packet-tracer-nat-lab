# 🔐 Architecture Réseau Sécurisée avec ACL, NAT, DMZ et Micro-segmentation (Cisco Packet Tracer)

## 📌 Présentation du projet

Ce projet consiste en la conception et l’implémentation d’une architecture réseau sécurisée simulant une PME, réalisée avec Cisco Packet Tracer.

L’objectif est de démontrer des compétences pratiques en cybersécurité réseau à travers :
- la segmentation réseau par VLAN
- l’application de politiques de contrôle d’accès (ACL)
- la mise en place d’une DMZ
- l’utilisation de NAT (PAT et NAT statique)
- l’isolation d’une base de données (micro-segmentation)
- la validation par des tests techniques réels

---

## 🧠 Objectifs de sécurité

L’architecture a été conçue pour respecter les principes suivants :

- 🔒 Principe du moindre privilège
- 🧱 Segmentation des zones réseau
- 🌐 Exposition contrôlée des services publics
- 🚫 Isolation des réseaux sensibles
- 🔄 Validation par des preuves techniques (ACL hits, NAT, tests)

---

## 🏗️ Architecture du réseau

### Segmentation par VLAN

| Zone | VLAN | Réseau |
|------|------|--------|
| USERS | 10 | 192.168.10.0/24 |
| IT | 20 | 192.168.20.0/24 |
| SERVERS | 30 | 192.168.30.0/24 |
| GUEST | 40 | 192.168.40.0/24 |
| DMZ | - | 192.168.50.0/24 |
| DATABASE | 60 | 192.168.60.0/24 |
| WAN | - | 203.0.113.0/30 |
| Internet simulé | - | 8.8.8.0/24 |

---

## 🔐 Contrôles de sécurité implémentés

### 1. Accès administrateur sécurisé
- Accès SSH autorisé uniquement depuis le VLAN IT

---

### 2. Segmentation des utilisateurs (ACL USERS)
- Autorisation vers :
  - DNS interne
  - serveur applicatif
  - serveur web DMZ
- Interdiction d’accès au VLAN IT

---

### 3. Isolation du réseau invité (ACL GUEST)
- Accès Internet autorisé
- Accès aux réseaux internes bloé
- Accès à la gateway explicitement autorisé

---

### 4. Publication DMZ (NAT statique)
- Serveur web accessible depuis Internet via :
  - `http://203.0.113.2`
- Filtrage WAN avec ACL

---

### 5. NAT dynamique (PAT)
- Accès Internet pour USERS, IT et GUEST

---

### 6. Micro-segmentation base de données
- VLAN dédié (VLAN 60)
- Accès autorisé uniquement depuis le serveur applicatif
- Blocage de tous les autres accès

---

## 🧪 Validation technique

Les contrôles ont été validés à travers :

- tests de connectivité (ping, telnet, HTTP)
- vérification des ACL via les compteurs (match)
- analyse des translations NAT

---

## 📊 Résultats clés

| Test | Résultat |
|------|--------|
| IT → SSH routeur | ✅ |
| USERS → IT | ❌ |
| USERS → DMZ Web | ✅ |
| GUEST → interne | ❌ |
| GUEST → Internet | ✅ |
| Internet → DMZ | ✅ |
| APP → DB | ✅ |
| USER → DB | ❌ |

---

## 📸 Captures d’écran

Les preuves sont disponibles dans :

<<<<<<< HEAD
```text
docs/screenshots/
=======
---

## 👤 Auteur

**Eric Stephane**  
Master Réseaux / Cybersécurité / IA 

---

## 📄 Licence

Projet Personnel – usage pédagogique.
>>>>>>> ced3fe11bb8eb4e1f8875882e50111d61202d982
