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
