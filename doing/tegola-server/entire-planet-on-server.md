# REF https://www.linuxbabe.com/ubuntu/set-up-tegola-vector-tile-server-ubuntu-20-04?utm_source=pocket_reader

Tegola uses the Mapbox vector tile format.

* [ ] pick a cloud vps that has comparable specs to Contabo

The specs recommended by LinuxBabe were:
* A 10 core CPU
* 60 GB RAM
* 1.6 TB Intel Optane SSD

* [ ] log into contabo

* [ ] adduser drifter

* [ ] try Ine1dY0uB@by and if not Ine1dY0uB4by

* [ ] usermod -aG sudo drifter

* [ ] `su - drifter` to change to drifter user

* [ ] `sudo ls -la /root` to test for sudo privledges

* [ ] log out of server

* [ ] log in with `drifter@144.126.131.168`

vvvv Ok I'm in Contabo server as drifter user

* [ ] sudo apt update; sudo apt upgrade -y

* [ ] echo "dev [signed-by=/etc/apt/keyrings/postgresql.asc] http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)0pdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list

* [ ] sudo mkdir /etc/apt/keyrings/

* [ ] wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo tee /etc/apt/keyrings/postgresql.asc

* [ ] sudo apt update

* [ ] sudo apt install -y postgresql postgresql-contrib postgresql-15 postgresql-client-15

* [ ] sudo apt inatall postgis postgresql-15-postgis-3

* [ ] sudo -u postgres -i

* [ ] create a PostgreSQL database user `osm`
```
dreateuser osm

psql -c "ALTER USER osm WITH PASSWORD 'Ine1dY0uB4by';"
```

* [ ] create a databse named osm and make `osm` owner of the db
*`-E UTF8` specifies the character encoding scheme to be used in the datase is `UTF8`*
`createdb -E UTF8 -O osm osm`

* [ ] create the `postgis` and `hstore` extensions for the `osm` database
```
psql -c "CREATE EXTENSION postgis;" -d osm

psql -c "CREATE EXTENSION hstore;" -d osm
```

* [ ] set osm as the table owner
```
psql -c "ALTER TABLE spatial_ref_sys OWNER TO osm;" -d osm
```

* create a database named `natural_earth` and make `osm` the owner of the database
```
createdb -E UTF8 -O osm natural_earth
```

* [ ] create the `postgis` and `hstore` extension for the `natural_earth` database
```
psql -c "CREATE EXTENSION postgis;" -d natural_earth

psql -c "CREATE EXTENSION hstore;" -d natural_earth
```

* [ ] configure PostgreSQL to speed  up import process and improve performance
```
shared_buffers = 15GB

work_mem = 1GB

effective_cache_size = 20GB
```

* [ ] restart the server for changes to take place
`sudo systemctl restart postgresql`

* [ ] find the process id of the running Postgres instance
```
sudo head -1 /var/lib/postgresql/15/main/postmaster.pid
```
*if there isn't a postmaster.pid file then Postgres isn't running*

* [ ] check the VmPeak value of this process ID
` grep ^VmPeak /proc/PROCESS_ID/status`
---> VmPeak: 16161536 kB
*this is the peak memory size that will be used by PostgreSQL

* [ ] check the size of huge page in Linux
`cat /proc/meminfo | grep -i huge`
```
AnonHugePages:         0 kB
ShmemHugePages:        0 kB
FileHugePages:         0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
```

* [x] calculate the number of huge pages I need = VmPeak/hugePageSize
16161536/2048 = 7891.375

* [x] allocate this many huge pages inside of `/etc/sysctl.conf` by adding this to the end of the file
` vm.nr_hugepages = 7892`... or WHATever the number is from the calculation above

* [ ] `sudo sysctl -p` to apply changes
*I can verify the meminfo again with `cat /proc/meminfo | grep -i huge`*

* restart postgres to use huge pages
`sudo systemctl restart postgresql`

* [x] install screen with `sudo apt install screen`... this is so I can let map data load and detach and do other stuff

* [x] start screen with `screen` (hit Enter after I see the startup text)

*imposm converts OpenStreetMap data to postGIS-enabled PostgreSQL databases*
* [x] use wget to request install
```
wget https://github.com/omniscale/imposm3/releases/download/v0.11.1/imposm-0.11.1-linux-x86-64.tar.gz
```

* [x] extract the archive
```
tar xvf imposm-0.11.1-linux-x86-64.tar.gz
```

* [x] move it to the `/opt/` directory
`sudo mv imposm-0.11.1-linux-x86-64 /opt/imposm`

*download speeds for openstreetmap.org are currently restricted to 2048 KB/s... so download from mirror*
* [x] request download entire planet map from mirror `https://download.bbbike.org` with:
`wget -c https://download.bbbike.org/osm/planet/planet-latest.osm.pbf`

* [x] start the data import with:
```
/opt/imposm/imposm import -connection postgis://osm:IG0tY0uB4by@localhost/osm -mapping/opt/tegola-osm/imposm3-mapping.json -read planet.latest.osm.pbf -write
```
... or WHATever the name of the planet file is

* [x] detach and let the data import
... current writing planet data




... The above is until step 4

* [ ] split this file into the 4 steps
