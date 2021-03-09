## ÉNONCÉ DU TRAVAIL PRATIQUE 01

Il faut démarrer, avec docker-compose, une application multi-services qui propose les services suivants:

* Le réseau privé: **reseauWP**
	* **Serveur Web principal** de l'appliccation sur le port **80**
	* Le SGBD **mariaDB** sur le port **3307**
	* Le service **wordpress** sur le port **88**
	* Le service **phpmyadmin** sur le port **82**

* Le réseau privé: **reseauPMM**
	* Le SGBD **postgreSQL**  sur le port **5432**
	* Le service **percona PMM Server** sur le port **83**
 	* Le service **percona PMM client**
 	* Le service **postgresAdmin** sur le port **81**

<a href="https://hub.docker.com/r/perconalab/pmm-client">test d'un lien</a>

<a href="#">![Écran de l'application](ecran-depart.png)</a>
