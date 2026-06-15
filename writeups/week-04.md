## Théorie 3.1 — Architecture and Infrastructure Concepts

- Cloud vs On-premises vs Hybrid : contrôle total vs flexibilité vs combinaison
- Network segmentation : diviser en zones de confiance différentes (LAN = interne, DMZ = services exposés, réseau isolé = tests offensifs)
- DMZ (Demilitarized Zone) : zone tampon entre Internet et LAN. Si la DMZ est compromise, le LAN reste protégé.
- Defense in depth : multiplier les couches de sécurité
- Jump server (bastion host) : point de contrôle unique pour accéder aux zones sensibles
- Air gap : isolation physique totale. Protège contre les attaques réseau mais pas contre les vecteurs physiques (ex : Stuxnet via clé USB)
- Zero Trust : never trust, always verify — même à l'intérieur du réseau segmenté

## Théorie 3.2 — Secure Infrastructure

- Firewall stateful vs stateless vs NGFW
  Stateful : suit l'état des connexions (le plus courant)
  Stateless : filtre paquet par paquet sans contexte
  NGFW : stateful + inspection applicative layer 7 + IDS/IPS intégré
- IDS vs IPS :
  IDS = détecte et alerte (passif). Ex : Suricata en mode écoute.
  IPS = détecte et bloque automatiquement (actif). Ex : Suricata en mode inline.
  HIDS = surveille un hôte. NIDS = surveille le trafic réseau.
- Honeypot : système leurre pour attirer et étudier les attaquants
  Honeynet : réseau de honeypots
  Honeyfile : fichier leurre — si accédé = alerte immédiate
  Honeytoken : donnée leurre (credential, token) — si utilisée = vol confirmé
- Load balancer : distribue le trafic, garantit la disponibilité (Availability CIA)
- Proxy forward : protège les clients. Proxy reverse : protège les serveurs.
- SIEM : centralise et corrèle les logs. Dans le lab = Wazuh (W6).

## Lab W4

- Suricata installé sur pfSense via Package Manager
- Interface LAN configurée en mode IDS (Block Offenders désactivé)
- Règles ET Open téléchargées et activées (attack_response, botcc, compromised,dos, exploit, malware, scan, sql, web_server)
- Problème : Suricata ne démarre pas (processus absent après start)
  Cause probable : conflit de configuration ou règle mal formatée
  Action : à déboguer à la prochaine session avec logs détaillés
- Note : le trafic intra-LAN entre VMs sur le même réseau VirtualBox ne passe pas forcément par l'interface pfSense — limitation architecturale à résoudre via configuration de monitoring dédié
- 7 juin : Débogage approfondi Suricata
  Cause racine identifiée : règles ET téléchargées (emerging.rules.tar.gz présent dans /usr/local/etc/suricata/) mais jamais extraites vers les dossiers des interfaces
  Conséquence : service actif mais aucune règle chargée en mémoire → impossible de générer des alertes
  Action prévue : forcer l'extraction manuelle des règles à la prochaine session
