# Architecture du lab

## Matériel

- Lenovo ThinkPad T14 Gen 3 — Intel i7-1255U, 32 Go RAM
- OS hôte : Ubuntu 26.04.1 LTS

## Composants

| Composant | Rôle | Ressources | Réseau |
|-----------|------|------------|--------|
| Wazuh 4.14.7 (Docker, single-node) | SIEM : manager, indexer, dashboard | 3 conteneurs | Bridge Docker 172.18.0.1 |
| Kali Linux 2026.2 | Attaquant | 2 vCPU, 4 Go, 40 Go | NAT libvirt (virbr0, 192.168.122.0/24) |
| Windows 11 Enterprise (éval.) | Victime | 4 vCPU, 8 Go, 60 Go, TPM émulé | NAT libvirt |

Dashboard Wazuh : `https://localhost:443` depuis l'hôte.
Les agents des VMs joignent le manager via la passerelle `192.168.122.1`.

## Choix techniques

- **Wazuh plutôt que Security Onion** : plus léger, tourne en Docker sur l'hôte, couvre HIDS + SIEM + intégrité de fichiers.
- **KVM plutôt que VirtualBox** : natif au noyau Linux, meilleures performances.
- **Une seule machine** : tout le cycle attaque → détection → analyse est reproductible localement.

## Problèmes rencontrés

| Problème | Cause | Solution |
|----------|-------|----------|
| Agents refusés par le manager | Agents 4.14.7, manager 4.12.0 (« Agent version must be lower or equal to manager version ») | Redéploiement de wazuh-docker sur la branche v4.14.7 |
| Copier-coller impossible hôte ↔ Windows | SPICE guest tools inopérants | Transfert via `python3 -m http.server` temporaire sur l'hôte |
| `qemu-kvm` introuvable sur Ubuntu 26.04 | Paquet virtuel | Installation de `qemu-system-x86` |

## Adresses IP

<!-- À compléter : IP des VMs (`ip a` sur Kali, `ipconfig` sur Windows) -->
| Machine | IP |
|---------|----|
| Hôte (virbr0) | 192.168.122.1 |
| Kali | |
| Windows 11 | |
