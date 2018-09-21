
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
package com.ruozedata.spark.core.day01

import org.apache.spark.{SparkConf, SparkContext}

/**
  * 日志统计分析
  * 11： 域名
  * 20： 流量
  * 7：IP
  * 13：访问路径
  * 分隔符：\t
  */
object LogApp {
  def main(args: Array[String]) {

    // Spark编程模板第一步：创建SparkContext
    val sparkConf = new SparkConf().setAppName("LogApp").setMaster("local[2]")
    val sc = new SparkContext(sparkConf)

    // Spark编程模板第二步：读取日志文件并进行相应的业务逻辑处理
    val lines = sc.textFile("file:///D:/baidu.log")

    //TODO... 需求一：求每个域名的流量
    /**
      * 1） 获取到日志中每条记录的域名(第11字段)和流量(第20字段)
      *     log ==> (11,20)
      * 2） 按照域名进行分组并求和  reduceByKey(_+_)
      */
//    lines.map(x => {
//      val temp = x.split("\t")
//      var traffic = 0L
//      try{
//        traffic = temp(19).trim.toLong
//      } catch {
//        case e:Exception => 0L
//      }
//      (temp(10), traffic)
//    }).reduceByKey(_+_).take(100).foreach(println)

    /**
      * TODO... 求每个省份的访问次数的TopN
      *
      * 1） 获取ip
      * 2） (省份,1)
      * 3） reduceByKey(_+_)  ==> (北京市,100)
      * 4）排序 sortBy
      */
//    lines.map(x => {
//      val temp = x.split("\t")
//      (IpUtils.getProvince(temp(6)),1)
//    }).reduceByKey(_+_).sortBy(_._2, false)

    /**
      *  TODO... 求每个域名下访问数最多的文件资源(/a/b/c/xxx.mp4)
      *
      *  第一个/后到第一个？之前的内容
      *  http://domain/a/b/c/xxx.mp4?x=y&w=z..................
      */
    lines.map(x => {
      val temp = x.split("\t")
      ((temp(10),getResource(temp(12))),1)
  }).reduceByKey(_+_).groupBy(_._1._1)
      .mapValues(_.toList.sortBy(_._2).reverse.take(10))
        .map(_._2)
      .collect().foreach(println)

      //.take(10).foreach(println)

    // Spark编程模板第三步：关闭SparkContext
    sc.stop()
  }


  // TODO... 求访问次数最多的资源文件

  def getResource(url:String) = {
    val pathTemp = url.replaceFirst("//","")
    var pathIndex = pathTemp.indexOf("/")
    var path = ""
    if(pathIndex != -1) {
      path = pathTemp.substring(pathIndex)
      pathIndex = path.indexOf("?")
      if(pathIndex != -1) {
        path = path.substring(0,pathIndex)
      }
    }
    path
  }
}
