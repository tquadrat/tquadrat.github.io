# Does *Table* exist?

One problem that I have quite often is that I need to check whether a particular table (already) exists.

  1. [JDBC in General](#jdbc-in-general)
  2. [H2](#h2)

## JDBC in General

The generic solution for JDBC is

```java
public final boolean hasTable( final Connection connection, final String catalog, final String schemaPattern, final String tableNamePattern, final String... tableTypes ) throws SQLException
{
    final var metaData = connection.getMetaData();
    var retValue = false;
    final String [] effectiveTypes = nonNull( tableTypes ) && tableTypes.length == 0 ? null : tableTypes;
    try( final var resultSet = metaData.getTables( catalog, schemaPattern, tableNamePattern, effectiveTypes ) )
    {
        retValue = resultSet.next();
    }
    
    //---* Done *------------------------------------------------
    return retValue;
}   //  hasTable()
```
Obviously, `connection` is the connection instance that connects the program to the RDBMS. `catalog` is the name of the catalog; the empty string "" stands for no catalog, `null` for all catalogs. Same for `schemaPattern`, representing the schema. 'Pattern' means that the wildcard characters '%' and '\_' can be used. 

The name of the desired table is given with `tableNamePattern` – and when really a pattern is used, the method would return `true` if at least one match was achieved.

`tableTypes` finally is a list of table types, as returned by `DatabaseMetaData.getTableTypes()`. If empty, any type is returned.

## Particular Databases

The check whether a particular *Table* exists can be done also with a `SELECT` statement that might look different for the various RDBMS.

### H2

For H2, the SQL to lookup a *Table* by name looks like this:
```sql
SELECT * FROM information_schema.tables
    WHERE TABLE_NAME = ?
        AND TABLE_SCHEMA = 'PUBLIC'
```
Of course, `PUBLIC` must be replaced by the proper schema name if the table is not in the default public schema.
