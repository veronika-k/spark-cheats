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
