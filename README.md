# ssh-send-commands

Le script a pour but d'automatiser une tache qui ajouter des machines (serveurs) distantes du reseau dans un fichier de configuration SSH (.ssh/config), permettra a l'administrateur système de bien gérer la connexions SSH pour la connexion à distance sécurisée, et envoyer des commandes via SSH vers des nombreuses machines distantes du réseau. Si l'utilisateur a besoin d'accéder aux serveurs, cela pourrait être facile, car le script ajoutera toutes les informations requises à fichier .ssh / config, pour s'authentifier sans mot de passe en utilisant seulement les clés ssh partager.

Le module atexit dans la distribution standard de Python a deux fonctions - register () et unregister (). Les deux fonctions prennent une fonction existante comme argument. Les fonctions enregistrées sont exécutées automatiquement lorsque la session d'interprétation se termine normalement. Si plusieurs fonctions sont enregistrées, leur exécution s'effectue dans l'ordre inverse de l'enregistrement. Cela signifie que les fonctions f1 (), f2 () et f3 () sont enregistrées l'une après l'autre, leur ordre d'exécution sera f3 (), f2 () et f1 ().

La fonction unregister () supprime la fonction spécifiée de la liste des fonctions à appeler automatiquement.

Le code suivant montre comment une fonction est enregistrée pour une exécution automatique à la fin du code. Le programme demande à un utilisateur de saisir des nombres successivement et les ajoute. Lorsque la boucle est terminée, la fonction exit_handler s'enregistrée () est appelée automatiquement pour enregistrer l'ajout dans un fichier(config).

#!/usr/bin/env python3

# Importer Modules

       from sys import argv
       import atexit
       import os

# Créer un repertoire .ssh

    - if not os.path.exists(".ssh"):
        os.makedirs(".ssh")
        print ("ssh folder created")
        print ("\n")

# Fichier de configuration 

    if os.path.exists('.ssh/' + filename):
      print ("Config File exists in .ssh/")
      print ("Now We Editing the same Config file")
      print ("\n")

    filename = ".ssh/config"


    def exit_handler():
        print ('Information Saved')


    if os.path.exists:
       config = open(filename, 'a')
       print ("Creating The ssh config File")
       print ("\n")
       
    else: 
      config = open(filename, 'w')
      print (config)

# Création clé ssh

    if input("Do you want to create ssh key (y). Skip with Enter: "):
         os.system("ssh-keygen -t rsa")
        print ("\n")

# Scan (balayer) ouvrir ports ssh du réseau

    scan1 = input("Scan Your network for open ssh:")
    os.system("nmap -v " + scan1 + "/24" + "| grep " + " 'ssh'")
    print ("\n")

    scan2 = input("Scan Your network for IP Addresses: ")
    os.system("nmap -v " + scan2 + "/24" + "| grep " + " 'port 22'")
    print ("\n")

# Exécution 

    try:
       while True:
            first = input("Please Enter Machine Name: ")
            zero = input("This for the root user:")
            second = input("Please Enter The Hostname Of the Machine Or IP Address: ")
            third = input("Please Enter The Port Number. Skip with Enter: ")
            fourth = input("Please Enter The User: " )
            fifth = input("Copy the ssh id to the machine. Do you want to continue (y) ")
            sixth = input("Copy the ssh id to root. Do you want to continue (y):")
            if first:
                config.write("Host " + first)
                config.write("\n")
            if second:
                config.write("Hostname " + second)
                config.write("\n")
            if third: 
                config.write("Port " + third)
                config.write("\n")
            if fourth:
                config.write("User " + fourth)
                config.write("\n")
                config.write("\n")
            if zero:
                config.write("\n")
                config.write("Host " + zero + "\n" + "Hostname " + second + "\n" + third + "\n" + "User " + "root" + "\n")
                config.write("\n")   
            if fifth:
                    os.system("ssh-copy-id " + fourth + "@" + second)
            if sixth:
                    os.system("ssh -t " + fourth + "@" + second  + " " + " " " 'sudo cp --parents .ssh/authorized_keys /root/' ")    
            print ("Finished and starting with the new machine")
            print ("\n")
            if first != fourth:
                config.write("\n")
                config.write("\n")
                
    except KeyboardInterrupt:    
                  config.close()
    atexit.register(exit_handler)

Enregistrez le code ci-dessus sous auto_ssh.py et exécutez à partir de la ligne de commande. Les nombres successifs saisis sont ajoutés dans le fichier(config) à la fin. Le fichier config sera créé dans le répertoire .ssh

# Scénario
Si la solution de sécurité échoue, l'administrateur système utilisera le script pour automatiser la distribution des clés SSH pour toutes les machines du réseau et permettra à l'administrateur d'accéder facilement aux serveurs du réseau pour envoyer des commandes en utilisant de SSH -t  machine spécifique accompagnée des autorisations root.



