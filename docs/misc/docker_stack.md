
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

