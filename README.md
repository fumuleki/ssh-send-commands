# ssh-send-commands

Le script pour but d'automatiser l'envoi de l'ID public SSH, et également envoyer des commandes via SSH à de nombreuses machines, et si l'utilisateur a besoin d'accéder aux machines, cela pourrait être facile, car le script ajoutera toutes les informations requises à .ssh / config.

# Scénario
Si la solution de sécurité échoue, l'administrateur système utilisera le script pour automatiser la distribution des clés SSH pour toutes les machines du réseau et permettra à l'administrateur de SSH -t complètement la machine spécifique accompagnée des autorisations root. L'administrateur système peut utiliser les commandes suivantes pour assurer la sécurité du système, jusqu'à ce que la solution de surveillance revienne en activité.

   - $ ssh -t hostname top -U [username]
   - $ ssh -t hostname  ps -u [username]
   - $ ssh -t hostname watch w
   - $ ssh -t hostname watch w [username]
   - $ ssh -t hostname watch who 
   - $ ssh -t hostname watch who -a
   - $ ssh -t hostname watch users
   - $ ssh -t hostname tail -f /var/log/syslog
   - $ ssh -t hostname htop
