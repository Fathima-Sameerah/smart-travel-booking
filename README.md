## Smart Travel Booking Platform

This repository contains a distributed backend system for a smart travel booking application, built using Spring Boot 3+ and a microservices architecture. The platform is designed to be scalable and maintainable, with each service running independently and communicating through modern, recommended approaches.

Inter-service communication is handled using OpenFeign for declarative REST clients and Spring WebClient for reactive, non-blocking calls. Deprecated components such as RestTemplate are intentionally avoided. For development and testing, each microservice uses an in-memory H2 database and runs on its own dedicated port.


## Services & Ports
| Service | Port | Key Endpoint |
|---------|------|--------------|
| Booking | 8080 | POST /api/bookings |
| User | 8081 | GET /api/users/{id} |
| Flight | 8082 | GET /api/flights/{id} |
| Hotel | 8083 | GET /api/hotels/{id} |
| Payment | 8084 | POST /api/payments |
| Notification | 8085 | POST /api/notifications |

## Communication Flow
1. POST to Booking with {userId, flightId, hotelId, travelDate}.
2. Validate user (WebClient to 8081).
3. Check flight/hotel (Feign to 8082/8083).
4. Calculate cost, save PENDING.
5. Process payment (WebClient to 8084).
6. Send notification (WebClient to 8085).
7. Update CONFIRMED.

## Setup
- Java 17+, Maven, Spring Boot 3.2+.
- Run each: `cd <service> && mvn spring-boot:run`.
- H2 Console: http://localhost:<port>/h2-console.

## Testing
- Postman Collection: smart-travel-postman-collection.json.
- Screenshots: See /screenshots/ folder.

## Submission
- GitHub Repo: [https://github.com/Fathima-Sameerah/smart-travel-booking].
- Postman JSON attached.
- Screenshots of successful flow.

## Microservices and Ports

| Service Name         | Port | Main Endpoint           |
| -------------------- | ---- | ----------------------- |
| Booking Service      | 8080 | POST /api/bookings      |
| User Service         | 8081 | GET /api/users/{id}     |
| Flight Service       | 8082 | GET /api/flights/{id}   |
| Hotel Service        | 8083 | GET /api/hotels/{id}    |
| Payment Service      | 8084 | POST /api/payments      |
| Notification Service | 8085 | POST /api/notifications |

## Request Flow Overview

1. A booking request is sent to the **Booking Service** with `userId`, `flightId`, `hotelId`, and `travelDate`.
2. User details are validated by calling the **User Service** using **WebClient**.
3. Flight and hotel availability are verified via **Feign clients** connected to the Flight and Hotel services.
4. The total booking cost is calculated and stored with a **PENDING** status.
5. Payment is processed by invoking the **Payment Service** using **WebClient**.
6. A confirmation message is sent through the **Notification Service**.
7. Once all steps succeed, the booking status is updated to **CONFIRMED**.


## Environment Setup

* Java 17 or higher
* Maven
* Spring Boot version 3.2 or above

To start a service:

```bash
cd <service-name>
mvn spring-boot:run
```

The H2 database console can be accessed at:

```
http://localhost:<service-port>/h2-console
```

## Testing and Verification

* API testing is performed using a **Postman collection** named `smart-travel-postman-collection.json`.
* Screenshots demonstrating successful request flows are available in the `/screenshots` directory.

## Author
M.S.P Sameera
ICT21911

## Submission Details

* GitHub Repository: [https://github.com/Fathima-Sameerah/smart-travel-booking](https://github.com/Fathima-Sameerah/smart-travel-booking)
* Postman collection included
* Screenshots of successful interactions provided

