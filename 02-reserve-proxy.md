# What is a Reverse Proxy?
A reverse proxy is a server that sits in front of backend servers and forwards client requests to them. Instead of clients connecting directly to your application, they connect to the reverse proxy, which then relays the request.

# Why we use Reverse Proxy?
- **Security:** It hides backend servers from direct exposure to the internet, reducing attack surface.
- **Load Balancing:** Distributes incoming traffic across multiple backend servers for better performance and reliability.
- **SSL Termination:** Handles HTTPS encryption, offloading this work from backend servers.
- **Caching:** Stores responses to reduce load and speed up repeated requests.
- **Centralized Access Control:** Manages authentication, rate limiting, and logging in one place.

when there's someone who will perform DDOS attack to your application 
Reserve Proxy can detect bot traffic from DDOS and Reserve Proxy won't pass the traffic to your Application server.

# Example use case using node.js
Install node.js on your machine
```bash
sudo apt update
sudo apt install nodejs npm -y
```

create a directory for node server
```bash
mkdir ~/node-backend && cd ~/node-backend
vim server.js
```

the script server.js
```bash
const http = require('http');
http.createServer((req, res) => {
  res.end('Hello from Node.js backend!');
}).listen(3000);
```

Run the script
```bash
node server.js
```

output : ```Your app is now running at http://localhost:3000```

## Configure backend with Nginx as reserve proxy
```bash
sudo vim /etc/nginx/sites-available/default
```
Replace location / with:
```bash
location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```

### Reload the Nginx
Check config for the syntax errors
```bash
sudo nginx -t
```

Reload Nginx
```bash
sudo systemctl reload nginx
```

### Test in browser
```bash
hhtp://localhost
```

You should see: Hello from Node.js backend!