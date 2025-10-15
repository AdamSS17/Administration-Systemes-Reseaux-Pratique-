# Administration-Systemes-Reseaux-Pratique-
# phase 2
# 2.1configuration router cisco
# interconnecter switch routeur et pc 
# puis configurer routeur avec enable conf terminal enable secret [mot de passe](protège l'accès à ce que l'on appelle le Mode Privilégié utilise un chiffrement fort (MD5) pour masquer le mot de passe dans le fichier de configuration)
# Sauvegarder et Vérifier (Les Commandes Cruciales)
# pour le  sauvegarde il faut revenir en mode privilegier Router(config)# end
# dabord Affichez la configuration courante (pour voir votre travail) Router# SHOW RUNNING-CONFIG il Affiche l'état actuel et actif de l'équipement (ce qui est dans la RAM)
   # Vérifier que l'adresse IP, le mot de passe, ou le nom que vous venez de configurer est bien pris en compte.
   # Dépanner un problème (par exemple, vérifier pourquoi une interface ne s'allume pas).
   # Documenter la configuration avant de faire un changement risqué.
# copy running-config startup-config (Sauvegarde) Copie la configuration active (RAM) vers la configuration de démarrage (NVRAM).
   # La RAM est une mémoire volatile (elle perd ses données quand il n'y a plus de courant).
   # La NVRAM est une mémoire non volatile (elle garde ses données).
   # Lorsqu'un routeur ou un switch démarre, il va TOUJOURS chercher sa configuration dans la startup-config (NVRAM).
   # Si vous configurez des adresses IP, des routes, des VLANs, puis que vous oubliez de faire copy running-config startup-config et que le routeur redémarre (suite à une panne, ou un reload), toutes vos modifications seront effacées, et l'équipement reviendra à son état précédent.
# Le routeur demandera : Destination filename [startup-config]?. Appuyez simplement sur Entrée pour confirmer.
# Une fois la configuration du mot de passe reussi   et l'afficher dans la running-config sous forme chiffrée, et à le sauvegarder avec copy run start
   # Testez la sécurité : Tapez exit jusqu'à ce que vous soyez complètement déconnecté, puis reconnectez-vous.
   # Essayez de taper enable et entrez le mot de passe [mot de passe]
# 2.2 Configuration d'un LAN (Réseau Local)
# L'objectif est d'activer l'interface du routeur et de lui donner une adresse IP pour qu'il puisse servir de Passerelle (Gateway) à vos PC.
## Tâche 1 : Configuration de l'Interface du Routeur
# Dans Packet Tracer, retournez sur le routeur R1 (celui que vous venez de configurer)
# Identifiez l'interface par exemple GigabitEthernet0/0 (ou G0/0).
# Passez en Mode de Configuration d'Interface 
# Router# configure terminal Router(config)# interface [NOM_DE_L'INTERFACE]  # Ex: interface GigabitEthernet0/0 Router(config-if)#
# Attribuez l'Adresse IP (La Passerelle) avec la commande ip address 192.168.1.1 255.255.255.0
# Activez l'Interface avec la commande no shutdown
# À ce stade, vous devriez voir des messages de changement d'état de l'interface, et le point sur le lien dans Packet Tracer devrait passer du rouge/orange au vert
# retourner en mode privilegie avec la commande END avant de sauvegarder   avec copy run start
# Tâche 2 : Configuration du PC Client
# Cliquez sur le PC dans votre topologie Packet Tracer. Allez dans l'onglet Desktop (Bureau) puis IP Configuration. Configurez ces paramètres en mode Statique : Adresse IP : 192.168.1.100 (ou toute IP libre dans le réseau, ex: $192.168.1.x$) Masque de sous-réseau : 255.255.255.0 Passerelle par défaut (Default Gateway) : 192.168.1.1 (C'est l'IP que vous venez de donner au routeur !)
# Tâche 3 : Validation
# Sur le PC, ouvrez le Command Prompt 
# Testez la passerelle avec ping 192.168.1.1
# Si le ping réussit, vous avez configuré votre premier routeur Cisco pour servir de passerelle à votre LAN !
# Étape 2.3 : Configurer le Routeur Cisco en Serveur DHCP
# Tâche 1 : Exclure les Adresses Statiques (Sécurité et Stabilité)
# L'exclusion est la première étape pour garantir la stabilité de notre réseau.
# onutilise la commande ip dhcp excluded-address 192.168.1.1 192.168.1.9 
# 192.168.1.1(Cette adresse est la Passerelle par défaut de votre réseau (l'IP de l'interface du Routeur R1). La passerelle doit toujours être statique (jamais distribuée par DHCP) pour éviter les problèmes.) 
# Nous excluons toutes les adresses entre 192.168.1.1 et 192.168.1.9. Cela réserve les 9 premières adresses du réseau pour d'autres équipements de service qui doivent avoir une adresse statique (ex: Serveurs, Imprimantes Réseau, autres Routeurs).) Cette commande indique au serveur DHCP de NE PAS distribuer les adresses IP dans la plage spécifiée.
# on va dans le mode de configuration CONFIGURE TERMINAL et on lance la commande ip dhcp excluded-address 192.168.1.1 192.168.1.9
# Tâche 2 : Créer le Pool DHCP (Le Réservoir d'Adresses)
# Le "Pool" est la configuration du service DHCP lui-même. C'est l'endroit où vous définissez les paramètres que les clients recevront.
# Créer le Pool. avec ip dhcp LAN-POOL Cette commande passe en DHCP Configuration Mode (Router(dhcp-config)#). LAN_POOL est simplement le nom que vous donnez à ce service (vous pouvez le nommer comme vous voulez).
# Définir le réseau. avec network 192.168.1.0 255.255.255.0  Indique au serveur DHCP quel est le réseau qu'il doit gérer. 192.168.1.0 est l'adresse réseau. 255.255.255.0 est le masque de sous-réseau (qui définit le nombre d'adresses disponibles).
# Définir la Passerelle avec default-router 192.168.1.1 Indique aux clients DHCP quelle est l'adresse de leur Passerelle par défaut. C'est par cette adresse (le routeur lui-même) qu'ils passeront pour communiquer avec d'autres réseaux (Internet, etc.).
# OPTIONNEL MAIS RECOMMANDÉ dns-server 8.8.8.8 Indique aux clients quelle adresse utiliser pour le DNS (Domain Name System). Le DNS est essentiel pour traduire les noms de domaine (google.com) en adresses IP. 8.8.8.8 est un serveur DNS public de Google
# on va dans le mode de configuration CONFIGURE TERMINAL et on lance les commandes "ip dhcp pool LAN-POOL" puis "network 192.168.1.0 255.255.255.0 " puis "default-router 192.168.1.1" enfin "dns-server 8.8.8.8"
# retourner en mode privilegie avec la commande END avant de sauvegarder   avec "copy run start"
# Testez le Client Sur le PC Client, allez dans Desktop > IP Configuration puis Passez de Static à DHCP
# Le PC devrait recevoir une adresse IP entre 192.168.1.10 et 192.168.1.254 et la Passerelle 192.168.1.1.




