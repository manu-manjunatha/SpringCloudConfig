# Spring Cloud Config Client Demo

## Run Client Application

Start the Spring Boot client application:

```bash
mvn spring-boot:run
```

---

## Call API

Invoke the API endpoint:

```bash
curl http://localhost:8081/message
```

### Output

```text
Hello from DEV profile
```

---

# Change Configuration Dynamically

Modify the Git configuration file:

```yaml
app:
  message: Updated DEV Message
```

Commit and push the changes to the Git repository.

---

# Refresh Without Restart

Enable the Spring Boot Actuator refresh endpoint.

## application.yml

```yaml
management:
  endpoints:
    web:
      exposure:
        include: refresh
```

Trigger the refresh endpoint:

```bash
curl -X POST http://localhost:8081/actuator/refresh
```

Now call the API again:

```bash
curl http://localhost:8081/message
```

### Output

```text
Updated DEV Message
```

---

# Profile Switching

Run the application using the `prod` profile:

```bash
mvn spring-boot:run -Dspring-boot.run.profiles=prod
```

The client now loads:

```text
employee-service-prod.yml
```

And runs on:

```text
9091
```

---

# Production Best Practices

## Use Git Branches

Configure the Git branch label:

```yaml
spring:
  cloud:
    config:
      label: main
```

---

## Encrypt Secrets

Use Spring Cloud Config encryption endpoints:

```text
/encrypt
/decrypt
```

Example encrypted property:

```yaml
password: "{cipher}A1B2C3..."
```

---

## Use Spring Cloud Bus

Use Spring Cloud Bus for automatic configuration refresh across all microservices.

### Dependencies

```xml
<!-- RabbitMQ -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>
```

or Kafka-based bus support.

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-kafka</artifactId>
</dependency>
```