# MongoDB Ops Manager Docker image

Produces a simple docker image to run MongoDB Ops Manager. Please consult the [MongoDB documentation](https://docs.opsmanager.mongodb.com/current/)
for the latest information about Ops Manager.

NOTE: the resulting container does not provide a MongoDB database for Ops Manager. A minimum
of one MongoDB instance will be required, though a replica set is recommended. More advanced
deployments are possible. Please consult [documentation](#official-documentation) for details.

## Version

1. Latest Version: 4.0.14.50550.20190730T1610Z-1

## Getting Started

### Get the image

```bash
docker pull grumblex/opsmanager
```

### Configuration

You must provide a database for the Ops Manager application. For simple trial installation, not recommended for production,
you could simply link a database to the instance.

1. A simple linked deployment:
```bash
docker run --name mongo  -d mongo:4
docker run -d -t \
  --name opsmanager \
  --link mongo \
  grumblex/opsmanager
```
1. Provide your own properties file with a custom config
```bash
docker run -d \
  --name mongodb-opsmgr \
  -v /home/user/ops-manager/conf/app.properties:/opt/mongodb/mms/conf/conf-mms.properties  \
  grumblex/opsmanager
```

### Connecting to Ops Manager

After starting up the Ops Manager container you will need to wait 3-5 minutes for the application to startup.
After the application finishes bootstrapping itself you can open a browser to `http://{DOCKER_HOST}:{OPS_MGR_PORT}`.
The default port is `8080` but can be changed by providing a different port when launching the container with the `-p` parameter.

## Building the Image

```bash
docker build ops-manager/
```

## Official Documentation
- [Ops Manager Overview](https://docs.opsmanager.mongodb.com/current/application/)
- [Installation Guide](https://docs.opsmanager.mongodb.com/current/installation/)
- [Hardware and Software Requirements](https://docs.opsmanager.mongodb.com/current/core/requirements/)
- [Advanced Configuration Options](https://docs.opsmanager.mongodb.com/current/tutorial/nav/advanced-deployments/)
