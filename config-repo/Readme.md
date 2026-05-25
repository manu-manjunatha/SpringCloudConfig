# Create Config Repository

## Create a Git Repository

```bash
mkdir config-repo
cd config-repo
git init
```

---

## Add Configuration Files

### `application.yml`

```yaml
app:
  message: Default message from Config Server
```

---

### `employee-service-dev.yml`

```yaml
server:
  port: 8081

app:
  message: Hello from DEV profile

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/devdb
    username: devuser
    password: devpass
```

---

### `employee-service-prod.yml`

```yaml
server:
  port: 9091

app:
  message: Hello from PROD profile

spring:
  datasource:
    url: jdbc:mysql://prod-db:3306/proddb
    username: produser
    password: prodpass
```

---

## Commit the Repository

```bash
git add .
git commit -m "Initial config"
```