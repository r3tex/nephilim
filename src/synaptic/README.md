# Synaptic Layer

## Build instructions

```
sudo singularity build synaptic.sif Singularity
```

## Run instructions

```
sudo singularity instance start \
--env PORT=9092 --env PORT=9644 synaptic.sif synaptic
```

## Networking

Redpanda uses the following default ports:
```
Port	Purpose
9092	Kafka API
8082	HTTP Proxy
8081	Schema Registry
9644	Admin API and Prometheus
33145	internal RPC
```

## Data Schema

### Topic X TODO
```
one, two, three TODO
```