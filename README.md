<div align="center">
<p align="center">
  <a href="https://github.com/losuler/pihole-dnscrypt-docker">
    <img src="img/logo.png" alt="logo" width="150" height="150">
  </a>

  <p align="center">
    <h3 align="center">Pi-hole DNSCrypt Docker</h3>
    <p align="center">
      A docker-compose for Pi-hole and DNSCrypt, daemonized with a systemd service file.
    </p>
  </p>
</p>
</div>

## Dependencies

```
docker
docker-compose
```

### Uses the following Docker containers:

- https://github.com/pi-hole/docker-pi-hole
- https://github.com/klutchell/dnscrypt-proxy

## Configuration

Edit `docker-compose.yml` in the following ways.

Uncomment `WEBPASSWORD` and put in a password, by default it will be randomized.

```yaml
WEBPASSWORD: 'password'
```

Uncomment `TZ` and put in your timezone, default is UTC.

- On Linux you can use `timedatectl list-timezones` to find the correct timezone.

```yaml
TZ: 'America/Chicago'
```

Edit `etc-dnscrypt-proxy/dnscrypt-proxy.toml` to your preference.

## Installation

1. Clone this repository to a directory of your choice.

    ```bash
    git clone https://gitlab.com/losuler/pihole-dnscrypt-docker
    ```

2. Edit `pihole-dnscrypt-docker.service` to point to the directory of the cloned repository.

    ```bash
    WorkingDirectory=/path/to/pihole-dnscrypt-docker
    ```

3. Copy the systemd service file.

    ```bash
    cp pihole-dnscrypt-docker.service /etc/systemd/system/
    ```

4. Reload the systemd manager configuration.

    ```bash
    systemctl daemon-reload
    ```

5. Enable and start the systemd service.

    ```bash
    systemctl enable --now pihole-dnscrypt-docker
    ```

## Updating images

1. To update all images used by this docker-compose.

    ```bash
    docker-compose pull
    ```

2. Restart the systemd service.

    ```bash
    systemctl restart pihole-dnscrypt-docker
    ```

List old/unused images.

```bash
docker images -f dangling=true
```

Remove old/unused images.

```bash
docker image prune
```

## Viewing logs

To view the status of the service.

```bash
systemctl status pihole-dnscrypt-docker
```

To view the entire log (append `-f` to view a live feed of the logs).

```bash
journalctl -u pihole-dnscrypt-docker
```

## Testing

To test the running of the docker-compose before running the service.

```bash
docker-compose up --force-recreate
```
