<center> <u> <h1 style="font-size: 50px;"> Postgres setup</h1> </u> </center>

## Table of contents
**1. Task requirement**

**2. Environment details**

**3. System configuration**

**4. Definition of tools**


## 1. Task requirement: Podman.Postgres

## 2. Environment details: 
- Os:- Ubuntu 22.04.3 LTS
- Podman- 3.4.4
- Psql (PostgreSQL) 14.9

## 3. System configuration:
- CPU - 4
- Storage -16 GB


## 4. Definition of tools:

- Podman is an open-source container management tool used to create, run, and manage containers on Linux systems.

-PostgreSQL is an open-source relational database management system (RDBMS).
Which is used for data storage and management.



## 1. Create a postgres container with podman
```
sudo apt install -y podman
```
![](1.png)
```
podman version
```
![](2.png)

```
podman run --name postgres-container -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 docker.io/library/postgres:latest

```
![](3.png)


- Podman run: This command is used to create and run a container.
- -d: This option is used to run the container in background mode, meaning the container will run and your terminal will remain available.
- --name my-postgres: With this option you can identify your container with the name "my-postgres".
- -e POSTGRES_PASSWORD=mysecretpassword: With this option you are setting the environment variable, whose name is "POSTGRES_PASSWORD" and value is "mysecretpassword". This password will be used to access PostgreSQL database.
- -v /mydata:/var/lib/postgresql/data: With this option you are mounting a volume. /mydata will map the path of the host system to the path of /var/lib/postgresql/data container. This allows you to store your database data in the host system, so that it persists, and the data remains safe even after you delete the container.
- 'postgres:14: This is the image name that you are using from the container. "postgres:14" represents the official Docker image of version 14 of PostgreSQL. This container will run with the PostgreSQL database server.

## Verify that the PostgreSQL container is running:

```
podman ps
```

![](4.png)


## 2.create users,databases,tables,extensions on the same.

```
podman exec -it postgres-container psql -U postgres

```


![](5.png)

## (a) Create Users
```
CREATE USER noida WITH PASSWORD 'noida1';
CREATE USER delhi WITH PASSWORD 'delhi1';
CREATE USER gurugram WITH PASSWORD 'gurugram1';
```
![](6.png)


## (b) Databases
```
CREATE DATABASE my_database;

```

![](7.png)



## (c) Tables

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

![](9.png)


- CREATE TABLE: This keyword tells the database to create a new table.
  
- my_table: This is the name of the table that is being created.
- ( id SERIAL NOT NULL PRIMARY KEY, name VARCHAR(255) NOT NULL ): This is the definition of the table, which includes the names and data types of the columns in the table.

### Here is a more detailed explanation of each part of the statement:

- id SERIAL NOT NULL PRIMARY KEY: This column will store the unique identifier for each row in the table. The SERIAL data type means that the database will automatically generate a unique integer value for each new row that is inserted into the table. The NOT NULL constraint means that this column cannot be empty. The PRIMARY KEY constraint means that this column uniquely identifies each row in the table.

- name VARCHAR(255) NOT NULL: This column will store the name of each row in the table. The VARCHAR(255) data type means that this column can store up to 255 characters of text. The NOT NULL constraint means that this column cannot be empty.


## (d)  extensions
```
CREATE EXTENSION pg_trgm;
```

![](10.png)

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

![](11.png)


- id: A serial column that is the primary key of the table. This means that each row in the table will have a unique id value.
- name: A VARCHAR column that stores the name of the hospital.
- address: A VARCHAR column that stores the address of the hospital.
- phone: A VARCHAR column that stores the phone number of the hospital.
- NOT NULL: constraint on all of the columns means that each column must have a value. No rows will be inserted into the table if any of the columns are empty.
- VARCHAR : is a variable-length string data type in SQL. It means that it can store strings of any length, up to the maximum length specified when the column is created. It is a good choice for storing strings of variable length, such as names, addresses, and phone numbers.



## (b) Read
```
SELECT * FROM users;

```

![](12.png)


## (C ) Update


```
UPDATE users SET email = 'new.email@example.com' WHERE id = 1;

```

![](13.png)

## (D) Delete
```
DELETE FROM users WHERE id = 1;

```

![](14.png)


## 4. Create three users with a password.
```
CREATE ROLE user1 WITH LOGIN PASSWORD 'password1';
```
![](15.png)

```
CREATE ROLE user2 WITH LOGIN PASSWORD 'password2';

```
![](16.png)

```
CREATE ROLE user3 WITH LOGIN PASSWORD 'password3';

```
![](17.png)

```
\du
```
![](18.png)
- show user



## 5. Grant select permission for user1,select,insert,delete for user2 and all for user3.

- Granting selection permission to user1:

```
GRANT SELECT ON public.users TO user1;
```

![](19.png)

- To grant select, insert, and delete permissions to user2:

```
GRANT SELECT, INSERT, DELETE ON public.users TO user2;
```
![](20.png)

- Give all permissions to user3
```
GRANT ALL PRIVILEGES ON public.users TO user3;
```

![](21.png)









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
![](22.png)

**(a) Table structure**
```
\d users
```

![](23.png)



**(b) finding database size**
```
SELECT pg_size_pretty(pg_database_size(current_database()));
```
![](24.png)



**(c) table size**
```
SELECT pg_size_pretty(pg_total_relation_size('users'));
```
![](25.png)


