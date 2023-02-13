Step 6: Import the OSM Land and Natural Earth dataset
Edit the /opt/tegola-osm/osm_land.sh file.

sudo nano /opt/tegola-osm/osm_land.sh
Enter your database details.

# database connection variables
DB_NAME="osm"
DB_HOST="localhost"
DB_PORT="5432"
DB_USER="osm"
DB_PW="osm_password"
Save and close the file. Install gdal.

sudo apt install gdal-bin
Generate relation land_polygons in the osm database.

/opt/tegola-osm/osm_land.sh


Next, edit the /opt/tegola-osm/natural_earth.sh file.

sudo nano /opt/tegola-osm/natural_earth.sh
Enter your database details.

# database connection variables
DB_NAME="natural_earth"
DB_HOST="localhost"
DB_PORT="5432"
DB_USER="osm"
DB_PW="osm_password"
Save and close the file. Then generate tables in the natural_earth database.

/opt/tegola-osm/natural_earth.sh
Run the postgis_helpers SQL script.

sudo -u postgres -i psql -d osm -a -f /opt/tegola-osm/postgis_helpers.sql
Run the postgis_index.sql script to add indexes to OSM table columns to increase query performance.

* [ ] sudo -u postgres -i psql -d osm -a -f /opt/tegola-osm/postgis_index.sql
WHEN I run this, I get this
```
CREATE INDEX ON osm_transport_lines_gen0 (type);
psql:/opt/tegola-osm/postgis_index.sql:6: ERROR:  relation "osm_transport_lines_gen0" does not exist
```

From that command, the database is osm.
??HOW to I open a console for database osm?
