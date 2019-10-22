
# Mysqli-DB-Class

**Manipulate with your data using simple methods**

Powerful actions in simple Active Record style. No any SQL writing. Fast and low-memory usage, compact and cleaner resulting code.


-   Upload sdba folder on your server.
-   Open  **db_config.php**  and configure connection with your database.
```
public static $dbname = 'dbname'; // Your database name
public static $dbuser = 'dbuser'; // Your database username
public static $dbpass = 'dbpass'; // // Your database password
public static $dbhost = 'localhost'; // Your database host, 'localhost' is default.
public static $dbencoding = 'utf8'; // Your database encoding, default is 'utf8'. Do not change, if not sure.
```
- include sdba.php in your script

# First request
Create object of your table, for example - table users. Lets retrieve all rows from `users` and write in $users_list variable.

```
$users = DB::table('users'); // creating table object
$users_list = $users->get(); // retrieving all rows from users table
```
