# --- ETAPA 1: Compilación (Build con Maven estándar) ---
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app

# Entramos y copiamos desde la subcarpeta correcta de Despachos
COPY Springboot-API-REST-DESPACHO/pom.xml .
RUN mvn dependency:go-offline -B

COPY Springboot-API-REST-DESPACHO/src ./src
RUN mvn clean package -DskipTests

# --- ETAPA 2: Ejecución ---
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Requisito Pauta: Usuario no-root
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8081

CMD ["java", "-jar", "app.jar"]