
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

# Features

The script allows you to organize the work with database with a simple methods and without  writing queries manually.

- Simple insert, update and delete
- Batch inserts and updates
- Where conditions and fulltext search
- Sorting and grouping
- Joins of multiple tables
- Foreign keys updating
- Checking the uniqueness of records
- Concatenation and group concatenation
- Min, max, sum and total
- Increments and decrements
- You do not need to remember about tildes and quotes

# System Requirements and Limitations
System Requirements

- PHP5
- MySQL5
- mysqli extention




## get

Get rows from table as list of associative arrays.

array  **get** ( [int  _$limit_] [, int  _$start_] )

Will be loaded only  _**limit**_  rows, stating from  _**start**_. If both parameters in not set, will be loaded all found rows.


`$articles`  `= Sdba::table(``'articles'``);`

`$list`  `=` `$articles``->get(10)` `// loads 10 articles`

## get_one

Get one row from table as associative array.

array  **get** ( void )

Method has no parameters

`$articles`  `= Sdba::table(``'articles'``);`

`$item`  `=` `$articles``->get_one()` `// loads 1 article`

##  get_list

Get rows from table as list values.

array  **get** ( mixed  _$field_  [, int  _$limit_] [, int  _$start_] [, string $table] )

_**field**_  - selected field, can be single field(strind), or array(key=>value) and will be placed in key=>value list. Will be loaded only  _**limit**_  rows, stating from  _**start**_. If both parameters in not set, will be loaded all found rows;  **_table_**  - sets a table, that's different from current instance.


`$articles`  `= Sdba::table(``'articles'``);`

`$list`  `=` `$articles``->get(10)` `// loads 10 articles`

## get_single

Get one row from table as associative array.

string  **get** ( string  _$field_  [, string  _$table_] )

_**field**_  - selected field;  **_table_**  - sets a table, that's different from current instance.

`$articles`  `= Sdba::table(``'articles'``);`

`$item`  `=` `$articles``->get_one()` `// loads 1 article`

##  total

Returns count of rows in a table.

int **total**  ( void )

Method has no parameters

`$articles`  `= Sdba::table(``'articles'``);`

`$count`  `=` `$articles``->total();` `// returns number of rows in table`

##  delete

Deletes rows from table. You can define specific rows using where() method.

void  **delete**( [int  _$limit_] [, int  _$start_] [, string  _$table_] )

**_limit_**  - maximum rows for deleting,  **_start_**  - start number of row,  **_table_**  - sets a table, that's different from current instance

`$articles`  `= Sdba::table(``'articles'``);`

`$articles``->where(``'id'``, 55);`

`$articles``->``delete``();`

## insert

Inserts row(s) in database.

void  **insert**( [array _$arr_] [, string  _$table_] )

**_arr_**  - array of rows values or list of arrays,  **_table_**  - sets a table, that's different from current instance

`$users`  `= Sdba::table(``'users'``);`

`$data`  `=` `array``(``'name'``=>``'John'``,``'email'``=>``'john@example.com'``);`

`$users``->insert(``$data``);`

`// or batch insert`

`$data`  `=` `array``(`

`array``(``'name'``=>``'John'``,``'email'``=>``'john@example.com'``);`

`array``(``'name'``=>``'Bob'``,``'email'``=>``'bob@example.com'``);`

`array``(``'name'``=>``'Kate'``,``'email'``=>``'kate@example.com'``);`

`);`

`$users``->insert(``$data``);`

## insert_id

Get insert id of last inserted item

int **insert_id**( void )

`$new_user`  `=` `array``(``'email'``=>``'user@example.com'``,` `'password'``=>``'123456'``);`

`$users`  `= Sdba::table(``'users'``);`

`$users``->insert(``$new_user``);`

`$user_id`  `=` `$users``->insert_id();`

## update

Updates row(s) in database. You can define specific rows using where() method.

void  **update**( array _$arr_  [, int  _$limit_] [, int  _$start_] [, string  _$table_] )

**_arr_**  - array of rows values or list of arrays,  **_limit_**  - maximum rows for updating,  **_start_**  - start number of row,  **_table_**  - sets a table, that's different from current instance

`$users`  `= Sdba::table(``'articles'``);`

`$users``->where(``'created <'``,` `'2012-10-30'``);`

`$data`  `=` `array``(``'published'``=> 0);`

`$users``->update(``$data``);`

