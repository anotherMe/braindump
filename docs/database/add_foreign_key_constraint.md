# Add foreign key constraint

During table creation:

<code>
CREATE TABLE my_table 
  field1,
  field2,
  CONSTRAINT my_fk_name FOREIGN KEY (field2)
      REFERENCES my_foreign_table (my_foreign_column) MATCH SIMPLE
      ON UPDATE NO ACTION ON DELETE NO ACTION
);
</code>

After table creation:

<code>
ALTER TABLE my_table 
ADD CONSTRAINT my_fk_name
FOREIGN KEY (my_field) 
REFERENCES my_foreign_table (my_foreign_column)
ON DELETE NO ACTION;
</code>