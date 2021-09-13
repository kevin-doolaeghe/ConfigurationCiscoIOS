# Aide à la configuration de routeurs/commutateurs sous Cisco IOS

## Auteur

Kevin Doolaeghe

## Sources

* [Cours de X. Redon](https://rex.plil.fr/)
* [Cours de S. Flament](http://btsirisinfo.free.fr/)

## Sommaire

* [Commandes de base](#commandes-de-base)
  * [> Mode d'exécution utilisateur](#-mode-dexécution-utilisateur)
  * [# Mode d'exécution privilégié](#-mode-dexécution-privilégié)
  * [(config)# Mode de configuration globale](#config-mode-de-configuration-globale)
  * [(config-line)# Mode de configuration de ligne](#config-line-mode-de-configuration-de-ligne)
  * [(config-if)# Mode de configuration d'interface](#config-if-mode-de-configuration-dinterface)
  * [Commandes `show`](#commandes-show)
* [Configuration d'un routeur](#configuration-dun-routeur)
* [Configuration d'un commutateur](#)
* [Configuration spécifique](#configuration-spécifique)
  * [DHCP](#protocole-dhcp)
  * [ACT](#listes-de-contrôle-daccès-acl)
  * [NAT](#nat)
  * [Telnet](#telnet)
  * [SSH](#secure-shell-ssh)
  * [VLAN/Trunk](#vlan-et-tronçons)
  * [Configuration IP](#configuration-ip)
  * [Routage RIP](#configuration-du-routage-rip)
  * [Routage OSPF](#configuration-du-routage-ospf)
* [Exemple de configuration](#exemple-de-configuration)

## Commandes de base

### > Mode d'exécution utilisateur

* Entrer en mode d'exécution privilégié :
```
router>enable
```

### # Mode d'exécution privilégié

* Entrer en mode de configuration globale :
```
router#configure terminal
```

* Sauvegarder la configuration active en mémoire NVRAM :
```
router#copy running-config startup-config
```

* Effacer la configuration stockée en mémoire NVRAM :
```
router#erase startup-config
```

* Envoyer une requête `ping` à l'adresse spécifiée :
```
router#ping {ip-address}
```

* Suivre chaque saut jusqu'à l'adresse spécifiée :
```
router#traceroute {ip-address}
```

### (config)# Mode de configuration globale

* Changer le nom d'hôte du périphérique :
```
router(config)#hostname {hostname}
```

* Créer une route :
```
router(config)#{ip|ipv6} route {network-address} {subnet-mask} {ip-address|exit-intf}
```

* Configurer une route IPv4 par défaut :
```
router(config)#ip route 0.0.0.0 0.0.0.0 {ip-address|exit-intf}
```

* Configurer une route IPv6 par défaut :
```
router(config)#ipv6 route :: /0 {ipv6-address|exit-intf}
```

* Définir un mot de passe actif non chiffré :
```
router(config)#enable password {password}
```

* Définir un mot de passe actif utilisant un chiffrement fort :
```
router(config)#enable secret {password}
```

* Activer le chiffrement des mots de passe de type `password` :
```
router(config)#service password-encryption
```

* Configurer une bannière contenant un message du jour :
```
router(config)#banner motd # Restricted Access #
```

* Entrer en mode de configuration de ligne de console :
```
router(config)#line console 0
```

* Entrer en mode de configuration de ligne de terminal virtuel (`telnet`, `ssh`) :
```
router(config)#line vty 0 15
```

* Entrer en mode de configuration d'interface (`g0/0`, `f0/0`, `s0/0/0`,`loopback`, `vlan1`..) :
```
router(config)#interface {intf}
```

### (config-if)# Mode de configuration d'interface

* Définir la configuration IPv4 de l'interface :
```
router(config-if)#ip address {network-address} {subnet-mask}
```

* Définir l'adresse IPv6 de lien local :
```
router(config-if)#ipv6 address fe80::1 link-local
```

* Définir l'adresse IPv6 de monodiffusion globale :
```
router(config-if)#ipv6 address 2001:db8:acad::1/64
```

* Définir la description de l'interface :
```
router(config-if)#description {description}
```

* Définir la fréquence de l'horloge pour un périphérique de type ETCD :
```
router(config-if)#clock rate 56000
```

* Activer l'interface :
```
router(config-if)#no shutdown
```

### (config-line)# Mode de configuration de ligne

* Définir un mot de passe de ligne :
```
router(config-line)#password {password}
```

* Activer le contrôle d'accès par mot de pase à l'ouverture de la session :
```
router(config-line)#login
```

### Commandes `show`

* Afficher la configuration stockée en NVRAM :
```
router#show startup-config
```

* Afficher le contenu du fichier de configuration en cours d'exécution :
```
router#show running-config
```

* Afficher la version du logiciel IOS et les informations sur le matériel :
```
router#show version
```

* Afficher l'historiques des commandes exécutées :
```
router#show history
```

* Lister les interfaces :
```
router#show interfaces
```

* Afficher la configuration IP des interfaces du périphérique :
```
router#show {ip|ipv6} interface [brief]
```

* Afficher les routes par défaut, de secours, statiques, internes et externes (EIGRP, OSPF, RIP..) :
```
router#show {ip|ipv6} route [egp|ospf|rip]
```

* Afficher la table d'adresses MAC :
```
router#show mac-address-table
```

* Afficher les configurations NAT :
```
router#show ip nat [translations|statistics]
```

* Afficher les VLAN :
```
router#show vlan
```

* Afficher les tronçons :
```
show interface trunk
```

* Afficher l'état des adresses MAC sécurisées :
```
show port-security address
```

* Afficher les détails des voisins :
```
show cpd neighbors detail
```

* Afficher le tableau ARP du périphérique :
```
show arp
```

* Afficher l'heure en vigueur dans le routeur :
```
show clock
```

## Configuration d'un routeur

* Activer le routage IPv4 :
```
router(config)#ip routing
```

* Activer le routage IPv6 :
```
router(config)#ipv6 unicast-routing
```

## Configuration d'un commutateur

* Configurer une passerelle par défaut :
```
switch(config)#ip default-gateway {ip-address}
```

* Détecter automatiquement le type de câble (droit ou croisé) :
```
switch(config-if)#mdix auto
```

* Négocier automatiquement les paramètres bidirectionnels :
```
switch(config-if)#duplex auto
```

* Négocier automatiquement les paramètres de vitesse :
```
switch(config-if)#speed auto
```

* Activer la sécurité des ports :
```
switch(config-if)#switchport port-security
```

* Activer l'apprentissage rémanent :
```
switch(config-if)#switchport port-security mac-address sticky
```

## Configuration spécifique

### Protocole DHCP
```
router(config)#ip dhcp pool LAN2
router(dhcp-config)#network 10.4.7.0 255.255.255.0
router(dhcp-config)#default-router 10.4.7.254
router(dhcp-config)#dns-server 8.8.8.8
router(dhcp-config)#exit
router(config)#ip address excluded-address 1O.4.7.254
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
router(config)#enable secret cisco
router(config)#line vty 0 15
router(config-line)#password cisco
router(config-line)#exit
```

### Secure Shell (SSH)

```
router#configure terminal
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
switch(config)#vlan 2
switch(config-vlan)#name Principal
switch(config-vlan)#exit
```

* Affecter un VLAN à une interface :
```
switch#configure terminal
switch(config)#interface gigabitEthernet0/7
switch(config-if)#switchport
switch(config-if)#switchport mode access
switch(config-if)#switchport access vlan 2
switch(config-if)#exit
```

* Création d'un tronçon (802.1Q)
```
switch#configure terminal
switch(config)#interface fastEthernet0/1
switch(config-if)#switchport trunk encapsulation dot1q
switch(config-if)#switchport mode trunk
switch(config-if)#exit
```

* Configuration d'un tronçon sur une sous-interface :
```
router#configure terminal
router(config)#interface GigabitEthernet0/1.2
router(config-subif)#encapsulation dot1Q 2
router(config-subif)#ip address 192.168.2.1 255.255.255.0
router(config-subif)#exit
router(config)#exit
```

* Configuration d'un tronçon sur un VLAN :
```
router#configure terminal
router(config)#interface Vlan2
router(config-if)#ip address 192.168.2.1 255.255.255.0
router(config-if)#exit
router(config)#exit
```

### Configuration IP

* Configuration IPv4 sur une interface :
```
router#configure terminal
router(config)#interface GigabitEthernet0/1
router(config-if)#ip address 192.168.0.1 255.255.255.0
router(config-if)#exit
router(config)#exit
```

* Configuration IPv4 sur les VLAN :
```
router#configure terminal
router(config)#interface Vlan1
router(config-if)#ip address 192.168.0.10 255.255.255.0
router(config-if)#exit
router(config)#exit
```

* Activer le routage :
```
router#configure terminal
router(config)#ip routing
router(config)#exit
router#show ip route
```

### Configuration du routage RIP
```
router(config)#router rip
router(config-router)#version 2
router(config-router)#no auto-summary
router(config-router)#network 192.168.222.32
router(config-router)#network 172.26.1.32
router(config-router)#exit
```

### Configuration du routage OSPF
```
router(config)#router ospf 1
router(config-router)#router-id 1.1.1.1
router(config-router)#network 172.16.1.1 0.0.0.0 area 0
router(config-router)#network 172.16.2.1 0.0.0.0 area 0
router(config-router)#exit
```

## Exemple de configuration

```
router>enable
```

```
router#configure terminal
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
router(config)#vlan 1
router(config-if)#name service
router(config-if)#exit

router(config)#vlan 2
router(config-if)#name filaire1
router(config-if)#exit

router(config)#vlan 3
router(config-if)#name filaire2
router(config-if)#exit

router(config)#vlan 4
router(config-if)#name wifi1
router(config-if)#exit

router(config)#vlan 5
router(config-if)#name wifi2
router(config-if)#exit
```

* Autorisation des trames du VLAN n°2 sur l'interface :
```
switch(config)#interface g0/1/0
switch(config-if)#switchport mode access
switch(config-if)#switchport access vlan 2
switch(config-if)#no shutdown
switch(config-if)#exit

switch(config)#interface g0/1/2
switch(config-if)#switchport mode access
switch(config-if)#switchport access vlan 2
switch(config-if)#no shutdown
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
router(config)#interface vlan1
router(config-if)#ip address 172.26.1.58 /30
router(config-if)#no shutdown
router(config-if)#exit

router(config)#interface vlan 2
router(config-if)#ip address 172.26.1.38 /29
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

* Configuration IP des VLAN :
```
router(config)#interface vlan 2
router(config-if)#ip address 192.168.2.1 255.255.255.0
router(config-if)#exit
router(config)#exit
router(config)#interface vlan 3
router(config-if)#ip address 172.26.1.46 /29
router(config-if)#exit
router(config)#exit
router(config)#interface vlan 4
router(config-if)#ip address 172.26.1.50 /30
router(config-if)#exit
router(config)#exit
router(config)#interface vlan 5
router(config-if)#ip address 172.26.1.54 /30
router(config-if)#exit
router(config)#exit
```

* Autorisation du VLAN dans l'interface :
```
router(config)#interface g0/1/1
router(config-if)#switchport mode access
router(config-if)#switchport access vlan 3
router(config-if)#no shutdown
router(config-if)#exit
```

* Déclaration du tronçon :
```
router(config)#interface g0/1/3
router(config-if)#switchport mode trunk
router(config-if)#switchport trunk allowed vlan 4,5
router(config-if)#no shutdown
router(config-if)#exit
```

* Configuration du routage dynamique :
```
router(config)#router rip
router(config-router)#version 2
router(config-router)#no auto-summary
router(config-router)#network 192.168.222.32
router(config-router)#network 172.26.1.32
router(config-router)#exit
```

* Déclaration des tronçons :
```
router(config)#interface g0/0/0
router(config-if)#no ip address
router(config-if)#no shutdown
router(config-if)#exit
router(config)#interface g0/0/0.132
router(config-if)#encapsulation dot1q 132
router(config-if)#ip address 192.168.222.43 255.255.255.240
router(config-if)#no shutdown
router(config-if)#exit
router(config)#interface g0/0/0.20
router(config-if)#encapsulation dot1q 20
router(config-if)#ip address 192.168.1.110 255.255.255.0
router(config-if)#no shutdown
router(config-if)#exit
```

* Déclaration des routes :
```
router(config)#no ip route 192.168.222.33
router(config)#ip route 192.168.1.253
```

* Ajout d'une route par défaut :
```
router(config)#ip route 0.0.0.0 0.0.0.0 192.168.222.33
```

* Configuration du DHCP :
```
router(config)#ip dhcp pool groupea
router(dhcp-config)#network 172.26.1.48 /30
router(dhcp-config)#dns-server 193.48.57.48
router(dhcp-config)#default-router 172.26.1.50
router(dhcp-config)#exit

router(config)#ip dhcp pool groupeb
router(dhcp-config)#network 172.26.1.52 /30
router(dhcp-config)#dns-server 193.48.57.48
router(dhcp-config)#default-router 172.26.1.54
router(dhcp-config)#exit

router(config)#ip dhcp excluded-address 172.26.1.50
router(config)#ip dhcp excluded-address 172.26.1.54
```

* Sauvegarde de la configuration actuelle dans la NVRAM :
```
router(config)#copy running-config startup-config
```
