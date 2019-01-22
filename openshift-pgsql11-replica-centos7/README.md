# OpenShift PostgreSQL Replica

This project contains the PostgreSQL Replica image for OpenShift.

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
docker tag openshift-pgsql11-replica-centos7 $(minishift openshift registry)/myproject/openshift-pgsql11-replica-centos7

# Push the image to the registry
docker push $(minishift openshift registry)/myproject/openshift-pgsql11-replica-centos7
```

The image can be deployed through the [minishift](https://github.com/minishift/minishift/releases) web console,
using the `openshift-pgsql11-replica-centos7-template.json` template.

## Configuration

| Property | Default | Unit | Required | Description |
|----------|---------|------|----------|-------------|
| PG_MASTER | | | Yes | The IP of the master |
| PG_DATABASE | | | Yes | The name of the database |
| PG_USER_NAME | | | Yes | The user name |
| PG_REPLICATION_NAME | | | Yes | The replication user |
| PG_REPLICATION_PASSWORD | | | Yes | The password for the replication user |
| PG_SLOT_NAME | | | Yes | The replication slot name |

## SSL support

SSL support will be enabled when `/pgconf/data` contains the files `root.crt`, `postgresql.crt` and `postgresql.key`.

Remember to disable passphase such that the server can boot without a password prompt.

A guide to this can be found [here](https://www.howtoforge.com/postgresql-ssl-certificates).
Test and production environments should **NOT** be using self-signed certificates.
