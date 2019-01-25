# OpenShift PostgreSQL Primary

This project contains the PostgreSQL Primary image for OpenShift.

## Getting Started

```bash
su -

# Start Docker
systemctl start docker

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
docker tag openshift-pgsql11-primary-centos7 $(minishift openshift registry)/myproject/openshift-pgsql11-primary-centos7

# Push the image to the registry
docker push $(minishift openshift registry)/myproject/openshift-pgsql11-primary-centos7
```

The image can be deployed through the [minishift](https://github.com/minishift/minishift/releases) web console,
using the `openshift-pgsql11-primary-centos7-template.json` template.

## Configuration

| Property | Default | Unit | Required | Description |
|----------|---------|------|----------|-------------|
| PG_DATABASE | | | Yes | The name of the database |
| PG_USER_NAME | | | Yes | The user name |
| PG_USER_PASSWORD | | | Yes | The password for the user |
| PG_REPLICATION_NAME | | | Yes | The replication user |
| PG_REPLICATION_PASSWORD | | | Yes | The password for the replication user |
| PG_NETWORK_MASK | | | Yes | The network mask for database access |
| PG_DATABASE_ENCODING | UTF8 | | | The encoding of the database |
| PG_MAX_CONNECTIONS | 100 | | | `max_connections` setting |
| PG_SHARED_BUFFERS | 256 | MB | | `shared_buffers` setting |
| PG_WORK_MEM | 8 | MB | | `work_mem` setting |
| PG_MAX_PARALLEL_WORKERS | 8 | | | `max_parallel_workers` setting |
| PG_EFFECTIVE_CACHE_SIZE | 1 | GB | | `effective_cache_size` setting |
| PG_MAX_WAL_SIZE | 1 | GB | | `max_wal_size` setting |
| PG_PASSWORD_ENCRYPTION | scram-sha-256 | | | `password_encryption` setting |
| PG_REPLICA1 | replica1 | | | Replication slot name 1 |
| PG_REPLICA2 | replica2 | | | Replication slot name 2 |
| PG_REPLICA3 | replica3 | | | Replication slot name 3 |
| PG_REPLICA4 | replica4 | | | Replication slot name 4 |
| PG_REPLICA5 | replica5 | | | Replication slot name 5 |

## Volumes

| Name | Description |
|------|-------------|
| `/pgconf` | Volume for SSL configuration |
| `/pgdata` | PostgreSQL data directory |
| `/pgwal` | PostgreSQL Write-Ahead Log (WAL) |

The data of each of these volumes is located within their `data` directory.

## SSL support

SSL support will be enabled when `/pgconf/data` contains the files `root.crt`, `server.crt` and `server.key`.

Remember to disable passphase such that the server can boot without a password prompt.

A guide to this can be found [here](https://www.howtoforge.com/postgresql-ssl-certificates).
Test and production environments should **NOT** be using self-signed certificates.
