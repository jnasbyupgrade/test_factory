test_factory
===============

A system for managing unit test data in Postgres.

Documentation for the most recent version is on [PGXN](http://pgxn.org/dist/test_factory/doc/test_factory.html).

[![PGXN version](https://badge.fury.io/pg/test_factory.svg)](https://badge.fury.io/pg/test_factory)
[![🐘 Postgres](https://github.com/decibel/test_factory/actions/workflows/ci.yml/badge.svg)](https://github.com/decibel/test_factory/actions/workflows/ci.yml)

Easy Installation
=================
Install [pgxn-client](http://pgxnclient.projects.pgfoundry.org/install.html), then do:

    pgxn install test_factory

or

    pgxn load -d database_name test_factory

(Run pgxn --help for more info.)

Hard Installation
=================

To build it, just do this:

    make
    make installcheck
    make install

If you encounter an error such as:

    "Makefile", line 8: Need an operator

You need to use GNU make, which may well be installed on your system as
`gmake`:

    gmake
    gmake install
    gmake installcheck

If you encounter an error such as:

    make: pg_config: Command not found

Be sure that you have `pg_config` installed and in your path. If you used a
package management system such as RPM to install PostgreSQL, be sure that the
`-devel` package is also installed. If necessary tell the build process where
to find it:

    env PG_CONFIG=/path/to/pg_config make && make installcheck && make install

And finally, if all that fails (and if you're on PostgreSQL 8.1 or lower, it
likely will), copy the entire distribution directory to the `contrib/`
subdirectory of the PostgreSQL source tree and try it there without
`pg_config`:

    env NO_PGXS=1 make && make installcheck && make install

If you encounter an error such as:

    ERROR:  must be owner of database regression

You need to run the test suite using a super user, such as the default
"postgres" super user:

    make installcheck PGUSER=postgres

Once test_factory is installed, you can add it to a database. If you're running
PostgreSQL 9.1.0 or greater, it's a simple as connecting to a database as a
super user and running:

    CREATE EXTENSION test_factory;

If you've upgraded your cluster to PostgreSQL 9.1 and already had test_factory
installed, you can upgrade it to a properly packaged extension with:

    CREATE EXTENSION test_factory FROM unpackaged;

For versions of PostgreSQL less than 9.1.0, you'll need to run the
installation script:

    psql -d mydb -f /path/to/pgsql/share/contrib/test_factory.sql

If you want to install test_factory and all of its supporting objects into a specific
schema, use the `PGOPTIONS` environment variable to specify the schema, like
so:

    PGOPTIONS=--search_path=extensions psql -d mydb -f test_factory.sql

Copyright and License
---------------------

Copyright (c) 2015 Jim Nasby <Jim.Nasby@BlueTreble.com>.

