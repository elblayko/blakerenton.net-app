The proxy service automatically tracks the expiry date of ACME certificates it generates.  If there are less than 30 days remaining before the certificate expires, Traefik will attempt to renew it automatically.  Configuration for other DNS providers can be found at https://doc.traefik.io/traefik/https/acme/#dnschallenge

## Configure secrets:

`traefik/.env`:
```
CF_API_EMAIL=mail@domain.com
CF_API_KEY=cloudflare-api-key
```

```
chmod 600 .env
```

The TLS/SSL certificate is stored at `traefik/acme.json`. It is provided as a bind-mount to the container and correct permissions are required or it will be ignored.

`acme.json`:
```
touch traefik/acme.json
chmod 600 traefik/acme.json
```

# Usage:

```
# Traefik should be the first service up.
cd traefik && docker compose up -d

# Start remaining services.
cd home && docker compose up -d
```
