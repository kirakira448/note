
# 目录结构

## 1. 总览

```txt
spring-gradle-template
│  build.gradle    # 父级的gradle文件，通用依赖都写在这里
│  gradlew         # Linux 下可执行脚本
│  gradlew.bat     # Windows 下可执行脚本
│  settings.gradle   # 项目的必要设置，如：模块依赖关系
│
├─biz-1-app           # 启动模块
│
├─biz-1			# 业务模块 1，自定义名称
│
├─biz-2			# 业务模块 2，自定义名称
│
├─biz-common		# 业务相关的通用文件，当移除后，剩下的就是一个基础的后端api框架
│
├─common			# 通用的utils，dao，固定值定义等
│
├─gradle			# 父级gradle目录
│
├─src				# 父级生成的src目录，可以删除
│
└─web-common		# web相关的通用文件，如：request模块，response模块
```


## 2. biz-1-app结构

```txt
app
│  build.gradle                       # 所有要启动的项目都要在这里定义依赖
├─src/
	├── main/
	│   ├── java/
	│   │   ├── com/
	│   │   │   ├── hoso/
	│   │   │   │   └── Application.java      # Spring Boot 应用程序入口
	│   ├── resources/                        # 资源文件夹
	│   │   ├── static/                       # 静态资源
	│   │   ├── templates/                    # 模板文件（如果使用模板引擎）
	│   │   └── application.yml               # 应用程序配置文件，数据库的配置也写在这
	└── test/                                 # 测试代码
	    └── java/
	        └── com/
	            └── example/
	                └── controller/           # 控制器测试
	                    └── UserControllerTest.java
```

## 3. biz-1结构

```txt
biz-2
│  build.gradle
├─src/
	├── main/
	│   ├── java/
	│   │   ├── com/
	│   │   │   ├── hoso/
	│   │   │   │   ├── controllers/           # 控制器类
	│   │   │   │   │   └── UserController.java
	│   │   │   │   ├── services/              # 服务类接口和实现
	│   │   │   │   │   ├── impl/	
	│	│   │   │   │   │   └── UserServiceImpl.java
	│   │   │   │   │   └── UserService.java
	│   │   │   │   ├── mappers/           # 数据访问层接口
	│   │   │   │   │   └── UserMapper.java
	│   │   │   │   ├── models/                # 实体类和DTO
	│	│   │   │   │   ├──bean
	│   │	│   │   │   │   └──UserBean.java
	│   │   │   │   │   └──dto
	│	│   │   │   │       └── UserInfoDto.java
	│   │   │   │   ├── configs/               # 配置类
	│   │   │   │       └── AppConfig.java
	│   ├── resources/                        # 资源文件夹
	│       ├── templates/                    # 模板文件（如果使用模板引擎）
	│	        └── com/
	│	             └── hoso/
	│	                  └──mapper/         # 数据访问层实现
	│	                      └── UserMapper.xml
	│    
	└── test/                                 # 测试代码
	    └── java/
	        └── com/
	            └── hoso/
	                └── controller/           # 控制器测试
	                    └── UserControllerTest.java
					

```


# 命名规则

## Bean
所有字段使用驼峰命名（“camelCase”）

在`application.yml`中添加如下配置，用于和数据库字段匹配
```yml
mybatis:  
  configuration:  
    map-underscore-to-camel-case: true  # CamelCase convert to snake_case
```

# 关于时间格式

## postgresql

时间使用 `timestamp` 格式存储

## Java-Spring
使用`Timestamp`接收

# Swagger配置

### 依赖项

最外层的`build.gradle`中添加如下依赖
```groovy
dependencies {
	// ...
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.1.0'  
}
```

### 如果有拦截器

在拦截器的`excludePathPatterns`中添加以下url
```
{"/swagger-ui/**","/swagger-ui/**.html","/swagger-ui/**.css","/swagger-ui/**.js","/v3/api-docs/**"}
```

>按照逻辑，本来添加`{"/swagger-ui/**", "/v3/api-docs/**"}`就足够了，
>但是暂时没有搞清楚为什么`"/swagger-ui/**"`不能正确生效。

### 访问路径

path: http://{host}:{port}/{context-path}/swagger-ui/index.html


# mybatis映射

如果想用xml映射sql语句，需要在resources中构建相同的目录结构

### 错误示范

java目录：
```
├── java/
│   ├── com/
│   │   ├── hoso/
│   │   │   ├── product/
│   │   │   │   ├── mappers/
```

resources目录：
```
├── resources/
│   ├── com.hoso.product.mappers
```

这样在idea中看起来是一样的，但是实际上路径不一样

### 正确做法

resources目录：
```
├── resources/
│   ├── com/
│   │   ├── hoso/
│   │   │   ├── product/
│   │   │   │   ├── mappers/
```