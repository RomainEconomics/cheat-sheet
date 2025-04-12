
# Ansible Setup

## Links

- [YT Video](https://www.youtube.com/watch?v=-Q4T9wLsvOQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70&index=2)

## Examples

First we need a ssh key pair without passphrase.

```bash
ssh-keygen -t ed25519 -C "ansible"
```

Then we need to copy the public key to the remote server.

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@remote
```

Then in the remote server, we should be able to see the public key in the `~/.ssh/authorized_keys` file.

Then we can test the connection with the remote server.




### 