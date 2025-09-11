# What is a Load Balancer?

A load balancer is a system that distributes incoming network traffic across multiple backend servers. Its main goal is to ensure no single server becomes overwhelmed, improving reliability and performance.

# Type of Load Balancer
- round-robin	Default — rotates through all backends equally
- least_conn	Sends traffic to the backend with the fewest active connections
- ip_hash	Uses client IP to consistently route requests to the same backend


# Why is a Load Balancer Required?

- **High Availability:** Prevents downtime by rerouting traffic if a server fails.
- **Scalability:** Allows you to add more servers to handle increased traffic.
- **Performance:** Balances requests so no server is overloaded, resulting in faster response times.
- **Flexibility:** Supports rolling updates and maintenance without affecting users.
- **Security:** Can hide backend servers and enforce security policies.

Load balancers are essential for modern web applications to ensure smooth, reliable, and

# Round Robin Load Balancer
Edit default configuration
```bash
sudo vim /etc/nginx/sites-available/default
```

Paste upstream Above server
```bash
# This script perform the round robin
upstream backend_app {
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        }

server {
    listen 80;
    server_name localhost;

location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```

## Create simple node backend for this Nginx 
### Create a folder for bakcend 
```bash
mkdir test1 && cd test1
```

### Node server 1
```bash
const http = require('http');
http.createServer((req, res) => {
  res.end('Hello from Node.js backend!');
}).listen(3001);
```

### Node server 2
```bash
const http = require('http');
http.createServer((req, res) => {
  res.end('Hello from Node.js backend!');
}).listen(3002);
```

### Run the script
```bash
node server1.js
node server2.js
```

### Reload systemctl 
```bash
sudo nginx -t
sudo systemctl reload nginx
```

# Switch Load Balancer
## Least Connection
```bash
upstream backend_app {
        least_conn;
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        }

```
## Ip-Hash
```bash
upstream backend_app {
        ip-hash;
        server 127.0.0.1:3001;
        server 127.0.0.1:3002;
        }
```