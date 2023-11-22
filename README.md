<center> <u> <h1 style="font-size: 50px;"> POSTGRESQL SETUP</h1> </u> </center>



## Table of contents



**1. Task requirement**

**2. Tools Use**

**3. Environment details**

**4. System configuration**

**5. Definition of tools**



## 1. Task requirement: 
-  Create a postgresql container using podman
-  Create users,databases,tables and extensions on the same.
-  Perform crud operations.
-  Create three users with a password.
-  Grant select permission for user1,select,insert,delete for user2 and all for user3.
-  Understanding the table structure,finding database size, table size etc.



## 2. Tools use:

- Podman
- Postgres


## 2. Environment details (minimum): 

- OS- Ubuntu 22.04.3 LTS (Download Link Here ) (https://ubuntu.com/download/desktop) 
- Podman- 3.4.4 
- Psql- (PostgreSQL) 14.9


## Minimum System Requirements for PostgreSQL:

- **CPU:** Dual-core processor
  

- **RAM:** 2 GB

- **Storage:** 20 GB




## 4. Definition of tools:

- **Podman** is an open-source container management tool used to create, run, and manage containers on Linux systems.

- **PostgreSQL** is an open-source relational database management system (RDBMS)
which is used for data storage and management.


## System update

```
sudo apt-get update
```

## input

```
- https://brave-browser-apt-release.s3.brave.com stable InRelease
Hit:1 Hit:2 http://in.archive.ubuntu.com/ubuntu jammy InRelease
Get:3 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:4 http://in.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB] Get:5 http://security.ubuntu.com/ubuntu jammy-security/main amd64 DEP-11 Metadata [43.0 KB]
Get:6 http://in.archive.ubuntu.com/ubuntu jammy-backports InRelease [109 kB]
Get:7 http://security.ubuntu.com/ubuntu jammy-security/universe amd64 DEP-11 Metadata [55.1 kB]
Get:8
http://in.archive.ubuntu.com/ubuntu jammy-updates/main i386 Packages [523 kB]
Get:9 http://in.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages [1,148 kB]
Get:10 Get:11 http://in.archive.ubuntu.com/ubuntu jammy-updates/main Translation-en [245 kB] http://in.archive.ubuntu.com/ubuntu jammy-updates/main amd64 DEP-11 Metadata [101 kB]
Get:12 http://in.archive.ubuntu.com/ubuntu jammy-updates/restricted amd64 Packages [1,103 kB]
Get:13 http://in.archive.ubuntu.com/ubuntu jammy-updates/restricted Translation-en [179 kB]
Get:14 Get:15 http://in.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 DEP-11 Metadata [305 kB] http://in.archive.ubuntu.com/ubuntu jammy-updates/multiverse amd64 DEP-11 Metadata [940 B]
Get:16 http://in.archive.ubuntu.com/ubuntu jammy-backports/main amd64 DEP-11 Metadata [4,940 B]
Get:17 http://in.archive.ubuntu.com/ubuntu jammy-backports/universe amd64 DEP-11 Metadata [18.8 kB]
Fetched 4,064 kB in 15s (268 kB/s) Reading package lists... Done
```



- **sudo:** "Sudo" stands for "Superuser Do." It is used in Linux to execute a command as the root (admin) user, allowing the command to run with root privileges.


- **apt-get:** This is a command used for package management on Linux. It helps in acquiring, installing, removing, and updating packages in the package management system.

- **update:** The "update" in this command is used to refresh the package management database with information about new packages. It provides the user with information about new packages and their versions, allowing them to be installed on the system.




## 1. Create a postgres container using podman

```
sudo apt install -y podman

```
## input

```
Reading package lists... Done
Building dependency tree... Done Reading state information... Done
Suggested packages:
containers-storage docker-compose
The following NEW packages will be installed:
podman
0 upgraded, 1 newly installed, o to remove and 2 not upgraded.
Need to get 10.6 MB of archives.
After this operation, 36.5 MB of additional disk space will be used.
Get:1 http://in.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 podman amd64 3.4.4+ds1-1ubuntu1.22.04.2 [10.6 MB]
Fetched 10.6 MB in 4s (2,722 kB/s)
Selecting previously unselected package podman.
(Reading database... 198982 files and directories currently installed.) Preparing to unpack.../podman_3.4.4+ds1-1ubuntu1.22.04.2_amd64.deb
Unpacking podman (3.4.4+ds1-1ubuntu1.22.04.2).."
Setting up podman (3.4.4+ds1-1ubuntu1.22.04.2)
Created symlink /etc/systemd/user/default.target.wants/podman.service Created symlink /etc/systemd/user/sockets.target.wants/podman.socket /usr/lib/systemd/user/podman.service.
/usr/lib/systemd/user/podman.socket. Created symlink /etc/systemd/system/default.target.wants/podman.service/lib/systemd/system/podman.service.
Created symlink /etc/systemd/system/sockets.target.wants/podman.socket/lib/systemd/system/podman.socket.
Created symlink /etc/systemd/system/default.target.wants/podman-auto-update.service/lib/systemd/system/podman-auto-update.service.
Created symlink /etc/systemd/system/timers.target.wants/podman-auto-update.timer/lib/systemd/system/podman-auto-update.timer. Created symlink /etc/systemd/system/default.target.wants/podman-restart.service/lib/systemd/system/podman-restart.service.
Processing triggers for man-db (2.10.2-1)...
prince@123:-$
```

```
podman version
```

## input 

```
Version: 3.4.4
API Version: 3.4.4
Go Version:
go1.18.1
Built:
Thu Jan 1 05:30:00 1970
OS/Arch:
linux/amd64
```


```
podman run --name postgres-container -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 docker.io/library/postgres:latest

```
```
prince@123:-$ podman run-name postgres-container -e POSTGRES_PASSWORD=mysecretpassword dp 5432:5432 docker.to/library/postgres: latest 413a4432f26d5fb9f7358c447c17502b66054a0e1aa35a09fd67d628731502e2
prince@123:-$
```

- **podman run:** This is the command used to run containers with Podman, an alternative containerization tool to Docker.

- **--name postgres-container:** This option specifies a custom name ("postgres-container") for the container. You can refer to the container by this name.

- **-e POSTGRES_PASSWORD=mysecretpassword:** This option sets an environment variable named "POSTGRES_PASSWORD" with the value "mysecretpassword." This is typically used to configure the password for the PostgreSQL database within the container.

- **-d:** This option runs the container in detached mode, which means it runs in the background, and you get the terminal prompt back for further commands.

- **-p 5432:5432:** This option maps port 5432 from the host to port 5432 inside the container. This allows you to access the PostgreSQL server running in the container through port 5432 on your host machine.

- **docker.io/library/postgres:latest:** This is the image name. It specifies the Docker image you want to run. In this case, it's "postgres" from the "library" repository on Docker Hub, using the "latest" tag.







## Verify that the PostgreSQL container is running:

```
podman ps
```
```
prince@123:-$ podman ps
CONTAINER ID IMAGE
COMMAND
CREATED
STATUS
PORTS
docker.to/library/postgres:
postgres
15 seconds ago
Up 15 seconds ago
NAMES
413a4432f26d
prince@123:-$
latest
0.0.0.0:5432->5432/tcp
postgres-container
```

## Connect Postgres container


```
podman exec -it postgres-container psql -U postgres

```
```
prince@123:-$ podman execit postgres-container psql -U postgres psql (16.0 (Debian 16.0-1.pgdg120+1))
Type "help" for help.
postgres=#
```

- **podman:** This is the command-line tool for managing containers, similar to Docker.

- **exec:** This subcommand is used to execute a command within a running container.

- **-it:** These are options commonly used in container management to interact with the container's terminal (interactive mode).

- **postgres-container:** This is the name or ID of the container in which you want to execute the command.

- **psql -U postgres:** This is the command you want to execute inside the container. It's running the PostgreSQL command-line tool (psql) and connecting to the PostgreSQL database using the postgres user.




## 2.Create users,databases,tables and Extensions on the same.




## (a) Create Users
```
CREATE USER noida WITH PASSWORD 'noida1';
CREATE USER delhi WITH PASSWORD 'delhi1';
CREATE USER gurugram WITH PASSWORD 'gurugram1';
```
```
postgres # CREATE USER noida WITH PASSWORD 'noidal';
CREATE USER delht WITH PASSWORD delhii'; CREATE USER gurugram WITH PASSWORD 'gurugram1';
CREATE ROLE
CREATE ROLE
CREATE ROLE
postgres=#
```


## (b) Databases
```
CREATE DATABASE my_database;

```
```
postgres=# CREATE DATABASE my_database;
CREATE DATABASE
postgres=#
```


## (c) Tables

- connect database

```
\c my_database;
```


```
     CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100) UNIQUE
);

```
```
my_database=#
CREATE TABLE users (
id SERIAL PRIMARY KEY, first_name VARCHAR(50), last_name VARCHAR(50), email VARCHAR(100) UNIQUE
);
CREATE TABLE my_database=#
```

- **CREATE TABLE:** This keyword tells the database to create a new table.
  
- **my_table:** This is the name of the table that is being created.

- **id SERIAL NOT NULL PRIMARY KEY:** This column will store the unique identifier for each row in the table. The SERIAL data type means that the database will automatically generate a unique integer value for each new row that is inserted into the table. The NOT NULL constraint means that this column cannot be empty. The PRIMARY KEY constraint means that this column uniquely identifies each row in the table.

- **name VARCHAR(255) NOT NULL:** This column will store the name of each row in the table. The VARCHAR(255) data type means that this column can store up to 255 characters of text. The NOT NULL constraint means that this column cannot be empty.




## (d)  Extensions
```
CREATE EXTENSION pg_trgm;
```
```
CREATE EXTENSION
my_database=#
```

**EXTENSION** This SQL statement is used to create or activate an extension in the PostgreSQL database. Extensions are additional modules or functions that extend PostgreSQL database functionality.

**pg_trgm** This extension provides full-text search and trigram similarity capabilities in PostgreSQL.
Using full-text search, you can search for text in your data. Using Trigram similarity, you can calculate the similarity of text in your data.
What are the reasons for using these capabilities? For example, you can use these capabilities to search for contents in a website, to search for data in a database, or to search for documents in a document collection.




### 3.Perform crud operations.

**CRUD (Create, Read, Update, Delete)**

### (a)Create 
```
INSERT INTO users (first_name, last_name, email) VALUES ('John', 'Doe', 'john.doe@example.com');

```
```
INSERT 0 1
my_database=#
```

- **id:** A serial column that is the primary key of the table. This means that each row in the table will have a unique id value.
- **name:** A VARCHAR column that stores the name of the hospital.
- **address:** A VARCHAR column that stores the address of the hospital.
- **phone:** A VARCHAR column that stores the phone number of the hospital.
- **NOT NULL:** constraint on all of the columns means that each column must have a value. No rows will be inserted into the table if any of the columns are empty.
- **VARCHAR:** is a variable-length string data type in SQL. It means that it can store strings of any length, up to the maximum length specified when the column is created. It is a good choice for storing strings of variable length, such as names, addresses, and phone numbers.



## (b) Read
```
SELECT * FROM users;

```
```
id | first_name | last_name |
email
1 | John
john.doe@example.com
(1 row)
my_database=#
| Doe
```


## (C ) Update


```
UPDATE users SET email = 'new.email@example.com' WHERE id = 1;

```


UPDATE 1
my_database=#



## (D) Delete
```
DELETE FROM users WHERE id = 1;

```

```
DELETE 1
my_database=#
```

## 4. Create three users with a password.
```
CREATE ROLE user1 WITH LOGIN PASSWORD 'password1';
```
```
CREATE ROLE
my_database=#
```

```
CREATE ROLE user2 WITH LOGIN PASSWORD 'password2';

```
```
CREATE ROLE
my_database=#
```

```
CREATE ROLE user3 WITH LOGIN PASSWORD 'password3';

```
```
CREATE ROLE
my_database=#
```

```
\du
```
```
List of roles
Role name
Attributes
delhi
gurugram
notda
postgres
user 1
user2
user 3
my_database=#
Superuser, Create role, Create DB, Replication, Bypass RLS
```
- show user



## 5. Grant select permission for user1,select,insert,delete for user2 and all for user3.

- Granting selection permission to user1:

```
GRANT SELECT ON public.users TO user1;
```
```
GRANT
my_database=#
```

- To grant select, insert, and delete permissions to user2:

```
GRANT SELECT, INSERT, DELETE ON public.users TO user2;
```

```
GRANT
my_database=#
```

- Give all permissions to user3
```
GRANT ALL PRIVILEGES ON public.users TO user3;
```

```
GRANT
my_database=#
```








### 6. Understanding the table structure,finding database size, table size etc.

**INSERT INTO**
```
INSERT INTO users (first_name, last_name, email)
VALUES
    ('John', 'Doe', 'john.doe@example.com'),
    ('Jane', 'Smith', 'jane.smith@example.com'),
    ('Alice', 'Johnson', 'alice.johnson@example.com'),
    ('Bob', 'Brown', 'bob.brown@example.com'),
    ('Eva', 'Davis', 'eva.davis@example.com'),
    ('Michael', 'Lee', 'michael.lee@example.com'),
    ('Samantha', 'Taylor', 'samantha.taylor@example.com'),
    ('William', 'Anderson', 'william.anderson@example.com'),
    ('Olivia', 'Moore', 'olivia.moore@example.com'),
    ('Daniel', 'Wilson', 'daniel.wilson@example.com');
```

```
INSERT 10
my_database=#

```

**(a) Table structure**
```
\d users
```
```
my database=# \
d users
Column
id
Table "
public.users"
| Collation |
Nullable |
Default
integer
not
Type
null | nextval('users_id_seq'::regclass)
first_name
character varying(50)
last name character varying(50)
character varying(100)|
email
Indexes:
"users_pkey" PRIMARY KEY, btree (id)
"users_email_key" UNIQUE CONSTRAINT, btree (email)
my_database=#
```


**(b) Finding database size**
```
SELECT pg_size_pretty(pg_database_size(current_database()));
```
```
pg_size_pretty
7700 kB
(1 row)
my database=#
```


**(c) Table size**
```
SELECT pg_size_pretty(pg_total_relation_size('users'));
```

```
pg_size_pretty
40 kB
(1 row)
my_database=#
```

