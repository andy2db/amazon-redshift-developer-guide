# UPDATE<a name="r_UPDATE"></a>


+ [Syntax](#r_UPDATE-synopsis)
+ [Parameters](#r_UPDATE-parameters)
+ [Usage Notes](#r_UPDATE_usage_notes)
+ [Examples of UPDATE Statements](c_Examples_of_UPDATE_statements.md)

Updates values in one or more table columns when a condition is satisfied\. 

**Note**  
The maximum size for a single SQL statement is 16 MB\.

## Syntax<a name="r_UPDATE-synopsis"></a>

```
UPDATE table_name SET column = { expression | DEFAULT } [,...]
[ FROM fromlist ]
[ WHERE condition ]
```

## Parameters<a name="r_UPDATE-parameters"></a>

 *table\_name*   
A temporary or persistent table\. Only the owner of the table or a user with UPDATE privilege on the table may update rows\. If you use the FROM clause or select from tables in an expression or condition, you must have SELECT privilege on those tables\. You cannot give the table an alias here; however, you can specify an alias in the FROM clause\.   
Amazon Redshift Spectrum external tables are read\-only\. You can't UPDATE an external table\.

SET *column* =   
One or more columns that you want to modify\. Columns that are not listed retain their current values\. Do not include the table name in the specification of a target column\. For example, `UPDATE tab SET tab.col = 1` is invalid\.

 *expression*   
An expression that defines the new value for the specified column\. 

DEFAULT   
Updates the column with the default value that was assigned to the column in the CREATE TABLE statement\. 

FROM *tablelist*   
You can update a table by referencing information in other tables\. List these other tables in the FROM clause or use a subquery as part of the WHERE condition\. Tables listed in the FROM clause can have aliases\. If you need to include the target table of the UPDATE statement in the list, use an alias\. 

WHERE *condition*   
Optional clause that restricts updates to rows that match a condition\. When the condition returns `true`, the specified SET columns are updated\. The condition can be a simple predicate on a column or a condition based on the result of a subquery\.   
You can name any table in the subquery, including the target table for the UPDATE\. 

## Usage Notes<a name="r_UPDATE_usage_notes"></a>

After updating a large number of rows in a table: 

+ Vacuum the table to reclaim storage space and resort rows\. 

+ Analyze the table to update statistics for the query planner\. 

Left, right, and full outer joins are not supported in the FROM clause of an UPDATE statement; they return the following error: 

```
ERROR: Target table must be part of an equijoin predicate
```

 If you need to specify an outer join, use a subquery in the WHERE clause of the UPDATE statement\. 

If your UPDATE statement requires a self\-join to the target table, you need to specify the join condition as well as the WHERE clause criteria that qualify rows for the update operation\. In general, when the target table is joined to itself or another table, a best practice is to use a subquery that clearly separates the join conditions from the criteria that qualify rows for updates\. 