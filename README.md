# ssh-send-commands

Le script a pour but d'automatiser certaine tache de distributions des clés SSH, et envoyer des commandes via SSH aux nombreuses machines du réseau, et si l'utilisateur a besoin d'accéder aux machines, cela pourrait être facile, car le script ajoutera toutes les informations requises à .ssh / config.

# Scénario
Si la solution de sécurité échoue, l'administrateur système utilisera le script pour automatiser la distribution des clés SSH pour toutes les machines du réseau et permettra à l'administrateur de SSH -t complètement la machine spécifique accompagnée des autorisations root.

#!/usr/bin/env python3

# Importer Modules

    - from sys import argv
     - import atexit
     - import os

script, filename = argv

# Créer un dossier .ssh

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
