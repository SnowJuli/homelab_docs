# homelab_docs

## Requirements

- [ ] Ansible
  - Secrets
  - SSH Key
- [ ] Docker ([not managed by snap](https://askubuntu.com/questions/907110/docker-snap-cannot-connect-to-the-docker-daemon-is-the-docker-daemon-running-o))

## Cheatsheet

```yaml
    labels:
      - 'traefik.enable=true'
      # Service HTTP
      - 'traefik.http.routers.service.entrypoints=http'
      - 'traefik.http.routers.service.rule=Host(`service.domain`)'
      - 'traefik.http.middlewares.service.redirectscheme.scheme=https'
      - 'traefik.http.middlewares.service.redirectscheme.permanent=false'
      - 'traefik.http.routers.service.service=noop@internal'
      # Service HTTPS
      - 'traefik.http.routers.-secure.entrypoints=https'
      - 'traefik.http.routers.service-secure.rule=Host(`service.domain`)'
      - 'traefik.http.routers.service-secure.service=service-ui'
      - 'traefik.http.routers.service-secure.tls=true'
      - 'traefik.http.routers.service-secure.tls.domains=service.domain'
      - 'traefik.http.services.service-ui.loadBalancer.server.port=6969'
      - 'traefik.http.services.service-ui.loadBalancer.passHostHeader=true'
```

```yaml
networks:
  default:
    name: traefik_default
    external: true
```
