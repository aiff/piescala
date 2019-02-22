# 默认的scala配置版本一片爆红  pom配置不对 导致的 meave报错 重新修改  然后要下载更新。。。
`````````
<build>
    <plugins>

      <plugin>
        <groupId>org.scala-tools</groupId>
        <artifactId>maven-scala-plugin</artifactId>
        <version>2.15.2</version>
       <executions>
          <execution>
            <goals>
              <goal>compile</goal>
             <!-- <goal>testCompile</goal>-->
            </goals>
          </execution>
        </executions>
      </plugin>

      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.6.0</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
          <skip>true</skip>
        </configuration>
      </plugin>

      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.19</version>
        <configuration>
          <skip>true</skip>
        </configuration>
      </plugin>

    </plugins>
  </build>
````````
##  错误
````
Exception in thread "main" org.apache.spark.SparkException: Job aborted due to stage failure: Task 0 in stage 0.0 failed 1 times, most recent failure: Lost task 0.0 in stage 0.0 (TID 0, localhost, executor driver): java.lang.ArrayIndexOutOfBoundsException: 1 at com.ruoze.pipe.pie$$anonfun$main$1.apply(pie.scala:26)

```主要是取值的时候 超过下标了
