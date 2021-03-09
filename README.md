# javaeurekaserver
```
java eureka注册中心

打包：
  mvn clean package

部署执行：
    创建日志目录：
        mkdir -p /data/logs/java/euraka-server

    启动集群服务：
        java -jar target/javaeurekaserver-1.0-SNAPSHOT.jar --spring.profiles.active=node1
        java -jar target/javaeurekaserver-1.0-SNAPSHOT.jar --spring.profiles.active=node2
        java -jar target/javaeurekaserver-1.0-SNAPSHOT.jar --spring.profiles.active=node3
    
    启动单机服务：
        java -jar target/javaeurekaserver-1.0-SNAPSHOT.jar --spring.profiles.active=standalone
        可以通过参数设置注册中心名称： -Deureka.datacenter=cloud ，默认值为default


浏览器访问：
    http://localhost:8761/
    http://localhost:8762/
    http://localhost:8763/

```

## 配置说明
```
spring.application.name=eureka-server #服务名，即应用名
server.port=8083 #监听的端口
eureka.instance.hostname=localhost  #服务访问host地址
eureka.environment=prod   #环境代号，不指定则默认为是test
eureka.datacenter=mycloud01 #指定数据中心名，默认default
eureka.client.registerWithEureka=true  #是否注册到注册中心
eureka.client.fetchRegistry=true
# 注册中心地址，多个用逗号分隔
eureka.client.service-url.defaultZone=http://${eureka.instance.hostname}:${server.port}/eureka/


```

