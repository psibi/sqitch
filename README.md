# Instructions

* Actual setup here: https://metacpan.org/pod/distribution/App-Sqitch/lib/sqitchtutorial.pod

Some instructions needs to be modified:

* [Postgresql Password Change](https://stackoverflow.com/a/14588440/1651941)
* [Grant normal user privilege](https://dba.stackexchange.com/a/33291)
* [Allow login to new roles](https://stackoverflow.com/a/35255152/1651941)
* Command changes:

``` shellsession
$ sudo -u postgres psql
psql (10.5 (Ubuntu 10.5-0ubuntu0.18.04))
Type "help" for help.

postgres=# ALTER USER sibi CREATEDB;
ERROR:  role "sibi" does not exist
postgres=# CREATE ROLE sibi;
CREATE ROLE
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 sibi      | Cannot login                                               | {}

postgres=# ALTER USER sibi CREATEDB;
ALTER ROLE
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 sibi      | Create DB, Cannot login                                    | {}
postgres=# ALTER ROLE sibi WITH LOGIN;
postgres=# \q

$ createdb flipr_test

$ psql flipr_test -U sibi
psql (10.5 (Ubuntu 10.5-0ubuntu0.18.04))
Type "help" for help.

flipr_test=> \dn
  List of schemas
  Name  |  Owner
--------+----------
 flipr  | sibi
 public | postgres
 sqitch | sibi
(3 rows)
```


