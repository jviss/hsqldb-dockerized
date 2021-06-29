# HSQLDB in a Docker Image
Exactly what it says on the tin. Useful in Spring and other Java applications. This image uses OpenJDK 16 on a slim Debian Buster.

## Release: joseviss/hsqldb:latest

# Quick Start

```
$ docker run -d -p 9001:9001 --name hsqldb joseviss/hsqldb
```

Connection Details: 
- URL: `jdbc:hsqldb:hsql://localhost/test`
- Username: sa
- Password: (blank)

# Docker Compose

This image is optimized for use with docker compose.

# Set Username and Password

You can specify the Username and Password with the environment variables `HSQLDB_USER` and `HSQLDB_PASSWORD`.

## Example:

```
$ docker run -d --name hsqldb \
	-e "HSQLDB_USER=sa" \
  	-e "HSQLDB_PASSWORD=password" \
	-p 9001:9001 \
	mitchtalmadge/hsqldb
```

## Default Credentials

If you do not set the environment variables, the defaults are:
- Username: sa
- Password: (blank)

# Set the Database alias

You can adjust the Database Alias with the environment variable: `HSQLDB_DATABASE_ALIAS`

This will change the JDBC URL.

Example:

```
$ docker run -d --name hsqldb \
	-e "HSQLDB_DATABASE_ALIAS=example" \
	-p 9001:9001 \
	mitchtalmadge/hsqldb
```

> The correct JDBC URL is now: jdbc:hsqldb:hsql://localhost/example

# Set the Database Name

You can specify the Database Name with the environment variable `HSQLDB_DATABASE_NAME`

Example:

```
$ docker run -d --name hsqldb \
	-e "HSQLDB_DATABASE_NAME=hsqldb" \
	-p 9001:9001 \
	mitchtalmadge/hsqldb
```

> Database hsqldb will be available in folder /opt/database

# Mount the Database Files Externally

The database files are inside the volume /opt/database and can be mounted.

Example:

```
$ docker run -d --name hsqldb \
	-v ./database:/opt/database \
	-p 9001:9001 \
	mitchtalmadge/hsqldb
```

# Additional HSQLDB Parameters

This container supports the following additional settings:

* Disable HSQL Trace Mode (do not display JDBC trace messages): `HSQLDB_TRACE="false"`
* Enable HSQL Silent Mode (true => do not display all queries): `HSQLDB_SILENT="true"`
* Disable HSQL Remote Connections (can open databases remotely): `HSQLDB_REMOTE="false"`

Example:

```
$ docker run -d --name hsqldb \
  -e "HSQLDB_TRACE=false" \
  -e "HSQLDB_SILENT=true" \
  -e "HSQLDB_REMOTE=false" \
  -p 9001:9001 \
  mitchtalmadge/hsqldb
```

# Java-VM Parameters

You can define start up parameters for the Java Virtual Machine, e.g. setting the memory size.

```
$ docker run -d --name hsqldb \
	-e "JAVA_VM_PARAMETERS=-Xmx512m -Xms256m" \
	-p 9001:9001 \
	mitchtalmadge/hsqldb
```

# References

* [HSQLDB](http://hsqldb.org/)
