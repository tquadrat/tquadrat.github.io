# Database Lore


I bareley know how to spell database correctly, so I am quite often surprised about details about RBDMS and other databases that other will not even notice as something remarkable. Some of these things are collected here, and some of it made its way into a *Foundation* Library with some tools related to JDBC.

## JDBC in General

### Does *Table* exist?

One problem that I have quite often is that I need to check whether a particular table (already) exists.

The generic solution is

```java
public final boolean hasTable( final Connection connection, final String catalog, final String schemaPattern, final String tableNamePattern, final String... tableTypes ) throws SQLException
{
    final var metaData = connection.getMetaData();
    var retValue = false;
    final String [] effectiveTypes = nonNull( tableTypes ) && tableTypes.length == 0 ? null : tableTypes;
    try( final var resultSet = metaData.getTables( catalog, schemaPattern, tableNamePattern, effectiveTypes ) )
    {
        retValue = resultSet.hasNext();
    }
}   //  hasTable()
```
Obviously, `connection` is the connection instance that connects the program to the RDBMS. `catalog` is the name of the catalog; the empty string "" stands for no catalog, `null` for all catalogs. Same for `schemaPattern`, representing the schema. 'Pattern' means that the wildcard characters '%' and '\_' can be used. 

The name of the desired table is given with `tableNamePattern` – and when really a pattern is used, the method would return `true` if at least one match was achieved.

`tableTypes` finally is a list of table types, as returned by `DatabaseMetaData.getTableTypes()`. If empty, any type is returned.

### Data Types for Date Values, Time Values, TimeDate Values and TimeStamps

The original JDBC implementation used `java.util.Date` as well as `java.sql.Date`, `java.sql.Time` and `java.sql.Timestamp`, with all the shortcomings of the `java.util.Date` class.

The new time/date classes from the `java.time` package that were introduced with Java 8 are made available by some JDBC drivers through the `PreparedStatement.setObject()` and `ResultSet.getObject()` APIs.

* * *

## Particular Databases

### H2

#### Does *Table* exist?

The problem described [above](#does-table-exist) can be solved also with a `SELECT` statement; for H2 it looks like this

```sql
SELECT * FROM information_schema.tables
    WHERE TABLE_NAME = ?
        AND TABLE_SCHEMA = 'PUBLIC'
```
Of course, `PUBLIC` must be replaced by the proper schema name if the table is not in the default public schema.

#### Data Types for Date Values, Time Values, TimeDate Values and TimeStamps

H2 allows the mapping of its datatypes `DATE`, `TIME`, `TIME WITH TIME ZONE`, `TIMESTAMP`, `TIMESTAMP WITHOUT TIME ZONE`, `DATETIME`, `SMALLDATETIME` and `TIMESTAMP WITH TIME ZONE` to the new `java.time` types that were introduced with Java 8 like the table below: 

|H2 SQL Type|Java Types|
|--------|----------|
|`DATE`|`java.sql.Date`, **`java.time.LocalDate`**|
|`TIME`|`java.sql.Time`, **`java.time.LocalTime`**|
|`TIME WITH TIME ZONE`|**`java.time.OffsetTime`**|
|`TIMESTAMP`|`java.sql.Timestamp`, `java.util.Date`, **`java.time.LocalDateTime`**|
|`TIMESTAMP WITHOUT TIME ZONE`|`java.sql.Timestamp`, `java.util.Date`, **`java.time.LocalDateTime`**|
|`DATETIME`|`java.sql.Timestamp`, `java.util.Date`, **`java.time.LocalDateTime`**|
|`SMALLDATETIME`|`java.sql.Timestamp`, `java.util.Date`, **`java.time.LocalDateTime`**|
|`TIMESTAMP WITH TIME ZONE`|**`java.time.OffsetDateTime`**, `java.time.ZonedDateTime`, `java.time.Instant`|

The recommended Java type is shown in **`bold`**.

Sample code:
```java
final ResultSet resultSet = …
…
LocalDateTime dateTime = resultSet.getObject( "DATE_TIME", LocalDateTime.class ); // for a TIMESTAMP column
…
final ZoneDateTime today = …
final PreparedStatement statement = …
…
statement.setObject( 7, today ); // for a TIMESTAMP WITH TIME ZONE column
…
```

### PostgreSQL

#### Data Types for Date Values, Time Values, TimeDate Values and TimeStamps

According to the [documentation](https://jdbc.postgresql.org/documentation/head/java8-date-time.html), PostgreSQL does support the new `java.time` types as shown in the table below:

|PostgreSQL™ Type|Java Type|
|----------------|---------|
|`DATE`|`java.time.LocalDate`|
|`TIME` [ `WITHOUT TIME ZONE` ]|`java.time.LocalTime`|
|`TIMESTAMP` [ `WITHOUT TIME ZONE` ]|`java.time.LocalDateTime`|
|`TIMESTAMP WITH TIME ZONE`|`java.time.OffsetDateTime`|

This is closely aligned with tables B-4 and B-5 of the JDBC 4.2 specification. It is important that `java.time.ZonedDateTime`, `java.time.Instant` and `java.time.OffsetTime` are not suppported, also not the use of `TIME WITH TIME ZONE` with JDBC. Also note that all `java.time.OffsetDateTime` instances will be in UTC (have offset 00:00). This is because the backend stores them as UTC.

These sample were taken from the PostgreSQL documentation linked above:

##### Reading Java 8 Date and Time values using JDBC
```Java
Statement st = conn.createStatement();
ResultSet rs = st.executeQuery( "SELECT * FROM mytable WHERE columnfoo = 500" );
while( rs.next() )
{
    System.out.print( "Column 1 returned " );
    LocalDate localDate = rs.getObject( 1, LocalDate.class );
    System.out.println( localDate );
}
rs.close();
st.close();
````

##### Writing Java 8 Date and Time values using JDBC
```Java
LocalDate localDate = LocalDate.now();
PreparedStatement st = conn.prepareStatement( "INSERT INTO mytable (columnfoo) VALUES (?)" );
st.setObject( 1, localDate );
st.executeUpdate();
st.close();
```

I reformatted the code slightly and fixed the syntax error … 

### Derby (Apache DB)

#### Data Types for Date Values, Time Values, TimeDate Values and TimeStamps

Derby supports only `java.sql.Date`, `java.sql.Time` and `java.sql.Timestamp` for the SQL data types `DATE`, `TIME` and `TIMESTAMP`.
