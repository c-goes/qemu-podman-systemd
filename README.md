# qemu-podman-systemd

QEMU systemd in rootless podman container.

Small PoC to run a Podman systemd container for another architecture.


Using the [containers images from Balena](https://www.balena.io/blog/building-arm-containers-on-any-x86-machine-even-dockerhub/) including a [qemu with a new flag `execve`](https://github.com/balena-io/qemu) it is possible to containerize a complete system for another architecture in a rootless Podman container.


## build the container

```
podman build -t localhost/debian-arm .
```

## start systemd in container

```
podman run --systemd=always --rm --name=debian-arm  --entrypoint=/usr/bin/qemu-arm-static -it localhost/debian-arm -execve -0 /sbin/init /sbin/init
```

## run a shell

```
podman exec -it debian-arm /usr/bin/qemu-arm-static -execve /bin/bash
```