
**Auteur :** Erwann GIRAULT (CUPGE Cyber / ENSSAT) et 2 autres camarades anonymisés
**Objectif :** Conception et déploiement d'une infrastructure de deux sites en miroir.

* ✅ **Administration Réseau :** Configuration avancée Cisco (IOS, VLANs, Trunking, OSPF), Gestion de la congestion et Qualité de Service (QoS).
* ✅ **Cybersécurité :** Durcissement des accès (Port Security, 802.1X), Filtrage (ACLs), Segmentation.
* ✅ **Système :** Administration Linux Debian (Bind9, Apache2, ISC-DHCP, ProFTPD).

---

**Résumé du projet**

Ce projet porte sur le déploiement d'une architecture réseau interconnectant deux sites distants. L'objectif est d'assurer la disponibilité des services (Web, DNS, Vidéo) tout en garantissant une ségrégation des flux publics et privés.

L'architecture repose sur les point techniques suivants :

* **Routage & Segmentation :** Utilisation du protocole **OSPF Multi-Area** (Backbone Area 0 / LAN Area 31 & 32) et séparation physique des switchs (Switch Public vs Privé).
* **Contrôle d'Accès :** Implémentation de **802.1X via FreeRADIUS**. Aucun accès physique au réseau privé n'est possible sans une authentification valide du *supplicant*.
* **Sécurité :** Centralisation du filtrage (via **ACLs étendues**) sur le routeur interne et masquage du plan d'adressage du réseau privé via **NAT/PAT**.
* **Continuité de Service (QoS) :** Mise en place de files d'attente prioritaires pour le flux vidéo RTP, garantissant la fluidité du service même en cas de saturation du lien WAN.

Cependant, l'analyse de l'infrastructure déployée révèle deux axes d'amélioration majeurs pour un passage en production :

* **Confidentialité :** L'administration actuelle repose sur des protocoles en clair (FTP, HTTP) vulnérables au *sniffing* et aux attaques *Man-in-the-Middle*. **Solution :** Migration vers des protocoles chiffrés (SFTP, HTTPS).
* **Résilience :** Le lien WAN unique constitue un point de défaillance unique ; sa perte entraîne l'isolement total du site. **Solution :** Ajout de redondance au niveau des routeurs de bordure.
