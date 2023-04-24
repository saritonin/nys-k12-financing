## Contents of this folder
- k12nyfin.sql - a MySQL export of the database
- k12nyfin.sqlite - a SQLite version of the database
- table_descriptions.dbml - a [DMBL](https://github.com/holistics/dbml) file containing all table descriptions<br />
explore the schema at [dbdocs.io](https://dbdocs.io/sarah.lauser.school/K12_finances)

## Database server
This database was initially created on a private database server.
|                |                                  |
|----------------|----------------------------------|
| Server type    | MySQL                            |
| Server version | 8.0.28-0ubuntu0.20.04.3 (Ubuntu) |
| Server charset | UTF-8 Unicode (utf8)             |


## Processes used to create these files
Export from MySQL via phpMyAdmin
- Export method: Quick
- Format: SQL
- Export

Conversion to SQLite
- https://www.rebasedata.com/convert-sql-to-sqlite-online