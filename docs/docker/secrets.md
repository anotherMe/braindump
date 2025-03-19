
To reference a Docker secret in docker-compose.yml, follow these steps:

## Create the secret

```bash
echo "your_token_here" | docker secret create github_token -
```


## Reference the secret

Define the secret in docker-compose.yml:

```yaml
version: '3.7'

services:
  my-service:
    image: my-image
    deploy:
      replicas: 1
      restart_policy:
        condition: on-failure
    secrets:
      - github_token

secrets:
  github_token:
    external: true
```



## Access the secret

The secret will be available as a file in /run/secrets/github_token inside the container:

```bash
cat /run/secrets/github_token
```
