# SOC Lab – Centre d'opérations de sécurité maison

Lab de détection construit de zéro sur une seule machine physique : une VM attaquante, une VM victime et un SIEM qui surveille le tout. L'objectif est de reproduire le travail d'un analyste SOC de bout en bout : simuler une attaque, la détecter, l'investiguer et documenter la réponse.

## Architecture

```
ThinkPad T14 Gen 3 (i7-1255U, 32 Go) — Ubuntu 26.04 LTS
├── Docker → Wazuh 4.14.7 (manager, indexer, dashboard)
└── KVM / libvirt (réseau NAT 192.168.122.0/24)
    ├── Kali Linux 2026.2  — attaquant  (agent Wazuh)
    └── Windows 11 Ent.    — victime    (agent Wazuh)
```

Détails : [docs/architecture.md](docs/architecture.md)

## Scénarios

| # | Scénario | Technique MITRE ATT&CK | Statut |
|---|----------|------------------------|--------|
| 00 | [Validation de la télémétrie Sysmon et analyse d'un faux positif](scenarios/00-validation-telemetrie.md) | — | Terminé |
| 01 | [Reconnaissance réseau (nmap)](scenarios/01-reconnaissance-nmap.md) | T1046 | Terminé |
| 02 | Brute force RDP/SMB | T1110 | À faire |
| 03 | Persistance (tâche planifiée / clé Run) | T1053 / T1547 | À faire |

Chaque scénario suit le même format : contexte, exécution de l'attaque, détection, investigation, réponse, leçons apprises. Voir [scenarios/](scenarios/).

## Règles de détection

Règles Wazuh personnalisées écrites pendant les scénarios : [detections/](detections/)

## Compétences démontrées

- Déploiement et administration d'un SIEM (Wazuh) en conteneurs
- Virtualisation (KVM/libvirt), réseau isolé
- Simulation d'attaques et cartographie MITRE ATT&CK
- Écriture de règles de détection et analyse de journaux Windows/Linux
- Documentation d'incidents
