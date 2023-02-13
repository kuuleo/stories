Tegola is running in the foreground. In order to run it in the background, we can create a systemd serivce, which also allow Tegola to automatically start at system boot time. Press Ctrl+C to stop the current Tegola process, then create the tegola.service file.

sudo nano /etc/systemd/system/tegola.service
Add the following lines to this file.

[Unit]
Description=Tegola Vector Tile Server

[Service]
Type=simple
User=www-data
ExecStart=/usr/local/bin/tegola serve --config=/opt/tegola-osm/tegola.toml
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
Save and close the file. Make www-data as the owner of the /tmp/tegola-cache/ directory.

sudo chown www-data:www-data /tmp/tegola-cache/ -R
Then enable and start this service.

sudo systemctl enable tegola --now
Check its status. Make sure it’s running.

systemctl status tegola

If it’s not running, you can check the journal logs to find out what went wrong.

sudo journalctl -eu tegola
Then in your web browser address bar, type

your-server-ip-address:8080
You should see the vector tile map. Congrats! You just successfully built your own vector tile server. Note that old versions of Firefox can’t display these vector tiles. You need to use a third-party library to display vector tile based maps, which is explained at the end of this tutorial.
