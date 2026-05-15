# RDBMS Data Types for Date Values, Time Values, TimeDate Values and TimeStamps

The original JDBC implementation used `java.util.Date` as well as `java.sql.Date`, `java.sql.Time` and `java.sql.Timestamp`, with all the shortcomings of the `java.util.Date` class.

The new time/date classes from the `java.time` package that were introduced with Java&nsp;8 are made available by some JDBC drivers through the `PreparedStatement.setObject()` and `ResultSet.getObject()` APIs. But still the various RDBMS products will handle date/time values differently.

 1. [H2](#h2)
 2. [PostgreSQL](#postgresql)
 3. [Derby (Apache DB)](#derby-apache-db)
* * *

## Particular Databases

### H2

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

According to the [documentation](https://jdbc.postgresql.org/documentation/head/java8-date-time.html), PostgreSQL does support the new `java.time` types as shown in the table below:

|PostgreSQL™ Type|Java Type|
|----------------|---------|
|`DATE`|`java.time.LocalDate`|
|`TIME` [ `WITHOUT TIME ZONE` ]|`java.time.LocalTime`|
|`TIMESTAMP` [ `WITHOUT TIME ZONE` ]|`java.time.LocalDateTime`|
|`TIMESTAMP WITH TIME ZONE`|`java.time.OffsetDateTime`|

This is closely aligned with tables B-4 and B-5 of the JDBC 4.2 specification. It is important that `java.time.ZonedDateTime`, `java.time.Instant` and `java.time.OffsetTime` are not suppported, also not the use of `TIME WITH TIME ZONE` with JDBC. Also note that all `java.time.OffsetDateTime` instances will be in UTC (have offset 00:00). This is because the backend stores them as UTC.

These sample were taken from the PostgreSQL documentation linked above:

#### Reading Java 8 Date and Time values using JDBC
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

#### Writing Java 8 Date and Time values using JDBC
```Java
LocalDate localDate = LocalDate.now();
PreparedStatement st = conn.prepareStatement( "INSERT INTO mytable (columnfoo) VALUES (?)" );
st.setObject( 1, localDate );
st.executeUpdate();
st.close();
```

I reformatted the code slightly and fixed the syntax error … 

### Derby (Apache DB)

Apache Derby supports only `java.sql.Date`, `java.sql.Time` and `java.sql.Timestamp` for the SQL data types `DATE`, `TIME` and `TIMESTAMP`.
