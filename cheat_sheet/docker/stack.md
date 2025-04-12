# Docker Stack

## Main Commands

```bash
# 1. Access remotely to the docker instance
docker context create CTX_NAME --docker "host=ssh://USER@IP"
docker use context CTX_NAME

# 2. Define swarm mode
docker swarm init

# 3. Define some secrets (from a file)
docker secret create db-password ./secret-pwd.txt
docker secret ls

# 4. Deploy a stack
docker stack deploy -c compose.yaml STACK_NAME
# If using private images
docker stack deploy --with-registry-auth -c docker-compose.yml STACK_NAME

# 5. Main stack commands
docker stack ls
docker stack ps STACK_NAME
docker stack rm STACK_NAME
docker service ls
docker service ps SERVICE_NAME
docker service logs -f SERVICE_NAME
docker service rm SERVICE_NAME
docker service rollback SERVICE_NAME

```

# Docker Compose vs Docker Stack

While you're already familiar with Docker Compose, Docker Stack serves a different purpose in the container orchestration ecosystem. Let me outline the key differences and show you the most relevant commands for working with Docker Stack.

## Key Differences

| Feature         | Docker Compose                                   | Docker Stack                                   |
| --------------- | ------------------------------------------------ | ---------------------------------------------- |
| Purpose         | Development environments, single host deployment | Production orchestration across multiple hosts |
| Swarm Mode      | No (standalone)                                  | Yes (requires Docker Swarm)                    |
| Configuration   | docker-compose.yml                               | Same format, but supports deploy key           |
| Scale           | Limited to single host                           | Across a cluster                               |
| Rolling Updates | No                                               | Yes                                            |
| Health Checks   | Basic                                            | Advanced orchestration                         |

## Purpose of Docker Stack

Docker Stack is designed for production deployments in a Docker Swarm environment. It allows you to:

- Deploy multi-service applications as a single stack
- Scale services across multiple nodes
- Implement rolling updates
- Configure advanced networking
- Manage secrets and configs

## Most Relevant Commands for Docker Stack

### 1. Initialize a Swarm (prerequisite)

```bash
# Initialize a swarm on the current node
docker swarm init --advertise-addr <YOUR-IP>

# To add worker nodes (command provided after init)
docker swarm join --token <TOKEN> <MANAGER-IP>:<PORT>
```

### 2. Deploy a Stack

```bash
# Deploy or update a stack
docker stack deploy -c docker-compose.yml my_stack_name

# You can also use the --with-registry-auth flag if using private images
docker stack deploy --with-registry-auth -c docker-compose.yml my_stack_name
```

### 3. List Stacks

```bash
docker stack ls
```

### 4. List Services in a Stack

```bash
docker stack services my_stack_name
```

### 5. List Tasks in a Stack

```bash
docker stack ps my_stack_name
```

### 6. Remove a Stack

```bash
docker stack rm my_stack_name
```

## Typical Workflow

1. Convert your existing docker-compose.yml file to be Stack-compatible by adding deploy sections:

```yaml
version: "3.8"
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    deploy:
      replicas: 3
      update_config:
        parallelism: 1
        delay: 10s
      restart_policy:
        condition: on-failure
```

2. Initialize a Swarm (if not already done)
3. Deploy your stack
4. Monitor services and tasks
5. Scale or update as needed
6. Remove stack when no longer needed

## Key Advantages to Consider

- **High Availability**: Services can be replicated across multiple nodes
- **Load Balancing**: Built-in load balancing for replicated services
- **Rolling Updates**: Update services without downtime
- **Self-Healing**: Automatically restarts failed containers
- **Secrets Management**: Securely manage sensitive information
