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

## nginx配置示例
```
upstream sgp_eureka {
   server 127.0.0.1:8083;
}
server {
        listen 80;
        set $app_name "eureka";
        #注册中心：http://dev-eureka-开发者.nfangbian.com/
        server_name  ~^dev-eureka-(?<cloud_name>\w+)\.nfangbian\.com$;
        #server_name     dev-eureka.nfangbian.com;

        access_log  /data1/logs/nginx/$app_name.$cloud_name.access.log  main;
        error_log  /data1/logs/nginx/eureka.error.log;

        location / {
            proxy_pass http://sgp_eureka;
            #proxy_redirect off;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $host;
        }

       	proxy_intercept_errors on;
	    error_page 500 502 503 504 = /5xx.html;
	    error_page 404 405 = /4xx.html;

}

```