#### update_fk

Rebuilds relations for foreign key.

void  **update_fk**(string  _$left_key_name_, string  _$left_key_val_, string  _$right_key_name_, mixed  _$right_key_val_  [, string  _$table_] )

**_left_key_name_**  - name of foreign key,  _**left_key_val**_  - value of foreign key,  **_right_key_name_**  - name of relation key,  **_right_key_val_**  - new relation values (can be comma-separated string or array),  **_table_**  - sets a table, when it is different from current instance

`$fk_articles_categories`  `= Sdba::table(``'articles_fk'``);`

`$fk_articles_categories``->update_fk(``'art_id'``,15,``'cat_id'``,``'2,3,8,12'``);`

`//or`

`$keys`  `=` `array``(``'2'``,``'3'``,``'8'``,``'12'``);`

`$fk_articles_categories``->update_fk(``'art_id'``,15,``'cat_id'``,``$keys``);`

## set

Inserts row(s) in database or updates when row already exist.

void  **set**( array _$arr_  )

**_arr_**  - list of arrays, duplicate rows will be updated

`$users`  `= Sdba::table(``'users'``);`

`$data`  `=` `array``(`

`array``(``'id'``=>5,``'name'``=>``'John'``,``'email'``=>``'john@example.com'``);` `//will be updated, if 'id' found`

`array``(``'name'``=>``'Bob'``,``'email'``=>``'bob@example.com'``);` `// will be inserted`

`array``(``'name'``=>``'Kate'``,``'email'``=>``'kate@example.com'``);` `// will be inserted`

`);`

`$users``->set(``$data``);`

## fields

Sets field, that will bee loaded from database, or not will be loaded when  **_reverse_**  is  **true**.

object  **fields**( mixed _$fields_  [, bool  _$reverse_] [, string  _$table_] )

**_fields_**  - fields from table (can be comma-separated string or array),  **_reverse_**  - reversing method action,  **_table_**  - sets a table, when it is different from current instance


`$users`  `= Sdba::table(``'users'``);`

`$users``->fields(``'name'``,``'email'``);` `// will extract only name and email columns`

`$user_list`  `=` `$users``->get();`

##  alias

Sets alias for field in result set

object  **alias**(mixed  _$field_, string  _$alias_  [, string  _$table_] )

**_fields_**  - result field, can be string or  _field=>alias_ array;  **_alias_**  - new name of field in result set;  **_table_**  - table, when it is different from current instance.

`$users`  `= Sdba::table(``'users'``);`

`$users``->alias(``'id'``,``'user_id'``);`

`$users``->get();`

## where

Sets where condition. Affects the methods  **get, get_one,** **total,** **update, delete**.

object  **where**( mixed  _$field_  [, string _$value_] [, string _$table_] [, bool  _$no_quotes_] [, string  _$join_with_] [, string  _$operator_] )

**_field_**  - table field (can be string with operator, or field=>value array),  **_value_**  - condition value,  **_table_**  - table, when it is different from current instance,  **_no_quotes_**  - prevent value from inserting quotes (need for use mysql functions in where, like NOW() etc),  **_join_with_**  - operator for joining condition,  **_operator_**  - condition operator, system feature.

`$users`  `= Sdba::table(``'users'``);`

`$users``->where(``'active'``, 1);`

`$user_list`  `=` `$users``->get();`

##  and_where

Alias of  **where()**, used for convenience and readability.

object  **and_where**( string  _$field_  [, string _$value_] [, string _$table_] [, bool  _$no_quotes_] )

`$users`  `= Sdba::table(``'users'``);`

`$users``->where(``'active'``, 1)->and_where(``'sex !='``,``'man'``);`

`$user_list`  `=` `$users``->get();`

##  or_where

Alias of  **where()**, used for convenience and readability.

object  **or_where**( string  _$field_  [, string _$value_] [, string _$table_] [, bool  _$no_quotes_] )

`$users`  `= Sdba::table(``'users'``);`

`$users``->where(``'active'``, 0)->or_where(``'banned'``,1);`

`$user_list`  `=` `$users``->get();`

## like

Creates like condition, based on  **where()**.

object  **like**( string  _$field_, string _$value_  [, string _$table_] [, array  _$pattern_] [, string  _$join_with_] )

