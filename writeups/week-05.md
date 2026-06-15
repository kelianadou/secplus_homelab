## Théorie 3.3 — Data Protection

- 3 états des données : at rest (chiffrement disque, LUKS/BitLocker), in transit
  (TLS/VPN), in use (enclaves sécurisées, Intel SGX, HSM)
- Data classifications : Public, Sensitive, Confidential, Critical, Private, Restricted
- Data types réglementés : PII (Personally Identifiable Information),
  PHI (Protected Health Information, régi par HIPAA), Financial (PCI-DSS), IP
- Data sovereignty : les données sont soumises aux lois du pays où elles sont stockées (ex : RGPD)
- Méthodes de protection : encryption (réversible), hashing (irréversible),
  masking (1234-XXXX-XXXX-5678), tokenization (token vers vraie donnée en coffre),
  obfuscation, segmentation, permissions

## Théorie 3.4 — Resilience

- High Availability mesurée en % (99.9% = 8h indispo/an, 99.999% = 5 min/an)
- Redundancy : geographic dispersion, power redundancy, load balancing
- Backups : Full (lourd, restauration simple), Incremental (rapide, restauration longue),
  Differential (compromis), Snapshot (instantané)
- Règle 3-2-1 : 3 copies sur 2 supports différents dont 1 hors site
- Metrics : RTO (temps d'indisponibilité acceptable), RPO (perte de données en temps
  depuis la dernière sauvegarde), MTTR, MTBF
- Plans : BCP (continuité), DRP (récupération désastre), BIA (impact analysis)
- Sites : Hot (temps réel, minutes), Warm (heures), Cold (jours)

## Théorie 4.1 — Computing resources security

- Secure baselines : establish, deploy, maintain
- Hardening targets : mobile, workstations, switches, routers, cloud, servers,
  ICS/SCADA, embedded, IoT
- Mobile deployment : BYOD (perso), COPE (entreprise + perso autorisé),
  CYOD (choix dans liste validée)
- Wireless : WPA3 > WPA2, EAP-TLS le plus sécurisé (certificats des deux côtés)
- Sandboxing : exécution isolée de code suspect

## Théorie 4.2 — Asset management

- Principe : "tu ne peux pas sécuriser ce que tu ne sais pas que tu possèdes"
- Cycle : Acquisition (supply chain risk), Assignment (ownership, classification),
  Disposal (sanitization, shredding, degaussing inutile sur SSD)
- Inventory hardware + software + data obligatoire

## Théorie 4.3 — Vulnerability management

- Identification : vulnerability scan (OpenVAS, Nessus), SAST (code source),
  DAST (app en exécution, comme DVWA), threat feeds, pentest, bug bounty
- Analysis : false positive/negative, prioritization
- CVE = identifiant unique (ex :
