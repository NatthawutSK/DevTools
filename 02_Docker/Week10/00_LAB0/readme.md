
### Step 1: Building Docker Images for Express Apps


```bash

docker build -t express-app .

```

### Step 2: Creating a Docker Network

Create a custom network for your Docker containers. This allows the containers to communicate with each other.

```bash
docker network create express-network
```

### Step 3: Running Express App Containers

Run the containers for `app1` and `app2` on the created network:

```bash
docker run -d --name app1 --network express-network -p 3001:3000 express-app
docker run -d --name app2 --network express-network -p 3002:3000 express-app
```

### Step 4: Setting Up Nginx for Load Balancing


```bash
docker run -d --name nginx-load-balancer --network express-network -p 8080:80 -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf:ro nginx
```

