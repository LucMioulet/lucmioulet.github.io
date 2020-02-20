# Engineering: Changing the name of a dynamodb table
DynamoDB is a great Key-value database.
One issue with it is that you cannot rename easily a table name. 
This posts presents an easy and safe way of doing it.
Overall you will create a restoration point, create a new table from this restoration point, then delete the old table.

1. Select the table you for which you would like to change the name. 
2. Go to backup tab
3. Create an On demand backup.
4. Go to the backups section of the DynamoDB menu.
5. Select the backup you just created.
6. Click on "restore backup".
7. Define the new name of the table.
8. Click on Restore.

The last operation might take some time. However according to this [doc](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Restore.Tutorial.html) it should not consume any resources.
Eventually you can delete the old table, when you feel safe enough.
