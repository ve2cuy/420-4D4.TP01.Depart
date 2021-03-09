## ÉNONCÉ DU TRAVAIL PRATIQUE 01 - PONDÉRATION: 30%
### Date de remise: Dimanche, le 28 mars 2021, 23h59 sur github, dans un projet privé.
### Il faut m'inviter comme collaborateur (ve2cuy) et m'envoyer le lien du projet à aboudrea@cstj.qc.ca 

## Il faut démarrer, avec **docker-compose**, une application multi-services qui propose les micro-services suivants:

* Le réseau privé: **reseauWP**
  * **Serveur Web principal** de l'appliccation sur le port **80**
    * À partir du contenu de ce dépot Github ainsi qu'une image personnalisée de *nginx*
      * Il faut éditer le fichier *index.html* pour renseigner correctement les images et les liens du site web. 
  * Le SGBD **mariaDB** sur le port **3307**
  * Le service **wordpress** sur le port **88**
    * L'image wordpress doit contenir le thème <a href="https://wordpress.org/themes/simple-style/">simple-style</a> 
    * L'image wordpress doit contenir le plugin <a href="https://wordpress.org/plugins/code-prettify/">code-prettify</a>
      * Il faudra donc construire une image personnalisée de *wordpress* (docker build)  
    * Dépendances:  "mariaDB"  

  * Le service **phpmyadmin** sur le port **82**
    * Dépendances:  "mariaDB"  

* Le réseau privé: **reseauPMM**
  * Le SGBD <a href="https://hub.docker.com/_/postgres">**postgreSQL**</a>  sur le port **5432**
  * Le service <a href="https://hub.docker.com/r/percona/pmm-server">**percona PMM Server**</a> sur le port **83**
    * Dépendances:  "postgres", "pmm-server"  
  * Le service <a href="https://hub.docker.com/r/perconalab/pmm-client">**percona PMM client**</a> adapté au SGBD postgresSQL, dans le but d'obtenir des statistiques d'utilisation du SGBD via l'application 'percona PMM Server'.
  * Le service <a href="https://hub.docker.com/r/dpage/pgadmin4">**postgresAdmin**</a> sur le port **81**  
    * Dépendances:  "postgres"  

Construction des images personnalisées et démarrage des services de l'application:

	docker-compose up -d --build
  
<br/>

### Voici la liste, obtenue avec docker-compose ps, des services:
	Name                      Command                  State                  Ports
 	-------------------------------------------------------------------------------------------------
 	TP01                  /docker-entrypoint.sh ngin ...   Up             0.0.0.0:80->80/tcp
 	mariabd               docker-entrypoint.sh mysqld      Up             0.0.0.0:3307->3306/tcp
 	pg-admin              /entrypoint.sh                   Up             443/tcp, 0.0.0.0:81->80/tcp
 	phpmyadmin            /docker-entrypoint.sh apac ...   Up             0.0.0.0:82->80/tcp
 	pmm-client-postgres   /entrypoint.py                   Up
 	postgres              docker-entrypoint.sh postgres    Up             0.0.0.0:5432->5432/tcp
 	serveur-pmm           /opt/entrypoint.sh               Up (healthy)   443/tcp, 0.0.0.0:83->80/tcp
 	wordpress             docker-entrypoint.sh apach ...   Up             0.0.0.0:88->80/tcp  
  
<br/>

### Voici la liste des réseaux:
	NETWORK ID     NAME               DRIVER    SCOPE
	84da018281e3   bridge             bridge    local
	5b64d4b7c1d2   host               host      local
	786951a15a98   none               null      local
	21115657f748   reseauPMM          bridge    local
	c29c6df663c8   reseauWP           bridge    local

<br/>

	NOTE: Il ne faut pas inscrire, dans le fichier 'docker-compose.yml' 
	des informations sensibles comme par exemple, des noms d'utilisateurs
	ou des mots de passe.
	
	Utiliser plutot le fichier .env pour créer des variables de substitution.

### Voici la liste des variables utilisées dans le fichier docker-compose.yml
	# perconalab/pmm-server
	PMM_USER=
	PMM_PASS=

	# Wordpress
	WP_HOST=
	WP_USER=
	WP_PASSWORD=
	WP_DB_NAME=

	# MariaDB : La base de données pour WP
	MYSQL_DATABASE=
	MYSQL_USER=
	MYSQL_PASSWORD=
	MYSQL_ROOT_PASSWORD=

	# PostgreSQL
	POSTGRES_USER=
	POSTGRES_PASSWORD=

	# postgresADMIN
	PGADMIN_DEFAULT_EMAIL=tp01@420-4d4.com
	PGADMIN_DEFAULT_PASSWORD=secret

### Voici l'écran principal de l'application (service nginx sur port 80)
<a href="#">![Écran de l'application](ecran-depart.png)</a>



[![Alt text](https://img.youtube.com/vi/VID/0.jpg)](https://www.youtube.com/watch?v=VID)
