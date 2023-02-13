# REF https://www.linuxbabe.com/ubuntu/basemap-tileserver-gl-openmaptiles-ubuntu-22-04

OpenMapTiles relies on Docker, so we need to install Docker.

sudo apt install docker.io docker-compose
Add your user account to the docker group.

sudo usermod -aG docker username
Log out and log back in for the change to take effect. Then run the following command to check running Docker containers.

docker ps
It should at least output the following texts.

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
Clone the OpenMapTiles Github repo.

cd ~ 

git clone https://github.com/openmaptiles/openmaptiles.git
Create the data.yml, mapping.yml and SQL files.

cd openmaptiles/

sudo make
ubuntu openmaptiles generate-sql

Edit the docker-compose.yml file.

nano docker-compose.yml
* [x] Change the port nubmer to 2345.
Originally it was this:
```
ports:
    -"${PGPORT:-5432}:${PGPORT:-5432}"

```
  postgres:
    image: "${POSTGIS_IMAGE:-openmaptiles/postgis}:${TOOLS_VERSION}"
    # Use "command: postgres -c jit=off" for PostgreSQL 11+ because of slow large MVT query processing
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - postgres
    ports:
      - "2345"
    env_file: .env
Save and close the file. Then edit the .env file.

* [ ] make these changes in `nano .env`
Find the following lines.

* [x]  Make sure these values are in sync with the ones in .env-postgres file
PGDATABASE=openmaptiles
PGUSER=openmaptiles
PGPASSWORD=openmaptiles
PGHOST=postgres
PGPORT=5432
Change them to the following. 172.17.0.1 is the Docker network interface.

PGDATABASE=openstreetmap
PGUSER=osm
PGPASSWORD=osm_password
PGHOST=172.17.0.1
PGPORT=5432
Find the following lines.

# Which zooms to generate with   make generate-tiles-pg
MIN_ZOOM=0
MAX_ZOOM=7
Set max zoom level to 14.

# Which zooms to generate with make generate-tiles-pg
MIN_ZOOM=0
MAX_ZOOM=14
Save and close the file.  

* [ ] Create a .osmenv file in your home directory.

nano ~/.osmenv
Add the following lines.

export PGDATABASE=openstreetmap
export PGUSER=osm
export PGPASSWORD=osm_password
export PGHOST=172.17.0.1
export PGPORT=5432
Save and close the file. Then run the following command to set the above environment variables.

source ~/.osmenv

chmod 700 ~/.osmenv
OpenMapTiles will start a Docker container and access PostgreSQL database via 172.17.0.1, so we need to configure PostgreSQL to listen on this IP address.

sudo nano /etc/postgresql/15/main/postgresql.conf
Find the following line.

#listen_addresses = 'localhost'
Change it to:

listen_addresses = 'localhost,172.17.0.1'
Save and close the file. Then edit pg_hba.conf file.

sudo nano /etc/postgresql/15/main/pg_hba.conf
Find the following lines.

# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
This allows users to log in to PostgreSQL from the 127.0.0.1 IP address. We need to add the 172.17.0.0/24 and 172.18.0.0/24 network to allow login from Docker.

# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
host    all             all             172.17.0.0/24           scram-sha-256
host    all             all             172.18.0.0/24           scram-sha-256
Save and close the file. Restart PostgreSQL for the changes to take effect.

sudo systemctl restart postgresql
If you enabled firewall on the server, you should also allow connections from the 172.17.0.0/24 and 172.18.0.0/24 network. For example, if you use the UFW firewall, run the following command.

sudo ufw insert 1 allow in from 172.17.0.0/24

sudo ufw insert 1 allow in from 172.18.0.0/24
You also need to allow SSH.

sudo ufw allow ssh
Enable and restart UFW for the changes to take effect.

sudo ufw enable

sudo systemctl restart ufw
List the PostgreSQL listening addresses:

sudo ss -lnpt | grep postgres
You should see that PostgreSQL listens on both 127.0.0.1 and 172.17.0.1.

LISTEN 0      244            172.17.0.1:5432       0.0.0.0:*    users:(("postgres",pid=19767,fd=6))                                           
LISTEN 0      244             127.0.0.1:5432       0.0.0.0:*    users:(("postgres",pid=19767,fd=5))
