# DATABASES: TEST-DRIVING A REPOSITORY CLASS CHALLENGE

----

## Introduction

>In the realm of PostgreSQL, we manipulate tables, column names and records. However, in Ruby programs, we represent data using classes, objects and attributes. We therefore need a way to transform the data retrieved from the database into data that can be used in our program.
>
>To achieve this, you will learn how to build two kind of classes — they're regular Ruby classes, but designed to achieve a specific purpose in our program:
>
> * A **Model class** is used to hold a record's data.
>For example, if we have a table students, we'd have a class Student, with attributes for each column. A single object holds the data for a specific student record. This class usually doesn't contain >any logic, but is only used to hold data.
>
> * A **Repository class** implements methods to run SQL queries on the database to retrieve, create, update or delete data.
>For example, if we have one table students, we'd have a class StudentRepository containing methods that communicates with the database using SQL.

----

## Objective

To learn how to test-drive "Model" and "Repository" classes to `SELECT` records from the database.

For this challenge, I will be creating a Book Store project that will use a "Model" and "Repository" classes.

----

## Sequence diagram for Book Store Project

```mermaid
sequenceDiagram
    participant t as terminal
    participant app as Main program (in app.rb)
    participant ar as Book Repository class <br /> (in lib/book_repository.rb)
    participant db_conn as DatabaseConnection class in (in lib/database_connection.rb)
    participant db as Postgres database

    Note left of t: Flow of time <br />⬇ <br /> ⬇ <br /> ⬇ 

    t->>app: Runs `ruby app.rb`
    app->>db_conn: Opens connection to database by calling connect method on DatabaseConnection
    db_conn->>db_conn: Opens database connection using PG and stores the connection
    app->>ar: Calls all method on the Book Repository class
    ar->>db_conn: Sends SQL query by calling `exec_params` method on DatabaseConnection
    db_conn->>db: Sends query to database via the open database connection
    db->>db_conn: Returns an array of hashes, one for each row of the book table

    db_conn->>ar: Returns an array of hashes, one for each row of the book table
    loop 
        ar->>ar: Loops through array and creates a book object for every row
    end
    ar->>app: Returns array of book objects/instances
    app->>t: Prints list of books to terminal
```

----

## Designing a repository class for selecting records from the database

| Method |      Job       | Arguments |   SQL query it executes  |     Returns    |
| ------ | -------------- | --------- | ------------------------ | -------------- |
|  all   | gets all books |   none    | `SELECT ... FROM books;` | Array of book  |

----

## How to run it and print out the list of books in the terminal:

```bash
# in the book-store directory:
$ ruby app.rb
```
