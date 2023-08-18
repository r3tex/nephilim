# Macrothymic Layer

Redis needs to be run as root on the system.

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