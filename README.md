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
      - 'traefik.http.routers.replace.entrypoints=http'
      - 'traefik.http.routers.replace.rule=Host(`replace.domain`)'
      - 'traefik.http.middlewares.replace.redirectscheme.scheme=https'
      - 'traefik.http.middlewares.replace.redirectscheme.permanent=false'
      - 'traefik.http.routers.replace.service=noop@internal'
      # Service HTTPS
      - 'traefik.http.routers.replace-secure.entrypoints=https'
      - 'traefik.http.routers.replace-secure.rule=Host(`replace.domain`)'
      - 'traefik.http.routers.replace-secure.service=replace-ui'
      - 'traefik.http.routers.replace-secure.tls=true'
      - 'traefik.http.routers.replace-secure.tls.domains=replace.domain'
      - 'traefik.http.services.replace-ui.loadBalancer.server.port=6969'
      - 'traefik.http.services.replace-ui.loadBalancer.passHostHeader=true'
```

```yaml
networks:
  network1:
    name: proxy
    external: true
```
