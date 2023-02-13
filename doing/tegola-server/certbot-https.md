To encrypt the HTTP traffic when you visit Tegola server from outside, we can enable HTTPS by installing a free TLS certificate issued from Let’s Encrypt. Run the following command to install Let’s Encrypt client (certbot) on Ubuntu 20.04.

sudo apt install certbot
If you use Nginx, then you also need to install the Certbot Nginx plugin.

sudo apt install python3-certbot-nginx
Next, run the following command to obtain and install TLS certificate.

sudo certbot --nginx --agree-tos --redirect --hsts --staple-ocsp --email you@example.com -d vector-tile.example.com
If you use Apache, then you need to install the Certbot Apache plugin.

sudo apt install python3-certbot-apache
Next, run the following command to obtain and install TLS certificate.

sudo certbot --apache --agree-tos --redirect --hsts --staple-ocsp --uir --email you@example.com -d vector-tile.example.com
Where:

--nginx: Use the nginx plugin.
--apache: Use the Apache plugin.
--agree-tos: Agree to terms of service.
--redirect: Force HTTPS by 301 redirect.
--hsts: Add the Strict-Transport-Security header to every HTTP response. Forcing browser to always use TLS for the domain. Defends against SSL/TLS Stripping.
--staple-ocsp: Enables OCSP Stapling. A valid OCSP response is stapled to the certificate that the server offers during TLS.
--uir: upgrade insecure requests.
The certificate should now be obtained and automatically installed. And you can access Tegola via HTTPS: https://vector-tile.example.com.
