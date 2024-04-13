# How to run Spring Boot application in a Docker container that connects to a PostgreSQL database
We need to follow these general steps:

1. **Dockerize your Spring Boot application**:
   - Create a Dockerfile in the root directory of your Spring Boot project.
   - Build the Docker image using the Dockerfile.

2. **Set up PostgreSQL container**:
   - Run a PostgreSQL Docker container or use an existing PostgreSQL container. Make sure you have the necessary credentials and database created.

3. **Configure Spring Boot application**:
   - Configure your Spring Boot application to connect to the PostgreSQL database. You can do this by specifying the database connection properties in the `application.properties` or `application.yml` file.

4. **Build your Spring Boot application**:
   - Build your Spring Boot application, either using Maven or Gradle.

5. **Run the Docker container**:
   - Run the Docker container with your Spring Boot application image. Make sure to link it to the PostgreSQL container or provide environment variables with the PostgreSQL connection details.

Here's a simplified example to illustrate these steps:

**Dockerfile**:
```Dockerfile
# Use the official OpenJDK image as a parent image
FROM openjdk:11-jre-slim

# Set the working directory in the container
WORKDIR /app

# Copy the packaged Spring Boot application JAR file into the container
COPY target/my-application.jar /app

# Specify the command to run your Spring Boot application
CMD ["java", "-jar", "my-application.jar"]
```

**application.properties**:
```properties
spring.datasource.url=jdbc:postgresql://postgres-container:5432/my_database
spring.datasource.username=my_username
spring.datasource.password=my_password
```

**Building and running the Docker container**:
```bash
# Build the Docker image
docker build -t my-application .

# Run the Docker container, linking it to the PostgreSQL container
docker run -d --name my-application-container --link postgres-container -p 8080:8080 my-application
```

In this example:
- Replace `my-application.jar` with the name of your Spring Boot application JAR file.
- Replace `my_database`, `my_username`, and `my_password` with your PostgreSQL database name, username, and password respectively.
- Ensure that `postgres-container` matches the name of your PostgreSQL container.

This is a basic example to get you started. Depending on your specific requirements and environment, you may need to adjust the configurations and Docker setup accordingly. Additionally, consider using Docker Compose for managing multi-container Docker applications more easily.
