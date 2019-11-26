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

3. Optionally edit `docker-compose.yml` and uncomment `WEBPASSWORD` with a password of your choice:

```
WEBPASSWORD: 'secure-password'
```

4. Optionally edit `etc-dnscrypt-proxy/dnscrypt-proxy.toml` to your preference.

5. Reload the systemd manager configuration:

```
sudo systemctl daemon-reload
```

6. Copy the systemd service file:

```
sudo cp pihole-dnscrypt-docker.service /usr/lib/systemd/system/
```

7. Enable the systemd service:

```
sudo systemctl enable pihole-dnscrypt-docker
```

8. Start the systemd service:

```
sudo systemctl start pihole-dnscrypt-docker
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
