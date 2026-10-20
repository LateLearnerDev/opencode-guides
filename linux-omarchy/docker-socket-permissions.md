# Fixing Docker socket permission errors

When Docker reports `permission denied` for `/var/run/docker.sock`, the current user cannot access the daemon socket. First confirm Docker works with elevated privileges using `sudo docker ps`. If that succeeds, add the user to the `docker` group:

```sh
sudo usermod -aG docker "$USER"
```

This grants the account access to the Docker daemon. **Security caveat:** membership in the `docker` group effectively grants root-level control of the machine; only add trusted users. Log out and back in (or reboot) so the new group membership is applied, then verify with `docker ps`.

If `sudo docker ps` also fails, the issue may instead be that the Docker daemon is not running or installed correctly; check the system's Docker service before changing socket permissions. Avoid using `chmod 666 /var/run/docker.sock`, which makes the daemon accessible to every local user and is not a safe fix.
