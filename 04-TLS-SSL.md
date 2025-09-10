# What is TLS and SSL?

**SSL (Secure Sockets Layer)** and **TLS (Transport Layer Security)** are cryptographic protocols that secure data transmitted over the internet. TLS is the successor to SSL and is more secure.

- /etc/ssl/certs/nginx-selfsigned.crt	SSL certificate
- /etc/ssl/private/nginx-selfsigned.key	Private key
- /etc/nginx/sites-available/default	HTTPS proxy config

# Why Use TLS/SSL?

- **Encryption:** Protects sensitive data from being intercepted during transmission.
- **Authentication:** Verifies the identity of the server to clients.
- **Data Integrity:** Ensures data is not tampered with during transit.
- **Trust:** Enables HTTPS, showing users their connection is secure.

TLS/SSL is essential for securing websites, APIs, and any service that transmits sensitive

# Generate and Configure TLS and SSL
## Step 1 change to early directory 
```bash
cd ~
```
Afterwards paste this command 
```bash
sudo openssl req -x509 -nodes -days 365 \
 -newkey rsa:2048 \
 -keyout /etc/ssl/private/nginx-selfsigned.key \
 -out /etc/ssl/certs/nginx-selfsigned.crt
```

After you enter this command you will ask for some question like email, region and more fill this Question to your information
- Common Name (CN): use ``localhost`` or your ``server’s IP``

## Step 2 Edit Nginx Confiuration
Edit the Default site config
```bash

```

Replace with the following
```bash
server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
    ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

# Optional: Redirect HTTP to HTTPS
server {
    listen 80;
    server_name localhost;
    return 301 https://$host$request_uri;
}
```

# Step 3 Reload Nginx
```bash
sudo nginx -t
sudo systemctl reload nginx
```

# Test on localhost
```bash
https://localhost
```