# spark-cheats

### DF creation

```scala
import org.apache.spark.sql.SparkSession
import org.apache.spark.sql.types._

object SparkSQLExample {
  def main(args: Array[String]) {
    val spark = SparkSession
      .builder()
      .appName("Spark SQL basic example")
      .config("spark.some.config.option", "some-value")
      .getOrCreate()
    val sc = sparkSession.sparkContext
    
    import spark.implicits._
        
    val rdd = sc.parallelize(1 to 10).map(x => (x, "name" + x.toString))
    val df =  rdd.toDF("number","name")
    df.show()      
  }
}
```

Result will be:
```text
+------+------+
|number|  name|
+------+------+
|     1| name1|
|     2| name2|
|     3| name3|
|     4| name4|
|     5| name5|
|     6| name6|
|     7| name7|
|     8| name8|
|     9| name9|
|    10|name10|
+------+------+
```
```scala
df.printSchema()
```

```text
root
 |-- number: integer (nullable = false)
 |-- name: string (nullable = true)
```
## Work with columns

1.Using $-notation
2.Using SQL
3.Reffering to Dataframe

```scala 
    df.filter($"number" > 5).show()
    df.filter("name like '%1%'").show()
    df.filter(df("number") < 3).show()
```
