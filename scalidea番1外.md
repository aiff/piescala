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
