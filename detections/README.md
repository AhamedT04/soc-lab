# Règles de détection personnalisées

Règles Wazuh écrites pendant les scénarios. Elles vont dans `/var/ossec/etc/rules/local_rules.xml` du manager (conteneur `wazuh.manager`).

Plage d'ID utilisée : 100100 – 100199.

| ID | Scénario | Description |
|----|----------|-------------|
| 100100 | 01 | Paquet bloqué par le pare-feu Windows (5152/5157), niveau 2 (sous le seuil d'alerte), base de corrélation |
| 100101 | 01 | Scan de ports probable : 20+ paquets bloqués depuis la même IP en 10 s (T1046) |
