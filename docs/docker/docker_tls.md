
# Enable remote Docker daemon access

Following instructions refer to *Amazon Linux 2* as OS. The *Amazon Linux 2* is a RedHat derived distribution, which uses **systemd**.


## Creating CA / keys

In order to create all the needed certificates and keys, I followed the [official Docker documentation](https://docs.docker.com/engine/security/protect-access/#create-a-ca-server-and-client-keys-with-openssl).

Note that you can replace the *$HOST* variable using an IP address instead of an alphanumeric address.

Note that, when creating the `extfile.cnf`, you need to set all the IPs of the host machine ( public, internal, loopback) and all the IPs of the client machines:

```
echo subjectAltName = DNS:54.154.116.228,IP:54.154.116.228,IP:127.0.0.1,IP:172.16.36.85,IP:88.51.227.81,IP:217.56.224.72 >> extfile.cnf
```

In this case, host IPS are:

- 54.154.116.228
- 127.0.0.1
- 172.16.36.85

While client IPs are:

- 88.51.227.81
- 217.56.224.72


For general reference: [Docker documentation](https://docs.docker.com/engine/security/protect-access/)


## Modify Docker configuration

Then we need to enable Docker socket. We do that creating / modifying the file `/etc/docker/daemon.json`:

```json
{
        "tls": true,
        "tlsverify": true,
        "tlscacert": "/mnt/seven/docker-certs/ca.pem",
        "tlscert": "/mnt/seven/docker-certs/server-cert.pem",
        "tlskey": "/mnt/seven/docker-certs/server-key.pem",
        "hosts": ["unix:///var/run/docker.sock", "tcp://0.0.0.0:2376"]
}
```

In this file you specify:

- the position of the certificates / keys
- the port on which the docker socket will be listening


## Modify Docker daemon startup script

Since I had problem starting the Docker daemon after creating the above file, upon inspecting systemctl errors:

`journaltctl -xe`

I found that Systemd is "unable to configure the Docker daemon with file /etc/docker/daemon.json: the following directives are specified both as a flag and in the configuration file ...".

So I had to modify the systemd Docker startup script `/usr/lib/systemd/system/docker.service`:

```script
#ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock $OPTIONS $DOCKER_STORAGE_OPTIONS $DOCKER_ADD_RUNTIMES
ExecStart=/usr/bin/dockerd --containerd=/run/containerd/containerd.sock $OPTIONS $DOCKER_STORAGE_OPTIONS $DOCKER_ADD_RUNTIMES
```

