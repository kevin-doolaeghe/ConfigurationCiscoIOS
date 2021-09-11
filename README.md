# Aide à la configuration de routeurs/commutateurs sous Cisco IOS

## Auteur

Kevin Doolaeghe

## Sources

* [Cours de X Redon](https://rex.plil.fr/)
* [Cours de S. Flament](http://btsirisinfo.free.fr/)

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
| `show ip route egp` | Afficher les routes extérieures avec les protocole EGP |
| `show ip route rip` | Afficher les routes extérieures avec les protocole RIP |
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
| `show ip nat [translations|statistics]` | Afficher les informations NAT |
| `show vlan` | Afficher les VLANs créés |
| `show interface trunk` | Afficher les interfaces `dot1q` |

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
| `description LAN2` | Définir la description de l'interface |
| `clock rate 56000` | Définir la fréquence de l'horloge pour un périphérique de type ETCD |
| `no shutdown` | Activer l'interface |

## DHCP

```
ip address excluded-address 1O.4.7.254
ip dhcp pool LAN7
network 10.4.7.0 255.255.255.0
default-router 10.4.7.254
dns-server 8.8.8.8
```

## Listes de contrôle d'accès (ACL)

* Configuration d'une règle simple (règles 1 à 99) :
```
RG20-7202#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
RG20-7202(config)#access-list 1 deny 193.48.64.0 0.0.0.255
RG20-7202(config)#access-list 1 permit any
RG20-7202(config)#interface fastEthernet1/0
RG20-7202(config-if)#ip access-group 1 out
RG20-7202(config-if)#exit
```

* Configuration d'une règle complexe (règles 99 à 199) :
```
RG20-7202#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
RG20-7202(config)#access-list 100 deny tcp 193.48.64.39 0.0.0.0 any eq ftp      
RG20-7202(config)#access-list 100 permit ip any any
RG20-7202(config)#interface fastEthernet1/0
RG20-7202(config-if)#ip access-group 100 out
RG20-7202(config-if)#exit
```

* Afficher les listes de contrôle d'accès :
```
show access-lists
```

## NAT

```
ip nat [inside|outside]
show ip nat [translations|statistics]
```

* Réaliser une translation d'IP (NAT statique) et non une mascarade (NAT dynamique) :
```
ip nat inside source static network 100.64.0.16 193.48.57.176 /28
```

* Associer des interfaces/VLAN au protocole NAT :
```
int vlan 131
  ip nat outside
  exit
int  vlan 333
  ip nat inside
  exit
```

## Telnet

```
router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
router(config)#enable secret cisco
router(config)#line vty 0 15
router(config-line)#password cisco
router(config-line)#exit
```

## Secure Shell (SSH)

```
router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
router(config)#hostname router
router(config)#aaa new-model
router(config)#username admin privilege 15 secret cisco
router(config)#ip domain-name cisco.com
router(config)#crypto key generate rsa
router(config)#line vty 0 15
router(config-line)#transport input ssh
router(config-line)#exit
```

## VLAN et tronçons

* Configuration d'un VLAN :
```
switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
switch(config)#vlan 2
switch(config-vlan)#name Principal
switch(config-vlan)#exit
```

* Affecter un VLAN à une interface :
```
switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
switch(config)#interface gigabitEthernet0/7
switch(config-if)#switchport
switch(config-if)#switchport mode access
switch(config-if)#switchport access vlan 2
switch(config-if)#exit
```

* Création d'un tronçon (802.1Q)
```
switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
switch(config)#interface fastEthernet0/1
switch(config-if)#switchport trunk encapsulation dot1q
switch(config-if)#switchport mode trunk
switch(config-if)#exit
```

* Configuration d'un tronçon sur une sous-interface :
```
router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
router(config)#interface GigabitEthernet0/1.2
router(config-subif)#encapsulation dot1Q 2
router(config-subif)#ip address 192.168.2.1 255.255.255.0
router(config-subif)#exit
router(config)#exit
```

* Configuration d'un tronçon sur un VLAN :
```
router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
router(config)#interface Vlan2
router(config-if)#ip address 192.168.2.1 255.255.255.0
router(config-if)#exit
router(config)#exit
```

## Configuration IP

* Configuration IPv4 sur une interface :
```
router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
router(config)#interface GigabitEthernet0/1
router(config-if)#ip address 192.168.0.1 255.255.255.0
router(config-if)#exit
router(config)#exit
```

* Configuration IPv4 sur les VLAN :
```
router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
router(config)#interface Vlan1
router(config-if)#ip address 192.168.0.10 255.255.255.0
router(config-if)#exit
router(config)#exit
```

* Activer le routage :
```
router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
router(config)#ip routing
router(config)#exit
router#show ip route
```