**_field_**  - table field (can be string with operator, or field=>value array),  **_value_**  - condition value,  **_table_**  - table, when it is different from current instance,  **_pattern_** - mask for like operation(array with two values - first and last symbol, default is array('%','%')),  **_join_with_**  - operator for joining condition.

`$users`  `= Sdba::table(``'users'``);`

`$users``->like(``'name'``,` `'Bob'``));` `// will find 'bob','bobby','bob miller','crazy bob', etc`

`$user_list`  `=` `$users``->get();`

##  not_like

Alias of  **like()**, used for convenience and readability.

object  **not_like**( string  _$field_, string _$value_  [, string _$table_] [, array  _$pattern_] )

##  and_like

Alias of  **like()**, used for convenience and readability.

object  **and_like**( string  _$field_, string _$value_  [, string _$table_] [, array  _$pattern_] )

##  and_not_like

Alias of  **like()**, used for convenience and readability.

object  **and_not_like**( string  _$field_, string _$value_  [, string _$table_] [, array  _$pattern_] )

##  or_like

Alias of  **like()**, used for convenience and readability.

object  **or_like**( string  _$field_, string _$value_  [, string _$table_] [, array  _$pattern_] )

## or_not_like

Alias of  **like()**, used for convenience and readability.

object  **or_not_like**( string  _$field_, string _$value_  [, string _$table_] [, array  _$pattern_] )

##  where_in

Creates like condition, based on  **where()**.

object  **where_in**( string  _$field_, mixed _$value_  [, string _$table_] )

**_field_**  - table field (can be string with operator, or field=>value array),  **_value_**  - condition values(can be comma-separated string or array),  **_table_**  - table, when it is different from current instance.

`$users`  `= Sdba::table(``'users'``);`

`$users``->like(``'name'``,` `'Bob'``));` `// will find 'bob','bobby','bob miller','crazy bob', etc`

`$user_list`  `=` `$users``->get();`

##  where_not_in

Alias of  **where_in****()**, used for convenience and readability.

object  **where_in**( string  _$field_, string _$value_  [, string _$table_] )

##  and_in

Alias of  **where_in****()**, used for convenience and readability.

object  **and_in**( string  _$field_, string _$value_  [, string _$table_] )

##  and_not_in

Alias of  **where_in****()**, used for convenience and readability.

object  **and_not_in**( string  _$field_, string _$value_  [, string _$table_] )

##  or_in

Alias of  **where_in****()**, used for convenience and readability.

object  **or_in**( string  _$field_, string _$value_  [, string _$table_] )

##  or_not_in

Alias of  **where_in****()**, used for convenience and readability.

object  **or_not_in**( string  _$field_, string _$value_  [, string _$table_] )

##  open_sub

Allow to create subcondition in where() part (opens '(' in sql query)

object  **open_sub**( [string _$join_with_] )

**_join_with_** - (optional) sets 'glue' between subcondition and other ones in where() side of query, default is 'AND'

`$users`  `= Sdba::table(``'users'``);`

`$users``->where(``'name'``,` `'Bob'``));`

`$users``->open_sub();`

`$users``->where(``'name'``,` `'Bob'``));`

`$users``->or_where(``'name'``,` `'Jack'``));`

`$users``->close_sub();`

`$user_list`  `=` `$users``->get();`

##  close_sub

Closes sub condition.

object  **close_sub**( void )

##  and_sub()

Alias of  **open_sub**( 'AND' ), used for convenience and readability.

object  **and_sub**( void )

##  or_sub()

Alias of  **open_sub**( 'OR' ), used for convenience and readability.

object  **or_sub**( void )

##  fulltext

Creates fultext search (working with fulltext index only)

object  **fulltext**( mixed _$fields_, string  _$phrase_  [, string  _$mode_] [, string _$table_] )

**_fields_**  - comma-separated string or array of fieldnames,  **_phrase_**  - search string,  _**mode**  -_ search mode, default is  **natural** (natural language mode), can be  **boolean**  (boolean mode) or  **expansion**  (natural language mode with query expansion);  **_table_**  - table, when it is different from current instance.

`$articles`  `= Sdba::table(``'articles'``);`

`$articles``->fulltext(``'title,text'``,` `'Hollidays with Evanto'``));`

`$articles_list`  `=` `$articles``->get();`

##  sort_by

Sorts your result data

object  **sort_by**( string  _$field_  [, string  _$direction_] [, string _$table_] )

