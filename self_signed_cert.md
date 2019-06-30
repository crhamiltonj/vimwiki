# Self Signed Certificate for Web Development and Testing

## Nginx
1. Create the self signed key
  `sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt`
2. Configure Nginx to use SSL
  * Create a configuration snippet containing the SSL key and certificate file locations
    `sudo vim /etc/nginx/snippets/self-signed.conf`
    inside the file add the following
    ```
      ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
      ssl certificate_key /etc/ssl/private/nginx-selfsigned.key;
    ```
  * Create a configuration snippet container strong SSL settings that can be used with any certificates in the future
    `sudo vim /etc/nginx/snippets/ssl-params.conf`
    inside the file add the following:
    ```
    ssl_protocols TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_dhparam /etc/nginx/dhparam.pem;
    ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:DHE-RSA-AES256-GCM-SHA512:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-SHA384;
    ssl_ecdh_curve secp384r1; # Requires nginx >= 1.1.0
    ssl_session_timeout  10m;
    ssl_session_cache shared:SSL:10m;
    ssl_session_tickets off; # Requires nginx >= 1.5.9
    ssl_stapling on; # Requires nginx >= 1.3.7
    ssl_stapling_verify on; # Requires nginx => 1.3.7
    resolver 8.8.8.8 8.8.4.4 valid=300s;
    resolver_timeout 5s;
    # Disable strict transport security for now. You can uncomment the following
    # line if you understand the implications.
    # add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload";
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";
    ```
  * Adjust the Nginx server blocks to handle SSL requests and use the two snippets above
    Backup the original configuration file.
    `sudo cp /etc/nginx/sites-available/example.com /etc/nginx/sites-available/example.com.bak`
    Then edit the configuration file to support SSL. It probably looks like this:
    ```
    server {
      listen 80;
      listen [::]:80;
      
      server_name example.com www.example.com;
      
      root /var/www/example.com/html;
      index index.html index.htm index.nginx-debina.html;
    }
    ```
    Change it so it looks like this:
    ```
    server {
      listen 443 ssl;
      listen [::]:443 ssl;
      include snippets/self-signed.conf;
      include snippets/ssl-params.conf;
      
      server_name example.com www.example.com;
      
      root /var/www/example.com/html;
      index index.html index.htm index.nginx-debian.html;
    }
    
    server {
      listen 80;
      listen [::]:80;
      
      server_name example.com www.example.com;
      
      return 302 https://$server_name$request_url;
    }
    ```
  * Adjust the Firewall
    `sudo ufw allow 'Nginx Full'`
    `sudo ufw delete allow 'Nginx HTTP'`
  * Check the config file settings
    `sudo nginx -t`
  * Restart nginx
    `sudo systemctl restart nginx`
  * Test settings
    try `https://<server_ip>`
  * Change to a permanent redirect for port 80
    `return 301 https://$server_name$request_uri;`
