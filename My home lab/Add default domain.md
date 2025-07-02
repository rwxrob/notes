Update `/etc/systemd/resolved.conf`:

```
Domains=lan
```

Then restart:

```bash
sudo systemctl restart systemd-resolved
```

The can check `/etc/resolve.d` (which is automatically created).