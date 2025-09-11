# What Nginx
Nginx is a high-performance, open-source web server and reverse proxy server. It is widely used for serving static content, load balancing, and Http caching.


# Why use Nginx?

Both Nginx and HTTPD are same however the Performance of Nginx is far better when you compare it with HTTPD. Nginx come with an ever-driven architecture whereas HTTPD comes with thread-based architecture, because of which when you are dealing with a large number of users or dealing with a lots of process Nginx can be much useful when compare to HTTPD.

Nginx also Handles many simultaneous connections with low resource usage. when you're dealing with your application on container or kubernetes Nginx is prefered.

Excellent for serving static files and acting as a reverse proxy.
Built-in load balancing and caching features. and the last one Configuration is simple and flexible. 


## Nginx vs. Apache HTTPD

| Feature | Nginx | Apache HTTPD |
| :--- | :--- | :--- |
| **Architecture** | Event-driven, asynchronous | Process/thread-based |
| **Performance** | High concurrency, low memory | Good, but less scalable |
| **Static Content** | Very fast | Fast, but slower than Nginx |
| **Dynamic Content** | Uses FastCGI, proxy | Native modules (mod_php) |
| **Configuration** | Simple, declarative | Flexible, but complex |
| **Use Cases** | Reverse proxy, load balancer | Dynamic sites, .htaccess |

## Nginx Folder structure (Linux)
| File/Directory | Purpose |
| :--- | :--- |
| `/etc/nginx/nginx.conf` | Main configuration file |
| `/etc/nginx/sites-available/` | Stores virtual host (server block) configs |
| `/etc/nginx/sites-enabled/` | Symlinks to active site configs |
| `/var/www/html` | Default web root directory |
| `/var/log/nginx/` | Contains access and error logs |

## Common Use Case Nginx In Devops

| Use Case | Example |
| :--- | :--- |
| **Web server** | Serving static React/Angular apps |
| **Reverse proxy** | Forwarding requests to backend apps (Node.js, Python, Java) |
| **Load balancer** | Distributing load between multiple backend servers |
| **SSL termination** | Handling HTTPS at the edge |
| **Caching** | Reducing load on upstream services |
| **Ingress controller (Kubernetes)** | Managing traffic inside Kubernetes clusters |
| **Rate limiting & security enforcement** | Protecting APIs from abuse or bots |

## Install Nginx on Ubuntu/Debian
```bash
sudo apt update
sudo apt install nginx -y
```


Nginx is preferred for high-traffic, static content, and proxy scenarios. Apache HTTPD is more flexible for dynamic content and legacy applications.
