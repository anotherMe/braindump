
# Docker stack

## Cookbook

### Restart specific service in docker swarm stack

You'll have to retrieve the service ID first:

```bash
$ docker stack services <stack_name>

ID                  NAME              ...
3xrdy2c7pfm3        stack-name_api    ...
```

then you can:

```bash
$ docker service update --force 3xrdy2c7pfm3
```

### List running processes

```bash
docker stack ps YOUR_STACK_NAME
```

or, using a filter:

```bash
docker stack ps -f "desired-state=running" YOUR_STACK_NAME
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


