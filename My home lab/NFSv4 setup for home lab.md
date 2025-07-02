In the `/etc/exports` file add entry for admin user:

```exports
/srv/nfs4/homes/rwxrob *(rw,sync,anonuid=1000,anongid=1000,sec=sys)
```


> [!NOTE] 
> `uid` and `gid` are NFSv3 *only*.

Then on the client `/etc/fstab`:

```fstab
walt:/srv/nfs4/homes/rwxrob  /s/rwxrob  nfs4  sec=sys,rw,sync  0  0
```

Make sure that the directory ownership for *both* the exported directory and the mount point coincide.

To check that its working use `df -h /s/rwxrob` or whatever.