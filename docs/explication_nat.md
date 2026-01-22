# Network Address Translation (NAT)
## Analyse théorique et implémentation pratique sous Cisco Packet Tracer (Niveau Master)

---

## 1. Introduction

Le **Network Address Translation (NAT)** est un mécanisme fondamental des réseaux IP modernes, conçu initialement pour pallier la pénurie d’adresses IPv4 et renforcer la séparation entre réseaux privés et réseaux publics.  
Malgré l’émergence d’IPv6, le NAT reste **massivement déployé** dans les infrastructures d’entreprise, les réseaux d’accès Internet et les environnements cloud.

Ce document présente :
- une **analyse conceptuelle approfondie** du NAT,
- une **implémentation pratique** sous Cisco Packet Tracer,
- une **comparaison critique** des différentes formes de NAT.

Le travail s’inscrit dans une démarche académique de niveau **Master en réseaux et cybersécurité**.

---

## 2. Problématique de l’adressage IPv4

### 2.1 Adresses privées et routabilité

Les plages d’adresses privées définies par la RFC 1918 :
- 10.0.0.0/8  
- 172.16.0.0/12  
- 192.168.0.0/16  

ne sont **pas routables sur Internet**.  
Toute tentative de communication directe entre un hôte privé et un réseau public nécessite un mécanisme intermédiaire.

### 2.2 Rôle du NAT

Le NAT permet :
- la **traduction d’adresses IP** (et éventuellement de ports),
- l’**économie d’adresses IPv4 publiques**,
- une **forme de cloisonnement logique** entre réseau interne et externe.

Il ne constitue toutefois **pas un mécanisme de sécurité à part entière**, mais plutôt un effet secondaire de masquage.

---

## 3. Environnement expérimental

### 3.1 Topologie du laboratoire

Le laboratoire comprend :
- un routeur d’entreprise (R1),
- un routeur fournisseur d’accès (R2),
- un réseau LAN interne,
- un réseau Internet simulé,
- plusieurs hôtes internes,
- un serveur Web interne.

### 3.2 Plan d’adressage

- LAN : 192.168.10.0/24  
- WAN (R1–R2) : 203.0.113.0/30  
- Internet simulé : 198.51.100.0/24  

Une **ACL côté ISP** bloque explicitement les adresses privées sur le lien WAN afin de reproduire le comportement réel d’Internet.

---

## 4. Implémentations du NAT

### 4.1 NAT Overload (PAT)

#### Principe

Le **Port Address Translation (PAT)** permet à plusieurs hôtes internes de partager une **unique adresse IP publique** en différenciant les flux par les numéros de ports.

#### Analyse technique

- Traduction IP + port source
- Création de *translations étendues*
- Forte dépendance à la table NAT

#### Avantages

- Scalabilité élevée
- Consommation minimale d’IP publiques
- Déploiement quasi universel

#### Limites

- Complexité accrue pour les connexions entrantes
- Problèmes potentiels avec certains protocoles non NAT-friendly

---

### 4.2 NAT statique

#### Principe

Le NAT statique établit une correspondance **permanente et univoque** entre une adresse IP privée et une adresse IP publique.

Dans ce projet :
- Serveur interne : 192.168.10.100
- IP publique : 203.0.113.100

#### Approche réaliste

L’adresse publique n’est **pas assignée à une interface physique**, mais représentée par :
- une **interface loopback**,
- une route statique /32 côté ISP.

Cette approche reflète fidèlement les scénarios de délégation d’adresses IP publiques par les fournisseurs d’accès.

#### Enjeux de sécurité

- Exposition directe du service
- Nécessité de mécanismes complémentaires (ACL, firewall, IDS/IPS)

---

### 4.3 NAT dynamique

#### Principe

Le NAT dynamique repose sur un **pool d’adresses IP publiques** attribuées dynamiquement aux hôtes internes.

#### Observation expérimentale

Le laboratoire met en évidence :
- l’allocation temporaire des IP publiques,
- l’épuisement du pool,
- le refus de nouvelles connexions lorsque le pool est saturé.

Ce comportement démontre une **limite structurelle** du NAT dynamique.

#### Analyse critique

Bien que plus traçable que le PAT, le NAT dynamique :
- dépend fortement de la taille du pool,
- est aujourd’hui peu utilisé dans les réseaux modernes.

---

## 5. Comparaison synthétique

| Type de NAT | Traduction des ports | Consommation IP | Cas d’usage |
|------------|----------------------|-----------------|-------------|
| PAT | Oui | Très faible | Accès Internet |
| Statique | Non | Élevée | Publication de services |
| Dynamique | Non | Moyenne | Accès contrôlé |

---

## 6. Réalisme et bonnes pratiques

Afin d’assurer un laboratoire représentatif :
- filtrage des adresses privées côté ISP,
- séparation stricte des rôles NAT / routage,
- utilisation d’IP publiques routées via loopback.

Ces choix permettent d’éviter les simplifications excessives souvent observées dans les environnements simulés.

---

## 7. Conclusion

Ce projet met en évidence :
- l’importance historique et actuelle du NAT,
- les compromis entre économie d’adresses et flexibilité,
- la prédominance du PAT dans les architectures modernes.

Malgré IPv6, le NAT reste un **élément structurant des réseaux IP contemporains**, tant pour des raisons techniques qu’économiques.

---

## 8. Outils utilisés

- Cisco Packet Tracer  
- Cisco IOS  

---

## 9. Auteur

Eric Stephane  
Programme de Master – Réseaux / Cybersécurité
