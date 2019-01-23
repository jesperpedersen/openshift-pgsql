# OpenShift PostgreSQL

This repository contains [PostgreSQL](https://www.postgresql.org) images for [OpenShift](https://www.openshift.com/).

The images makes use of

* [OpenShift S2I CentOS](https://hub.docker.com/r/centos/s2i-core-centos7/) 7
* [PostgreSQL](https://www.postgresql.org) 11.x
* Community provided RPMs through [yum.postgresql.org](https://yum.postgresql.org)
* Checksum for `PGDATA`
* SCRAM-SHA256 password encryption by default
* SSL support
* `pg_stat_statements` integration
* Asynchronous replication, up to 6 slaves
* Volumes for `/pgconf`, `/pgdata` and `/pgwal`

Features that should be added

* Synchronous replication with `remote_apply`
* Additional GUCs
* Backup using [barman](https://www.pgbarman.org)
* [pgpool-II 4.0 image](http://www.pgpool.net)

Images are provided **`AS IS`** according to the license agreement with
no guarantees of correctness and stability.

## License

All images are released under the MIT license.

## Author

Jesper Pedersen

jesper (dot) pedersen (at) redhat (dot) com
