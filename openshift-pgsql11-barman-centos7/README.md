# OpenShift PostgreSQL Replica

This project contains the PostgreSQL Barman image for OpenShift.

## Getting Started

```bash
su -

# Start minishift, and note the URL for the web console
minishift start

# Set the Docker environment variables
eval $(minishift docker-env)

# Login into OpenShift (developer / whatever)
oc login

# Login into Docker registry
docker login -u developer -p $(oc whoami -t) $(minishift openshift registry)

# Make the container
make

# Create a Docker tag
docker tag openshift-pgsql11-barman-centos7 $(minishift openshift registry)/myproject/openshift-pgsql11-barman-centos7

# Push the image to the registry
docker push $(minishift openshift registry)/myproject/openshift-pgsql11-barman-centos7
```

The image can be deployed through the [minishift](https://github.com/minishift/minishift/releases) web console,
using the `openshift-pgsql11-barman-centos7-template.json` template.

## Configuration

| Property | Default | Unit | Required | Description |
|----------|---------|------|----------|-------------|
| PG_MASTER | | | Yes | The IP of the master |
| PG_DATABASE | | | Yes | The name of the database |
| PG_REPLICATION_PASSWORD | | | Yes | The password for the replication user |

## Volumes

| Name | Description |
|------|-------------|
| `/pgconf` | Volume for configuration |
| `/pgbackup` | Volume for backup |
