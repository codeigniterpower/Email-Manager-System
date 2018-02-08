# Email-Manager-System

CodeIgniter v2.2.1 and Boostrap v3.3.2

- Add/Edit Users
- Add/Edit Aliases for Users
- Add/Edit Forwards for Users
- Add/Edit Vacation for Users
- Add/Edit Domain names
- the "ZXCVBN" Password Strenght tester
- Migration

## Logical workflow

Based on those mail sistem that performs in db their users and domains (commonly posfix that uses mysql as DBMS).

In the MTA daemon, sure will be a section that talks about the configuration using database event real sistem users.. 
obviously will be a table for that.. the project assumes each fiel can be edited except for those defined as password field.

The proyect was improved little only to manage autocreatino of DB (if connection was susessfull), 
provide some explanations and corrected the links between controllers to work in any webserver.

## Database

As explained, based on those MTA that performs users in database with default uid, 
in `users_model.php` each user are under a hardcoded `uid` that will be the user that virtualized the rest of.

## LICENSE

Unkown (c) 2015 Kiril Kirkov
GPLv2 (c) 2017 PICCORO Lenz MCKAY

This proyect was taken from the archived repository due author does not respond, 
and any license was defined in that moment ar commit 2ebe5f11aea1d19401329c0c2fe8661bc5dd7058 ..


