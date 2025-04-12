# Install deb files

## Debian Package Management (dpkg)

```bash
# Install a deb file
dpkg -i package.deb
sudo dpkg -i package.deb

# Remove a package
sudo dpkg -r package_name
```

Issue with `dpkg` is that it does not install dependencies. Hence, insted we use `apt` instead.

## Advanced Package Tool (apt)

- `bat /etc/apt/sources.list.d/ubuntu.sources`: Show all repositories from the system
- `ll /etc/apt/sources.list.d/`: Show all third-party repositories

Updates only update the sources list. To install the updates, use `upgrade`.
