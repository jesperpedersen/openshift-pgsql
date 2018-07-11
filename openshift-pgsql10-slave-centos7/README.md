# OpenShift PostgreSQL Slave

This project contains the PostgreSQL Slave image for OpenShift.

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
docker tag openshift-pgsql10-slave-centos7 $(minishift openshift registry)/myproject/openshift-pgsql10-slave-centos7

# Push the image to the registry
docker push $(minishift openshift registry)/myproject/openshift-pgsql10-slave-centos7
```

## Configuration

| Property | Default | Unit | Required | Description |
|----------|---------|------|----------|-------------|
| PG_MASTER | | | Yes | The IP of the master |
| PG_REPLICATION_NAME | | | Yes | The replication user |
| PG_REPLICATION_PASSWORD | | | Yes | The password for the replication user |

## SSL support

SSL support will be enabled when `/pgconf/data` contains the files `root.crt`, `postgresql.crt` and `postgresql.key`.

Remember to disable passphase such that the server can boot without a password prompt.

A guide to this can be found [here](https://www.howtoforge.com/postgresql-ssl-certificates).
Test and production environments should **NOT** be using self-signed certificates.
