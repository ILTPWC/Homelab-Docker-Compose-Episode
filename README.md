# ILTPWC - Episode "Whats running on my Raspberry PI"

This repository contains the sourcecode shown in the ILTPWC video [Whats running on my Raspberry PI as a home server](https://m.youtube.com/watch?v=ckvnHEIX4do).


# Use Case
The docker-compose file used within this repository spins up a lot of services in my home network.
I had to remove all the secrets (e.g. the data folders of my password manager) as well as all the API Tokens used with letsencrypt service.
If you want to use the docker-compose file you have to add your own URLs and credentials.

Host: Raspberry PI4 4gb
Architecture: armv7

## Prerequisite
The host needs to disable `sudo systemctl disable systemd-resolved` otherwise traefik can't route Port 53 to the PiHole instance
You have to replace all <ADD_YOUR_TOKEN>, <ADD_YOUR_MAIL>, <ADD_YOUR_PASSWORD> and <ADD_YOUR_URL> tags before you can docker-compose up -d
You also have to adjust the traefik.yml and change the provider from digitalocean to whatever provider you're using for dns
In order to access a password protected traefik you have to replace the <ADD_YOUR_HTPASSWD> with a user and password string that you have created as a passwd.
You can also start with a test username that uses a test password which would result in a string like "test: $apr1$z9jr06mo$KM0k/AemhwnvX3HyP4uhg"

## Installation
1. Checkout the sourcecode
2. modify acme.json file permissions `sudo chmod 600 ./data-traefik/acme.json`
3. sudo docker-compose up -d

If this is the first time you setup the services you need to set a password for pihole
1. Enter the containers Bash with `sudo docker exec -it pihole bash`
2. Generate a new password for pihole within the container `sudo pihole -a -p`

## Included services

- Traefik | The reverse proxy that handles SSL/TLS termination
- Portainer | Fancy Web Interface to manage Docker Containers (local and remote via agent)
- Vaultwarden | Password Manager
- Dashy | The Dashboard for your HomeNetwork
- Uptime | Small Service to do Healthchecks (deprecated in my setup because Dashy can also do that)
- Sshwiffty | Fancy SSH Terminal in your Browser
- MariaDB | In case you need a MySQL database that runs with ease on a raspberry pi
- Node-Red | Great for Home Automation
- https | Webserver for my docs-as-code library
- PiHole | The ad-block and DNS resolver for your raspberry pi (and every other server ;))
- CodeServer | An instance of VSCode to access from your browser
- Gogs | Lightweight git server on your raspberry pi
- HomeAssist | As the name suggested a great tool to automate your home
- Grafana | Great Dashboard to display metric based information
- Prometheus | Collects data to display on grafana
- RabbitMQ | The open source message broker that I use for home automation
- WatchTower | A great tool to keep your containers up to date

# Call to action
If you like what I do consider to (star & watch here on Github) or (like & subscribe to ILTPWC on YouTube)