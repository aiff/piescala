# 报错    .sql("show  tables").show

/home/hadoop/apache-hive-1.1.0-cdh5.7.0-bin/lib/mysql-connector-java.jar

```
spark.sql("show tables").show(false)
18/12/04 14:12:20 ERROR ObjectStore: Version information found in metastore 
differs 1.1.0 from expected schema version 1.2.0. Schema verififcation is disabled hive.metastore.schema.verification so setting version.
18/12/04 14:12:21 WARN ObjectStore: Failed to get database global_temp,
returning NoSuchObjectException
+--------+----------------------+-----------+
|database|tableName             |isTemporary|
+--------+----------------------+-----------+
|default |ruozedata_emp         |false      |
|default |ruozedata_emp_external|false      |
|default |ruozedata_emp_managed |false      |
|default |ruozedata_person      |false      |
```
