# dokku-psql-single-container

dokku-psql-single-container is a plugin for [dokku][dokku] that provides a Postgresql server in a single container for your applications.

It uses the official Postgresql docker image (version 9.3).

## Installation

```
git clone https://github.com/Flink/dokku-psql-single-container /var/lib/dokku/plugins/psql-sc
dokku plugins-install
```


## Commands
```
$ dokku help
    psql:admin_console                              Launch a postgresql console as admin user
    psql:console     <app>                          Launch a postgresql console for <app>
    psql:create      <app>                          Create a Postgresql database for <app>
    psql:delete      <app>                          Delete Postgresql database for <app>
    psql:dump        <app> > <filename.dump>        Dump <app> database to PG dump format
    psql:list                                       List all databases
    psql:restart                                    Restart the Postgresql docker container
    psql:restore     <app> < <filename.*>           Restore database to <app> from any format exported by pg_dump
    psql:start                                      Start the Postgresql docker container if it isn't running
    psql:status                                     Shows status of Postgresql
    psql:stop                                       Stop the Postgresql docker container
    psql:url         <app>                          Get DATABASE_URL for <app>
```

## Info
This plugin adds the following environment variables to your app automatically (they are available via `dokku config`):

* DATABASE\_URL
* DB\_HOST
* DB\_NAME
* DB\_PASS
* DB\_PORT
* DB\_TYPE
* DB\_USER
* POSTGRESQL\_URL

## Usage

### Start PostgreSQL:
```
$ dokku psql:start                 # Server side
$ ssh dokku@server psql:start      # Client side
```

### Stop PostgreSQL:
```
$ dokku psql:stop                  # Server side
$ ssh dokku@server psql:stop       # Client side
```

### Restart PostgreSQL:
```
$ dokku psql:restart               # Server side
$ ssh dokku@server psql:restart    # Client side
```

### Create a new database for an existing app:
```
$ dokku psql:create foo            # Server side
$ ssh dokku@server psql:create foo # Client side
```

### Dump database:
```
$ dokku psql:dump foo > filename.dump # Server side
```

### Restore database from dump:
```
$ dokku psql:restore foo < filename.dump # Server side
```

### Copy database foo to database bar using pipe:
```
$ dokku psql:dump foo | dokku psql:restore bar # Server side
```

## Acknowledgements

This plugin is based originally on the [one by Olivier Hardy](https://github.com/ohardy/dokku-psql).

## License

This plugin is released under the MIT license. See the file [LICENSE](LICENSE).

[dokku]: https://github.com/progrium/dokku
