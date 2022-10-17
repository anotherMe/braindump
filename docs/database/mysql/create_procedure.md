
```sql

DROP PROCEDURE IF EXISTS my_fancy_procedure_name;

DELIMITER //

//
CREATE PROCEDURE my_fancy_procedure_name (
	param1 varchar(64), 
	param2 varchar(64)
	) 
BEGIN
	

	/* do something useful */

    /* return table results */

    select * from my_table;
	
END;
//

DELIMITER ;

```