## The environment file

Traefik uses environment variables to request a certificate from the CA. When using Cloudflare for DNS, Traefik will look for `CF_API_EMAIL` and `CF_API_KEY` environment variables. Additional configuration for other DNS providers can be found at https://doc.traefik.io/traefik/https/acme/#dnschallenge

.env:

```
CF_API_EMAIL=hello@email.com
CF_API_KEY=my-api-key
```

## acme.json

This is where the certificate from the CA will be stored. It is provided as a bind-mount to the container and correct permissions are required, else it will be ignored. Use `chmod 600 acme.json`. Traefik automatically tracks the expiry date of ACME certificates it generates.  If there are less than 30 days remaining before the certificate expires, Traefik will attempt to renew it automatically.
