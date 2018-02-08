# emaildb install

Based on those mail sistem that performs in db their users and domains (commonly posfix that uses mysql as DBMS).

## Requirements

* lighttpd/apache2
* php 5.3+ (tested only with php 5.4+, short opentag must be set on)
* mysql/postgres  (postgres must use the public sheme only)

**Process**

1. Just put the code directory inside a subdirectorio or directly in the htdocs.
2. Setup the database connection in `application/config/config.php` and call from your browser.

## Database

As explained, based on those MTA that performs users in database with default uid, 
in `users_model.php` each user are under a hardcoded `uid` that will be the user that virtualized the rest of.

**Users** the MTA must performs and use the definition table same as this project, unless you modified the users model, 
so the table definition will looks and assumed those fiels:

``` SQL
CREATE TABLE `users` (
  `name` VARCHAR(40) COLLATE utf8_bin,
  `login` VARCHAR(40) COLLATE utf8_bin,
  `password` VARCHAR(40) COLLATE utf8_bin,
  `domain` VARCHAR(40) COLLATE utf8_bin,
  `decrypt` VARCHAR(40) COLLATE utf8_bin,
  `home` VARCHAR(40) COLLATE utf8_bin,
  `uid` VARCHAR(40) COLLATE utf8_bin,
  PRIMARY KEY (`login`, `domain`) -- users as differents domains, so the controller/model dont need to take care of a id pk
) ;
```
**The domains** are the main pivot of the users:

``` SQL
CREATE TABLE `domains` (
  `domain` VARCHAR(40) COLLATE utf8_bin,
  PRIMARY KEY (`domain`)
) ;

```

**forwarders and vacations** are features not really need and currently depends of the MTA/MAIL implementation.

``` sql
CREATE TABLE `userforward` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `recipients` VARCHAR(40) NULL,
  `domain` VARCHAR(40) NULL,
  `local_part` VARCHAR(40) NULL,
  PRIMARY KEY (`id`));
```

``` sql
CREATE TABLE `aliases` (
  `local_part` varchar(40) DEFAULT NULL,
  `domain` varchar(40) NOT NULL,
  `recipients` varchar(40) DEFAULT NULL,
  PRIMARY KEY (`email`,`domain`, `recipients`)
) ;
```

``` sql
CREATE TABLE `vacation` (
  `email` varchar(40) NOT NULL,
  `local_part` varchar(40) DEFAULT NULL,
  `domain` varchar(40) NOT NULL,
  `recipients` varchar(40) DEFAULT NULL,
  `startdate` date DEFAULT NULL,
  `enddate` varchar(40) DEFAULT NULL,
  `subject` varchar(40) DEFAULT NULL,
  `message` varchar(40) DEFAULT NULL,
  `created` varchar(40) DEFAULT NULL,
  `active` varchar(40) DEFAULT NULL,
  PRIMARY KEY (`email`,`domain`)
) ;

```
