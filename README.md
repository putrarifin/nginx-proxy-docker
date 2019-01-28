# Docker + Letsencrypt + nginx proxy

## How to install

Start the solution, go to the ```nginx-proxy``` folder and launch

```bash
docker-compose up -d
```

Set the path root settings in the ```example.env```

```
PATH_ROOT=/home/user/docker/
```

## Link a website to the reverse-proxy
To link a website to the running nginx-proxy, we need to update its own

1 Environment variables
```
services:
  my-app: 
    …
    environment:
      VIRTUAL_HOST: your-website.tld 
      VIRTUAL_PORT: 3000
      LETSENCRYPT_HOST: your-website.tld
      LETSENCRYPT_EMAIL: your-email@domain.tld
```

VIRTUAL_HOST: your domain name, used in the nginx configuration.
VIRTUAL_PORT: (opt.) the port your website is listening to (default to 80).
LETSENCRYPT_HOST: your domain name, used in the Let’s Encrypt configuration.
LETSENCRYPT_EMAIL: your email, used in the Let’s Encrypt configuration.

2. Ports
```
services:
  my-app: 
    …
    expose:
      - 3000
```
Same as the VIRTUAL_PORT above.

3.Network
```
networks:
  default:
    external:
      name: nginx-proxy
```

## Now lets start the website with:

```
$ cd /home/user/docker/your-website.tld
$ docker-compose up -d
```
