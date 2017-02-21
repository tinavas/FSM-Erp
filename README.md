# FSM-Erp
Management tool for workshop, stores and maintenance

### Database updating Routes:

### /api/db/update_db_field
This is used to update a given field in the database from any input. The attributes required in the input field in order to make it work are: 

>col="\<column_to_update_in_db>"

>colid="\<id_field_of_row_to_update_in_the_db>", Usually the primary key

>colidval="\<id_value_of_the_id_column>", usually the value of the primary key

In order to work every input must have a unique id which can be generated by adding a name_\<serial value from primary key>\. The class .update has to be added to the input element. The table name to update will come from a hidden input with id dbtable: 

>\<input type="hidden" id="dbtable" value="table to update in db">\

### /api/db/insert_db_field
to be written

### /api/db/delete_db_field
This route will delete a complete row from a table in the database. The **.delete** class has to be added to the button triggering it in order to work. Extra attributes will have to be added in the button tag.

>dbcolid="primary key column of the row to delete" As per update route

>dbcolidval="value of the primary key to idetify the deleted row"

We also have to identify the table from where to delete. This is done by adding a hidden element in the page as:

>\<input type="hidden" id="dbtable" value="table_name">

If deleting from a main page then dbtable is the appropriate tag to use. If we have to delete from a details page then the id will change to **dbtable-det** and we have to add an extra attribute **is-detail="true"** to the input as we might need to identify both the normal table and the detail table on the page. The function will take care of deleting the correct row from the tables.

### Autocompletes
Create the route that returns label and value in JSON format in the autocomplete.js routes files
The display element will have to be called like the name of the field with an added "_txt" concatenated string after it.

Place a hidden field under the display element:

>\<input type="hidden" name="field_in_db" id="field_in_db">

Add an attribute to the input element called ac-source

>ac-source="\<name_of_the_route_in_autcompletes.js>"

The library will automatically take care of filling the name in the 

>\<input type="text" name="dbfield_txt" id="dbfield_txt"> 

and the correct id from the dropdown in

>\<input type="hidden" name="dbfield" id="dbfield">

field and the correct value in the 

>\<input name="xxxx" id="xxxx"> field automatically

You can then use the hidden field to update the database field in the table by following the update_db_field method (simply add the  **.update** class, the **col**, **colid**, and **colidval** atrributes)

Do not use the _txt field as this will send the text and make the update fail unless the field you are actually updating is of text or varchar type. If you are using foreign keys to identify the item then use the hidden input to trigger the update as the foreign key will be an integer value referencing the main table.
