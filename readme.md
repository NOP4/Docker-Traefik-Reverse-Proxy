# docker-compose for Traefik Reverse Proxy with let's encrypt, HSTS and autoconfiguration when deploying new containers.

Traefik is a reverse proxy which can be used for your docker containers. For more information on Traefik, visit https://traefik.io

This docker-compose file gives an example of deploying it without creating any configuration file. Everything is set-up using labels.

When you deploy applications, you'll never need to ajust the Traefik proxy, it will reconfigure itself to proxy your new apps.

This compose file will request let's encrypt certificate for your sites.


## Step 1 - Bridge network creation
Create a `traefik_web` bridge network.

## Step 2 - Firewall configuration

```
ufw allow http
ufw allow https
```

If it's not already done:
```
ufw allow ssh
ufw enable
```


## Step 3 - Docker-compose deployment
Adapt the docker-compose.yml file with your email address for let's encrypt notifications.

Deploy the docker-compose.yml as a standalone application. That means that all your applications will be in different stack. No need to have an all in one garbage one...

This can be done as a stack on portainer. That's it! Job done.


## Testing
To test it out, you can deploy another simple stack, such as the usage-example.yml provided.

This example stack will start an apache server to for a apache.exemple.com website, request for a let's encrypt TLS certificate and setup HSTS for you. Redirection of port 80 to 443 is already setup in the Traefik stack.

All you need is crate a "A" registry entry in your DNS records for the subdomain.


## Let's encrypt notes
Certificates will be renewed automatically, but in case you want to force a renewal, you can delete the letsencrypt container folder content and restart Traefik.
