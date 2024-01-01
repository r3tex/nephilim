# Exosomatic Layer

This image is built on a Clear Linux [image](https://hub.docker.com/_/clearlinux/) with a [Julia Language](https://julialang.org/) runtime.

## Build instructions

```
sudo singularity build macrothymic.sif Singularity
```

## Run instructions

```
sudo ingularity instance start \
--bind /mnt/optane1/macrothymic/var/run/redis:/var/run/redis \
--bind /mnt/optane1/macrothymic/var/lib/redis:/var/lib/redis \
--bind /mnt/optane1/macrothymic/var/log/redis:/var/log/redis \
--env PORT=8081 macrothymic.sif macrothymic
```

## Networking

Redis uses the following default ports:
```
Port	Purpose
6379	Client TCP
```

## Data Schema

### Keyspace X TODO
```
one, two, three TODO
```