**_field_**  - sort field;  **_direction_**  - sort direction (**asc**,  **desc**);  **_table_**  - table, when it is different from current instance.

`$articles`  `= Sdba::table(``'articles'``);`

`$articles``->sort_by(``'title'``);`

`$articles``->sort_by(``'created'``,``'desc'``);`

`$articles_list`  `=` `$articles``->get();`

##  random

Randomizing of your result data.

object  **random**( void )

`$articles`  `= Sdba::table(``'articles'``);`

`$articles``->random();`

`$articles_list`  `=` `$articles``->get(5);` `// get 5 random articles`

##  join

Select multiple tables with join fearure.

object  **join**( string _$type_, string  _$field_, string  _$join_table_, string  _$join_field_  [, string  _$left_table_] [, string  _$alias_ ] [, mixed  _$right_fields_] [, bool  _$reverse_fields_] )

**_type_**  - joining type, can be any like LEFT, RIGHT, INNER etc, but better to use alias methods (**left_join(), right_join(), inner_join()**);  **_field_**  - join field in main table;  **_join_table_**  - joined table;  **_join_field_**  - relation field in joined table;  **_left_table_**  - main table, when it is different from current instance;  _**alias**_  - use alias, if you want to join same table more once;  **_right_fields_**  - selected fields from joined table (see **fields()**  method); reverse for selected fields for joined table (see **fields()**  method).

See examples for  **left_join, inner_join**

##  left_join

Alias of  **join****()**, used for convenience and readability.

object  **left_join**( string  _$field_, string  _$join_table_, string  _$join_field_  [, string  _$left_table_] [, string  _$alias_ ] [, mixed  _$right_fields_] [, bool  _$reverse_fields_] )

`$articles`  `= Sdba::table(``'articles'``);`

`$articles``->left_join(``'cat_id'``,``'categories'``,``'cid'``);` `// selects articles with categories`

`$articles_list`  `=` `$articles``->get();`

## right_join

Alias of  **join****()**, used for convenience and readability.

object  **right_join**( string  _$field_, string  _$join_table_, string  _$join_field_  [, string  _$left_table_] [, string  _$alias_ ] [, mixed  _$right_fields_] [, bool  _$reverse_fields_] )

##  inner_join

Alias of  **join****()**, used for convenience and readability.

object  **inner_join**( string  _$field_, string  _$join_table_, string  _$join_field_  [, string  _$left_table_] [, string  _$alias_ ] [, mixed  _$right_fields_] [, bool  _$reverse_fields_] )

`$users`  `= Sdba::table(``'users'``);`

`$users``->left_join(``'id'``,``'profiles'``,``'user_id'``);` `// users with profile`

`$users_list`  `=` `$users``->get();`

##  group_by

Groups your result data.

object  **group_by**( string  _$field_ [, string _$table_] )

**_field_**  - group field; **_table_**  - table, when it is different from current instance.


`$users`  `= Sdba::table(``'users'``);`

`$users``->inner_join(``'id'``,``'articles'``,``'user_id'``);`

`$users``->group_by(``'id'``);` `// removes duplicates, when user wrote more one article`

`$users_list`  `=` `$users``->get();` `// users who wrote articles`

##  sum

Selects sum for selected column

mixed  **sum**(string  _$field_ [, string  _$alias_] [, string  _$table_] )

**_field_**  - selected column,  **_alias_**  - alias of sum for get(), get_one result sets;  **_table_**  - table, when it is different from current instance.

`$cart`  `= Sdba::table(``'cart'``);`

`$total`  `=` `$cart``->sum('price);`

## max

mixed  **max**(string  _$field_ [, string  _$alias_] [, string  _$table_] )

**_field_**  - selected column,  **_alias_**  - alias of max for get(), get_one result sets;  **_table_**  - table, when it is different from current instance.

`$cart`  `= Sdba::table(``'cart'``);`

`$max`  `=` `$cart``->max('price);`

##  min

mixed  **min**(string  _$field_ [, string  _$alias_] [, string  _$table_] )

**_field_**  - selected column,  **_alias_**  - alias of min for get(), get_one result sets;  **_table_**  - table, when it is different from current instance.

`$cart`  `= Sdba::table(``'cart'``);`

`$min`  `=` `$cart``->min('price);`

## concat

Concatenate fields in one

mixed  **concat**( mixed  _$fields_  , string  _$alias_  [, string  _$separator_] [, string  _$table_] )

