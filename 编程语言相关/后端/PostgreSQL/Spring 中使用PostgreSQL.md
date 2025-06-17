## 引入依赖

gradle：
```gredle
runtimeOnly 'org.postgresql:postgresql'
```

## 修改`application.yml`

`application.yml`
```yml
spring:  
  datasource:  
    driver-class-name: org.postgresql.Driver  # 上一步引入的依赖
    url: jdbc:postgresql://localhost:5432/ytdemo # 最后为使用的数据库名称 
    username: postgres  # 一般pgsql的默认username为postgres
	password: 123456    # 自定义的密码
```

