## Install PostgreSQL

Tanserver currently only supports [PostgreSQL](https://www.postgresql.org/download/), which allows you to establish a long-term database connection to improve performance, and will automatically reconnect when the connection is broken.

After installing PostgreSQL locally, you can connect to `127.0.0.1:5432`.

## Edit configuration file

Edit `/etc/tanserver.conf`

``` linenums="1"
database {
#	pgsql {
#		hostaddr = 127.0.0.1
#		port = 5432
#
#		user = postgres
#		password = postgres
#
#		database = postgres
#	}
}
```

Delete `#` and change to your PostgreSQL information.

!!! note
    Your pgSQL version should >= `9.2`.
