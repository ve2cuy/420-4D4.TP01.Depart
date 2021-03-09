## ÉNONCÉ DU TRAVAIL PRATIQUE 01 - PONDÉRATION: 30%

Il faut démarrer, avec **docker-compose**, une application multi-services qui propose les micro-services suivants:

* Le réseau privé: **reseauWP**
  * **Serveur Web principal** de l'appliccation sur le port **80**
  * Le SGBD **mariaDB** sur le port **3307**
  * Le service **wordpress** sur le port **88**
    * L'image wordpress doit contenir le thème <a href="https://wordpress.org/themes/simple-style/">simple-style</a> 
    * L'image wordpress doit contenir le plugin <a href="https://wordpress.org/plugins/code-prettify/">code-prettify</a>
      * Il faudra donc construire une image personnalisée de *wordpress* (docker build)  
  * Le service **phpmyadmin** sur le port **82**

* Le réseau privé: **reseauPMM**
  * Le SGBD <a href="https://hub.docker.com/_/postgres">**postgreSQL**</a>  sur le port **5432**
  * Le service <a href="https://hub.docker.com/r/percona/pmm-server">**percona PMM Server**</a> sur le port **83**
  * Le service <a href="https://hub.docker.com/r/perconalab/pmm-client">**percona PMM client**</a>
  * Le service <a href="https://hub.docker.com/r/dpage/pgadmin4">**postgresAdmin**</a> sur le port **81**  
  
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

### Voici l'écran principal de l'application (service nginx sur port 80)
<a href="#">![Écran de l'application](ecran-depart.png)</a>



[![Alt text](https://img.youtube.com/vi/VID/0.jpg)](https://www.youtube.com/watch?v=VID)
