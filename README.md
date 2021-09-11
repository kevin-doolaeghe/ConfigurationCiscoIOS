# Aide à la configuration de routeurs/commutateurs Cisco IOS

## Sommaire

* [> Mode d'exécution utilisateur](#-mode-dexécution-utilisateur)
* [# Mode d'exécution privilégié](#-mode-dexécution-privilégié)
* [(config)# Mode de configuration globale](#config-mode-de-configuration-globale)
* [(config-line)# Mode de configuration de ligne](#config-line-mode-de-configuration-de-ligne)
* [(config-if)# Mode de configuration d'interface](#config-if-mode-de-configuration-dinterface)

## > Mode d'exécution utilisateur

| Commande | Détail |
|:-------------:|:--------------|
| `enable` | Entrer en mode d'exécution privilégié |
| `show arp` | Afficher le tableau ARP du périphérique |
| `show clock` | Afficher l'heure en vigueur dans le routeur |
| `show interfaces` | Afficher les statistiques des interfaces d'un périphérique |
| `show ip(v6) interface [brief]` | Affiche les informations IP des interfaces d'un périphérique |
| `show ip(v6) route` | Afficher la table de routage |
| `show version` | Afficher la version du logiciel IOS et les informations sur le matériel |

## # Mode d'exécution privilégié

| Commande | Détail |
|:-------------:|:--------------|
| `configure terminal` | Entrer en mode de configuration globale |
| `copy running-config startup-config` | Sauvegarder la configuration active en mémoire NVRAM |
| `erase startup-config` | Effacer la configuration stockée en mémoire NVRAM |
| `ping 8.8.8.8` | Envoyer une requête `ping` à l'adresse spécifiée |
| `traceroute 192.168.1.254` | Suivre chaque saut jusqu'à l'adresse spécifiée |
| `show startup-config` | Afficher la configuration stockée en NVRAM |
| `show running-config` | Afficher le contenu du fichier de configuration en cours d'exécution |
| `show ip nat...` | Afficher les informations NAT selon l'option (translations, statistics) |

## (config)# Mode de configuration globale

| Commande | Détail |
|:-------------:|:--------------|
| `hostname routeur1` | Attibuer un nom d'hôte au périphérique |
| `enable password cisco` | Définir un mot de passe actif non chiffré |
| `enable secret cisco` | Définir un mot de passe actif utilisant un chiffrement fort |
| `service password-encryption` | Activer le chiffage des mots de passe de type `password` |
| `banner motd # Warning !! Restricted Access #` | Configurer une bannière contenant un message du jour |
| `line console 0` | Entrer en mode de configuration de ligne de console |
| `line vty 0 15` | Entrer en mode de configuration de ligne de terminal virtuel (`telnet`, `ssh`) |
| `interface g0/0` | Entrer en mode de configuration d'interface (`g0/0`, `f0/0`, `s0/0/0`, `vlan1`..) |
| `ip route 7.7.0.0 255.255.255.0 4.4.5.8` | Créer une route vers le réseau `7.7.0.0` en passant par `4.4.5.8` |
| `ip route 7.7.0.0 255.255.255.0 s0/0/1` | Créer une route vers le réseau `7.7.0.0` en sortant par `s0/0/0` |
| `ip default-gateway 10.10.1.1` | Configurer la passerelle par défaut d'un équipement |
| `ipv6 route 2001:db8:acad:2::/64 s0/0/0 fe80::2` | Créer une route vers le réseau en sortant par `s0/0/0` |
| `ipv6 unicast-routing` | Activer le routage IPv6 |

## (config-line)# Mode de configuration de ligne

| Commande | Détail |
|:-------------:|:--------------|
| `password cisco` | Définir un mot de passe de ligne |
| `login` | Activer le contrôle d'accès par mot de pase à l'ouverture de la session |

## (config-if)# Mode de configuration d'interface

| Commande | Détail |
|:-------------:|:--------------|
| `ip address 192.168.0.5 255.255.255.0` | Définir la configuration IPv4 de l'interface |
| `ipv6 address fe80::1 link-local` | Définir l'adresse IPv6 de lien local |
| `ipv6 address 2001:db8:acad::1/64` | Définir l'adresse IPv6 de monodiffusion globale |
| `description lan2` | Définir la description de l'interface |
| `clock rate 56000` | Définir la fréquence de l'horloge pour un périphérique de type ETCD |
| `no shutdown` | Activer l'interface |
