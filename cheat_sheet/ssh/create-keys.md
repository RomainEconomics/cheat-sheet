# Ssh

## Examples

### Copy ssh to a remote server

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub user@remote
```

Then in the remote server, we should be able to see the public key in the `~/.ssh/authorized_keys` file.
