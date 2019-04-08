# Boilerplate for nginx with Let’s Encrypt on docker-compose

> This repository is accompanied by a [step-by-step guide on how to
set up nginx and Let’s Encrypt with Docker](https://medium.com/@pentacent/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71).

`init-letsencrypt.sh` fetches and ensures the renewal of a Let’s
Encrypt certificate for one or multiple domains in a docker-compose
setup with nginx.
This is useful when you need to set up nginx as a reverse proxy for an
application.

## Installation
1. [Install docker-compose](https://docs.docker.com/compose/install/#install-compose).


2. Clone this repository: `git clone https://github.com/Stores-Discount/nginx-certbot .`

3. Set the domain you want to secure

```
export OS_DOMAIN="<DOMAIN>"
# Eg: export OS_DOMAIN="api.dev.olst.io"
```


3. Generate proxy VHOST config file

```bash
mkdir -p data/nginx/
sed "s/__DOMAIN_NAME__/$OS_DOMAIN/g" template/nginx/template.conf > data/nginx/$OS_DOMAIN.conf
```

4. Run init the script:

```
chmod +x ./init-letsencrypt.sh
./init-letsencrypt.sh $OS_DOMAIN
```

5. Run server:

`docker-compose up -d`

6. Clean global vars:

`unset OS_DOMAIN`


## License
All code in this repository is licensed under the terms of the `MIT License`. For further information please refer to the `LICENSE` file.
