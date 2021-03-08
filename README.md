# javaeurekaserver
```
java eureka注册中心

打包：
  mvn clean package

部署执行：
    java -jar target/javaeurekaserver-1.0-SNAPSHOT.jar --spring.profiles.active=node1
    java -jar target/javaeurekaserver-1.0-SNAPSHOT.jar --spring.profiles.active=node2
    java -jar target/javaeurekaserver-1.0-SNAPSHOT.jar --spring.profiles.active=node3

浏览器访问：
    http://localhost:8761/
    http://localhost:8762/
    http://localhost:8763/

```

