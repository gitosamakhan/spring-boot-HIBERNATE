
<h1 align="center">
    Hibernate 🥫 
</h1>

<p align="center">
    Hibernate ORM (Object-Relational Mapping) is an object-relational mapping tool for the Java programming language. It provides a framework for mapping an object-oriented domain model to a relational database.
</p>


## Hibernate Annotations

`NOTE`
* The Persistence tab in IntelliJ will show the database tables/entities that we created using hibernate/persistence.
* Make sure to import all the annotations from `javax.persistence`.

Annotations | Description
---| ---| 
`@Entity` | Marks the class as an entity.
`@Table(name="table-name")` | Maps the entity to table.
`@Id` | Marks the field as an ID-Column of the table.
`@Column` | Shows that the field is the column of the database.


## Coding Concepts / Snippets

[comment]: <> (Setup Mysql)
<details>
<summary>Setup MySql</summary>

* Install MySQL.
* Open CMD in the `C:\Program Files\MySQL\MySQL Server 8.0\bin` path, and enter the following command:

      mysql -u root -p

* It will ask for a password, enter the password and now we have access to MySQL.
* Now create a user to access the database using the following command.

      CREATE USER 'dbadmin'@'localhost' IDENTIFIED BY 'password';

* Once the user is created, you can check if the user exists by using the following command:

      SELECT user FROM mysql.user;

* Now create a database using the following query:

      CREATE DATABASE testdb;

* Create a table using the following query. Make sure to select the database using `use databaseName` command to select the database for table creation.

      CREATE TABLE Employee (
        firstName VARCHAR(30) NOT NULL, 
        lastName VARCHAR(30) NOT NULL, 
        employeeId INT UNSIGNED NOT NULL PRIMARY KEY
      );

  The `show tables` command will show all tables in the database, and `describe tablename` command will show details of the table.


* Now we have to give privileges to the user that we just created in order to access the database. use the query below to assign privileges.

       GRANT ALL PRIVILEGES ON testdb.employee TO 'dbadmin'@'localhost' WITH GRANT OPTION;

* To check the privileges of a user, use the following query:

      SHOW GRANTS FOR 'dbadmin'@'localhost';

* Set auto increment in MySQL and just pass the values of all columns except PK, it will automatically increment PK.
  
      ALTER TABLE student MODIFY id int NOT NULL AUTO_INCREMENT;

</details>

[comment]: <> (Testing Database Connection)
<details>
<summary>Testing Database Connection</summary>

Following code is used to test the connection with the database.

    package com.osama.springhibernate;
    
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration;
    
    import java.sql.Connection;
    import java.sql.DriverManager;
    
    @SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
    public class SpringHibernateApplication {
    
        public static void main(String[] args) {
            SpringApplication.run(SpringHibernateApplication.class, args);
    
            /*
            * Database: MySQL
            * Testing Database Connection
            */
            String userName = "dbadmin";
            String password = "admin";
            String jdbcUrl = "jdbc:mysql://localhost:3306/testdb";
            try {
                System.out.println("Connecting to database");
                Connection con = DriverManager.getConnection(jdbcUrl, userName, password);
                System.out.println("Connection Successful");
            } catch (Exception exception) {
                exception.printStackTrace();
            }
        }
    }

Make sure to add `@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})` in the annotation.

</details>

[comment]: <> (Session Factory)
<details>
<summary>Session Factory</summary>

* Session Factory Reads the Hibernate config file and creates the heavy-weight session objects. 
* `Session objects` develops connection with the database, and we use that object again and again.

</details>

