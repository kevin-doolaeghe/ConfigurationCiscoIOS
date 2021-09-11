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
* [Configuration spécifique](#configuration-spécifique)

## > Mode d'exécution utilisateur

* Entrer en mode d'exécution privilégié :
```
enable
```

* Afficher le tableau ARP du périphérique :
```
show arp
```

* Afficher l'heure en vigueur dans le routeur :
```
show clock
```

* Afficher les statistiques des interfaces d'un périphérique :
```
show interfaces
```

* Affiche les informations IP des interfaces d'un périphérique :
```
show {ip|ipv6} interface {brief}
```

* Afficher la table de routage :
```
show {ip|ipv6} route
```

* Afficher les routes extérieures avec les protocole EIGRP :
```
show ip route egp
```

* Afficher les routes extérieures avec les protocole RIP :
```
show ip route rip
```

* Afficher les routes extérieures avec les protocole OSPF :
```
show ip route ospf
```

* Afficher la version du logiciel IOS et les informations sur le matériel :
```
show version
```

## # Mode d'exécution privilégié

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

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

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

```

*  :
```

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

## Configuration spécifique

### DHCP

```
router(config)#ip address excluded-address 1O.4.7.254
router(config)#ip dhcp pool LAN2
router(config)#network 10.4.7.0 255.255.255.0
router(config)#default-router 10.4.7.254
router(config)#dns-server 8.8.8.8
```

### Listes de contrôle d'accès (ACL)

* Configuration d'une règle simple (règles 1 à 99) :
```
router#configure terminal
router(config)#access-list 1 deny 193.48.64.0 0.0.0.255
router(config)#access-list 1 permit any
router(config)#interface fastEthernet1/0
router(config-if)#ip access-group 1 out
router(config-if)#exit
```

* Configuration d'une règle complexe (règles 99 à 199) :
```
router#configure terminal
router(config)#access-list 100 deny tcp 193.48.64.39 0.0.0.0 any eq ftp      
router(config)#access-list 100 permit ip any any
router(config)#interface fastEthernet1/0
router(config-if)#ip access-group 100 out
router(config-if)#exit
```

* Afficher les listes de contrôle d'accès :
```
router(config)#show access-lists
```

### NAT

```
router(config)#ip nat [inside|outside]
router(config)#show ip nat [translations|statistics]
```

* Réaliser une translation d'IP (NAT statique) et non une mascarade (NAT dynamique) :
```
router(config)#ip nat inside source static network 100.64.0.16 193.48.57.176 /28
```

* Associer des interfaces/VLAN au protocole NAT :
```
router(config)#interface vlan 131
router(config-if)#ip nat outside
router(config-if)#exit
router(config)#interface vlan 333
router(config-if)#ip nat inside
router(config-if)#exit
```

### Telnet

```
router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
router(config)#enable secret cisco
router(config)#line vty 0 15
router(config-line)#password cisco
router(config-line)#exit
```

### Secure Shell (SSH)

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

### VLAN et tronçons

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

### Configuration IP

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

## Exemple de configuration

```
router>enable
```

```
router#configure terminale
```

* Changement du nom du périphérique :
```
router(config)#hostname router
```

* Configuration de l'accès SSH :
```
router(config)#aaa new-model
router(config)#username admin privilege 15 secret cisco
router(config)#ip domain-name cisco.com
router(config)#crypto key generate rsa
router(config)#ip ssh version 2
router(config)#line vty 0 15
router(config-line)#login local
router(config-line)#transport input ssh
router(config-line)#exit
```

* Configuration de l'accès console :
```
router(config)#line console 0
router(config-line)#password cisco
router(config-line)#login
router(config-line)#exit
```

* Configuration de l'accès par mot de passe :
```
router(config)#service password-encryption
router(config)#enable secret cisco
router(config)#banner motd #Restricted access#
```

* Création du VLAN n°2 :
```
router(config)#vlan 2
router(config-if)#name vlan2
router(config-if)#exit
```

* Autorisation des trames du VLAN n°2 sur l'interface :
```
switch(config)#interface g0/1
switch(config-if)#switchport
switch(config-if)#switchport mode access
switch(config-if)#switchport access vlan 2
switch(config-if)#exit
```

* Création d'un tronçon (protocole 802.1Q) :
```
switch(config)#interface fastEthernet0/1
switch(config-if)#switchport trunk encapsulation dot1q
switch(config-if)#switchport mode trunk
switch(config-if)#exit
```

* Configuration IP d'une interface :
```
router(config)#interface g0/1
router(config-if)#ip address 192.168.0.1 255.255.255.0
router(config-if)#exit
```

* Configuration IP d'un VLAN :
```
router(config)#interface vlan2
router(config-if)#ip address 192.168.0.10 /24
router(config-if)#no shutdown
router(config-if)#exit
```

* Activation du routage :
```
router(config)#ip routing
router(config)#exit
router#show ip route
router#configure terminal
```

* 
```
router(config)#interface g0/1.2
router(config-subif)#encapsulation dot1Q 2
router(config-subif)#ip address 192.168.2.1 255.255.255.0
router(config-subif)#exit
router(config)#exit
```

* 
```
router(config)#interface vlan2
router(config-if)#ip address 192.168.2.1 255.255.255.0
router(config-if)#exit
router(config)#exit
```

```
router(config)#copy running-config startup-config
```








```
enable
	configure terminal
		hostname router13
		username admin privilege 15 secret glopglop
		ip domain-name deule.net
		crypto key generate rsa
		ip ssh version 2
		line vty 0 15
			login local
			transport input ssh
			exit
		line console 0
			password glopglop
			login
			exit
		service password-encryption
		enable secret glopglop
		banner motd #Restricted access#
		vlan 1
			name service
			exit
		interface vlan 1
			ip address 172.26.1.58 /30
			no shutdown
		vlan 2
			name filaire1
			exit
		interface vlan 2
			ip address 172.26.1.38 /29
			no shutdown
			exit
		interface g0/1/0
			switchport mode access
			switchport access vlan 2
			no shutdown
			exit
		interface g0/1/2
			switchport mode access
			switchport access vlan 2
			no shutdown
			exit
		vlan 3
			name filaire2
			exit
		interface vlan 3
			ip address 172.26.1.46 /29
			no shutdown
			exit
		interface g0/1/1
			switchport mode access
			switchport access vlan 3
			no shutdown
			exit
		vlan 4
			name wifi1
			exit
		interface vlan 4
			ip address 172.26.1.50 /30
			no shutdown
			exit
		vlan 5
			name wifi2
			exit
		interface vlan 5
			ip address 172.26.1.54 /30
			no shutdown
			exit
		interface g0/1/3
			switchport mode trunk
			switchport trunk allowed vlan 4,5
			no shutdown
			exit
		ip dhcp pool groupea
			network 172.26.1.48 /30
			dns-server 193.48.57.48
			default-router 172.26.1.50
			exit
		ip dhcp pool groupeb
			network 172.26.1.52 /30
			dns-server 193.48.57.48
			default-router 172.26.1.54
			exit
		ip dhcp excluded-address 172.26.1.50
		ip dhcp excluded-address 172.26.1.54
		ip route 0.0.0.0 0.0.0.0 192.168.222.33
		interface g0/0/0
			ip address 192.168.222.43 /28
			no shutdown
			exit
		router rip
			version 2
			no auto-summary
			network 192.168.222.32
			network 172.26.1.32
			exit
 
		int g0/0/0
			no ip address
			exit
		int g0/0/0.132
			encapsulation dot1q 132
			ip address 192.168.222.43 255.255.255.240
			no shutdown
			exit
		int g0/0/0.20
			encapsulation dot1q 20
			ip address 192.168.1.110 255.255.255.0
			no shutdown
			exit
		no ip route 192.168.222.33
		ip route 192.168.1.253
		exit
	copy running-config startup-config
```
