# Matrice de test détaillée

| ID | Test | Description | Résultat attendu |
|----|------|------------|----------------|
| M1 | SSH IT | Accès admin | PASS |
| M2 | SSH USER | Bloqué | FAIL |
| U1 | DNS USER | Résolution | PASS |
| U2 | USER → APP | Accès service | PASS |
| U3 | USER → DMZ | HTTP | PASS |
| U4 | USER → IT | Isolation | FAIL |
| G1 | GUEST → LAN | Isolation | FAIL |
| G2 | GUEST → Internet | NAT | PASS |
| W1 | Internet → DMZ | Web public | PASS |
| DB1 | APP → DB | Autorisé | PASS |
| DB2 | USER → DB | Bloqué | FAIL |