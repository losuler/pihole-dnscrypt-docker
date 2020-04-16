# Pi-hole DNSCrypt Docker

## About

A docker-compose for Pi-hole and DNSCrypt, daemonized with a systemd service file. 

### Uses the following Docker containers:

https://github.com/pi-hole/docker-pi-hole

https://github.com/klutchell/dnscrypt-proxy

## Dependencies

```
docker
docker-compose
```

## Installation

1. Clone this repository to a directory of your choice:

    ```
    git clone https://gitlab.com/losuler/pihole-dnscrypt-docker
    ```

2. Edit `pihole-dnscrypt-docker.service` to point to the directory of the cloned repository:

    ```
    WorkingDirectory=/path/to/pihole-dnscrypt-docker
    ```

3. (Optional) Edit `docker-compose.yml`:

    Uncomment `WEBPASSWORD` and put in a password, by default it will be randomized.

    ```
    WEBPASSWORD: 'password'
    ```

    Uncomment `TZ` and put in your timezone (see `timedatectl list-timezones`), default is UTC.

    ```
    TZ: 'America/Chicago'
    ```

4. (Optional) Edit `etc-dnscrypt-proxy/dnscrypt-proxy.toml` to your preference.

5. Copy the systemd service file:

    ```
    sudo cp pihole-dnscrypt-docker.service /etc/systemd/system/
    ```

6. Reload the systemd manager configuration:

    ```
    sudo systemctl daemon-reload
    ```

7. Enable the systemd service:

    ```
    sudo systemctl enable pihole-dnscrypt-docker
    ```

8. Start the systemd service:

    ```
    sudo systemctl start pihole-dnscrypt-docker
    ```

## Updating images

1. To update all images used by this docker-compose:

    ```
    sudo docker-compose pull
    ```

2. Restart the systemd service:

    ```
    sudo systemctl restart pihole-dnscrypt-docker
    ```

3. (Optional) List old/unused images:

    ```
    sudo docker images -f dangling=true
    ```

4. (Optional) Remove old/unused images:

    ```
    sudo docker image prune
    ```

## Viewing logs

To view the status of the service:

```
sudo systemctl status pihole-dnscrypt-docker
```

To view the entire log (append `-f` to view a live feed of the logs):

```
sudo journalctl -u pihole-dnscrypt-docker
```

## Testing

To test the running of the docker-compose before running the service:

```
sudo docker-compose up --force-recreate
```
