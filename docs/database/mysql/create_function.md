
# Create function example

```sql

DELIMITER //

DROP FUNCTION  IF EXISTS get_add_column_statement //

CREATE FUNCTION get_add_column_statement (
	table_name varchar(64), 
	column_name varchar(64), 
	column_type longtext, 
	column_default longtext, 
	data_type varchar(64), 
	is_nullable varchar(3)
	) 
RETURNS longtext
BEGIN

	declare my_statement longtext;

	set my_statement = 'This is the result you are expecting';

	return my_statement;
	
END;
//

DELIMITER ;

```