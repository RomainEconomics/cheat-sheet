
# Gpg

## Links

- [GnuPG](https://gnupg.org/)

## Examples

### List keys

```bash
gpg --list-keys
``` 

### Create new key

```bash
gpg --full-generate-key
```

then follow the prompts:

- Kind of key: (1) RSA and RSA
- Keys size: 4096 (better to have high value)
- 0 (doesn't expire) or some expiration date (e.g. 1y)

```bash
gpg --list-keys # to see the new key
```

### Update key

```bash
gpg --edit-key <email>
help   # list all commands available
list   # list all the keys
key 0  # select first key
expire # change expiration date
```

### Update passphrase

```bash
gpg --passwd <email>
```