
# Lxd

## Links

- 

## Examples

### Install

```bash
sudo apt update
sudo apt dist-upgrade
adduser USER
sudo snap install lxd
sudo usermod -a -G lxd USER
```

### List all containers

```bash
lxc ls
```

### Available images

```bash
lxc remote list
lxc image list ubuntu: 22.04 | grep CONTAINER
```

### Launch a container

```bash
lxc launch ubuntu:HASH CONTAINER_NAME
lxc exec CONTAINER_NAME -- apt update && sudo apt upgrade -y
```