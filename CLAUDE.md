# CLAUDE.md

## Purpose
HotelBookingApp is a web application for hotel reservations, serving customers, hotel managers, and admins. It supports user registration/management, hotel management, hotel search by location and dates, room booking, credit-card payment (with Luhn/expiry/CVV validation; no third-party gateway), booking management, and an admin panel. Built on the Spring MVC (Model-View-Controller) pattern.

## Tech Stack
- **Backend:** Java 17, Spring Boot 3.1.1 (Spring Web MVC, Spring Data JPA, Spring Security 6.1.1, Bean Validation)
- **Frontend:** Thymeleaf (with layout dialect and Spring Security extras), Bootstrap 5.3, Bootstrap Icons, jQuery / jQuery-UI, Leaflet (maps via Nominatim geocoding)
- **Database:** MySQL (PostgreSQL driver also on classpath); JPA/Hibernate with `ddl-auto=update`
- **Build:** Maven (Spring Boot parent, Maven wrapper `./mvnw` present)
- **Other:** Lombok

## Build / Run / Test
- Build / install dependencies: `mvn install` (or `./mvnw install`)
- Run: `mvn spring-boot:run` — serves at http://localhost:8080/
- Test: `mvn test`
- Configure DB credentials in `src/main/resources/application.properties` before running (defaults: MySQL `hotel_booking` db at `localhost:3306`, user/pass `root`/`root`, auto-creates DB). A `application-dev.properties` profile also exists.

## Key Directories
- `src/main/java/edu/sabanciuniv/hotelbookingapp/`
  - `HotelBookingAppApplication.java` — Spring Boot entry point
  - `controller/` — MVC controllers (Auth, Admin, Booking, Customer, HotelManager, HotelSearch, MyAccount, CredentialReset)
  - `service/` + `service/impl/` — business logic interfaces and implementations
  - `repository/` — Spring Data JPA repositories
  - `model/` — JPA entities; `model/dto/` DTOs; `model/enums/` enums
  - `security/` — Spring Security config helpers (custom UserDetailsService, success handler)
  - `config/SecurityConfig.java` — security configuration
  - `validation/` — custom validation annotations/validators (e.g. card expiry)
  - `exception/` — global exception handler and domain exceptions
  - `initialize/TestDataInitializer.java` — seeds test data
- `src/main/resources/templates/` — Thymeleaf views (admin, booking, customer, etc.)
- `src/main/resources/` — `application.properties`, `messages.properties`
- `src/test/java/...` — tests (`HotelBookingAppApplicationTests.java`)
