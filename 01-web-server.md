# What is web server
A web server is software that serves static files (like .html, .css, .js, .png) over HTTP. When users visit your website, the web server responds with these files.

# Nginx Default Directories and Config

| Path                                | Description                              |
|-------------------------------------|------------------------------------------|
| `/var/www/html`                     | Default directory for static files       |
| `/etc/nginx/sites-available/default`| Default config file pointing to web root |

## Anatomy of a Basic server Block
```bash
server {
    listen 80;
    server_name localhost;

    location / {
        root /var/www/html;
        index index.html;
        try_files $uri $uri/ =404;
    }

    error_page 404 /404.html;
    location = /404.html {
        internal;
    }
}
```

Explanation Script Configuration Above:
``listen 80;`` → Listens on HTTP port 80
``server_name localhost;`` → Domain or IP to respond to
``root`` → Path where NGINX looks for files
``index`` → Default file to serve (usually index.html)
``location`` / → URL path handling

# Serve a Static Web to Nginx
1. Create a file html
```bash

```

2. Reload Nginx 
```bash
sudo systemctl reload nginx
```

3. Visit ```http://localhost``` on your server's IP 

# Difference between Root and Alias
Root Appends the request URI to the given path. Typically used for directory-based locations.
```bash
location /static/ {
    root /var/www/html;
}
```

Alias
```bash
location /static/ {
    alias /var/www/html/assets/;
}
```

Alias Replaces the location part with the given path. Typically used for mapping URIs to a different directory.
