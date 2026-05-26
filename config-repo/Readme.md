# Create Config Repository

Spring Cloud Config Server uses a centralized repository to manage configuration files for microservices.

The repository can be:
- A Git repository (recommended)
- A local filesystem repository (native mode)

When using the `git` backend, the folder **must not be just a normal directory**.

It must be a valid Git repository containing a hidden `.git` folder.

---

# Why Git Repository is Required

Spring Cloud Config Server internally uses **JGit** to:
- read configuration files
- manage versions
- track changes
- refresh configurations

Because of this, the configured folder must contain:

```text
.git
```

If `.git` is missing, Spring throws:

```text
java.lang.IllegalStateException: No .git at ...
```

This means:
- Spring expected a Git repository
- But found only a regular folder

---

# Normal Directory vs Git Repository

## Normal Directory

A normal folder only contains files.

Example:

```text
config-repo/
 ├── application.yml
 ├── employee-service-dev.yml
 └── employee-service-prod.yml
```

This is NOT sufficient for Git mode.

---

## Git Repository

A Git repository contains:
- configuration files
- `.git` metadata folder

Example:

```text
config-repo/
 ├── .git/
 ├── application.yml
 ├── employee-service-dev.yml
 └── employee-service-prod.yml
```

The `.git` folder stores:
- commit history
- branches
- repository metadata
- version tracking information

---

# Create a Git Repository

## Step 1 — Create Repository Folder

```bash
mkdir config-repo
cd config-repo
```

---

## Step 2 — Initialize Git Repository

```bash
git init
```

This command creates the hidden `.git` folder.

After initialization:

```text
config-repo/
 ├── .git/
```

Now the folder becomes a valid Git repository.

---

# Add Configuration Files

## Global Configuration

### `application.yml`

Applied to all services.

```yaml
app:
  message: Default message from Config Server
```

---

# Environment-Specific Configuration

## `employee-service-dev.yml`

Used when the `dev` profile is active.

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

## `employee-service-prod.yml`

Used when the `prod` profile is active.

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

# Repository Structure

After adding files:

```text
config-repo/
 ├── .git/
 ├── application.yml
 ├── employee-service-dev.yml
 └── employee-service-prod.yml
```

---

# Commit the Repository

## Stage Files

```bash
git add .
```

---

## Commit Files

```bash
git commit -m "Initial config"
```

This saves the configuration files into Git history.

---

# Verify Git Repository

Run:

```bash
git status
```

Expected output:

```text
On branch master
nothing to commit, working tree clean
```

This confirms:
- Git repository is initialized correctly
- Config files are committed successfully

---

# Spring Cloud Config Server Configuration

Example Config Server setup:

```yaml
server:
  port: 8888

spring:
  application:
    name: spring-cloud-config-server

  cloud:
    config:
      server:
        git:
          uri: file:///path/to/config-repo
```

---

# Access Configuration

URL format:

```text
http://localhost:8888/{application}/{profile}
```

Example:

```text
http://localhost:8888/employee-service/dev
```

---

# Important Notes

## Git Mode

Requires:
- valid Git repository
- `.git` folder
- committed files

---

## Native Mode

If you do not want Git:

```yaml
spring:
  profiles:
    active: native

  cloud:
    config:
      server:
        native:
          search-locations: file:///path/to/config-repo
```

In native mode:
- normal folders are allowed
- `.git` is not required

---

# Summary

Spring Cloud Config Server in Git mode requires a valid Git repository.

A normal folder is not enough because Spring internally uses JGit for repository operations.

To make the folder valid:
1. Create folder
2. Run `git init`
3. Add configuration files
4. Commit files

This creates the `.git` folder required by Spring Cloud Config Server.