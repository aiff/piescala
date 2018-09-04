
scala> val df=spark.read.json("file:///home/cs/spark-2.2.1-bin-hadoop2.7/examples/src/main/resources/people.json")
18/09/04 19:42:28 ERROR ObjectStore: Version information found in metastore differs 1.1.0 from expected schema version 1.2.0. Schema verififcation is disabled hive.metastore.schema.verification so setting version.
18/09/04 19:42:28 WARN ObjectStore: Failed to get database global_temp, returning NoSuchObjectException
df: org.apache.spark.sql.DataFrame = [age: bigint, name: string]

scala> df.p
persist   printSchema

scala> df.printSchema
   def printSchema(): Unit

scala> df.printSchema
root
 |-- age: long (nullable = true)
 |-- name: string (nullable = true)
