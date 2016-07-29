## Aster Example Table
```sql
CREATE TABLE listener.sales_data (
 uuid varchar,
 source_id varchar,
 time_stamp time with time zone,
 data varchar
 )
 DISTRIBUTE BY HASH(uuid);
```
