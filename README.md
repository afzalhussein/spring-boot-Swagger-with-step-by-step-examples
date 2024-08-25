# spring-boot-Swagger-with-step-by-step-examples

Swagger is a popular tool for documenting and testing RESTful APIs. In this guide, I'll teach you how to integrate Swagger with a Spring Boot application step by step.

### Step 1: Create a Spring Boot Project

You can create a new Spring Boot project using Spring Initializr (https://start.spring.io/) or your favorite integrated development environment (IDE). Make sure to include the "Spring Web" and "Spring Boot DevTools" dependencies.

### Step 2: Add Swagger Dependencies

Open your project's `pom.xml` file (for Maven) or `build.gradle` (for Gradle) and add the following dependencies:

For Maven:
```xml
<dependencies>
    <!-- Other dependencies -->
    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-boot-starter</artifactId>
        <version>3.0.0</version>
    </dependency>
</dependencies>
```

For Gradle:
```groovy
dependencies {
    // Other dependencies
    implementation 'io.springfox:springfox-boot-starter:3.0.0'
}
```

### Step 3: Configure Swagger

Create a configuration class to enable Swagger in your Spring Boot application. In the `src/main/java` directory, create a package (e.g., `com.example.swaggerdemo`) and create a class named `SwaggerConfig` inside it.

```java
package com.example.swaggerdemo;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
public class SwaggerConfig {

    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.example.swaggerdemo")) // Replace with your base package
                .build()
                .apiInfo(apiInfo());
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("Swagger Demo API")
                .description("Sample API for Swagger documentation")
                .version("1.0")
                .build();
    }
}
```

In this configuration class:

- We enable Swagger using `@EnableSwagger2`.
- We configure Swagger to scan and document the APIs in the specified base package.
- We define API information such as title, description, and version.

Replace `"com.example.swaggerdemo"` with the base package of your Spring Boot application.

### Step 4: Create an API Controller

Create a RESTful API controller that you want to document with Swagger. For example, create a class named `DemoController` in the same package as your `SwaggerConfig` class:

```java
package com.example.swaggerdemo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class DemoController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Swagger!";
    }
}
```

### Step 5: Run Your Application

Run your Spring Boot application. You can use your IDE or use the following Maven or Gradle command:

For Maven:
```bash
mvn spring-boot:run
```

For Gradle:
```bash
./gradlew bootRun
```

Your application will start, and you can access the Swagger UI at `http://localhost:8080/swagger-ui.html` (assuming your application is running on port 8080).

### Step 6: Explore and Test Your API

With Swagger UI, you can explore your API documentation and test your API endpoints interactively. You'll see a list of available endpoints, and you can click on them to see details and execute requests.

### Conclusion

You've successfully integrated Swagger with your Spring Boot application. Swagger provides a convenient way to document and test your RESTful APIs, making it easier for developers to understand and interact with your API endpoints. You can further customize Swagger configurations and annotations to provide more detailed documentation for your API.
