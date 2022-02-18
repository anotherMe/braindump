
# Docker stack

## Cookbook

### Restart one service in docker swarm stack

```bash
$ docker stack services <stack_name>
ID                  NAME              ...
3xrdy2c7pfm3        stack-name_api    ...
```

```bash
$ docker service update --force 3xrdy2c7pfm3
```


### Ottenere l'IP di un nodo

```bash
docker node inspect <node id> --format '{{ .Status.Addr  }}'
```


### Add to existing stack

Add services specified in `new-services.yml` to stack `vossibility`:

```bash
docker stack deploy --compose-file new-services.yml vossibility
```


