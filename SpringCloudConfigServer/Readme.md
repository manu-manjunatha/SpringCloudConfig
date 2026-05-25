# Spring Cloud Config Server

## Run Config Server

Start the Spring Cloud Config Server using Maven:

```bash
mvn spring-boot:run
```

---

## Test the Config Server

Run the following command:

```bash
curl http://localhost:8888/employee-service/dev
curl http://localhost:8888/employee-service/prod

```

---

## Expected Response

```json
{
  "name": "employee-service",
  "profiles": [
    "dev"
  ],
  "label": null,
  "version": "206b9c43767f8e3da71ad713bfc9c54da329b2e0",
  "state": "",
  "propertySources": [
    {
      "name": "file:///Users/mmanjunatha/A_Drive/Equinix/MyPrograms/SpringCloudConfig/config-repo/employee-service-dev.yml",
      "source": {
        "server.port": 8081,
        "app.message": "Hello from DEV profile",
        "spring.datasource.url": "jdbc:mysql://localhost:3306/devdb",
        "spring.datasource.username": "devuser",
        "spring.datasource.password": "devpass"
      }
    },
    {
      "name": "file:///Users/mmanjunatha/A_Drive/Equinix/MyPrograms/SpringCloudConfig/config-repo/application.yml",
      "source": {
        "app.message": "Default message from Config Server"
      }
    }
  ]
}
```

```json
{
  "name": "employee-service",
  "profiles": [
    "prod"
  ],
  "label": null,
  "version": "206b9c43767f8e3da71ad713bfc9c54da329b2e0",
  "state": "",
  "propertySources": [
    {
      "name": "file:///Users/mmanjunatha/A_Drive/Equinix/MyPrograms/SpringCloudConfig/config-repo/employee-service-prod.yml",
      "source": {
        "server.port": 9091,
        "app.message": "Hello from PROD profile",
        "spring.datasource.url": "jdbc:mysql://prod-db:3306/proddb",
        "spring.datasource.username": "produser",
        "spring.datasource.password": "prodpass"
      }
    },
    {
      "name": "file:///Users/mmanjunatha/A_Drive/Equinix/MyPrograms/SpringCloudConfig/config-repo/application.yml",
      "source": {
        "app.message": "Default message from Config Server"
      }
    }
  ]
}
```