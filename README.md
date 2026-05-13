# Spring MVC Employee Details Demo

A lightweight educational **Spring MVC** web application that demonstrates how request handling, controller methods, model attributes, and JSP views work together in a classic Java web stack.

## Overview

This project contains a small workflow:

1. Open the home page.
2. Navigate to an employee details form.
3. Submit an employee name.
4. Display the processed result on a response page.

The app is designed as a learning example for:

- `@Controller` and `@RequestMapping`
- Parameter binding with `@RequestParam`
- Passing data to a view through `Model`
- JSP rendering with `InternalResourceViewResolver`
- DispatcherServlet configuration in `web.xml`

## Tech Stack

- **Java 17**
- **Maven** (`war` packaging)
- **Spring Framework** (core/context/beans + Spring MVC)
- **JSP + JSTL**
- **Servlet API**

## Project Structure

```text
src/
├── main/
│   ├── java/com/puhaev/spring/mvc/
│   │   └── MyController.java
│   └── webapp/WEB-INF/
│       ├── applicationContext.xml
│       ├── web.xml
│       └── view/
│           ├── first-view.jsp
│           ├── ask-emp-details-view.jsp
│           └── show-emp-details-view.jsp
└── ...
```

## Request Flow

- `GET /` → returns `first-view.jsp`
- `GET /askDetails` → returns `ask-emp-details-view.jsp`
- Request to `/showDetails` with `employeeName` parameter:
  - Controller receives the value via `@RequestParam("employeeName")`
  - Adds formatting (`Mr. <name>!`)
  - Puts it into `Model` as `nameAttribute`
  - Returns `show-emp-details-view.jsp`

## Configuration Notes

### `web.xml`

- Registers Spring `DispatcherServlet` with name `dispatcher`
- Loads context from `/WEB-INF/applicationContext.xml`
- Maps servlet to `/` so all requests are handled by Spring MVC

### `applicationContext.xml`

- Scans controllers in `com.puhaev.spring.mvc`
- Enables annotation-based MVC handling
- Configures JSP resolver:
  - prefix: `/WEB-INF/view/`
  - suffix: `.jsp`

## How to Build

```bash
mvn clean package
```

This produces a WAR file in `target/` (for example: `spring_course_mvc.war`).

## How to Run

Deploy the generated WAR to a Java servlet container (for example, Apache Tomcat 9).

Typical steps:

1. Build the project: `mvn clean package`
2. Copy WAR from `target/` to your container deployment directory (e.g. `webapps/`)
3. Start the servlet container
4. Open the application in a browser

Example URL pattern:

```text
http://localhost:8080/spring_course_mvc/
```

> The exact context path depends on your server deployment settings.

## Learning Highlights

- Demonstrates progressive evolution of controller method styles (raw request, model binding, `@RequestParam`) in the source.
- Keeps configuration explicit (XML + servlet descriptor), which is useful for understanding legacy and foundational Spring MVC setups.
- Serves as a good starter template before moving to Java-based config or Spring Boot.

## Potential Improvements

- Align Spring dependency versions (currently mixed major versions in `pom.xml`)
- Add form validation (`@Valid`, `BindingResult`)
- Add unit/integration tests for controller endpoints
- Add a modern build profile for embedded server execution
- Migrate to Jakarta Servlet APIs for newer containers

## License

Educational sample project for learning purposes.
