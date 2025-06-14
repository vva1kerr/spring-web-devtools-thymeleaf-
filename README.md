# Spring Boot Demo Project

This is a Spring Boot web application that demonstrates the basic setup and functionality of a Spring Boot project.

## Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── com/
│   │       └── sg/
│   │           └── springbootdemo/
│   │               ├── controller/    # REST controllers
│   │               └── SpringbootdemoApplication.java  # Main application class
│   └── resources/
│       └── templates/  # Thymeleaf templates
└── test/              # Test files
```

## Technologies Used

- Java 21
- Spring Boot 3.5.0
- Spring Web
- Thymeleaf (Template Engine)
- Spring Boot DevTools
- Maven (Build Tool)

## Getting Started

### Prerequisites

- Java 21 or higher
- Maven 3.6.x or higher

### Running the Application

1. Clone the repository
2. Navigate to the project directory
3. Run the application using Maven:
   ```bash
   ./mvnw spring-boot:run
   ```
   Or if you're using Windows:
   ```bash
   mvnw.cmd spring-boot:run
   ```

The application will start on `http://localhost:8080`
* `http://localhost:8080/test`
* `http://localhost:8080/testList`

## Project Features

- Spring Boot Web application with REST endpoints
- Thymeleaf template engine for server-side rendering
- Spring Boot DevTools for development convenience
- Maven for dependency management and build automation

## Dependencies and Their Usage

### Spring Web (`spring-boot-starter-web`)
This dependency provides the core web functionality:
- Enables the creation of web applications using Spring MVC
- Used in `MainController.java` through annotations:
  ```java
  @Controller          // Marks the class as a web controller
  @GetMapping("test")  // Maps HTTP GET requests to specific methods
  @PostMapping("testForm") // Maps HTTP POST requests to specific methods
  ```
- Provides the `Model` class for passing data to views:
  ```java
  model.addAttribute("number", number);
  model.addAttribute("firstName", name);
  ```
- Handles HTTP request/response cycle and servlet container integration

### Thymeleaf (`spring-boot-starter-thymeleaf`)
The template engine used for server-side rendering:
- Used in HTML templates (`test.html`, `testList.html`) with Thymeleaf namespace:
  ```html
  <html xmlns:th="http://www.thymeleaf.org">
  ```
- Key Thymeleaf features used in the project:
  - Variable expressions: `${variable}` for displaying data
    ```html
    <span th:text="${number}"></span>
    ```
  - Iteration: `th:each` for looping through collections
    ```html
    <p th:each="number : ${numberList}">
    ```
  - Conditional rendering: `th:switch` and `th:case`
    ```html
    <div th:switch="${aString}">
        <p th:case="differentCase">A different case</p>
        <p th:case="*">The default case</p>
    </div>
    ```
- Provides natural templating that allows for static preview of templates

### Spring Boot DevTools (`spring-boot-devtools`)
Enhances the development experience:
- Automatic application restart when files change
  - Detects changes in classpath resources
  - Triggers application restart
  - Excludes certain resources from triggering restart (like static resources)
- Live reload for browser updates
  - Automatically refreshes the browser when templates change
  - Works with the browser's live reload plugin
- Enhanced development experience
  - Provides better error messages
  - Includes development-time configuration
  - Enables remote debugging support

## How It Works

### Component Interaction

The application follows the MVC (Model-View-Controller) pattern:

1. **Controller Layer** (`MainController.java`)
   - Handles HTTP requests and manages application logic
   - Contains several endpoints:
     - `/test`: Displays a simple page with a number and name
     - `/testForm`: Handles form submissions to update the name and number
     - `/testList`: Displays a list of numbers
     - `/testConditional`: Demonstrates conditional rendering

2. **View Layer** (Thymeleaf Templates)
   - `test.html`: Displays and allows editing of name and number
   - `testList.html`: Shows a list of numbers and conditional content
   - Uses Thymeleaf's template engine for dynamic content rendering

3. **Data Flow**
   - Controllers use the `Model` object to pass data to views
   - Views use Thymeleaf expressions (`${variable}`) to display data
   - Form submissions are handled via POST requests
   - State is maintained in controller variables (name and number)

### Key Features Implementation

1. **Form Handling**
   ```java
   @PostMapping("testForm")
   public String testForm(HttpServletRequest request) {
       name = request.getParameter("formFirstName");
       number = Integer.parseInt(request.getParameter("formNumber"));
       return "redirect:/test";
   }
   ```
   - Processes form submissions
   - Updates controller state
   - Redirects back to the test page

2. **List Display**
   ```java
   @GetMapping("testList") 
   public String testList(Model model) {
       List<Integer> numbers = new ArrayList<>();
       numbers.add(0);
       numbers.add(10);
       numbers.add(6);
       numbers.add(35);
       model.addAttribute("numberList", numbers);
       return "testList";
   }
   ```
   - Creates and populates a list
   - Passes it to the view via the Model
   - Thymeleaf iterates over the list to display items

3. **Template Rendering**
   ```html
   <p th:each="number : ${numberList}">
       <span th:text="${number}"> </span>
   </p>
   ```
   - Uses Thymeleaf's `th:each` for iteration
   - `th:text` for displaying dynamic content
   - Supports conditional rendering with `th:switch` and `th:case`

## Development

The project uses Spring Boot DevTools which provides:
- Automatic application restart when files change
- Live reload for browser updates
- Enhanced development experience

## Building

To build the project:
```bash
./mvnw clean install
```

This will create a runnable JAR file in the `target` directory.

## Testing

Run the tests using:
```bash
./mvnw test
```

## License

This project is licensed under the MIT License - see the LICENSE file for details. 