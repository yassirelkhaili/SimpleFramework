# 🚀 Simple ORM

## Introduction

```plaintext
Welcome to the SimpleORM Project, an open source PHP ORM designed by me to be used in future projects as well as master the behind the scene fundamentals of Object-Relational Mapping, advanced PHP OOP concepts, and design patterns. 📚 This project serves as a practical playground for me to further understand how ORMs work behind the scenes.
```

```plaintext
This readme serves as the official documentation to this project. All information about how to get started using SimpleORM is included in this readme.
```

```plaintext
Why should you use SimpleORM too? because it's blazingly fast. Plus it's open source and easy to add new features to it as you wish in order to tailor it to your own needs as a developer.
```

## I. Simple command line interface


### Introduction

```plaintext
SimpleORM includes a simple command line interface called well... simple. It supports multiple commands that make using simpleORM seamless.
```

### Simple commands

- help

```plaintext
This command prints a list of all current commands supported by simple.
```

Example use:

```bash
php simple help
```

- generate

```plaintext
This command generates an entity representing a database table in the Models folder.
It is often used to efficiently create tables in order to later migrate them to a database later on.
```

Example use:

```bash
php generate:entity Users
```

- migrate

```plaintext
This command migrate an entity from your Models folder to your database.
```

Example use:

```bash
php migrate:entity Users
```

- destroy

```plaintext
This command deletes an entity from the Models folder.
```

Example use:

```bash
php destroy:entity Users
```

- rollback

```plaintext
This command reverses a migration basically dropping which ever table name you give it.
```

Example use:

```bash
php rollback:entity Users
```

## Entities

## Establishing a connection

```plaintext
SimpleORM offers a simple way to establish a connection to your database.
Simply fill up the fields in the .env.db file in the project root with your database credentials and you are set.
```
Examle use:

```bash
DRIVER = "mysql"
DB_HOST = "localhost"
DB_PORT = "3301"
DB_NAME = "ormtest"
DB_USER = "root"
DB_PWORD = ""
```

## Entity Mapper:

### Definition

```plaintext
SimpleORM uses an Entity Mapper which is a class that handles entity mapping in order to get all of its properties and types that way SimpleORM knows how to create the appropriate database table.
Default location: SimpleORM/src/Utils/EntityMapper.php
```

## Entity Generator:

### Definition

```plaintext
SimpleORM uses an Entity Generator which is a class that handles entity generation and puts it in the Models folder.
Default location: SimpleORM/src/Utils/EntityGenerator.php
```

## Query Generator:

### Definition

```plaintext
SimpleORM uses a Query Generator which is basically the chef that cooks up all of the queries and serves them to the Entity Manager.
Default location: SimpleORM/src/SimpleORM/QueryGenerator.php
```

## Entity Manager:

### Definition

```plaintext
SimpleORM uses an Entity Manager which is the class you will be interacting with almost all the time. It's basically the server that takes your order to the kitchen then serves you the food. and by order I mean SimpleORM methods/queries and by your food I mean data/records from the database.
Default location: SimpleORM/src/SimpleORM/EntityManager.php
```

## How to use SimpleORM

### require Enity Manager Class

```php
require "./src/SimpleORM/EntityManager.php";

use EntityManager\EntityManager;
```

### instantiate a new Entity Manager Object

```plaintext
Required parameters: 
- $conn object from SimpleORM/src/Database/connections/conn.php This is autimatically included when you require the Entity Manager
- entity/database table name as string
```

```php
$entity = new EntityManager($conn, "Users");
```
### Insert Methods

- Individual insert

Example use:

```php
$entity->email = "example@gmail.com";
$entity->name = "name";
$entity->lastname = "lastname";
$entity->userID = 21;
$entity->save();
```

- Batch insert

```plaintext
Required parameters: 
- Array of records as associative arrays with column names keys pointing to values
```

Example use:

```php
$entity->saveMany([
    ["name"=> "nam eqwd","email"=> "email@gmail.com", "lastname" => "lastname"],
    ["name"=> "nameqwd2","email"=> "email2@gmail.com", "lastname" => "lastname"],
    ["name"=> "nameqwd3","email"=> "email3@gmail.com", "lastname" => "lastname"],
]);
```

### Fetch Methods

- Fetch records

Example use:

```php
$entity->fetchAll()->get(); // fetches all records from the database table
```

- paginate 
```plaintext
Limits the number of records to be fetched
```

```plaintext
Required parameters: 
- value: integer
```

Example use:

```php
$entity->fetchAll()->get(int number);
```

- where

```plaintext
Specifies which records should be fetched
Required parameters: 
- column name: string
- value: any
```

Example use:

```php
$entity->fetchAll()->where("name", "exampleName")->get();
$entity->fetchAll()->where("name", "exampleName")-where("email", "exampleEmail")->get(number);
```



