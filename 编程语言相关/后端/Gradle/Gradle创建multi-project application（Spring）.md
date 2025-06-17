
## 基本结构

创建完成后，项目的基本结构如下
```text
root-project
├── build.gradle      // gradle配置文件
├── app               // 入口项目
├── child-project1    // 子项目
├── child-project2
├── child-project3
└── settings.gradle   // gradle配置文件
```

## 0. 创建项目

直接使用`IDEA`提供的`Spring Initializer`即可，构建工具选择`Gradle`

如果没有`Spring Initializer`，可以使用[Spring官方构建网站](https://start.spring.io/)
## 1. `root-project`

### 1.1. 删除src文件夹

**构建完成后删除`src`目录**，因为根目录属于管理模块目录不提供运行的应用

### 1.2. 配置`build.gradle`文件 

修改结果
```groovy
buildscript{  
   ext {  
  
   }   allprojects {  
      gradle.projectsEvaluated {  
         allprojects {  
            jar{ enabled  = true}  
         }      }   }}  
  
  
plugins {  
   id 'groovy'  
   id 'org.springframework.boot' version '3.1.6'  
   id 'io.spring.dependency-management' version '1.1.4'  
}  

// 所有project都应用以下设定
allprojects {  
   repositories {  
      mavenCentral()  
   }  
}  

// 所有 子 project都应用以下设定
subprojects {  
   group = 'com.hoso'  
   version = '0.0.1-SNAPSHOT'  

	// 子项目中添加的插件（和上面的plugins内容一致）
   apply plugin: 'groovy'  
   apply plugin: 'org.springframework.boot'  
   apply plugin: 'io.spring.dependency-management' 
   // ※ 所有子项目默认不创建启动jar包 ※
   bootJar{  
      enabled=false  
   }  
   ext {}  
   // 子项目会用到的依赖项
   dependencies {  
      implementation 'org.springframework.boot:spring-boot-starter-data-jpa'  
      implementation 'org.springframework.boot:spring-boot-starter-validation'  
      implementation 'org.springframework.boot:spring-boot-starter-web'  
      implementation 'org.apache.groovy:groovy'  
      compileOnly 'org.projectlombok:lombok'  
      developmentOnly 'org.springframework.boot:spring-boot-devtools'  
      runtimeOnly 'org.postgresql:postgresql'  
      annotationProcessor 'org.projectlombok:lombok'  
      testImplementation 'org.springframework.boot:spring-boot-starter-test'  
      implementation 'com.auth0:java-jwt:4.4.0'  
   }  
  
   tasks.named('bootBuildImage') {  
      builder = 'paketobuildpacks/builder-jammy-base:latest'  
   }  
  
   tasks.named('test') {  
      useJUnitPlatform()  
   }  
}  
  
  
java {  
   sourceCompatibility = '17'  
}  
  
configurations {  
   compileOnly {  
      extendsFrom annotationProcessor  
   }  
}
```


## 2. 创建子project

### 创建方法
右键root-project，创建新的Module
Build system 选择Gradle
Parent 选择root-project

### 2.1. app（启动入口project）

app 模块用于启动项目，Spring的启动Application文件写在这里。

#### 2.1.1. 修改`build.gradle`文件

1. 删除所有内容，只留下：
```groovy
repositories {  
    mavenCentral()  
}
```

2. 覆盖父级的bootJar设定
```groovy
bootJar{  
    enabled = true  
}
```

3. 添加依赖项
```groovy
dependencies {  
    implementation project(":child-project1")  
	implementation project(":child-project2")  
	implementation project(":child-project3")  
}
```

#### 2.1.2 创建`Application.java`
app: com.example.app.Application.java
```java
package com.hoso.app;  
  
import org.springframework.boot.SpringApplication;  
import org.springframework.boot.autoconfigure.SpringBootApplication;  

@MapperScan("com.example.mapper")
@SpringBootApplication(scanBasePackages = "com.example")  
public class Application {  
    public static void main(String[] args){  
        SpringApplication.run(Application.class,args);  
    }  
}
```

>**注意：**
>**因为`Spring Boot`无法自动识别其他模块下的类，所以需要手动处理一下，有三种方法**：
>1. **使用`@Import`**，也就是`@Import(TestService.class)`
>2. **使用`scanBasePackageClasses`**，也就是
>`@SpringBootApplication(scanBasePackageClasses={TestService.class})`
>3. **使用`scanBasePackages`**，也就是例子中的代码`@SpringBootApplication(scanBasePackages = "com.example")`

>有可能会遇到 SpringBoot项目启动报错：Field Mapper in ServiceImpl required a bean of type ‘Mapper‘ that could not be found
>这时需要添加注解:`@MapperScan("com.example.mapper")`

### 2.2. 创建其他子project

使用创建方法创建子项目。
每个子项目分别写自己的`Controller`，`Service`等包。
