To access the Tegola using a domain name, we can set up a reverse proxy for Tegola with Nginx or Apache. This will also allow us to enable HTTPS with free Let’s Encrypt certificate.

Nginx
Nginx is a very popular web server and reverse proxy. If you prefer to use Nginx, run the following command to install it.

sudo apt install nginx
Then create a server block file for Tegola.

sudo nano /etc/nginx/conf.d/tegola.conf
Add the following content to this file. Replace vector-tile.example.com with your own domain name. You should also create DNS A record for this sub-domain. If you don’t have a real domain name, I recommend going to NameCheap to buy one. The price is low and they give whois privacy protection free for life.

server {
      listen 80;
      listen [::]:80;
      server_name vector-ile.example.com;

      access_log /var/log/nginx/tegola.access;
      error_log /var/log/nginx/tegola.error;

      location / {
          proxy_pass http://127.0.0.1:8080;
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;

          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
          proxy_set_header X-Forwarded-Protocol $scheme;
          proxy_set_header X-Forwarded-Host $http_host;
      }
}
Save and close this file. Then test Nginx configuration.

sudo nginx -t
If the test is successful, reload Nginx for the change to take effect.

sudo systemctl reload nginx
Now you can access Tegola via vector-tile.example.com.
