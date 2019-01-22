# OpenShift PostgreSQL

This repository contains [PostgreSQL](https://www.postgresql.org) images for [OpenShift](https://www.openshift.com/).

**DEPRECATED; Only images on `master` branch are maintained**

The images makes use of

* [OpenShift S2I CentOS](https://hub.docker.com/r/centos/s2i-core-centos7/) 7
* [PostgreSQL](https://www.postgresql.org) 10.x
* Community provided RPMs through [yum.postgresql.org](https://yum.postgresql.org)
* Checksum for `PGDATA`
* SCRAM-SHA256 password encryption by default
* SSL support
* `pg_stat_statements` integration
* Asynchronous replication, up to 6 slaves
* Backup using [pgbackrest](https://pgbackrest.org) including Point-in-Time recovery
* Volumes for `/pgconf`, `/pgdata`, `/pgwal` and `/pgbackup`

Features that should be added

* Synchronous replication with `remote_apply`
* Additional GUCs
* [pgpool-II 4.0 image](http://www.pgpool.net)

Images are provided **`AS IS`** according to the license agreement with
no guarantees of correctness and stability.

## License

All images are released under the MIT license.

## Author

Jesper Pedersen

jesper (dot) pedersen (at) redhat (dot) com
