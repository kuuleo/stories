Edit the configuration file.

sudo nano /opt/tegola-osm/tegola.toml
Configure the listening port, cache type, and data provider as follows.

[webserver]
port = ":8080"

# Tegola offers three tile caching strategies: "file", "redis", and "s3"
[cache]
type = "redis"
#bucket = "${S3CACHE_BUCKET}"
#basepath = "${S3CACHE_BASEPATH}"
#region = "${S3CACHE_REGION}"
#aws_access_key_id = "${S3CACHE_AWS_ACCESS_KEY_ID}"
#aws_secret_access_key = "${S3CACHE_AWS_SECRET_ACCESS_KEY}"

#   OpenStreetMap (OSM)
[[providers]]
name = "osm"
type = "postgis"
host = "127.0.0.1"
port = "5432"
database = "osm"
user = "osm"
password = "osm_password"

# Natural Earth
[[providers]]
name = "ne"
type = "postgis"
host = "127.0.0.1"
port = "5432"
database = "natural_earth"
user = "osm"
password = "osm_password"
Notice there are two databases: osm and natural_earth.

Find the following line.

center = [-76.275329586789, 39.153492567373, 8.0] # optional center value. part of the TileJSON spec
You can set a custom center location (longitude and latitude) for your map and the default zoom level. Notice that you must use decimal values and can’t use integer values.

center = [0.8, 55.5, 5.0] # optional center value. part of the TileJSON spec
Save and close the file. Then install Redis cache server.

sudo apt install redis-server
Start Tegola.

/usr/local/bin/tegola serve --config=/opt/tegola-osm/tegola.toml
Now Tegola is listening on port 8080.
