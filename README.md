# Book Network

## Overview

Book Network is a Spring Boot-based web application designed to facilitate book sharing and borrowing between users. It provides features for user authentication, book management, borrowing/returning books, user feedback, and security handling through JWT authentication.

## Features

- User registration and authentication
- JWT-based security
- Book management (add, update, list, archive, shareable status)
- Borrowing and returning books
- Feedback and rating system
- Email notifications for account activation
- Exception handling and logging
- Swagger API documentation
- Docker support

## Technologies Used

- **Spring Boot** - Core framework
- **Spring Security** - Authentication and authorization
- **Spring Data JPA** - Database interactions
- **JWT** - Authentication mechanism
- **H2/PostgreSQL** - Database support
- **Thymeleaf** - Email templating
- **Lombok** - Reducing boilerplate code
- **Docker** - Containerization

## Installation & Setup

### Prerequisites

- Java 17+
- Maven
- PostgreSQL (or H2 for in-memory usage)
- Docker (optional, for containerized deployment)

### Running Locally

1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/book-network.git
   cd book-network
   ```
2. Update the application properties in `application.yml` (e.g., database settings, JWT secret, mail configuration).
3. Build the project:
   ```sh
   mvn clean install
   ```
4. Run the application:
   ```sh
   mvn spring-boot:run
   ```
5. The API will be available at `http://localhost:8080`.

### Running with Docker

1. Ensure Docker is installed.
2. Run the application with:
   ```sh
   docker-compose up --build
   ```

## Code Explanation

### Authentication Module

- `AuthenticationController.java`: Handles user registration, login, and account activation.
- `AuthenticationService.java`: Manages user authentication, JWT token generation, and account activation via email.
- `JwtService.java`: Handles JWT token generation, validation, and extraction.

### Book Management

- `BookController.java`: Provides APIs to add, retrieve, update, borrow, and return books.
- `BookService.java`: Implements business logic for book management, including book borrowing rules.
- `Book.java`: Represents a book entity, including metadata like title, author, ISBN, and ownership.

### Security

- `SecurityConfig.java`: Configures Spring Security and JWT authentication filters.
- `JwtFilter.java`: Filters incoming requests to validate JWT tokens.
- `UserDetailsServiceImpl.java`: Loads user details from the database for authentication.

### Feedback System

- `FeedbackController.java`: Handles submission and retrieval of book feedback.
- `FeedbackService.java`: Implements logic for storing and fetching feedback.
- `Feedback.java`: Represents user feedback with ratings and comments.

### Global Exception Handling

- `GlobalExceptionHandler.java`: Catches and handles application-wide exceptions.
- `OperationNotPermittedException.java`: Custom exception for restricted operations.

## API Endpoints

### Authentication (`/auth`)

- `POST /register` - Register a new user
- `POST /authenticate` - Authenticate and receive JWT
- `GET /activate-account` - Activate user account via email link

### Books (`/books`)

- `POST /` - Add a new book
- `GET /{book-id}` - Get details of a book
- `GET /` - List available books
- `POST /borrow/{book-id}` - Borrow a book
- `PATCH /borrow/return/{book-id}` - Return a borrowed book

### Feedback (`/feedbacks`)

- `POST /` - Add feedback to a book
- `GET /book/{book-id}` - List feedback for a book

## Security

- Uses JWT authentication
- Secure endpoints require a valid token
- Role-based access control (`ROLE_USER`, `ROLE_ADMIN`)
