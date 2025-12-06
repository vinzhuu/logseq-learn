tags:: [[Spring Cloud OpenFeign]]
---

- ## 官方文档使用
	- ### 从 Spring Cloud 文档进入
		- 在相应版本的 Spring Cloud 文档中 (如 [Spring Cloud 2021.0.5 文档](https://docs.spring.io/spring-cloud/docs/2021.0.5/reference/html/) )
			- 查看 OpenFeign 文档： [spring-cloud-openfeign](https://docs.spring.io/spring-cloud-openfeign/docs/3.1.5/reference/html/)
			- 查看配置汇总: [Spring Cloud configuration properties](https://docs.spring.io/spring-cloud/docs/2021.0.5/reference/html/configprops.html)
	- ### 从组件首页进入
		- [spring-cloud-openfeign 组件首页](https://spring.io/projects/spring-cloud-openfeign)
- ## 快速开始
	- 创建一个 Maven 项目，POM 文件内容如下：
	  logseq.order-list-type:: number
		- ``` xml
		  <?xml version="1.0" encoding="UTF-8"?>
		  <project xmlns="http://maven.apache.org/POM/4.0.0"
		           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
		      <modelVersion>4.0.0</modelVersion>
		  
		      <groupId>org.example</groupId>
		      <artifactId>openfeign-demo</artifactId>
		      <version>1.0-SNAPSHOT</version>
		  
		      <properties>
		          <maven.compiler.source>8</maven.compiler.source>
		          <maven.compiler.target>8</maven.compiler.target>
		          <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		  
		          <spring.boot.version>2.6.13</spring.boot.version>
		          <spring.cloud.version>2021.0.5</spring.cloud.version>
		      </properties>
		  
		      <dependencyManagement>
		          <dependencies>
		              <!-- ======================= Spring Boot 依赖约束 ======================= -->
		  
		              <dependency>
		                  <groupId>org.springframework.boot</groupId>
		                  <artifactId>spring-boot-dependencies</artifactId>
		                  <version>${spring.boot.version}</version>
		                  <type>pom</type>
		                  <scope>import</scope>
		              </dependency>
		  
		              <!-- ======================= Spring Cloud 依赖约束 ======================= -->
		  
		              <dependency>
		                  <groupId>org.springframework.cloud</groupId>
		                  <artifactId>spring-cloud-dependencies</artifactId>
		                  <version>${spring.cloud.version}</version>
		                  <type>pom</type>
		                  <scope>import</scope>
		              </dependency>
		          </dependencies>
		      </dependencyManagement>
		  
		      <dependencies>
		          <!-- Spring Boot 启动依赖  -->
		          <dependency>
		              <groupId>org.springframework.boot</groupId>
		              <artifactId>spring-boot-starter</artifactId>
		          </dependency>
		  
		          <!-- Spring Boot Web  -->
		          <dependency>
		              <groupId>org.springframework.boot</groupId>
		              <artifactId>spring-boot-starter-web</artifactId>
		          </dependency>
		  
		          <!-- openfeign -->
		          <dependency>
		              <groupId>org.springframework.cloud</groupId>
		              <artifactId>spring-cloud-starter-openfeign</artifactId>
		          </dependency>
		      </dependencies>
		  </project>
		  ```
	- 创建一个启动类, 并注意加上 `@EnableFeignClients` 以开启 Feign Client 功能。
	  logseq.order-list-type:: number
		- ``` java
		  @SpringBootApplication
		  @EnableFeignClients
		  public class App {
		  	public static void main(String[] args) {
		  		SpringApplication.run(App.class, args);
		  	}
		  }
		  ```
	- 创建一个 Feign Client 接口类。
	  logseq.order-list-type:: number
		- Spring Boot 会为该接口创建代理对象，并加到 Bean 容器中。
			- ``` java
			  @FeignClient(value = "name", url = "https://api.github.com")
			  public interface GithubApiClient {
			  	@GetMapping("/zen")
			  	String getZen();
			  }
			  ```
	- 从容器中获取 Feign Client 的 Bean，调用其方法 (在 main 方法中调用)。
	  logseq.order-list-type:: number
		- ``` java
		  @SpringBootApplication
		  @EnableFeignClients
		  public class App {
		  	public static void main(String[] args) {
		  		ConfigurableApplicationContext run = SpringApplication.run(App.class, args);
		  		GithubApiClient githubApiClient = run.getBean(GithubApiClient.class);
		  		System.out.println(githubApiClient.getZen());
		  	}
		  }
		  ```
- ## @EnableFeignClients
	- 用于标注 `@Configuration-annotated-classes` ，已开启 Feign Client 功能。
	- 它有如下几个属性：
		- `value` / `basePackages` : 指定 Feign Client 所在的包路径。
			- 如 `com.example` .
		- `basePackageClasses` : 指定 Feign Client 所在的包的某一个类的 `class` 对象，配置后，会扫描此类所在包，及其子包。
			- 相较于 `basePackages` 配置字符串路径，这个配置类型安全 (type-safe) 。
			- 可以在 Feign Client 所在包的根目录，声明一个无任何代码的类 (注意：Feign Client 无需继承这个类)，配置到 `basePackageClasses` 属性。
		- `defaultConfiguration` : 指定所有 Feign Client 的默认配置类。
		- `clients` : 指定使用 `@FeignClient` 标注的类，该属性配置后, `basePackages` 和 `basePackageClasses` 将无效。
		-
- ## @FeignClient
	- ### Feign Client
		- 使用 `@FeignClient` 标注的接口类即可视为一个 Feign Client ，他是一系列