**_fields_**  - concatenated fields, can be comma-separated string or array;  **_alias_**  - name of field in result set;  **_separator_**  - values separator, default is comma;  **_table_**  - table, when it is different from current instance.

`$users`  `= Sdba::table(``'users'``);`

`$users``->concat(``'first_name,last_name'``,``'full_name'``,``' '``);`

`$users_list`  `=` `$users``->get();`

##  group_concat

Concatenate fields from group in one

mixed  **group_concat**( string  _$field_  [, string  _$alias_] [, string  _$separator_] [, string  _$table_] [, bool  _$distinct_] [, string  _$order_by_] [, string  _$direct_] )

**_field_**  - concatenated column;  **_alias_**  - name of field in result set;  **_separator_**  - values separator, default is comma;  **_table_**  - table, when it is different from current instance;  **_distinct_**  - remove duplicates from group;  **_order_by_**  - column for group sorting;  **_direct_**  - sort direction (**asc, desc**).

`$users`  `= Sdba::table(``'users'``);`

`$users``->left_join(``'id'``,``'avards_fk'``,``'user_id'``);` `// fk`

`$users``->inner_join(``'avard_id'``,``'avards'``,``'id'``,``'avards_fk'``);` `// avards table`

`$users``->group_concat(``'avard_name'``);`

`$users``->group_by(``'id'``);`

`$users_list`  `=` `$users``->get();`

##  is_unique

Checking value for uniqueness

bool  **is_unique**( string  _$field_, string  _$value_  [, string  _$table_] )

**_field_**  - name of checked field;  **_value_**  - checked value;  **_table_**  - table, when it is different from current instance.

Returns **true**, when value is uniqueness, or  **false**  if not.

`$users`  `= Sdba::table(``'users'``);`

`$bool`  `=` `$users``->is_unique(``'email'``,``'john@example.com'``);` `// return true or false`

## increment

Increment of row(s) value

void  **increment**( string  _$field_  [, int _$num_] [, string  **$table**] )

**_field_**  - field for action;  **_$num_**  - increment number (default is 1);  **_table_**  - table, when it is different from current instance.

`$articles`  `= Sdba::table(``'articles'``);`

`$articles``->where(``'id'``,55);`

`$articles``->increment(``'views'``);`

##  decrement

Decrement of row(s) value

void  **decrement**( string  _$field_  [, int _$num_] [, string  **$table**] )

**_field_**  - field for action;  **_$num_**  - decrement number (default is 1);  **_table_**  - table, when it is different from current instance.

`$users`  `= Sdba::table(``'users'``);`

`$users``->where(``'id'``,118);`

`$users``->decrement(``'raiting'``,10);`

##  distinct

Add DISTINCT operator in query

object  **distinct**( void )

Method has no parameters

## auto_reset

Change autoreset status

object  **auto_reset**( [bool  _$state_] )

**_state_**  - true to enable, false to disable

`$users`  `= Sdba::table(``'users'``);`

`$users``->auto_reset(true);`

##  reset

Resets conditions (fields, wheres, sort_by, group_by, joins)

object  **reset**( void )

`$users`  `= Sdba::table(``'users'``);`

`...some actions...`

`$users``->reset();`

##  query

Executes manual query

object  **query**( string  _$query_  )

**_query_**  - sql query.

`$db`  `= Sdba::db();`

`$db``->query(```'TRUNCATE TABLE `articles`'```);` `// clear articles table`

##  result

Get result set of manual query as list of arrays

array  **result**()

`$db`  `= Sdba::db();`

`$db``->query(```"SELECT * FROM `users`"```);`

`$users`  `=` `$db``->result();`

##  row

Get one result row of manual query as associative array

array  **row**()
 
`$db`  `= DB::db();`

`$db``->query(```"SELECT * FROM `users` WHERE `id` = 34"```);`

`$user`  `=` `$db``->row();`

#  escape

Escape special chars for safety queries. Adds quotes automatically. Need only for manual queries.

string **escape**( string  _$val_  [, bool  _$not_qu_  )

**_val_**  - string value;  **_not_qu_**  - disable adding quotes when  **true**, default is **false**
 

`$db`  `= DB::db();`

`$comment`  `=` `$db``->escape(``$_POST``[``'comment'``]);`

`$db``->query(```"INSERT INTO `comments` (`comment`) VALUES ({$comment})"```);`
