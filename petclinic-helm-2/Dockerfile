# stage1
FROM maven:latest AS BUILDER
WORKDIR /app
COPY . .
RUN mvn package -DskipTests

# stage2
FROM openjdk:8-jre-alpine
EXPOSE 8080
WORKDIR /petclinic
COPY --from=BUILDER /app/target/*.jar ./majd-petclinic.jar
CMD java -jar majd-petclinic.jar --spring.config.location=/mnt/application-mysql.properties


